## 71. Internal working of HashMap.

**Answer:**
`HashMap` in Java works on the principle of **hashing**.
1.  **put(K, V):**
    *   Calculates `hash(K)`.
    *   Finds the bucket index: `index = hash & (n-1)`.
    *   If bucket is empty, adds a Node.
    *   If bucket is occupied (Collision), it traverses the contents (LinkedList or Red-Black Tree).
    *   If key exists (via `equals()`), it updates the value. If not, it appends the new node.
2.  **get(K):**
    *   Finds bucket index.
    *   Traverses the list/tree comparing keys using `equals()`.
    *   Returns value if found, else `null`.
*   **Java 8 Improvement:** If a bucket has > 8 nodes, the LinkedList converts to a **Red-Black Tree** (O(log n) performance) instead of O(n).

**Code Snippet:**
```java
HashMap<String, Integer> map = new HashMap<>(); // Initial capacity 16
map.put("Key", 1); // Hash -> Index -> Store Node
```

---

## 72. What is load factor?

**Answer:**
The **Load Factor** is a measure that decides when to increase the capacity of the HashMap to maintain constant-time performance.
*   **Default:** `0.75` (75%).
*   **Threshold:** When the number of entries > `capacity * loadFactor`, the map is resized.
*   **Example:** For default capacity 16, resizing happens at `16 * 0.75 = 12` entries.
*   **Trade-off:**
    *   Higher Load Factor = Fewer resizes (saves space) but more collisions (slower lookups).
    *   Lower Load Factor = Frequent resizes (wastes space) but fewer collisions (faster lookups).

---

## 73. What is rehashing?

**Answer:**
**Rehashing** is the process of re-calculating the hash code of already stored entries (Key-Value pairs) and moving them to a new, larger hash map.
*   It happens when the map crosses the **Threshold**.
*   The capacity is usually **doubled** (e.g., 16 -> 32).
*   It is computationally expensive because every single element must be re-inserted into the new array buckets.

**Code Snippet:**
```java
// Conceptual Logic
if (size > threshold) {
    Node[] newTable = new Node[oldCapacity * 2];
    for (Node node : oldTable) {
        // Re-calculate index for newTable size
        // Move node to new bucket
    }
}
```

---

## 74. HashMap vs ConcurrentHashMap.

**Answer:**
*   **`HashMap`:** Not thread-safe. Fast. Allows 1 null key. Use in single-threaded apps.
*   **`ConcurrentHashMap`:** Thread-safe.
    *   **Locking:** Uses **Bucket-Level Locking** (or CAS in Java 8+) rather than locking the whole map (like Hashtable). This allows concurrent reads and writes to different segments.
    *   **Nulls:** Does **not** allow null keys or null values.
    *   **Performance:** Higher throughput in multi-threaded environments.

**Code Snippet:**
```java
Map<String, String> chm = new ConcurrentHashMap<>();
// Thread 1 puts "A"
// Thread 2 puts "B" -> Can happen simultaneously if hash("A") != hash("B")
```

---

## 75. HashSet vs TreeSet.

**Answer:**
*   **`HashSet`:**
    *   Backing: Uses `HashMap` internally.
    *   Order: **Unordered**. No guarantee of iteration order.
    *   Performance: O(1) for add/remove/contains.
    *   Null: Allows 1 null.
*   **`TreeSet`:**
    *   Backing: Uses `TreeMap` (Red-Black Tree) internally.
    *   Order: **Sorted** (Natural ordering or custom Comparator).
    *   Performance: O(log n).
    *   Null: Does **not** allow null (throws NPE).

**Code Snippet:**
```java
Set<String> hashSet = new HashSet<>();
hashSet.add("B"); hashSet.add("A"); // Order unpredictable: [A, B] or [B, A]

Set<String> treeSet = new TreeSet<>();
treeSet.add("B"); treeSet.add("A"); // Always sorted: [A, B]
```

---

## 76. ArrayList vs LinkedList.

**Answer:**
*   **`ArrayList`:** Dynamic Array.
    *   Access: **O(1)** (Direct index).
    *   Insert/Delete: **O(n)** (Shifting required).
    *   Usage: Read-heavy applications.
*   **`LinkedList`:** Doubly Linked List.
    *   Access: **O(n)** (Traversal required).
    *   Insert/Delete: **O(1)** (Pointer change, if node is known).
    *   Usage: Frequent insertion/deletion in the middle.

---

## 77. Vector vs ArrayList.

