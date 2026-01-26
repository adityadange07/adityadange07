# Core Java Interview Questions & Answers

## 1. What is a HashCode Contract?
**Detailed Explanation**: The contract between `equals()` and `hashCode()` is fundamental to the correct working of hash-based collections (HashMap, HashSet, Hashtable). The contract, defined in `java.lang.Object`, states:
1.  **Consistency**: Whenever `hashCode()` is invoked on the same object more than once during an execution, it must return the same integer, provided no information used in `equals` comparisons is modified.
2.  **Equality implies Identical Hash**: If `obj1.equals(obj2)` is true, then `obj1.hashCode()` MUST be equal to `obj2.hashCode()`.
3.  **Inequality does NOT imply Distinct Hash (Collision)**: If `obj1.equals(obj2)` is false, it is NOT required that `hashCode()` be different. However, distinct hash codes for unequal objects behave better for performance.

**Violation Consequences**: If you override `equals` but not `hashCode`, two logically equal objects (e.g., two `Person("John")` objects) will have different hash codes (derived from memory address). If you put one in a HashMap, you won't be able to retrieve it using the other, because the map looks in the wrong "bucket".

**Example**:
```java
import java.util.Objects;

public class Person {
    private String name;
    private int id;

    public Person(String name, int id) {
        this.name = name;
        this.id = id;
    }

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

---

## 2. What is ThreadPool in Java?
**Detailed Explanation**: A **ThreadPool** is a pool of pre-initialized worker threads that are ready to perform tasks. Instead of creating a new thread for every task (which is expensive in terms of system resources and overhead), the application reuses threads from the pool.
*   **Benefits**:
    *   **Performance**: Eliminates the overhead of creating and destroying threads for each task.
    *   **Resource Management**: Limits the maximum number of threads, preventing the system from running out of memory.
    *   **Response Time**: Tasks are processed immediately if a thread is available.
*   In Java, the `ExecutorService` interface and `Executors` factory class are used to create thread pools.

**Example**:
```java
import java.util.concurrent.ExecutorService;
import java.util.concurrent.Executors;

public class ThreadPoolExample {
    public static void main(String[] args) {
        // Create a pool with 3 fixed threads
        ExecutorService executor = Executors.newFixedThreadPool(3);

        for (int i = 1; i <= 5; i++) {
            int taskNumber = i;
            executor.submit(() -> {
                System.out.println("Task " + taskNumber + " running on " + Thread.currentThread().getName());
            });
        }

        // Shutdown the pool after tasks are submitted
        executor.shutdown();
    }
}
```

---

## 3. Working of ConcurrentHashMap
**Detailed Explanation**: `ConcurrentHashMap` is a thread-safe implementation of `Map` designed for high concurrency.
*   **Java 7**: Used **Segment Locking**. The map was divided into segments (default 16), and each segment had its own lock. This allowed 16 threads to write concurrently to different segments.
*   **Java 8+**: Improved performance significantly by removing segments.
    *   **Structure**: Uses an array of `Node` (buckets). Each bucket is a linked list or Red-Black Tree (if size > 8).
    *   **Read (get)**: Completely lock-free (uses `volatile` fields). Very fast.
    *   **Write (put)**:
        *   If the bucket is empty, it uses **CAS (Compare-And-Swap)** to insert the node. This is lock-free.
        *   If the bucket is not empty (collision), it synchronizes **only on the head node** of that specific bucket using `synchronized(node)`.
    *   This provides extremely fine-grained locking, allowing huge numbers of concurrent writers.

**Example**:
```java
import java.util.Map;
import java.util.concurrent.ConcurrentHashMap;

public class ConcurrentMapExample {
    public static void main(String[] args) {
        Map<String, Integer> map = new ConcurrentHashMap<>();

        // Multiple threads can write safely
        new Thread(() -> map.put("A", 1)).start();
        new Thread(() -> map.put("B", 2)).start();

        // Read does not block writers
        System.out.println(map.get("A"));
    }
}
```

---

## 4. Difference between HashSet and HashMap
**Detailed Explanation**:
*   **HashMap**: Implements `Map` interface. It stores data as **Key-Value** pairs. Keys must be unique, values can be duplicated. It allows one null key.
*   **HashSet**: Implements `Set` interface. It stores **Objects** (only keys). It ensures all elements are unique.
*   **Relationship**: Internally, a `HashSet` **USES** a `HashMap`. When you call `set.add(item)`, it actually performs `map.put(item, PRESENT)`, where `PRESENT` is a dummy object.

**Example**:
```java
import java.util.HashMap;
import java.util.HashSet;

