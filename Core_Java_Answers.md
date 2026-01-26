# Core Java Interview Questions & Answers (Deep Dive)

## 1. What is a HashCode Contract?
**Detailed Explanation:**
The contract between `equals()` and `hashCode()` is fundamental to the correct working of hash-based collections (`HashMap`, `HashSet`, `Hashtable`).
contracts defined in `java.lang.Object`:
1.  **Consistency:** Whenever `hashCode()` is invoked on the same object more than once during an execution, it must return the same integer, provided no information used in `equals` comparisons is modified.
2.  **Equality implies Identical Hash:** If `obj1.equals(obj2)` is `true`, then `obj1.hashCode()` MUST be equal to `obj2.hashCode()`.
3.  **Inequality does NOT imply Distinct Hash (Collision):** If `obj1.equals(obj2)` is `false`, it is NOT required that `hashCode()` be different. However, distinct hash codes for unequal objects behave better for performance.

**Violation Consequences:**
If you override `equals` but not `hashCode`, two logically equal objects (e.g., two `Person("John")` objects) will have different hash codes (derived from memory address). If you put one in a `HashMap`, you won't be able to retrieve it using the other, because the map looks in the wrong "bucket".

**Example:**
```java
public class Person {
    private String name;
    private int id;

    // ... constructors ...

    @Override
    public boolean equals(Object o) {
        if (this == o) return true; // Reference check
        if (o == null || getClass() != o.getClass()) return false; // Class check
        Person person = (Person) o;
        return id == person.id && Objects.equals(name, person.name);
    }

    @Override
    public int hashCode() {
        // Generates hash based on same fields used in equals
        return Objects.hash(name, id);
    }
}
```

## 2. What is ThreadPool in Java?
**Detailed Explanation:**
Creating a thread in Java maps to an OS-level thread, which is an expensive operation (allocation of stack memory, OS scheduling overhead). A **ThreadPool** manages a pool of worker threads.
- **Lifecycle:** Threads are created once and kept alive. They pick tasks from a **BlockingQueue**, execute them, and go back to waiting.
- **Core Pool Size:** Minimum threads to keep alive.
- **Max Pool Size:** Maximum threads allowed if the queue is full.
- **Keep Alive Time:** Time generic threads wait for tasks before terminating (if count > core size).

**Internal Working (`ThreadPoolExecutor`):**
1.  New task submitted.
2.  If `runningThreads < corePoolSize`, create new thread.
3.  Else, add task to `Queue`.
4.  If `Queue` is full and `runningThreads < maxPoolSize`, create new thread.
5.  If `Queue` full and `runningThreads == maxPoolSize`, reject task (Recall handler: Abort, CallerRuns, etc.).

**Example:**
```java
// Creates a pool with 2 fixed threads
ExecutorService executor = Executors.newFixedThreadPool(2);

for (int i = 0; i < 5; i++) {
    executor.submit(() -> {
        System.out.println("Processing by " + Thread.currentThread().getName());
        try { Thread.sleep(1000); } catch (InterruptedException e) {}
    });
}
executor.shutdown(); // Stops accepting new tasks
```

## 3. Working of ConcurrentHashMap
**Detailed Explanation:**
`ConcurrentHashMap` allows concurrent read and thread-safe update operations without locking the entire map.

**Java 7 Architecture (Legacy):**
- Used **Segment Stripping**. The map was divided into 16 Segments.
- Each Segment acted like a separate HashMap with its own lock.
- Concurrency Level = 16 (16 threads could write simultaneously).

**Java 8+ Architecture (Current):**
- **No Segments:** Uses a single array `Node<K,V>[] table`.
- **Read (`get`):** Non-blocking. Uses `volatile` reads. Very fast.
- **Write (`put`):** 
    1.  Calculates hash and finds index.
    2.  If the bucket is empty (`null`), it uses **CAS (Compare-And-Swap)** to insert the new node. This is lock-free.
    3.  If the bucket is non-empty, it synchronizes **ONLY on the head node** of that specific bucket (using `synchronized(node)`).
    4.  If the bucket is a `TreeBin` (Red-Black Tree), it uses tree locking logic.
    5.  **Size Calculation:** Uses `LongAdder` logic (baseCount + counterCells) to avoid contention on a single size variable.