**Answer:**
Both implement `List` and use dynamic arrays.
*   **`Vector`:**
    *   **Synchronized** (Thread-safe). Every method is synchronized.
    *   **Slow** due to locking overhead.
    *   Legacy class (since Java 1.0).
    *   Growth: Doubles size (100% increase).
*   **`ArrayList`:**
    *   **Not Synchronized**.
    *   **Fast**.
    *   Standard choice.
    *   Growth: Increases by 50%.

**Code Snippet:**
```java
List<String> v = new Vector<>(); // Thread-safe, slow
List<String> al = new ArrayList<>(); // Not thread-safe, fast (Default choice)
```

---

## 78. What is fail-fast vs fail-safe?

**Answer:**
*   **Fail-Fast:** Iterators that throw `ConcurrentModificationException` immediately if the underlying collection is modified structurally while iterating.
    *   Examples: `ArrayList`, `HashMap`, `HashSet` iterators.
    *   Mechanism: Checks `modCount` flag.
*   **Fail-Safe:** Iterators that do **not** throw exception if modified. They work on a clone or snapshot (Weakly Consistent).
    *   Examples: `ConcurrentHashMap`, `CopyOnWriteArrayList` iterators.

---

## 79. What is Iterator vs ListIterator?

**Answer:**
*   **`Iterator`:**
    *   Traverses: **Forward only**.
    *   Works with: `List`, `Set`, `Queue` (Any Collection).
    *   Methods: `hasNext()`, `next()`, `remove()`.
*   **`ListIterator`:**
    *   Traverses: **Bidirectional** (Forward and Backward).
    *   Works with: **`List` only**.
    *   Methods: `hasPrevious()`, `previous()`, `add()`, `set()`, `nextIndex()`.

**Code Snippet:**
```java
List<String> list = Arrays.asList("A", "B");
ListIterator<String> lit = list.listIterator();
while(lit.hasNext()) System.out.println(lit.next()); // Fwd
while(lit.hasPrevious()) System.out.println(lit.previous()); // Bwd
```

---

## 80. What is Comparable vs Comparator?

**Answer:**
Used for sorting objects.
*   **`Comparable` (Natural Order):**
    *   Interface: `java.lang.Comparable`.
    *   Method: `compareTo(Object o)`.
    *   Modification: Must modify the class itself. "This object compared to that."
    *   Usage: Default sort (e.g., `Collections.sort(list)`).
*   **`Comparator` (Custom Order):**
    *   Interface: `java.util.Comparator`.
    *   Method: `compare(Object o1, Object o2)`.
    *   Modification: Separate class/lambda. Does not touch original class.
    *   Usage: Multiple sorting strategies (e.g., sort by name, then by age).

**Code Snippet:**
```java
// Comparable
class Student implements Comparable<Student> {
    public int compareTo(Student s) { return this.id - s.id; }
}

// Comparator
Collections.sort(list, (s1, s2) -> s1.name.compareTo(s2.name));
```

---

## 81. What is PriorityQueue?

**Answer:**
`PriorityQueue` is a Queue implementation that processes elements based on their **Priority** rather than FIFO (First-In-First-Out).
*   **Ordering:** Elements are ordered according to their **Natural Ordering** (Comparable) or by a **Comparator** provided at construction time.
*   **Head:** The head of the queue is always the **least** element (Min-Heap by default).
*   **Nulls:** Does not allow null elements.
*   **Performance:** O(log n) for enqueueing (offer) and dequeueing (poll).

**Code Snippet:**
```java
// Default: Min-Heap (Smallest number first)
Queue<Integer> pq = new PriorityQueue<>();
pq.add(10);
pq.add(5);
pq.add(20);

System.out.println(pq.poll()); // Output: 5
System.out.println(pq.poll()); // Output: 10
```

---

## 82. What is BlockingQueue?

**Answer:**
`BlockingQueue` is an interface in `java.util.concurrent` that supports operations that wait for the queue to become non-empty when retrieving an element, and wait for space to become available when storing an element.
*   **Usage:** Essential for **Producer-Consumer** problems.
*   **Implementations:** `ArrayBlockingQueue`, `LinkedBlockingQueue`, `PriorityBlockingQueue`.
*   **Key Methods:** `put()` (blocks if full), `take()` (blocks if empty).

**Code Snippet:**
```java
BlockingQueue<String> queue = new ArrayBlockingQueue<>(10);

// Producer Thread
new Thread(() -> {
    try { queue.put("Job 1"); } catch (InterruptedException e) {}
}).start();

// Consumer Thread
new Thread(() -> {
    try { String job = queue.take(); } catch (InterruptedException e) {}
}).start();
```