public class MapVsSet {
    public static void main(String[] args) {
        // HashMap: Key -> Value
        HashMap<String, String> countryCodes = new HashMap<>();
        countryCodes.put("USA", "1");
        countryCodes.put("India", "91");
        
        // HashSet: Unique Elements
        HashSet<String> visitedCountries = new HashSet<>();
        visitedCountries.add("USA");
        visitedCountries.add("India");
        visitedCountries.add("USA"); // Duplicate ignored
        
        System.out.println(visitedCountries); // Output: [USA, India]
    }
}
```

---

## 5. What is a Synchronized Map? Used in multithreading environment.
**Detailed Explanation**: A synchronized map is a wrapper around a regular map that makes all its method calls `synchronized`. This ensures thread safety but hurts performance.
*   **Creation**: `Collections.synchronizedMap(new HashMap<>())`.
*   **How it works**: It uses a mutex (lock object). Every time a thread calls `put` or `get`, it acquires a lock on the **entire map**.
*   **Downside**: Only one thread can access the map at a time, even for reads. This creates a bottleneck in highly concurrent applications (unlike `ConcurrentHashMap`).
*   **Usage**: Used when you need basic thread safety for small maps and don't have high concurrency requirements.

**Example**:
```java
import java.util.Collections;
import java.util.HashMap;
import java.util.Map;

public class SyncMapExample {
    public static void main(String[] args) {
        Map<String, String> syncMap = Collections.synchronizedMap(new HashMap<>());

        syncMap.put("Key", "Value");

        // Iteration requires manual synchronization
        synchronized (syncMap) {
            for (String key : syncMap.keySet()) {
                System.out.println(key);
            }
        }
    }
}
```

---

## 6. Contrast between hashCode() and equals() methods?
**Detailed Explanation**:
*   **`equals()`**: Determines **logical equality**. It checks if two objects represent the "same thing" (e.g., same ID and name). Default implementation in `Object` compares memory addresses (reference equality).
*   **`hashCode()`**: Returns an **integer representation** of the object. It is used exclusively by hash-based collections (HashMap, HashSet) to determine which "bucket" to store the object in.
*   **Key difference**: `equals()` is about accuracy (are they exactly the same?); `hashCode()` is about performance (grouping objects into buckets).

**Example**:
```java
String s1 = new String("Java");
String s2 = new String("Java");

// equals() checks content
System.out.println(s1.equals(s2)); // true

// hashCode() generates int based on content
System.out.println(s1.hashCode()); // e.g., 2301506
System.out.println(s2.hashCode()); // e.g., 2301506 (Must be same)
```

---

## 7. Which Java version did you use in your project?
**Detailed Explanation**: This is an HR/Experience question. You should answer with the version used in your standard environment, usually an LTS (Long Term Support) version like Java 8, 11, or 17.
*   **Answer Strategy**: Mention the version and 1-2 key features you utilized.

**Example Answer**:
"In my most recent project, we used **Java 17**. We migrated from Java 8 to take advantage of the performance improvements and new language features like **Records** for cleaner DTOs and **Text Blocks** for writing readable SQL queries in code. We also utilized the improved Garbage Collectors."

---

## 8. Difference between HashMap and LinkedHashMap
**Detailed Explanation**:
*   **HashMap**: Does **not** guarantee any order of elements. The order can change when the map is resized. It is the fastest implementation.
*   **LinkedHashMap**: Extends HashMap. It maintains a **Doubly Linked List** running through all its entries.
    *   **Insertion Order**: Default. Iterates elements in the order they were added.
    *   **Access Order**: Can be configured. Iterates elements based on last access (useful for LRU Caches).
*   **Trade-off**: `LinkedHashMap` is slightly slower (overhead of maintaining the linked list) but predictable in iteration.

**Example**:
```java
import java.util.HashMap;
import java.util.LinkedHashMap;

public class OrderExample {
    public static void main(String[] args) {
        HashMap<String, String> map = new HashMap<>();
        map.put("Z", "Zebra");
        map.put("A", "Apple");
        System.out.println(map); // Random order (e.g., {A=Apple, Z=Zebra})

        LinkedHashMap<String, String> linkedMap = new LinkedHashMap<>();
        linkedMap.put("Z", "Zebra");
        linkedMap.put("A", "Apple");
        System.out.println(linkedMap); // Guarantee: {Z=Zebra, A=Apple}
    }
}
```

---

## 9. Difference between HashSet and TreeSet
**Detailed Explanation**:
*   **HashSet**:
    *   Backed by a `HashMap`.
    *   **Unordered**: Elements are stored based on hash codes.
    *   **Performance**: O(1) for add/remove/contains. Fastest.
    *   **Null**: Allows one null element.
*   **TreeSet**:
    *   Backed by a `TreeMap` (Red-Black Tree).
    *   **Sorted**: Elements are stored in natural order (Comparable) or custom order (Comparator).
    *   **Performance**: O(log n). Slower than HashSet.
    *   **Null**: Does NOT allow nulls (throws exception).

**Example**:
```java
import java.util.HashSet;
import java.util.TreeSet;

