# LEVEL 2: INTERMEDIATE (2-4 Years Experience)

# Advanced Core Java

# Collection Deep Dive

## 58. Contract between hashCode() and equals() methodes?

### **58. Contract Between `hashCode()` and `equals()` in Java**

In Java, **`hashCode()`** and **`equals()`** are closely related methods in the `Object` class. They are essential for **hash-based collections** like `HashMap`, `HashSet`, and `Hashtable`.

Java defines a **contract** between these two methods to ensure correct behavior of objects in hash-based collections.

---

### **🔹 1. `equals()` Method**

* Used to **compare two objects for logical equality**.
* Default implementation (in `Object`) checks **reference equality** (`==`).
* Can be **overridden** to compare object content.

**Example:**

```java
@Override
public boolean equals(Object obj) {
    if(this == obj) return true;
    if(obj == null || getClass() != obj.getClass()) return false;
    User user = (User) obj;
    return id == user.id && name.equals(user.name);
}
```

---

### **🔹 2. `hashCode()` Method**

* Returns an **integer value** representing the object in hash-based collections.
* Default implementation provides a **memory address-based hash**.
* Should be **overridden whenever `equals()` is overridden**.

**Example:**

```java
@Override
public int hashCode() {
    return Objects.hash(id, name);
}
```

---

### **🔹 3. The Contract Between `equals()` and `hashCode()`**

1. **Consistent hash code:**

   * If two objects are equal according to `equals()`, they **must have the same hash code**.
   * `obj1.equals(obj2) → obj1.hashCode() == obj2.hashCode()`

2. **Unequal objects may have different or same hash codes:**

   * If two objects are **not equal**, their hash codes **may or may not be the same**.
   * Hash collisions are allowed but should be minimized.

3. **Consistency:**

   * Multiple invocations of `hashCode()` should return the same integer **as long as object state doesn’t change**.
   * Multiple invocations of `equals()` should consistently return true/false **if object state doesn’t change**.

---

### **🔹 4. Importance in Collections**

* **HashMap / HashSet / Hashtable** use `hashCode()` to determine **bucket location**.
* Then `equals()` is used to **check actual equality** within the bucket.
* Violating the contract can cause **duplicates or incorrect retrievals**.

**Example Problem:**

```java
User u1 = new User(1, "Aditya");
User u2 = new User(1, "Aditya");

HashSet<User> set = new HashSet<>();
set.add(u1);
set.add(u2); // Will add duplicate if hashCode() not overridden
```

* If `hashCode()` is not overridden, `u1` and `u2` may go into **different buckets** → duplicate in `HashSet`.

---

### **🔹 5. Summary**

| Rule                                        | Description                                                                                      |
| ------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| **Equal objects must have same hash code**  | `u1.equals(u2) → u1.hashCode() == u2.hashCode()`                                                 |
| **Unequal objects can have same hash code** | Collisions are allowed                                                                           |
| **Consistency**                             | `hashCode()` and `equals()` must consistently return the same result during an object’s lifetime |

---

💡 **Interview Tip:**

> "Whenever you override `equals()`, you **must also override `hashCode()`** to maintain the general contract. Otherwise, objects may behave incorrectly in hash-based collections."

---

If you want, I can next explain **Difference between == and .equals() with hashCode examples**, which is often asked in interviews.

Do you want me to cover that next?

---

## 59. Explain the internal working of HashMap in Java.

### **59. Internal Working of `HashMap` in Java**

`HashMap` is a **hash-based collection** in Java that stores **key-value pairs**. It provides **constant-time performance (O(1))** for `get()` and `put()` operations in ideal cases. Understanding its **internal working** is important for performance tuning and interview questions.

---

### **🔹 1. Data Structure Used**

* Internally, a `HashMap` uses an **array of buckets**, where each bucket stores a **linked list** (Java 7) or **balanced tree (Java 8+)** of `Map.Entry` objects.
* Each **key-value pair** is stored as a `Node<K,V>` or `Entry<K,V>` object.

```java
static class Node<K,V> implements Map.Entry<K,V> {
    final int hash;
    final K key;
    V value;
    Node<K,V> next;
}
```

---

### **🔹 2. How HashMap Stores Data**

1. **Calculate hash code** of the key:

   ```java
   int hash = key.hashCode();
   ```
2. **Find bucket index** using:

   ```java
   index = hash % capacity; // capacity = size of internal array
   ```
3. **Store key-value pair**:

   * If bucket is empty → store directly.
   * If bucket already has entries → check `equals()`:

     * If key exists → update value.
     * If key does not exist → append to the bucket’s linked list (Java 7) or add to tree if list exceeds threshold (Java 8+).

---

### **🔹 3. Handling Collisions**

* **Collision** occurs when **two keys map to the same bucket**.
* Resolved using:

  * **Linked list** (before Java 8)
  * **Tree (Red-Black tree)** if bucket size exceeds 8 (Java 8+)
* This improves **lookup performance** in case of many collisions from O(n) to O(log n).

---

### **🔹 4. Resizing**

* Default **initial capacity**: 16
* **Load factor**: 0.75 (default)
* When number of entries > `capacity * loadFactor`, the `HashMap` **doubles its capacity** and **rehashes all entries** to new buckets.

---

### **🔹 5. Key Points about Keys and Values**

1. **Keys**:

   * Must override **`hashCode()` and `equals()`** for correct behavior.
   * `null` key allowed (only one).

2. **Values**:

   * Can be duplicate.
   * `null` values allowed.

---

### **🔹 6. Example: Putting Data in HashMap**

```java
HashMap<Integer, String> map = new HashMap<>();
map.put(1, "Aditya");
map.put(17, "Ramdas"); // Collides with key 1 if capacity = 16 (1 % 16 = 1, 17 % 16 = 1)
```

* Both keys map to the same bucket → stored as a **linked list or tree**.
* Lookup checks **hash first, then equals()** to find the correct entry.

---

### **🔹 7. Internal Performance**

| Operation  | Average Case | Worst Case              |
| ---------- | ------------ | ----------------------- |
| `get()`    | O(1)         | O(log n) (Java 8+ tree) |
| `put()`    | O(1)         | O(log n) (tree)         |
| `remove()` | O(1)         | O(log n)                |

> Worst case happens when many keys collide and form a tree.

---

### **🔹 8. Key Features Recap**

* Not synchronized (use `ConcurrentHashMap` for thread safety).
* Maintains **no order** (for ordered maps, use `LinkedHashMap` or `TreeMap`).
* Single `null` key allowed, multiple `null` values allowed.
* Uses **hash + equals** to ensure **unique keys**.

---

💡 **Interview Tip:**

> "HashMap uses an **array of buckets**, stores entries in **linked lists or trees**, handles collisions using chaining, and resizes dynamically. `hashCode()` and `equals()` of keys are crucial for correct behavior."

---

If you want, I can next explain **Difference between HashMap, HashTable, LinkedHashMap, and TreeMap**, which is a commonly asked interview question.

Do you want me to cover that next?

---

## 60. What happens on a HashMap collision?

### **60. What Happens on a HashMap Collision in Java**

A **collision** in a `HashMap` occurs when **two different keys produce the same hash code or map to the same bucket index**. HashMap handles collisions internally to ensure **both entries are stored and retrievable**.

---

### **🔹 1. How Collision Happens**

* HashMap calculates the **bucket index** using:

```java
index = hash(key) % capacity;
```

* If **two different keys** produce the same index → **collision occurs**.

**Example:**

```java
HashMap<Integer, String> map = new HashMap<>(16);
map.put(1, "Aditya");
map.put(17, "Ramdas"); // 1 % 16 = 1, 17 % 16 = 1 → collision
```

Both keys map to **bucket index 1**, causing a collision.

---

### **🔹 2. How Java Handles Collisions**

**Before Java 8 (Linked List Approach):**

* Each bucket stores a **linked list of entries**.
* Steps when a collision occurs:

  1. Check if the **key already exists** in the bucket using `equals()`.
  2. If **key exists**, update its value.
  3. If **key does not exist**, append the new entry to the **linked list**.

**After Java 8 (Linked List + Tree Approach):**

* Each bucket initially stores a **linked list**.
* If the **list size exceeds 8**, it is converted into a **Red-Black Tree** for faster lookup (`O(log n)` instead of `O(n)`).

---

### **🔹 3. Example: Handling Collision**

```java
HashMap<Integer, String> map = new HashMap<>();
map.put(1, "Aditya");
map.put(17, "Ramdas"); // Collision, same bucket index

System.out.println(map.get(1));  // Aditya
System.out.println(map.get(17)); // Ramdas
```

* HashMap **calculates bucket index** → both go to the same bucket.
* It traverses the **linked list or tree**, compares **hash and key using equals()**, and retrieves the correct value.

---

### **🔹 4. Key Points About Collision Handling**

1. **Chaining:** Multiple entries stored in the same bucket using **linked list or tree**.
2. **Equality Check:** After finding the bucket, HashMap uses **`equals()`** to locate the exact key.
3. **Performance:**

   * Ideal: `O(1)` for get/put.
   * Worst case (all keys in same bucket):

     * Java 7 → `O(n)` (linked list)
     * Java 8 → `O(log n)` (tree)

---

### **🔹 5. Summary**

* **Collision occurs** when two keys map to the same bucket.
* Handled using **linked list** (Java 7) or **tree after threshold** (Java 8+).
* **Key comparison using equals()** ensures the correct value is retrieved.
* Proper **hashCode() implementation** reduces collisions and improves performance.

---

💡 **Interview Tip:**

> "In case of a HashMap collision, entries are stored in the same bucket using a linked list or tree. HashMap first compares **hash codes**, then **keys using equals()** to resolve collisions."

---

If you want, I can next explain **Difference between HashMap, LinkedHashMap, and TreeMap**, which is a common follow-up question in interviews.

Do you want me to cover that next?

---

## 61. What is the load factor in HashMap?

### **61. What is Load Factor in HashMap**

The **load factor** in a `HashMap` is a measure that **controls when the HashMap should increase its capacity** (resize). It is crucial for **balancing memory usage and performance**.

---

### **🔹 1. Definition**

**Load Factor (LF)** =

[
\text{LF} = \frac{\text{Number of entries}}{\text{Number of buckets (capacity)}}
]

* It represents **how full the HashMap can get before it is resized**.
* Default load factor in Java: **0.75**

---

### **🔹 2. How It Works**

1. HashMap has an **initial capacity** (default 16).
2. When the number of entries exceeds **capacity × load factor**, the map is **resized** (capacity is doubled).
3. Resizing involves **rehashing all entries** into the new bucket array.

**Example:**

* Initial capacity = 16
* Load factor = 0.75
* Threshold = 16 × 0.75 = 12
* When the 13th entry is added, **HashMap resizes to 32 buckets**.

---

### **🔹 3. Why Load Factor Matters**

* **Low Load Factor (e.g., 0.5):**

  * Fewer collisions → faster `get()`/`put()`
  * More memory used → larger array

* **High Load Factor (e.g., 0.9):**

  * More collisions → slower performance
  * Less memory used → compact storage

* Default **0.75** is a **good trade-off** between performance and memory.

---

### **🔹 4. Example**

```java
HashMap<Integer, String> map = new HashMap<>(16, 0.75f); // initial capacity 16, load factor 0.75
```

* Threshold = 16 × 0.75 = 12
* When the 13th entry is inserted → HashMap **resizes** to 32 buckets.

---

### **🔹 5. Key Points**

1. **Capacity:** Number of buckets in HashMap (power of 2).
2. **Load Factor:** Controls when resizing happens.
3. **Threshold:** capacity × load factor → resize occurs after this.
4. **Resizing cost:** Rehashing all entries → can impact performance if frequent.

---

💡 **Interview Tip:**

> "Load factor determines how full the HashMap can get before resizing. Default is 0.75, balancing **space efficiency** and **lookup performance**."

---

If you want, I can next explain **Difference between Initial Capacity, Load Factor, and Threshold in HashMap**, which is frequently asked in interviews.

Do you want me to cover that next?

---

## 62. Difference between HashMap, LinkedHashMap, and TreeMap?

### **62. Difference Between HashMap, LinkedHashMap, and TreeMap in Java**

`HashMap`, `LinkedHashMap`, and `TreeMap` are all implementations of the **Map interface**, but they differ in **ordering, performance, and underlying data structures**.

---

### **🔹 1. HashMap**

* **Ordering:** No order guaranteed (random).
* **Nulls:** Allows **one null key** and multiple null values.
* **Performance:**

  * `get()` / `put()` → O(1) average, O(n) worst-case (collision).
* **Data Structure:** Array of **buckets** with **linked lists or trees** (Java 8+).
* **Use Case:** When **order doesn’t matter** and **fast access** is needed.

```java
HashMap<Integer, String> map = new HashMap<>();
```

---

### **🔹 2. LinkedHashMap**

* **Ordering:** Maintains **insertion order** (or access order if `accessOrder=true`).
* **Nulls:** Allows **one null key** and multiple null values.
* **Performance:** Slightly slower than HashMap due to **doubly-linked list maintenance**.

  * `get()` / `put()` → O(1) average.
* **Data Structure:** HashMap + **doubly-linked list** of entries.
* **Use Case:** When you need **predictable iteration order**.

```java
LinkedHashMap<Integer, String> map = new LinkedHashMap<>();
```

**Access Order Example:**

```java
LinkedHashMap<Integer, String> map = new LinkedHashMap<>(16, 0.75f, true);
```

* Iteration order = **order of access** → useful for **LRU cache** implementation.

---

### **🔹 3. TreeMap**

* **Ordering:** **Sorted order of keys** (natural ordering or custom Comparator).
* **Nulls:** **Does NOT allow null keys**, allows multiple null values.
* **Performance:**

  * `get()` / `put()` → O(log n) (Red-Black Tree).
* **Data Structure:** **Red-Black Tree** (self-balancing BST).
* **Use Case:** When you need **sorted map** or range queries.

```java
TreeMap<Integer, String> map = new TreeMap<>();
```

---

### **🔹 4. Summary Table**

| Feature                   | HashMap                    | LinkedHashMap                | TreeMap                   |
| ------------------------- | -------------------------- | ---------------------------- | ------------------------- |
| **Order**                 | No order                   | Insertion / Access order     | Sorted order              |
| **Null Key**              | Yes (1)                    | Yes (1)                      | No                        |
| **Null Value**            | Yes                        | Yes                          | Yes                       |
| **Performance (get/put)** | O(1) avg                   | O(1) avg                     | O(log n)                  |
| **Underlying Structure**  | Array + Linked List / Tree | HashMap + Doubly Linked List | Red-Black Tree            |
| **Use Case**              | Fast lookup, unordered     | Maintain order, cache        | Sorted map, range queries |

---

💡 **Interview Tip:**

> "Use `HashMap` for **fast and unordered storage**, `LinkedHashMap` for **predictable iteration order**, and `TreeMap` when you need **sorted keys**."

---

If you want, I can next explain **Difference between HashSet, LinkedHashSet, and TreeSet**, which is often asked as a follow-up in interviews.

Do you want me to cover that next?

---

## 63. Differenece between HashMap, LinkedHashMap, and ConcurrentHashMap?

### **63. Difference Between HashMap, LinkedHashMap, and ConcurrentHashMap in Java**

`HashMap`, `LinkedHashMap`, and `ConcurrentHashMap` are **Map implementations**, but they differ in **ordering, thread-safety, and performance**.

---

### **🔹 1. HashMap**

* **Thread-safety:** Not thread-safe; must be externally synchronized for concurrent access.
* **Ordering:** No order guaranteed.
* **Nulls:** Allows **one null key** and multiple null values.
* **Performance:** Fast, `O(1)` average for `get()`/`put()`.
* **Use Case:** Single-threaded applications where ordering does not matter.

```java
HashMap<Integer, String> map = new HashMap<>();
```

---

### **🔹 2. LinkedHashMap**

* **Thread-safety:** Not thread-safe.
* **Ordering:** Maintains **insertion order** (or access order if `accessOrder=true`).
* **Nulls:** Allows **one null key** and multiple null values.
* **Performance:** Slightly slower than HashMap due to **doubly-linked list maintenance**.
* **Use Case:** When predictable **iteration order** is required (e.g., caches).

```java
LinkedHashMap<Integer, String> map = new LinkedHashMap<>();
```

* Access order example (for LRU cache):

```java
LinkedHashMap<Integer, String> map = new LinkedHashMap<>(16, 0.75f, true);
```

---

### **🔹 3. ConcurrentHashMap**

* **Thread-safety:** Thread-safe, allows **concurrent read/write operations** without locking the whole map.
* **Ordering:** Does **not maintain insertion order**.
* **Nulls:** **Does NOT allow null keys or null values**.
* **Performance:** Uses **bucket-level locking (Java 7)** or **CAS operations (Java 8)** → better concurrent performance than synchronizing a HashMap.
* **Use Case:** Multi-threaded applications needing **high-performance concurrent access**.

```java
ConcurrentHashMap<Integer, String> map = new ConcurrentHashMap<>();
```

---

### **🔹 4. Summary Table**

| Feature                         | HashMap             | LinkedHashMap          | ConcurrentHashMap                       |
| ------------------------------- | ------------------- | ---------------------- | --------------------------------------- |
| **Thread-safety**               | No                  | No                     | Yes                                     |
| **Ordering**                    | No                  | Insertion/Access order | No                                      |
| **Null Key**                    | Yes (1)             | Yes (1)                | No                                      |
| **Null Value**                  | Yes                 | Yes                    | No                                      |
| **Performance (single-thread)** | Fast                | Slightly slower        | Slower than HashMap for single-threaded |
| **Performance (multi-thread)**  | Needs external sync | Needs external sync    | High concurrent performance             |
| **Use Case**                    | Fast unordered map  | Ordered map            | Thread-safe concurrent map              |