**Key Difference from `Collections.synchronizedMap`:**
- `SynchronizedMap` wraps methods in `synchronized(this)`, locking the *entire* map for every operation (read or write). `ConcurrentHashMap` locks only at the finest granularity possible (bucket head).

## 4. Difference between HashSet and HashMap
**Internal Deep Dive:**
A `HashSet` is basically a `HashMap` where:
- The element you add is stored as the **Key**.
- The **Value** is a static dummy object called `PRESENT` (`new Object()`).
- Because HashMap keys must be unique, HashSet guarantees uniqueness.

| Feature | HashMap | HashSet |
| :--- | :--- | :--- |
| **Internals** | Uses `Node<K,V>` array. | Uses a `HashMap<E,Object>` instance internally. |
| **Method Signature** | `V put(K key, V value)` returns previous value. | `boolean add(E e)` returns true if added. |
| **Nulls** | 1 null key, multiple null values. | 1 null element. |
| **Iteration** | Uses `entrySet()`, `keySet()`. | Uses `iterator()`. |

## 5. What is a Synchronized Map?
**Usage & Context:**
- Created via `Collections.synchronizedMap(new HashMap<>())`.
- **Mechanism:** It wraps the underlying map. Every method (`get`, `put`, `size`) is wrapped in a `synchronized` block on a mutex (usually the map itself).
- **Iteration Risk:** Even though individual methods are safe, iterating over a `SynchronizedMap` is **NOT** thread-safe internally. You must manually synchronize the block:
  ```java
  Map<String, String> syncMap = Collections.synchronizedMap(new HashMap<>());
  synchronized (syncMap) { // Must lock during iteration
      for (String key : syncMap.keySet()) { ... }
  }
  ```

## 6. Contrast between hashCode() and equals()
**Refined:**
- `equals()`: Defines **logical equality**. By default (Object class), it uses `==` (reference equality), meaning two separate objects in memory are never equal. We override it to compare content (e.g., comparing `String` content).
- `hashCode()`: A native integer value. Default is derived from memory address.
- **Crucial Link:** They work together for **Hash-based collections**. If you put an object in a HashMap, it first hashes the key to find the bucket. Then it iterates the bucket and uses `equals()` to find the exact key. If `hashCode` is wrong, it looks in the wrong bucket. If `equals` is wrong, it doesn't find the key in the right bucket.

## 7. Java 8 Features (Deep Dive)
**1. Lambda Expressions:**
Enables functional programming. Removes boilerplate anonymous inner classes.
```java
// Old
new Thread(new Runnable() { public void run() { System.out.println("Run"); } }).start();
// Java 8
new Thread(() -> System.out.println("Run")).start();
```

**2. Stream API:**
- **Pipeline:** Source -> Intermediate Ops (Lazy) -> Terminal Op (Eager).
- **Parallel Stream:** Uses `ForkJoinPool.commonPool()` to split tasks across CPU cores.
- **Example:**
  ```java
  List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");
  List<String> result = names.stream()
      .filter(name -> name.length() > 3) // Intermediate
      .map(String::toUpperCase) // Intermediate
      .sorted() // Intermediate
      .collect(Collectors.toList()); // Terminal
  ```

**3. Optional Class:**
A container object which may or may not contain a non-null value. Prevents explicit `null` checks.
```java
Optional<String> opt = Optional.ofNullable(getName());
String result = opt.orElse("Unknown");
// or
opt.ifPresent(name -> System.out.println(name));
```

**4. Default Methods:**
Allows adding methods to interfaces without breaking implementing classes.
```java
interface Vehicle {
    void start();
    default void stop() { System.out.println("Vehicle stopped"); }
}
```

## 8. HashMap vs LinkedHashMap (Internals)
- **HashMap:** Nodes are `Node<K,V> next`. Order is chaotic (depends on Hash).
- **LinkedHashMap:** Nodes are `Entry<K,V> before, after` (extends HashMap.Node). It maintains a **Doubly Linked List** running through all entries.
- **Access Order:** `LinkedHashMap` has a constructor flag `accessOrder`. If `true`, accessing an element (`get`) moves it to the end of the list. This is used to implement **LRU Caches**.