public class SetDiff {
    public static void main(String[] args) {
        HashSet<Integer> hashSet = new HashSet<>();
        hashSet.add(5); hashSet.add(1); hashSet.add(10);
        System.out.println(hashSet); // [1, 5, 10] or [5, 10, 1] (No Guarantee)

        TreeSet<Integer> treeSet = new TreeSet<>();
        treeSet.add(5); treeSet.add(1); treeSet.add(10);
        System.out.println(treeSet); // [1, 5, 10] (Always Sorted)
    }
}
```

---

## 10. Difference between Comparable and Comparator
**Detailed Explanation**: Both are interfaces used for sorting objects.
*   **Comparable (`java.lang.Comparable`)**:
    *   Used to define the **Natural Ordering** of a class.
    *   The class usually implements this interface itself.
    *   Method: `public int compareTo(T o)`.
    *   **Use case**: "This object knows how to compare itself to another." (e.g., String, Integer).
*   **Comparator (`java.util.Comparator`)**:
    *   Used to define **Custom Ordering** (or if you can't modify the class).
    *   Implemented in a separate class or as a lambda.
    *   Method: `public int compare(T o1, T o2)`.
    *   **Use case**: "I want to sort this list of people by Age, then by Name."

**Example**:
```java
import java.util.*;

class Student implements Comparable<Student> {
    String name;
    int id;
    
    // Comparable: Natural sort by ID
    public int compareTo(Student other) {
        return this.id - other.id;
    }
}

public class SortExample {
    public static void main(String[] args) {
        List<Student> students = new ArrayList<>();
        // ... add students ...
        
        Collections.sort(students); // Uses Comparable (sort by ID)
        
        // Comparator: Custom sort by Name
        Collections.sort(students, new Comparator<Student>() {
             public int compare(Student s1, Student s2) {
                 return s1.name.compareTo(s2.name);
             }
        });
        // Java 8 Style
        Collections.sort(students, (s1, s2) -> s1.name.compareTo(s2.name));
    }
}
```

---

## 11. Java 8 Features
**Detailed Explanation**: Java 8 was a major release that introduced functional programming concepts.
1.  **Lambda Expressions**: Anonymous functions (`(params) -> body`). Makes code concise.
2.  **Stream API**: A powerful way to process collections of objects (filtering, mapping, reducing) effectively. Supports parallel processing.
3.  **Optional Class**: A container object which may or may not contain a non-null value. Helps avoid `NullPointerException`.
4.  **Default Methods**: Interfaces can now have methods with bodies (`default void method() { ... }`). Allows adding new methods to interfaces without breaking implementing classes.
5.  **Method References**: Shorthand notation for a lambda expression calling a specific method (`System.out::println`).
6.  **Date/Time API**: `java.time` package (`LocalDate`, `LocalDateTime`). Immutable and thread-safe replacements for `Date/Calendar`.

**Example**:
```java
import java.util.Arrays;
import java.util.List;

public class Java8Demo {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "");

        // Stream + Lambda + Method Reference
        names.stream()
             .filter(name -> !name.isEmpty()) // Lambda
             .map(String::toUpperCase)        // Method Reference
             .forEach(System.out::println);
    }
}
```

---

## 12. Internal working of HashMap (HashCode, Equals, Collision, Rehashing)
**Detailed Explanation**:
1.  **Hashing**: When you `put(key, value)`, map calls `key.hashCode()`. It applies a bitwise function to spread bits (perturbation) and calculates an index: `index = hash & (n-1)`.
2.  **Collision**: If the bucket at `index` is empty, the node is stored. If NOT empty (Collision), it checks the existing `key` using `equals()`:
    *   If `equals()` is true, the value is updated.
    *   If `equals()` is false, the new node is added to the end of the Linked List (or Tree) in that bucket.
3.  **Treeify**: (Java 8+) If a single bucket's linked list grows beyond 8 nodes, it converts into a Red-Black Tree for O(log n) performance.
4.  **Rehashing**: When the total number of entries > `capacity * loadFactor` (default 16 * 0.75 = 12), the map resizes. It doubles the capacity (16 -> 32) and recalculates the index for EVERY entry to distribute them into the new larger array. Expensive operation.

**Example**:
```text
Map.put("A", 1); -> Hash("A")=65 -> Index 1 -> Store [A,1]
Map.put("B", 2); -> Hash("B")=66 -> Index 2 -> Store [B,2]
Map.put("Aa", 3); -> Hash("Aa")=2112 -> If Index 1 (Collision!)
    -> "Aa".equals("A")? False.
    -> Add to list at Index 1: [A,1] -> [Aa,3]