---

💡 **Interview Tip:**

> "`HashMap` and `LinkedHashMap` are not thread-safe. Use `ConcurrentHashMap` for high-performance concurrent access. LinkedHashMap is useful when iteration order matters."

---

If you want, I can next explain **Difference between HashSet, LinkedHashSet, and TreeSet**, which is often asked in interviews.

Do you want me to cover that next?

---

## 64. How can you convert a HashMap into an ArrayList?

### **64. How to Convert a `HashMap` into an `ArrayList` in Java**

In Java, a `HashMap` stores **key-value pairs**, while an `ArrayList` stores an **ordered collection of elements**. Depending on your use case, you might want to convert a `HashMap` into an `ArrayList` of:

1. **Keys**
2. **Values**
3. **Map Entries (key-value pairs)**

---

### **🔹 1. Convert HashMap Keys to ArrayList**

```java
import java.util.*;

public class HashMapToArrayList {
    public static void main(String[] args) {
        HashMap<Integer, String> map = new HashMap<>();
        map.put(1, "Aditya");
        map.put(2, "Ramdas");
        map.put(3, "Dange");

        // Convert keys to ArrayList
        ArrayList<Integer> keyList = new ArrayList<>(map.keySet());

        System.out.println("Keys: " + keyList);
    }
}
```

**Output:**

```
Keys: [1, 2, 3]
```

---

### **🔹 2. Convert HashMap Values to ArrayList**

```java
// Convert values to ArrayList
ArrayList<String> valueList = new ArrayList<>(map.values());

System.out.println("Values: " + valueList);
```

**Output:**

```
Values: [Aditya, Ramdas, Dange]
```

---

### **🔹 3. Convert HashMap Entries to ArrayList**

```java
// Convert Map.Entry to ArrayList
ArrayList<Map.Entry<Integer, String>> entryList = new ArrayList<>(map.entrySet());

for (Map.Entry<Integer, String> entry : entryList) {
    System.out.println(entry.getKey() + " -> " + entry.getValue());
}
```

**Output:**

```
1 -> Aditya
2 -> Ramdas
3 -> Dange
```

---

### **🔹 4. Using Streams (Java 8+)**

**Convert values using streams:**

```java
ArrayList<String> valueListStream = map.values()
                                       .stream()
                                       .collect(Collectors.toCollection(ArrayList::new));
```

**Convert entries using streams:**

```java
ArrayList<Map.Entry<Integer, String>> entryListStream = map.entrySet()
                                                           .stream()
                                                           .collect(Collectors.toCollection(ArrayList::new));
```

---

### **🔹 Summary**

| Conversion Type     | Code Example                      |
| ------------------- | --------------------------------- |
| Keys → ArrayList    | `new ArrayList<>(map.keySet())`   |
| Values → ArrayList  | `new ArrayList<>(map.values())`   |
| Entries → ArrayList | `new ArrayList<>(map.entrySet())` |

💡 **Interview Tip:**

> "You can convert a HashMap to an ArrayList using **keySet(), values(), or entrySet()**. Java 8 Streams can also be used for more functional-style conversions."

---

If you want, I can next explain **Difference between HashMap and ArrayList**, which is often asked in interviews.

Do you want me to cover that next?

---

## 65. What are the differences between Comparable and Comparator?

### **65. Differences Between `Comparable` and `Comparator` in Java**

Both `Comparable` and `Comparator` are used to **sort objects in Java**, but they differ in **how and where the sorting logic is defined**.

---

### **🔹 1. Comparable**

* **Package:** `java.lang`
* **Purpose:** Defines **natural ordering** of objects.
* **Interface Type:** **Functional interface** with a single method:

```java
public int compareTo(T o);
```

* **Usage:** The class itself implements `Comparable` and overrides `compareTo()`.
* **Number of Sort Sequences:** Only **one sort sequence** (natural ordering) per class.
* **Example:**

```java
class Student implements Comparable<Student> {
    String name;
    int age;

    public Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    public int compareTo(Student s) {
        return this.age - s.age; // sort by age
    }

    @Override
    public String toString() {
        return name + " - " + age;
    }
}

import java.util.*;

public class ComparableExample {
    public static void main(String[] args) {
        List<Student> list = new ArrayList<>();
        list.add(new Student("Aditya", 25));
        list.add(new Student("Ram", 22));
        list.add(new Student("Dange", 30));

        Collections.sort(list); // uses compareTo
        System.out.println(list);
    }
}
```

**Output:**

```
[Ram - 22, Aditya - 25, Dange - 30]
```

---

### **🔹 2. Comparator**

* **Package:** `java.util`
* **Purpose:** Defines **custom ordering** of objects.
* **Interface Type:** Functional interface with a single method:

```java
public int compare(T o1, T o2);
```

* **Usage:** A separate class or lambda implements `Comparator`.
* **Number of Sort Sequences:** Multiple comparators can be defined for **different criteria**.
* **Example: Sort by name**

```java
class NameComparator implements Comparator<Student> {
    @Override
    public int compare(Student s1, Student s2) {
        return s1.name.compareTo(s2.name); // sort by name
    }
}

Collections.sort(list, new NameComparator());
System.out.println(list);
```

**Output:**

```
[Aditya - 25, Dange - 30, Ram - 22]
```

* **Java 8+ Lambda Version:**

```java
list.sort((s1, s2) -> s1.name.compareTo(s2.name));
```

---

### **🔹 3. Key Differences**

| Feature                   | Comparable                     | Comparator                                       |
| ------------------------- | ------------------------------ | ------------------------------------------------ |
| **Package**               | `java.lang`                    | `java.util`                                      |
| **Interface Type**        | Functional interface           | Functional interface                             |
| **Method**                | `compareTo(Object o)`          | `compare(Object o1, Object o2)`                  |
| **Implementation**        | Class implements `Comparable`  | Separate class or lambda implements `Comparator` |
| **Sorting Sequence**      | Natural ordering (1 per class) | Custom ordering (multiple possible)              |
| **Object Modification**   | Required in the class          | No need to modify the class                      |
| **Java 8 Lambda Support** | Not required                   | Can use lambda or method reference               |

---

💡 **Interview Tip:**

> "`Comparable` is used for **natural order**, `Comparator` is used for **custom order**. Use `Comparator` when you don’t want to modify the original class or need multiple sorting criteria."

---

If you want, I can next explain **Difference between `List`, `Set`, and `Map` in Java**, which is a common fundamental question.

Do you want me to cover that next?

---

## 66. What is a ConcurrentHashMap? How does it work?

### **66. ConcurrentHashMap in Java**

`ConcurrentHashMap` is a **thread-safe variant of HashMap** in Java designed for **highly concurrent environments**. Unlike `HashMap`, it can be safely used by multiple threads **without external synchronization**.

---

### **🔹 1. Key Features**

| Feature                  | Description                                                                             |
| ------------------------ | --------------------------------------------------------------------------------------- |
| **Thread-Safety**        | Supports concurrent read and write operations without locking the entire map.           |
| **Nulls**                | Does **not allow null keys or null values**.                                            |
| **Performance**          | Highly efficient in multi-threaded environments compared to synchronizing a HashMap.    |
| **Underlying Structure** | Segment-based locking (Java 7) or **bucket-level CAS & synchronized blocks** (Java 8+). |

---

### **🔹 2. How ConcurrentHashMap Works**

#### **Java 7 (Segment-based Locking)**

* The map is divided into **segments** (default 16).
* Each segment is like a small **HashMap with its own lock**.
* Threads accessing different segments can operate **concurrently**.
* Only the **segment of the key being accessed** is locked during updates.

**Visualization:**

```
ConcurrentHashMap
  ├─ Segment 0 ─ lock
  ├─ Segment 1 ─ lock
  └─ Segment 15 ─ lock
```

* **Read operations** (`get`) do **not require locking** → fast.
* **Write operations** (`put`, `remove`) lock only the relevant segment → high concurrency.

---

#### **Java 8+ (Bucket-level Locking with CAS)**

* Segments removed → uses **array of Node<K,V> buckets** like HashMap.
* **Reads**: Non-blocking, use **volatile + CAS** for thread-safety.
* **Writes**: Only the **bucket being updated** is synchronized.
* If a bucket’s size grows beyond a threshold, the bucket is converted to a **Red-Black Tree** for efficient lookup.

---

### **🔹 3. Example Usage**

```java
import java.util.concurrent.ConcurrentHashMap;

public class ConcurrentHashMapExample {
    public static void main(String[] args) {
        ConcurrentHashMap<Integer, String> map = new ConcurrentHashMap<>();

        // Add entries
        map.put(1, "Aditya");
        map.put(2, "Ramdas");

        // Access entries
        System.out.println(map.get(1)); // Aditya

        // Update concurrently
        map.putIfAbsent(3, "Dange"); // Thread-safe insert

        System.out.println(map);
    }
}
```

**Output:**

```
Aditya
{1=Aditya, 2=Ramdas, 3=Dange}
```

---

### **🔹 4. Key Points**

1. **Thread-safe alternative** to `HashMap`.
2. **No null keys or null values**.
3. **High performance** in multi-threaded environments.
4. Supports **concurrent retrievals and updates**.
5. **Iteration**:

   * Iterators are **weakly consistent** → reflect some, but not necessarily all, changes during iteration.

---

### **🔹 5. Difference Between HashMap and ConcurrentHashMap**

| Feature        | HashMap                 | ConcurrentHashMap            |
| -------------- | ----------------------- | ---------------------------- |
| Thread Safety  | Not thread-safe         | Thread-safe                  |
| Null Key/Value | Yes                     | No                           |
| Performance    | Fast in single-threaded | Optimized for multi-threaded |
| Locking        | None                    | Bucket/segment-level locking |
| Iterators      | Fail-fast               | Weakly consistent            |

---

💡 **Interview Tip:**

> "ConcurrentHashMap allows **highly concurrent read/write operations** without locking the entire map. It uses **bucket-level locking (Java 8)** and does not allow null keys or values."

---

If you want, I can next explain **Difference between `ConcurrentHashMap` and `Collections.synchronizedMap()`**, which is a common follow-up interview question.

Do you want me to cover that next?

---

## 67. What's the different between HashTable and ConcurrentHashMap?

### **67. Difference Between `Hashtable` and `ConcurrentHashMap` in Java**

Both `Hashtable` and `ConcurrentHashMap` are **thread-safe Map implementations**, but they differ in **performance, locking mechanism, null handling, and modern usage**.

---

### **🔹 1. Thread-Safety and Locking**

| Feature                            | Hashtable                                      | ConcurrentHashMap                                                              |
| ---------------------------------- | ---------------------------------------------- | ------------------------------------------------------------------------------ |
| **Thread-Safety**                  | Thread-safe                                    | Thread-safe                                                                    |
| **Locking Mechanism**              | Synchronizes **entire table** for every method | Locks **only the bucket/segment** being updated (Java 8: bucket-level locking) |
| **Performance in Multi-threading** | Slower (entire table locked)                   | Faster (fine-grained locking allows high concurrency)                          |

---

### **🔹 2. Null Keys and Null Values**

| Feature        | Hashtable   | ConcurrentHashMap |
| -------------- | ----------- | ----------------- |
| **Null Key**   | Not allowed | Not allowed       |
| **Null Value** | Not allowed | Not allowed       |

> Both **do not allow null keys or values**, unlike `HashMap`.

---

### **🔹 3. Iterators**

| Feature      | Hashtable                        | ConcurrentHashMap                                                    |
| ------------ | -------------------------------- | -------------------------------------------------------------------- |
| **Iterator** | Enumerator (legacy) or fail-fast | Weakly consistent (does not throw `ConcurrentModificationException`) |

* **Weakly consistent iterator**: Reflects some but not necessarily all changes during iteration.

---

### **🔹 4. Legacy vs Modern Use**

* `Hashtable` is a **legacy class** from JDK 1.0.
* `ConcurrentHashMap` is **modern, high-performance**, part of **java.util.concurrent**, and preferred in multi-threaded applications.

---

### **🔹 5. Example Usage**

**Hashtable:**

```java
Hashtable<Integer, String> table = new Hashtable<>();
table.put(1, "Aditya");
table.put(2, "Ramdas");
```

**ConcurrentHashMap:**

```java
ConcurrentHashMap<Integer, String> map = new ConcurrentHashMap<>();
map.put(1, "Aditya");
map.put(2, "Ramdas");
map.putIfAbsent(3, "Dange"); // Thread-safe insert
```

---

### **🔹 6. Key Differences Summary**

| Feature            | Hashtable           | ConcurrentHashMap             |
| ------------------ | ------------------- | ----------------------------- |
| **Thread Safety**  | Entire table locked | Bucket-level locking (Java 8) |
| **Performance**    | Slower              | Faster, better concurrency    |
| **Null Key/Value** | Not allowed         | Not allowed                   |
| **Iterator**       | Fail-fast           | Weakly consistent             |
| **Legacy**         | Yes                 | Modern (preferred)            |
| **Use Case**       | Rarely used now     | Use in multi-threaded apps    |

---

💡 **Interview Tip:**

> "Use `ConcurrentHashMap` instead of `Hashtable` in modern Java because it provides **high-performance thread-safe operations** with **bucket-level locking** and weakly consistent iteration."

---

If you want, I can next explain **Difference between HashMap, TreeMap, and ConcurrentHashMap**, which is also commonly asked in interviews.

Do you want me to cover that next?

---

## 68. What is the difference between Vector and ArrayList?

### **68. Difference Between `Vector` and `ArrayList` in Java**

Both `Vector` and `ArrayList` are **resizable arrays** in Java that implement the **List interface**, but they differ in **thread-safety, performance, and legacy usage**.

---

### **🔹 1. Thread-Safety**

| Feature       | Vector                                 | ArrayList                            |
| ------------- | -------------------------------------- | ------------------------------------ |
| Thread-Safety | Synchronized (thread-safe)             | Not synchronized (not thread-safe)   |
| Performance   | Slower due to synchronization overhead | Faster in single-threaded operations |

> `Vector` synchronizes **every method**, making it safe for multi-threaded access but slower.
> `ArrayList` is faster in **single-threaded** environments.

---

### **🔹 2. Legacy vs Modern**

| Feature    | Vector                             | ArrayList                                |
| ---------- | ---------------------------------- | ---------------------------------------- |
| Introduced | Java 1.0 (legacy)                  | Java 1.2 (part of Collections framework) |
| Usage      | Legacy, rarely used in modern code | Preferred resizable array implementation |

---

### **🔹 3. Growth Rate**

* **Vector:** Doubles its size when capacity is exceeded.
* **ArrayList:** Increases size by **50%** of current capacity when exceeded.

```java
ArrayList<Integer> list = new ArrayList<>(10); // initial capacity = 10
Vector<Integer> vector = new Vector<>(10);     // initial capacity = 10
```

---

### **🔹 4. Null Elements**

| Feature       | Vector                        | ArrayList             |
| ------------- | ----------------------------- | --------------------- |
| Null Elements | Allows multiple nulls         | Allows multiple nulls |
| Null Keys     | N/A (List does not have keys) | N/A                   |

---

### **🔹 5. Iterators**

| Feature     | Vector    | ArrayList     |
| ----------- | --------- | ------------- |
| Iterator    | Fail-fast | Fail-fast     |
| Enumeration | Supported | Not supported |

> `Vector` has legacy **Enumeration interface** in addition to Iterator.

---

### **🔹 6. Example**

```java
// ArrayList
ArrayList<String> arrayList = new ArrayList<>();
arrayList.add("Aditya");
arrayList.add("Ramdas");

// Vector
Vector<String> vector = new Vector<>();
vector.add("Aditya");
vector.add("Ramdas");
```

---

### **🔹 7. Summary Table**

| Feature                      | Vector                | ArrayList        |
| ---------------------------- | --------------------- | ---------------- |
| **Thread-safety**            | Synchronized          | Not synchronized |
| **Performance**              | Slower                | Faster           |
| **Introduced in**            | JDK 1.0 (legacy)      | JDK 1.2          |
| **Growth**                   | Doubles capacity      | Increases by 50% |
| **Legacy Methods**           | Enumeration supported | No Enumeration   |
| **Preferred in modern Java** | Rarely                | Yes              |

---

💡 **Interview Tip:**

> "Use `ArrayList` in modern Java for most cases. `Vector` is legacy and only used if thread-safety is required without external synchronization, but `Concurrent collections` are preferred today."

---

If you want, I can next explain **Difference between ArrayList, LinkedList, and Vector**, which is a common follow-up question in interviews.

Do you want me to cover that next?

---

## 69. HashMap vs HashTable.

### **69. Difference Between `HashMap` and `Hashtable` in Java**

Both `HashMap` and `Hashtable` implement the **Map interface** and store **key-value pairs**, but they differ in **thread-safety, null handling, performance, and legacy usage**.

---

### **🔹 1. Thread-Safety**

| Feature            | HashMap                                                          | Hashtable                                      |
| ------------------ | ---------------------------------------------------------------- | ---------------------------------------------- |
| **Thread-Safety**  | Not thread-safe                                                  | Thread-safe (synchronized methods)             |
| **Concurrent Use** | Needs external synchronization (`Collections.synchronizedMap()`) | Safe for multi-threading but slows performance |

> `HashMap` is faster in single-threaded apps. `Hashtable` locks the entire table for each method, reducing concurrency.

---

### **🔹 2. Null Keys and Values**

| Feature         | HashMap                     | Hashtable                      |
| --------------- | --------------------------- | ------------------------------ |
| **Null Key**    | Allows **one null key**     | Does **not allow null keys**   |
| **Null Values** | Allows multiple null values | Does **not allow null values** |