---

## 83. What is EnumMap?

**Answer:**
`EnumMap` is a specialized `Map` implementation for use with **enum type keys**.
*   **Internals:** It is represented internally as an **Array**. Since ordinal values of Enums are known (0, 1, 2...), it uses the ordinal as the array index.
*   **Performance:** Extremely fast and compact. Faster than `HashMap`.
*   **Nulls:** Does not allow null keys.

**Code Snippet:**
```java
enum Day { MON, TUE, WED }

EnumMap<Day, String> map = new EnumMap<>(Day.class);
map.put(Day.MON, "Work");
map.put(Day.TUE, "Sleep");
```

---

## 84. What is IdentityHashMap?

**Answer:**
`IdentityHashMap` uses **Reference Equality** (`==`) instead of Meaningful Equality (`equals()`) to compare keys.
*   **Duplication:** It considers two objects distinct if they are different objects in memory (`k1 != k2`), even if `k1.equals(k2)` returns true.
*   **Usage:** Rare. Used for topology preservation (graph traversal), serialization, or handling proxy objects.

**Code Snippet:**
```java
IdentityHashMap<String, String> map = new IdentityHashMap<>();
String s1 = new String("Ky");
String s2 = new String("Ky");

map.put(s1, "Value1");
map.put(s2, "Value2");

System.out.println(map.size()); // Output: 2 (Because s1 != s2 in memory)
// In HashMap, size would be 1
```

---

## 85. What is WeakHashMap?

**Answer:**
`WeakHashMap` is a Map implementation where keys are stored as `WeakReference`.
*   **GC Behavior:** If a key is no longer referenced by any other part of the application (only strongly referenced by this map), the Garbage Collector discards the key, and the entry is automatically removed from the map.
*   **Usage:** Ideal for building **Caches** where you want execution to clear up memory automatically if keys aren't used elsewhere.

**Code Snippet:**
```java
WeakHashMap<Object, String> map = new WeakHashMap<>();
Object key = new Object();
map.put(key, "Data");

key = null; // Remove strong reference
System.gc(); // Suggest GC

// Internally, the entry "Data" will be removed eventually.
```

---

## 86. What is ConcurrentSkipListMap?

**Answer:**
`ConcurrentSkipListMap` is a thread-safe, sorted map.
*   **Structure:** Implement using a **Skip List** data structure (probabilistic alternative to balanced trees).
*   **Feature:** It is a concurrent alternative to `TreeMap`.
*   **Performance:** Expected O(log n) for insertion, removal, and search. Supports high concurrency better than synchronizing a TreeMap.

---

## 87. What is CopyOnWriteArrayList?

**Answer:**
`CopyOnWriteArrayList` is a thread-safe variant of `ArrayList`.
*   **Mechanism:** All mutative operations (`add`, `set`) are implemented by making a fresh copy of the underlying array.
*   **Usage:** Very expensive for writes, but very efficient for modification-light, read-heavy scenarios (e.g., Listener lists).
*   **Iterators:** Never throw `ConcurrentModificationException`. They iterate over the snapshot of the array taken when iterator was created.

**Code Snippet:**
```java
List<String> list = new CopyOnWriteArrayList<>();
list.add("A");

for (String s : list) {
    list.add("B"); // Allowed, no exception. 
    // Iterator sees only ["A"], future reads see ["A", "B"].
}
```

---

## 88. What is immutable collection?

**Answer:**
An Immutable Collection is a collection that cannot be modified after creation.
*   **Java 9+:** `List.of()`, `Set.of()`, `Map.of()`.
*   **Attempts to modify:** Call to `add()`, `remove()` throws `UnsupportedOperationException`.
*   **Unmodifiable vs Immutable:** `Collections.unmodifiableList(list)` returns a read-only *view*. If the backing `list` changes, the view changes. True immutable collections (like `List.of`) have no backing list to change.

**Code Snippet:**
```java
List<String> list = List.of("A", "B", "C"); // Immutable
// list.add("D"); // Throws UnsupportedOperationException
```

---

## 89. What are synchronized collections?

**Answer:**
Synchronized Collections are wrappers provided by the `Collections` class to make standard collections thread-safe.
*   **Methods:** `Collections.synchronizedList()`, `synchronizedSet()`, `synchronizedMap()`.
*   **Drawback:** They achieve thread safety by synchronizing every method (coarse-grained locking). This reduces scalability (only one thread can access the map at a time).
*   **Better Alternative:** `ConcurrentHashMap`, `CopyOnWriteArrayList`.