```

---

## 13. What is the difference between ConcurrentHashMap and HashMap?
**Detailed Explanation**:
*   **HashMap**:
    *   **Thread Safety**: Not thread-safe. If one thread modifies structure while another iterates, it throws `ConcurrentModificationException` (Fail-Fast).
    *   **Nulls**: Allows 1 null key and multiple null values.
    *   **Locking**: None.
*   **ConcurrentHashMap**:
    *   **Thread Safety**: Thread-safe. Designed for high concurrency.
    *   **Nulls**: **Does NOT** allow null keys or null values (throws `NullPointerException`).
    *   **Locking**: Uses Bucket-Level locking (synchronized/CAS). It never locks the whole map.
    *   **Iterator**: Fail-Safe (Weakly Consistent). It reflects the state of the map at the time of creation, plus *maybe* later updates. It does NOT throw exceptions.

**Example**:
```java
// HashMap
Map<String, String> map = new HashMap<>();
map.put(null, "value"); // OK

// ConcurrentHashMap
Map<String, String> concurrentMap = new ConcurrentHashMap<>();
// concurrentMap.put(null, "value"); // Throws NullPointerException
```

---

## 14. What are the pillars of OOPS?
**Detailed Explanation**:
1.  **Encapsulation**: Bundling data (variables) and methods (functions) together in a class and restricting access using modifiers (private, public). Protects object integrity.
2.  **Inheritance**: The mechanism where a new class (Child) acquires the properties and behaviors of an existing class (Parent). Promotes code reusability.
3.  **Polymorphism**: The ability of an object to take many forms.
    *   **Compile-time**: Method Overloading.
    *   **Runtime**: Method Overriding.
4.  **Abstraction**: Hiding the implementation details and showing only functionality to the user. Achieved via Abstract Classes and Interfaces.

**Example**:
```java
// Abstraction & Inheritance
abstract class Animal { // Abstract
    abstract void sound(); 
}

// Encapsulation
class Dog extends Animal { // Inheritance
    private String name; // Encapsulated data

    public void sound() { // Polymorphism (Overriding)
        System.out.println("Bark");
    }
}
```

---

## 15. Difference between Abstract Class and Interface
**Detailed Explanation**:
*   **Abstract Class**:
    *   Can have both abstract (no body) and concrete (with body) methods.
    *   Can have state (instance variables).
    *   Can have constructors.
    *   A class can extend only **ONE** abstract class.
    *   Used for "is-a" relationship (sharing valid code).
*   **Interface**:
    *   All methods are implicitly `public abstract` (until Java 8 added default/static).
    *   Cannot have instance variables (only `public static final` constants).
    *   No constructors.
    *   A class can implement **MULTIPLE** interfaces.
    *   Used for "can-do" relationship (defining a contract).

**Example**:
```java
abstract class Vehicle {
    int fuel; // State
    abstract void drive();
}

interface Flyable {
    void fly(); // Contract
}

// Can extend 1 class, implement many interfaces
class FlyingCar extends Vehicle implements Flyable {
    void drive() { ... }
    public void fly() { ... }
}
```

---

## 16. Can we create an object of an abstract class?
**Detailed Explanation**:
**No, we cannot directly instantiate an abstract class.** It is incomplete by design.
*   **Reason**: It may contain abstract methods (methods without a body). If you could create an object, calling that method would do nothing or crash.
*   **Usage**: You must create a subclass that extends the abstract class and provides implementations for all abstract methods. You then instantiate the subclass.
*   *Note*: You can use an **Anonymous Inner Class** to provide the implementation inline, which looks like instantiation, but you are actually creating an instance of a nameless subclass.

**Example**:
```java
abstract class Base {
    abstract void print();
}

public class Test {
    public static void main(String[] args) {
        // Base b = new Base(); // COMPILER ERROR
        
        Base b = new Base() { // Anonymous Inner Class
            void print() { System.out.println("Hello"); }
        };
        b.print();
    }
}
```

---

## 17. If a class implements multiple interfaces with the same method name, what happens?
**Detailed Explanation**:
1.  **Abstract Methods**: If two interfaces have the same abstract method `void show()`, and the class implements both, it’s fine. The class just needs to provide **one** implementation that satisfies both interfaces.
2.  **Default Methods (The Diamond Problem)**: If two interfaces provide a `default` implementation for the exact same method signature, the compiler throws an error because it doesn't know which one to use.
    *   **Solution**: The class **MUST** override the method and explicitly call one (or both) of the interface implementations using `InterfaceName.super.method()`.

**Example**:
```java
interface A { default void show() { System.out.println("A"); } }
interface B { default void show() { System.out.println("B"); } }