---

### **🔹 3. Performance**

| Feature                        | HashMap   | Hashtable                        |
| ------------------------------ | --------- | -------------------------------- |
| **Average time complexity**    | O(1)      | O(1)                             |
| **Thread contention overhead** | None      | High due to synchronized methods |
| **Use in modern applications** | Preferred | Rarely used now                  |

---

### **🔹 4. Legacy vs Modern**

| Feature                           | HashMap                         | Hashtable                              |
| --------------------------------- | ------------------------------- | -------------------------------------- |
| **Introduced in**                 | JDK 1.2 (Collections framework) | JDK 1.0 (legacy)                       |
| **Part of Collections Framework** | Yes                             | Legacy class (partially adapted later) |

---

### **🔹 5. Iterator**

| Feature           | HashMap       | Hashtable          |
| ----------------- | ------------- | ------------------ |
| **Iterator Type** | Fail-fast     | Fail-fast          |
| **Enumeration**   | Not supported | Supported (legacy) |

---

### **🔹 6. Example**

```java
// HashMap
HashMap<Integer, String> hashMap = new HashMap<>();
hashMap.put(1, "Aditya");
hashMap.put(null, "NullKey"); // Allowed

// Hashtable
Hashtable<Integer, String> hashtable = new Hashtable<>();
hashtable.put(1, "Aditya");
// hashtable.put(null, "NullKey"); // Throws NullPointerException
```

---

### **🔹 7. Summary Table**

| Feature           | HashMap   | Hashtable                       |
| ----------------- | --------- | ------------------------------- |
| **Thread-Safety** | No        | Yes (synchronized)              |
| **Null Key**      | Yes (1)   | No                              |
| **Null Value**    | Yes       | No                              |
| **Performance**   | Faster    | Slower                          |
| **Legacy**        | Modern    | Legacy                          |
| **Iterator**      | Fail-fast | Fail-fast, supports Enumeration |

---

💡 **Interview Tip:**

> "Use `HashMap` in modern Java. `Hashtable` is legacy and rarely used. For thread-safe maps, prefer `ConcurrentHashMap` over `Hashtable`."

---

If you want, I can next explain **Difference between HashMap, LinkedHashMap, TreeMap, and ConcurrentHashMap** in one comparison table for clarity, which is a common interview question.

Do you want me to do that next?

---

## 70. ArrayList vs LinkedList.

### **70. Difference Between `ArrayList` and `LinkedList` in Java**

Both `ArrayList` and `LinkedList` implement the **List interface**, but they differ in **internal structure, performance, and use cases**.

---

### **🔹 1. Internal Data Structure**

| Feature                  | ArrayList               | LinkedList                                                                |
| ------------------------ | ----------------------- | ------------------------------------------------------------------------- |
| **Underlying Structure** | Resizable **array**     | **Doubly linked list** of nodes                                           |
| **Memory Usage**         | Less memory per element | More memory per element (stores data + pointers to next & previous nodes) |

---

### **🔹 2. Performance**

| Operation                       | ArrayList             | LinkedList                                      |
| ------------------------------- | --------------------- | ----------------------------------------------- |
| **Access by index (`get(i)`)**  | O(1) (fast)           | O(n) (slow, traverse from head/tail)            |
| **Insertion at end (`add(e)`)** | O(1) amortized        | O(1)                                            |
| **Insertion in middle**         | O(n) (shift elements) | O(1) (adjust pointers, if position known)       |
| **Deletion**                    | O(n) (shift elements) | O(1) (adjust pointers, if node reference known) |

---

### **🔹 3. Use Cases**

| Feature                                     | ArrayList       | LinkedList      |
| ------------------------------------------- | --------------- | --------------- |
| **Frequent random access**                  | ✅ Preferred     | ❌ Not efficient |
| **Frequent insertions/deletions in middle** | ❌ Expensive     | ✅ Preferred     |
| **Memory efficiency**                       | ✅ Less overhead | ❌ More overhead |

---

### **🔹 4. Null Elements and Duplicates**

* Both **allow null elements** and **duplicate values**.

---

### **🔹 5. Iterators**

* Both support **fail-fast iterators**.
* LinkedList also implements **Deque** interface → supports **addFirst(), addLast(), removeFirst(), removeLast()**.

---

### **🔹 6. Example**

```java
// ArrayList
ArrayList<String> arrayList = new ArrayList<>();
arrayList.add("Aditya");
arrayList.add("Ramdas");
System.out.println(arrayList.get(1)); // Ramdas

// LinkedList
LinkedList<String> linkedList = new LinkedList<>();
linkedList.add("Aditya");
linkedList.add("Ramdas");
linkedList.addFirst("Dange"); 
System.out.println(linkedList); // [Dange, Aditya, Ramdas]
```

---

### **🔹 7. Summary Table**

| Feature                       | ArrayList                        | LinkedList                    |
| ----------------------------- | -------------------------------- | ----------------------------- |
| **Structure**                 | Dynamic array                    | Doubly linked list            |
| **Access by index**           | O(1)                             | O(n)                          |
| **Insertion/Deletion middle** | O(n)                             | O(1)                          |
| **Insertion/Deletion end**    | O(1) amortized                   | O(1)                          |
| **Memory Overhead**           | Low                              | High (pointers)               |
| **Use Case**                  | Random access, few modifications | Frequent insertions/deletions |

---

💡 **Interview Tip:**

> "Use `ArrayList` for **fast random access**. Use `LinkedList` for **frequent insertions/deletions**, especially at the beginning or middle of the list."

---

If you want, I can next explain **Difference between Array, ArrayList, and LinkedList**, which is commonly asked together in interviews.

Do you want me to cover that next?

---


# Java 8 Features

## 71. What is a Functional Interface?

### **71. What is a Functional Interface in Java**

A **Functional Interface** is an interface that has **exactly one abstract method**. It is used as the **target for lambda expressions and method references** in Java 8 and later.

---

### **🔹 1. Key Characteristics**

1. **Single Abstract Method (SAM):** Must have exactly **one abstract method**.
2. **Optional Default/Static Methods:** Can have **default and static methods**.
3. **@FunctionalInterface Annotation:** Optional, but recommended.

   * Compiler will **throw an error** if the interface annotated with `@FunctionalInterface` has more than one abstract method.
4. **Used for Lambda Expressions:** Enables **concise functional programming**.

---

### **🔹 2. Example**

```java
@FunctionalInterface
interface Calculator {
    int add(int a, int b);  // Single abstract method

    // Default method (optional)
    default void printMessage() {
        System.out.println("Calculator Functional Interface");
    }

    // Static method (optional)
    static void greet() {
        System.out.println("Hello from Calculator");
    }
}
```

**Using Lambda Expression:**

```java
public class FunctionalInterfaceExample {
    public static void main(String[] args) {
        Calculator calculator = (a, b) -> a + b; // Lambda expression
        System.out.println("Sum: " + calculator.add(5, 10)); // Sum: 15

        calculator.printMessage(); // Default method
        Calculator.greet();        // Static method
    }
}
```

---

### **🔹 3. Common Functional Interfaces in Java 8+**

| Interface       | Abstract Method           | Purpose                           |
| --------------- | ------------------------- | --------------------------------- |
| `Runnable`      | `void run()`              | Execute code in a thread          |
| `Callable<V>`   | `V call()`                | Execute code that returns a value |
| `Comparator<T>` | `int compare(T o1, T o2)` | Compare objects                   |
| `Consumer<T>`   | `void accept(T t)`        | Perform an operation on `T`       |
| `Supplier<T>`   | `T get()`                 | Provide a value of type `T`       |
| `Function<T,R>` | `R apply(T t)`            | Transform `T` into `R`            |
| `Predicate<T>`  | `boolean test(T t)`       | Test a condition on `T`           |

---

### **🔹 4. Key Points**

* Can have **only one abstract method**, but **multiple default or static methods**.
* Enables **lambda expressions**, **streams**, and **functional programming**.
* Optional `@FunctionalInterface` annotation improves **readability** and **compile-time checking**.

---

💡 **Interview Tip:**

> "A functional interface has exactly **one abstract method**, making it compatible with lambda expressions. Use `@FunctionalInterface` for clarity and compile-time safety."

---

If you want, I can next explain **Difference between Functional Interface, Lambda, and Method Reference**, which is often asked in Java 8 interviews.

Do you want me to cover that next?

---

## 72. Explain Java 8 features (Lamdas, Streams, Optional).

### **72. Key Java 8 Features: Lambdas, Streams, and Optional**

Java 8 introduced several **major enhancements** that modernized Java programming, especially for **functional programming and cleaner code**. The most commonly discussed features are **Lambda Expressions**, **Streams API**, and **Optional**.

---

## **1. Lambda Expressions**

**Definition:**
A **Lambda Expression** is an **anonymous function** that can be treated as a **method argument or stored as a variable**. It enables **functional programming** in Java.

**Syntax:**

```java
(parameters) -> expression
(parameters) -> { statements; }
```

**Example:**

```java
// Using Lambda to implement Runnable
Runnable r = () -> System.out.println("Hello, Lambda!");
new Thread(r).start();

// Using Lambda with a List
List<String> names = Arrays.asList("Aditya", "Ramdas", "Dange");
names.forEach(name -> System.out.println(name));
```

**Advantages:**

* Less boilerplate code
* Enables functional-style programming
* Works with **Functional Interfaces**

---

## **2. Streams API**

**Definition:**
A **Stream** represents a **sequence of elements supporting functional-style operations** (map, filter, reduce, etc.). It does **not store data**, but **processes collections**.

**Types of operations:**

* **Intermediate**: Returns a new stream (e.g., `filter()`, `map()`)
* **Terminal**: Returns a result or side-effect (e.g., `collect()`, `forEach()`, `count()`)

**Example:**

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);

// Filter even numbers and square them
List<Integer> squares = numbers.stream()
                               .filter(n -> n % 2 == 0)
                               .map(n -> n * n)
                               .collect(Collectors.toList());

System.out.println(squares); // [4, 16]
```

**Advantages:**

* Concise and readable code
* Enables **parallel processing** (`parallelStream()`)
* Works well with **lambda expressions**

---

## **3. Optional Class**

**Definition:**
`Optional<T>` is a **container object** which may or may not contain a **non-null value**. It helps **avoid `NullPointerException`**.

**Key Methods:**

* `isPresent()` → checks if value exists
* `ifPresent(Consumer)` → executes code if value exists
* `orElse(T other)` → returns value or default
* `orElseGet(Supplier)` → lazy default value
* `orElseThrow(Supplier)` → throw exception if value absent

**Example:**

```java
Optional<String> name = Optional.ofNullable(null);

// Check presence
if (name.isPresent()) {
    System.out.println(name.get());
} else {
    System.out.println("No value present");
}

// Using orElse
System.out.println(name.orElse("Default Name")); // Default Name

// Using ifPresent
name.ifPresent(n -> System.out.println(n)); // No output
```

**Advantages:**

* Reduces **null checks**
* Makes API **safer and more readable**
* Encourages **functional programming**

---

## **4. Summary Table**

| Feature      | Purpose                                       | Example                                  | Benefits                                |
| ------------ | --------------------------------------------- | ---------------------------------------- | --------------------------------------- |
| **Lambda**   | Anonymous functions, replace boilerplate code | `(a,b) -> a+b`                           | Functional programming, concise code    |
| **Streams**  | Functional-style collection processing        | `list.stream().filter(...).collect(...)` | Cleaner, readable, parallel processing  |
| **Optional** | Avoid nulls, safer APIs                       | `Optional.ofNullable(value)`             | Null-safety, reduces NPE, readable code |

---

💡 **Interview Tip:**

> "Java 8 promotes **functional programming**. Use **lambda expressions** for concise code, **Streams** for collection operations, and **Optional** to safely handle nullable values."

---

If you want, I can next explain **Java 8 Stream operations in detail (filter, map, reduce, collect, flatMap, distinct, sorted)** with examples, which is a common interview topic.

Do you want me to cover that next?

---

## 73. Difference between map() vs flatMap() in Java 8?

### **73. Difference Between `map()` and `flatMap()` in Java 8 Streams**

Both `map()` and `flatMap()` are **intermediate operations** in Java 8 Streams used to transform elements, but they behave differently, especially when dealing with **nested structures**.

---

## **1. `map()`**

**Definition:**

* Transforms each element of a stream into **another object** using a **Function**.
* **Output:** Stream of **same size**, each element transformed individually.

**Syntax:**

```java
<R> Stream<R> map(Function<? super T, ? extends R> mapper)
```

**Example:**

```java
List<String> words = Arrays.asList("Java", "Python");

// Convert each word to uppercase
List<String> upper = words.stream()
                          .map(String::toUpperCase)
                          .collect(Collectors.toList());

System.out.println(upper); // [JAVA, PYTHON]
```

* **Key Point:** Each element maps to **exactly one element** in the output stream.

---

## **2. `flatMap()`**

**Definition:**

* Transforms each element into a **stream of values**, then **flattens all streams into a single stream**.
* **Output:** Flattened stream of elements (removes nesting).

**Syntax:**

```java
<R> Stream<R> flatMap(Function<? super T, ? extends Stream<? extends R>> mapper)
```

**Example: Flatten list of words into characters**

```java
List<String> words = Arrays.asList("Java", "Python");

// Flatten each word into characters
List<String> chars = words.stream()
                          .flatMap(word -> Arrays.stream(word.split("")))
                          .collect(Collectors.toList());

System.out.println(chars); 
// [J, a, v, a, P, y, t, h, o, n]
```

* **Key Point:** Useful for **nested collections or arrays**, produces **single-level stream**.

---

## **3. Key Differences**

| Feature            | `map()`                          | `flatMap()`                                                 |
| ------------------ | -------------------------------- | ----------------------------------------------------------- |
| **Purpose**        | Transform each element           | Transform and flatten nested elements                       |
| **Input → Output** | Element → Single element         | Element → Stream of elements                                |
| **Output Stream**  | Same level                       | Flattened (single-level)                                    |
| **Use Case**       | Simple transformations           | Nested structures like List<List<T>>, Optional<Optional<T>> |
| **Example**        | `words.map(String::toUpperCase)` | `words.flatMap(w -> Arrays.stream(w.split("")))`            |

---

### **4. When to Use**

* **`map()`** → When you have a **1-to-1 transformation**.
* **`flatMap()`** → When you have a **1-to-many transformation** or **nested collections** that need flattening.

---

💡 **Interview Tip:**

> "`map()` transforms each element individually, `flatMap()` transforms and flattens nested structures into a single stream."

---

If you want, I can next explain **Difference between `Optional.map()` and `Optional.flatMap()`**, which is closely related and often asked in Java 8 interviews.

Do you want me to cover that next?

---

## 74. What is Stream API and its advantages?

### **74. Stream API in Java 8 and Its Advantages**

The **Stream API** in Java 8 allows you to process **collections of data** (like `List`, `Set`, or arrays) in a **functional, declarative, and efficient** way. Streams focus on **what to do** with data rather than **how to do it**.

---

## **1. What is a Stream?**

A **Stream** is:

1. **A sequence of elements** from a source (collection, array, I/O channel).
2. **Supports functional-style operations** (map, filter, reduce, etc.).
3. **Does not store data** itself (data remains in the source).
4. **Lazy evaluation** – operations are performed only when required.
5. **Can be sequential or parallel** (for parallel processing).

---

## **2. Types of Stream Operations**

### **a) Intermediate Operations**

* Return a new stream and are **lazy**.
* Examples:

  * `filter()` → selects elements based on a condition
  * `map()` → transforms elements
  * `flatMap()` → flattens nested structures
  * `distinct()` → removes duplicates
  * `sorted()` → sorts elements

### **b) Terminal Operations**

* Produce a **result or side-effect** and **trigger stream processing**.
* Examples:

  * `collect()` → collect elements into a collection
  * `forEach()` → iterate and perform action
  * `count()` → count elements
  * `reduce()` → combine elements

---

## **3. Example of Stream API**

```java
import java.util.*;
import java.util.stream.*;

public class StreamExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Aditya", "Ramdas", "Dange", "John");

        // Filter names starting with 'D', convert to uppercase, collect as list
        List<String> filtered = names.stream()
                                     .filter(name -> name.startsWith("D"))
                                     .map(String::toUpperCase)
                                     .collect(Collectors.toList());

        System.out.println(filtered); // [DANGE]
    }
}
```

---

## **4. Advantages of Stream API**

| Advantage                   | Explanation                                                                          |
| --------------------------- | ------------------------------------------------------------------------------------ |
| **Functional Programming**  | Allows concise, readable code using **lambda expressions**.                          |
| **Parallel Processing**     | Supports `parallelStream()` to utilize multi-core processors efficiently.            |
| **Lazy Evaluation**         | Intermediate operations are evaluated **only when a terminal operation is invoked**. |
| **Declarative Code**        | Focuses on **what to do** rather than **how to do it**.                              |
| **Chaining Operations**     | Multiple operations can be **chained** in a single pipeline.                         |
| **Reduce Boilerplate Code** | Avoids explicit iteration (`for` or `while`) and temporary collections.              |
| **Better Readability**      | Code is more **clean, readable, and maintainable**.                                  |

---

💡 **Interview Tip:**

> "Streams in Java 8 allow **functional, declarative, and parallel processing** of collections. They reduce boilerplate, support chaining, and make code more readable."

---

If you want, I can next explain **Difference between Sequential Stream and Parallel Stream** with examples, which is a frequently asked Java 8 interview question.

Do you want me to cover that next?

---

## 75. What is Stream pipeline?

### **75. What is a Stream Pipeline in Java 8**

A **Stream pipeline** is a **sequence of stream operations** that **process data from a source** and produce a result. It is composed of three main components: **source → intermediate operations → terminal operation**.

---

## **1. Components of a Stream Pipeline**

| Component                   | Description                                                                                                                                                              |
| --------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Source**                  | The data source (Collection, Array, I/O channel, etc.) from which the stream is created.                                                                                 |
| **Intermediate Operations** | Operations that **transform, filter, or map** the stream elements. They are **lazy** and return another stream. Examples: `map()`, `filter()`, `distinct()`, `sorted()`. |
| **Terminal Operation**      | Operations that **produce a result** or side-effect and **trigger the execution** of the pipeline. Examples: `collect()`, `forEach()`, `count()`, `reduce()`.            |

---

## **2. How It Works**

1. **Pipeline is created** but **not executed** until a terminal operation is invoked.
2. Intermediate operations are **lazy** → no processing occurs until terminal operation.
3. Data flows **from source → intermediate → terminal**.

**Diagram:**

```
Collection/Array (Source)
          |
      stream()
          |
  Intermediate Operations
