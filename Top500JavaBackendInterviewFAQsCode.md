# Top 500 Java Backend Interview FAQs

## 1. Explain the difference between `==` and `.equals()` in Java.

**Answer:**
In Java, the `==` operator checks for **reference equality**, meaning it verifies if two variables point to the exact same memory address (or consistent value for primitives). The `.equals()` method is designed for **logical equality**. By default in the `Object` class, it behaves like `==`, but classes like `String`, `Integer`, and `Date` override it to compare the actual *content* of the objects.

**Code Snippet:**
```java
public class EqualityCheck {
    public static void main(String[] args) {
        String s1 = "Hello";              // String Pool
        String s2 = new String("Hello");  // Heap Memory

        System.out.println(s1 == s2);       // false (Different memory addresses)
        System.out.println(s1.equals(s2));  // true (Same content)
    }
}
```

---

## 2. Why is String immutable in Java?

**Answer:**
Strings are immutable for **Security**, **Performance**, and **Thread Safety**.
1.  **String Constant Pool:** Java saves memory by reusing identical string literals. If strings were mutable, changing one reference would affect all others pointing to the same literal.
2.  **Security:** Strings are used for critical values like database URLs, usernames, and class names. Immutability prevents malicious modification.
3.  **Thread Safety:** Since state cannot change, strings are inherently thread-safe and can be shared without synchronization.
4.  **HashCode Caching:** The hash code is calculated once and cached, making Strings excellent keys for HashMaps.

**Code Snippet:**
```java
String s = "Java";
s.concat(" World"); 
// The original string 's' remains "Java". 
// A new string "Java World" is created and lost because it wasn't assigned.
System.out.println(s); // Output: Java
```

---

## 3. What is the difference between HashMap and ConcurrentHashMap?

**Answer:**
**`HashMap`** is fast but **not thread-safe**. If accessed by multiple threads without external synchronization, it can lead to data corruption or infinite loops.
**`ConcurrentHashMap`** is **thread-safe** and optimized for high concurrency. By default (Java 8+), it uses **bucket-level locking** (locking only the specific node being accessed) and CAS operations, allowing multiple threads to read and write simultaneously without locking the entire map. It also does not allow `null` keys or values.

**Code Snippet:**
```java
// Thread-safe map efficient for high concurrency
Map<String, Integer> map = new ConcurrentHashMap<>();

map.put("A", 1);
map.put("B", 2);

// Multiple threads can safely allow operations here
map.forEach((k, v) -> System.out.println(k + ": " + v));
```

---

## 4. Explain the concept of fail-fast vs fail-safe iterators.

**Answer:**
**Fail-Fast Iterators** (e.g., `ArrayList`, `HashMap`) throw a `ConcurrentModificationException` immediately if the collection is structurally modified (added/removed) during iteration. They use a `modCount` variable to detect changes.
**Fail-Safe Iterators** (e.g., `CopyOnWriteArrayList`, `ConcurrentHashMap`) operate on a clone or a snapshot of the collection (or use a different consistency model). They do **not** throw exceptions if the collection is modified during iteration, but they might not reflect the latest changes.

**Code Snippet:**
```java
List<String> list = new CopyOnWriteArrayList<>(); // Fail-Safe
list.add("A");
list.add("B");

Iterator<String> it = list.iterator();
while (it.hasNext()) {
    String s = it.next();
    if (s.equals("A")) {
        list.add("C"); // Allowed, no exception thrown
    }
}
System.out.println(list); // Output: [A, B, C]
```

---

## 5. What is the significance of hashCode() and equals() method?

**Answer:**
These methods define the contract for object equality, which is critical for hash-based collections (`HashMap`, `HashSet`).
1.  **Contract:** If `a.equals(b)` is true, then `a.hashCode()` *must* be equal to `b.hashCode()`.
2.  **Collision:** Accessing a HashMap uses the hash code to find the "bucket" location. If `hashCode()` is not implemented correctly (e.g., returns random numbers), the map cannot retrieve the object even if it exists.
3.  **Performance:** A good `hashCode()` distributes objects evenly across buckets, minimizing collisions and keeping access time close to O(1).

**Code Snippet:**
```java
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    Person person = (Person) o;
    return id == person.id && Objects.equals(name, person.name);
}

@Override
public int hashCode() {
    return Objects.hash(id, name); // Must match fields used in equals
}
```

---

## 6. How does ArrayList work internally?

**Answer:**
An `ArrayList` is backed by a dynamic **Object array**. When you add an element:
1.  It checks if the array has space.
2.  If full, it creates a **new array** with **50% more capacity** (`newCapacity = oldCapacity + (oldCapacity >> 1)`).
3.  It copies all old elements to the new array using `System.arraycopy`.
This makes access by index very fast (O(1)), but inserting/deleting in the middle is slow (O(n)) due to element shifting.

**Code Snippet:**
```java
// Visualization of internal growth logic (simplified)
public void add(E element) {
    if (size == elements.length) {
        int newSize = elements.length + (elements.length >> 1); // Grow by 50%
        elements = Arrays.copyOf(elements, newSize);
    }
    elements[size++] = element;
}
```

---

## 7. What is the difference between ArrayList and LinkedList?

**Answer:**
**`ArrayList`**: Backed by a **dynamic array**. Fast for **read/random access** (O(1)). efficient memory usage (contiguous). Slow for manipulation (insert/delete in middle) because of shifting.
**`LinkedList`**: Backed by a **doubly-linked list** (nodes with references to prev/next). Slow for **read/random access** (O(n)) because it must traverse nodes. Fast for **manipulation** (O(1) add/remove) provided you have the reference to the node, as no shifting is needed.

**Code Snippet:**
```java
List<String> arrayList = new ArrayList<>(); // Use for read-heavy
arrayList.get(100); // O(1) direct access

List<String> linkedList = new LinkedList<>(); // Use for add/remove-heavy
linkedList.addFirst("New"); // O(1) pointer update
```

---

## 8. How does Java handle memory management?

**Answer:**
Java uses automatic memory management via the **JVM**, divided primarily into:
1.  **Stack Memory:** Stores primitive variables and method call frames. Automatic allocation/deallocation when methods start/end. Thread-safe (each thread has its own stack).
2.  **Heap Memory:** Stores **Objects** and JRE classes. Shared by all threads. Objects here are managed by Garbage Collection.
3.  **Metaspace:** (Java 8+) Stores class metadata, static variables, and method bytecode in native memory.

**Code Snippet:**
```java
public void myMethod() {
    int x = 5;                        // Stored in Stack
    Person p = new Person("John");    // Reference 'p' in Stack, Object in Heap
} // 'x' and 'p' (reference) removed from Stack. Object implies eligible for GC.
```

---

## 9. What is the role of the final keyword?

**Answer:**
`final` is a non-access modifier that restricts modification.
1.  **final Variable:** Logic constant. Value cannot be reassigned once initialized.
2.  **final Method:** Logic lock. Cannot be overridden by subclasses (prevents changing behavior).
3.  **final Class:** Logic seal. Cannot be subclassed (e.g., `String`, `Integer`).

**Code Snippet:**
```java
final class Constants {       // 1. Class cannot be extended
    final double PI = 3.14;   // 2. Variable cannot be changed

    final void print() {      // 3. Method cannot be overridden
        System.out.println("Pi: " + PI);
    }
}
```

---

## 10. How does Garbage Collection work in Java?

**Answer:**
Garbage Collection (GC) is a background process that manages heap memory.
1.  **Mark:** GC identifies "live" objects reachable from GC Roots (stack variables, static references).
2.  **Sweep/Delete:** Unreachable objects are considered "garbage" and their memory is reclaimed.
3.  **Compact (Optional):** Moves objects to contiguous memory blocks to reduce fragmentation.
It uses a **Generational Strategy**: New objects start in **Young Generation** (fast/frequent GC). Survivors are promoted to **Old Generation** (slow/infrequent GC).

**Code Snippet:**
```java
public void createGarbage() {
    String s = new String("Trash");
    s = null; 
    // The String object "Trash" is now unreachable.
    // JVM will eventually reclaim its memory.
    System.gc(); // Request GC (recommendation only)
}
```

---

## 11. What is a WeakHashMap?