class C implements A, B {
    // Compiler Error if we don't override
    @Override
    public void show() {
        A.super.show(); // Resolve ambiguity
        // or code your own logic
    }
}
```

---

## 18. Polymorphism scenarios (Overloading vs Overriding)
**Detailed Explanation**:
*   **Overloading (Compile-time Polymorphism)**:
    *   Same method name, different parameter list (number or type).
    *   Return type doesn't matter.
    *   Binding happens at compile time.
    *   Example: `add(int a, int b)` vs `add(double a, double b)`.
*   **Overriding (Runtime Polymorphism)**:
    *   Exact same method signature (name + params) in Parent and Child class.
    *   Child provides a specific implementation.
    *   Binding happens at runtime based on the actual object type (Dynamic Dispatch).

**Example**:
```java
class Calculator {
    // Overloading
    int add(int a, int b) { return a+b; }
    int add(int a, int b, int c) { return a+b+c; }
}

class Animal { void sound() { System.out.println("..."); } }
class Cat extends Animal {
    // Overriding
    @Override
    void sound() { System.out.println("Meow"); } 
}
```

---

## 19. Collection Framework (ArrayList vs LinkedList, List vs Set)
**Detailed Explanation**:
*   **List vs Set**:
    *   **List**: Ordered collection (0, 1, 2...). Allows duplicates. Access by Index.
    *   **Set**: Unordered collection. No duplicates. No Index access.
*   **ArrayList vs LinkedList**:
    *   **ArrayList**: Uses a dynamic array (resizable).
        *   **Get**: O(1) - Fast (direct memory jump).
        *   **Add/Remove**: O(n) - Slow (needs to shift elements).
        *   Use when: Heavy reading, distinct specific order.
    *   **LinkedList**: Uses a Doubly Linked List.
        *   **Get**: O(n) - Slow (must traverse nodes).
        *   **Add/Remove**: O(1) - Fast (just change pointers).
        *   Use when: Frequent manipulation (insert/delete) in the middle.

**Example**:
```java
// List: Duplicates allowed
List<String> list = new ArrayList<>();
list.add("A"); list.add("A"); // OK

// Set: Unique only
Set<String> set = new HashSet<>();
set.add("A"); set.add("A"); // Ignored
```

---

## 20. Exception Handling (Try-Catch-Finally, Try-with-resources, Custom Exceptions, Checked vs Unchecked)
**Detailed Explanation**:
*   **Try-Catch-Finally**: `try` contains risky code. `catch` handles the error. `finally` runs **always** (success or failure) to clean up (close files).
*   **Try-with-resources**: (Java 7+) Syntax `try (Resource res = ...) { }`. Automatically calls `res.close()` at the end. Cleaner code.
*   **Checked vs Unchecked**:
    *   **Checked (`Exception`)**: Compile-time check. You MUST handle it (try-catch or throws). E.g., `IOException`.
    *   **Unchecked (`RuntimeException`)**: Runtime check. Logic errors. Optional handling. E.g., `NullPointerException`.
*   **Custom Exception**: Inherit from `Exception` (Checked) or `RuntimeException` (Unchecked).

**Example**:
```java
// Try-with-resources
try (FileReader fr = new FileReader("test.txt")) {
    // Read file
} catch (IOException e) {
    // Handle error
} 
// 'fr' is closed automatically
```

---

## 21. What is the difference between final, finally, and finalize?
**Detailed Explanation**:
1.  **`final` (Keyword)**:
    *   Variable: Constant (cannot change value).
    *   Method: Cannot be overridden.
    *   Class: Cannot be inherited (e.g., `String` class).
2.  **`finally` (Block)**: Used in exception handling. The code inside `finally` executes regardless of whether an exception occurred or not. Used for closing resources.
3.  **`finalize` (Method)**: `protected void finalize()`. Called by Garbage Collector before destroying an object. **Deprecated** in Java 9+ because it's unpredictable.

**Example**:
```java
final int x = 10;
// x = 20; // Error

try {
    // code
} finally {
    System.out.println("Always runs");
}
```

---

## 22. String Immutability: Why is String immutable? How to create an immutable class?
**Detailed Explanation**:
*   **Why Immutable?**
    1.  **String Pool**: Java saves memory by reusing identical string literals. If strings were mutable, changing one reference would affect all others pointing to the same literal.
    2.  **Security**: Strings are used for passwords, database URLs, etc. Immutability prevents tampering.
    3.  **Thread Safety**: Immutable objects are automatically thread-safe.
*   **How to create Immutable Class**:
    1.  Declare class `final` (no inheritance).
    2.  Make all fields `private final`.
    3.  No Setters.
    4.  Initialize all fields in Constructor.
    5.  Deep Copy: If a field is mutable (like a List), return a copy in the getter, not the original.

**Example**:
```java
public final class ImmutableUser {
    private final String name;
    
    public ImmutableUser(String name) {
        this.name = name;
    }
    