(filter, map, sorted, distinct)
          |
    Terminal Operation
(forEach, collect, reduce)
```

---

## **3. Example**

```java
import java.util.*;
import java.util.stream.*;

public class StreamPipelineExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Aditya", "Ramdas", "Dange", "John");

        List<String> result = names.stream()                 // Source
                                   .filter(n -> n.startsWith("D"))  // Intermediate
                                   .map(String::toUpperCase)        // Intermediate
                                   .sorted()                        // Intermediate
                                   .collect(Collectors.toList());   // Terminal

        System.out.println(result); // [DANGE]
    }
}
```

**Explanation:**

1. **Source:** `names.stream()` creates a stream from the list.
2. **Intermediate Operations:**

   * `filter()` → selects names starting with "D"
   * `map()` → converts names to uppercase
   * `sorted()` → sorts the names
3. **Terminal Operation:** `collect()` → collects results into a List and **triggers execution**

---

## **4. Key Points**

* **Lazy Evaluation:** Intermediate operations are executed **only when terminal operation runs**.
* **Chaining:** Multiple intermediate operations can be chained in a **single pipeline**.
* **Single-use:** A stream can be **consumed only once**. After a terminal operation, it cannot be reused.

---

💡 **Interview Tip:**

> "A Stream pipeline is a **sequence of operations** starting from a source, passing through zero or more intermediate operations, and ending with a terminal operation. Execution happens only when the terminal operation is invoked."

---

If you want, I can next explain **Difference between `map()`, `flatMap()`, and `filter()` in Stream pipelines**, which is a common Java 8 interview topic.

Do you want me to cover that next?

---

## 76. Difference between intermediate and terminal oprators in Stream API.

### **76. Difference Between Intermediate and Terminal Operators in Java 8 Stream API**

In the **Java 8 Stream API**, operations are classified as **Intermediate** or **Terminal** based on how they behave in a **stream pipeline**.

---

## **1. Intermediate Operators**

**Definition:**

* **Transform or filter the stream** without consuming it.
* **Lazy:** They are **not executed immediately**; execution happens only when a terminal operation is invoked.
* **Return:** Another **Stream**, allowing **chaining** of multiple operations.

**Common Examples:**

* `map()` → transforms elements
* `filter()` → filters elements based on a predicate
* `distinct()` → removes duplicates
* `sorted()` → sorts elements
* `limit(n)` → limits the number of elements
* `skip(n)` → skips first n elements

**Example:**

```java
List<String> names = Arrays.asList("Aditya", "Ramdas", "Dange");
Stream<String> stream = names.stream()
                             .filter(n -> n.startsWith("D"))
                             .map(String::toUpperCase);
```

* `filter()` and `map()` are **intermediate** → pipeline not executed yet.

---

## **2. Terminal Operators**

**Definition:**

* **Consume the stream** and produce a **result** or side-effect.
* **Trigger the execution** of the stream pipeline.
* **Return:** A **non-stream value** like a Collection, primitive, or void.

**Common Examples:**

* `collect()` → collect results into a Collection
* `forEach()` → iterate and perform an action
* `count()` → count elements
* `reduce()` → combine elements into a single value
* `anyMatch()`, `allMatch()`, `noneMatch()` → boolean results

**Example:**

```java
List<String> result = names.stream()
                           .filter(n -> n.startsWith("D"))
                           .map(String::toUpperCase)
                           .collect(Collectors.toList()); // Terminal
```

* `collect()` triggers execution of the **intermediate operations**.

---

## **3. Key Differences**

| Feature         | Intermediate Operator                         | Terminal Operator                                    |
| --------------- | --------------------------------------------- | ---------------------------------------------------- |
| **Execution**   | Lazy (not executed immediately)               | Eager (executes the pipeline)                        |
| **Return Type** | Stream (allows chaining)                      | Non-stream value (Collection, primitive, void, etc.) |
| **Purpose**     | Transform/filter data                         | Produce a result or side-effect                      |
| **Examples**    | `map()`, `filter()`, `sorted()`, `distinct()` | `collect()`, `forEach()`, `count()`, `reduce()`      |

---

💡 **Interview Tip:**

> "Intermediate operators **transform the stream lazily** and return a stream. Terminal operators **consume the stream**, produce a result, and **trigger pipeline execution**."

---

If you want, I can next explain **Difference between `findFirst()`, `findAny()`, `anyMatch()`, `allMatch()` in Streams**, which is another commonly asked topic.

Do you want me to cover that next?

---

## 77. Using Stream API, find the 2nd highest salary from employee objects list.

### ✅ **77. Find the 2nd Highest Salary Using Stream API (Java 8)**

This is one of the **most common Java 8 interview questions**, used to test your understanding of **Streams, sorting, and data extraction** from collections.

---

## 🧠 **Problem Statement**

Given a list of `Employee` objects, find the **2nd highest salary** using the **Stream API**.

### **Employee Class Example**

```java
class Employee {
    private String name;
    private double salary;

    public Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    public double getSalary() {
        return salary;
    }

    public String getName() {
        return name;
    }
}
```

---

## ✅ **Solution 1: Using `sorted()` and `skip()`**

```java
import java.util.*;
import java.util.stream.*;

public class SecondHighestSalary {
    public static void main(String[] args) {
        List<Employee> employees = Arrays.asList(
            new Employee("Aditya", 50000),
            new Employee("Ramdas", 70000),
            new Employee("Dange", 90000),
            new Employee("John", 70000)
        );

        // Find 2nd highest salary
        Optional<Double> secondHighest = employees.stream()
            .map(Employee::getSalary)               // Extract salary
            .distinct()                             // Remove duplicates
            .sorted(Comparator.reverseOrder())      // Sort descending
            .skip(1)                                // Skip the highest
            .findFirst();                           // Get the next one

        if (secondHighest.isPresent())
            System.out.println("2nd Highest Salary: " + secondHighest.get());
        else
            System.out.println("Not enough employees!");
    }
}
```

### **Output:**

```
2nd Highest Salary: 70000.0
```

---

## ✅ **Solution 2: Using `collect()` and List Indexing**

```java
List<Double> sortedSalaries = employees.stream()
    .map(Employee::getSalary)
    .distinct()
    .sorted(Comparator.reverseOrder())
    .collect(Collectors.toList());

if (sortedSalaries.size() >= 2)
    System.out.println("2nd Highest Salary: " + sortedSalaries.get(1));
else
    System.out.println("Not enough employees!");
```

---

## ✅ **Solution 3: Using `max()` and `filter()`**

This approach removes the top salary, then finds the maximum of remaining.

```java
Double maxSalary = employees.stream()
    .map(Employee::getSalary)
    .max(Double::compare)
    .orElseThrow(() -> new RuntimeException("No employees"));

Double secondHighest = employees.stream()
    .map(Employee::getSalary)
    .filter(sal -> sal < maxSalary)
    .max(Double::compare)
    .orElseThrow(() -> new RuntimeException("No second highest"));

System.out.println("2nd Highest Salary: " + secondHighest);
```

---

## 🧩 **Summary of Approaches**

| Approach | Technique                      | Complexity   | Notes                             |
| -------- | ------------------------------ | ------------ | --------------------------------- |
| 1        | `sorted().skip(1).findFirst()` | O(n log n)   | Clean and readable                |
| 2        | `collect()` and index access   | O(n log n)   | Easy for debugging                |
| 3        | `max()` + `filter()`           | O(2n) ≈ O(n) | More efficient for large datasets |

---

💡 **Interview Tip:**

> “To find the 2nd highest salary, use Stream operations like `map()`, `distinct()`, `sorted(Comparator.reverseOrder())`, and `skip(1)`.
> It’s a good test of both sorting and Stream fluency.”

---

Would you like me to extend this example to find the **N-th highest salary (e.g., 3rd, 4th, etc.)** dynamically using Streams?

---

## 78. Use of Stream Api in projects.

### **78. Use of Stream API in Real Projects**

The **Stream API** introduced in Java 8 is widely used in modern Java projects for **processing collections in a clean, declarative, and efficient way**. Below are the key **use cases and examples** from real-world scenarios.

---

## **1. Filtering Data**

**Use Case:** Filtering a list of objects based on a condition.

**Example:** Filtering active users from a list.

```java
List<User> users = getUsers();
List<User> activeUsers = users.stream()
                              .filter(User::isActive)
                              .collect(Collectors.toList());
```

**Project Example:**

* Filtering **active employees**, **products in stock**, or **pending orders** in an ERP or e-commerce system.

---

## **2. Transforming Data (Mapping)**

**Use Case:** Transform one type of data into another.

```java
List<Employee> employees = getEmployees();
List<String> employeeNames = employees.stream()
                                      .map(Employee::getName)
                                      .collect(Collectors.toList());
```

**Project Example:**

* Converting **Employee objects** to **DTOs** before sending JSON responses in a REST API.
* Mapping database entities to **view models** in web applications.

---

## **3. Aggregation & Statistics**

**Use Case:** Calculating totals, averages, or other statistics.

```java
double totalSalary = employees.stream()
                             .mapToDouble(Employee::getSalary)
                             .sum();

double avgSalary = employees.stream()
                            .mapToDouble(Employee::getSalary)
                            .average()
                            .orElse(0.0);
```

**Project Example:**

* Generating **report summaries**, like total sales, average order value, or employee payroll calculations.

---

## **4. Sorting Data**

**Use Case:** Sort collections efficiently.

```java
List<Employee> sortedEmployees = employees.stream()
                                          .sorted(Comparator.comparing(Employee::getSalary).reversed())
                                          .collect(Collectors.toList());
```

**Project Example:**

* Displaying **top performers**, **most expensive products**, or **recent orders** in dashboards.

---

## **5. Removing Duplicates**

**Use Case:** Removing duplicates from a collection.

```java
List<String> emails = users.stream()
                           .map(User::getEmail)
                           .distinct()
                           .collect(Collectors.toList());
```

**Project Example:**

* Ensuring **unique email addresses** in marketing campaigns or registration lists.

---

## **6. Flat Mapping Nested Data**

**Use Case:** Flatten nested collections for processing.

```java
List<Order> orders = getOrders();
List<Product> allProducts = orders.stream()
                                  .flatMap(order -> order.getProducts().stream())
                                  .collect(Collectors.toList());
```

**Project Example:**

* Extracting **all products from multiple orders** for analytics or inventory checks.

---

## **7. Parallel Processing**

**Use Case:** Improve performance for large datasets.

```java
long count = employees.parallelStream()
                      .filter(emp -> emp.getSalary() > 50000)
                      .count();
```

**Project Example:**

* Parallel processing in **financial computations**, **log analysis**, or **big data batch jobs**.

---

## **8. Collecting & Grouping Data**

**Use Case:** Group data by a key and perform aggregations.

```java
Map<String, List<Employee>> deptMap = employees.stream()
                                               .collect(Collectors.groupingBy(Employee::getDepartment));
```

**Project Example:**

* Grouping **employees by department**, **orders by customer**, or **products by category** in dashboards.

---

## **9. Real-World Project Examples**

| Project Type             | Stream API Use Case                                               |
| ------------------------ | ----------------------------------------------------------------- |
| E-commerce               | Filter products by category, sort by price, calculate total sales |
| HRMS / Payroll           | Calculate average salary, group employees by department           |
| Banking / Finance        | Analyze transactions, detect fraud patterns, generate reports     |
| Social Media / Messaging | Process user messages, filter spam, flatten comment threads       |
| REST APIs                | Convert entities to DTOs, filter responses, remove duplicates     |

---

### **Advantages in Projects**

1. **Cleaner Code:** Avoids verbose loops.
2. **Declarative Style:** Focus on **what to do**, not **how to do it**.
3. **Lazy Evaluation:** Efficient processing of large datasets.
4. **Parallelism:** Easily enable **parallel processing** with `parallelStream()`.
5. **Integration:** Works with **Collections, arrays, and I/O streams**.

---

💡 **Interview Tip:**

> "Stream API is widely used in modern projects for **filtering, mapping, sorting, grouping, and parallel processing** of data collections. It makes code more **readable, maintainable, and efficient**."

---

If you want, I can next explain **practical examples of using Stream API in a real Spring Boot project**, including filtering, mapping, and aggregating data from a database.

Do you want me to cover that next?

---

## 79. Lambda expressions vs Anonymous classes.

### **79. Lambda Expressions vs Anonymous Classes in Java**

Lambda expressions were introduced in **Java 8** to provide a **concise way to implement functional interfaces**. They often replace **anonymous inner classes**. Below is a detailed comparison.

---

## **1. Syntax & Conciseness**

| Feature           | Anonymous Class                                | Lambda Expression                  |
| ----------------- | ---------------------------------------------- | ---------------------------------- |
| **Syntax**        | `new Runnable() { public void run() { ... } }` | `() -> System.out.println("Run");` |
| **Lines of Code** | Verbose, boilerplate code                      | Concise, minimal code              |
| **Readability**   | Less readable for small implementations        | More readable and expressive       |

**Example: Runnable**

```java
// Anonymous Class
Runnable r1 = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello from Anonymous Class");
    }
};
new Thread(r1).start();

// Lambda Expression
Runnable r2 = () -> System.out.println("Hello from Lambda");
new Thread(r2).start();
```

---

## **2. Target**

| Feature    | Anonymous Class                 | Lambda Expression                                                         |
| ---------- | ------------------------------- | ------------------------------------------------------------------------- |
| **Target** | Any interface or abstract class | Only **functional interfaces** (interfaces with a single abstract method) |

---

## **3. `this` Reference**

| Feature            | Anonymous Class                            | Lambda Expression                          |
| ------------------ | ------------------------------------------ | ------------------------------------------ |
| **`this` Keyword** | Refers to the **anonymous class instance** | Refers to the **enclosing class instance** |

**Example:**

```java
class Test {
    void method() {
        Runnable r1 = new Runnable() {
            public void run() {
                System.out.println(this); // Anonymous class instance
            }
        };
        Runnable r2 = () -> System.out.println(this); // Enclosing class instance
    }
}
```

---

## **4. Scope of Variables**

* Both **Anonymous classes** and **Lambda expressions** can access **effectively final local variables**.

**Example:**

```java
int num = 10; // effectively final
Runnable r = () -> System.out.println(num);
```

---

## **5. Performance**

| Feature         | Anonymous Class             | Lambda Expression                                           |
| --------------- | --------------------------- | ----------------------------------------------------------- |
| **Compilation** | Compiled as **inner class** | Can use **invokedynamic**, lighter and optimized at runtime |
| **Memory**      | Slightly heavier            | More memory efficient                                       |

---

## **6. Use Cases**

| Use Case                             | Anonymous Class         | Lambda Expression              |
| ------------------------------------ | ----------------------- | ------------------------------ |
| Implement **multi-method interface** | ✅                       | ❌ (only functional interfaces) |
| Short functional code                | ❌ verbose               | ✅ concise                      |
| Access `this` inside method          | ✅ refers to inner class | ✅ refers to outer class        |

---

## **7. Summary Table**

| Feature              | Anonymous Class                  | Lambda Expression                     |
| -------------------- | -------------------------------- | ------------------------------------- |
| **Syntax**           | Verbose                          | Concise                               |
| **Target**           | Any interface / abstract class   | Only functional interfaces            |
| **`this` reference** | Anonymous class instance         | Enclosing class instance              |
| **Performance**      | Slightly heavier                 | Lighter, optimized                    |
| **Readability**      | Low for small implementations    | High, clean                           |
| **Use Case**         | Complex interfaces, multi-method | Simple functional interfaces, Streams |

---

💡 **Interview Tip:**

> "Use **lambda expressions** for functional interfaces and cleaner code. Anonymous classes are still useful for multi-method interfaces or when `this` needs to refer to the inner class."

---

If you want, I can next explain **Difference between Lambda Expressions and Method References**, which is a common follow-up in Java 8 interviews.

Do you want me to cover that next?

---


# Advance OOP

## 80. What is a Functional Interface?

### **80. What is a Functional Interface in Java**

A **Functional Interface** is a special type of interface in Java that has **exactly one abstract method**. It serves as a **target for lambda expressions or method references**.

---

## **1. Key Characteristics**

1. **Single Abstract Method (SAM):** Must have **only one abstract method**.
2. **Can have default or static methods:** These do not count as abstract methods.
3. **Optional `@FunctionalInterface` annotation:**

   * Ensures the interface **cannot have more than one abstract method**.
   * Compiler will throw an error if violated.
4. **Supports Lambda Expressions:** Can be used wherever a functional interface is expected.

---

## **2. Example**

```java
@FunctionalInterface
interface Calculator {
    int add(int a, int b);  // Single abstract method