**Code Snippet:**
```java
List<String> fastList = new ArrayList<>();
List<String> safeList = Collections.synchronizedList(fastList);
```

---

## 90. What is Collections.unmodifiableList()?

**Answer:**
It returns an **Unmodifiable View** of the specified list.
*   **Read-Only:** You can query (get, size), but you cannot modify (add, remove) the returned list.
*   **View vs Copy:** It does **not** create a copy. It wraps the original list. If the original list is modified efficiently, the unmodifiable view reflects those changes.
*   **Usage:** Encapsulation. Exposing a list from a class without allowing external modification.

**Code Snippet:**
```java
List<String> internal = new ArrayList<>();
internal.add("Secret");

List<String> publicView = Collections.unmodifiableList(internal);
// publicView.add("Hack"); // Exception
internal.add("Leak"); // Works
System.out.println(publicView); // Output: [Secret, Leak]
```

---

## 91. What is type erasure?

**Answer:**
**Type Erasure** is a process by which the Java Compiler (javac) removes all generic type information (e.g., `<String>`, `<T>`) during compilation.
*   **Result:** The bytecode (`.class`) contains only raw types or bounded types (References become `Object` or the Bound).
*   **Purpose:** Backward compatibility with pre-Generics Java (versions before Java 5).
*   **Consequence:** Generic type information is **not available at runtime**. `List<String>` and `List<Integer>` become just `List` at runtime.

**Code Snippet:**
```java
// Compile Time
List<String> list = new ArrayList<>();
list.add("Hello");
String s = list.get(0); // Compiler inserts cast

// Runtime (Erasure)
List list = new ArrayList();
list.add("Hello");
String s = (String) list.get(0); // Explicit cast in bytecode
```

---

## 92. What are bounded types?

**Answer:**
Bounded Types allow you to restrict the types that can be used as type arguments in a parameterized type.
*   **Upper Bound (`extends`):** Accepts a type and its subclasses. `T extends Number` means T can be Integer, Double, etc.
*   **Lower Bound (`super`):** Accepts a type and its superclasses (Used with Wildcards).
*   **Multiple Bounds:** `T extends Class & Interface`.

**Code Snippet:**
```java
// T must be a subclass of Number
public <T extends Number> double add(T a, T b) {
    return a.doubleValue() + b.doubleValue();
}
```

---

## 93. What is wildcard?

**Answer:**
A Wildcard (represented by `?`) in generics represents an **Unknown Type**.
*   **Unbounded Wildcard (`<?>`):** Accepts any type. Read-only (mostly).
*   **Upper Bounded Wildcard (`<? extends T>`):** Accepts T or any subclass of T.
*   **Lower Bounded Wildcard (`<? super T>`):** Accepts T or any superclass of T.

**Code Snippet:**
```java
// Accepts List of any type
public void printList(List<?> list) { 
    for(Object elem : list) System.out.println(elem);
}
```

---

## 94. What is PECS rule?

**Answer:**
**PECS** stands for **Producer Extends, Consumer Super**. It is a mnemonic to remember which wildcard to use.
*   **Producer (`extends`):** If you need to **read** (produce) items from a generic collection, use `<? extends T>`. You cannot add to it (except null).
*   **Consumer (`super`):** If you need to **write** (consume) items into a generic collection, use `<? super T>`. You can add T and its subclasses to it.

**Code Snippet:**
```java
// Producer: Read Numbers
public void sum(List<? extends Number> list) {
    Number n = list.get(0); // OK
    // list.add(10); // COMPILE ERROR
}

// Consumer: Add Integers
public void addNumbers(List<? super Integer> list) {
    list.add(10); // OK
    // Integer i = list.get(0); // ERROR (Returns Object)
}
```

---

## 95. Why generics are invariant?

**Answer:**
Generics in Java are **Invariant**, meaning `List<String>` is **NOT** a subtype of `List<Object>`, even though `String` is a subtype of `Object`.
*   **Reason:** Type Safety. If `List<String>` were a subtype of `List<Object>`, you could assign a `List<String>` to a `List<Object>` variable and then add an `Integer` to it, creating a runtime ClassCastException when retrieving items. Array types are **covariant**, which leads to runtime errors. Generics prevent this at compile time.

**Code Snippet:**
```java
List<String> strs = new ArrayList<>();
// List<Object> objs = strs; // COMPILE ERROR!
// If allowed:
// objs.add(1); // Pollutes the String list with Integer
// String s = strs.get(0); // ClassCastException at runtime
```