    public String getName() {
        return name;
    }
}
```

---

## 23. String vs StringBuilder vs StringBuffer
**Detailed Explanation**:
*   **String**: **Immutable**. Every modification (`+`, `concat`) creates a NEW object in memory.
*   **StringBuilder**: **Mutable**. Modifies the existing object. **Not Thread-safe**. Fast. Use this for string manipulation in a single thread.
*   **StringBuffer**: **Mutable**. **Thread-safe** (all methods are `synchronized`). Slower. Use only when string is shared between threads.

**Example**:
```java
String s = "Hello";
s = s + " World"; // Creates NEW string "Hello World"

StringBuilder sb = new StringBuilder("Hello");
sb.append(" World"); // Modifies existing object
```

---

## 24. What is the String Constant Pool (SCP) and Heap memory?
**Detailed Explanation**:
*   **Heap Memory**: General memory area where all Java objects are created (`new KeyWord`).
*   **String Constant Pool (SCP)**: A special pool inside the Heap (or Metaspace in older versions) that stores **String Literals**.
*   **Mechanism**:
    *   `String s1 = "ABC"`: Checks SCP. If "ABC" exists, returns reference. If not, creates "ABC" in SCP and returns reference.
    *   `String s2 = new String("ABC")`: Forcefully creates a **new object** in normal Heap memory. "ABC" literal might also be created in SCP if not present.

**Example**:
```java
String s1 = "Java";
String s2 = "Java"; // s1 == s2 is TRUE (Same reference in SCP)

String s3 = new String("Java"); // s1 == s3 is FALSE (SCP vs Heap)
```

---

## 25. Multithreading (Lifecycle, creation, sync)
**Detailed Explanation**:
*   **Ways to create**:
    1.  Extend `Thread` class.
    2.  Implement `Runnable` interface (Better, allows extending other classes).
    3.  Implement `Callable` (Returns a result).
*   **Lifecycle**: New -> Runnable -> Running -> Blocked/Waiting -> Terminated.
*   **Synchronization**: Controls access to shared resources using locks.
    *   `wait()`: Thread gives up lock and sleeps until notified.
    *   `notify()`: Wakes up one waiting thread.
    *   `join()`: Thread A waits for Thread B to finish.
*   **Deadlock**: Situation where Thread 1 holds Lock A expecting Lock B, and Thread 2 holds Lock B expecting Lock A. Both wait forever.

**Example**:
```java
class MyTask implements Runnable {
    public void run() {
        System.out.println("Running");
    }
}
Thread t = new Thread(new MyTask());
t.start();
```

---

## 26. ExecutorService and ThreadPoolExecutor
**Detailed Explanation**:
*   **ExecutorService**: A high-level interface for managing threads. It decouples task submission from task execution.
*   **ThreadPoolExecutor**: The core implementation. It manages a pool of threads.
    *   **Core Pool Size**: Minimum threads always alive.
    *   **Max Pool Size**: Maximum threads allowed.
    *   **Queue**: Holds tasks if all threads are busy.
*   It handles life-cycle automatically (creating, reusing, destroying threads).

**Example**:
```java
ExecutorService es = Executors.newFixedThreadPool(10);
es.submit(() -> System.out.println("Async Task"));
es.shutdown(); // Stop after tasks done
```

---

## 27. Java Memory Management (Stack vs Heap, PermGen vs Metaspace, GC)
**Detailed Explanation**:
*   **Stack Memory**: Stores primitive local variables and method calls (frames). Thread-specific. Fast access. Cleared when method ends.
*   **Heap Memory**: Stores **Objects** (Classes, Arrays). Shared by all threads. Managed by Garbage Collector.
*   **PermGen (Java 7)** / **Metaspace (Java 8+)**: Stores Class Metadata (static variables, method data). Metaspace uses native OS memory and auto-resizes.
*   **Garbage Collection (GC)**: Automatic process to delete unused objects.
    *   **Young Gen**: Newly created objects. Minor GC is fast.
    *   **Old Gen**: Long-surviving objects. Major GC is slow.

---

## 28. What is the volatile keyword?
**Detailed Explanation**: `volatile` is a modifier for variables. It guarantees **Visibility** of changes to variables across threads.
*   **Problem**: Threads cache variables in CPU registers for speed. If Thread 1 updates `flag = true` in its cache, Thread 2 might still see `flag = false` in its cache.
*   **Solution**: `volatile boolean flag`. Reads and writes go directly to **Main Memory** (RAM).
*   *Note*: It does **not** make operations atomic (like `i++`).

**Example**:
```java
private volatile boolean running = true;

public void run() {
    while (running) {
        // ... keeps running until another thread sets running=false
    }
}
```

---

## 29. What is the transient keyword?
**Detailed Explanation**: Used in Serialization. If you define a field as `transient`, it is **ignored** when writing the object to a file.
*   **Use Case**: Passwords, sensitive data, or derived fields that don't need to be saved.
*   On deserialization, the transient field gets its default value (null or 0).

**Example**:
```java
class User implements Serializable {
    String name;
    transient String password; // Won't be saved
}
```

---

## 30. Serialization in Java
**Detailed Explanation**: The process of converting a Java Object into a byte stream to save to a file or send over a network.
*   **Interface**: Class must implement `java.io.Serializable` (Marker interface).
*   **Deserialization**: Converting byte stream back to Object.
*   **serialVersionUID**: A unique ID used to verify that the sender and receiver have loaded classes for that object that are compatible. If code changes, ID changes, causing `InvalidClassException` unless manually defined.

**Example**:
```java
// Serialize
ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("file.txt"));
out.writeObject(myObj);