    // Default method (optional)
    default void printMessage() {
        System.out.println("Calculator Functional Interface");
    }

    // Static method (optional)
    static void greet() {
        System.out.println("Hello from Calculator");
    }
}
```

**Using Lambda Expression:**

```java
public class FunctionalInterfaceExample {
    public static void main(String[] args) {
        Calculator calculator = (a, b) -> a + b; // Lambda expression
        System.out.println("Sum: " + calculator.add(5, 10)); // Sum: 15

        calculator.printMessage(); // Default method
        Calculator.greet();        // Static method
    }
}
```

---

## **3. Common Functional Interfaces in Java 8+**

| Interface       | Abstract Method           | Purpose                           |
| --------------- | ------------------------- | --------------------------------- |
| `Runnable`      | `void run()`              | Execute code in a thread          |
| `Callable<V>`   | `V call()`                | Execute code that returns a value |
| `Comparator<T>` | `int compare(T o1, T o2)` | Compare objects                   |
| `Consumer<T>`   | `void accept(T t)`        | Perform an operation on `T`       |
| `Supplier<T>`   | `T get()`                 | Provide a value of type `T`       |
| `Function<T,R>` | `R apply(T t)`            | Transform `T` into `R`            |
| `Predicate<T>`  | `boolean test(T t)`       | Test a condition on `T`           |

---

## **4. Key Points**

* Only **one abstract method** allowed.
* Can include **default and static methods**.
* Enables **lambda expressions** and **functional programming** in Java.
* Improves **code readability and conciseness**.

---

💡 **Interview Tip:**

> "A Functional Interface has exactly **one abstract method**. It allows us to use **lambda expressions** and **method references**, making code more concise and readable."

---

If you want, I can next explain **Difference between Functional Interface, Lambda, and Method Reference**, which is often asked together in Java 8 interviews.

---

## 81. What are Sealed Classes (Java 17)?

### **81. Sealed Classes in Java 17**

**Sealed Classes** were introduced in **Java 17** to **restrict which classes or interfaces can extend or implement them**. They provide **more control over inheritance**, making the class hierarchy **more secure and predictable**.

---

## **1. Key Features**

1. **Restrict Subclassing:** Only specific classes or interfaces can extend/implement the sealed class/interface.
2. **`permits` keyword:** Lists the allowed subclasses.
3. **Types of subclasses:**

   * `final` → cannot be subclassed further
   * `non-sealed` → open for further subclassing
   * `sealed` → restrict further subclassing to specific classes
4. Improves **maintainability, security, and exhaustive pattern matching** (with `switch` in Java 17+).

---

## **2. Syntax**

```java
// Sealed class
public sealed class Shape permits Circle, Rectangle, Square {
    // common methods
}

// Final subclass (cannot be extended further)
public final class Circle extends Shape {
    // implementation
}

// Non-sealed subclass (can be extended)
public non-sealed class Rectangle extends Shape {
    // implementation
}

// Another final subclass
public final class Square extends Shape {
    // implementation
}
```

---

## **3. How It Works**

* `Shape` is **sealed**, so only `Circle`, `Rectangle`, and `Square` are allowed as direct subclasses.
* `Circle` and `Square` are **final**, cannot have subclasses.
* `Rectangle` is **non-sealed**, so it can have further subclasses.

**Diagram:**

```
          Shape (sealed)
         /      |       \
   Circle(f) Rectangle(ns) Square(f)
                    |
                  SubRectangle
```

* `(f)` = final
* `(ns)` = non-sealed

---

## **4. Advantages**

| Advantage                       | Explanation                                                                 |
| ------------------------------- | --------------------------------------------------------------------------- |
| **Controlled Inheritance**      | Restricts which classes can extend a class.                                 |
| **Better Design**               | Prevents unwanted subclassing, ensuring a predictable hierarchy.            |
| **Exhaustive Pattern Matching** | Can be used with `switch` expressions to ensure all subclasses are handled. |
| **Improved Security**           | Limits modification or misuse of inheritance in critical systems.           |

---

## **5. Example: Using with `switch` (Java 17+)**

```java
public void printShapeType(Shape shape) {
    switch (shape) {
        case Circle c -> System.out.println("Circle");
        case Rectangle r -> System.out.println("Rectangle");
        case Square s -> System.out.println("Square");
    }
}
```

* No `default` case is needed because the compiler knows all possible subclasses of the **sealed class**.

---

💡 **Interview Tip:**

> "Sealed classes restrict which classes can extend them, improving **security, maintainability, and enabling exhaustive pattern matching**. They are a modern alternative to enums and abstract classes for controlled hierarchies."

---

If you want, I can next explain **Difference between Sealed, Non-sealed, and Final classes in Java 17** with examples.

Do you want me to cover that next?

---

## 82. What is Fail-Fast Iteration & how to handle it?

### **82. Fail-Fast Iteration in Java**

**Fail-Fast Iteration** occurs when a **collection is modified structurally** (add/remove elements) while it is being **iterated**, causing the **iterator to throw a `ConcurrentModificationException`** immediately.

---

## **1. Key Concept**

* **Fail-Fast iterators** detect **concurrent modification** of the collection.
* They **fail immediately** rather than allowing unpredictable behavior.
* Common **fail-fast collections** in Java include:

  * `ArrayList`, `HashMap`, `HashSet`, `LinkedHashMap`, etc.

> Note: Structural modification = adding or removing elements (not changing existing element values).

---

## **2. Example of Fail-Fast**

```java
import java.util.*;

public class FailFastExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>(Arrays.asList("A", "B", "C"));

        for (String s : list) {
            if (s.equals("B")) {
                list.remove(s); // Structural modification while iterating
            }
        }
    }
}
```

**Output:**

```
Exception in thread "main" java.util.ConcurrentModificationException
```

---

## **3. How to Handle Fail-Fast Iteration**

### **a) Using `Iterator`’s `remove()` method**

```java
Iterator<String> iterator = list.iterator();
while (iterator.hasNext()) {
    String s = iterator.next();
    if (s.equals("B")) {
        iterator.remove(); // Safe removal
    }
}
System.out.println(list); // [A, C]
```

* **Key:** Always use the iterator’s `remove()` method, not `list.remove()`, while iterating.

---

### **b) Using `CopyOnWriteArrayList` (Concurrent Collection)**

```java
import java.util.concurrent.CopyOnWriteArrayList;

CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>(Arrays.asList("A", "B", "C"));
for (String s : list) {
    if (s.equals("B")) {
        list.remove(s); // No ConcurrentModificationException
    }
}
System.out.println(list); // [A, C]
```

* `CopyOnWriteArrayList` is **fail-safe**, meaning it **doesn’t throw an exception** during concurrent modifications.
* Trade-off: **Higher memory usage**, as it copies the list on write.

---

### **c) Using `forEach` with `removeIf()`**

```java
list.removeIf(s -> s.equals("B"));
```

* Removes elements **safely without throwing exceptions**.

---

## **4. Fail-Fast vs Fail-Safe**

| Feature         | Fail-Fast                                | Fail-Safe                               |
| --------------- | ---------------------------------------- | --------------------------------------- |
| **Collections** | ArrayList, HashMap, HashSet              | CopyOnWriteArrayList, ConcurrentHashMap |
| **Behavior**    | Throws `ConcurrentModificationException` | Does not throw exception                |
| **Performance** | Faster                                   | Slightly slower due to copying          |

---

💡 **Interview Tip:**

> "Fail-Fast iterators detect concurrent modifications and throw `ConcurrentModificationException`. Handle it safely using **Iterator.remove()**, **removeIf()**, or **fail-safe collections like CopyOnWriteArrayList**."

---

If you want, I can next explain **Difference Between Fail-Fast and Fail-Safe Iterators** with examples, which is a frequently asked interview question.

Do you want me to cover that next?

---

## 83. What is ConcurrentModificationException? Fail safe and fail fast iterators?

### **83. ConcurrentModificationException, Fail-Fast, and Fail-Safe Iterators**

In Java, **modifying a collection while iterating** can lead to **ConcurrentModificationException** or be handled safely depending on the iterator type. Let’s break it down.

---

## **1. What is ConcurrentModificationException (CME)?**

* **Definition:**
  `ConcurrentModificationException` is a **runtime exception** thrown by **fail-fast iterators** when a collection is **structurally modified** during iteration.

* **Structural Modification:**
  Adding or removing elements (not updating element values).

**Example:**

```java
import java.util.*;

public class CMEExample {
    public static void main(String[] args) {
        List<String> list = new ArrayList<>(Arrays.asList("A", "B", "C"));
        
        for (String s : list) {
            if (s.equals("B")) {
                list.remove(s); // Structural modification
            }
        }
    }
}
```

**Output:**

```
Exception in thread "main" java.util.ConcurrentModificationException
```

---

## **2. Fail-Fast Iterators**

* **Behavior:** Detect **concurrent modifications** and **throw `ConcurrentModificationException` immediately**.
* **Collections:**

  * `ArrayList`, `HashMap`, `HashSet`, `LinkedHashMap`, `TreeSet`
* **Key Points:**

  * Use **Iterator’s `remove()`** to safely remove elements.
  * Iteration stops immediately if modification detected.

**Example: Using Iterator.remove() safely**

```java
Iterator<String> iterator = list.iterator();
while (iterator.hasNext()) {
    String s = iterator.next();
    if (s.equals("B")) {
        iterator.remove(); // Safe removal
    }
}
System.out.println(list); // [A, C]
```

---

## **3. Fail-Safe Iterators**

* **Behavior:** Do **not throw `ConcurrentModificationException`** even if collection is modified during iteration.
* **Collections:**

  * `CopyOnWriteArrayList`, `ConcurrentHashMap`, `ConcurrentSkipListMap`
* **Key Points:**

  * Operate on **a copy of the collection** (snapshot).
  * Slower for **write-heavy operations**, but safe for **concurrent reads and writes**.

**Example: Using CopyOnWriteArrayList**

```java
import java.util.concurrent.CopyOnWriteArrayList;

CopyOnWriteArrayList<String> list = new CopyOnWriteArrayList<>(Arrays.asList("A", "B", "C"));

for (String s : list) {
    if (s.equals("B")) {
        list.remove(s); // No exception
    }
}

System.out.println(list); // [A, C]
```

---

## **4. Key Differences: Fail-Fast vs Fail-Safe**

| Feature                    | Fail-Fast                   | Fail-Safe                               |
| -------------------------- | --------------------------- | --------------------------------------- |
| **Throws CME?**            | Yes                         | No                                      |
| **Collections**            | ArrayList, HashMap, HashSet | CopyOnWriteArrayList, ConcurrentHashMap |
| **Modification Detection** | Immediate                   | Works on snapshot                       |
| **Performance**            | Faster                      | Slower (copy overhead)                  |
| **Use Case**               | Single-threaded iteration   | Multi-threaded/concurrent iteration     |

---

💡 **Interview Tip:**

> "Fail-Fast iterators detect structural changes and throw `ConcurrentModificationException`. Fail-Safe iterators work on a **copy of the collection**, so they don’t throw exceptions during concurrent modifications."

---

If you want, I can next explain **real-world use cases of Fail-Fast vs Fail-Safe iterators in projects** with examples.

Do you want me to cover that?

---

## 84. Final, finnaly and finalize().

### **84. Difference Between `final`, `finally`, and `finalize()` in Java**

These three keywords/methods sound similar but have **completely different purposes** in Java.

---

## **1. `final`**

**Type:** Keyword
**Purpose:** Used to **restrict or prevent modification**.

**Uses:**

1. **Final variable:** Value cannot be changed once assigned.

   ```java
   final int x = 10;
   // x = 20; // Compilation error
   ```
2. **Final method:** Cannot be overridden by subclasses.

   ```java
   class Parent {
       final void show() { System.out.println("Hello"); }
   }
   ```
3. **Final class:** Cannot be subclassed.

   ```java
   final class MyClass { }
   ```

---

## **2. `finally`**

**Type:** Block
**Purpose:** Used in **exception handling** to **execute code regardless of whether an exception occurs or not**.

**Key Points:**

* Always executes after `try`/`catch`.
* Useful for **resource cleanup** (closing files, DB connections).

**Example:**

```java
try {
    int data = 10 / 0;
} catch (ArithmeticException e) {
    System.out.println("Exception caught");
} finally {
    System.out.println("Finally block executed"); // Always executed
}
```

**Output:**

```
Exception caught
Finally block executed
```

---

## **3. `finalize()`**

**Type:** Method (from `Object` class)
**Purpose:** Called by **Garbage Collector (GC)** before object is destroyed to **perform cleanup**.

**Key Points:**

* Can be overridden in a class.
* Not guaranteed to run immediately or at all.
* Deprecated in **Java 9+** due to unpredictability.

**Example:**

```java
class Demo {
    @Override
    protected void finalize() throws Throwable {
        System.out.println("Finalize called before GC destroys object");
    }
}

public class TestFinalize {
    public static void main(String[] args) {
        Demo d = new Demo();
        d = null; // Eligible for GC
        System.gc(); // Request GC
    }
}
```

**Output:**

```
Finalize called before GC destroys object
```

*(May vary depending on JVM timing)*

---

## **4. Comparison Table**

| Feature                    | `final`                                            | `finally`                       | `finalize()`                  |
| -------------------------- | -------------------------------------------------- | ------------------------------- | ----------------------------- |
| **Type**                   | Keyword                                            | Block                           | Method                        |
| **Purpose**                | Restrict modification                              | Ensure execution of block       | Cleanup before GC             |
| **Where used**             | Variables, methods, classes                        | try-catch                       | Object class                  |
| **Execution guarantee**    | Compile-time                                       | Always executed after try/catch | Not guaranteed; depends on GC |
| **Overriding/Subclassing** | Final method/class cannot be overridden/subclassed | N/A                             | Can be overridden             |

---

💡 **Interview Tip:**

> "`final` restricts modification, `finally` executes regardless of exceptions, and `finalize()` is called by GC before object destruction."

---

If you want, I can next explain **difference between `final`, `finally`, and `const` (if asked in interviews)**, which sometimes confuses beginners.

Do you want me to cover that next?

---

## 85. Autoboxing vs Unboxing.

### **85. Autoboxing vs Unboxing in Java**

**Autoboxing** and **unboxing** are features in Java that **automatically convert between primitive types and their corresponding wrapper classes**.

---

## **1. Autoboxing**

**Definition:**

* **Automatic conversion of a primitive type into its corresponding wrapper class** by the compiler.

**Example:**

```java
int num = 10;
Integer obj = num; // primitive int → Integer (autoboxing)
System.out.println(obj); // 10
```

**Common Primitive ↔ Wrapper Conversions:**

| Primitive | Wrapper Class |
| --------- | ------------- |
| int       | Integer       |
| double    | Double        |
| char      | Character     |
| boolean   | Boolean       |
| long      | Long          |
| float     | Float         |
| byte      | Byte          |
| short     | Short         |

**When it happens:**

* When assigning a primitive to a variable of its wrapper type.
* When passing a primitive to a method expecting an object.

---

## **2. Unboxing**

**Definition:**

* **Automatic conversion of a wrapper class object into its corresponding primitive type** by the compiler.

**Example:**

```java
Integer obj = 20;
int num = obj; // Integer → int (unboxing)
System.out.println(num); // 20
```

**When it happens:**

* When performing arithmetic operations on wrapper objects.
* When assigning a wrapper object to a primitive type variable.

---

## **3. Examples Together**

```java
Integer a = 10; // Autoboxing
Integer b = 20; // Autoboxing

int sum = a + b; // Unboxing happens here: Integer → int
System.out.println(sum); // 30
```

* **Explanation:**

  * `a` and `b` are **Integer objects** (autoboxed from int).
  * During `a + b`, Java **unboxes** them to `int`, performs addition, and returns `int`.

---

## **4. Key Differences**

| Feature                    | Autoboxing                               | Unboxing                                           |
| -------------------------- | ---------------------------------------- | -------------------------------------------------- |
| **Definition**             | Primitive → Wrapper                      | Wrapper → Primitive                                |
| **Happens Automatically?** | Yes                                      | Yes                                                |
| **Example**                | `int i = 5; Integer obj = i;`            | `Integer obj = 5; int i = obj;`                    |
| **Purpose**                | Use primitives as objects                | Use objects as primitives                          |
| **When Used**              | Assign primitive to wrapper, collections | Assign wrapper to primitive, arithmetic operations |

---

💡 **Interview Tip:**

> "Autoboxing converts **primitive → wrapper**, unboxing converts **wrapper → primitive**. Both happen automatically and are heavily used in **Collections and Java 8 Streams**."

---

If you want, I can next explain **Autoboxing and Unboxing in Collections with performance implications**, which is a commonly asked advanced interview topic.

Do you want me to cover that next?

---

## 86. What is Cloneable? Deep clones vs shallow clones.

### **86. `Cloneable` Interface in Java & Deep vs Shallow Cloning**

Cloning is a way to **create a copy of an existing object** in Java. The `Cloneable` interface and `clone()` method are used for this purpose.

---

## **1. What is `Cloneable`?**

* **Type:** Marker interface (has **no methods**).
* **Purpose:** Indicates that a class **supports cloning** via the `Object.clone()` method.
* **Behavior:**

  * If a class implements `Cloneable`, `Object.clone()` can be called on its objects.
  * If not, `clone()` throws **`CloneNotSupportedException`**.

**Example:**

```java
class Employee implements Cloneable {
    String name;
    int age;

    Employee(String name, int age) {
        this.name = name;
        this.age = age;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // Calls Object.clone()
    }
}