**Answer:**
A `WeakHashMap` is a special Map implementation where the **keys** are stored as **WeakReferences**.
-   **Behavior:** If a key object is no longer referenced anywhere else in the application (i.e., it's only referenced by the WeakHashMap), the Garbage Collector is free to reclaim it.
-   **result:** Once the key is garbage collected, the entry (key-value pair) is automatically removed from the map.
-   **Use Case:** Excellent for **caching** or storing metadata about objects where you don't want the map itself to prevent the object from being cleaned up.

**Code Snippet:**
```java
WeakHashMap<Object, String> map = new WeakHashMap<>();
Object key = new Object();
map.put(key, "Metadata");

key = null; // Key is now only referenced by WeakHashMap
System.gc(); // Force GC

// After GC, the entry is removed from the map
// Note: Verification requires waiting for GC to run
```

---

## 12. How is synchronization achieved in Java?

**Answer:**
Synchronization ensures that shared resources are accessed by only one thread at a time to prevent data inconsistency. It is achieved via:
1.  **`synchronized` keyword:** Can be applied to methods or specific blocks. It uses the intrinsic lock (monitor) of the object (or class).
2.  **`Lock` Interface (e.g., ReentrantLock):** Provides manual locking with more features (fairness, tryLock).
3.  **Atomic Classes:** (`AtomicInteger`, `AtomicReference`) generic thread-safe operations without explicit locks using CAS.

**Code Snippet:**
```java
public class Counter {
    private int count = 0;

    // Synchronized Method - Only one thread can execute this at a time
    public synchronized void increment() {
        count++;
    }

    // Synchronized Block - More granular control
    public void incrementBlock() {
        synchronized(this) {
            count++;
        }
    }
}
```

---

## 13. What are the different thread states?

**Answer:**
A Thread in Java can be in one of 6 states (defined in `Thread.State` enum):
1.  **NEW:** Created but not yet started (`start()` not called).
2.  **RUNNABLE:** Executing in the JVM (could be running or waiting for CPU).
3.  **BLOCKED:** Waiting for a monitor lock to enter/re-enter a synchronized block.
4.  **WAITING:** Waiting indefinitely for another thread (e.g., `Object.wait()`, `Thread.join()`).
5.  **TIMED_WAITING:** Waiting for another thread for a specified time (e.g., `Thread.sleep(1000)`).
6.  **TERMINATED:** Execution has completed.

**Code Snippet:**
```java
Thread t = new Thread(() -> System.out.println("Running"));
System.out.println(t.getState()); // NEW
t.start();
// State transitions to RUNNABLE, then TERMINATED
```

---

## 14. What is the difference between Runnable and Callable?

**Answer:**
Both are interfaces for tasks executed by threads, but they differ significantly:
-   **Runnable (`java.lang.Runnable`):**
    -   Method: `void run()`
    -   Cannot return a result.
    -   Cannot throw checked exceptions.
-   **Callable (`java.util.concurrent.Callable`):**
    -   Method: `V call()`
    -   **Returns a result** (via `Future`).
    -   **Can throw checked exceptions**.

**Code Snippet:**
```java
ExecutorService executor = Executors.newFixedThreadPool(2);

// Runnable
executor.submit(() -> System.out.println("Runnable task"));

// Callable
Future<Integer> future = executor.submit(() -> {
    return 123; // Returns logic
});
```

---

## 15. What is thread starvation?

**Answer:**
**Thread Starvation** occurs when a thread is perpetually denied access to shared resources (like CPU time or database connections) because other threads are monopolizing them.
-   **Causes:**
    -   High-priority threads constantly executing (swamping low-priority ones).
    -   Threads holding locks for infinite durations.
    -   Wait methods invoked without timeout.
-   Unlike Deadlock (where *no* one progresses), in Starvation, *some* threads progress while others freeze.

**Code Snippet:**
```java
// Concept: High priority thread monopolizing CPU
Thread high = new Thread(task);
high.setPriority(Thread.MAX_PRIORITY); // 10

Thread low = new Thread(task);
low.setPriority(Thread.MIN_PRIORITY);  // 1
```

---

## 16. What is the difference between wait(), sleep(), and yield()?

**Answer:**
1.  **`wait()`:** Defined in `Object`. Releases the lock. The thread waits until another thread invokes `notify()`. Used for inter-thread communication.
2.  **`sleep()`:** Defined in `Thread`. **Keeps the lock**. The thread pauses for a specific time and then wakes up. Used for pausing execution.
3.  **`yield()`:** Defined in `Thread`. Hint to scheduler that current thread is willing to pause and let other threads of same priority execute.

**Code Snippet:**
```java
synchronized(obj) {
    obj.wait();        // Releases lock, waits for notify
    Thread.sleep(1000); // Keeps lock, waits 1 sec
    Thread.yield();     // Suggests switch to other threads
}
```

---

## 17. How does the volatile keyword work?

**Answer:**
The `volatile` keyword guarantees **visibility** and **ordering** (happens-before relationship) of variables across threads.
-   **Visibility:** Reads and writes go directly to **Main Memory** (RAM), bypassing CPU Caches. If Thread A changes a volatile variable, Thread B sees it immediately.
-   **Atomicity:** It does **not** guarantee atomicity for compound actions (like `i++`).
-   **Usage:** Flags (e.g., `volatile boolean running`), singletons (Double-Checked Locking).

**Code Snippet:**
```java
private volatile boolean running = true;

public void run() {
    while (running) {
        // Safe: Loop will terminate immediately when 'running' is set to false by another thread
    }
}
```

---

## 18. What is a race condition? How to prevent it?

**Answer:**
A **Race Condition** occurs when multiple threads access and modify shared data concurrently, and the final outcome depends on the unpredictable timing of their execution (e.g., "Check-Then-Act" operations).
-   **Prevention:**
    -   Use `synchronized` or `Locks`.
    -   Use Atomic Variables (`AtomicInteger`).
    -   Use Thread-safe Collections (`ConcurrentHashMap`).

**Code Snippet:**
```java
// Race Condition (Unsafe)
count++; 

// Solution (Safe)
AtomicInteger atomicCount = new AtomicInteger(0);
atomicCount.incrementAndGet(); // Atomic operation
```

---

## 19. Explain ReentrantLock vs synchronized block.

**Answer:**
Both provide mutual exclusion, but `ReentrantLock` is more flexible.
1.  **Flexibility:** `ReentrantLock` allows `tryLock()` (attempt to lock without waiting forever) and `lockInterruptibly()`. `synchronized` blocks indefinitely.
2.  **Fairness:** `ReentrantLock` can be "fair" (longest waiting thread gets lock first). `synchronized` is unfair.
3.  **Scope:** `ReentrantLock` can be locked/unlocked in different methods. `synchronized` is block-scoped.
4.  **Cost:** `ReentrantLock` requires explicit `unlock()` in a `finally` block to avoid deadlocks.

**Code Snippet:**
```java
Lock lock = new ReentrantLock();

lock.lock();
try {
    // Critical Section
} finally {
    lock.unlock(); // Mandatory cleanup
}
```

---

## 20. What is thread pooling and how is it implemented?

**Answer:**
**Thread Pooling** maintains a pool of worker threads. Instead of creating and destroying a thread for every task (which is expensive in terms of detailed system resources), tasks are submitted to the pool and executed by existing idle threads.
-   **Implementation:** Java provides the `Executor` framework.
-   **Types:**
    -   `FixedThreadPool`: Helper pool with fixed number of threads.
    -   `CachedThreadPool`: Creates threads as needed, reuses if idle.
    -   `ScheduledThreadPool`: For delayed/periodic tasks.

**Code Snippet:**
```java
// Create a pool of 5 threads
ExecutorService pool = Executors.newFixedThreadPool(5);

for (int i = 0; i < 10; i++) {
    pool.submit(() -> System.out.println("Task executed by " + Thread.currentThread().getName()));
}
pool.shutdown();
```

---

## 21. What is the Fork/Join framework?

**Answer:**
The **Fork/Join Framework** (introduced in Java 7) is designed for parallel processing of tasks that can be broken down into smaller subtasks recursively (Divide and Conquer).
-   **Core Components:**
    -   `ForkJoinPool`: A specialized thread pool that implements **Work Stealing** (idle threads steal tasks from busy threads' deques).
    -   `RecursiveTask`: For tasks that return a result.
    -   `RecursiveAction`: For tasks that do not return a result.
-   **Usage:** It's the engine behind purely parallel operations like `Arrays.parallelSort()` and parallel Streams.

**Code Snippet:**
```java
public class Fibonacci extends RecursiveTask<Integer> {
    final int n;
    Fibonacci(int n) { this.n = n; }
    
    protected Integer compute() {
        if (n <= 1) return n;
        Fibonacci f1 = new Fibonacci(n - 1);
        f1.fork(); // Async execution
        Fibonacci f2 = new Fibonacci(n - 2);
        return f2.compute() + f1.join(); // Wait for result
    }
}
```

---

## 22. Explain Stream API with examples.

**Answer:**
The **Stream API** (Java 8) allows functional-style operations on streams of elements (sequences of data), supporting map-filter-reduce transformations.
-   **Key Features:**
    -   **Declarative:** Focus on *what* to do, not *how*.
    -   **Lazy Evaluation:** Intermediate operations (filter, map) are lazy; processing starts only when a terminal operation (collect, forEach) is invoked.
    -   **Parallelism:** Easy parallel processing via `.parallelStream()`.

**Code Snippet:**
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");

// Filter names starting with 'C', convert to uppercase, and collect to list
List<String> result = names.stream()
    .filter(name -> name.startsWith("C"))
    .map(String::toUpperCase)
    .collect(Collectors.toList());

System.out.println(result); // Output: [CHARLIE]
```

---

## 23. Difference between map() and flatMap() in Streams?

**Answer:**
-   **`map()`:** Transforms each element into **one** new element. Input `Stream<T>` -> Output `Stream<R>`.
    -   *Example:* Convert list of Strings to list of Integers (lengths).
-   **`flatMap()`:** Transforms each element into a **Stream** of elements, and then **flattens** (merges) all those streams into a single stream. Input `Stream<T>` -> Output `Stream<R>` (where R is the flattened type).
    -   *Example:* Convert a list of lists `[[1,2], [3,4]]` into a single list `[1,2,3,4]`.

**Code Snippet:**
```java
List<List<String>> listOfLists = Arrays.asList(
    Arrays.asList("a", "b"),
    Arrays.asList("c", "d")
);

// Map: Returns Stream<Stream<String>> (Stream of Lists) - usually not what you want
// FlatMap: Returns Stream<String> (a single flattened stream of "a","b","c","d")
List<String> flatList = listOfLists.stream()
    .flatMap(List::stream)
    .collect(Collectors.toList());
```

---

## 24. What are functional interfaces?

**Answer:**
A **Functional Interface** is an interface that contains **exactly one abstract method**.
-   They can have multiple `default` or `static` methods.
-   **Annotation:** `@FunctionalInterface` ensures the compiler checks this rule.
-   **Significance:** They are the target types for **Lambda Expressions** and Method References.
-   **Common Examples:** `Runnable`, `Callable`, `Comparator` and `java.util.function` interfaces:
    -   `Predicate<T>`: boolean test(T t)
    -   `Function<T, R>`: R apply(T t)
    -   `Consumer<T>`: void accept(T t)
    -   `Supplier<T>`: T get()

**Code Snippet:**
```java
@FunctionalInterface
interface MathOperation {
    int operate(int a, int b);
}

// Using Lambda
MathOperation addition = (a, b) -> a + b;
System.out.println(addition.operate(5, 3)); // 8
```

---

## 25. What is the difference between Optional.of() and Optional.ofNullable()?

**Answer:**
`Optional` is a container object used to avoid `NullPointerException` by explicitly representing the presence or absence of a value.
-   **`Optional.of(value)`:** Creates an Optional describing the given non-null value.
    -   **Throws:** `NullPointerException` immediately if the value is null.
    -   *Use when:* You are certain the value must not be null.
-   **`Optional.ofNullable(value)`:** Creates an Optional describing the value if non-null, otherwise returns an empty Optional.
    -   **Does NOT throw:** Exception if value is null.
    -   *Use when:* The value might legitimately be null.

**Code Snippet:**
```java
String name = null;

// Optional.of(name); // Throws NPE immediately

Optional<String> opt = Optional.ofNullable(name); // Safe
System.out.println(opt.isPresent()); // false
System.out.println(opt.orElse("Default")); // "Default"
```

---

## 26. What is method reference? Give examples.

**Answer:**
**Method Reference** is a shorthand notation of a lambda expression to call a method. It uses the `::` symbol.
There are four types:
1.  **Static Method:** `ClassName::staticMethodName` (e.g., `Math::max`)
2.  **Instance Method of Object:** `instance::methodName` (e.g., `System.out::println`)
3.  **Instance Method of Class (Arbitrary Object):** `ClassName::methodName` (e.g., `String::toLowerCase`)
4.  **Constructor:** `ClassName::new` (e.g., `ArrayList::new`)

**Code Snippet:**
```java
List<String> messages = Arrays.asList("Hello", "World");

// Lambda
messages.forEach(msg -> System.out.println(msg));

// Method Reference
messages.forEach(System.out::println);
```

---

## 27. How does Collectors.groupingBy() work?

**Answer:**
`Collectors.groupingBy()` is a static factory method in the Stream API akin to the "GROUP BY" clause in SQL.
-   It groups elements of a stream according to a **classification function**.
-   **Result:** A `Map` where:
    -   **Key:** The result of the classification function.
    -   **Value:** A List of items that match that key (by default).
-   You can also provide a downstream collector to aggregate values (e.g., counting, summing).

**Code Snippet:**
```java
List<String> items = Arrays.asList("apple", "banana", "apricot", "blueberry");

// Group by first letter
Map<Character, List<String>> grouped = items.stream()
    .collect(Collectors.groupingBy(s -> s.charAt(0)));

System.out.println(grouped); 
// Output: {a=[apple, apricot], b=[banana, blueberry]}
```

---

## 28. What is the default method in interfaces?

**Answer:**
Introduced in Java 8, **default methods** allow interfaces to have methods with implementation.
-   **Purpose:** To enable **Backward Compatibility**. It allows adding new methods to interfaces without breaking existing implementing classes.
-   **Keyword:** `default`.
-   **Override:** Implementing classes can override the default implementation if needed.
-   **Correction:** If a class implements two interfaces with the same default method signature, the class **must** override the method to resolve ambiguity.

**Code Snippet:**
```java
interface Vehicle {
    void start();
    
    default void honk() {
        System.out.println("Beep!");
    }
}

class Car implements Vehicle {
    public void start() { System.out.println("Starting"); }
    // honk() is inherited automatically
}
```

---

## 29. What are sealed classes in Java?

**Answer:**
**Sealed Classes** (Java 17, preview in 15) allow a class or interface to **restrict which other classes or interfaces may extend or implement it**.
-   **Goal:** To model a fixed set of alternatives (algebraic data types) and more control over inheritance hierarchy.
-   **Keywords:** `sealed`, `permits`.
-   **Subclasses:** Must be `final`, `sealed`, or `non-sealed`.

**Code Snippet:**
```java
public sealed class Shape permits Circle, Square { }

final class Circle extends Shape { }
final class Square extends Shape { }

// Error: class Triangle extends Shape {} // Not permitted
```

---

## 30. What is a record class in Java?

**Answer:**
**Records** (Java 16, preview in 14) are a concise way to create **immutable data carrier classes**.
-   **Boilerplate Reduction:** They automatically generate:
    -   Constructor
    -   Accessors (e.g., `name()`, not `getName()`)
    -   `equals()`, `hashCode()`, `toString()`
-   **Immutability:** Fields are `private final`.
-   **No Inheritance:** Records cannot extend other classes (they implicitly extend `java.lang.Record`).

**Code Snippet:**
```java
// Define a record
public record Person(String name, int age) {}

// Usage
Person p = new Person("Alice", 30);
System.out.println(p.name()); // Alice
System.out.println(p); // Person[name=Alice, age=30]
```

---

## 31. Difference between checked and unchecked exceptions.

**Answer:**
-   **Checked Exceptions:**
    -   Inherit from `Exception` (but not `RuntimeException`).
    -   **Compile-time enforcement:** The compiler forces you to handle them (try-catch) or declare them (throws).
    -   *Use Case:* Recoverable errors (e.g., `IOException`, `SQLException`, `FileNotFoundException`).
-   **Unchecked Exceptions (Runtime Exceptions):**
    -   Inherit from `RuntimeException`.
    -   **No Compile-time enforcement:** Handling is optional.
    -   *Use Case:* Programming errors (e.g., `NullPointerException`, `ArrayIndexOutOfBoundsException`, `IllegalArgumentException`).

**Code Snippet:**
```java
// Checked: Must handle
try {
    FileReader file = new FileReader("somefile.txt");
} catch (FileNotFoundException e) {
    e.printStackTrace();
}

// Unchecked: Can crash if not handled, but compiler doesn't complain
int[] arr = new int[5];
// System.out.println(arr[10]); // Throws ArrayIndexOutOfBoundsException at runtime
```

---

## 32. Custom exception handling in real-world applications.

**Answer:**
In real-world apps (like Spring Boot), custom exceptions specific to the domain are created to make error handling more meaningful and structure the response to the client.
-   **Best Practice:**
    -   Extend `RuntimeException` (for cleaner code, unchecked).
    -   Create a global exception handler (e.g., `@ControllerAdvice` in Spring) to catch these exceptions and return a standard JSON error response (status, message, timestamp).

**Code Snippet:**
```java
// 1. Define Custom Exception
public class UserNotFoundException extends RuntimeException {
    public UserNotFoundException(String message) {
        super(message);
    }
}

// 2. Throw it in business logic
if (user == null) {
    throw new UserNotFoundException("User with ID 123 not found");
}

// 3. Handle it (Global Handler Example)
// @ExceptionHandler(UserNotFoundException.class)
// public ResponseEntity<String> handle(UserNotFoundException ex) {
//     return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
// }
```

---

## 33. What is the diamond problem in Java?

**Answer:**
The **Diamond Problem** is an ambiguity that arises in multiple inheritance when a class inherits from two classes that have a method with the same signature.
-   **Java's Solution:** Java **does not support multiple inheritance of classes**. A class can extend only one superclass, avoiding this issue.
-   **Interfaces:** Java allows implementing multiple interfaces. If two interfaces have default methods with the same signature, the compiler forces the implementing class to override the method to resolve the conflict explicitly.

**Code Snippet:**
```java
interface A {
    default void hello() { System.out.println("Hello A"); }
}

interface B {
    default void hello() { System.out.println("Hello B"); }
}

// Compile Error if hello() is not overridden
class C implements A, B {
    @Override
    public void hello() {
        A.super.hello(); // Resolve ambiguity: Call A's version
        // or B.super.hello();
    }
}
```

---

## 34. How does autoboxing/unboxing work?

**Answer:**
-   **Autoboxing:** Automatic conversion of primitive types to their corresponding object wrapper classes (e.g., `int` -> `Integer`).
-   **Unboxing:** Automatic conversion of wrapper classes back to primitives (e.g., `Integer` -> `int`).
-   **Mechanism:** The compiler inserts `Integer.valueOf(int)` for boxing and `Integer.intValue()` for unboxing.
-   **Risk:** Unboxing a `null` wrapper object throws a `NullPointerException`.

**Code Snippet:**
```java
// Autoboxing
Integer numObj = 10; // Compiler does: Integer.valueOf(10)

// Unboxing
int numPrim = numObj; // Compiler does: numObj.intValue()

Integer nullObj = null;
// int crash = nullObj; // Throws NullPointerException
```

---

## 35. Explain Enum in Java.

**Answer:**
An **Enum** (Enumeration) is a special Java type used to define a collection of constants.
-   **Features:**
    -   Type-safe.
    -   Can have fields, methods, and constructors.
    -   Can implement interfaces.
    -   implicitly `static` and `final`.
    -   Used in `switch` statements.
-   **Under the hood:** It extends `java.lang.Enum`.

**Code Snippet:**
```java
enum UserRole {
    ADMIN("Administrator"), 
    USER("Regular User");

    private final String description;

    UserRole(String description) { this.description = description; }

    public String getDescription() { return description; }
}

public class Test {
    public static void main(String[] args) {
        UserRole role = UserRole.ADMIN;
        System.out.println(role.getDescription()); // Output: Administrator
    }
}
```

---

## 36. When to use TreeMap vs HashMap?

**Answer:**
-   **`HashMap`:**
    -   **Order:** No guarantee of order (neither insertion nor sorted).
    -   **Performance:** O(1) for get/put.
    -   **Use Case:** General-purpose caching, lookups where order doesn't matter.
-   **`TreeMap`:**
    -   **Order:** Sorted according to the **natural ordering** of keys or a custom `Comparator`.
    -   **Performance:** O(log n) for get/put (Red-Black Tree).
    -   **Use Case:** When you need keys to be sorted (e.g., range views, navigation).

**Code Snippet:**
```java
Map<String, Integer> treeMap = new TreeMap<>();
treeMap.put("Banana", 2);
treeMap.put("Apple", 1);
treeMap.put("Cherry", 3);

// Keys will be sorted alphabetically
System.out.println(treeMap); // {Apple=1, Banana=2, Cherry=3}
```

---

## 37. Why should hashCode() be consistent with equals()?

**Answer:**
If `equals()` is overridden but `hashCode()` is not (or vice-versa), it violates the contract required by hash-based collections (`HashMap`, `HashSet`).
-   **The Rule:** Equal objects must have equal hash codes.
-   **Consequence:** If two "equal" objects have different hash codes, `HashMap` will place them in different buckets. You won't be able to retrieve an object using an equal key because the map searches in the wrong bucket.

**Code Snippet:**
```java
// Broken Implementation
class Key {
    int id;
    // equals() checks id, but hashCode() is default (memory address)
}

Map<Key, String> map = new HashMap<>();
map.put(new Key(1), "Data");
// map.get(new Key(1)) will likely return NULL because hashCodes differ
```

---

## 38. How to make an object immutable?

**Answer:**
To create an immutable class:
1.  Declare the class as `final` (cannot be subclassed).
2.  Make all fields `private` and `final`.
3.  **No Setters:** Do not provide setter methods.
4.  **Constructor Initialization:** Initialize all fields via the constructor.
5.  **Defensive Copying:** If a field is a mutable object (like `Date` or `List`), return a copy of it in the getter, not the original reference.

**Code Snippet:**
```java
public final class ImmutablePerson {
    private final String name;
    private final List<String> hobbies;

    public ImmutablePerson(String name, List<String> hobbies) {
        this.name = name;
        this.hobbies = new ArrayList<>(hobbies); // Deep Copy
    }

    public List<String> getHobbies() {
        return new ArrayList<>(hobbies); // Return Copy to prevent external modification
    }
}
```

---

## 39. What is the use of transient keyword?

**Answer:**
The `transient` keyword is used in **Serialization**.
-   **Function:** It indicates that a field should **not be serialized**. When an object is converted to a byte stream (saved to file/network), transient fields are ignored.
-   **Deserialization:** When the object is restored, the transient field is restricted to its default value (null for objects, 0 for int).
-   **Use Case:** Security (don't save passwords), or derived fields that can be recalculated.

**Code Snippet:**
```java
public class User implements Serializable {
    private String username;
    private transient String password; // Will NOT be saved
    
    // ...
}
```

---

## 40. What is reflection in Java?

**Answer:**
**Reflection** is an API that allows a program to examine or modify the behavior of classes, interfaces, fields, and methods at **runtime**, even if they are private.
-   **Capabilities:** Instantiate new objects, invoke methods, get/set field values dynamically.
-   **Drawbacks:** Slower performance, breaks encapsulation, harder to debug.
-   **Use Case:** Frameworks (Spring, Hibernate), JUnit, Dependency Injection containers.

**Code Snippet:**
```java
Class<?> clazz = Class.forName("java.util.ArrayList");
Method[] methods = clazz.getDeclaredMethods();

for (Method method : methods) {
    System.out.println("Method name: " + method.getName());
}

// Access private field
Field field = MyClass.class.getDeclaredField("privateField");
field.setAccessible(true); // Bypass security check
```

---

## 41. Difference between static and instance initialization block.

**Answer:**
-   **Static Initialization Block (`static { ... }`):**
    -   Executed **once** when the class is loaded by the ClassLoader.
    -   Used to initialize static variables or perform one-time setup.
-   **Instance Initialization Block (`{ ... }`):**
    -   Executed **every time** an instance of the class is created.
    -   Runs **before** the constructor (but after the super constructor).
    -   Used to share common code across multiple constructors.

**Code Snippet:**
```java
public class InitExample {
    static {
        System.out.println("Static Block - Runs Once");
    }

    {
        System.out.println("Instance Block - Runs for every 'new'");
    }

    public InitExample() {
        System.out.println("Constructor");
    }

    public static void main(String[] args) {
        new InitExample();
        new InitExample();
    }
}
// Output:
// Static Block - Runs Once
// Instance Block - Runs for every 'new'
// Constructor
// Instance Block - Runs for every 'new'
// Constructor
```

---

## 42. Difference between shallow copy and deep copy.

**Answer:**
When copying an object:
-   **Shallow Copy:**
    -   Creates a new object but copies the **references** of the nested objects.
    -   Changes to the nested objects in the copy **affect** the original.
    -   Default behavior of `Object.clone()`.
-   **Deep Copy:**
    -   Creates a new object and **recursively copies** all nested objects.
    -   The copy and original are completely independent.

**Code Snippet:**
```java
class Address { String city; }
class Person implements Cloneable { 
    Address address; 
    // ... clone() implementation 
}

// Shallow Copy Scenario
Person p1 = new Person();
p1.address = new Address(); p1.address.city = "NY";

Person p2 = p1.clone(); // Shallow copy
p2.address.city = "LA";

System.out.println(p1.address.city); 
// Output: "LA" (Original modified because they share the Address object)
```

---

## 43. What is the use of `System.identityHashCode()`?

**Answer:**
`System.identityHashCode(obj)` returns the hash code for the given object as determined by the default `Object.hashCode()` implementation (typically based on memory address), **even if the object's class has overridden `hashCode()`**.
-   **Use Case:**
    -   To check if two references truly point to the same instance when `equals()` and `hashCode()` have been overridden to check content.
    -   Used by `IdentityHashMap`.

**Code Snippet:**
```java
String s1 = new String("Hello");
String s2 = new String("Hello");

// Logic hash code (based on content) - SAME
System.out.println(s1.hashCode() == s2.hashCode()); // true

// Identity hash code (based on memory address) - DIFFERENT
System.out.println(System.identityHashCode(s1) == System.identityHashCode(s2)); // false
```

---

## 44. Explain CompletableFuture with example.

**Answer:**
`CompletableFuture` (Java 8) is an enhancement over `Future` used for asynchronous programming. It allows you to:
-   **Chain** multiple async tasks (pipeline).
-   **Combine** results of multiple tasks.
-   **Handle Exceptions** gracefully.
-   Manually complete the future.
-   Run tasks without blocking the main thread until the result is needed.

**Code Snippet:**
```java
CompletableFuture.supplyAsync(() -> {
    return "Hello"; // Run in background
})
.thenApply(s -> s + " World") // Transform result
.thenAccept(System.out::println); // Consume result

// Main thread can continue...
```

---

## 45. How do you implement a singleton pattern?

**Answer:**
The Singleton pattern ensures a class has only **one instance** and provides a global point of access.
**Best Practice ("Bill Pugh" Initialization):**
-   Lazy initialization.
-   Thread-safe without synchronization overhead.
-   Relies on the JVM's class loading mechanism.

**Code Snippet:**
```java
public class Singleton {
    private Singleton() {} // Private constructor

    private static class Holder {
        private static final Singleton INSTANCE = new Singleton();
    }

    public static Singleton getInstance() {
        return Holder.INSTANCE;
    }
}
```

---

## 46. What are some ways to break a singleton?

**Answer:**
A standard Singleton can be broken (creating >1 instance) via:
1.  **Reflection:** Setting the private constructor to accessible.
2.  **Serialization:** Deserializing an object creates a new instance (fix: implement `readResolve`).
3.  **Cloning:** If the class implements `Cloneable` (fix: throw exception in `clone`).
4.  **Multi-threading:** If not implemented correctly (e.g., simplistic lazy loading without sync).
**Solution:** Use an **Enum** singleton (Java guarantees exactly one instance per constant).

**Code Snippet:**
```java
// Breaking with Reflection
Constructor<Singleton> constructor = Singleton.class.getDeclaredConstructor();
constructor.setAccessible(true);
Singleton s2 = constructor.newInstance(); 

// Enum Singleton (The Safe Way)
public enum SafeSingleton {
    INSTANCE;
    public void doWork() { }
}
```

---

## 47. What is double-checked locking?

**Answer:**
Double-Checked Locking is an optimization for **Lazy Initialization** of a Singleton to reduce synchronization overhead.
1.  Check if instance is null (no locking).
2.  If null, enter `synchronized` block.
3.  Check if instance is null **again** (in case another thread created it while we waited).
4.  Create instance.
**Crucial:** The `instance` variable must be **`volatile`** to prevent instruction reordering issues.

**Code Snippet:**
```java
public class Singleton {
    private static volatile Singleton instance; // volatile is key

    public static Singleton getInstance() {
        if (instance == null) { // First check
            synchronized (Singleton.class) {
                if (instance == null) { // Second check
                    instance = new Singleton();
                }
            }
        }
        return instance;
    }
}
```

---

## 48. What are phantom references?

**Answer:**
**PhantomReference** is the weakest reference type in Java (weaker than Soft and Weak).
-   **Flavor:** You **cannot** retrieve the object from a PhantomReference (get() always returns null).
-   **Purpose:** It is used solely to determine **when an object has been physically removed from memory**.
-   **Mechanism:** It must be used with a `ReferenceQueue`. When the GC collects the object, it puts the phantom reference into the queue.
-   **Use Case:** Cleaning up non-java resources (like native memory) more flexibly than `finalize()`.

**Code Snippet:**
```java
Object obj = new Object();
ReferenceQueue<Object> queue = new ReferenceQueue<>();
PhantomReference<Object> phantom = new PhantomReference<>(obj, queue);

obj = null;
System.gc();

// Later, check queue...
if (queue.poll() != null) {
    System.out.println("Object has been garbage collected");
}
```

---

## 49. Why is clone() considered bad practice?

**Answer:**
The `clone()` method (and `Cloneable` interface) is flawed because:
1.  **Shallow Copy Default:** It performs a shallow copy, which causes issues with mutable fields.
2.  **No Constructor:** It bypasses the constructor, which can skip initialization logic.
3.  **Marker Interface:** `Cloneable` is a marker interface but doesn't define `clone()`; `Object` defines it as `protected`. You have to override it and widen visibility.
4.  **Exceptions:** Throws `CloneNotSupportedException` (checked) which is annoying.
**Better Alternative:** Copy Constructor or Factory Method.

**Code Snippet:**
```java
// Better than clone(): Copy Constructor
public class Person {
    private String name;
    
    public Person(Person other) {
        this.name = other.name; // Manual deep copy logic here if needed
    }
}
```

---

## 50. How would you design your own custom collection?

**Answer:**
To design a custom collection (e.g., a simplified `ArrayList`):
1.  **Backing Structure:** Choose an internal data structure (e.g., `Object[]` array).
2.  **Generics:** Use generics `<E>` for type safety.
3.  **Dynamic Resizing:** Implement logic to grow the array when full.
4.  **Iterable:** Implement `Iterable<E>` to support for-each loops.
5.  **Methods:** Implement `add`, `get`, `remove`, `size`.

**Code Snippet:**
```java
public class MyList<E> implements Iterable<E> {
    private Object[] elements = new Object[10];
    private int size = 0;

    public void add(E item) {
        if (size == elements.length) {
           // resizing logic...
        }
        elements[size++] = item;
    }

    public E get(int index) {
        return (E) elements[index];
    }

    public Iterator<E> iterator() {
        return new Iterator<E>() { /* ... */ };
    }
}
```

---

## 51. Explain method overloading vs overriding.

**Answer:**
-   **Overloading (Compile-Time Polymorphism):**
    -   Same method name, **different parameter list** (type, number, or order).
    -   Return type can be different (not sufficient alone).
    -   Happens within the **same class** (or subclass).
    -   Resolved by compiler based on reference type.
-   **Overriding (Run-Time Polymorphism):**
    -   Same method name, **same parameter list**, same return type (or covariant).
    -   Happens in **parent and child classes** (Inheritance).
    -   Resolved by JVM based on the actual object type.
    -   Annotations: `@Override` is recommended.

**Code Snippet:**
```java
class Calc {
    // Overloading
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}

class AdvancedCalc extends Calc {
    // Overriding
    @Override
    int add(int a, int b) {
        System.out.println("Using Advanced Calc");
        return a + b;
    }
}
```

---

## 52. Explain covariant return types.

**Answer:**
Since Java 5, when Overriding a method, the return type in the child class does not need to be exactly the same as the parent class; it can be a **subclass (subtype)** of the parent's return type. This is called a **Covariant Return Type**.
-   **Benefit:** It eliminates the need for type casting in the client code when working with factory methods or specific implementations.

**Code Snippet:**
```java
class Animal {
    Animal get() { return new Animal(); }
}

class Dog extends Animal {
    @Override
    Dog get() { // Covariant Return Type (Dog is-a Animal)
        return new Dog(); 
    }
}

// Usage
Dog d = new Dog().get(); // No casting needed: (Dog) new Dog().get() 
```

---

## 53. How does Java handle pass-by-value or reference?

**Answer:**
Java is **strictly Pass-By-Value**.
-   **Primitives:** A copy of the actual value (e.g., `5`) is passed. Changing the local variable inside the method does not affect the original variable.
-   **Objects:** A copy of the **reference** (memory address) is passed. 
    -   You **can** modify the object's state (e.g., `obj.setName("New")`) because both the original and the copy point to the same object.
    -   You **cannot** reassign the original reference to a new object (e.g., `obj = new Object()`) inside the method; this only changes the local copy of the reference.

**Code Snippet:**
```java
void change(int x, StringBuilder sb) {
    x = 100; // Won't affect original x
    sb.append(" World"); // Will affect original sb
    sb = new StringBuilder("New"); // Won't affect original reference
}
```

---

## 54. Can we override private/static/final methods?

**Answer:**
-   **Private:** **No.** Private methods are not visible to subclasses, so they cannot be overridden. Defining a method with the same name in a subclass is just a new, unrelated method.
-   **Final:** **No.** The `final` keyword specifically prevents overriding. Compiler error.
-   **Static:** **No.** Static methods belong to the class, not the instance. If you define a static method with the same signature in the subclass, it is called **Method Hiding**, not overriding. Parent reference calls parent static method; Child reference calls child static method.

**Code Snippet:**
```java
class Parent {
    static void show() { System.out.println("Parent Static"); }
}

class Child extends Parent {
    static void show() { System.out.println("Child Static"); } // Hiding
}

Parent p = new Child();
p.show(); // Output: "Parent Static" (Binding happens at compile time)
```

---

## 55. When would you use an abstract class over interface?

**Answer:**
-   **Use Abstract Class when:**
    -   You want to share **state** (non-static, non-final fields) among related classes.
    -   You want to provide a common base implementation with a constructor.
    -   You expect to add methods in the future (adding abstract methods covers strict contract, but concrete methods can be added easily).
    -   Strict "Is-A" relationship.
-   **Use Interface when:**
    -   You want to define a **role** or **capability** (e.g., `Comparable`, `Serializable`) implemented by unrelated classes.
    -   You need multiple inheritance of type.
    -   API definition is stable.

**Code Snippet:**
```java
// Abstract Class: Shared state
abstract class Employee {
    String name; // State
    public Employee(String name) { this.name = name; }
    abstract double calculatePay();
}

// Interface: Capability
interface Payable {
    void processPayment();
}
```

---

## 56. What is `java.lang.instrument` used for?

**Answer:**
The `java.lang.instrument` package provides services that allow **Java Agents** to **instrument** (modify) programs running on the JVM.
-   **Mechanism:** It allows an agent to modify the byte-code of classes **before** they are loaded by the ClassLoader (using `ClassFileTransformer`).
-   **Use Cases:**
    -   **Profilers/Monitoring Tools:** (e.g., New Relic, Dynatrace) to inject timing code.
    -   **Code Coverage Tools:** (e.g., JaCoCo) to track lines executed.
    -   **AOP Frameworks:** To inject aspects dynamically.

**Code Snippet:**
```java
// Agent setup (conceptual)
public static void premain(String args, Instrumentation inst) {
    inst.addTransformer(new MyByteCodeTransformer());
}
```

---

## 57. What is Metaspace in Java?

**Answer:**
**Metaspace** (introduced in Java 8) replaced the **PermGen** (Permanent Generation) memory space.
-   **Purpose:** Stores class metadata (class definitions, method bytecodes, static variables).
-   **Key Difference:** 
    -   **PermGen:** Was part of Heap reference (contiguous) and had a fixed max size, leading to frequent `OutOfMemoryError: PermGen space`.
    -   **Metaspace:** Uses **Native Memory** (OS memory). It grows automatically by default (up to available system RAM), reducing OOM errors unless explicitly capped via `-XX:MaxMetaspaceSize`.

**Code Snippet:**
```bash
# JVM Argument to limit Metaspace
java -XX:MaxMetaspaceSize=256m -jar app.jar
```

---

## 58. How to detect memory leaks in Java?

**Answer:**
A memory leak happens when objects are no longer used but are still referenced (e.g., in a static Map), preventing GC.
**Detection Steps:**
1.  **Monitor:** Use tools like **VisualVM** or **JConsole** to watch Heap usage. If it keeps growing despite GC, there's a leak.
2.  **Heap Dump:** Take a snapshot of memory (`jmap` or VisualVM) when usage is high.
3.  **Analyze:** Use **Eclipse MAT (Memory Analyzer Tool)**.
    -   Run "Leak Suspects Report".
    -   Check "Dominator Tree" to see which objects consume the most memory.
    -   Tracing "GC Roots" validates why an object is still alive.

**Code Snippet:**
```java
// Common Leak: Static Cache
public class Leaky {
    private static final List<Object> cache = new ArrayList<>();
    
    public void addToCache(Object o) {
        cache.add(o); // Never removed -> Leak!
    }
}
```

---

## 59. What is ClassLoader? Types of class loaders?

**Answer:**
A **ClassLoader** is responsible for loading class files (`.class`) from the file system/network into the JVM memory.
**Delegation Hierarchy:**
1.  **Bootstrap ClassLoader:** Loads core Java libraries (`rt.jar`, `java.lang.*`). Written in native code (C++).
2.  **Platform/Extension ClassLoader:** Loads extensions from `lib/ext`.
3.  **Application/System ClassLoader:** Loads classes from the **Classpath** (`-cp`).
**Delegation Model:** A loader asks its parent to load the class first. Only if the parent fails does the child attempt to load it.

**Code Snippet:**
```java
public class LoaderCheck {
    public static void main(String[] args) {
        // App ClassLoader
        System.out.println(LoaderCheck.class.getClassLoader()); 
        
        // Bootstrap (returns null usually as it's native)
        System.out.println(String.class.getClassLoader()); 
    }
}
```

---

## 60. What is JIT compiler?

**Answer:**
**JIT (Just-In-Time) Compiler** is a component of the JVM that optimizes performance.
-   **Process:**
    1.  Java compiles code to **Bytecode** (platform independent).
    2.  Initially, JVM **interprets** bytecode (slow).
    3.  **HotSpot Detection:** The JVM monitors which methods are called frequently ("Hot Spots").
    4.  **JIT Compilation:** It compiles these hot bytecode sections into **Native Machine Code** (CPU specific).
    5.  Future calls execute the native code directly (Fast).
-   **Optimizations:** Inlining, Dead Code Elimination, Loop Unrolling.

**Code Snippet:**
```text
// Concept:
Bytecode (Input) -> [Interpreter + Profiler] -> (Hot?) -> [JIT Compiler] -> Native Code -> CPU
```

---

## 61. How do annotations work internally?

**Answer:**
Annotations in Java are a form of metadata.
-   **Internal Representation:** When you define an `@interface`, the compiler creates an interface that extends `java.lang.annotation.Annotation`.
-   **Runtime:** When the JVM loads a class with existing **RUNTIME** retention annotations, it creates a **Dynamic Proxy** implementing the annotation interface.
-   **Access:** When you call `method.getAnnotation(MyAnno.class)`, the JVM returns this proxy object, which intercepts calls to the annotation's methods and returns the values provided.

**Code Snippet:**
```java
// Definition
@Retention(RetentionPolicy.RUNTIME)
@interface MyInfo {
    String value();
}

// Internal view (Conceptual)
// public interface MyInfo extends Annotation {
//     String value();
// }
```

---

## 62. How to create custom annotations?

**Answer:**
To create a custom annotation, use result `@interface`. You must specify:
1.  **Retention Policy (`@Retention`):** When is it available? (SOURCE, CLASS, RUNTIME).
2.  **Target (`@Target`):** Where can it be used? (METHOD, TYPE, FIELD, etc.).
3.  **Attributes:** Define methods (look like fields) which can have default values.

**Code Snippet:**
```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface LogExecutionTime {
    boolean active() default true; 
}

// Usage
public class Service {
    @LogExecutionTime(active = true)
    public void serve() { ... }
}
```

---

## 63. What is annotation processing in Java?

**Answer:**
**Annotation Processing** is a compile-time hook.
-   **Tool:** `javac` scans source files for annotations.
-   **Processor:** You can write an `AbstractProcessor` to handle specific annotations.
-   **Action:** Processors can analyze code and **generate new source files** (e.g., Lombok generates getters/setters, Dagger generates dependency injection code).
-   **Constraint:** They cannot *modify* existing source files, only create new ones.

**Code Snippet:**
```java
@SupportedAnnotationTypes("com.example.MyAnno")
public class MyProcessor extends AbstractProcessor {
    @Override
    public boolean process(Set<? extends TypeElement> annotations, RoundEnvironment roundEnv) {
        // Logic to generate code
        return true;
    }
}
```

---

## 64. What are lambdas and how do they work internally?

**Answer:**
A **Lambda Expression** is a concise way to represent an instance of a Functional Interface.
-   **Internal Working (invokedynamic):**
    -   Unlike anonymous inner classes (which generate a separate `.class` file like `Test$1.class`), lambdas do **NOT** generate a class file at compile time.
    -   Compiler generates an `invokedynamic` bytecode instruction.
    -   **Runtime:** The JVM uses `LambdaMetafactory` to spin a lightweight class on the fly that implements the interface and delegates the call to the actual logic (often a private static method generated in the host class).

**Code Snippet:**
```java
Runnable r = () -> System.out.println("Run");
// Compiles to invokedynamic instruction
// Runtime: Creates specific implementation of Runnable
```

---

## 65. Explain Type Erasure in Generics.

**Answer:**
**Type Erasure** is the process by which the Java Compiler removes all generic type information directly after compilation to ensure **backward compatibility** with older Java versions (pre-Java 5).
-   `List<String>` and `List<Integer>` both become just raw `List` at runtime.
-   Type checks are inserted at compile-time.
-   Casts are inserted automatically where data is retrieved.

**Code Snippet:**
```java
// Compile Time
List<String> list = new ArrayList<>();
list.add("Hello");
String s = list.get(0);

// After Erasure (Runtime Representation)
List list = new ArrayList(); // Generic type removed
list.add("Hello");
String s = (String) list.get(0); // Cast inserted
```

---

## 66. How are Generics implemented internally?

**Answer:**
Generics are a **compile-time restriction**.
1.  **Code Check:** Compiler verifies type safety (e.g., prevents adding `Integer` to `List<String>`).
2.  **Erasure:** Compiler removes `<T>` and replaces it with the underlying bound (usually `Object`, or the upper bound like `Number` if defined `<T extends Number>`).
3.  **Bridge Methods:** Generated to preserve polymorphism when extending generic classes.
This implies you cannot check `if (obj instanceof List<String>)` at runtime because the type info is gone.

**Code Snippet:**
```java
public class Box<T> {
    private T val;
}
// Becomes internally:
// public class Box { private Object val; }
```

---

## 67. Explain bounded vs unbounded wildcards.

**Answer:**
Wildcards `?` allows flexibility in Generics.
1.  **Unbounded (`<?>`):** Accepts any type. Read-only (conceptually, objects are treated as `Object`).
2.  **Upper Bounded (`<? extends Number>`):** Accepts Number or its subclasses. "Producer" - you can read specific types (Number), but cannot write (don't know if actual list is Integer or Double).
3.  **Lower Bounded (`<? super Integer>`):** Accepts Integer or its superclasses. "Consumer" - you can write Integers into it.

**Code Snippet:**
```java
// Upper Bound (Producer)
public void printNumbers(List<? extends Number> list) {
    Number n = list.get(0); // Safe to read
    // list.add(10); // COMPILE ERROR: Unsafe
}

// Lower Bound (Consumer)
public void addNumbers(List<? super Integer> list) {
    list.add(10); // Safe to add Integer
}
```

---

## 68. What is raw type in Java?

**Answer:**
A **Raw Type** is the name of a generic class or interface without any type arguments (e.g., using `List` instead of `List<String>`).
-   **Risk:** It bypasses generic type checks, allowing you to insert any object type. This often leads to `ClassCastException` at runtime.
-   **Usage:** Only for backward compatibility. Avoid in new code.

**Code Snippet:**
```java
List rawList = new ArrayList(); // Raw type
rawList.add("String");
rawList.add(10); // Works (Compiler warning only)

// Runtime Error
String s = (String) rawList.get(1); // ClassCastException
```

---

## 69. How would you make a list thread-safe?

**Answer:**
Standard `ArrayList` is not thread-safe. Options to make it safe:
1.  **`Collections.synchronizedList(new ArrayList<>())`:** Wraps the list. All individual methods (add, get) are synchronized. (Note: Iteration still requires manual synchronization).
2.  **`CopyOnWriteArrayList`:** (JUC) Thread-safe. Best for **Read-Heavy** scenarios. Mutations create a fresh copy of the array. Iterators are fail-safe.
3.  **`Vector`:** (Legacy) Synchronized, but generally deprecated due to performance.

**Code Snippet:**
```java
List<String> safeList = Collections.synchronizedList(new ArrayList<>());

// Must synchronize manually during iteration!
synchronized(safeList) {
    for (String s : safeList) { /* ... */ }
}
```

---

## 70. How to avoid deadlock in concurrent programming?

**Answer:**
A **Deadlock** happens when two threads wait forever for each other to release locks.
**Avoidance Strategies:**
1.  **Lock Ordering:** Always acquire locks in a consistent, fixed global order. (e.g., Always Lock A then Lock B).
2.  **Lock Timeout:** Use `Lock` interface with `tryLock(timeout)`. If lock helps for too long, back off and retry.
3.  **Granularity:** Keep synchronized blocks as short as possible. Avoid calling alien methods while holding locks.

**Code Snippet:**
```java
// Strategy: Order Locks by HashCode
int hashA = System.identityHashCode(objA);
int hashB = System.identityHashCode(objB);

if (hashA < hashB) {
    synchronized (objA) { synchronized (objB) { /* work */ } }
} else {
    synchronized (objB) { synchronized (objA) { /* work */ } }
}
```

---

## 71. Difference between Spring and Spring Boot.

**Answer:**
-   **Spring Framework:**
    -   A comprehensive framework for building Java Enterprise applications.
    -   Requires **extensive XML or Java configuration** (boilerplate) to set up components (DataSource, MVC, TransactionManager).
    -   No built-in server; you must package as a WAR and deploy to an external Tomcat/Jetty.
-   **Spring Boot:**
    -   An extension of Spring designed to simplify startup and development.
    -   **Auto-Configuration:** Automatically configures beans based on dependencies on the classpath.
    -   **Stand-alone:** Embeds a server (Tomcat/Jetty) so you can run as a JAR (`java -jar app.jar`).
    -   **Opinionated Defaults:** Reduces boilerplate significantly.

**Code Snippet:**
```java
// Spring (Legacy): explicit setup needed
// @Bean public ViewResolver viewResolver() { ... }

// Spring Boot: Just add dependency
// implementation 'org.springframework.boot:spring-boot-starter-web'
// (Tomcat and Spring MVC are auto-configured)
```

---

## 72. What is dependency injection and how is it implemented in Spring?

**Answer:**
**Dependency Injection (DI)** is a design pattern where objects receive their dependencies (collaborators) from an external source rather than creating them themselves. It promotes loose coupling.
Spring implements DI via the **IoC (Inversion of Control) Container**.
**Types of Injection:**
1.  **Constructor Injection** (Recommended): Dependencies passed via constructor. Ensures immutability and valid state.
2.  **Setter Injection:** Dependencies passed via setter methods. Optional dependencies.
3.  **Field Injection:** Direct injection into fields using `@Autowired`. (Discouraged due to testing difficulty).

**Code Snippet:**
```java
@Service
public class UserService {
    private final UserRepository repo;

    // Constructor Injection (Best Practice)
    @Autowired 
    public UserService(UserRepository repo) {
        this.repo = repo;
    }
}
```

---

## 73. Difference between `@Component`, `@Service`, `@Repository`, and `@Controller`.

**Answer:**
All four are stereotypes for Spring-managed beans.
-   **`@Component`:** Check generic stereotype for any Spring-managed component.
-   **`@Service`:** Specialization of `@Component` for the **Service Layer** (Business Logic). Semantically indicates business processing.
-   **`@Repository`:** Specialization for the **DAO Layer** (Data Access). It adds automatic translation of database-specific exceptions (e.g., `SQLException`) into Spring's `DataAccessException` hierarchy.
-   **`@Controller`:** Specialization for the **Presentation Layer** (Spring MVC). Marks the class as a web request handler.

**Code Snippet:**
```java
@Repository
public class UserDao { ... } // Handles DB Exceptions

@Service
public class UserService { ... } // Business Logic

@Controller
public class UserController { ... } // Web Endpoints
```

---

## 74. What is the role of `@Autowired` and how does it work?

**Answer:**
`@Autowired` is used for **automatic dependency injection**.
-   **Mechanism:** Spring scans for a bean that matches the type of the property/constructor argument.
-   **ByType:** Default behavior. If exactly one bean of that type exists, it's injected.
-   **Ambiguity:** If multiple beans of the same type exist, Spring throws an exception unless you use `@Qualifier("beanName")` to specify which one, or mark one as `@Primary`.

**Code Snippet:**
```java
@Autowired
@Qualifier("mySqlDataSource") // Resolves ambiguity
private DataSource dataSource;
```

---

## 75. How does Spring Boot auto-configuration work?

**Answer:**
Auto-configuration attempts to automatically configure your Spring application based on the jar dependencies that you have added.
-   **Mechanism:**
    -   Triggered by `@EnableAutoConfiguration` (part of `@SpringBootApplication`).
    -   Scans the classpath for `META-INF/spring.factories` (or `imports` file in newer versions).
    -   Uses `@Conditional` annotations (e.g., `@ConditionalOnClass`, `@ConditionalOnMissingBean`) to decide whether to create a bean.
-   **Example:** If `H2` database jar is on the classpath and no `DataSource` bean is manually defined, Spring Boot auto-configures an in-memory H2 database.

**Code Snippet:**
```java
// Logic inside a starter (simplified)
@Configuration
@ConditionalOnClass(DataSource.class) // Only if DataSource interface exists
@ConditionalOnMissingBean(DataSource.class) // Only if user hasn't defined one
public class DataSourceConfig {
    // create default DataSource
}
```

---

## 76. What are the starter dependencies in Spring Boot?

**Answer:**
**Starters** are a set of convenient dependency descriptors that you can include in your application. They aggregate common related dependencies into a single artifact.
-   **Benefit:** You don't need to hunt for compatible versions of various libraries (e.g., Spring MVC, Jackson, Tomcat). The starter manages the versions (BOM).
-   **Examples:**
    -   `spring-boot-starter-web`: Includes Spring MVC, REST, Tomcat, Jackson.
    -   `spring-boot-starter-data-jpa`: Includes Spring Data JPA, Hibernate, JDBC.
    -   `spring-boot-starter-test`: Includes JUnit, Mockito, Spring Test.

**Code Snippet:**
```xml
<!-- Maven -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

---

## 77. What is `@SpringBootApplication` composed of?

**Answer:**
`@SpringBootApplication` is a meta-annotation that combines three other important annotations:
1.  **`@Configuration`:** Indicates the class is a source of bean definitions.
2.  **`@EnableAutoConfiguration`:** Enables Spring Boot's automatic configuration mechanism.
3.  **`@ComponentScan`:** Tells Spring to scan the current package (and sub-packages) for other components, configurations, and services.

**Code Snippet:**
```java
@SpringBootApplication
// Equivalent to:
// @Configuration
// @EnableAutoConfiguration
// @ComponentScan
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```

---

## 78. How does component scanning work in Spring Boot?

**Answer:**
Component scanning tells Spring where to look for annotated components (`@Component`, `@Service`, etc.) to register them as beans in the ApplicationContext.
-   **Default:** By default, `@SpringBootApplication` scans the **package where the main class is located** and all its **sub-packages**.
-   **Custom:** You can override this using `@ComponentScan(basePackages = "com.other.package")` if your beans are located outside the main package hierarchy.

**Code Snippet:**
```java
package com.example.app;

@SpringBootApplication // Scans com.example.app and sub-packages
public class App { }

// Safe: com.example.app.service.MyService (Scanned)
// Unsafe: com.example.other.OtherService (NOT Scanned by default)
```

---

## 79. How do profiles work in Spring Boot?

**Answer:**
**Profiles** provide a way to segregate parts of your application configuration and make it available only in certain environments (e.g., Dev, Test, Prod).
-   **Activation:** Using `spring.profiles.active=dev` property or VM argument `-Dspring.profiles.active=prod`.
-   **Properties:** `application-dev.properties` overrides `application.properties` when "dev" is active.
-   **Beans:** Use `@Profile("dev")` to load beans only in specific profiles.

**Code Snippet:**
```java
@Service
@Profile("dev")
public class DevDataSeeder { 
    // Only loaded in dev environment
}
```

---

## 80. What are beans in Spring? Lifecycle?

**Answer:**
A **Bean** is an object instantiated, assembled, and managed by the Spring IoC container.
**Lifecycle:**
1.  **Instantiation:** Spring creates the bean instance.
2.  **Populate Properties:** Dependencies are injected (DI).
3.  **Initialization:**
    -   `BeanNameAware` / `BeanFactoryAware` callbacks.
    -   `@PostConstruct` annotated methods.
    -   `InitializingBean.afterPropertiesSet()`.
    -   Custom `init-method`.
4.  **Use:** Application uses the bean.
5.  **Destruction:**
    -   `@PreDestroy` methods.
    -   `DisposableBean.destroy()`.
    -   Custom `destroy-method`.

**Code Snippet:**
```java
@Component
public class LifeCycleBean {
    @PostConstruct
    public void init() { System.out.println("Bean Initialized"); }

    @PreDestroy
    public void destroy() { System.out.println("Bean Destroyed"); }
}
```

---

## 81. Difference between ApplicationContext and BeanFactory.

**Answer:**
Both are IoC containers, but `ApplicationContext` is the advanced one.
-   **`BeanFactory`:**
    -   Basic container. Provides DI.
    -   **Lazy Loading:** Beans are instantiated only when requested (`getBean()`).
    -   Best for resource-constrained systems (mobile/embedded).
-   **`ApplicationContext`:**
    -   Extends `BeanFactory`.
    -   **Eager Loading:** Instantiates all Singleton beans at startup.
    -   **Features:** Adds AOP, Internationalization (i18n), Event Publishing, and Annotation support.
    -   Standard for most enterprise apps.

**Code Snippet:**
```java
// BeanFactory (Resource)
Resource res = new ClassPathResource("beans.xml");
BeanFactory factory = new XmlBeanFactory(res);

// ApplicationContext (Enterprise)
ApplicationContext context = new ClassPathXmlApplicationContext("beans.xml");
```

---

## 82. How to define a custom scope?

**Answer:**
Spring provides standard scopes (`singleton`, `prototype`, `request`, `session`). To create a custom scope (e.g., specific to a "Conversation" or "Batch Job"):
1.  Implement the `org.springframework.beans.factory.config.Scope` interface.
2.  Implement methods: `get()`, `remove()`, `registerDestructionCallback()`.
3.  Register the scope with `CustomScopeConfigurer` or programmatically via `ConfigurableBeanFactory`.

**Code Snippet:**
```java
public class MyThreadScope implements Scope {
    private final ThreadLocal<Map<String, Object>> threadScope = ...;

    @Override
    public Object get(String name, ObjectFactory<?> objectFactory) {
        // Logic to return object from ThreadLocal
    }
    // ... implement other methods
}

// Registration
@Bean
public CustomScopeConfigurer customScope() {
    CustomScopeConfigurer configurer = new CustomScopeConfigurer();
    configurer.addScope("thread", new MyThreadScope());
    return configurer;
}
```

---

## 83. What is AOP? Explain with use-case.

**Answer:**
**Aspect-Oriented Programming (AOP)** allows separating **Cross-Cutting Concerns** (code that affects multiple layers but isn't business logic) from the main business logic.
-   **Key Concepts:**
    -   **Aspect:** The module/class defining the cross-cutting logic (e.g., `LoggingAspect`).
    -   **Advice:** What action is taken (Before, After, Around).
    -   **Pointcut:** Where to apply the advice (expression matching methods).
-   **Use Cases:** Logging, Transaction Management, Security, Caching.

**Code Snippet:**
```java
@Aspect
@Component
public class LoggingAspect {
    
    // Run BEFORE any method in service package
    @Before("execution(* com.example.service.*.*(..))")
    public void logBefore(JoinPoint joinPoint) {
        System.out.println("Executing: " + joinPoint.getSignature().getName());
    }
}
```

---

## 84. Difference between cross-cutting concern and business logic?

**Answer:**
-   **Business Logic (Core Concern):** The primary functionality the application is built for.
    -   *Example:* Calculating taxes, transferring money, processing an order.
    -   Unique to specific modules.
-   **Cross-Cutting Concern:** Functionality that spans across multiple application layers and modules.
    -   *Example:* Logging every method call, checking security permissions, managing database transactions.
    -   Repetitive boilerplate if implemented in every method. AOP solves this.

**Code Snippet:**
```java
public void transferMoney() {
    // Cross-Cutting: log.info("Start");
    // Cross-Cutting: tx.begin();
    
    // BUSINESS LOGIC: from.debit(); to.credit();
    
    // Cross-Cutting: tx.commit();
}
```

---

## 85. How to implement custom annotations with AOP?

**Answer:**
Combining AOP with custom annotations provides a powerful way to apply logic selectively.
1.  **Create Annotation:** `@interface MyLog`.
2.  **Create Aspect:** Define a `@Around` advice.
3.  **Pointcut:** Target methods annotated with `@MyLog`.

**Code Snippet:**
```java
// 1. Annotation
@Retention(RetentionPolicy.RUNTIME)
public @interface TrackTime {}

// 2. Aspect
@Aspect
@Component
public class TimingAspect {
    @Around("@annotation(TrackTime)")
    public Object measure(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();
        Object proceed = joinPoint.proceed(); // Run actual method
        System.out.println("Time: " + (System.currentTimeMillis() - start));
        return proceed;
    }
}
```

---

## 86. What is the use of `transaction`?

**Answer:**
A **Transaction** is a unit of work that must either **fully complete** or **fully fail** (Atomic). In Spring, the `@Transactional` annotation manages this.
-   **Success:** If the method finishes without exception, the transaction is **Committed** (saving changes to DB).
-   **Failure:** If a RuntimeException occurs, the transaction is **Rolled Back** (undoing changes).
-   **ACID Properties:** Atomicity, Consistency, Isolation, Durability.

**Code Snippet:**
```java
@Service
public class OrderService {
    @Transactional
    public void placeOrder(Order order) {
        inventoryRepo.decreaseStock(order.getProduct());
        paymentService.charge(order.getUser());
        // If payment fails, stock decrease is ROLLED BACK automatically.
    }
}
```

---

## 87. What is the difference between programmatic and declarative transaction management?

**Answer:**
-   **Declarative (Recommended):**
    -   Separates transaction logic from business code.
    -   Uses **Annotations** (`@Transactional`) or XML.
    -   Powered by **AOP**. Simple to use and maintain.
-   **Programmatic:**
    -   Transaction code is mixed with business logic.
    -   Uses `TransactionTemplate` or `PlatformTransactionManager`.
    -   Gives fine-grained control (e.g., commit half the work even if the rest fails), but code is messy.

**Code Snippet:**
```java
// Declarative
@Transactional
public void save() { repo.save(); }

// Programmatic
public void save() {
    transactionTemplate.execute(status -> {
        repo.save();
        return null;
    });
}
```

---

## 88. Explain propagation types in transaction management.

**Answer:**
Propagation defines how transaction boundaries behave when one transactional method calls another. Common types:
1.  **REQUIRED (Default):** Joins existing transaction. If none exists, creates a new one.
2.  **REQUIRES_NEW:** Suspends current transaction and creates a fresh/independent one.
3.  **SUPPORTS:** Runs in transaction if exists; otherwise runs non-transactionally.
4.  **MANDATORY:** Throws exception if no active transaction exists.
5.  **NEVER:** Throws exception if active transaction exists.

**Code Snippet:**
```java
@Transactional(propagation = Propagation.REQUIRED)
public void methodA() {
    methodB(); // Joins methodA's transaction
}

@Transactional(propagation = Propagation.REQUIRES_NEW)
public void methodB() {
    // Runs in own transaction. If methodB fails, methodA is NOT implicitly rolled back (unless exception propagates)
}
```

---

## 89. How does Spring handle circular dependency?

**Answer:**
Circular Dependency happens when Bean A depends on Bean B, and Bean B depends on Bean A.
-   **Setter/Field Injection:** Spring **can resolve** this using its 3-level cache (singleton factories). It creates the "raw" Bean A, injects it into B, finishes creating B, and then injects complete B into A.
-   **Constructor Injection:** Spring **cannot resolve** this and throws `BeanCurrentlyInCreationException`.
-   **Fix:** Use `@Lazy` on one of the constructor parameters to delay initialization.

**Code Snippet:**
```java
@Service
public class A {
    private final B b;
    // @Lazy breaks the cycle
    public A(@Lazy B b) { this.b = b; }
}
```

---

## 90. What is the difference between `@Value`, `@ConfigurationProperties`, and `Environment`?

**Answer:**
All are used to read properties (e.g., from `application.properties`).
1.  **`@Value`:** Injects a **single** property value into a field. Good for simple, one-off values.
2.  **`@ConfigurationProperties`:** Binds a **group** of related properties to a Java POJO heavily. Type-safe, supports validation, lists, and maps. (Best for complex config).
3.  **`Environment`:** An abstraction to access properties programmatically via `env.getProperty("key")`.

**Code Snippet:**
```java
// 1. @Value
@Value("${app.name}")
private String appName;

// 2. @ConfigurationProperties (Refers to app.mail.*)
@Component
@ConfigurationProperties(prefix = "app.mail")
public class MailConfig {
    private String host;
    private int port;
    // getters/setters
}
```

---

## 91. Explain RestTemplate vs WebClient.

**Answer:**
-   **RestTemplate:**
    -   Traditional, **Blocking** (Synchronous) HTTP client.
    -   Uses one thread per request. If the external service is slow, the thread is blocked.
    -   In maintenance mode (deprecated features) as of Spring 5.
-   **WebClient:**
    -   Modern, **Non-Blocking** (Asynchronous) HTTP client introduced in Spring 5 (WebFlux).
    -   Built on Project Reactor.
    -   Uses few threads to handle concurrency (Event Loop).
    -   Supports both Synchronous (block()) and Asynchronous execution.

**Code Snippet:**
```java
// RestTemplate (Blocking)
String result = restTemplate.getForObject("http://example.com", String.class);

// WebClient (Non-Blocking)
Mono<String> resultMono = webClient.get()
    .uri("http://example.com")
    .retrieve()
    .bodyToMono(String.class);
    
resultMono.subscribe(res -> System.out.println(res)); // Async Callback
```

---

## 92. What is reactive programming in Spring?

**Answer:**
**Reactive Programming** is a paradigm focused on building **non-blocking**, **event-driven** applications that can handle a massive number of concurrent connections with a small number of threads.
-   **Core Principle:** Backpressure. The consumer controls the speed of data flow from the producer to avoid being overwhelmed.
-   **Stack:** Spring WebFlux (built on Project Reactor).
-   **Container:** Netty (Event Loop based) instead of Servlet containers (Thread-per-request).

**Code Snippet:**
```java
// Reactive Controller
@GetMapping("/stream")
public Flux<Integer> streamNumbers() {
    return Flux.interval(Duration.ofSeconds(1))
               .map(i -> i.intValue());
}
```

---

## 93. Difference between Mono and Flux?

**Answer:**
Both are implementations of the generic `Publisher<T>` interface in Project Reactor.
-   **`Mono<T>`:** Represents a stream of **0 or 1** element.
    -   *Use Case:* Retrieving a single user by ID, HTTP Call returning one object.
-   **`Flux<T>`:** Represents a stream of **0 to N** elements.
    -   *Use Case:* Retrieving a list of users, infinite event stream.

**Code Snippet:**
```java
// Mono: Completes successfully with one item or empty
Mono<String> mono = Mono.just("Hello");

// Flux: Emits multiple items
Flux<String> flux = Flux.just("A", "B", "C");
```

---

## 94. What is Spring WebFlux?

**Answer:**
**Spring WebFlux** is the reactive-stack web framework added in Spring 5.0. It is fully non-blocking, supports Reactive Streams back pressure, and runs on servers like Netty, Undertow, and Servlet 3.1+ containers.
-   **Programming Models:**
    1.  **Annotated Controllers:** Similar to Spring MVC (`@RestController`, `@GetMapping`).
    2.  **Functional Endpoints:** Lambda-based routing usage `RouterFunction` and `HandlerFunction`.

**Code Snippet:**
```java
// Functional Endpoint Style
@Bean
public RouterFunction<ServerResponse> route(UserHandler handler) {
    return RouterFunctions
        .route(GET("/users/{id}"), handler::getUser)
        .andRoute(GET("/users"), handler::getAllUsers);
}
```

---

## 95. How to secure a REST API using Spring Security?

**Answer:**
Spring Security secures APIs via a chain of filters. To secure a REST API:
1.  Add `spring-boot-starter-security`.
2.  create a configuration class extending `WebSecurityConfigurerAdapter` (Deprecated) or defining a `SecurityFilterChain` bean (Modern).
3.  Configure authentication (UserDetailsService) and authorization (URL patterns).

**Code Snippet:**
```java
@Bean
public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
    http
        .csrf().disable() // Disable CSRF for stateless REST APIs
        .authorizeHttpRequests()
        .requestMatchers("/public/**").permitAll()
        .anyRequest().authenticated()
        .and()
        .httpBasic(); // Use Basic Auth
    return http.build();
}
```

---

## 96. Difference between permitAll() and authenticated()?

**Answer:**
These methods define access rules in `HttpSecurity` configuration.
-   **`permitAll()`:** The URL pattern is accessible to **everyone**, including anonymous (unlogged) users. No authentication required.
-   **`authenticated()`:** The URL pattern is accessible **only** to users who have successfully authenticated (logged in).

**Code Snippet:**
```java
http.authorizeHttpRequests()
    .requestMatchers("/login", "/register").permitAll() // Open to all
    .requestMatchers("/admin/**").authenticated();      // Must be logged in
```

---

## 97. What is CSRF and how to handle it in Spring?

**Answer:**
**CSRF (Cross-Site Request Forgery)** is an attack where a malicious site tricks a user into executing unwanted actions on a web application where they are currently authenticated (using session cookies).
-   **Spring Handling:** Spring Security enables CSRF protection by default. It expects a **CSRF Token** in POST/PUT/DELETE requests.
-   **REST APIs:** Since REST APIs are typically **stateless** (using JWT instead of Session Cookies), CSRF protection is usually **disabled** because the browser doesn't automatically send the token like it does with cookies.

**Code Snippet:**
```java
// For Stateless REST APIs
http.csrf().disable();
```

---

## 98. What is AuthenticationManager?

**Answer:**
`AuthenticationManager` is the main interface for authentication in Spring Security.
-   **Method:** `authenticate(Authentication authentication)`.
-   **Role:** It delegates the validation of credentials to one or more `AuthenticationProvider`s (e.g., specific logic for DAO/DB, LDAP, OAuth).
-   **Result:** If successful, returns a fully populated `Authentication` object (with authorities/roles); otherwise throws specific exceptions like `BadCredentialsException`.

**Code Snippet:**
```java
// Usage in a Login Controller
Authentication authentication = authenticationManager.authenticate(
    new UsernamePasswordAuthenticationToken(username, password)
);
SecurityContextHolder.getContext().setAuthentication(authentication);
```

---

## 99. How to implement custom authentication in Spring Security?

**Answer:**
To implement custom logic (e.g., verifying a custom token or header):
1.  Create a **Custom Filter** (extends `OncePerRequestFilter`) to extract credentials.
2.  Create a **Custom AuthenticationProvider** to validate credentials.
3.  Register the filter in the `SecurityFilterChain`.

**Code Snippet:**
```java
// Custom Provider
@Component
public class ApiKeyProvider implements AuthenticationProvider {
    @Override
    public Authentication authenticate(Authentication auth) {
        String key = (String) auth.getPrincipal();
        if ("secret-key".equals(key)) {
            return new ApiKeyAuthenticationToken(key, Collections.emptyList());
        }
        throw new BadCredentialsException("Invalid Key");
    }
    // ... supports() implementation
}
```

---

## 100. Let's compare Filters and Interceptors.

**Answer:**
Both intercept requests, but operate at different levels.
-   **Filters (`javax.servlet.Filter`):**
    -   Part of **Servlet Standard**.
    -   Run **before** the request reaches the DispatcherServlet.
    -   Scope: Processing raw requests/responses (compression, raw security, logging).
    -   Not Spring Beans by default (unless registered).
-   **Interceptors (`HandlerInterceptor`):**
    -   Part of **Spring MVC**.
    -   Run **after** DispatcherServlet but **before** the Controller.
    -   Scope: Application-specific logic (checking user context, adding model attributes).
    -   Are Spring Beans (can inject Service/DAO).

**Code Snippet:**
```java
// Filter: Raw Request
public void doFilter(...) {
    System.out.println("Filter: Raw Check");
    chain.doFilter(req, res);
}

// Interceptor: Handler Context
public boolean preHandle(...) {
    System.out.println("Interceptor: Controller Check");
    return true;
}
```

---

## 101. What is the difference between `Filter` and `HandlerInterceptor`?

**Answer:**
While both intercept requests, they differ in scope and capabilities:
| Feature | Filter (`javax.servlet.Filter`) | HandlerInterceptor (`org.springframework.web.servlet.HandlerInterceptor`) |
| :--- | :--- | :--- |
| **Origin** | Servlet Specification (Standard Java EE). | Spring MVC Framework. |
| **Execution** | Runs **before** the request reaches the `DispatcherServlet`. | Runs **after** `DispatcherServlet` determines the handler, but **before** the Controller. |
| **Scope** | Global (Web Layer). Can modify raw request/response (byte streams). | specific to Spring MVC Handlers. Can access Handler/Controller object. |
| **Bean Access** | Not Spring Beans by default (harder to inject services). | Full Spring Bean support (easy to inject `@Service`). |
| **Use Case** | Security, Compression, CORS, Logging. | Authorization checks, Locale change, Theme change. |

**Code Snippet:**
```java
// Filter configuration
@Bean
public FilterRegistrationBean<MyFilter> loggingFilter() {
    FilterRegistrationBean<MyFilter> reg = new FilterRegistrationBean<>();
    reg.setFilter(new MyFilter());
    reg.addUrlPatterns("/api/*");
    return reg;
}

// Interceptor configuration
@Override
public void addInterceptors(InterceptorRegistry registry) {
    registry.addInterceptor(new MyInterceptor()).addPathPatterns("/api/**");
}
```

---

## 102. How does Spring handle exceptions?

**Answer:**
Spring provides multiple ways to handle exceptions globally or locally:
1.  **`@ExceptionHandler`:** Handles exceptions for a specific Controller.
2.  **`@ControllerAdvice` / `@RestControllerAdvice`:** Global exception handling for all Controllers.
3.  **`ResponseStatusException`:** Programmatic way to throw exceptions with specific HTTP status codes.
4.  **`HandlerExceptionResolver`:** Low-level interface for custom resolution.

**Code Snippet:**
```java
// Recommended: Global Exception Handler
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    @ResponseStatus(HttpStatus.NOT_FOUND)
    public ErrorResponse handleUserNotFound(UserNotFoundException ex) {
        return new ErrorResponse("USER_NOT_FOUND", ex.getMessage());
    }
}
```

---

## 103. What is the difference between `@ControllerAdvice` and `@ExceptionHandler`?

**Answer:**
-   **`@ExceptionHandler`:**
    -   Defines the logic to handle a specific exception type.
    -   Scope: Default is **Local** (only within the Controller where it is defined).
-   **`@ControllerAdvice`:**
    -   A specialization of `@Component`.
    -   It allows applying `@ExceptionHandler`, `@InitBinder`, and `@ModelAttribute` methods **globally** to all Controllers in the application.
    -   Think of it as an "Aspect" for Controllers.

**Code Snippet:**
```java
@Controller
public class MyController {
    // Local: Only handles exceptions from MyController
    @ExceptionHandler(NullPointerException.class)
    public void handle() { ... }
}

@ControllerAdvice
public class GlobalHandler {
    // Global: Handles exceptions from ANY controller
    @ExceptionHandler(Exception.class)
    public void handleGlobal() { ... }
}
```

---

## 104. How to return consistent error responses in Spring REST?

**Answer:**
To ensure clients always receive a predictable error structure (JSON):
1.  Define a standard POJO class (e.g., `ApiError` with fields: `timestamp`, `status`, `error`, `path`).
2.  Create a `@RestControllerAdvice` class.
3.  Implement `@ExceptionHandler` methods that catch various exceptions (custom and standard Spring exceptions like `MethodArgumentNotValidException`).
4.  Return `ResponseEntity<ApiError>` from these methods.

**Code Snippet:**
```java
public class ApiError {
    private LocalDateTime timestamp;
    private int status;
    private String message;
    // Constructor/Getters
}

@RestControllerAdvice
public class RestExceptionHandler {
    @ExceptionHandler(Exception.class)
    public ResponseEntity<ApiError> handleAll(Exception ex) {
        ApiError error = new ApiError(LocalDateTime.now(), 500, ex.getMessage());
        return new ResponseEntity<>(error, HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

---

## 105. How to create custom validators in Spring Boot?

**Answer:**
To create a custom validation annotation (e.g., checking if a password is strong):
1.  Create the **Annotation** (e.g., `@StrongPassword`) annotated with `@Constraint`.
2.  Create the **Validator Class** implementing `ConstraintValidator<Annotation, Type>`.
3.  Implement the `isValid` logic.

**Code Snippet:**
```java
// 1. Annotation
@Target({ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
@Constraint(validatedBy = PasswordValidator.class)
public @interface StrongPassword {
    String message() default "Password too weak";
    Class<?>[] groups() default {};
    Class<? extends Payload>[] payload() default {};
}

// 2. Logic
public class PasswordValidator implements ConstraintValidator<StrongPassword, String> {
    @Override
    public boolean isValid(String password, ConstraintValidatorContext context) {
        return password != null && password.length() > 8 && password.matches(".*[A-Z].*");
    }
}
```

---

## 106. Difference between validation groups and constraints?

**Answer:**
-   **Constraints:** The actual rules applied to fields (e.g., `@NotNull`, `@Size`, `@Email`). They define *what* is valid.
-   **Validation Groups:** A way to apply a **subset** of constraints depending on the operation.
    -   *Example:* When **Creating** a user, `id` should be Null. When **Updating** a user, `id` should be NotNull. You can define `CreateGroup` and `UpdateGroup` interfaces to separate these rules on the same DTO.

**Code Snippet:**
```java
public class UserDTO {
    @Null(groups = Create.class)
    @NotNull(groups = Update.class)
    private Long id;

    @NotBlank(groups = {Create.class, Update.class})
    private String name;
}

// Usage in Controller
@PostMapping
public void create(@Validated(Create.class) @RequestBody UserDTO user) { ... }
```

---

## 107. What is the use of @Valid and @Validated?

**Answer:**
-   **`@Valid` (`javax.validation` / `jakarta.validation`):**
    -   Standard Java Bean Validation annotation.
    -   Triggers validation on the annotated object.
    -   Does **not** support Validation Groups.
-   **`@Validated` (`org.springframework.validation`):**
    -   Spring's specific variant.
    -   Supports **Validation Groups** (e.g., `@Validated(OnCreate.class)`).
    -   Can be used on *class level* to enable validation for method parameters (e.g., `@RequestParam @Min(5) int id`).

**Code Snippet:**
```java
// Standard Validation
public void register(@Valid @RequestBody UserDto user) { ... }

// Group Validation (Spring specific)
public void update(@Validated(OnUpdate.class) @RequestBody UserDto user) { ... }
```

---

## 108. How to use Swagger/OpenAPI in Spring Boot?

**Answer:**
Swagger (now OpenAPI) documents REST APIs automatically.
-   **Setup:** Add `springdoc-openapi-starter-webmvc-ui` dependency (for Spring Boot 3+).
-   **Access:** The UI is typically available at `/swagger-ui/index.html`.
-   **Customization:** Use annotations like `@Operation`, `@ApiResponse`, and `@Schema` to enrich the documentation.

**Code Snippet:**
```java
@RestController
public class UserController {

    @Operation(summary = "Get user by ID", description = "Returns a single user")
    @ApiResponses(value = {
        @ApiResponse(responseCode = "200", description = "Found the user"),
        @ApiResponse(responseCode = "404", description = "User not found")
    })
    @GetMapping("/users/{id}")
    public User getUser(@PathVariable Long id) { ... }
}
```

---

## 109. Difference between @PathVariable and @RequestParam.

**Answer:**
-   **`@PathVariable`:** Use when the value is part of the **URI path** (RESTful resource identification).
    -   *Example:* `/users/101` -> ID is 101.
    -   Mandatory by default.
-   **`@RequestParam`:** Use when the value is a **query parameter** (filtering, sorting, optional data).
    -   *Example:* `/users?role=ADMIN&page=1` -> role is ADMIN.
    -   Optional by default (or can set `required=false`).

**Code Snippet:**
```java
// PathVariable: /books/123
@GetMapping("/books/{id}")
public Book getBook(@PathVariable String id) { ... }

// RequestParam: /books?author=Rowling
@GetMapping("/books")
public List<Book> searchBooks(@RequestParam(defaultValue = "All") String author) { ... }
```

---

## 110. What is HATEOAS?

**Answer:**
**HATEOAS** (Hypermedia as the Engine of Application State) is a constraint of the REST application architecture.
-   **Concept:** The API response should include not just data, but also **links** (Hypermedia) to related actions/resources, guiding the client on what they can do next.
-   **Spring Support:** `Spring HATEOAS` library provides `RepresentationModel` and `WebMvcLinkBuilder` to easily add these links.

**Code Snippet:**
```json
// Response without HATEOAS
{ "id": 1, "name": "Alice" }

// Response WITH HATEOAS
{
  "id": 1, 
  "name": "Alice",
  "_links": {
    "self": { "href": "http://api.com/users/1" },
    "orders": { "href": "http://api.com/users/1/orders" }
  }
}
```

---

## 111. How does `@Async` work in Spring Boot?

**Answer:**
`@Async` allows a method to be executed in a separate thread.
-   **Mechanism:** When you call an `@Async` method, Spring intercepts the call and submits the task to a **TaskExecutor** (Thread Pool). The caller returns immediately (or receives a `Future`/`CompletableFuture`).
-   **Requirements:**
    1.  Add `@EnableAsync` to a configuration class.
    2.  The method must be `public`.
    3.  Calling the method from *within* the same class won't work (self-invocation bypasses the proxy).

**Code Snippet:**
```java
@Service
public class EmailService {
    @Async
    public void sendEmail() {
        // Runs in a separate thread
        System.out.println("Sending email via " + Thread.currentThread().getName());
    }
}
```

---

## 112. What is Spring Scheduler? Cron jobs?

**Answer:**
Spring Scheduler allows executing tasks at specific intervals.
-   **Setup:** Add `@EnableScheduling`.
-   **Annotations:** Use `@Scheduled` on methods.
-   **Options:**
    -   `fixedRate`: Runs every X ms (start-to-start).
    -   `fixedDelay`: Runs X ms *after* the previous execution finishes.
    -   `cron`: Uses Unix-like cron expressions (Seconds Minutes Hours Day Month Weekday).

**Code Snippet:**
```java
@Component
public class ReportJob {
    // Runs at 10:15 AM every day
    @Scheduled(cron = "0 15 10 * * *")
    public void generateReport() {
        System.out.println("Generating Report...");
    }
}
```

---

## 113. How to publish and listen to events in Spring?

**Answer:**
Spring's Event Mechanism helps decouple components.
1.  **Define Event:** Create a class (can be any POJO or extend `ApplicationEvent`).
2.  **Publish:** Inject `ApplicationEventPublisher` and call `publishEvent()`.
3.  **Listen:** Use `@EventListener` on a method in a managed bean.

**Code Snippet:**
```java
// 1. Event
record UserCreatedEvent(String username) {}

// 2. Publisher
@Service
public class UserService {
    @Autowired ApplicationEventPublisher publisher;
    public void register() {
        publisher.publishEvent(new UserCreatedEvent("Alice"));
    }
}

// 3. Listener
@Component
public class NotificationService {
    @EventListener
    public void handle(UserCreatedEvent event) {
        System.out.println("Welcome " + event.username());
    }
}
```

---

## 114. Check difference between synchronous and asynchronous event publishing.

**Answer:**
-   **Synchronous (Default):** The listener executes in the **same thread** as the publisher. The publisher blocked until the listener finishes.
    -   *Use Case:* Transactional logic where listener failure should rollback the publisher's transaction.
-   **Asynchronous:** The listener executes in a **separate thread**.
    -   *Use Case:* Sending emails, analytics, logging (fire and forget).
    -   *Implementation:* Annotate the listener method with `@Async`.

**Code Snippet:**
```java
@EventListener
@Async // Runs in a new thread
public void handleAsync(UserCreatedEvent event) {
    longTask();
}
```

---

## 115. How does caching work in Spring Boot?

**Answer:**
Spring Cache Abstraction applies caching to Java methods, reducing the number of executions based on the information in the cache.
-   **Setup:** `@EnableCaching`.
-   **Annotations:**
    -   `@Cacheable("users")`: Checks cache. If found, returns value. If not, executes method and caches result.
    -   `@CachePut("users")`: Updates the cache with the method result.
    -   `@CacheEvict("users")`: Removes entries from cache.

**Code Snippet:**
```java
@Service
public class ProductService {
    
    @Cacheable(value = "products", key = "#id")
    public Product getProduct(Long id) {
        // Only executed if ID not in cache
        return db.findById(id); 
    }
    
    @CacheEvict(value = "products", key = "#id")
    public void updateProduct(Long id) {
        // Clears cache for this ID
    }
}
```

---

## 116. How to use Redis for caching?

**Answer:**
Redis is a popular distributed in-memory data store.
1.  **Dependency:** Add `spring-boot-starter-data-redis`.
2.  **Config:** Configure `spring.data.redis.host/port` in properties.
3.  **Auto-Config:** Spring Boot detects Redis and configures `RedisCacheManager` as the generic Cache Manager.
4.  **Usage:** Use standard annotations (`@Cacheable`). Data is serialized (usually JSON or Byte array) and stored in Redis.

**Code Snippet:**
```properties
# application.properties
spring.data.redis.host=localhost
spring.data.redis.port=6379
spring.cache.type=redis
```

---

## 117. How to monitor Spring Boot applications?

**Answer:**
Monitoring is achieved using **Spring Boot Actuator**.
-   It adds production-ready features to the application.
-   Exposes operational information via HTTP endpoints (or JMX).
-   integrates with monitoring tools like Prometheus, Grafana, Datadog.

**Code Snippet:**
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

---

## 118. What are Spring Boot Actuators?

**Answer:**
Actuators are endpoints that let you monitor and interact with your application. Common endpoints:
-   `/actuator/health`: Application health status (UP, DOWN).
-   `/actuator/info`: Arbitrary application info.
-   `/actuator/metrics`: Different keys (memory, cpu, database pool).
-   `/actuator/loggers`: View and modify logging levels at runtime.
-   `/actuator/env`: Environment properties.
(Note: Most are disabled by default for security; enable via `management.endpoints.web.exposure.include=*`).

**Code Snippet:**
```json
// GET /actuator/health
{
    "status": "UP"
}
```

---

## 119. How to expose custom metrics?

**Answer:**
Spring Boot uses **Micrometer** as a facade for metrics. To generic custom metrics:
1.  Inject `MeterRegistry`.
2.  Register metrics like:
    -   **Counter:** Monotonically increasing value (e.g., Request Count).
    -   **Gauge:** Instantaneous value (e.g., Queue Size).
    -   **Timer:** Duration of events.

**Code Snippet:**
```java
@Service
public class OrderService {
    private final Counter orderCounter;

    public OrderService(MeterRegistry registry) {
        this.orderCounter = registry.counter("orders.placed");
    }

    public void placeOrder() {
        orderCounter.increment(); // Exported to Prometheus/Graphite
    }
}
```

---

## 120. How to configure a Datasource manually?

**Answer:**
Instead of relying on auto-configuration (which reads `spring.datasource.*`), you can define a `DataSource` bean manually. This is useful for multiple datasources.
1.  Create `@Configuration` class.
2.  Use `DataSourceBuilder`.
3.  Load properties using `@ConfigurationProperties`.

**Code Snippet:**
```java
@Configuration
public class DbConfig {
    
    @Bean
    @ConfigurationProperties(prefix = "app.datasource")
    public DataSource myDataSource() {
        return DataSourceBuilder.create().build();
    }
}
/* Properties:
app.datasource.url=jdbc:mysql://...
app.datasource.username=root
*/
```

---

## 121. What is Spring Data JPA?

**Answer:**
Spring Data JPA is part of the Spring Data project that makes it easy to implement JPA-based repositories.
-   **Abstraction:** It adds an extra layer of abstraction on top of the JPA Provider (like Hibernate).
-   **Goal:** To reduce the boilerplate code required to implement a Data Access Layer (DAO). You typically just definitions an interface extending `JpaRepository`, and Spring provides the implementation at runtime.

**Code Snippet:**
```java
// No implementation class needed!
public interface UserRepository extends JpaRepository<User, Long> {
    // Spring generates the implementation details automatically.
}
```

---

## 122. What are derived query methods?

**Answer:**
Derived query methods allow you to define queries just by **naming the method** correctly in the repository interface. Spring Data parses the method name and creates the query for you.
-   **Keywords:** `findBy`, `countBy`, `deleteBy`.
-   **Conditions:** `And`, `Or`, `Between`, `LessThan`, `GreaterThan`, `Like`, `OrderBy`.

**Code Snippet:**
```java
public interface UserRepository extends JpaRepository<User, Long> {
    // Generates: SELECT * FROM user WHERE email = ? AND active = true
    List<User> findByEmailAndActiveTrue(String email);

    // Generates: SELECT * FROM user WHERE age > ? ORDER BY name DESC
    List<User> findByAgeGreaterThanOrderByNameDesc(int age);
}
```

---

## 123. Difference between CrudRepository, PagingAndSortingRepository, and JpaRepository.

**Answer:**
These are the core repository interfaces in a hierarchy:
1.  **`CrudRepository`:** Basic CRUD operations (`save`, `findById`, `delete`, `count`).
2.  **`PagingAndSortingRepository`:** Extends `CrudRepository`. Adds methods for Pagination and Sorting (`findAll(Pageable)`, `findAll(Sort)`).
3.  **`JpaRepository`:** Extends `PagingAndSortingRepository`. Adds JPA-specific methods handling persistence context (`flush`, `saveAndFlush`, `deleteInBatch`).

**Code Snippet:**
```java
// Hierarchy Visualization
// Repository -> CrudRepository -> PagingAndSortingRepository -> JpaRepository
```

---

## 124. How to handle pagination in Spring Data?

**Answer:**
Pagination is handled by passing a `Pageable` object to repository methods.
-   **Input:** `PageRequest.of(pageNumber, pageSize, Sort)`.
-   **Output:** Returns a `Page<T>` (contains list of items + total pages/elements info) or `Slice<T>` (contains list + "has next" flag, cheaper query).

**Code Snippet:**
```java
// Service
public Page<User> getUsers(int page, int size) {
    Pageable pageable = PageRequest.of(page, size, Sort.by("name"));
    return userRepository.findAll(pageable);
}

// Result (Page)
// { "content": [...], "totalPages": 10, "totalElements": 100, ... }
```

---

## 125. What is Query By Example (QBE)?

**Answer:**
QBE is a dynamic querying technique. Instead of writing specific queries, you create an instance of the entity (`Probe`), set the fields you want to filter by, and query the repository using that instance.
-   **Pros:** Dynamic filters, no SQL writing.
-   **Cons:** Limited (doesn't support nested associations or complex OR/AND grouping easily).

**Code Snippet:**
```java
User probe = new User();
probe.setRole("ADMIN");
probe.setActive(true);
// Ignored: null fields (like ID or Name)

Example<User> example = Example.of(probe);
List<User> admins = userRepository.findAll(example);
```

---

## 126. How to write native queries in JPA?

**Answer:**
Sometimes JPQL (Java Persistence Query Language) isn't enough, and you need database-specific SQL features.
-   **Usage:** Use `@Query` annotation with `nativeQuery = true`.
-   **Projection:** You can map results to an Interface (Projections) or `Object[]` if it doesn't match an Entity exactly.

**Code Snippet:**
```java
@Query(
    value = "SELECT * FROM users u WHERE u.email LIKE %:domain", 
    nativeQuery = true
)
List<User> findUsersByDomain(@Param("domain") String domain);
```

---

## 127. Difference between EntityManager and JdbcTemplate.

**Answer:**
-   **`JdbcTemplate`:**
    -   Low-level SQL abstraction.
    -   Works with **Raw SQL**.
    -   No "Persistence Context" or caching. You manually map rows to objects.
    -   Best for: Batch updates, stored procedures, complex generic reports.
-   **`EntityManager`:**
    -   JPA Standard abstraction (Hibernate).
    -   Works with **Entities** and **JPQL**.
    -   Has **Persistence Context** (First-level cache, Dirty Checking, Lazy Loading).
    -   Best for: CRUD, navigating object graphs (OOP style).

**Code Snippet:**
```java
// JdbcTemplate
jdbcTemplate.query("SELECT * FROM users", new BeanPropertyRowMapper<>(User.class));

// EntityManager
entityManager.createQuery("SELECT u FROM User u", User.class).getResultList();
```

---

## 128. What is `@EntityGraph`?

**Answer:**
`@EntityGraph` is used to solve the **N+1 Select Problem**. It allows you to define which related associations (joins) should be loaded eagerly in a specific query, overriding the default `Lazy` fetch capability.
-   **FETCH graph:** Attributes specified are EAGER, others are LAZY.
-   **LOAD graph:** Attributes specified are EAGER, others keep their default strategy.

**Code Snippet:**
```java
// User has @OneToMany List<Order> orders (Lazy by default)

@EntityGraph(attributePaths = {"orders"})
@Query("SELECT u FROM User u")
List<User> findAllWithOrders();
// Result: Single JOIN query executed.
```

---

## 129. What is lazy vs eager loading?

**Answer:**
These define *when* related data behaves.
-   **Eager Loading (`FetchType.EAGER`):** Related entities are loaded immediately along with the parent. (e.g., Load User -> Join and load Address too).
-   **Lazy Loading (`FetchType.LAZY`):** Related entities are loaded **on-demand** when you access the getter (`user.getOrders()`). If the session is closed, this throws `LazyInitializationException`.
-   **Defaults:** `@OneToOne`/`@ManyToOne` are EAGER. `@OneToMany`/`@ManyToMany` are LAZY.

**Code Snippet:**
```java
@Entity
public class User {
    @OneToMany(fetch = FetchType.LAZY) // Default
    private List<Order> orders;
}
```

---

## 130. How does dirty checking work in JPA?

**Answer:**
**Dirty Checking** is the mechanism where Hibernate automatically detects changes made to an entity and updates the database.
1.  **Load:** Entity is loaded into the **Persistence Context** (Memory). Hibernate keeps a snapshot of the initial state.
2.  **Modify:** You modify properties of the object (e.g., `user.setName("New Name")`).
3.  **Flush/Commit:** When the transaction commits, Hibernate compares the current object with the initial snapshot.
4.  **Update:** If differences are found, it **automatically** initiates an `UPDATE` SQL statement. No explicit `save()` call is needed.

**Code Snippet:**
```java
@Transactional
public void updateName(Long id, String newName) {
    User user = userRepository.findById(id).orElseThrow();
    user.setName(newName);
    // user.save() is NOT required!
    // Transaction commit triggers update.
}
```

---

## 131. What is the N+1 select problem? Solution?

**Answer:**
The **N+1 Select Problem** occurs when you fetch a list of **N** entities (1 Query) and then iterate over them to access a lazily-loaded related entity, triggering **N** additional queries.
-   **Example:** Fetch 100 Users (1 query). Loop through them and call `user.getAddress()`. If Address is Lazy, Hibernate fires 100 queries to get addresses. Total = 101 queries.
-   **Solution:** Use **Join Fetch** in JPQL or `@EntityGraph` to fetch the association in the *initial* query.

**Code Snippet:**
```java
// Problematic (Lazy default)
List<User> users = repo.findAll();

// Solution (JPQL Join Fetch)
@Query("SELECT u FROM User u JOIN FETCH u.address")
List<User> findAllWithAddress();
// Result: 1 Query (Inner Join)
```

---

## 132. Difference between optimistic and pessimistic locking.

**Answer:**
-   **Optimistic Locking:**
    -   Assumes conflicts are effortless.
    -   Uses a `@Version` column (e.g., timestamp or integer).
    -   On update, checks if the version in DB matches the version in memory. If not, throws `OptimisticLockException`.
    -   Better performance (No DB locks).
-   **Pessimistic Locking:**
    -   Assumes conflicts are frequent.
    -   Locks the database row (`SELECT ... FOR UPDATE`) when reading.
    -   Other transactions block until the lock is released.
    -   Guarantees integrity but reduces concurrency significantly.

**Code Snippet:**
```java
// Optimistic
@Entity
public class Product {
    @Version
    private int version;
}

// Pessimistic (Repository)
@Lock(LockModeType.PESSIMISTIC_WRITE)
@Query("SELECT p FROM Product p WHERE p.id = :id")
Optional<Product> findByIdLocked(Long id);
```

---

## 133. What is `@DynamicUpdate` in Hibernate?

**Answer:**
By default, Hibernate updates **all columns** of an entity in the `UPDATE` statement, even if only one field changed.
-   **`@DynamicUpdate`:** Tells Hibernate to generate the SQL statement at runtime, including **only the columns that actually changed**.
-   **Pros:** Prevents overwriting concurrent changes to *different* columns (sometimes), reduces DB I/O for large tables with many columns.
-   **Cons:** Performance hit because it cannot use cached PreparedStatement (SQL changes every time).

**Code Snippet:**
```java
@Entity
@DynamicUpdate
public class User {
    // ...
}
```

---

## 134. How does `@Inheritance` work in JPA?

**Answer:**
JPA supports mapping object inheritance to database tables using 3 strategies:
1.  **SINGLE_TABLE (Default):** One table for the entire hierarchy. Uses a "Discriminator Column" (e.g., `dtype`) to distinguish types. Fast, but columns from subclasses must be nullable.
2.  **JOINED:** Base class has a table; subclasses have their own tables with only their specific fields (linked by FK). Normalized, but slow (Joins).
3.  **TABLE_PER_CLASS:** Each concrete class has its own table containing all columns (base + specific). No polymorphism (Union queries needed).

**Code Snippet:**
```java
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "payment_type")
public abstract class Payment { ... }

@Entity
@DiscriminatorValue("CC")
public class CreditCardPayment extends Payment { ... }
```

---

## 135. What is a DTO? Why is it used?

**Answer:**
**DTO (Data Transfer Object)** is a plain Java object used to carry data between processes or layers (e.g., Controller to Service).
-   **Security:** Hides sensitive internal structure (e.g., don't expose `User.password` or `User.version` to API).
-   **Decoupling:** Enables changing the Database Entity without breaking the API Contract.
-   **Performance:** Can aggregate data from multiple entities into one response object to reduce network calls.
-   **Serialization:** Prevents infinite recursion issues with bidirectional Entity relationships (User <-> Order).

**Code Snippet:**
```java
// Entity
class User { String username; String password; }

// DTO
class UserDTO { String username; } // Password excluded
```

---

## 136. How to map DTO to Entity and vice versa?

**Answer:**
1.  **Manual Mapping:** tedious setter/getter code. Best for simple/small projects. Control is 100%.
2.  **BeanUtils:** (`Spring BeanUtils`) Reflection-based copy. Slow and brittle (refactoring breaks it).
3.  **ModelMapper:** Runtime reflection mapping library. Easy setup, performance cost.
4.  **MapStruct:** (Industry Standard) **Compile-time** code generation. Generates type-safe, performant mapper implementation classes.

**Code Snippet:**
```java
// MapStruct Interface
@Mapper
public interface UserMapper {
    UserMapper INSTANCE = Mappers.getMapper(UserMapper.class);
    
    @Mapping(target = "email", source = "contactEmail")
    UserDTO userToDto(User user);
}
```

---

## 137. What is ModelMapper?

**Answer:**
**ModelMapper** is a library that intelligently maps objects to each other (e.g., Entity -> DTO).
-   It uses reflection to match fields by name automatically.
-   **Pros:** Very little boilerplate code.
-   **Cons:** Runtime overhead (Reflection), harder to debug if mapping is wrong.
-   *Note:* It is less preferred now compared to MapStruct (which is compile-time).

**Code Snippet:**
```java
ModelMapper modelMapper = new ModelMapper();
UserDTO dto = modelMapper.map(userEntity, UserDTO.class);
```

---

## 138. What are common performance pitfalls in Spring Boot applications?

**Answer:**
1.  **N+1 Select Problem:** Fetching too much data in loops.
2.  **Eager Loading:** Loading entire object graphs unnecessary.
3.  **Missing Indexes:** Database queries running slow table scans.
4.  **Improper Pool Sizing:** DB Connection pool (HikariCP) is too small/large.
5.  **Lack of Caching:** Re-computing expensive logic.
6.  **Excessive Logging:** Generating huge Strings in debug logs in production.

**Code Snippet:**
```java
// Bad: String concatenation happens even if DEBUG is disabled
log.debug("User " + user.toString() + " processed.");

// Good: SLF4J Parameterized logging (No cost if disabled)
log.debug("User {} processed.", user);
```

---

## 139. How to use Spring Boot with Docker?

**Answer:**
Containerizing a Spring Boot app makes it portable.
1.  **Dockerfile:** Standard way. Use a multi-stage build to keep image Size small (Use JRE, not JDK for runtime).
2.  **Cloud Native Buildpacks (CNB):** Built-in Maven command (`mvn spring-boot:build-image`). No Dockerfile needed. It detects Java and builds an optimized image automatically.
3.  **Jib:** Google's Maven plugin to build images without Docker daemon.

**Code Snippet:**
```dockerfile
# Simple Dockerfile
FROM eclipse-temurin:17-jre
COPY target/app.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]
```

---

## 140. How to externalize configurations in Spring Boot?

**Answer:**
Spring Boot allows separating config from code (12-Factor App rule).
**Priority Order (Low to High):**
1.  `application.properties` (Packaged inside Jar).
2.  `application-profile.properties` (Packaged).
3.  OS Environment Variables (`SPRING_DATASOURCE_PASSWORD`).
4.  Command Line Arguments (`--server.port=9090`).
5.  **Spring Cloud Config Server:** Centralized git-based config management.

**Code Snippet:**
```bash
# Override port without touching code
java -jar app.jar --server.port=8081
```

---

## 141. What is Spring Config Server?

**Answer:**
**Spring Cloud Config** provides server-side and client-side support for externalized configuration in a distributed system.
-   **Centralized:** It stores configurations for all microservices in a central location (Git, SVN, Vault, or File System).
-   **Dynamic Refresh:** Allows changing configuration at runtime without restarting the services (using `/actuator/refresh` or Spring Cloud Bus).
-   **Versioning:** Leveraging Git provides history and versioning of configuration files.

**Code Snippet:**
```yaml
# bootstrap.yml (Client Side)
spring:
  application:
    name: order-service
  cloud:
    config:
      uri: http://config-server:8888
```

---

## 142. Difference between Spring Cloud Config and application.yml?

**Answer:**
-   **`application.yml` (Local):** Packaged *inside* the microservice JAR. Changing it requires rebuilding and redeploying the application. Good for static, unchanging config.
-   **Spring Cloud Config (Remote):** Stored *outside* the application (e.g., in a Git repo). Changing it only requires a refresh (bean re-initialization) or restart. Critical for managing 50+ microservices where redeploying all to change one property is infeasible.

**Code Snippet:**
```
// Hierarchy:
1. Remote Git Config (High Priority)
2. Local application-profile.yml
3. Local application.yml (Low Priority)
```

---

## 143. How to use Spring Cloud with Eureka?

**Answer:**
**Eureka** is a Service Discovery server (Registry).
1.  **Server:** Create a Spring Boot app with `@EnableEurekaServer`.
2.  **Client:** Add `@EnableDiscoveryClient` to microservices.
3.  **Registration:** Clients register themselves with Eureka (IP, Port, Service ID) on startup.
4.  **Discovery:** Other services query Eureka to find the location of a service (e.g., "Where is user-service?") instead of hardcoding URLs.

**Code Snippet:**
```java
// Server
@SpringBootApplication
@EnableEurekaServer
public class RegistryApp { ... }

// Client (application.properties)
eureka.client.serviceUrl.defaultZone=http://localhost:8761/eureka/
```

---

## 144. What is a circuit breaker in Spring Cloud?

**Answer:**
A **Circuit Breaker** prevents cascading failures in microservices.
-   **State: CLOSED:** Requests flow normally.
-   **State: OPEN:** After a threshold of failures (e.g., 50% timeout), the circuit opens. Requests are **blocked immediately** (fail fast) without calling the failing service.
-   **State: HALF-OPEN:** After a specific wait time, a few requests are allowed to pass to test if the service has recovered.
-   **Implementation:** Resilience4j (Hystrix is deprecated).

**Code Snippet:**
```java
@CircuitBreaker(name = "backendA", fallbackMethod = "fallback")
public String remoteCall() {
    return restTemplate.getForObject("http://slow-service", String.class);
}

public String fallback(Exception e) {
    return "Default Response"; // Graceful degradation
}
```

---

## 145. What is Spring Cloud Gateway? Difference with Zuul?

**Answer:**
**Spring Cloud Gateway** is the modern API Gateway built on Spring WebFlux (Non-blocking).
-   **Zuul 1 (Legacy):** Blocking (Servlet 2.5), Thread-per-request. deprecated.
-   **Spring Cloud Gateway:** Non-blocking (Netty), built on Reactor. Supports WebSockets, long-lived connections, and better performance. Defines **Routes**, **Predicates** (matching logic), and **Filters** (modify request/response).

**Code Snippet:**
```yaml
spring:
  cloud:
    gateway:
      routes:
        - id: user_route
          uri: lb://user-service # Load Balanced URI
          predicates:
            - Path=/users/**
          filters:
            - AddRequestHeader=X-Auth, Token
```

---

## 146. How to write filters in Spring Gateway?

**Answer:**
Filters allow you to modify incoming requests or outgoing responses.
1.  **Pre-Filter:** Logic *before* sending request to downstream service (e.g., Authentication, Logging).
2.  **Post-Filter:** Logic *after* receiving response (e.g., Adding security headers).
3.  **Global vs GatewayFilter:** Global applies to all routes; GatewayFilter applies to specific routes.

**Code Snippet:**
```java
@Component
public class LoggingFilter implements GlobalFilter {
    @Override
    public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        System.out.println("Request: " + exchange.getRequest().getPath());
        return chain.filter(exchange)
            .then(Mono.fromRunnable(() -> {
                System.out.println("Response Status: " + exchange.getResponse().getStatusCode());
            }));
    }
}
```

---

## 147. What is Resilience4j and how is it integrated?

**Answer:**
**Resilience4j** is a lightweight fault tolerance library designed for Java 8 and functional programming. It replaces Hystrix.
-   **Modules:** Circuit Breaker, Rate Limiter, Retry, Bulkhead (Limiting concurrent calls).
-   **Integration:** Can be used with AOP annotations (`@Retry`, `@RateLimiter`) or programmatically decorators.
-   **Config:** Centralized config in `application.yml`.

**Code Snippet:**
```yaml
resilience4j.ratelimiter:
  instances:
    backendA:
      limitForPeriod: 10
      limitRefreshPeriod: 1s
      timeoutDuration: 0 # Fail immediately if limit reached
```

---

## 148. What is Sleuth and Zipkin? How do they work?

**Answer:**
They provide **Distributed Tracing**.
-   **Spring Cloud Sleuth (Micrometer Tracing in Boot 3):** Automatically generates Trace IDs (for the whole flow) and Span IDs (for individual steps). It injects these IDs into logs (MDC) so you can track a request across microservices.
-   **Zipkin:** A visualization server. Sleuth sends the trace data to Zipkin, which provides a UI to view the timeline, latency, and dependency graph of requests.

**Code Snippet:**
```text
// Log Output with Sleuth
// [Service-Name, TraceId, SpanId]
INFO [order-service, 65e3, 7a2b] : Processing Order...
```

---

## 149. What is Spring Retry?

**Answer:**
**Spring Retry** provides declarative retry support for operations that might fail transiently (e.g., network glitch).
-   **Usage:** Add `@EnableRetry` to config and `@Retryable` to methods.
-   **Features:** Specify exception types, max attempts, and backoff (delay) policy.

**Code Snippet:**
```java
@Retryable(
    value = SQLException.class, 
    maxAttempts = 3, 
    backoff = @Backoff(delay = 2000)
)
public void connectToDb() {
    // Fails -> Waits 2s -> Retries -> Fails -> Waits 2s -> Retries
}

@Recover
public void recover(SQLException e) {
    // Fallback logic after all retries fail
}
```

---

## 150. What are distributed transactions and how to manage them in Spring?

**Answer:**
A distributed transaction spans multiple databases or microservices. Maintaining ACID is hard.
-   **2PC (Two-Phase Commit):** Traditional (XA). Heavy locking, poor performance. Supported by JTA (`@Transactional`).
-   **SAGA Pattern (Recommended):** A sequence of local transactions. If one fails, **Compensating Transactions** are executed to undo previous changes.
    -   *Choreography:* Event-based (Services publish/listen to events).
    -   *Orchestration:* Central coordinator (e.g., Camunda, Axon) tells services what to do.

**Code Snippet:**
```java
// SAGA (Choreography)
// 1. Order Service: Creates Order (PENDING) -> Publishes OrderCreatedEvent
// 2. Inventory Service: Listens -> Reserves Stock -> Publishes StockReservedEvent
// 3. Payment Service: Listens -> Charges Card -> Publishes PaymentSuccessEvent
// 4. Order Service: Listens -> Updates Order to CONFIRMED
```

---

## 151. What is Saga Pattern?

**Answer:**
The **Saga Pattern** is a sequence of local transactions where each transaction updates data within a single service. The key idea is that distributed transactions (2PC) are avoided.
-   **Workflow:**
    1.  Service A execute a local transaction and publishes an event.
    2.  Service B listens to the event and executes its local transaction.
-   **Failure Handling:** If a step fails, the Saga executes **Compensating Transactions** (undo operations) to rollback changes made by previous steps.
-   **Types:**
    -   **Choreography:** decentralized (Event-based).
    -   **Orchestration:** Centralized (Coordinator tells services what to do).

**Code Snippet:**
```java
// Compensating Action Example
public void cancelOrder(Long orderId) {
    // 1. Re-add stock to inventory
    inventoryService.releaseStock(orderId);
    // 2. Refund payment
    paymentService.refund(orderId);
    // 3. Mark order as CANCELLED
    orderRepo.updateStatus(orderId, "FAILED");
}
```

---

## 152. How to implement service discovery?

**Answer:**
Service Discovery allows services to find each other dynamically without hardcoding Host/Port.
-   **Tools:** Netflix Eureka, Consul, Zookeeper, Kubernetes (Native DNS).
-   **Mechanism:**
    1.  **Register:** Service instances register their network location (IP:Port) with the Service Registry on startup.
    2.  **Fetch:** Clients (other services/Gateway) query the Registry to get the list of available instances for a service name.

**Code Snippet:**
```yaml
# application.yml for Eureka Client
eureka:
  client:
    serviceUrl:
      defaultZone: http://localhost:8761/eureka/
  instance:
    prefer-ip-address: true
```

---

## 153. Difference between Ribbon and Spring Cloud LoadBalancer?

**Answer:**
-   **Ribbon:**
    -   Netflix's client-side load balancer.
    -   Part of `spring-cloud-starter-netflix-ribbon`.
    -   **Blocking** I/O (initially).
    -   **Deprecated** (Maintenance mode).
-   **Spring Cloud LoadBalancer:**
    -   Spring's own replacement for Ribbon.
    -   Built with **Spring WebFlux** (Non-blocking support).
    -   Supports caching to reduce registry lookups.
    -   The default choice in modern Spring Cloud versions.

**Code Snippet:**
```java
// Usage (Automatic with OpenFeign or RestTemplate)
@LoadBalanced // Enables logical service name resolution
@Bean
public RestTemplate restTemplate() {
    return new RestTemplate();
}
// restTemplate.getForObject("http://user-service/...", ...)
```

---

## 154. What is Hystrix? Why is it deprecated?

**Answer:**
**Hystrix** is a latency and fault tolerance library from Netflix (Circuit Breaker implementation).
-   **Deprecated:** Netflix announced it entered maintenance mode in 2018. It was built on RxJava 1 (Blocking/Synchronous model issues with modern reactive stacks).
-   **Replacement:** **Resilience4j** is the recommended replacement. It is lightweight, modular, and designed for Java 8 functional programming and Reactive streams.

**Code Snippet:**
```java
// Legacy Hystrix Code
@HystrixCommand(fallbackMethod = "reliable")
public String getInfo() { ... }
```

---

## 155. What is FeignClient and how does it work?

**Answer:**
**Spring Cloud OpenFeign** is a declarative Web Service client. It makes writing HTTP clients easier.
-   **How it works:**
    1.  Create an Interface and annotate with `@FeignClient`.
    2.  Define methods mapped to HTTP endpoints (`@GetMapping`).
    3.  Spring generates a proxy implementation at runtime (using dynamic proxy).
    4.  It integrates automatically with **Service Discovery** (Eureka) and **Load Balancer**.

**Code Snippet:**
```java
@FeignClient(name = "user-service") // Service ID in Eureka
public interface UserClient {
    
    @GetMapping("/users/{id}")
    UserDTO getUser(@PathVariable("id") Long id);
}

// Usage: Inject UserClient and call getUser(1)
```

---

## 156. Difference between OpenFeign and RestTemplate?

**Answer:**
-   **RestTemplate:**
    -   Imperative, template-based client.
    -   Requires boilerplate (URL construction, parameter mapping).
    -   Harder to unit test directly.
    -   Maintenance mode.
-   **OpenFeign:**
    -   Declarative (Interface-based).
    -   No boilerplate (Just method signatures).
    -   Feels like calling a local method.
    -   Built-in support for Load Balancing, Circuit Breaking, and Error Handling (ErrorDecoder).

**Code Snippet:**
```java
// RestTemplate (Verdict: Verbose)
restTemplate.getForObject("http://user-service/users/" + id, User.class);

// Feign (Verdict: Clean)
userClient.getUser(id);
```

---

## 157. How does OAuth2 work with Spring Security?

**Answer:**
**OAuth2** is an authorization framework.
-   **Roles:** Resource Owner (User), Client (App), Authorization Server (Keycloak/Okta/Google), Resource Server (API).
-   **Spring Security 5+:**
    -   **Client Support:** `spring-boot-starter-oauth2-client` handles login redirect to Auth Server (e.g., "Login with Google").
    -   **Resource Server Support:** `spring-boot-starter-oauth2-resource-server` handles validating access tokens (JWT) sent by clients.

**Code Snippet:**
```yaml
spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          issuer-uri: https://idp.example.com/auth/realms/myrealm
```

---

## 158. What is JWT? How is it integrated with Spring Boot?

**Answer:**
**JWT (JSON Web Token)** is a compact, URL-safe means of representing claims to be transferred between two parties.
-   **Structure:** Header . Payload (Claims) . Signature.
-   **Integration:**
    1.  **Generation:** When user logs in, Server signs a JWT (using a secret or private key) and sends it to Client.
    2.  **Validation:** Client sends JWT in `Authorization: Bearer <token>` header. Server (Filter) verifies the signature and expiration on every request. **Stateless** (No session storage).

**Code Snippet:**
```java
// Verifying JWT (Conceptual)
String token = header.substring(7);
Claims claims = Jwts.parser()
    .setSigningKey(secretKey)
    .parseClaimsJws(token)
    .getBody();
String user = claims.getSubject();
```

---

## 159. How to secure microservices with API Gateway?

**Answer:**
The **API Gateway** acts as the single entry point and security guard.
1.  **Centralized Auth:** The Gateway handles Authentication (e.g., validating JWT or OAuth2 Token).
2.  **Token Relay:** If valid, the Gateway forwards the request to downstream microservices, passing the Access Token (Token Relay) or user context headers.
3.  **Microservices:** Downstream services act as Resource Servers, validating the token signature (or trusting the Gateway via mutual TLS/Network policies).

**Code Snippet:**
```yaml
# Spring Cloud Gateway Config
spring:
  cloud:
    gateway:
      default-filters:
        - TokenRelay # Forwards OAuth2 token
```

---

## 160. What is Spring Session?

**Answer:**
**Spring Session** provides an API and implementations for managing user session information.
-   **Problem:** In a clustered environment (multiple instances of a service), standard HttpSession is stored in the local memory of one server. If the next request hits another server, session is lost.
-   **Solution:** Spring Session stores session data in a **shared external store** like **Redis**, JDBC, or Hazelcast.
-   **Result:** Session is available across all instances (Distributed Session).

**Code Snippet:**
```java
// Dependency: spring-session-data-redis
// Config:
@EnableRedisHttpSession
public class SessionConfig { ... }

// Usage: Standard HttpSession API (Transparent)
session.setAttribute("user", user); // Saved to Redis automatically
```

---

## 161. How to implement rate limiting in Spring Boot?

**Answer:**
Rate Limiting restricts the number of requests a user/client can make within a time window to prevent abuse.
-   ** libraries:** Bucket4j, Resilience4j, or Spring Cloud Gateway (Redis Rate Limiter).
-   **Algorithm:** Token Bucket is common. (You have a bucket of tokens; each request consumes 1. Tokens refill at a fixed rate).
-   **Implementation:** Use an interceptor or Filter to check if tokens are available before processing.

**Code Snippet:**
```java
// Logic with Bucket4j
Bucket bucket = Bucket4j.builder()
    .addLimit(Bandwidth.classic(10, Refill.greedy(10, Duration.ofMinutes(1))))
    .build();

if (bucket.tryConsume(1)) {
    return processRequest();
} else {
    throw new HttpStatusException(429, "Too Many Requests");
}
```

---

## 162. What is Service Registry and how does it help?

**Answer:**
A **Service Registry** is a database of available service instances in a microservices architecture.
-   **Problem:** In the cloud, IP addresses of services change dynamically (auto-scaling, failures).
-   **Solution:** Services register with the Registry (Eureka, Consul) on startup. Clients query the Registry to get the current address.
-   **Benefit:** Enables **Client-Side Load Balancing** and resilience without hardcoding URLs.

**Code Snippet:**
```text
(Conceptual)
Service A (192.168.1.5) -> Registers -> [Service Registry]
Service B (Client) -> Asks Registry "Where is Service A?" -> Registry returns "192.168.1.5"
```

---

## 163. How to trace a request across multiple services?

**Answer:**
Distributed Tracing (via Spring Cloud Sleuth/Micrometer Tracing) is used.
-   **Trace ID:** A unique ID assigned to the *initial* incoming request.
-   **Propagation:** This ID is passed in HTTP headers (`X-B3-TraceId`) to all downstream microservices.
-   **Logging:** The ID is added to the logs (MDC). Aggregating logs by Trace ID shows the full journey.
-   **Visualization:** Tools like Zipkin or Jaeger visualize the flow.

**Code Snippet:**
```java
// Headers propagated automatically by Sleuth
// X-B3-TraceId: 463ac35c9f6413ad
// X-B3-SpanId: a2fb4a1d1a96d312
```

---

## 164. How to implement a custom starter in Spring Boot?

**Answer:**
A Custom Starter encapsulates logic and dependencies to be reused across multiple projects (e.g., a standard "Company Security Starter").
1.  **Project:** Create a Maven/Gradle project.
2.  **AutoConfiguration:** Create a `@Configuration` class.
3.  **Conditional Beans:** Use `@ConditionalOnClass`, `@ConditionalOnProperty` to load beans only when needed.
4.  **Registration:** Create a file `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` listing your config class.

**Code Snippet:**
```java
@AutoConfiguration
@ConditionalOnProperty(name = "company.security.enabled", havingValue = "true")
public class CompanySecurityConfig {
    @Bean
    public CompanyAuthFilter authFilter() {
        return new CompanyAuthFilter();
    }
}
```

---

## 165. How to test Spring Boot applications?

**Answer:**
Spring Boot provides `@SpringBootTest` to load the full application context for integration testing.
-   **`@SpringBootTest`:** Starts the container.
-   **`@MockBean`:** Mocks a specific bean inside the context (replaces the real one).
-   **`TestRestTemplate`:** Used to call the running server endpoints.

**Code Snippet:**
```java
@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
class AppTests {
    @Autowired TestRestTemplate restTemplate;

    @Test
    void testHealth() {
        String response = restTemplate.getForObject("/actuator/health", String.class);
        assertThat(response).contains("UP");
    }
}
```

---

## 166. What is MockMvc and when to use it?

**Answer:**
**MockMvc** allows testing Spring MVC Controllers (Web Layer) **without** starting a full HTTP Server.
-   **Speed:** Faster than `@SpringBootTest` because it mocks the Servlet API.
-   **Usage:** Validating HTTP status, Headers, and JSON response content.

**Code Snippet:**
```java
@WebMvcTest(UserController.class)
class UserControllerTest {
    @Autowired MockMvc mockMvc;

    @Test
    void getUser() throws Exception {
        mockMvc.perform(get("/users/1"))
               .andExpect(status().isOk())
               .andExpect(jsonPath("$.name").value("Alice"));
    }
}
```

---

## 167. How to mock external services in integration tests?

**Answer:**
When running integration tests, you shouldn't call real 3rd party APIs (Payment Gateway, Facebook).
1.  **@MockBean:** Replace the Service calling the API with a Mockito mock.
2.  **WireMock:** A library that spins up a lightweight HTTP server to mock the *actual Network call*. This is better as it tests the HTTP client configuration too.

**Code Snippet:**
```java
// WireMock Example
stubFor(get(urlEqualTo("/external-api"))
    .willReturn(aResponse()
    .withStatus(200)
    .withBody("{\"status\":\"success\"}")));
```

---

## 168. What is `@DataJpaTest`?

**Answer:**
It is a **Slice Test** annotation that loads only the JPA components (Repositories, Entities, DataSource).
-   **Features:**
    -   Ignores Controller/Service/Security beans.
    -   Configures an **in-memory database** (H2) automatically.
    -   **Rolls back** transactions at the end of each test (Database remains clean).
-   **Use Case:** Testing custom Repository queries using native SQL or JPQL.

**Code Snippet:**
```java
@DataJpaTest
class UserRepositoryTest {
    @Autowired UserRepository repo;

    @Test
    void findByEmail() {
        User user = new User("test@test.com");
        repo.save(user);
        
        Optional<User> found = repo.findByEmail("test@test.com");
        assertTrue(found.isPresent());
    }
}
```

---

## 169. What is TestContainers and how to use with Spring Boot?

**Answer:**
**TestContainers** is a Java library that provides disposable instances of common databases (Postgres, MySQL, Redis) running in **Docker containers**.
-   **Problem with H2:** H2 (In-memory) syntax differs from production DB (Postgres). Tests might pass on H2 but fail in prod.
-   **Solution:** TestContainers spins up a *real* Postgres Docker container for the test duration.
-   **Integration:** `@testcontainers` (JUnit 5 extension).

**Code Snippet:**
```java
@Testcontainers
@SpringBootTest
class IntegrationTest {
    @Container
    static PostgreSQLContainer<?> postgres = new PostgreSQLContainer<>("postgres:15");

    @DynamicPropertySource
    static void configureProperties(DynamicPropertyRegistry registry) {
        registry.add("spring.datasource.url", postgres::getJdbcUrl);
    }
}
```

---

## 170. What is the difference between Unit Test and Integration Test in Spring?

**Answer:**
-   **Unit Test:**
    -   Tests a **single class/method** in isolation.
    -   **Mocks** all dependencies (Mockito).
    -   **Fastest** (No Spring Context, No DB).
    -   *Example:* Testing business logic in a Service class.
-   **Integration Test:**
    -   Tests the **interaction** between components (Controller + Service + DB).
    -   Loads **Spring Context** (`@SpringBootTest`).
    -   Verification of wiring and configuration.
    -   *Example:* Calling an API endpoint and checking if data is saved to DB.

**Code Snippet:**
```java
// Unit Test
@ExtendWith(MockitoExtension.class)
class ServiceTest { 
    @Mock Repository repo; // Mock Dependency
}

// Integration Test
@SpringBootTest
class AppTest { 
    @Autowired Repository repo; // Real Dependency
}
```

---

## 171. How is a microservice different from a monolith?

**Answer:**
-   **Monolith:**
    -   Single codebase, single build artifact (WAR/JAR).
    -   Shared database (usually).
    -   Scaling requires cloning the entire heavy application.
    -   *Analogy:* A giant supermarket where everything is under one roof. If the checkout line breaks, the whole store stops.
-   **Microservice:**
    -   Small, independent services focused on a specific business domain (Bounded Context).
    -   Independent deployment and scaling.
    -   Own database per service (Database-per-service pattern).
    -   *Analogy:* A shopping mall with separate specialized stores (Bakery, Clothing). If the Bakery closes, the Clothing store is unaffected.

**Code Snippet:**
```text
Monolith Structure:       Microservices Structure:
[ War File ]              [ Jar ] -> User DB
  - User Logic            [ Jar ] -> Order DB
  - Order Logic           [ Jar ] -> Inventory DB
  - Database Conn
```

---

## 172. What are the advantages and disadvantages of microservices?

**Answer:**
-   **Advantages:**
    -   **Scalability:** Scale only the hot services (e.g., Scale Order Service during Black Friday).
    -   **Fault Isolation:** One service crash doesn't bring down the whole system.
    -   **Tech Agnostic:** Use Java for backend, Node.js for I/O heavy tasks, Python for AI.
-   **Disadvantages:**
    -   **Complexity:** Distributed systems are hard (Network failures, Latency, Consistency).
    -   **Operational Overhead:** Need DevOps, Monitoring, and Orchestration (Kubernetes).
    -   **Data consistency:** Hard to maintain ACID across services (SAGA needed).

**Code Snippet:**
```text
Complexity Graph:
Monolith: Starts Low -> Grows Exponentially with code size.
Microservices: Starts High (Base complexity) -> Grows Linearly.
```

---

## 173. How do microservices communicate?

**Answer:**
1.  **Synchronous (Blocking):**
    -   REST (JSON/HTTP) or gRPC (Protobuf).
    -   *Use Case:* Immediate response required (e.g., UI waiting for data).
    -   *Downside:* Coupling. If B is down, A fails (or waits).
2.  **Asynchronous (Non-Blocking):**
    -   Message Broker (RabbitMQ, Kafka, ActiveMQ).
    -   *Use Case:* Fire and Forget (e.g., Sending Emails, Analytics).
    -   *Benefit:* Decoupled. If B is down, message stays in queue until B recovers.

**Code Snippet:**
```java
// Sync (RestTemplate)
response = restTemplate.getForObject("http://service/api", String.class);

// Async (RabbitMQ)
rabbitTemplate.convertAndSend("order-queue", orderObj);
```

---

## 174. What is Service Discovery?

**Answer:**
Service Discovery is the mechanism to automatically locate the network locations (IP and Port) of service instances.
-   **Client-Side Discovery:** Client queries the Registry (Eureka) to get the address, then calls the service directly. (Spring Cloud LoadBalancer).
-   **Server-Side Discovery:** Client calls a Load Balancer (AWS ELB, NGINX), which queries the Registry and forwards the request.

**Code Snippet:**
```text
Registry Table (Conceptual):
| Service Name | IP Address    | Port | Status |
|--------------|---------------|------|--------|
| user-service | 10.0.0.1      | 8080 | UP     |
| user-service | 10.0.0.2      | 8080 | UP     |
| order-service| 192.168.1.5   | 9000 | UP     |
```

---

## 175. What is Eureka and how does it work?

**Answer:**
**Netflix Eureka** is a REST-based Service Registry (Discovery Server).
-   **Heartbeat:** Registered services send a heartbeat (pulse) every 30 seconds.
-   **Eviction:** If Eureka doesn't receive a heartbeat for 90 seconds, it removes the instance from the registry.
-   **Self-Preservation:** If massive network partition happens (many distinct heartbeats fail), Eureka stops expiring instances to prevent removing healthy instances that are just unreachable.

**Code Snippet:**
```java
@EnableEurekaServer // On the Server App
@EnableDiscoveryClient // On the Microservices
```

---

## 176. What is API Gateway in microservices?

**Answer:**
An API Gateway is a server that acts as the single entry point for the system.
-   **Responsibilities:**
    -   **Routing:** Forwarding API calls to the correct microservice.
    -   **Cross-Cutting Concerns:** Authentication (OAuth2), SSL Termination, Rate Limiting, Logging, CORS.
    -   **Aggregation:** (Optional) Combining results from multiple services into one response (GraphQL or Backend-for-Frontend).

**Code Snippet:**
```text
Client -> [ API GATEWAY ] -> Service A
                          -> Service B
                          -> Service C
```

---

## 177. How does Spring Cloud Gateway work?

**Answer:**
Spring Cloud Gateway matches routes based on attributes of the incoming request (Path, Header, Host).
-   **Route:** ID, Destination URI, Predicates, and Filters.
-   **Predicate:** Java 8 Function Predicate. Matches the Request (e.g., `Path=/api/v1/**`).
-   **Filter:** Modifies Request/Response (e.g., `AddRequestHeader`).

**Code Snippet:**
```yaml
spring:
  cloud:
    gateway:
      routes:
        - id: payment_route
          uri: lb://payment-service
          predicates:
            - Path=/payments/**
            - Method=POST
```

---

## 178. What are Edge Services?

**Answer:**
Edge Services sits at the boundary (Edge) of your network, exposing your internal microservices to the outside world (Public Internet/Mobile Apps).
-   **Examples:** API Gateway, Load Balancers, Firewalls (WAF).
-   **Role:** They are the first line of defense. They handle public traffic, DDoS protection, and translation from public protocols (HTTP/JSON) to internal protocols (gRPC/Thrift).

**Code Snippet:**
```text
[ Internet ] -> [ Edge Service (Zuul/SCG) ] -> [ Private Network (Microservices) ]
```

---

## 179. Explain the importance of Bounded Contexts in microservices.

**Answer:**
**Bounded Context** is a central pattern in Domain-Driven Design (DDD). It defines the boundaries of a specific domain model.
-   **Concept:** The same term can mean different things in different contexts.
-   **Example:**
    -   In **Sales Context**, a `User` is a "Lead" or "Customer" (Interested in buying).
    -   In **Support Context**, a `User` is a "Ticket Requester" (Has a problem).
    -   In **Shipping Context**, a `User` is a "Recipient" (Address + Name).
-   **Microservice Mapping:** Ideally, **1 Bounded Context = 1 Microservice**. Do not try to create a single "Universal User Model".

**Code Snippet:**
```java
// Sales Service
class Customer { Long id; String salesFunnelStatus; }

// Shipping Service
class Recipient { Long id; String shippingAddress; }
```

---

## 180. What is Domain-Driven Design (DDD)?

**Answer:**
DDD is a software design approach giving priority to the **Domain Logic** (Business Rules) over Technology.
-   **Strategic Design:** Define Bounded Contexts and Ubiquitous Language (Common language between Devs and Business).
-   **Tactical Design:** Building blocks inside the code:
    -   **Entity:** Object with ID (User, Order).
    -   **Value Object:** Object defined by attributes, immutable, no ID (Money, Address, Email).
    -   **Aggregate:** A cluster of Entities treated as a unit (Order + OrderItems). One Root Entity controls access.
    -   **Repository:** Abstraction to load Aggregates.

**Code Snippet:**
```java
// Entity
class Order { @Id Long id; List<OrderItem> items; }

// Value Object
record Address(String street, String city) {} // Immutable
```

---

## 181. What is the difference between orchestration and choreography in microservices?

**Answer:**
Both are methods for managing interactions (Sagas) between microservices.
-   **Orchestration (Conductor):** Centralized. A specific service (Orchestrator) tells other services what to do.
    -   *Pros:* Easy to monitor and manage complex workflows.
    -   *Cons:* Tight coupling; Single point of failure (the orchestrator).
    -   *Analogy:* An Orchestra Conductor directing musicians.
-   **Choreography (Dancers):** Decentralized. Services react to events. No central coordinator.
    -   *Pros:* Loose coupling; Scalable.
    -   *Cons:* Harder to track the full workflow (observability).
    -   *Analogy:* Dancers on stage knowing their steps when the music changes.

**Code Snippet:**
```text
Orchestration: OrderService -> (Call) Payment -> (Call) Inventory -> (Call) Shipping
Choreography:  OrderService (Pub: OrderCreated) -> Payment (Sub: OrderCreated) -> Inventory (Sub: PaymentSuccess)
```

---

## 182. What is a distributed transaction?

**Answer:**
A transaction that spans across multiple databases or services.
-   **Challenge:** In a monolith with one DB, ACID is guaranteed by the DB engine. In Microservices, each service has its own DB. Ensuring that an update in Service A and Service B *both* succeed or *both* fail is extremely difficult (CAP Theorem).
-   **Solution:** Avoid 2PC (Two-Phase Commit) due to locking performance issues. Use **Saga Pattern** (Eventual Consistency).

**Code Snippet:**
```text
Transaction T1 (Service A: DB1)
Transaction T2 (Service B: DB2)
Both must commit, or both must rollback.
```

---

## 183. How do you achieve eventual consistency?

**Answer:**
**Eventual Consistency** guarantees that if no new updates are made to a given data item, eventually all accesses to that item will return the last updated value.
-   **Mechanism:**
    1.  Update local data.
    2.  Publish an event (asynchronously) to a Message Broker.
    3.  Other services consume the event and update their data.
    4.  There is a lag (milliseconds to seconds) where data is inconsistent, but it eventually converges.

**Code Snippet:**
```java
// Service A: Update User -> Fire Event
kafkaTemplate.send("user-updates", user);

// Service B (Replica/Cache): Listen -> Update
@KafkaListener(topics = "user-updates")
public void sync(User user) { ... }
```

---

## 184. Explain the Saga pattern with example.

**Answer:**
(As explained in Q151, elaborated here with a concrete failure scenario).
**Scenario: Booking a Trip.**
1.  **Step 1 (Flight Service):** Book Flight. (Success). Publishes `FlightBookedEvent`.
2.  **Step 2 (Hotel Service):** Listens to `FlightBookedEvent`. Tries to Book Hotel. **FAILS** (No rooms).
3.  **Compensating Transaction:** Hotel Service publishes `HotelBookingFailedEvent`.
4.  **Step 3 (Flight Service):** Listens to `HotelBookingFailedEvent`. Executes **Cancel Flight** (Undo Step 1).
5.  **Result:** System returns to consistent state (Nothing booked).

**Code Snippet:**
```java
// Flight Service Listener
@KafkaListener(topics = "hotel-booking-failed")
public void compensate(BookingId id) {
    flightRepository.cancelBooking(id); // Undo
}
```

---

## 185. How would you handle inter-service communication failures?

**Answer:**
Network calls will fail. Strategies to handle them:
1.  **Retries:** For transient errors (Network glitch). Use Exponential Backoff.
2.  **Timeouts:** Fail fast if a service is too slow. Don't block threads indefinitely.
3.  **Circuit Breaker:** Stop calling a failing service to give it time to recover.
4.  **Fallback:** Return a default value or cached response.
5.  **Bulkhead:** Isolate resources (Thread pools) so one failing service doesn't consume all threads.

**Code Snippet:**
```java
// Resilience4j Retry Config
retry:
  maxAttempts: 3
  waitDuration: 500ms
```

---

## 186. What is Circuit Breaker pattern?

**Answer:**
Imagine a house fuse box. If a specific appliance shorts, the fuse blows (Open Circuit) to protect the whole house wiring.
-   **Software:** If Service A calls Service B and Service B fails repeatedly (e.g., 50% error rate), the Circuit Breaker "Opens".
-   **Effect:** Service A stops calling Service B immediately and returns an error/fallback. This prevents resource exhaustion (threads waiting) and allows Service B to recover.

**Code Snippet:**
```java
// State Transition:
// CLOSED (Normal) --(Failures > Threshold)--> OPEN (Block calls)
// OPEN --(Wait Time)--> HALF-OPEN (Test) --(Success)--> CLOSED
```

---

## 187. How does Resilience4j work?

**Answer:**
**Resilience4j** is a modular library based on functional interfaces (`Supplier`, `Function`).
-   It uses **Decorators** around your functional calls.
-   **Modules:**
    -   `CircuitBreaker`: Tracks failure rate/slow calls.
    -   `RateLimiter`: Token bucket algorithm.
    -   `Bulkhead`: Semaphore or ThreadPool isolation.
    -   `Retry`: Loop with sleep.
    -   `TimeLimiter`: `CompletableFuture` handling.

**Code Snippet:**
```java
CircuitBreaker cb = CircuitBreaker.ofDefaults("backendService");
Supplier<String> decorated = CircuitBreaker.decorateSupplier(cb, () -> callRemote());
String result = Try.ofSupplier(decorated).recover(e -> "Fallback").get();
```

---

## 188. What is rate limiting? How do you implement it?

**Answer:**
**Rate Limiting** controls the rate of traffic sent by a client or service.
-   **Algorithms:**
    -   **Token Bucket:** Tokens are added at a fixed rate. Request consumes a token. Allows bursts.
    -   **Leaky Bucket:** Requests enter a queue and are processed at a constant rate. Smooths traffic.
    -   **Fixed Window:** Max X requests per minute. (Issue: Spike at second 59 and 00).
    -   **Sliding Window:** Smoother version of Fixed Window.
-   **Implementation:** Spring Cloud Gateway (Redis Rate Limiter) or Bucket4j.

**Code Snippet:**
```yaml
# Spring Cloud Gateway (Redis)
filters:
  - name: RequestRateLimiter
    args:
      redis-rate-limiter.replenishRate: 10 # 10 req/sec
      redis-rate-limiter.burstCapacity: 20
```

---

## 189. How to design idempotent APIs?

**Answer:**
**Idempotency** means making multiple identical requests has the same effect as making a single request.
-   **Safe Methods:** GET, PUT, DELETE should be idempotent by definition.
-   **Unsafe Methods:** POST (Creation) is not naturally idempotent.
-   **Implementation:**
    1.  Client generates a unique ID (`Idempotency-Key` UUID) for the request.
    2.  Server stores this Key + Response in a specific table/cache.
    3.  If a duplicate request comes with the same Key, return the stored response instead of processing again.

**Code Snippet:**
```java
// Pseudocode
if (redis.exists(key)) {
    return redis.get(key); // Return cached response
}
process();
redis.save(key, response);
```

---

## 190. What is a fallback method in circuit breaker?

**Answer:**
A **Fallback Method** is an alternative logic executed when the primary operation fails (Exception or Open Circuit).
-   **Purpose:** Graceful degradation. Instead of throwing "500 Internal Server Error" to the user, show somewhat useful data.
-   **Examples:**
    -   Primary DB down -> Read from Cache.
    -   Recommendation Engine down -> Show "Top 10 Popular Items".
    -   Inventory Check down -> Assume "In Stock" (Optimistic) or "Out of Stock" (Safe).

**Code Snippet:**
```java
@CircuitBreaker(name = "rec-service", fallbackMethod = "getPopularItems")
public List<Item> getRecommendations(User user) {
    throw new RuntimeException("Service Down");
}

public List<Item> getPopularItems(User user, Throwable t) {
    return List.of(new Item("iPhone"), new Item("MacBook")); // Default List
}
```

---

## 191. What is load balancing? Types?

**Answer:**
**Load Balancing** is the process of distributing incoming network traffic across multiple servers to ensure no single server becomes overwhelmed.
-   **L4 (Transport Layer):** Balances based on IP/Port (TCP/UDP). Very fast. (e.g., AWS Network Load Balancer).
-   **L7 (Application Layer):** Balances based on HTTP headers, URLs, Cookies. Smarter but slower. (e.g., NGINX, HAProxy, AWS ALB).

**Code Snippet:**
```text
(Conceptual)
Client -> [ Load Balancer ] -> Server 1 (CPU: 20%)
                            -> Server 2 (CPU: 80%) [Skipped]
                            -> Server 3 (CPU: 30%)
```

---

## 192. Difference between client-side and server-side load balancing.

**Answer:**
-   **Server-Side:**
    -   The client calls a single URL (e.g., `api.com`), which resolves to a Load Balancer (Hardware or NGINX). The LB forwards traffic.
    -   *Pros:* Simple client.
    -   *Cons:* Extra hop (latency), LB is a bottleneck.
-   **Client-Side:**
    -   The client gets a list of available IP addresses (from Service Registry) and chooses one itself (Round Robin/Random).
    -   *Pros:* No extra hop, better performance.
    -   *Cons:* Complex client logic (Ribbon/Spring Cloud LoadBalancer).

**Code Snippet:**
```java
// Client-Side (Pseudo)
List<String> servers = registry.get("user-service");
String target = servers.get(random.nextInt(servers.size()));
httpClient.get(target);
```

---

## 193. What is Ribbon? Is it still used?

**Answer:**
**Netflix Ribbon** is an Inter-Process Communication (IPC) library with built-in client-side load balancers.
-   **Status:** It is **maintenance mode** (deprecated) since 2018.
-   **Reason:** It was blocking and not compatible with modern reactive stacks (WebFlux).
-   **Replacement:** Spring Cloud LoadBalancer.

**Code Snippet:**
```properties
# Legacy Ribbon Config
user-service.ribbon.listOfServers=localhost:8081,localhost:8082
```

---

## 194. What is Spring Cloud LoadBalancer?

**Answer:**
It is the modern, non-blocking replacement for Ribbon, provided by the Spring Cloud team.
-   It integrates with Service Discovery (Eureka/Consul) to get the server list.
-   It supports caching the service list.
-   It works seamlessly with `WebClient` (Reactive) and `RestTemplate`.

**Code Snippet:**
```java
@Bean
@LoadBalanced // This annotation enables the interceptor
public WebClient.Builder webClientBuilder() {
    return WebClient.builder();
}
// Calling "http://user-service" automatically resolves to an IP
```

---

## 195. What is API versioning and how to implement it?

**Answer:**
API Versioning manages changes to the API without breaking existing clients.
-   **Strategies:**
    1.  **URI Path:** `/api/v1/users` (Most common, easy to cache).
    2.  **Query Param:** `/api/users?version=1` (Easy but hard to route).
    3.  **Custom Header:** `X-API-VERSION: 1` (Clean URL, harder to test in browser).
    4.  **Media Type (Accept Header):** `Accept: application/vnd.company.v1+json` (The "RESTful" way).

**Code Snippet:**
```java
@GetMapping(value = "/users", params = "version=1")
public UserV1 getUserV1() { ... }

@GetMapping(value = "/users", params = "version=2")
public UserV2 getUserV2() { ... }
```

---

## 196. How to secure microservices using OAuth2?

**Answer:**
Securing microservices usually involves an **Authorization Server** (Identity Provider) and **Resource Servers** (Microservices).
1.  **User Login:** User authenticates with Auth Server (e.g., Keycloak) → Receives Access Token (JWT).
2.  **API Call:** User sends Token in `Authorization` header to Gateway/Microservice.
3.  **Validation:** Microservice validates the signature of the JWT (locally via Public Key or remotely via Introspection endpoint).

**Code Snippet:**
```yaml
spring:
  security:
    oauth2:
      resourceserver:
        jwt:
          jwk-set-uri: https://idp.example.com/.well-known/jwks.json
```

---

## 197. What is JWT? How to use it in microservices?

**Answer:**
(Expansion on Q158).
-   **JWT (JSON Web Token)** is self-contained. It carries user info (Claims: ID, Roles, Expiry) inside the token string itself.
-   **Stateless:** The server doesn't need to query a DB to check if the user is logged in. It just verifies the cryptographic signature.
-   **Usage:** Pass the JWT through the entire microservice chain (Token Propagation).

**Code Snippet:**
```json
// Decoded JWT Payload
{
  "sub": "1234567890",
  "name": "John Doe",
  "admin": true,
  "exp": 1516239022
}
```

---

## 198. What is token propagation?

**Answer:**
**Token Propagation** (or Relay) relies on passing the authentication token (JWT) from one microservice to another in the chain.
-   **Scenario:** User -> Gateway (Auth) -> Service A -> Service B.
-   **Problem:** Service A needs to call Service B *on behalf of the user*.
-   **Solution:** Service A reads the `Authorization` header from the incoming request and copies it to the outgoing request to Service B. `FeignRequestInterceptor` or `WebClient` filters usually handle this.

**Code Snippet:**
```java
// Feign Interceptor to propagate token
@Bean
public RequestInterceptor requestInterceptor() {
    return template -> {
        String token = // get token from SecurityContext/Request
        template.header("Authorization", "Bearer " + token);
    };
}
```

---

## 199. How do you handle secrets in microservices?

**Answer:**
**Secrets** (DB passwords, API Keys) should NEVER be committed to Git.
-   **Environment Variables:** Inject them at runtime (Docker/K8s).
-   **Vault (HashiCorp):** Use centralized Secret Management. Spring Cloud Vault reads secrets securely on startup.
-   **Config Server (Cipher):** Encrypt properties in Git (`{cipher}FKJ...`) and decrypt them on the Config Server using a symmetric key.

**Code Snippet:**
```yaml
spring:
  datasource:
    password: ${DB_PASSWORD} # Injected from OS Env / K8s Secret
```

---

## 200. What is config server?

**Answer:**
(Recap from Q141).
**Spring Cloud Config Server** creates a centralized configuration management system.
-   **Why:** In a 100-microservice system, changing a DB URL in 100 `application.properties` files and redeploying 100 JARs is impossible.
-   **Solution:** All services point to Config Server. Config Server reads from a single Git Repo (`microservices-config`). You update the Git file once, and all services pick it up (after Refresh).

**Code Snippet:**
```bash
# Workflow
Dev -> Push change to Git -> Webhook -> Config Server -> Bus -> Microservices (Refresh)
```

## 201. How to refresh config without restarting services?

**Answer:**
You need to trigger a **Refresh Event** in the Spring Context.
-   **Manual:** Send a `POST /actuator/refresh` request to the application. This re-fetches configuration from the Config Server and updates beans annotated with `@RefreshScope`.
-   **Automatic (Spring Cloud Bus):**
    1.  Push change to Git.
    2.  Webhook triggers Config Server.
    3.  Config Server publishes an event to a Message Broker (RabbitMQ/Kafka).
    4.  All microservices listening to the broker receive the event and refresh themselves.

**Code Snippet:**
```java
@RefreshScope // Reloads bean when config changes
@RestController
class MessageController {
    @Value("${message}") String message;
}
```

---

## 202. What is bootstrap.yml vs application.yml?

**Answer:**
-   **`application.yml`:** The standard configuration file for the application application context. Loaded *after* the bootstrap context.
-   **`bootstrap.yml`:** Loaded *before* `application.yml` by the parent "Bootstrap Context".
    -   **Usage:** It is used to configure properties needed *to fetch* the external configuration (e.g., Config Server URL, Decryption keys).
    -   *Note:* In Spring Boot 2.4+, `bootstrap.yml` is deprecated in favor of `execution.config.import` in `application.yml`.

**Code Snippet:**
```yaml
# bootstrap.yml
spring:
  application:
    name: user-service
  cloud:
    config:
      uri: http://config-server:8888
```

---

## 203. What is centralized logging?

**Answer:**
In microservices, logs are scattered across multiple servers/containers. Debugging is impossible by SSH-ing into each one.
-   **Solution:** Ship all logs to a central location.
-   **ELK Stack:**
    -   **Elasticsearch:** Search Engine (Database).
    -   **Logstash/Fluentd:** Log Collector and Processor (Ingest).
    -   **Kibana:** Visualization Dashboard (UI).
-   **Workflow:** App -> Log File/Console -> Filebeat -> Logstash -> Elasticsearch -> Kibana.

**Code Snippet:**
```xml
<!-- Logback Appender (Conceptual) -->
<appender name="LOGSTASH" class="net.logstash.logback.appender.LogstashTcpSocketAppender">
    <destination>localhost:5000</destination>
</appender>
```

---

## 204. How does distributed tracing work?

**Answer:**
(See Q163).
Distributed tracing tracks a request as it flows through multiple microservices.
-   It assigns a **Trace ID** to the request at the entry point.
-   This ID is passed via headers (`B3-Propagation`) to all subsequent calls.
-   **Spans** represent individual units of work (e.g., Service A calling Service B).
-   Tracing systems collect these spans to build a "waterfall" graph of latency.

**Code Snippet:**
```text
Trace ID: 123
  |-- Span A (Gateway): 100ms
      |-- Span B (User Service): 50ms
          |-- Span C (DB Query): 20ms
```

---

## 205. What is Sleuth? What is Zipkin?

**Answer:**
-   **Spring Cloud Sleuth (Micrometer Tracing):**
    -   The *instrumentation* library.
    -   It automatically adds Trace IDs and Span IDs to logs.
    -   It injects headers into `RestTemplate`, `WebClient`, `Feign`.
-   **Zipkin:**
    -   The *server* and *UI*.
    -   It collects the traces sent by Sleuth.
    -   Provides a UI to search traces and visualize latency graphs.

**Code Snippet:**
```yaml
# sending spans to Zipkin
management:
  zipkin:
    tracing:
      endpoint: "http://zipkin:9411/api/v2/spans"
```

---

## 206. What are Span and Trace IDs?

**Answer:**
-   **Trace ID:** A unique identifier for the **entire** request chain (from user click to final response). It remains constant across all services involved in that request.
-   **Span ID:** A unique identifier for a **specific operation** (or hop) within the trace. Every time a request enters a new service (or a new thread/method), a new Span is created.
-   **Relationship:** A Trace is a tree of Spans.

**Code Snippet:**
```text
Log format: [Service Name, Trace ID, Span ID]
INFO [user-service, 5g7h8... , 1a2b3...] : Fetching user...
```

---

## 207. What is an Anti-Corruption Layer?

**Answer:**
A simplified layer (adapter) placed between your modern microservices and a legacy system (Monolith/Mainframe).
-   **Problem:** The legacy system has a messy, complex, or incompatible domain model.
-   **Solution:** The ACL translates the legacy model into your clean domain model. It prevents the "corruption" (bad design) of the legacy system from leaking into your new system.

**Code Snippet:**
```java
// Legacy Model: Map<String, Object> (Messy)
// New Domain Model: User (Clean)

public User getUser(String id) {
    Map<String, Object> legacyData = mainframeClient.fetch(id);
    return adapt(legacyData); // ACL Translation logic
}
```

---

## 208. What is the database-per-service pattern?

**Answer:**
Each microservice manages its own database.
-   **Rule:** Other services generally cannot access the database directly; they must use the owning service's API.
-   **Pros:** Loose coupling (Schema changes in A don't break B), Service autonomy.
-   **Cons:** Distributed transactions (Saga), Data duplication, cross-service queries (CQRS needed).

**Code Snippet:**
```text
Order Service -> Order DB (MySQL)
Catalog Service -> Catalog DB (Mongo)
Recommendation Service -> Rec DB (Neo4j)
```

---

## 209. What are shared-nothing architectures?

**Answer:**
An architecture where nodes (servers) do not share memory or disk storage.
-   Each node is independent and self-sufficient.
-   **Scaling:** You can simply add more nodes (Horizontal Scaling) without contention on shared resources (like a central lock manager or shared disk).
-   **Microservices:** Ideally follow this (Stateless services + Sharded/Partitioned DBs).

**Code Snippet:**
```text
Node 1 (CPU + RAM + Disk)  |  Node 2 (CPU + RAM + Disk)
       \                  /
        \                /
        (No Shared State)
```

---

## 210. What is CQRS? When to use it?

**Answer:**
**CQRS (Command Query Responsibility Segregation)** separates the models for reading and writing.
-   **Command (Write):** Handles Create, Update, Delete. Optimized for transactional integrity and business logic.
-   **Query (Read):** Handles Reads. Optimized for speed and display.
-   **Implementation:** Often uses two different databases. Write to DB1 -> Event -> Sync to Read DB2 (Elasticsearch/Redis).
-   **When to use:** High read/write disparity (1000 reads : 1 write), complex UI views requiring data from multiple aggregates.

**Code Snippet:**
```java
// Command Side (JPA)
public void createUser(CreateUserCmd cmd) { ... }

// Query Side (JdbcTemplate / Elasticsearch)
public UserStatsView getUserStats(String id) { ... }
```

---

## 211. What is Event Sourcing?

**Answer:**
**Event Sourcing** is a pattern where the state of the application is determined by a sequence of events, rather than just storing the current state.
-   **Traditional:** Update the `User` table (Current State). History is lost unless logged.
-   **Event Sourcing:** Store every change as an immutable event (`UserCreated`, `UserAddressChanged`, `UserDeactivated`).
-   **State Reconstruction:** Replay all events from the beginning to get the current state.
-   **Audit:** Perfect audit trail (we know exactly *what* happened and *when*).

**Code Snippet:**
```text
Event Store:
1. UserCreated(id=1, name="Alice")
2. UserAddressChanged(id=1, city="NY")
3. UserAddressChanged(id=1, city="SF")
Current State: Alice, SF.
```

---

## 212. What is a Sidecar Pattern?

**Answer:**
The **Sidecar Pattern** deploys a helper component (container) alongside the main application container (in the same Pod in K8s).
-   **Purpose:** Abstraction of infrastructure concerns (Logging, Monitoring, proxying Network traffic, SSL).
-   **Benefit:** The main application (written in Java) doesn't need dependencies for these concerns. The sidecar (written in Go/C++) handles them.

**Code Snippet:**
```text
[ POD ]
  |-- [ App Container (Java) ] <--> localhost <--> [ Sidecar Proxy (Envoy) ] <--> Network
```

---

## 213. What is Service Mesh? What tools are used?

**Answer:**
A **Service Mesh** is a dedicated infrastructure layer for handling service-to-service communication.
-   **Implementation:** It injects a **Sidecar Proxy** (e.g., Envoy) next to every service instance.
-   **Features:**
    -   Traffic Management (Canary deployments, A/B testing).
    -   Security (mTLS between all services automatically).
    -   Observability (Tracing, Metrics).
-   **Tools:** Istio, Linkerd, Consul Connect.

**Code Snippet:**
```text
Without Mesh: App A talks directly to App B.
With Mesh:    App A talks to Sidecar A -> Sidecar B -> App B.
```

---

## 214. What is Istio and Linkerd?

**Answer:**
Both are popular Service Mesh implementations for Kubernetes.
-   **Istio:**
    -   Feature-rich, highly configurable.
    -   Uses **Envoy** as the sidecar proxy.
    -   Backed by Google/IBM/Lyft.
    -   Can be complex to manage.
-   **Linkerd:**
    -   Lightweight, simpler, "it just works".
    -   Uses its own Rust-based micro-proxy.
    -   Focuses on simplicity and performance.

**Code Snippet:**
```yaml
# Istio VirtualService (Traffic Splitting)
spec:
  hosts:
  - reviews
  http:
  - route:
    - destination:
        host: reviews
        subset: v1
      weight: 75
    - destination:
        host: reviews
        subset: v2
      weight: 25
```

---

## 215. How do you monitor microservices?

**Answer:**
Monitoring involves collecting, aggregating, and analyzing metrics to understand the health and performance of the system.
-   **The 4 Golden Signals:**
    1.  **Latency:** Time taken to serve a request.
    2.  **Traffic:** Demand (Requests per second).
    3.  **Errors:** Rate of request failures (HTTP 500s).
    4.  **Saturation:** How "full" the service is (CPU, Memory, Queue depth).
-   **Stack:** Prometheus (Metrics), Grafana (Dashboard), AlertManager (Paging).

**Code Snippet:**
```text
PromQL (Prometheus Query Language):
rate(http_requests_total[5m])  // Average request rate over 5 minutes
```

---

## 216. What is Prometheus and Grafana?

**Answer:**
-   **Prometheus:**
    -   An open-source systems monitoring and alerting toolkit.
    -   **Pull Model:** It *scrapes* metrics from HTTP endpoints (e.g., `/actuator/prometheus`) at regular intervals.
    -   Stores data as Time Series.
-   **Grafana:**
    -   An open-source analytics and visualization platform.
    -   Connects to Prometheus (and other data sources).
    -   Displays beautiful graphs, heatmaps, and gauges.

**Code Snippet:**
```yaml
# Prometheus Scrape Config
scrape_configs:
  - job_name: 'spring-actuator'
    metrics_path: '/actuator/prometheus'
    static_configs:
      - targets: ['localhost:8080']
```

---

## 217. What are metrics and observability?

**Answer:**
-   **Metrics:** "What is happening?" (Aggregated numbers).
    -   *Example:* CPU is at 90%. Average latency is 200ms.
-   **Observability:** "Why is it happening?" (Granular insights).
    -   A property of the system that allows you to understand its internal state from external outputs (Logs, Metrics, Traces).
    -   It helps debug "unknown unknowns" (issues you didn't predict).

**Code Snippet:**
```text
Observability Pillars:
1. Logs (Events)
2. Metrics (Aggregates)
3. Traces (Context/Flow)
```

---

## 218. What is Health Check API?

**Answer:**
An endpoint used by infrastructure (Kubernetes, AWS LB) to check if the application is running and ready to accept traffic.
-   **Liveness Probe:** "Is the app alive?"
    -   If Fails: Restart the container. (Checking against deadlocks).
-   **Readiness Probe:** "Is the app ready to serve traffic?"
    -   If Fails: Remove from Load Balancer. (Checking if DB connection, Cache warming is done).

**Code Snippet:**
```text
GET /actuator/health/liveness
GET /actuator/health/readiness
```

---

## 219. How to perform health checks in Spring Boot?

**Answer:**
Spring Boot Actuator provides built-in health indicators.
-   **Endpoint:** `/actuator/health`.
-   **Logic:** It aggregates the health of all subsystems (DB, Disk Space, Redis, Mail Server).
-   **Custom Health Check:** Implement `HealthIndicator`.

**Code Snippet:**
```java
@Component
public class CustomHealthIndicator implements HealthIndicator {
    @Override
    public Health health() {
        if (checkExternalService()) {
            return Health.up().build();
        }
        return Health.down().withDetail("Reason", "Service unavailable").build();
    }
}
```

---

## 220. How do you debug issues in a distributed environment?

**Answer:**
Debugging is hard because you can't step-through code across servers easily.
1.  **Correlation ID:** The most important tool. Search logs in Kibana using the Request/Trace ID.
2.  **Centralized Logging:** Ensure logs from all services are in one place (ELK/Splunk) with timestamps synchronized.
3.  **Distributed Tracing:** Check Zipkin/Jaeger to see *where* the latency/error occurred.
4.  **Metrics:** Check Grafana to see if the issue correlates with a spike in traffic or resource exhaustion.
5.  **Simulate:** Use Chaos Engineering (Chaos Monkey) to reproduce failures.

**Code Snippet:**
```bash
# Kibana Search
service: "payment-service" AND traceId: "463ac35c9f6413ad" AND level: "ERROR"
```

---

## 221. What are dead-letter queues?

**Answer:**
A **Dead Letter Queue (DLQ)** is a service implementation to store messages that meet one or more of the following criteria:
-   Message that is sent to a queue that does not exist.
-   Queue length limit exceeded.
-   Message size length exceeded.
-   Message is rejected by another queue exchange.
-   Message reaches a threshold read counter number, because it is not consumed.
**Process:**
1.  Consumer reads message.
2.  Processing fails (Exception).
3.  Consumer retries X times.
4.  If still failing, move message to DLQ for manual inspection later.

**Code Snippet:**
```java
// RabbitMQ Listener with DLQ
@RabbitListener(queues = "orders")
public void process(Order order) {
    try {
        save(order);
    } catch (Exception e) {
        throw new AmqpRejectAndDontRequeueException(e); // Sends to DLQ configured in arguments
    }
}
```

---

## 222. How do you manage service versioning?

**Answer:**
Managing changes in service APIs without breaking consumers.
-   **Semantic Versioning:** Major.Minor.Patch (e.g., 2.1.0).
    -   **Major:** Breaking changes.
    -   **Minor:** New features, backward compatible.
    -   **Patch:** Bug fixes.
-   **Strategy:** Run multiple versions simultaneously (`v1` and `v2`) until all clients migrate to `v2`.

**Code Snippet:**
```yaml
# Helm Chart / Kubernetes
image: my-service:v1.0.0
# vs
image: my-service:v2.0.0
```

---

## 223. How to maintain backward compatibility?

**Answer:**
**Backward Compatibility** means newer versions of the service can still be used by older clients.
-   **Rule 1:** Never remove a field from DTOs. Mark it as `@Deprecated`.
-   **Rule 2:** Never change the type of a field (e.g., String to Int).
-   **Rule 3:** When adding a new mandatory field, provide a default value so old clients (who don't send it) don't break.
-   **Consumer-Driven Contracts (Pact):** Use tests to ensure you don't break consumers.

**Code Snippet:**
```java
class UserDTO {
    String name;
    @Deprecated
    String fullname; // Keep for old clients
}
```

---

## 224. How do you deploy multiple microservices together?

**Answer:**
Ideally, microservices should be deployed **independently**.
-   **CI/CD Pipeline:** Each service has its own git repo and its own pipeline (Build -> Test -> Docker Build -> Deploy).
-   **Orchestrator:** Kubernetes (or Docker Swarm) manages the deployment.
-   If you *must* deploy together (e.g., breaking change across A and B), use **Helm Charts** to package `v2` of Service A and `v2` of Service B as a release.

**Code Snippet:**
```yaml
# helm install my-stack ./chart
dependencies:
  - name: service-a
    version: 2.0.0
  - name: service-b
    version: 2.0.0
```

---

## 225. What is Blue-Green Deployment?

**Answer:**
A deployment strategy that reduces downtime and risk.
1.  **Blue (Live):** The current running version receiving 100% traffic.
2.  **Green (Idle):** Deploy the new version here. Test it.
3.  **Switch:** Once Green is verified, switch the Router/Load Balancer to send 100% traffic to Green.
4.  **Rollback:** If issues found, switch router back to Blue instantly.

**Code Snippet:**
```text
[ Router ] ----> [ Blue (v1) ] (Active)
           |
           ----> [ Green (v2) ] (Testing)
```

---

## 226. What is Canary Deployment?

**Answer:**
A strategy to release a new version to a small subset of users first.
1.  Deploy new version (Canary).
2.  Route **1%** or **5%** of traffic to Canary.
3.  Monitor metrics (Error rate, Latency).
4.  If good, gradually increase traffic (10% -> 50% -> 100%).
5.  If bad, rollback (0%).

**Code Snippet:**
```yaml
# Istio VirtualService
route:
- destination:
    host: my-service
    subset: v1
  weight: 95
- destination:
    host: my-service
    subset: v2
  weight: 5
```

---

## 227. How to rollback a faulty microservice?

**Answer:**
In a containerized environment (Kubernetes), rolling back is re-deploying the previous Docker Image tag.
-   **Command:** `kubectl rollout undo deployment/my-service`.
-   **Database:** If the failed version migrated the DB, rolling back code might break.
    -   *Best Practice:* DB changes should be backward compatible (expand-contract pattern).

**Code Snippet:**
```bash
# Kubernetes Rollback
kubectl rollout undo deployment/user-service --to-revision=2
```

---

## 228. What are common microservices pitfalls?

**Answer:**
Most common reasons why microservice projects fail:
1.  **Too Granular:** Creating a service for every function ("Nanoservices"). Overhead > Benefit.
2.  **Shared Database:** Breaking the encapsulation rule. Tightly couples services.
3.  **Distributed Monolith:** Services that must be deployed together or depend synchronously on each other.
4.  **Lack of Monitoring:** Flying blind.

**Code Snippet:**
```text
Pitfall:
Service A calls Service B calls Service C calls Service D.
(Latency explodes, Availability drops).
```

---

## 229. How would you refactor a monolith into microservices?

**Answer:**
Strategy: **Strangler Fig Pattern**.
-   Do not rewrite the whole monolith from scratch (Big Bang).
-   **Implementation:**
    1.  Put a Proxy/Gateway in front of the Monolith.
    2.  Identify one bounded context (e.g., "Notifications").
    3.  Build a new Microservice for "Notifications".
    4.  Update Proxy to route "Notification" traffic to the new service.
    5.  Repeat until Monolith is gone (strangled).

**Code Snippet:**
```text
Proxy Rules:
/users -> Monolith
/orders -> Monolith
/notifications -> New Service
```

---

## 230. What is a shared library in microservices?

**Answer:**
Code shared across services (packed as a JAR).
-   **Good for:** Cross-cutting concerns (Logging utils, String utils, common Exceptions).
-   **Bad for:** Domain logic (DTOs, Entities).
-   **Risk:** If you change the shared library, you couple all services. You force them to upgrade the library version together (Dependency Hell).

**Code Snippet:**
```xml
<!-- Common Utils (Safe) -->
<dependency>
    <groupId>com.company</groupId>
    <artifactId>common-logging</artifactId>
</dependency>
```

---

## 231. What is API Composition?

**Answer:**
**API Composition** is a pattern used to retrieve data from multiple microservices and aggregate it.
-   **Problem:** Client needs data from `UserService`, `OrderService`, and `ReviewService` for a single dashboard screen.
-   **Optimized Solution:** Instead of the Client making 3 round-trip calls, an **API Gateway** or a dedicated **Composite Service** makes the 3 calls (in parallel) and returns a single JSON.

**Code Snippet:**
```java
// API Composition in aggregator
CompletableFuture<User> user = userService.getUser(id);
CompletableFuture<List<Order>> orders = orderService.getOrders(id);
CompletableFuture.allOf(user, orders).join();
return new DashboardDTO(user.get(), orders.get());
```

---

## 232. What is service granularity?

**Answer:**
**Granularity** refers to the scope of functionality a service covers.
-   **Coarse-Grained:** Large services (e.g., "E-commerce Service"). Close to Monolith.
-   **Fine-Grained:** Very small services (e.g., "Tax Calculation Service").
-   **Right Granularity:** Aligns with a **Boolean Context** and team size. "Can a small team (Two-Pizza team) maintain and deploy it independently?"

**Code Snippet:**
```text
Examples:
- "Customer Service": Good (Handles Profile, Address).
- "Customer Name Update Service": Too Fine (Anemic).
```

---

## 233. How do you manage dependencies between microservices?

**Answer:**
-   **Avoid Cyclic Dependencies:** A -> B -> A. (Bad. Merge them).
-   **Minimize Synchronous calls:** Use Events (Async) where possible to decouple availability.
-   **Shared Libraries:** Only for util code, never for domain logic.
-   **Contract Tests (Pact):** To ensure API changes in Producer don't break Consumer.

**Code Snippet:**
```text
Dependencies Graph:
Service A (Producer) --> (Contract) --> Service B (Consumer)
```

---

## 234. How to test microservices independently?

**Answer:**
You cannot spin up the whole world (100 services) to test 1 service.
-   **Unit Tests:** Mock all classes.
-   **Integration Tests:** Use H2/TestContainers for DB. Mock external HTTP calls using **WireMock**.
-   **Contract Tests:** Verify that your mocks match the reality of the external service.

**Code Snippet:**
```java
// Mocking External Service B with WireMock
stubFor(get("/api/v1/data").willReturn(okJson("{\"data\": 123}")));
```

---

## 235. What is consumer-driven contract testing?

**Answer:**
A testing methodology where the **Consumer** (Client) defines what it needs from the **Producer** (Server).
-   **Workflow:**
    1.  Consumer defines a "Contract" (Expected Request/Response).
    2.  Consumer runs tests against this Contract (using a mock generated from it).
    3.  Producer runs tests against the *same* Contract to verify it fulfills it.
-   **Tools:** Pact, Spring Cloud Contract.

**Code Snippet:**
```json
// The Contract (Pact JSON)
"request": { "method": "GET", "path": "/user/1" },
"response": { "status": 200, "body": { "id": 1, "name": "Alice" } }
```

---

## 236. What is Pact and how does it work?

**Answer:**
**Pact** is a code-first tool for Consumer-Driven Contract testing.
1.  **Consumer Side:** Write a unit test using Pact DSL. Running it generates a `.json` Pact file.
2.  **Pact Broker:** Upload the file to a central server (Pact Broker).
3.  **Producer Side:** The build pipeline downloads the Pact file and replays the requests against the running Provider service to verify compatibility.

**Code Snippet:**
```java
// Consumer Test
builder
    .given("User 1 exists")
    .uponReceiving("Get User")
    .path("/users/1")
    .willRespondWith().status(200)
    .toPact();
```

---

## 237. How do you handle timeouts in microservices?

**Answer:**
Timeouts prevent a single slow service from blocking threads across the entire system.
-   **Connection Timeout:** Max time to establish TCP handshake. (e.g., 2s).
-   **Read Timeout:** Max time to wait for data after connection. (e.g., 5s).
-   **Global:** Use Resilience4j `TimeLimiter` or Ribbon/Feign config.
-   *Tip:* Always set timeouts shorter than the caller's timeout.

**Code Snippet:**
```yaml
# Feign Timeout
feign:
  client:
    config:
      default:
        connectTimeout: 2000
        readTimeout: 5000
```

---

## 238. What is asynchronous communication?

**Answer:**
Communication where the sender does not wait for a response.
-   **Pattern:** Fire-and-Forget or Publish-Subscribe.
-   **Tech:** Message Queues (RabbitMQ), Event Streams (Kafka).
-   **Pros:** Decoupling, Burst handling (Unprocessed messages wait in queue).
-   **Cons:** Complexity, Eventual Consistency.

**Code Snippet:**
```java
// Sender
rabbitTemplate.send("queue", message); // Returns immediately
```

---

## 239. When to use synchronous vs asynchronous communication?

**Answer:**
-   **Synchronous (REST/gRPC):**
    -   When the client *needs* the answer immediately to proceed (e.g., Login, Get Profile).
    -   Simple queries.
-   **Asynchronous (Messaging):**
    -   Long-running jobs (Generate PDF).
    -   Notifications (Email).
    -   Updates capable of being eventually consistent (e.g., Update search index capabilities after profile update).

**Code Snippet:**
```text
User Click "Buy" -> Sync (Validate payment) -> Async (Email, Shipping, Inventory)
```

---

## 240. What is eventual consistency vs strong consistency?

**Answer:**
-   **Strong Consistency:** Reads always return the latest write. (ACID, Monolith).
    -   *Cost:* High latency, lower availability (CAP Theorem).
-   **Eventual Consistency:** Reads *might* return stale data for a short time, but all nodes will eventually sync. (BASE, Microservices).
    -   *Benefit:* High Availability, Low Latency.
    -   *Real World:* ATM Balance might not show the check you deposited 1 second ago.

**Code Snippet:**
```text
Strong: Write A -> Lock -> Write B -> Unlock.
Eventual: Write A -> Ack -> Async Event -> Write B.
```

---

## 241. How to handle large payloads in microservices?

**Answer:**
Avoid passing large payloads (10MB+ JSON/XML) through the entire microservice chain (Gateway -> Service A -> Service B).
-   **Pattern:** **Claim Check Pattern**.
    1.  Service A receives the large payload.
    2.  Service A stores the payload in an external store (S3, Blob Storage, Redis).
    3.  Service A passes a reference ID ("Claim Check") to Service B.
    4.  Service B uses the ID to retrieve the payload from the store *if needed*.
-   **Compression:** Use GZIP encoded requests/responses.

**Code Snippet:**
```java
// Store Payload
String blobUrl = s3Client.upload(largeJson);
// Send Reference
messageQueue.send(new PayloadEvent(blobUrl));
```

---

## 242. How to implement file upload in a microservice?

**Answer:**
-   **Direct Upload (Best):** Client uploads directly to Cloud Storage (S3) using a **Presigned URL**. The microservice only handles the metadata (File Name, S3 Key).
-   **Through Service:** Use `MultipartFile` in Spring Boot.
    -   *Config:* Increase `spring.servlet.multipart.max-file-size`.
    -   *Stream:* Stream the input stream directly to storage to avoid loading the whole file into RAM (avoid OOM).

**Code Snippet:**
```java
@PostMapping("/upload")
public String upload(@RequestParam("file") MultipartFile file) {
    // Determine content type, generate key
    s3Service.putObject(bucket, key, file.getInputStream(), metadata);
    return key;
}
```

---

## 243. What is Throttling?

**Answer:**
**Throttling** is intentionally slowing down the processing rate of a service to match its capacity.
-   **Vs Rate Limiting:** Rate Limiting *rejects* requests (429) if limit exceeded. Throttling *queues* or *delays* them.
-   **Use Case:** A background job processing thousands of emails. If we send them all at once, the Email Provider bans us. We throttle to 50 emails/sec.

**Code Snippet:**
```java
// Guava RateLimiter (Throttles thread execution)
RateLimiter limiter = RateLimiter.create(5.0); // 5 tasks per second
for (Task task : tasks) {
    limiter.acquire(); // Blocks if rate exceeded
    executor.submit(task);
}
```

---

## 244. How do you scale a microservice?

**Answer:**
Scaling is adjusting capacity to handle load.
-   **X-Axis (Horizontal):** Run multiple copies (instances) of the service behind a Load Balancer. (Standard for stateless microservices).
-   **Y-Axis (Functional):** Split the service into smaller services (Decomposition).
-   **Z-Axis (Data Partitioning):** Sharding. Instance 1 handles Users A-M, Instance 2 handles N-Z.

**Code Snippet:**
```bash
# Kubernetes Horizontal Scaling
kubectl scale deployment/user-service --replicas=5
```

---

## 245. What is Horizontal vs Vertical Scaling?

**Answer:**
-   **Vertical Scaling (Scale Up):** Adding more power to the *existing* machine (Upgrade RAM 8GB -> 64GB, CPU 4 -> 32 Cores).
    -   *Limit:* Hardware limits. Downtime usually required.
    -   *Good for:* Monoliths, Databases.
-   **Horizontal Scaling (Scale Out):** Adding *more machines* (nodes) to the cluster.
    -   *Limit:* Theoretically infinite. No downtime.
    -   *Good for:* Microservices, Distributed Systems.

**Code Snippet:**
```text
Vertical:   [ Small Server ] -> [ HUGE SERVER ]
Horizontal: [ Server ] -> [ Server ] [ Server ] [ Server ]
```

---

## 246. What is Container Orchestration?

**Answer:**
Managing the lifecycle of containers (Docker) in a large distributed environment.
-   **Problems it solves:**
    -   **Scheduling:** Which server has 2GB RAM free for this container?
    -   **Resilience:** If a container crashes, restart it. If a Node dies, move containers elsewhere.
    -   **Scaling:** Auto-scale based on CPU usage.
    -   **Networking:** Service Discovery and Load Balancing between containers.
-   **Tools:** **Kubernetes (K8s)**, Docker Swarm, Apache Mesos.

**Code Snippet:**
```yaml
# K8s Deployment Descriptor (simplified)
kind: Deployment
spec:
  replicas: 3
  template:
    spec:
      containers:
      - name: app
        image: my-app:v1
```

---

## 247. How does Kubernetes support microservices?

**Answer:**
K8s provides native primitives that map perfectly to microservices patterns:
-   **Service:** Service Discovery + Load Balancing.
-   **Deployment:** Horizontal Scaling + Rolling Updates (Zero Downtime).
-   **ConfigMap/Secret:** Externalized Configuration.
-   **Ingress:** API Gateway / Edge Routing.
-   **Liveness/Readiness Probes:** Health Checks.

**Code Snippet:**
```text
Mapping:
Spring Boot App -> K8s Pod
application.yaml -> K8s ConfigMap
Eureka -> K8s Service (DNS)
Zuul -> K8s Ingress
```

---

## 248. What is the difference between Microservices and SOA?

**Answer:**
**SOA (Service Oriented Architecture)** is the predecessor to Microservices.
-   **SOA (Enterprise Scale):**
    -   Communication via **ESB (Enterprise Service Bus)** - a smart pipe with business logic (transformation, routing).
    -   Protocols: SOAP, XML.
    -   Shared Database often common.
-   **Microservices (Web Scale):**
    -   "Smart Endpoints and Dumb Pipes" (REST/HTTP). No complex ESB.
    -   Protocols: JSON, gRPC.
    -   **Database per Service**.
    -   Focus on **Decoupling** and **DevOps**.

**Code Snippet:**
```text
SOA:  [ Service A ] <--> [ Smart ESB (Logic) ] <--> [ Service B ]
Micro:[ Service A ] <--> [ Dumb Pipe (HTTP) ] <--> [ Service B ]
```

---

## 249. What is a Backend-For-Frontend (BFF) Pattern?

**Answer:**
A variation of the API Gateway pattern.
-   **Problem:** A Mobile App needs different data (less data, lightweight) than a Web Client (more data). A single "General Purpose API" pleases no one.
-   **Solution:** Create a specific Backend Service for each Frontend experience.
    -   `Mobile-BFF`: Aggregates data specifically for the iOS/Android app.
    -   `Web-BFF`: Aggregates data for the Desktop Browser.

**Code Snippet:**
```text
[ iOS App ] --> [ iOS BFF ] --> [ User Service ]
[ Web App ] --> [ Web BFF ] --> [ Order Service ]
```

---

## 250. What is the role of a Message Broker in microservices?

**Answer:**
A **Message Broker** (RabbitMQ, Kafka, ActiveMQ) acts as an intermediary for asynchronous communication.
-   **Decoupling:** Sender doesn't need to know if Receiver is online.
-   **Buffering:** If Consumer is slow, Broker holds messages in queue (Backpressure handling).
-   **Reliability:** Ensures message delivery (Ack/Nack) and persistence.
-   **Routing:** Fanout (Pub/Sub) to multiple consumers.

**Code Snippet:**
```text
Producer -> [ Exchange ] -> (Queue A) -> Consumer A
                         -> (Queue B) -> Consumer B
```

---

## 251. What are the best practices for microservice architecture?

**Answer:**
1.  **Single Responsibility:** One service = One Bounded Context.
2.  **Database Per Service:** No shared tables.
3.  **Async Communication:** Prefer Events over direct HTTP calls for decoupling.
4.  **Fail Fast:** Use Timeouts and Circuit Breakers.
5.  **Observability:** Centralized Logging, Tracing, and Metrics are non-negotiable.
6.  **Automation:** CI/CD for every service.
7.  **Consumer Driven Contracts:** Don't break clients.

**Code Snippet:**
```text
Checklist:
[x] Is it independently deployable?
[x] Does it own its data?
[x] Is it loosely coupled?
```

---

## 252. What is a Service Mesh used for?

**Answer:**
(See Q213).
A **Service Mesh** (Istio, Linkerd) manages the communication layer between services.
-   **Security:** Automatically encrypts traffic (mTLS) without code changes.
-   **Traffic Control:** Canary releases (send 5% traffic to v2), Retry logic, Rate Limiting.
-   **Observability:** Automatic tracing and metrics for every hop.

**Code Snippet:**
```yaml
# Istio mTLS Config (Enforces HTTPS between services)
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
spec:
  mtls:
    mode: STRICT
```

---

## 253. Explain the Ambassador pattern in microservices.

**Answer:**
The **Ambassador Pattern** creates a helper service that sends network requests on behalf of a consumer service or application.
-   **Role:** It acts as an out-of-process proxy co-located with the client.
-   **Responsibility:** Handles common client connectivity tasks: Routing, Logging, Circuit Breaking, Security (TLS).
-   **Analogy:** A diplomat (Ambassador) handles complex negotiations on behalf of a country, so the country doesn't deal with it directly.
-   *Note:* Often implemented as a Sidecar.

**Code Snippet:**
```text
[ App Container ] --> [ Ambassador Container (Proxy) ] --> [ External Service ]
(App talks to localhost, Ambassador talks to world)
```

---

## 254. What are the 12 Factors of Microservices?

**Answer:**
The **12-Factor App** methodology is a set of guidelines for building portable, scalable SaaS apps. Key factors:
1.  **Codebase:** One repo per service, many deploys.
2.  **Dependencies:** Explicitly declare (Maven/Gradle).
3.  **Config:** Store config in the environment (Env Vars), not code.
4.  **Backing Services:** Treat DB/Queue as attached resources.
5.  **Build, Release, Run:** Strictly separate stages.
6.  **Processes:** Execute the app as one or more stateless processes.
7.  **Port Binding:** Export services via port binding (e.g., 8080).
8.  **Concurrency:** Scale out via process model.
9.  **Disposability:** Fast startup and graceful shutdown.
10. **Dev/Prod Parity:** Keep them similar.
11. **Logs:** Treat logs as event streams (stdout).
12. **Admin Processes:** Run admin/management tasks as one-off processes.

**Code Snippet:**
```bash
# Factor 3: Config in Env
export JDBC_URL=jdbc:mysql://prod-db:3306/mydb
java -jar myapp.jar
```

---

## 255. What is Polyglot Persistence?

**Answer:**
Using different data storage technologies to handle different data storage needs within the same system.
-   **Concept:** "Use the right tool for the job."
-   **Examples:**
    -   **RDBMS (MySQL):** For transactional data (Orders, Payments).
    -   **NoSQL (MongoDB):** For flexible documents (Product Catalog).
    -   **Key-Value (Redis):** For caching and sessions.
    -   **Search (Elasticsearch):** For full-text search.
    -   **Graph (Neo4j):** For social networks/recommendations.

**Code Snippet:**
```text
Architecture:
OrderService -> MySQL
CatalogService -> MongoDB
ReviewService -> Cassandra
```

---

## 256. What is observability and why is it critical?

**Answer:**
(See Q217).
**Observability** is the measure of how well internal states of a system can be inferred from knowledge of its external outputs. in Microservices, it is critical because:
-   **Complexity:** You have 50 services. You can't guess where the error is.
-   **Distributed nature:** A failure in A might cause an error in Z.
-   **Components:** Logs, Metrics, Traces.

**Code Snippet:**
```text
"Monitoring tells you when you have a problem. Observability lets you understand *why*."
```

---

## 257. How do you ensure microservices are resilient?

**Answer:**
Resilience is the ability to recover from failures and continue functioning.
1.  **Redundancy:** Run multiple instances of every service.
2.  **Circuit Breakers:** Prevent cascading failures.
3.  **Timeouts:** Fail fast.
4.  **Retries:** Handle transient network blips.
5.  **Bulkheads:** Partition resources (Threads/Connections) so one failure doesn't sink the ship.
6.  **Rate Limiting:** Protect against load spikes.

**Code Snippet:**
```java
// Resilience4j Decorator
@CircuitBreaker(name = "backendA")
@Bulkhead(name = "backendA")
@Retry(name = "backendA")
public String doSomething() { ... }
```

---

## 258. What is the difference between telemetry, tracing, and logging?

**Answer:**
-   **Telemetry:** The overarching term for all data collected from the system (Metrics, Traces, Logs).
-   **Logging:** Discrete events. "Something happened at Time T". (e.g., "Error: NullPointer").
-   **Tracing:** The journey of a request. "Request X went from A -> B -> C and took 200ms".
-   **Metrics:** Aggregated data. "Average latency is 50ms".

**Code Snippet:**
```text
Log:   2023-10-01 12:00:00 ERROR [OrderService] Payment Failed.
Trace: [Gateway -> OrderService -> PaymentService (X)]
Metric: payment.failure_rate = 5%
```

---

## 259. What is Shadow Traffic?

**Answer:**
A testing technique where production traffic is duplicated (mirrored) and sent to a new version of the service (Shadow) **without** affecting the real response to the user.
-   **Purpose:** Test the new version with *real* data and *real* load without risk.
-   **Analysis:** Compare the response of Live vs Shadow version (e.g., did Shadow throw an error? Was it slower?).
-   **Tools:** Istio Mirroring, AWS VPC Traffic Mirroring.

**Code Snippet:**
```yaml
# Istio Mirroring
route:
- destination:
    host: v1 (Live)
  weight: 100
mirror:
  host: v2 (Shadow)
```

---

## 260. How do you handle API deprecation in microservices?

**Answer:**
You cannot just delete an endpoint (it breaks clients).
1.  **Mark Deprecated:** Add `@Deprecated` and a `Warning` header to the response (`Warning: 299 - "This API is deprecated. Use v2"`).
2.  **Communication:** Inform consumers (Teams/Partners).
3.  **Sunset Period:** Monitor usage via metrics ("Who is still calling v1?").
4.  **Brownout:** Intentionally fail 1% of requests to get attention.
5.  **Shutdown:** Remove the code.

**Code Snippet:**
```java
@Deprecated
@GetMapping("/v1/users")
public ResponseEntity<User> getUser() {
    return ResponseEntity.ok()
        .header("Warning", "Deprecated. Use /v2/users")
        .body(service.get());
}
```


---

## 261. How do you build a Microservice SDK?

**Answer:**
A **Microservice SDK** is a client library that the producer service provides to its consumers to simplify integration.
-   **Structure:**
    1.  **API Module:** Contains DTOs and Interfaces (Contacts).
    2.  **Client Module:** Contains `FeignClient` or `WebClient` implementation.
-   **Distribution:** Published to Artifactory/Nexus as a JAR.
-   **Usage:** Consumers add the JAR as a dependency and just `@Autowire` the client interface.

**Code Snippet:**
```java
// Producer provides this interface in a JAR
@FeignClient(name = "user-service")
public interface UserClient {
    @GetMapping("/users/{id}")
    UserDTO getUser(@PathVariable("id") Long id);
}
```

---

## 262. What is the difference between REST and gRPC?

**Answer:**
-   **REST (Representational State Transfer):**
    -   Protocol: HTTP/1.1 (Text-based JSON).
    -   Pros: Human readable, ubiquitous tooling (Browser, Postman).
    -   Cons: Verbose (Headers, JSON syntax overhead), slower.
-   **gRPC (Google Remote Procedure Call):**
    -   Protocol: HTTP/2 (Binary - Protobuf).
    -   Pros: Extremely fast, compact, supports streaming (Bi-directional), strongly typed contracts (`.proto`).
    -   Cons: Not browser-friendly (requires gRPC-Web), harder to debug.

**Code Snippet:**
```protobuf
// gRPC .proto file
service UserService {
  rpc GetUser (UserRequest) returns (UserResponse);
}
```

---

## 263. How do you integrate GraphQL in microservices?

**Answer:**
**GraphQL** allows clients to request exactly the data they need.
-   **Architecture:** Usually implemented in the **API Gateway** or a dedicated "Graph Level".
-   **Federation (Apollo):** Each microservice exposes a subgraph (its own piece of the schema). The Gateway stitches them together into one Supergraph.
-   **N+1 Problem:** Be careful of fetching lists where each item triggers a call to another service. Use **DataLoaders** (Batching) to solve this.

**Code Snippet:**
```graphql
type Query {
  user(id: ID): User # Fetched from User Service
  orders(userId: ID): [Order] # Fetched from Order Service
}
```

---

## 264. What is a lightweight vs heavyweight service?

**Answer:**
-   **Lightweight:**
    -   Fast startup (<1s), Low memory footprint (<100MB).
    -   Tech: Go, Node.js, Rust, GraalVM Native Image.
    -   Use: Sidecars, Serverless functions, simple CRUD.
-   **Heavyweight:**
    -   Slower startup (5-20s), Higher memory (500MB+).
    -   Tech: Traditional Java (Spring Boot + JVM), .NET.
    -   Use: Complex Domain Logic, Enterprise Integration.

**Code Snippet:**
```text
Comparison:
Node.js "Hello World": 15MB RAM.
Spring Boot "Hello World": 300MB RAM.
(Note: Spring Native aims to bridge this gap).
```

---

## 265. What is Head-of-Line Blocking?

**Answer:**
A performance issue where a line of packets is held up by the first packet.
-   **Context (HTTP/1.1):** Browsers open limited connections (e.g., 6) to a server. If one request takes 5 seconds, that connection is blocked for 5 seconds. Other requests wait in queue behind it.
-   **Context (Switching):** One packet dropped causes the receiver to wait, blocking subsequent packets.
-   **Solution:** **HTTP/2** (Multiplexing) allows sending multiple requests/responses in parallel over a single TCP connection.

**Code Snippet:**
```text
HTTP/1.1: [Req 1] (Wait) [Resp 1] [Req 2] ...
HTTP/2:   [Req 1] [Req 2] [Req 3] ... (Mixed stream)
```

---

## 266. What is a Correlation ID and how is it useful?

**Answer:**
(See Q220).
A unique identifier (UUID) attached to a request when it first enters the system (e.g., at the Load Balancer/Gateway).
-   **Propagation:** It is passed to every downstream service in HTTP Headers (`X-Correlation-ID` or `Trace-ID`).
-   **Logging:** Every log statement includes this ID.
-   **Benefit:** Provides a "Thread" to stitch together logs from 10 different services to debug a single user request.

**Code Snippet:**
```java
// MDC (Mapped Diagnostic Context)
MDC.put("correlationId", headerId);
logger.info("Processing..."); 
// Log: [2023-10-01] [main] [a1b2c3d4] Processing...
```

---

## 267. How to design authentication in a microservice ecosystem?

**Answer:**
Strategy: **Centralized Auth, Distributed Enforcement**.
1.  **Auth Service (Identity Provider):** Handles Login, Database of users, Issues Tokens (JWT).
2.  **API Gateway:** Validates the Token signature. Can create a "Principal" object.
3.  **Microservices:** Stateless. They trust the Gateway (or validate the JWT signature themselves using the Public Key). They don't check the DB for credentials.

**Code Snippet:**
```text
User -> [ Gateway (Validate JWT) ] -> [ Service A (@PreAuthorize) ]
                                   -> [ Service B ]
```

---

## 268. What is the Strangler Pattern in microservices migration?

**Answer:**
(See Q229).
A pattern to incrementally migrate a legacy system by gradually replacing specific pieces of functionality with new microservices and applications.
-   The "Strangler Fig" wraps around the old tree (Monolith) and eventually replaces it.
-   **Mechanism:** An **Intercepting Facade** (Proxy) routes traffic away from the Monolith to the new service for migrated features.

**Code Snippet:**
```text
Timeline:
Month 1: 100% Monolith.
Month 2: 90% Monolith, 10% Microservices (New Features).
Month 12: 10% Monolith (Legacy Read-only), 90% Microservices.
```

---

## 269. Explain real-world microservice monitoring setup using Spring Boot + Sleuth + Zipkin + Prometheus + Grafana.

**Answer:**
Data Flow Architecture:
1.  **Spring Boot App:**
    -   Runs logic.
    -   `Sleuth`: Intercepts calls, adds Trace IDs to MDC.
    -   `Micrometer`: Collects metrics (JVM, HTTP latency).
2.  **Expose:**
    -   Logs -> Filebeat (Sidecar) -> Logstash -> Elastic.
    -   Trace Spans -> Zipkin Server (via HTTP/RabbitMQ).
    -   Metrics -> `/actuator/prometheus` endpoint.
3.  **Harvest:**
    -   `Prometheus` Server scrapes the endpoint every 15s.
4.  **Visualize:**
    -   `Grafana` queries Prometheus to show Dashboard.
    -   Zipkin UI shows waterfalls.

**Code Snippet:**
```yaml
# Prometheus Job
- job_name: 'microservices'
  eureka_sd_configs: # Discovers ALL services from Eureka
  - server: http://eureka:8761/eureka
```

---

## 270. What is the difference between WHERE and HAVING?

**Answer:**
Both filter results, but at different times.
-   **WHERE:** Filters rows **before** aggregation (GROUP BY). It acts on individual records.
-   **HAVING:** Filters groups **after** aggregation. It acts on the result of functions like `SUM()`, `COUNT()`.

**Code Snippet:**
```sql
-- Find departments with total salary > 100k
SELECT dept, SUM(salary) 
FROM employees
WHERE active = true      -- Filter Row (only active employees)
GROUP BY dept
HAVING SUM(salary) > 100000; -- Filter Group (aggregated sum)
```

---

## 271. What is Indexing? How does it improve performance?

**Answer:**
**Indexing** creates a data structure (B-Tree, Hash, B+Tree) that sorts and stores the values of specific columns, allowing the database to find rows without scanning the entire table (Table Scan).
-   **Without Index:** Database reads every row (O(N)).
-   **With Index:** Database traverses a B-Tree (O(log N)).
-   **Trade-off:** Indexes speed up Reads (SELECT) but slow down Writes (INSERT/UPDATE), because the index structure must be updated on every write.

**Code Snippet:**
```sql
CREATE INDEX idx_user_email ON users(email);
-- SELECT * FROM users WHERE email = '...' becomes instantaneous.
```

---

## 272. What is a Composite Index?

**Answer:**
An index on **multiple columns**.
-   **Usage:** When you frequently query by multiple columns together (e.g., `WHERE firstname = 'John' AND lastname = 'Doe'`).
-   **Leftmost Prefix Rule:** A composite index `(A, B, C)` aids queries on:
    -   `A`
    -   `A, B`
    -   `A, B, C`
    -   It does **NOT** aid queries on `B` or `C` alone.

**Code Snippet:**
```sql
CREATE INDEX idx_name ON users(lastname, firstname);
-- Good: WHERE lastname='Doe'
-- Good: WHERE lastname='Doe' AND firstname='John'
-- Bad:  WHERE firstname='John' (Index not used)
```

---

## 273. What are Clustered and Non-Clustered Indexes?

**Answer:**
-   **Clustered Index:**
    -   Determines the **physical order** of data on the disk.
    -   A table can have only **one** clustered index (usually the Primary Key).
    -   The leaf nodes contain the actual row data.
-   **Non-Clustered Index:**
    -   Stored separately from the data.
    -   Contains the indexed column value and a pointer (Bookmark/RID) to the actual row in the clustered index.
    -   A table can have many non-clustered indexes.

**Code Snippet:**
```text
Clustered (PK):  [ID=1, Data] [ID=2, Data] [ID=3, Data] (Sorted by ID)
Non-Clustered:   [Name="Alice", Ptr=1] [Name="Bob", Ptr=3]
```

---

## 274. What is Normalization? Types?

**Answer:**
**Normalization** is the process of organizing data to reduce **Redundancy** and improve **Data Integrity**.
-   **1NF:** Atomic values (No lists/arrays in a cell), unique rows.
-   **2NF:** 1NF + No Partial Dependency (All non-key columns depend on the *whole* primary key).
-   **3NF:** 2NF + No Transitive Dependency (Non-key columns depend *only* on the PK, not on other non-key columns). "The Key, the whole Key, and nothing but the Key".

**Code Snippet:**
```text
Un-normalized: [Student, Course, Instructor, Instructor_Office]
3NF Split:
1. Students
2. Courses
3. Instructors (Link Office here)
4. Enrollments (Link Student & Course)
```

---

## 275. What is Denormalization?

**Answer:**
The process of adding redundancy back into the schema (e.g., combining tables) to improve **Read Performance**.
-   **Why:** Joins are expensive. If you always need `User` + `Address` together, joining them 1 million times is slow. Storing `Address` inside the `User` table (or document) eliminates the join.
-   **Cost:** Updates are slower and harder (Performance vs Integrity trade-off). You must update data in multiple places.

**Code Snippet:**
```json
// Denormalized (NoSQL style or JSON standard in SQL)
{
  "id": 1,
  "name": "Alice",
  "address": { "city": "NY", "zip": "10001" } // Embedded
}
```

---

## 276. What is ACID Property?

**Answer:**
Properties that guarantee database transactions are processed reliably.
-   **Atomicity:** All or Nothing. If one part fails, everything rolls back.
-   **Consistency:** Database goes from one valid state to another (Constraints enforced).
-   **Isolation:** Concurrent transactions don't interfere with each other (see Isolation Levels).
-   **Durability:** Once committed, data is saved permanently (even if power fails).

**Code Snippet:**
```sql
BEGIN TRANSACTION;
  UPDATE account SET balance = balance - 100 WHERE id = A;
  UPDATE account SET balance = balance + 100 WHERE id = B;
COMMIT; -- All happen, or none happen.
```

---

## 277. What is the difference between TRUNCATE, DELETE and DROP?

**Answer:**
-   **DELETE:** DML command. Deletes rows one by one. Can have `WHERE` clause. Slower. Logs every deletion (can rollout).
-   **TRUNCATE:** DDL command. Resets high-water mark. Deletes all data instantly. Cannot use `WHERE`. Cannot rollback (in some DBs). Faster.
-   **DROP:** DDL command. Deletes the data **and** the table structure/schema.

**Code Snippet:**
```sql
DELETE FROM users WHERE id = 1; -- Specific row
TRUNCATE TABLE users;           -- Empty table, keep structure
DROP TABLE users;               -- Destroy table
```

---

## 278. What are Window Functions? Examples?

**Answer:**
Functions that perform calculations across a set of table rows that are related to the current row. Unlike `GROUP BY`, they **do not collapse** rows.
-   **Common Functions:** `RANK()`, `DENSE_RANK()`, `ROW_NUMBER()`, `LEAD()`, `LAG()`.
-   **Syntax:** `FUNC() OVER (PARTITION BY ... ORDER BY ...)`

**Code Snippet:**
```sql
-- Rank employees by salary within their department
SELECT name, dept, salary,
       RANK() OVER (PARTITION BY dept ORDER BY salary DESC) as rank
FROM employees;
-- Result:
-- Bob, Sales, 5000, 1
-- Alice, Sales, 4000, 2
```

---

## 279. What is CTE?

**Answer:**
**CTE (Common Table Expression)** is a temporary result set (named temporary table) that exists only for the duration of a single query.
-   **Syntax:** `WITH cte_name AS (...)`
-   **Benefit:** Makes complex queries (with multiple sub-queries) readable.
-   **Recursive CTE:** Used for hierarchical data (e.g., Org Chart, Folder Structure).

**Code Snippet:**
```sql
WITH HighEarners AS (
    SELECT * FROM employees WHERE salary > 100000
)
SELECT * FROM HighEarners JOIN departments ...
```

---

## 280. How does GROUP BY work internally?

**Answer:**
1.  **Scanning:** The database scans the table (or index).
2.  **Sorting/Hashing:** It groups the rows based on the `GROUP BY` columns using a Sort algorithm or a Hash Table.
3.  **Aggregation:** It runs the aggregate function (`SUM`, `COUNT`) on each group.
4.  **Filtering:** It applies `HAVING` filters to remove unwanted groups.
-   *Performance Tip:* Indexing the `GROUP BY` column allows the DB to skip the Sorting step (results are already sorted by index).

**Code Snippet:**
```sql
SELECT city, COUNT(*) FROM users GROUP BY city;
-- Internal: Hash Map { "NY": 50, "LA": 30 ... }
```

---

## 281. What is Query Optimization?

**Answer:**
The process of defining the most efficient way to execute a SQL query.
-   **Techniques:**
    1.  **Use Indexes:** Ensure WHERE/JOIN/ORDER BY columns are indexed.
    2.  **Avoid SELECT \*:** Fetch only needed columns.
    3.  **Avoid Functions on Indexed Columns:** `WHERE YEAR(date) = 2023` kills the index. Use `WHERE date BETWEEN '2023-01-01' AND '2023-12-31'`.
    4.  **Analyze Execution Plan:** Use `EXPLAIN` to see if a Full Table Scan is happening.

**Code Snippet:**
```sql
EXPLAIN SELECT name FROM users WHERE id = 1;
-- Output: type: const, key: PRIMARY (Good)
```

---

## 282. How to analyze Slow Queries?

**Answer:**
1.  **Enable Slow Query Log:** Configure DB (e.g., MySQL `long_query_time = 2`) to log queries taking > 2 seconds.
2.  **Identify:** Pick the top offenders from the log.
3.  **EXPLAIN:** Run `EXPLAIN` on the query to see the plan.
    -   Look for `type: ALL` (Full Table Scan).
    -   Look for `Using filesort` (Sorting in memory/disk instead of index).
4.  **Optimize:** Add missing indexes or rewrite query.

**Code Snippet:**
```sql
-- Check MySQL Slow Log status
SHOW VARIABLES LIKE 'slow_query_log';
```

---

## 283. What is a Transaction Isolation Level?

**Answer:**
Defines how visible changes made by one transaction are to others.
1.  **Read Uncommitted:** Can read dirty data (uncommitted changes). Lowest isolation, highest performance. Problem: Dirty Reads.
2.  **Read Committed:** Can only read committed data. Problem: Non-repeatable reads. (Default in Postgres/Oracle).
3.  **Repeatable Read:** Ensures if you read a row twice, you get the same result. Problem: Phantom Reads (New rows appearing). (Default in MySQL).
4.  **Serializable:** Strict serial execution. Slowest. No concurrency issues.

**Code Snippet:**
```sql
SET TRANSACTION ISOLATION LEVEL SERIALIZABLE;
BEGIN; ... COMMIT;
```

---

## 284. Explain Deadlocks in SQL and how to resolve.

**Answer:**
A **Deadlock** happens when two transactions block each other, each waiting for a resource the other holds.
-   **Scenario:**
    -   Tx1: Locks Row A, wants Row B.
    -   Tx2: Locks Row B, wants Row A.
    -   Result: Both wait forever.
-   **Resolution:**
    1.  **Ordering:** Always access resources in the same order (A then B).
    2.  **Timeout:** Configure lock timeouts.
    3.  **Retry:** Catch deadlock exception in application and retry.

**Code Snippet:**
```text
Error: Deadlock found when trying to get lock; try restarting transaction
```

---

## 285. What are Stored Procedures? Pros/Cons?

**Answer:**
Code (SQL + Logic) stored and executed inside the Database.
-   **Pros:**
    -   Performance: Pre-compiled, reduces network round-trips (send 1 command, execute 100 lines).
    -   Security: Granular access control.
-   **Cons:**
    -   hard to debug and version control compared to Java code.
    -   Business logic leaks into the DB (Vendor lock-in).
    -   Hard to scale (DB is harder to scale than App Server).

**Code Snippet:**
```sql
CREATE PROCEDURE GetUser(IN userId INT)
BEGIN
  SELECT * FROM users WHERE id = userId;
END;
-- Call: CALL GetUser(1);
```

---

## 286. How do you handle migrations in Production DB?

**Answer:**
Use database migration tools like **Flyway** or **Liquibase**.
-   **Concept:** Version control for your database schema.
-   **Workflow:**
    1.  Create script `V1__init.sql`.
    2.  Create script `V2__add_email.sql`.
    3.  App start -> Tool checks `schema_version` table.
    4.  It sees V2 is not applied -> Applies V2 -> Updates `schema_version`.
-   **Production:** Never run DDL manually in Prod. Let the tool do it (or generate a script for DBA).

**Code Snippet:**
```sql
-- V2__Add_Column.sql
ALTER TABLE users ADD COLUMN email VARCHAR(255);
```

---

## 287. How do ORMs like Hibernate work?

**Answer:**
**ORM (Object Relational Mapping)** maps Java Classes to DB Tables.
-   **Reflection:** It inspects your `@Entity` class.
-   **Mapping:** It reads `@Table`, `@Column`.
-   **Session:** Acts as a buffer (First Level Cache) between App and DB.
-   **Dirty Checking:** When you modify a Java object, Hibernate detects the change and automatically generates the `UPDATE` SQL upon commit.

**Code Snippet:**
```java
User user = session.get(User.class, 1);
user.setName("New Name"); 
// No explicit update() needed. Hibernate fires Update on commit.
```

---

## 288. What is Hibernate First-Level Cache?

**Answer:**
It is the cache associated with the **Session** object.
-   **Scope:** Transactional (Request). Live as long as the Session is open.
-   **Behavior:** If you request object ID=1 twice in the same session, Hibernate returns the same instance from memory (no 2nd DB Query).
-   **Mandatory:** It cannot be disabled.

**Code Snippet:**
```java
User u1 = session.get(User.class, 1); // Select
User u2 = session.get(User.class, 1); // Cache Hit
// u1 == u2 is true
```

---

## 289. What is the difference between save(), persist(), merge() and update()?

**Answer:**
-   **`save()`:** Hibernate specific. Returns the generated PK immediately.
-   **`persist()`:** JPA standard. Returns `void`. Might delay SQL until flush.
-   **`update()`:** Re-attaches a Detached object to the session. Errors if object with same ID already exists in session.
-   **`merge()`:** Copies the state of a Detached object into a Persistent object. Returns the new Persistent instance. Safest for updates.

**Code Snippet:**
```java
User detached = new User(1, "Old");
User managed = session.merge(detached); // managed is connected, detached is ignored
```

---

## 290. What is the difference between get() and load()?

**Answer:**
-   **`get()`:**
    -   Hits the database immediately.
    -   Returns `null` if not found.
    -   Use when you are not sure if the object exists.
-   **`load()`:**
    -   Returns a **Proxy** (fake object) immediately (Lazy).
    -   Hits DB only when you access a property (e.g., `proxy.getName()`).
    -   Throws `ObjectNotFoundException` if not found.
    -   Use when you only need the reference (e.g., to set a Foreign Key).

**Code Snippet:**
```java
User u = session.load(User.class, 1); // No SQL yet
order.setUser(u); // Sets FK, still no SQL needed for User
session.save(order);
```

---

## 291. What is Lazy Initialization Exception?

**Answer:**
**`LazyInitializationException`** occurs when you try to access a lazily loaded relationship (e.g., `user.getOrders()`) *after* the Hibernate Session has been closed.
-   **Cause:** The proxy object needs the Session to fetch the data from the DB. If the transaction committed and session closed, the proxy forces an error.
-   **Solutions:**
    1.  **Join Fetch:** Use `JOIN FETCH` up-front in the JPQL query to load data eagerly.
    2.  **EntityGraph:** Define a graph of attributes to fetch.
    3.  **Open Session In View (OSIV):** (Anti-pattern) Keep session open until view renders.

**Code Snippet:**
```java
// Fix with JPQL
@Query("SELECT u FROM User u JOIN FETCH u.orders WHERE u.id = :id")
User getUserWithOrders(Long id);
```

---

## 292. What is the purpose of @JoinColumn and @OneToMany?

**Answer:**
-   **`@OneToMany`:** Defines the logical relationship (One User has Many Orders).
-   **`@JoinColumn`:** Defines the **physical mapping** (Foreign Key column).
-   **MappedBy:** If `@JoinColumn` is missing on the `OneToMany` side, Hibernate creates a minimal link table. To avoid this and use the FK in the child table, use `mappedBy="user"` on the Parent side.

**Code Snippet:**
```java
// Parent
@OneToMany(mappedBy = "user") // Look at 'user' field in Order
List<Order> orders;

// Child
@ManyToOne
@JoinColumn(name = "user_id") // FK Column in Order Table
User user;
```

---

## 293. How to handle Orphan Removal?

**Answer:**
**Orphan Removal** ensures that if you remove a child entity from the parent's collection, it is implicitly deleted from the database.
-   **Without it:** Removing an order from `user.getOrders()` only sets `order.user_id = null`.
-   **With it:** Removing the order deletes the row from the `Order` table.
-   **Usage:** Good for dependent objects (Owner-based lifecycle).

**Code Snippet:**
```java
@OneToMany(mappedBy = "user", orphanRemoval = true, cascade = CascadeType.ALL)
List<Order> orders;

// Usage
user.getOrders().remove(order0); // Deletes order0 from DB
```

---

## 294. How does Hibernate manage object states?

**Answer:**
An Entity instance can be in one of 4 states:
1.  **Transient:** Just created (`new User()`). Not stored in DB, not associated with Session.
2.  **Persistent:** Associated with Session. Represents a row in DB. Changes are automatically saved (Dirty Checking).
3.  **Detached:** Was persistent, but Session closed. Changes are NOT saved unless re-attached (`merge/update`).
4.  **Removed:** Scheduled for deletion.

**Code Snippet:**
```java
User u = new User(); // Transient
session.save(u);     // Persistent
session.close();     // Detached
```

---

## 295. What are common Hibernate Performance Issues?

**Answer:**
1.  **N+1 Select Problem:** Fetching a list of N parents, then fetching children for each parent (1 + N queries). Fix: `JOIN FETCH`.
2.  **Cartesian Product:** Eager fetching multiple bags (Lists) creates M * N rows in memory. Fix: `Set` or multiple queries.
3.  **Missing Indexes:** Slow queries.
4.  **Too many flushes:** Using `flush()` incorrectly inside loops.
5.  **Fetching unnecessary columns:** Selecting full Entities when DTOs are enough.

**Code Snippet:**
```sql
-- N+1 Example
SELECT * FROM users; -- 1 Query
SELECT * FROM orders WHERE user_id = 1; -- N Queries
SELECT * FROM orders WHERE user_id = 2;
...
```

---

## 296. How does the Second-Level Cache work in Hibernate?

**Answer:**
-   **First Level (L1):** Session scoped. Default on.
-   **Second Level (L2):** **SessionFactory** scoped (Global). Shared across all sessions/users.
    -   **Provider:** Requires a provider like EhCache, Caffeine, or Redis.
    -   **Usage:** Useful for read-heavy, rarely-changing reference data (e.g., Countries, Categories).
    -   **Strategy:** Read-Only, Read-Write, Transactional.

**Code Snippet:**
```java
@Entity
@Cacheable
@Cache(usage = CacheConcurrencyStrategy.READ_ONLY)
public class Country { ... }
```

---

## 297. Difference between Criteria API and JPQL?

**Answer:**
-   **JPQL (Java Persistence Query Language):**
    -   String-based (e.g., `"SELECT u FROM User u"`).
    -   Pros: Readable, similar to SQL.
    -   Cons: Not Type-safe. Runtime errors if you misspell a field.
-   **Criteria API:**
    -   Programmatic, Java-based construction of queries.
    -   Pros: **Type-safe** (Compile time checks). Dynamic query building options.
    -   Cons: Verbose and complex syntax.

**Code Snippet:**
```java
// Criteria API
CriteriaBuilder cb = em.getCriteriaBuilder();
CriteriaQuery<User> q = cb.createQuery(User.class);
Root<User> c = q.from(User.class);
q.select(c).where(cb.equal(c.get("name"), "Alice"));
```

---

## 298. What is flush() and clear()?

**Answer:**
-   **`flush()`:** Forces Hibernate to execute the SQL statements (Sync memory to DB) immediately. It does *not* commit the transaction.
-   **`clear()`:** Detaches **all** objects from the Session. It clears the L1 cache.
-   **Use Case:** Batch processing. Insert 50 records -> Flush -> Clear (to free memory) -> Repeat.

**Code Snippet:**
```java
for (int i = 0; i < 10000; i++) {
    session.save(new User(i));
    if (i % 50 == 0) {
        session.flush();
        session.clear(); // Prevents OutOfMemoryError
    }
}
```

---

## 299. What is a natively generated ID vs sequence?

**Answer:**
Strategies for `@GeneratedValue`:
1.  **IDENTITY (Native):** Relies on auto-increment column (MySQL/SQL Server). Hibernate must execute `INSERT` immediately to get the ID. Disables Batch Inserts.
2.  **SEQUENCE:** Uses a DB Sequence (Postgres/Oracle). Hibernate fetches a block of IDs (e.g., 50) upfront. Allows Batch Inserts. Best performance.
3.  **TABLE:** Simulates a sequence using a table. Slow.

**Code Snippet:**
```java
@Id
@GeneratedValue(strategy = GenerationType.SEQUENCE, generator = "user_seq")
private Long id;
```

---

## 300. What is Optimistic Locking in JPA?

**Answer:**
A mechanism to prevent lost updates without locking the database row.
-   **Mechanism:** Adds a `@Version` column (number/timestamp).
-   **Flow:**
    1.  Read Row (Version = 1).
    2.  Update Row ... `WHERE id=X AND version=1`.
    3.  If DB reports 0 rows updated (because someone else updated it to v2), throw `OptimisticLockException`.
-   **Usage:** High concurrency, read-heavy systems.

**Code Snippet:**
```java
@Entity
public class Product {
    @Version
    private Integer version; // Automatically managed by Hibernate
}
```

---

## 301. How to implement Soft Delete in Hibernate?

**Answer:**
**Soft Delete** means marking a record as "deleted" (e.g., `deleted = true` or `status = 'INACTIVE'`) instead of physically removing the row from the database (Hard Delete).
-   **Implementation:**
    1.  Add a `deleted` column to the entity.
    2.  Use `@SQLDelete`: Overrides the default `DELETE` SQL with an `UPDATE`.
    3.  Use `@Where`: Adds a filter clause (`deleted = false`) to all SELECT queries for this entity.

**Code Snippet:**
```java
@Entity
@SQLDelete(sql = "UPDATE user SET deleted = true WHERE id = ?")
@Where(clause = "deleted = false")
public class User {
    @Id
    private Long id;
    private boolean deleted = false;
}
```

---

## 302. How does MongoDB store data?

**Answer:**
MongoDB is a **NoSQL Document Database**.
-   **Format:** Stores data in **BSON** (Binary JSON) format.
-   **Structure:**
    -   **Document:** A set of key-value pairs (like a JSON object). Schema-less (flexible).
    -   **Collection:** A group of documents (analogous to a Table).
    -   **Database:** A container for collections.

**Code Snippet:**
```json
// A MongoDB Document
{
  "_id": "507f1f77bcf86cd799439011",
  "name": "Alice",
  "age": 25,
  "address": { "city": "NY", "zip": "10001" },
  "hobbies": ["reading", "coding"]
}
```

---

## 303. Difference between MongoDB and MySQL?

**Answer:**
| Feature | MySQL (RDBMS) | MongoDB (NoSQL) |
| :--- | :--- | :--- |
| **Data Model** | Tables, Rows, Columns | Documents (BSON), Collections |
| **Schema** | Rigid (Must define upfront) | Flexible (schemaless) |
| **Relations** | Joins, Foreign Keys | Embedded Data, References (Manual join) |
| **Scaling** | Vertical (bigger server) | Horizontal (Sharding) |
| **Transactions** | ACID (Matuae) | ACID (Multi-document supported since v4.0) |
| **Query Language** | SQL | MQL (JSON-based) |

**Code Snippet:**
```text
MySQL: SELECT * FROM users WHERE age > 25;
Mongo: db.users.find({ age: { $gt: 25 } });
```

---

## 304. What are Documents and Collections?

**Answer:**
-   **Document:** The basic unit of data in MongoDB. Comparable to a **Row** in RDBMS. It supports nested structures (arrays/objects). Max size 16MB.
-   **Collection:** A grouping of documents. Comparable to a **Table** in RDBMS. Collections do not enforce a schema (documents in the same collection can have different fields).

**Code Snippet:**
```javascript
db.createCollection("products");
db.products.insertOne({ name: "Phone", price: 500 });
```

---

## 305. How to model One-to-Many relationship in MongoDB?

**Answer:**
Two patterns:
1.  **Embedding (Denormalization):** Good for "Contains" relationships where the child is not accessed independently. Fast reads.
    -   *Example:* User has many Addresses. Store addresses inside the User document.
2.  **Referencing (Normalization):** Good for "Has" relationships or when the "Many" side is very large (Unbounded).
    -   *Example:* User has many Posts. Store `userId` in the Post document.

**Code Snippet:**
```json
// Embedded
{ "name": "Alice", "addresses": [ { "city": "NY" }, { "city": "SF" } ] }

// Referenced
{ "_id": 1, "name": "Alice" }
{ "_id": 101, "title": "Post 1", "user_id": 1 }
```

---

## 306. What is Aggregation Framework in MongoDB?

**Answer:**
A pipeline-based framework for data processing and transformation (similar to SQL `GROUP BY` and `JOIN`).
-   **Pipeline:** Documents pass through stages. Each stage transforms the documents.
-   **Stages:**
    -   `$match`: Filter documents (WHERE).
    -   `$group`: Aggregate data (GROUP BY).
    -   `$project`: Select/Rename fields (SELECT).
    -   `$sort`: Order results.
    -   `$lookup`: Left Outer Join.

**Code Snippet:**
```javascript
db.orders.aggregate([
  { $match: { status: "A" } },
  { $group: { _id: "$cust_id", total: { $sum: "$amount" } } }
]);
```

---

## 307. What is Sharding?

**Answer:**
**Sharding** is the process of splitting data across multiple machines (Shards) to support huge data sets and high throughput.
-   **Mechanism:** Data is partitioned based on a **Shard Key** (e.g., `userId`).
-   **Architecture:**
    -   **Mongos (Router):** Routes queries to correct shard.
    -   **Config Server:** Stores metadata (which chunk is on which shard).
    -   **Shards:** Store actual data.

**Code Snippet:**
```text
Shard Key: ranges of user_id
Shard A: Users 1-1000
Shard B: Users 1001-2000
```

---

## 308. What are Indexes in MongoDB?

**Answer:**
Similar to SQL indexes, they improve query performance.
-   **Types:**
    -   **Single Field:** `db.users.createIndex({ age: 1 })`.
    -   **Compound:** `db.users.createIndex({ name: 1, age: -1 })`.
    -   **Multikey:** Index on array fields (indexes each element).
    -   **Text:** For text search.
    -   **TTL:** Automatically deletes documents after a time.

**Code Snippet:**
```javascript
// Scan only index, not collection
db.users.find({ age: 25 }).explain("executionStats");
```

---

## 309. How does Redis work?

**Answer:**
**Redis (Remote Dictionary Server)** is an in-memory Key-Value store.
-   **Speed:** Extremely fast (sub-millisecond) because data is stored in RAM, not Disk (though it can persist to disk).
-   **Data Structures:** Supports Strings, Lists, Sets, hashes, Sorted Sets (ZSets), Bitmaps, HyperLogLogs.
-   **Thread Model:** Single-threaded Event Loop (keeps it lock-free and simple).

**Code Snippet:**
```bash
SET user:1 "Alice"
GET user:1
INCR counter
```

---

## 310. What is TTL in Redis?

**Answer:**
**Time To Live (TTL)** is a feature to automatically expire (delete) a key after a specified time.
-   **Commands:**
    -   `EXPIRE key seconds`: Set TTL.
    -   `TTL key`: Check remaining time.
    -   `SETEX key seconds value`: Set value and TTL in one atomic op.
-   **Usage:** Caching (Session expiry, API Rate limiting).

**Code Snippet:**
```bash
SETEX session_token 3600 "xyz" # Expires in 1 hour
```

---

## 311. Difference between Redis and Memcached?

**Answer:**
Both are in-memory key-value stores, but Redis is a "Data Structure Store".
-   **Data Types:** Memcached only supports Strings. Redis supports Lists, Sets, Hashes, Sorted Sets, etc.
-   **Persistence:** Memcached is purely volatile (data lost on restart). Redis supports persistence (RDB/AOF).
-   **Replication:** Redis supports Master-Slave replication out of the box. Memcached does not.
-   **Thread Model:** Memcached is multi-threaded. Redis is single-threaded.

**Code Snippet:**
```text
Redis = Memcached + Data Structures + Persistence + Replication
```

---

## 312. What are common use cases of Redis?

**Answer:**
1.  **Caching:** Reduce DB load (most common).
2.  **Session Storage:** Store user sessions in a central place for microservices.
3.  **Leaderboards:** Use `Sorted Sets` (ZSET) for real-time ranking.
4.  **Pub/Sub:** Real-time messaging (Chat rooms).
5.  **Queues:** Use `List` as a Message Queue (Sidekiq/Celery use Redis).
6.  **Rate Limiting:** Counter with TTL.

**Code Snippet:**
```bash
# Leaderboard: Add score 100 for user 'alice'
ZADD leaderboard 100 "alice"
```

---

## 313. How to store sessions in Redis?

**Answer:**
In a distributed system (microservices), you cannot store sessions in the server's RAM (statelessness).
-   **Mechanism:**
    1.  User logs in.
    2.  Server generates a `SessionID` (UUID).
    3.  Server stores `SET session:UUID "{ userData }" EX 1800` in Redis.
    4.  Server sends `SessionID` as a Cookie to the browser.
    5.  Future requests send the Cookie. Server checks Redis.
-   **Spring Boot:** Use `spring-session-data-redis`. It automatically replaces `HttpSession` with Redis implementation.

**Code Snippet:**
```java
// Spring Boot Dependency
implementation 'org.springframework.session:spring-session-data-redis'
// No code change needed. HttpSession now uses Redis.
```

---

## 314. What is Persistence in Redis?

**Answer:**
Redis can save data to the disk to survive restarts.
1.  **RDB (Redis Database):** Snapshots at intervals (e.g., every 5 mins). Fast restores, but potential data loss of last 5 mins.
2.  **AOF (Append Only File):** Logs every write command. Slower restore, but higher durability (1 second data loss).
3.  **Hybrid:** Use both.

**Code Snippet:**
```text
Config:
save 60 1000  # Save RDB if 1000 keys changed in 60s
appendonly yes # Enable AOF
```

---

## 315. How does Redis Pub/Sub work?

**Answer:**
Allows messages to be broadcast to multiple consumers.
-   **Publisher:** Sends message to a `Channel`.
-   **Subscriber:** Listens to a `Channel`.
-   **Fire and Forget:** If no one is listening, the message is lost (unlike a Message Queue where it persists).

**Code Snippet:**
```bash
# Terminal 1 (Subscriber)
SUBSCRIBE my_channel

# Terminal 2 (Publisher)
PUBLISH my_channel "Hello World"
```

---

## 316. What are Redis Data Types?

**Answer:**
1.  **String:** Basic text/binary (Max 512MB).
2.  **List:** Linked List (Queue/Stack). `LPUSH`, `RPOP`.
3.  **Set:** Unique strings. `SADD`, `SISMEMBER`.
4.  **Hash:** Map of fields (Object). `HSET user:1 name "Alice"`.
5.  **Sorted Set (ZSet):** Unique strings ordered by a score. `ZADD`.
6.  **Bitmap:** Bit-level operations.

**Code Snippet:**
```bash
HSET user:100 name "John" age "30"
HGETALL user:100
```

---

## 317. How to avoid Cache Stampede?

**Answer:**
**Cache Stampede** (Thundering Herd) happens when a popular cache key expires, and hundreds of requests hit the DB simultaneously to recalculate it.
-   **Solutions:**
    1.  **Locking (Mutex):** Only let 1 request compute the value. Others wait.
    2.  **Probabilistic Early Expiration:** Expire the key locally in the app *before* the actual Redis TTL, using a random factor.
    3.  **Logical TTL:** Store the expiry time *inside* the value. Check it manually and refresh in background.

**Code Snippet:**
```java
// Pseudo-code for Mutex
val = cache.get(key);
if (val == null) {
  if (acquireLock(key)) {
     val = db.get(key);
     cache.set(key, val);
     releaseLock(key);
  } else {
     sleep(100); retry();
  }
}
```

---

## 318. How does Cache Eviction work in Redis?

**Answer:**
When Redis memory is full, it must remove keys to make room. Policy is defined by `maxmemory-policy`.
-   **noeviction:** Returns error on write (Default).
-   **allkeys-lru:** Removes Least Recently Used keys only.
-   **volatile-lru:** Removes LRU keys that have an expiry (TTL) set.
-   **allkeys-random:** Random removal.

**Code Snippet:**
```text
Config:
maxmemory 2gb
maxmemory-policy allkeys-lru
```

---

## 319. What is Write-Through vs Write-Behind Cache?

**Answer:**
-   **Write-Through:** App writes to Cache AND DB continuously.
    -   Pros: Data Consistency (Cache == DB).
    -   Cons: Slower writes (2 operations).
-   **Write-Behind (Write-Back):** App writes to Cache only. Cache async writes to DB later.
    -   Pros: Very fast writes.
    -   Cons: Data loss risk if Cache crashes before syncing.

**Code Snippet:**
```text
Write-Through: App -> [Cache + DB] (Synchronous)
Write-Behind:  App -> [Cache] ... (Async) ... -> [DB]
```

---

## 320. When would you use NoSQL over SQL?

**Answer:**
Use NoSQL when:
1.  **Flexible Schema:** Data structure changes frequently (e.g., Log data, User Profiles with dynamic fields).
2.  **High Scalability:** You need massive write throughput or horizontal scaling (Sharding) that RDBMS struggles with.
3.  **Specialized Data:**
    -   Hierarchical data (MongoDB).
    -   Graph data/Social networks (Neo4j).
    -   Fast Key-Value access (Redis).
    -   Time Series (InfluxDB).
4.  **No Complex Joins:** Your queries don't require complex relationships.

**Code Snippet:**
```text
Use SQL for: Financial Systems (ACID), ERP, CRM.
Use NoSQL for: IoT Data, Real-time Analytics, Content Management (CMS).
```