// Deserialize
ObjectInputStream in = new ObjectInputStream(new FileInputStream("file.txt"));
MyObject obj = (MyObject) in.readObject();
```

---

## 31. What is Object Cloning? Shallow Copy vs Deep Copy
**Detailed Explanation**:
*   **Cloning**: Creating an exact copy of an object using `obj.clone()`. Requires executing `Cloneable` interface.
*   **Shallow Copy** (Default): Copies values of fields.
    *   Primitives: Copied.
    *   References: Copies the reference (address). Both new and old object point to the **same** inner object. Changing inner object affects both.
*   **Deep Copy**: Manually implemented. Creates a **new** instance for referenced objects too. The two objects are completely independent.

**Example**:
```java
// Shallow:
copy.list = original.list; 

// Deep:
copy.list = new ArrayList<>(original.list);
```

---

## 32. What is a Marker Interface?
**Detailed Explanation**: An interface that has **no methods or constants**.
*   **Purpose**: It provides run-time type information to the JVM or compiler. It "marks" a class as capable of some special behavior.
*   **Examples**:
    *   `Serializable`: Tells JVM "this object can be saved".
    *   `Cloneable`: Tells JVM "it's okay to use .clone()".
    *   `Remote`: For RMI.

---

## 33. Functional Interfaces
**Detailed Explanation**: An interface with exactly **one abstract method**. Used heavily in Java 8 for Lambda expressions.
*   **Common Interfaces (`java.util.function`)**:
    *   **`Predicate<T>`**: Takes T, returns boolean. (`filter(x -> x > 10)`)
    *   **`Consumer<T>`**: Takes T, returns void. (`forEach(x -> print(x))`)
    *   **`Supplier<T>`**: Takes nothing, returns T. (`generate(() -> Math.random())`)
    *   **`Function<T, R>`**: Takes T, returns R. (`map(x -> x.toString())`)

**Example**:
```java
Predicate<String> isEmpty = s -> s.length() == 0;
System.out.println(isEmpty.test("")); // true
```

---

## 34. Method References in Java 8
**Detailed Explanation**: A cleaner shorthand for a lambda expression that does nothing but call an existing method.
*   **Syntax**: `ClassName::methodName`
*   **Types**:
    *   Static method: `Math::max` (Equivalent to `(a,b) -> Math.max(a,b)`)
    *   Instance method: `System.out::println` (Equivalent to `x -> System.out.println(x)`)
    *   Constructor: `ArrayList::new`

**Example**:
```java
List<String> list = Arrays.asList("a", "b");
list.forEach(System.out::println); // Method Reference
```

---

## 35. Stream API operations
**Detailed Explanation**:
*   **Stream**: A sequence of elements supporting sequential and parallel aggregate operations.
*   **Intermediate Operations**: Lazy. Return a new Stream.
    *   `filter(predicate)`: Keep matches.
    *   `map(function)`: Transform elements.
    *   `sorted()`: Sort.
*   **Terminal Operations**: Eager. Trigger the pipeline and return a result.
    *   `collect()`: Save to List/Map.
    *   `forEach()`: Loop.
    *   `count()`: Count.
*   **Map vs FlatMap**:
    *   **Map**: One input -> One output. `List<String>`.
    *   **FlatMap**: One input -> Many outputs (Stream). Used to flatten `List<List<String>>` into `List<String>`.

**Example**:
```java
List<String> result = names.stream()
    .filter(s -> s.startsWith("A"))
    .map(String::toUpperCase)
    .collect(Collectors.toList());
```

---

## 36. CompletableFuture in Java 8
**Detailed Explanation**: An enhancement of `Future` for asynchronous programming.
*   **Problem with Future**: `future.get()` is blocking. You can't manually complete it or chain actions.
*   **CompletableFuture**: Non-blocking. Allows chaining multiple stages (`thenApply`, `thenAccept`). Can combine multiple futures. Handles exceptions gracefully used `exceptionally`.
*   **Use Case**: Fetching data from 3 APIs in parallel and combining results.

**Example**:
```java
CompletableFuture.supplyAsync(() -> fetchOrder())
    .thenApply(order -> enrichOrder(order))
    .thenAccept(order -> save(order));