public class CloneExample {
    public static void main(String[] args) throws CloneNotSupportedException {
        Employee e1 = new Employee("Aditya", 25);
        Employee e2 = (Employee) e1.clone(); // Shallow copy

        System.out.println(e1.name); // Aditya
        System.out.println(e2.name); // Aditya
    }
}
```

---

## **2. Shallow Cloning**

**Definition:**

* Copies **only the primitive fields** of the object.
* Copies **references for object fields**, meaning both original and clone share the same referenced objects.

**Example:**

```java
class Department {
    String deptName;

    Department(String deptName) {
        this.deptName = deptName;
    }
}

class Employee implements Cloneable {
    String name;
    Department dept;

    Employee(String name, Department dept) {
        this.name = name;
        this.dept = dept;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // Shallow clone
    }
}

public class ShallowCloneExample {
    public static void main(String[] args) throws CloneNotSupportedException {
        Department d = new Department("IT");
        Employee e1 = new Employee("Aditya", d);
        Employee e2 = (Employee) e1.clone();

        e2.dept.deptName = "HR"; // Changes original object's dept
        System.out.println(e1.dept.deptName); // HR (shared reference)
    }
}
```

**Key Point:** **Object references are shared**, primitive fields are copied.

---

## **3. Deep Cloning**

**Definition:**

* Creates a **full copy of the object**, including **all referenced objects**.
* Original and cloned object are **completely independent**.

**Example:**

```java
class Employee implements Cloneable {
    String name;
    Department dept;

    Employee(String name, Department dept) {
        this.name = name;
        this.dept = dept;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        Employee cloned = (Employee) super.clone();
        cloned.dept = new Department(this.dept.deptName); // Deep copy
        return cloned;
    }
}

public class DeepCloneExample {
    public static void main(String[] args) throws CloneNotSupportedException {
        Department d = new Department("IT");
        Employee e1 = new Employee("Aditya", d);
        Employee e2 = (Employee) e1.clone();

        e2.dept.deptName = "HR"; 
        System.out.println(e1.dept.deptName); // IT (independent copy)
    }
}
```

**Key Point:** **Changes in clone don’t affect original**, as referenced objects are also cloned.

---

## **4. Comparison Table: Shallow vs Deep Cloning**

| Feature               | Shallow Clone                                           | Deep Clone                                 |
| --------------------- | ------------------------------------------------------- | ------------------------------------------ |
| **Copy type**         | Copies **primitive fields only**                        | Copies **primitive + objects recursively** |
| **Reference objects** | Shared                                                  | Independent                                |
| **Modifications**     | Affect original object if object references are changed | Do not affect original object              |
| **Implementation**    | `super.clone()`                                         | `super.clone()` + clone referenced objects |
| **Use case**          | Lightweight copy                                        | Independent objects, complex structures    |

---

💡 **Interview Tip:**

> "Use **shallow cloning** for simple objects with no references. Use **deep cloning** when your object contains other objects and you want a completely independent copy."

---

If you want, I can next explain **alternatives to Cloneable in Java (like copy constructors and serialization for deep copy)**, which is often asked in interviews because `Cloneable` has pitfalls.

Do you want me to cover that?

---

## 87. Shallow Copy vs Deep Copy.

### **87. Shallow Copy vs Deep Copy in Java**

Shallow copy and deep copy are techniques to **duplicate objects**, but they differ in **how object references are handled**.

---

## **1. Shallow Copy**

**Definition:**

* Copies **primitive fields** directly.
* Copies **object references**, not the objects themselves.
* Both the original and copied object **share the same referenced objects**.

**Example:**

```java
class Department {
    String name;
    Department(String name) { this.name = name; }
}

class Employee implements Cloneable {
    String empName;
    Department dept;

    Employee(String empName, Department dept) {
        this.empName = empName;
        this.dept = dept;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // Shallow copy
    }
}

public class ShallowCopyExample {
    public static void main(String[] args) throws CloneNotSupportedException {
        Department d = new Department("IT");
        Employee e1 = new Employee("Aditya", d);
        Employee e2 = (Employee) e1.clone(); // Shallow copy

        e2.dept.name = "HR"; // Modifies original object's department
        System.out.println(e1.dept.name); // HR
    }
}
```

**Key Points:**

* Changes in **object references** in the clone affect the original.
* Quick and uses less memory.

---

## **2. Deep Copy**

**Definition:**

* Copies **primitive fields** and **creates new copies of referenced objects**.
* Original and cloned objects are **completely independent**.

**Example:**

```java
class Employee implements Cloneable {
    String empName;
    Department dept;

    Employee(String empName, Department dept) {
        this.empName = empName;
        this.dept = dept;
    }

    @Override
    protected Object clone() throws CloneNotSupportedException {
        Employee cloned = (Employee) super.clone();
        cloned.dept = new Department(this.dept.name); // Deep copy
        return cloned;
    }
}

public class DeepCopyExample {
    public static void main(String[] args) throws CloneNotSupportedException {
        Department d = new Department("IT");
        Employee e1 = new Employee("Aditya", d);
        Employee e2 = (Employee) e1.clone(); // Deep copy

        e2.dept.name = "HR"; // Original object unaffected
        System.out.println(e1.dept.name); // IT
    }
}
```

**Key Points:**

* Changes in the clone **do not affect** the original object.
* Safer but **slightly more memory-intensive**.

---

## **3. Comparison Table: Shallow vs Deep Copy**

| Feature               | Shallow Copy                                         | Deep Copy                                                        |
| --------------------- | ---------------------------------------------------- | ---------------------------------------------------------------- |
| **Copied fields**     | Primitive fields and references                      | Primitive fields and new copies of referenced objects            |
| **Shared references** | Yes                                                  | No                                                               |
| **Effect of changes** | Changes in clone affect original (for object fields) | Changes in clone do not affect original                          |
| **Implementation**    | `super.clone()`                                      | `super.clone()` + clone referenced objects                       |
| **Performance**       | Faster                                               | Slower due to object duplication                                 |
| **Use Case**          | Lightweight objects with no internal references      | Objects with complex nested objects that need independent copies |

---

💡 **Interview Tip:**

> "Shallow copy copies references; deep copy creates independent objects. Use deep copy when your object has nested objects and modifications to the clone should not affect the original."

---

I can next explain **practical ways to implement deep copy in Java using serialization, copy constructors, and libraries**, which is a common follow-up in interviews.

Do you want me to cover that?

---


# Memory Management

## 88. Explain Java Memory Management.

### **88. Java Memory Management**

Java memory management is the process by which the **JVM manages memory allocation and deallocation** for Java applications. It ensures **efficient memory usage** and helps in **garbage collection** of unused objects.

---

## **1. Memory Areas in JVM**

JVM divides memory into **five main regions**:

| Memory Area                           | Purpose                                                                    |
| ------------------------------------- | -------------------------------------------------------------------------- |
| **Heap**                              | Stores **objects and class instances**. Managed by Garbage Collector (GC). |
| **Stack**                             | Stores **method calls and local variables**. Follows **LIFO** order.       |
| **Method Area (PermGen / Metaspace)** | Stores **class metadata, static variables, and constants**.                |
| **Program Counter (PC) Register**     | Keeps **address of the currently executing instruction**.                  |
| **Native Method Stack**               | Stores **native method calls** (like C/C++ code called from Java).         |

---

## **2. Heap Memory**

* **Stores:** Objects, arrays, and class instances.
* **Divided into:**

  1. **Young Generation (Eden + Survivor Spaces):** New objects created here.

     * Most objects die quickly → minor GC happens frequently.
  2. **Old (Tenured) Generation:** Long-lived objects moved here from Young Generation.

     * Major GC occurs less frequently but takes longer.
  3. **Permanent Generation / Metaspace:** Class definitions, method info, static variables.

---

## **3. Stack Memory**

* Stores **method frames** containing:

  * Local primitive variables
  * References to objects in heap
  * Return addresses
* Automatically **pushed** on method call and **popped** on method return.
* **Thread-safe:** Each thread has its own stack.

**Example:**

```java
void method() {
    int x = 10; // stored in stack
    Employee e = new Employee(); // reference in stack, object in heap
}
```

---

## **4. Garbage Collection (GC)**

* **Purpose:** Automatically frees **memory of objects no longer referenced**.
* **Types of GC in JVM:**

  1. **Minor GC:** Cleans **Young Generation** (frequent).
  2. **Major GC / Full GC:** Cleans **Old Generation** (less frequent, expensive).

**Popular GC Algorithms:**

* Serial GC
* Parallel GC
* CMS (Concurrent Mark Sweep)
* G1 (Garbage First, Java 9+)

---

## **5. Object Life Cycle in JVM**

1. **Creation:** Object allocated in heap (usually Young Generation).
2. **Reference:** Object is used by application code.
3. **Garbage:** If **no live references exist**, object becomes unreachable.
4. **GC:** JVM automatically removes unreachable objects to free memory.

---

## **6. Memory Management Principles**

1. **Automatic Memory Management:** No manual memory allocation/deallocation like C/C++.
2. **Stack vs Heap:** Primitives and references → stack; actual objects → heap.
3. **Finalization:** `finalize()` called (deprecated in Java 9+) before GC may destroy object.
4. **Avoid Memory Leaks:**

   * Remove unnecessary references
   * Close resources (I/O, DB connections)
   * Use weak references if needed

---

## **7. Key Points for Interviews**

* JVM manages **Heap, Stack, Method Area, PC Register, Native Stack**.
* **Stack** is thread-local; **Heap** is shared among threads.
* **Garbage Collector** automatically reclaims memory.
* Use **try-with-resources** and avoid unnecessary references to help memory management.

---

💡 **Example Diagram:**

```
            JVM Memory
  -------------------------------
  Method Area: Class info, static
  Heap: Objects, arrays
      Young Gen (Eden + Survivor)
      Old Gen (Tenured)
  Stack: Method frames, local vars
  PC Register: Current instruction
  Native Stack: Native calls
```

---

If you want, I can next explain **Java Stack vs Heap in detail with memory allocation examples and how GC works internally**, which is a common follow-up in interviews.

Do you want me to cover that next?

---

## 89. What is garbage collection in Java? Types of GC?

### **89. Garbage Collection (GC) in Java**

Garbage Collection in Java is the **process of automatically freeing memory** by removing objects that are **no longer reachable** from the application. It helps **prevent memory leaks** and ensures **efficient memory utilization**.

---

## **1. What is Garbage Collection?**

* **Definition:** Automatic memory management mechanism in Java **handled by the JVM**.
* **Purpose:** Reclaims memory from objects that are **no longer in use**, so developers **don’t need to manually free memory** like in C/C++.
* **Trigger:** JVM decides when to run GC based on **heap usage**.
* **Method:** Objects with **no live references** are considered **garbage**.

**Example:**

```java
public class GCDemo {
    public static void main(String[] args) {
        Employee e1 = new Employee("Aditya");
        e1 = null; // Object becomes unreachable, eligible for GC

        System.gc(); // Suggests JVM to run GC
        System.out.println("End of main");
    }
}
```

> Note: `System.gc()` **only suggests** the JVM to run GC; it’s not guaranteed.

---

## **2. How Garbage Collection Works**

1. **Object Creation:** Objects allocated in **Heap memory** (usually Young Generation).
2. **Reference Checking:** JVM tracks **references to objects**.
3. **Marking:** Identifies objects **no longer reachable**.
4. **Sweeping/Deleting:** Removes unreachable objects from heap.
5. **Compacting (optional):** Moves surviving objects together to **reduce fragmentation**.

---

## **3. Types of Garbage Collectors in Java**

### **a) Serial Garbage Collector**

* **Single-threaded GC** → pauses application threads during GC (Stop-the-world).
* **Best for:** Small applications or single-core machines.
* **Flag:** `-XX:+UseSerialGC`

### **b) Parallel Garbage Collector (Throughput Collector)**

* Uses **multiple threads** for minor GC.
* Stops all application threads during GC but faster than Serial GC.
* **Best for:** Multi-threaded applications with high throughput.
* **Flag:** `-XX:+UseParallelGC`

### **c) Concurrent Mark Sweep (CMS) Collector**

* Performs GC **concurrently with application threads**.
* Goal: **Low pause times**.
* Steps:

  1. Initial Mark (stop-the-world)
  2. Concurrent Mark
  3. Remark (stop-the-world)
  4. Concurrent Sweep
* **Flag:** `-XX:+UseConcMarkSweepGC`

### **d) G1 (Garbage-First) Collector**

* Splits heap into **regions** and collects **regions with most garbage first**.
* **Concurrent and parallel GC** → low pause time and predictable performance.
* Default in **Java 9+**.
* **Flag:** `-XX:+UseG1GC`

### **e) ZGC (Java 11+) & Shenandoah (Java 12+)**

* **Low-latency concurrent collectors** for **huge heaps (multi-GB to TB)**.
* Aim: **sub-millisecond pause times** for large applications.

---

## **4. Key Terms in GC**

| Term                         | Meaning                                  |
| ---------------------------- | ---------------------------------------- |
| **Young Generation**         | New objects; frequent minor GC           |
| **Eden Space**               | Where new objects are allocated          |
| **Survivor Space**           | Objects surviving minor GC moved here    |
| **Old Generation (Tenured)** | Long-lived objects; major GC occurs here |
| **Permanent/Metaspace**      | Class definitions, static variables      |
| **Stop-the-world**           | Application threads paused during GC     |

---

## **5. Summary Table: GC Types**

| GC Type    | Threads               | Pause Time | Best For                 | Java Flag                 |
| ---------- | --------------------- | ---------- | ------------------------ | ------------------------- |
| Serial     | Single                | High       | Small apps               | `-XX:+UseSerialGC`        |
| Parallel   | Multi                 | Medium     | Multi-threaded           | `-XX:+UseParallelGC`      |
| CMS        | Concurrent            | Low        | Low-latency apps         | `-XX:+UseConcMarkSweepGC` |
| G1         | Concurrent + Parallel | Low        | Predictable, large heaps | `-XX:+UseG1GC`            |
| ZGC        | Concurrent            | Very Low   | Very large heaps         | `-XX:+UseZGC`             |
| Shenandoah | Concurrent            | Very Low   | Large heaps              | `-XX:+UseShenandoahGC`    |

---

💡 **Interview Tip:**

> "Garbage Collection in Java automatically frees unreachable objects. Serial, Parallel, CMS, G1, ZGC, and Shenandoah are common collectors, each optimized for throughput, low pause, or large heaps."

---

If you want, I can next explain **Java Generational GC (Young, Old, Survivor spaces) with an example of object life cycle**, which is a very common follow-up question.

Do you want me to cover that?

---

## 90. What is the finalize() method?

### **90. `finalize()` Method in Java**

The `finalize()` method is part of Java’s **garbage collection mechanism** and is called **by the Garbage Collector before an object is destroyed**.

---

## **1. Definition**

* **Method signature:**

```java
protected void finalize() throws Throwable
```

* **Purpose:** Allows an object to **clean up resources** (like closing files, releasing DB connections) **before it is garbage collected**.
* Declared in the **`Object` class**, so **every class inherits it**.

---

## **2. Key Points**

1. **Called by Garbage Collector**

   * JVM calls `finalize()` **automatically** when GC determines the object is unreachable.

2. **Not guaranteed to run immediately**

   * Timing is unpredictable; object may linger in memory before GC runs.

3. **Overridable**

   * You can override it to define custom cleanup behavior.

4. **Deprecated**

   * `finalize()` is deprecated since **Java 9** due to **unpredictable behavior** and performance issues.
   * Recommended alternatives: **try-with-resources** or **explicit cleanup methods**.

---

## **3. Example**

```java
class Demo {
    @Override
    protected void finalize() throws Throwable {
        System.out.println("Finalize method called before GC destroys object");
    }
}

public class FinalizeExample {
    public static void main(String[] args) {
        Demo d1 = new Demo();
        d1 = null; // Object becomes eligible for GC

        System.gc(); // Suggests JVM to run GC
        System.out.println("End of main");
    }
}
```

**Possible Output:**

```
End of main
Finalize method called before GC destroys object
```

> Note: Output may vary because GC runs at JVM’s discretion.

---

## **4. Use Cases**

* **Cleaning up non-memory resources**: Closing file streams, network sockets, database connections.
* **Logging object destruction** (rarely).

**Better Alternatives:**

* **Try-with-resources** for automatic closing of I/O resources.
* Explicit **cleanup methods** (e.g., `close()`).

---

## **5. Difference Between `finalize()` and `finally`**

| Feature         | finalize()                        | finally                              |
| --------------- | --------------------------------- | ------------------------------------ |
| **Type**        | Method                            | Block                                |
| **Called by**   | JVM GC                            | Program flow (try-catch)             |
| **Purpose**     | Cleanup before object destruction | Cleanup after try-catch execution    |
| **Guaranteed?** | No                                | Yes                                  |
| **Usage**       | Object resource cleanup           | Exception handling, resource release |

---

💡 **Interview Tip:**

> "`finalize()` is called by the GC before object destruction, but its execution is unpredictable. Use `try-with-resources` or explicit cleanup methods instead of relying on `finalize()`."

---

I can next explain **Java Stack vs Heap memory with examples of object allocation and how finalize() fits into GC**, which often comes up in interviews.

Do you want me to cover that?

---

## 91. Stack vs Heap Memory Allocation.

### **91. Stack vs Heap Memory Allocation in Java**

Java memory is divided mainly into **Stack** and **Heap**, and understanding their differences is crucial for performance, object lifecycle, and garbage collection.

---

## **1. Stack Memory**

* **Purpose:** Stores **method execution context**, local variables, and references to objects.
* **Characteristics:**

  1. **LIFO (Last-In-First-Out):** Each method call pushes a frame onto the stack; method return pops it.
  2. **Automatic memory management:** Memory is **freed automatically** when method exits.
  3. **Thread-local:** Each thread has its **own stack**.
  4. **Stores:**

     * Primitive data types (int, char, boolean, etc.)
     * References to objects in **heap**
  5. **Size:** Smaller, fixed per thread (StackOverflow can occur if too deep recursion).

**Example:**

```java
public class StackExample {
    void methodA() {
        int x = 10; // stored in stack
        methodB();
    }