## 9. Comparable vs Comparator
**Detailed Scenario:**
You have a class `Employee`.
- **Comparable (`implements Comparable<Employee>`):** You hardcode the "Natural Ordering" (e.g., sort by ID). This is the default sort.
  ```java
  public int compareTo(Employee e) { return this.id - e.id; }
  ```
- **Comparator:** You need special sorting requirements later (e.g., sort by Salary, then Name). You create separate classes or lambdas.
  ```java
  Comparator<Employee> salaryComp = (e1, e2) -> Double.compare(e1.salary, e2.salary);
  Collections.sort(employees, salaryComp);
  ```

## 10. Internal Working of HashMap (Deep Dive)
**Structure:** Array of Buckets `Node<K,V>[] table`.
**Put Operation Flow:**
1.  **Hash:** Compute `hash(key)`. `Key.hashCode() ^ (h >>> 16)` (XOR with upper bits to spread entropy).
2.  **Index:** `i = (n - 1) & hash`. (Bitwise mask is faster than modulo).
3.  **Collision Check:** Check `table[i]`.
    - If `null`: Insert new Node.
    - If `not null`: 
        - Check first node's hash and key. If match, replace value.
        - If node is `TreeNode`: Put into Red-Black Tree (O(log n)).
        - If node is `Node` (LinkedList): Traverse list. Insert at end. If matches, replace.
4.  **Treeify:** If LinkedList length > 8 (TREEIFY_THRESHOLD) AND Array capacity > 64, convert list to Red-Black Tree.
5.  **Resize:** If `size > capacity * loadFactor` (default 0.75), double the array size. Rehash all nodes to new positions.

## 11. Multithreading: Wait vs Notify vs Sleep
- **`wait()`:** Releases the lock and goes to waiting state. Must only be called inside `synchronized` context.
- **`notify()` / `notifyAll()`:** Wakes up waiting thread(s). They compete for the lock again.
- **`sleep()`:** Keeps the lock. Just pauses execution.

**Producer-Consumer Example:**
```java
class SharedBuffer {
    private LinkedList<Integer> list = new LinkedList<>();
    
    public synchronized void produce() throws InterruptedException {
        while (list.size() == 2) wait(); // Wait if full
        list.add(1);
        notify(); // Notify consumer
    }
    
    public synchronized void consume() throws InterruptedException {
        while (list.isEmpty()) wait(); // Wait if empty
        list.removeFirst();
        notify(); // Notify producer
    }
}
```

## 12. String vs StringBuilder vs StringBuffer (Memory)
- **String:** Stored in String Pool (if literal). Modifications create new objects. High GC pressure if concatenated in loops.
- **StringBuilder:** Uses `char[]` array. Resizes (creates new larger array, copies content) when capacity reached. Not thread-safe (fastest).
- **StringBuffer:** Same as Builder but all methods have `synchronized` keyword.

## 13. Java Memory Model (JVM)
- **Heap Phase:** Stores Objects / Class Instances. Shared by all threads. Split into:
    - **Young Gen:** Eden Space (new objects), Survivor S0/S1. GC is "Minor GC".
    - **Old Gen:** Long-lived objects. GC is "Major/Full GC".
- **Stack:** Per-Thread. Stores primitive variables and object references (pointers) for the current method execution.
- **Metaspace (Java 8+):** Replaced PermGen. Stores Class Metadata, Static variables, Bytecode. Uses Native Memory (OS memory), not Heap.

## 14. Fail-Fast vs Fail-Safe
- **Fail-Fast (ArrayList, HashMap):**
    - Uses a `modCount` variable.
    - Iterator stores `expectedModCount = modCount` at creation.
    - On `next()`, checks if `modCount != expectedModCount`. If yes, throws `ConcurrentModificationException`.
- **Fail-Safe (ConcurrentHashMap, CopyOnWriteArrayList):**
    - `CopyOnWriteArrayList`: Iterates over a snapshot array. Writes create a new array copy.
    - `ConcurrentHashMap`: Weakly consistent. Reflects the state of the map at some point. Guarantees no Exception, but might not see latest updates.