```

---

## 37. Use of Optional class
**Detailed Explanation**: A wrapper class `Optional<T>` intended to eliminate `NullPointerException`.
*   **Concept**: It explicitly forces the developer to handle the "value might be missing" case.
*   **Methods**:
    *   `isPresent()`: Check existence.
    *   `ifPresent(Consumer)`: Run code if exists.
    *   `orElse(default)`: Return default if empty.
    *   `orElseThrow()`: Throw error if empty.

**Example**:
```java
Optional<String> opt = Optional.ofNullable(getName());
String name = opt.orElse("Unknown User");
```

---

## 38. What is the difference between Fail-Fast and Fail-Safe iterators?
**Detailed Explanation**:
*   **Fail-Fast**:
    *   Works on the **original collection**.
    *   If collection structure changes (add/remove) while iterating, it immediately throws `ConcurrentModificationException`.
    *   Examples: `ArrayList`, `HashMap` iterators.
*   **Fail-Safe (Weakly Consistent)**:
    *   Works on a **copy** or a view of the data.
    *   Does NOT throw exception if modified.
    *   Examples: `ConcurrentHashMap`, `CopyOnWriteArrayList`.

---

## 39. What is the difference between Class-Level Locking and Object-Level Locking?
**Detailed Explanation**:
*   **Object-Level Locking**:
    *   `synchronized(this)` or `synchronized void method()`.
    *   Locks **that specific instance** of the object. Other threads can access other instances of the same class.
*   **Class-Level Locking**:
    *   `synchronized(MyClass.class)` or `static synchronized void method()`.
    *   Locks the **Class object** (Metadata).
    *   Block access to static synchronized methods across **ALL** instances.

**Example**:
```java
class Demo {
    // Blocks only this object
    synchronized void m1() {} 
    
    // Blocks ALL objects of class Demo
    static synchronized void m2() {} 
}
```

---

## 40. Explain Java ClassLoader work at runtime
**Detailed Explanation**: Java uses a delegation model to load classes.
1.  **Bootstrap ClassLoader**: Loads core libraries (`rt.jar` - String, System, etc.). Written in C++.
2.  **Extension/Platform ClassLoader**: Loads extensions from `lib/ext`.
3.  **Application/System ClassLoader**: Loads classes from your `CLASSPATH` (your code).
*   **Delegation Principle**: When App ClassLoader needs a class, it asks Parent (Ext). Ext asks Parent (Bootstrap). If Bootstrap finds it, good. If not, it comes back down. If no one finds it -> `ClassNotFoundException`.

---

## 41. Features of Java 17
**Detailed Explanation**:
1.  **Records**: A compact syntax for declaring data classes. Auto-generates getters, equals, hashcode, toString.
    `record Point(int x, int y) {}`
2.  **Sealed Classes**: Control which classes can extend your class.
    `public sealed class Shape permits Circle, Square {}`
3.  **Pattern Matching for instanceof**:
    `if (obj instanceof String s) { call(s); }` (No explicit casting needed).
4.  **Text Blocks**: Multiline strings using triple quotes `"""`.
5.  **Switch Expressions**: Return values from switch, arrow syntax.

---

## 42. Diamond problem in Java (Multiple Inheritance)
**Detailed Explanation**:
*   **Problem**: If Class C extends Class A and Class B, and both A and B have a method `print()`, which one does C inherit? This ambiguity is the Diamond Problem.
*   **Java's Stance**: Java relies on **Interfaces** to support multiple inheritance types but avoids the state complexity of multiple class inheritance.
*   **Modern Twist**: With Java 8 Default Methods, the problem returned. Java solves it by forcing the developer to override the conflicting method in Class C.

---

## 43. Can we overload the main method?
**Detailed Explanation**:
*   **Yes**, you can have multiple methods named `main` with different parameters.
*   **However**: The JVM looks specifically for the signature `public static void main(String[] args)` as the entry point.
*   Any other `main` method is just a normal method and won't be called automatically.

**Example**:
```java
public static void main(String[] args) { ... } // JVM starts here
public static void main(String arg) { ... } // Normal method
```

---

## 44. Can we make the main method private?
**Detailed Explanation**:
*   **You can** change access modifier to `private` and the code will **compile**.
*   **However**, at runtime, the JVM will fail to launch the application.
*   **Error**: "Main method not found in class..." because JVM expects it to be `public` to access it.

---

## 45. Output of: String s1="java"; String s2=new String("java"); s1==s2?
**Detailed Explanation**:
*   **Code**:
    ```java
    String s1 = "java"; // Goes to String Constant Pool (SCP)
    String s2 = new String("java"); // Goes to Heap (New Object)
    System.out.println(s1 == s2); 
    ```
*   **Answer**: **False**.
*   **Reason**: `==` compares **memory referneces (addresses)**.
    *   `s1` points to the literal in the SCP.
    *   `s2` points to a completely different object in the main Heap.
    *   They are stored in different memory locations.
    *   `s1.equals(s2)` would be True (content match).