    void methodB() {
        int y = 20; // stored in stack
    }

    public static void main(String[] args) {
        StackExample obj = new StackExample(); // reference in stack, object in heap
        obj.methodA();
    }
}
```

* Here, **`x` and `y` live in the stack**, while the `StackExample` object itself is in the **heap**.

---

## **2. Heap Memory**

* **Purpose:** Stores **objects and class instances** created with `new`.
* **Characteristics:**

  1. Shared among all threads.
  2. **Dynamic memory allocation**: Objects live until **Garbage Collector** removes them.
  3. Can be divided into:

     * **Young Generation (Eden + Survivor spaces)** → new objects
     * **Old Generation (Tenured)** → long-lived objects
     * **Metaspace** → class metadata, static variables
  4. **Slower access** than stack due to dynamic memory allocation.

**Example:**

```java
Employee e = new Employee("Aditya", 25); 
// 'e' reference stored in stack, actual Employee object in heap
```

---

## **3. Key Differences: Stack vs Heap**

| Feature               | Stack                                      | Heap                                        |
| --------------------- | ------------------------------------------ | ------------------------------------------- |
| **Stores**            | Method calls, local primitives, references | Objects, arrays, class instances            |
| **Memory Allocation** | Static, LIFO                               | Dynamic                                     |
| **Lifetime**          | Until method returns                       | Until object is garbage collected           |
| **Access Time**       | Faster                                     | Slower                                      |
| **Thread Safety**     | Thread-local (safe)                        | Shared among threads (need synchronization) |
| **Size**              | Smaller                                    | Larger                                      |
| **Error**             | StackOverflowError                         | OutOfMemoryError                            |

---

## **4. Object Lifecycle in Stack & Heap**

1. **Object creation:** `new Employee()` → object allocated in **heap**.
2. **Reference variable:** Stored in **stack**.
3. **Method call:** Stack frame created for local variables & references.
4. **Method exit:** Stack frame destroyed, heap object remains if referenced elsewhere.
5. **Garbage collection:** Object in heap removed if no references exist.

**Diagram:**

```
Stack (per thread)              Heap (shared)
-----------------              -----------------
methodA() frame                 Employee Object
  x=10                          name="Aditya"
  ref->Employee e               age=25
```

---

💡 **Interview Tip:**

> "Stack memory is for method execution and local variables (fast, thread-safe), heap memory is for objects (shared, managed by GC). Knowing the difference helps in understanding memory leaks, GC behavior, and performance issues."

---

I can next explain **Young Generation, Old Generation, Survivor Spaces, and how Garbage Collector works in Heap**, which is a common follow-up question in interviews.

Do you want me to cover that?

---

## 92. How to handle OutOfMemoryException?

### **92. How to Handle `OutOfMemoryError` in Java**

An **`OutOfMemoryError` (OOM)** occurs when the JVM **cannot allocate memory** for objects because the **heap is full**. This is a **runtime error**, not an exception, and usually indicates a memory leak or insufficient memory.

---

## **1. Causes of OutOfMemoryError**

1. **Heap Space Exhaustion**

   * Too many objects allocated in **heap**.
   * Example: Creating a large `ArrayList` without limit.

2. **Metaspace / PermGen Exhaustion**

   * Too many classes loaded dynamically (reflection, class loaders).
   * In Java 8+, PermGen is replaced by Metaspace.

3. **Stack Overflow (deep recursion)**

   * Caused by **StackOverflowError**, sometimes confused with OOM.

4. **Native Memory Exhaustion**

   * Excessive use of native libraries or direct buffers.

---

## **2. Common Scenarios**

```java
// Example of Heap OOM
List<Integer> list = new ArrayList<>();
while(true) {
    list.add(1); // Keeps allocating memory
}
```

**Symptoms:**

* Application crashes with `java.lang.OutOfMemoryError: Java heap space`.
* High GC activity but heap still full.

---

## **3. How to Handle/Prevent OOM**

### **a) Increase JVM Heap Size**

* Use JVM options to allocate more memory:

```bash
java -Xms512m -Xmx2g MyApp
```

* `-Xms` → initial heap size
* `-Xmx` → maximum heap size

### **b) Optimize Code & Data Structures**

* Avoid holding unnecessary references.
* Use **efficient data structures** (`LinkedList`, `HashMap` with correct initial capacity).
* Clear collections when no longer needed:

```java
list.clear();
```

### **c) Use Garbage Collector Wisely**

* Enable **GC logs** to analyze memory usage:

```bash
-XX:+PrintGCDetails -XX:+PrintGCDateStamps -Xloggc:gc.log
```

* Use appropriate GC for your workload (G1, Parallel, CMS, ZGC).

### **d) Avoid Memory Leaks**

* Release references in **long-lived objects**.
* Close **streams, connections, threads** properly.
* Use **weak references** for caches:

```java
Map<String, WeakReference<Employee>> cache = new HashMap<>();
```

### **e) Profile Memory Usage**

* Tools: **VisualVM, JConsole, JProfiler, YourKit**
* Identify objects consuming most memory, memory leaks, or infinite loops creating objects.

### **f) Handle Large Data Efficiently**

* Process large files in **chunks/streams** rather than loading entirely into memory.
* Use **pagination for DB queries**.

---

## **4. Catching OutOfMemoryError**

* You **can catch OOM**, but it's generally **not recommended**, as JVM may be unstable.

```java
try {
    List<Integer> list = new ArrayList<>();
    while(true) list.add(1);
} catch (OutOfMemoryError e) {
    System.out.println("Memory full! Consider increasing heap size.");
}
```

* Better approach: Prevent it rather than catching it.

---

## **5. Summary**

| Solution                  | Description                                  |
| ------------------------- | -------------------------------------------- |
| Increase Heap Size        | `-Xmx` and `-Xms` JVM options                |
| Optimize Code             | Avoid unnecessary objects, clear collections |
| GC Tuning                 | Use appropriate GC algorithm                 |
| Profile Memory            | Identify memory leaks using tools            |
| Efficient Data Processing | Streams, pagination, chunk processing        |
| Avoid Catching OOM        | Only use as last resort; JVM may be unstable |

---

💡 **Interview Tip:**

> "OutOfMemoryError happens when JVM cannot allocate memory. Avoid it by **optimizing memory usage, tuning heap, closing resources**, and analyzing memory leaks with profiling tools."

---

I can next explain **Java Memory Leaks: Common causes and how to detect/fix them**, which is often asked after OOM questions.

Do you want me to cover that?

---


# Multithreading Basics

## 93. What is multithreading in Java? Thread lifecycle?

### **93. Multithreading in Java & Thread Lifecycle**

Multithreading is one of the core concepts in Java for **concurrent execution of two or more threads** to **maximize CPU utilization** and improve performance.

---

## **1. What is Multithreading?**

* **Definition:** Multithreading is the ability of a program to **execute multiple threads concurrently** within a single process.
* **Thread:** A **lightweight sub-process**; each thread has its own **stack memory** but shares **heap memory** with other threads.
* **Use Cases:**

  * Performing background tasks (file I/O, network calls)
  * Parallel computations
  * GUI responsiveness
  * Server handling multiple client requests

**Example:**

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

public class MultithreadingDemo {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        t1.start();
        t2.start();
    }
}
```

* `t1` and `t2` run **concurrently**.
* `run()` method contains the **thread execution logic**.

---

## **2. Ways to Create Threads**

| Approach                            | Description                                               | Example                                |
| ----------------------------------- | --------------------------------------------------------- | -------------------------------------- |
| **Extending Thread class**          | Create a class that extends `Thread` and override `run()` | `class MyThread extends Thread`        |
| **Implementing Runnable interface** | Implement `Runnable` and pass instance to `Thread`        | `new Thread(new MyRunnable()).start()` |
| **Callable & Future**               | Returns a result and can throw exceptions                 | `ExecutorService.submit(Callable)`     |

---

## **3. Thread Lifecycle in Java**

A Java thread **transitions through different states** defined in the `Thread.State` enum:

1. **New (Created)**

   * Thread object is created using `Thread t = new Thread()`.
   * `start()` not yet called.

2. **Runnable**

   * `start()` called → thread is **ready to run**.
   * Scheduler decides when it actually runs.

3. **Running**

   * Thread scheduler selects the thread → `run()` executes.

4. **Blocked / Waiting**

   * Thread **cannot continue execution** until some condition is met (e.g., waiting for I/O, synchronization lock).

5. **Timed Waiting**

   * Thread waits for **a specified time** (e.g., `sleep()`, `join(timeout)`, `wait(timeout)`).

6. **Terminated (Dead)**

   * `run()` method completes or thread is stopped → cannot restart.

**Diagram:**

```
       New
        |
      start()
        |
     Runnable <--> Running
        |          |
      wait(),      sleep()
      join()
        |
     Waiting / Timed Waiting
        |
     notify()/time out
        |
     Runnable
        |
     Terminated
```

---

## **4. Common Thread Methods**

| Method             | Description                                             |
| ------------------ | ------------------------------------------------------- |
| `start()`          | Begins thread execution and calls `run()`               |
| `run()`            | Contains thread logic                                   |
| `sleep(ms)`        | Pauses thread for specified milliseconds                |
| `join()`           | Waits for this thread to finish                         |
| `yield()`          | Suggests thread scheduler to give CPU to another thread |
| `setPriority(int)` | Sets thread priority (1–10)                             |
| `interrupt()`      | Interrupts a thread in waiting/sleep state              |

---

## **5. Thread States Example**

```java
public class ThreadStateDemo {
    public static void main(String[] args) throws InterruptedException {
        Thread t = new Thread(() -> {
            try {
                Thread.sleep(1000);
            } catch (InterruptedException e) {}
        });

        System.out.println("State: " + t.getState()); // NEW
        t.start();
        System.out.println("State: " + t.getState()); // RUNNABLE
        Thread.sleep(500);
        System.out.println("State: " + t.getState()); // TIMED_WAITING
        Thread.sleep(1000);
        System.out.println("State: " + t.getState()); // TERMINATED
    }
}
```

---

💡 **Interview Tip:**

> "Multithreading allows concurrent execution, improving CPU utilization. Remember thread **lifecycle states** (NEW → RUNNABLE → RUNNING → WAITING/TIMED_WAITING → TERMINATED) and the differences between **Runnable vs Thread vs Callable**."

---

I can next explain **Thread Synchronization, Locks, and Thread Safety**, which is the natural continuation after thread lifecycle.

Do you want me to cover that?

---

## 94. What is synchronization in Java? synchronized keyword.

### **94. Synchronization in Java & `synchronized` Keyword**

Synchronization in Java is a mechanism that **controls access to shared resources by multiple threads** to ensure **data consistency and thread safety**.

---

## **1. What is Synchronization?**

* **Definition:** Synchronization is the process of **allowing only one thread at a time** to access a **critical section** (shared resource).
* **Purpose:** Prevent **race conditions**, **data inconsistency**, and **thread interference** when multiple threads access the same object or variable.

**Example Problem (Race Condition):**

```java
class Counter {
    int count = 0;

    void increment() {
        count++; // Not thread-safe
    }
}

public class RaceConditionDemo {
    public static void main(String[] args) throws InterruptedException {
        Counter c = new Counter();
        Runnable r = () -> {
            for(int i=0; i<1000; i++) c.increment();
        };

        Thread t1 = new Thread(r);
        Thread t2 = new Thread(r);

        t1.start();
        t2.start();
        t1.join();
        t2.join();

        System.out.println(c.count); // Might be < 2000 due to race condition
    }
}
```

* Multiple threads **interleave** and cause **incorrect results**.

---

## **2. `synchronized` Keyword**

* **Purpose:** Ensures that **only one thread at a time executes a synchronized method/block**.
* **Can be applied to:**

  1. **Instance methods** → locks the **object instance**.
  2. **Static methods** → locks the **class object**.
  3. **Code blocks** → locks the **specified object**.

---

### **a) Synchronized Instance Method**

```java
class Counter {
    int count = 0;

    synchronized void increment() { // locks this object
        count++;
    }
}
```

* Only one thread can execute `increment()` on the **same object** at a time.
* Different objects can still execute concurrently.

---

### **b) Synchronized Static Method**

```java
class Counter {
    static int count = 0;

    synchronized static void increment() { // locks Counter.class
        count++;
    }
}
```

* Locks the **class object** → prevents multiple threads from executing **any synchronized static method** simultaneously.

---

### **c) Synchronized Block**

```java
class Counter {
    int count = 0;

    void increment() {
        synchronized(this) { // only locks this block
            count++;
        }
    }
}
```

* Useful when **only part of the method needs synchronization** → improves performance.

**Alternative: Lock on a specific object**

```java
synchronized(lockObject) { 
    // critical section
}
```

---

## **3. Key Points**

1. **Locks:**

   * Object-level locks for **instance methods/blocks**.
   * Class-level locks for **static methods**.

2. **Reentrancy:**

   * Java’s synchronization is **reentrant**: a thread can acquire the same lock multiple times.

3. **Performance:**

   * Excessive synchronization can **slow down the application** due to thread contention.

4. **Thread Safety:**

   * Synchronization ensures **mutual exclusion**, preventing race conditions.

---

## **4. Example: Thread-Safe Counter**

```java
class Counter {
    private int count = 0;

    public synchronized void increment() { // synchronized method
        count++;
    }

    public int getCount() {
        return count;
    }
}

public class SyncDemo {
    public static void main(String[] args) throws InterruptedException {
        Counter c = new Counter();
        Runnable r = () -> {
            for(int i=0; i<1000; i++) c.increment();
        };

        Thread t1 = new Thread(r);
        Thread t2 = new Thread(r);

        t1.start();
        t2.start();
        t1.join();
        t2.join();

        System.out.println(c.getCount()); // 2000
    }
}
```

* `synchronized` ensures **correct count** even with multiple threads.

---

## **5. Summary Table**

| Feature                 | Description                                           |
| ----------------------- | ----------------------------------------------------- |
| **synchronized method** | Locks **entire method** for an object or class        |
| **synchronized block**  | Locks **only part** of the method, better performance |
| **Locks**               | Object-level for instance, Class-level for static     |
| **Thread Safety**       | Prevents race conditions                              |
| **Reentrancy**          | Thread can re-acquire the same lock                   |

---

💡 **Interview Tip:**

> "`synchronized` is used for mutual exclusion on shared resources. Prefer **synchronized blocks** over methods for better performance. For high-performance concurrent programs, consider `java.util.concurrent` locks or atomic classes instead of `synchronized`."

---

I can next explain **ReentrantLock, ReadWriteLock, and atomic classes** in Java, which are advanced alternatives to `synchronized` often asked in interviews.

Do you want me to cover that?

---

## 95. What is the difference between wait() and sleep()?

### **95. Difference Between `wait()` and `sleep()` in Java**

Both `wait()` and `sleep()` are used to **pause thread execution**, but they have **different purposes and behaviors**.

---

## **1. `sleep()` Method**

* **Definition:** Pauses the thread for a **specific time**.
* **Belongs to:** `Thread` class.
* **Usage:**

```java
Thread.sleep(milliseconds);
```

* **Key Points:**

  1. **Does not release any lock:** If the thread holds a lock (synchronized block), it **keeps the lock**.
  2. **Can be interrupted:** Throws `InterruptedException`.
  3. **Static method:** Called as `Thread.sleep(ms)` (not on thread object).
  4. **Purpose:** Timing or delaying execution.

**Example:**

```java
System.out.println("Start");
Thread.sleep(2000); // Sleep 2 seconds
System.out.println("End");
```

---

## **2. `wait()` Method**

* **Definition:** Causes a thread to **wait until another thread calls `notify()` or `notifyAll()`** on the same object.
* **Belongs to:** `Object` class.
* **Usage:**

```java
synchronized(obj) {
    obj.wait(); // Releases the lock and waits
}
```

* **Key Points:**

  1. **Must be inside synchronized block:** Thread must **hold the object lock**.
  2. **Releases the lock:** Thread **releases the monitor** and waits for notification.
  3. **Used for inter-thread communication** between producer-consumer type problems.
  4. Can optionally specify timeout: `obj.wait(1000)`

**Example (Producer-Consumer):**

```java
synchronized(queue) {
    while(queue.isEmpty()) {
        queue.wait(); // Wait until producer adds element
    }
}
```

---

## **3. Key Differences**

| Feature                        | `sleep()`                     | `wait()`                        |
| ------------------------------ | ----------------------------- | ------------------------------- |
| **Class**                      | `Thread`                      | `Object`                        |
| **Releases Lock**              | No                            | Yes                             |
| **Needs Synchronization**      | No                            | Yes (must hold object monitor)  |
| **Purpose**                    | Pause execution for some time | Wait for condition/notification |
| **Inter-thread Communication** | No                            | Yes                             |
| **Can be Interrupted**         | Yes (`InterruptedException`)  | Yes (`InterruptedException`)    |
| **Static/Instance**            | Static method                 | Instance method                 |

---

## **4. Summary**

* **Use `sleep()`** when you want the **current thread to pause for a fixed time**, usually for timing or delay purposes.
* **Use `wait()`** when you want the thread to **pause until a certain condition is met**, typically for **thread coordination** (like producer-consumer problems).

---

💡 **Interview Tip:**

> "`sleep()` pauses the thread without releasing locks, while `wait()` pauses the thread and releases the object lock for other threads to access shared resources."

---

I can next explain **notify() vs notifyAll() and how wait/notify mechanism works with producer-consumer problem**, which is commonly asked after wait/sleep questions.

Do you want me to cover that?

---

## 96. What is the volatile keyword?

### **96. `volatile` Keyword in Java**

The `volatile` keyword in Java is used to **indicate that a variable’s value will be modified by multiple threads** and ensures **visibility of changes across threads**.

---

## **1. Definition**

* **`volatile`** is a **modifier** applied to **variables**.
* **Purpose:** Guarantees that **any read of a volatile variable reflects the most recent write by any thread**.
* **Syntax:**

```java
volatile int counter;
```

---

## **2. Key Characteristics**

1. **Visibility Guarantee**

   * Changes made by one thread to a volatile variable are **immediately visible** to other threads.
   * Without `volatile`, threads may read **stale cached values** from CPU caches.

2. **No Atomicity**

   * Operations like `counter++` are **not atomic**, even if the variable is volatile.
   * Use `AtomicInteger` or synchronized block for atomic operations.

3. **Cannot Be Used With Methods or Classes**

   * Only applies to **instance or static variables**.

4. **Lightweight Alternative to Synchronization**

   * Suitable when you **only need visibility** without mutual exclusion.

---

## **3. Example**

```java
class VolatileDemo {
    private volatile boolean running = true;

    public void stop() {
        running = false;
    }

    public void run() {
        while(running) {
            // Do some work
        }
        System.out.println("Thread stopped.");
    }
}

public class Main {
    public static void main(String[] args) throws InterruptedException {
        VolatileDemo demo = new VolatileDemo();

        Thread t = new Thread(() -> demo.run());
        t.start();

        Thread.sleep(1000);
        demo.stop(); // Without volatile, t may not see this change immediately
    }
}
```

* **Without `volatile`**, the thread `t` may **never see** the updated value of `running` due to CPU caching.

---

## **4. When to Use `volatile`**

* **Flags or signals** between threads (like `running` in above example).
* **Single variable updates** where **atomicity is not required**.
* **Lightweight alternative** to synchronization for visibility.

---

## **5. When Not to Use `volatile`**

* **Compound operations** (`count++`, `count += 5`) → Not atomic, can cause race conditions.
* **Complex invariants** involving multiple variables → Use synchronized blocks or locks.

---

## **6. Summary Table**

| Feature         | Volatile                                             |
| --------------- | ---------------------------------------------------- |
| **Visibility**  | Yes, changes visible across threads immediately      |
| **Atomicity**   | No (compound operations are not atomic)              |
| **Applies to**  | Variables only (instance or static)                  |
| **Alternative** | Synchronization for atomic operations                |
| **Use Case**    | Flags, state indicators, lightweight shared variable |

---

💡 **Interview Tip:**

> "`volatile` ensures visibility of variable changes across threads, but does not provide atomicity. For atomic updates, use `AtomicInteger` or synchronized blocks."

---

I can next explain **`synchronized` vs `volatile` differences**, which is a common follow-up question in Java multithreading.

Do you want me to cover that?

---

## 97. What is ThreadLocal?

### **97. `ThreadLocal` in Java**

`ThreadLocal` is a special class in Java that provides **thread-local variables**. Each thread accessing a `ThreadLocal` variable **has its own independent copy**, which is not shared with other threads.

---

## **1. Definition**

* **Class:** `java.lang.ThreadLocal<T>`
* **Purpose:** Store **per-thread data**, like user sessions, transaction contexts, or request IDs, without using synchronization.
* **Each thread gets its own copy** of the variable, isolated from others.

**Syntax:**

```java
ThreadLocal<Integer> threadLocalVar = new ThreadLocal<>();
```

---

## **2. Key Methods**

| Method           | Description                                                                                        |
| ---------------- | -------------------------------------------------------------------------------------------------- |
| `get()`          | Returns the **current thread’s value** of the ThreadLocal variable                                 |
| `set(T value)`   | Sets the **current thread’s value** of the variable                                                |
| `remove()`       | Removes the value for the current thread (helps avoid memory leaks)                                |
| `initialValue()` | Returns the **initial value** for the thread when `get()` is called first time (can be overridden) |

---

## **3. Example**

```java
public class ThreadLocalExample {
    private static ThreadLocal<Integer> threadLocal = ThreadLocal.withInitial(() -> 0);

    public static void main(String[] args) {
        Runnable task = () -> {
            int value = threadLocal.get();
            value += 5;
            threadLocal.set(value);
            System.out.println(Thread.currentThread().getName() + ": " + threadLocal.get());
        };

        Thread t1 = new Thread(task, "Thread-1");
        Thread t2 = new Thread(task, "Thread-2");

        t1.start();
        t2.start();
    }
}
```

**Possible Output:**

```
Thread-1: 5
Thread-2: 5
```

* Each thread has **its own copy** of the variable.
* No **synchronization** needed.

---

## **4. Use Cases of ThreadLocal**

1. **User Session Management** in web applications.
2. **Database Connection / Transaction Management** (one connection per thread).
3. **Logging Contexts** (like `log4j` MDC).
4. **Avoid passing parameters** through multiple layers for per-thread data.

---

## **5. Important Notes**

1. **Memory Leak Risk:**

   * If threads are reused in a **thread pool**, values may persist → call `remove()` after use.

```java
threadLocal.remove(); // Prevents memory leaks in pooled threads
```

2. **Thread Safety:**

   * No explicit synchronization needed because each thread has **its own copy**.

3. **`initialValue()` vs `withInitial()`**

   * `withInitial(Supplier)` is a convenient factory method for setting default value.

---

💡 **Interview Tip:**

> "`ThreadLocal` provides thread-confined variables, allowing each thread to maintain its own copy. It's useful for per-thread context like sessions, transactions, or logging without synchronization."

---

I can next explain **difference between ThreadLocal, volatile, and synchronized**, which is a common multithreading interview question.

Do you want me to cover that?

---

## 98. What is deadlock in Java? How can it be avoided?

### **98. Deadlock in Java & How to Avoid It**

A **deadlock** is a situation in multithreading where **two or more threads are blocked forever**, each waiting for a resource held by the other. This leads to a **complete halt in execution** of the involved threads.

---

## **1. Definition**

* **Deadlock:** A state where threads **cannot proceed** because each is **waiting for a resource held by another thread**.
* **Occurs when:** Multiple threads try to acquire **multiple locks** in different order.

---

## **2. Conditions for Deadlock (Coffman Conditions)**

A deadlock occurs if all these **four conditions** hold simultaneously:

1. **Mutual Exclusion:** At least one resource must be held in **non-sharable mode** (only one thread at a time).
2. **Hold and Wait:** A thread holds at least **one resource and waits for another** held by other threads.
3. **No Preemption:** Resources cannot be forcibly taken from threads; they must be released voluntarily.
4. **Circular Wait:** A set of threads form a **circular chain** where each thread waits for a resource held by the next.

---

## **3. Example of Deadlock**

```java
class Resource {
    String name;
    Resource(String name) { this.name = name; }
}

public class DeadlockExample {
    public static void main(String[] args) {
        Resource r1 = new Resource("R1");
        Resource r2 = new Resource("R2");

        Thread t1 = new Thread(() -> {
            synchronized(r1) {
                System.out.println("Thread-1 locked R1");
                try { Thread.sleep(100); } catch (InterruptedException e) {}
                synchronized(r2) {
                    System.out.println("Thread-1 locked R2");
                }
            }
        });

        Thread t2 = new Thread(() -> {
            synchronized(r2) {
                System.out.println("Thread-2 locked R2");
                try { Thread.sleep(100); } catch (InterruptedException e) {}
                synchronized(r1) {
                    System.out.println("Thread-2 locked R1");
                }
            }
        });

        t1.start();
        t2.start();
    }
}
```

**Possible Output (Deadlock occurs):**

```
Thread-1 locked R1
Thread-2 locked R2
```

* Both threads **wait forever** for the other resource → deadlock.

---

## **4. How to Avoid Deadlocks**

### **a) Lock Ordering**

* Always acquire **multiple locks in the same order** across threads.

```java
synchronized(r1) {
    synchronized(r2) { ... }
}
```

### **b) Try-Lock with Timeout (ReentrantLock)**

* Use `java.util.concurrent.locks.ReentrantLock` with `tryLock(timeout)` to **avoid waiting forever**.

```java
if(lock1.tryLock(1000, TimeUnit.MILLISECONDS)) {
    try { ... } finally { lock1.unlock(); }
}
```

### **c) Lock Timeout**

* Use `Thread.join(timeout)` or `lock.tryLock(timeout)` to break circular wait.

### **d) Minimize Synchronized Blocks**

* Keep **critical sections short** to reduce lock contention.

### **e) Avoid Nested Locks**

* Reduce or eliminate acquiring multiple locks simultaneously.

### **f) Deadlock Detection Tools**

* Use **thread dumps** or **jconsole, VisualVM** to detect deadlocks.

---

## **5. Summary Table**

| Aspect         | Description                                                        |
| -------------- | ------------------------------------------------------------------ |
| **Definition** | Threads blocked forever, each waiting for resources held by others |
| **Conditions** | Mutual exclusion, hold & wait, no preemption, circular wait        |
| **Prevention** | Lock ordering, tryLock with timeout, minimal synchronized blocks   |
| **Detection**  | Thread dump, VisualVM, JConsole                                    |

---

💡 **Interview Tip:**

> "Deadlock occurs when threads wait indefinitely for each other’s locks. Avoid it by **consistent lock ordering, using tryLock with timeout, and minimizing nested locks**."

---

I can next explain **Live Lock vs Deadlock vs Starvation**, which is often asked in advanced Java multithreading interviews.

Do you want me to cover that?

---

## 99. Thread vs Runnable

### **99. Thread vs Runnable in Java**

In Java, both **`Thread`** and **`Runnable`** are used to create and run **threads**, but they have some important differences in usage, design, and flexibility.

---

## **1. Thread Class**

* **Definition:** `Thread` is a **class** that represents a thread of execution.
* **How to create a thread:**

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start(); // Starts new thread
    }
}
```

* **Key Points:**

  1. **Extends Thread class** → cannot extend another class.
  2. Each object of `Thread` is a **thread** itself.
  3. Directly overrides `run()` method.

---

## **2. Runnable Interface**

* **Definition:** `Runnable` is a **functional interface** with a single method `run()`.
* **How to create a thread:**

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

public class Main {
    public static void main(String[] args) {
        Thread t1 = new Thread(new MyRunnable());
        t1.start(); // Starts new thread
    }
}
```

* **Key Points:**

  1. **Implements Runnable** → can extend another class.
  2. Separates **thread logic (Runnable)** from **thread control (Thread object)**.
  3. Better for **thread pooling** and **executor framework**.

---

## **3. Key Differences: Thread vs Runnable**

| Feature                  | Thread                                         | Runnable                                                  |
| ------------------------ | ---------------------------------------------- | --------------------------------------------------------- |
| **Inheritance**          | Extends `Thread` class                         | Implements `Runnable` interface                           |
| **Multiple Inheritance** | Cannot extend another class                    | Can extend another class                                  |
| **Object vs Task**       | Each `Thread` object is a thread               | Runnable is the **task**, thread executes it              |
| **Memory Usage**         | Each thread object takes memory for the thread | Runnable can be shared across multiple threads            |
| **Flexibility**          | Less flexible                                  | More flexible, preferred in modern Java (ExecutorService) |
| **Example Usage**        | `t.start()`                                    | `new Thread(runnable).start()`                            |

---

## **4. When to Use Runnable**

1. When class **already extends another class**.
2. When using **ExecutorService or thread pool**.
3. For **separating task logic** from thread control.

**Example with ExecutorService:**

```java
ExecutorService executor = Executors.newFixedThreadPool(2);
executor.submit(new MyRunnable());
executor.submit(new MyRunnable());
executor.shutdown();
```

---

💡 **Interview Tip:**

> "Use **Runnable** for tasks and thread pools, and **Thread class** when you want a simple thread and do not need to extend any other class. Runnable provides better design flexibility."

---

I can next explain **Callable vs Runnable vs Thread**, which is commonly asked in multithreading interviews to test knowledge of return values and exception handling in threads.

Do you want me to cover that?

---

## 100. What is the difference between Runnable and Callable?

### **100. Runnable vs Callable in Java**

Both **`Runnable`** and **`Callable`** are used to define tasks that can be executed by a thread or thread pool, but they have some key differences in **return type, exception handling, and usage**.

---

## **1. Runnable Interface**

* **Definition:** A functional interface representing a task to run **without returning any result**.
* **Package:** `java.lang`
* **Method:**

```java
public void run();
```

* **Key Points:**

  1. **Cannot return a result**.
  2. **Cannot throw checked exceptions** (only runtime exceptions).
  3. Used with `Thread` or `ExecutorService`.

**Example:**

```java
Runnable task = () -> System.out.println("Runnable Task executed");
Thread t = new Thread(task);
t.start();
```

---

## **2. Callable Interface**

* **Definition:** A generic interface representing a task that **returns a result** and can **throw exceptions**.
* **Package:** `java.util.concurrent`
* **Method:**

```java
V call() throws Exception;
```

* **Key Points:**

  1. **Returns a value** (generic type `<V>`).
  2. **Can throw checked exceptions**.
  3. Must be executed via **ExecutorService**, not directly with `Thread`.
  4. Returns a **`Future<V>`**, which can be used to get the result.

**Example:**

```java
Callable<Integer> task = () -> {
    Thread.sleep(1000);
    return 123;
};

ExecutorService executor = Executors.newFixedThreadPool(1);
Future<Integer> future = executor.submit(task);
System.out.println("Callable result: " + future.get()); // 123
executor.shutdown();
```

---

## **3. Key Differences**

| Feature                | Runnable                        | Callable                                    |
| ---------------------- | ------------------------------- | ------------------------------------------- |
| **Return Value**       | None (`void`)                   | Yes (generic type `V`)                      |
| **Exception Handling** | Cannot throw checked exceptions | Can throw checked exceptions                |
| **Method**             | `void run()`                    | `V call() throws Exception`                 |
| **Execution**          | Thread or ExecutorService       | ExecutorService only (`submit()`)           |
| **Future**             | No                              | Yes, returns `Future<V>` to retrieve result |
| **Generics**           | Not supported                   | Supported (generic result type)             |

---

## **4. When to Use Callable**

1. When you need **a result** from a background task.
2. When the task may **throw checked exceptions**.
3. When using **ExecutorService** with **thread pools**.

---

💡 **Interview Tip:**

> "Use **Runnable** for tasks that don’t need a result, and **Callable** for tasks that return a value or throw exceptions. Callable works seamlessly with Future to get results asynchronously."

---

I can continue next with **Future vs CompletableFuture**, which is often asked after Callable in Java concurrency interviews.

Do you want me to cover that?

---

## 101. Synchronized method vs Synchronized blocks

### **101. Synchronized Method vs Synchronized Block in Java**

Both **synchronized methods** and **synchronized blocks** are used to **control access to shared resources** in multithreading and ensure **thread safety**, but they differ in **scope, flexibility, and performance**.

---

## **1. Synchronized Method**

* **Definition:** A method declared with the `synchronized` keyword, which ensures that **only one thread can execute the method at a time** for a given object.
* **Syntax:**

```java
public synchronized void increment() {
    count++;
}
```

* **Key Points:**

  1. **Locks the object instance** (`this`) for **non-static methods**.
  2. **Locks the class** (`ClassName.class`) for **static methods**.
  3. The **entire method is synchronized**, meaning all statements inside are locked.
  4. Simpler to implement but may **reduce performance** if only a small part of the method requires synchronization.

**Example:**

```java
class Counter {
    private int count = 0;

    public synchronized void increment() {
        count++;
    }

    public int getCount() {
        return count;
    }
}
```

---

## **2. Synchronized Block**

* **Definition:** A block of code within a method that is synchronized, allowing **fine-grained control** over which part of the method should be thread-safe.
* **Syntax:**

```java
public void increment() {
    synchronized(this) {
        count++;
    }
}
```

* **Key Points:**

  1. **Locks only the block**, not the entire method → better performance.
  2. Can **lock any object**, not just `this`.
  3. Useful for **reducing lock contention** in large methods.

**Example:**

```java
class Counter {
    private int count = 0;
    private Object lock = new Object();

    public void increment() {
        // Other non-critical code can run concurrently
        synchronized(lock) {
            count++;
        }
    }
}
```

---

## **3. Key Differences**

| Feature         | Synchronized Method                               | Synchronized Block                                   |
| --------------- | ------------------------------------------------- | ---------------------------------------------------- |
| **Scope**       | Entire method                                     | Only a specific block                                |
| **Lock Object** | `this` for instance, `ClassName.class` for static | Any object specified (`synchronized(lock)`)          |
| **Performance** | Slower if method has non-critical code            | Faster due to fine-grained locking                   |
| **Flexibility** | Less flexible                                     | More flexible, can lock multiple objects differently |
| **Syntax**      | `synchronized void methodName()`                  | `synchronized(lockObject) { ... }`                   |

---

## **4. Summary**

* **Use synchronized method**: When the **whole method** needs synchronization and code is small/simple.
* **Use synchronized block**: When **only part of the method** needs synchronization or when **locking a specific object** to improve performance.

---

💡 **Interview Tip:**

> "Synchronized blocks are preferred for **fine-grained control and better performance**, while synchronized methods are easier to implement but may lock unnecessary code."

---

I can next explain **Reentrant Locks vs Synchronized**, which is a common follow-up in Java concurrency interviews.

Do you want me to cover that?

---