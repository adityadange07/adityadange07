# Top 500 Java Backend Interview FAQs

### 1. Explain the difference between `==` and `.equals()` in Java.

*   **`==` Operator**: Checks for **reference equality**. It verifies if both references point to the *same object instance* in memory. For primitives (int, char, etc.), it compares actual values.
*   **`.equals()` Method**: Checks for **content equality**. It is a method (defined in `Object` class) intended to verify if the *state* or *data* of two objects is logically equivalent.
    *   *Note:* The default implementation of `.equals()` in the `Object` class behaves exactly like `==`. Classes like `String`, `Integer`, and reference types must override it to compare contents.

**Example:**
```java
String s1 = new String("HELLO");
String s2 = new String("HELLO");

System.out.println(s1 == s2);       // false (different memory addresses)
System.out.println(s1.equals(s2));  // true  (same content)
```

### 2. Why is String immutable in Java?

*   **String Pool Efficiency**: Immutability allows the JVM to save heap space by caching and reusing String literals in the **String Constant Pool**. If Strings were mutable, changing one reference to a literal would incorrectly affect all other references to that same literal.
*   **Security**: Strings are heavily used for parameters like database URLs, usernames, passwords, and file paths. Immutability ensures that these critical values cannot be changed (maliciously or accidentally) once created.
*   **Thread Safety**: Immutable objects are inherently thread-safe. They can be safely shared across multiple threads without any synchronization overhead.
*   **HashCode Caching**: Since the content cannot change, the hash code of a String is computed once and cached. This makes Strings highly performant as keys in `HashMap` or `HashSet`.

### 3. What is the difference between HashMap and ConcurrentHashMap?

*   **HashMap**: Not thread-safe and allows one null key. Fast for single-threaded applications but requires external synchronization in multi-threaded environments.
*   **ConcurrentHashMap**: Thread-safe implementation. Uses bucket-level locking (or CAS operations in newer versions) for writes, allowing concurrent reads without blocking. Does not allow null keys or values.

### 4. Explain the concept of fail-fast vs fail-safe iterators.

*   **Fail-Fast**: Iterators that throw a `ConcurrentModificationException` if the collection is structurally modified (add/remove) during iteration. They operate directly on the collection (e.g., ArrayList, HashMap iterators).
*   **Fail-Safe**: Iterators that do not throw exceptions if modified during iteration. They operate on a clone or snapshot of the collection (e.g., `ConcurrentHashMap`, `CopyOnWriteArrayList` iterators). They reflect a weakly consistent view.

### 5. What is the significance of hashCode() and equals() method?

*   **`equals()`**: Determines logical equality between two objects based on their content/state.
*   **`hashCode()`**: Returns an integer representation of the object, used for bucket placement in hash-based collections (HashMap, HashSet).
*   **Contract**: If `x.equals(y)` is true, `x.hashCode()` must equal `y.hashCode()`. Violating this breaks hash-based collections (e.g., retrieving objects from a Map).

### 6. How does ArrayList work internally?

*   **Backing Array**: Uses a dynamic array `Object[]` to store elements. Default initial capacity is 10.
*   **Resizing**: When the array becomes full, it creates a new array (typically 1.5x the size) and copies all elements from the old array to the new one.
*   **Access**: Provides O(1) random access because it uses array indexing.

### 7. What is the difference between ArrayList and LinkedList?

*   **Structure**: `ArrayList` uses a dynamic array; `LinkedList` uses a doubly linked list.
*   **Access**: `ArrayList` is faster (O(1)) for accessing elements (get/set). `LinkedList` is slower (O(n)) as it must traverse nodes.
*   **Modification**: `LinkedList` is faster (O(1)) for adding/removing elements (pointer updates), especially at the beginning/middle. `ArrayList` is slower (O(n)) because it requires shifting elements.

### 8. How does Java handle memory management?

*   **Stack Memory**: Stores primitive variables and method call frames. Memory is automatically allocated/deallocated with method execution (LIFO).
*   **Heap Memory**: Stores all objects (class instances) and arrays. Managed by Garbage Collector. Shared across all threads.
*   **Metaspace (Java 8+)**: Stores class metadata, static variables, and method codes (replacing PermGen). Located in native memory.

### 9. What is the role of the final keyword?

*   **final variable**: Creates a constant; its value cannot be changed once initialized.
*   **final method**: Prevents method overriding by subclasses.
*   **final class**: Prevents inheritance; the class cannot be subclassed (e.g., `String`, `Integer`).

### 10. How does Garbage Collection work in Java?

*   **Automatic Process**: Daemon thread that reclaims memory by destroying unreachable objects.
*   **Mark and Sweep**: Standard algorithm where GC "marks" typically reachable objects and "sweeps" (deletes) the unreachable ones.
*   **Generational Strategy**: Heap is divided into Young Generation (Eden, Survivor spaces) and Old Generation. New objects start in Young Gen. Long-surviving objects are promoted to Old Gen. Minor GC cleans Young Gen; Major/Full GC cleans Old Gen.

### 11. What is a WeakHashMap?

*   **Description**: A Map implementation where keys are stored as `WeakReference`s.
*   **Behavior**: If a key is no longer referenced strongly elsewhere in the application, the Garbage Collector will reclaim the key, and the entry will be automatically removed from the map.
*   **Use Case**: Ideal for building caches or listener collections where you want entries to be automatically cleaned up when they are no longer in use.

### 12. How is synchronization achieved in Java?

*   **synchronized Keyword**: Can be applied to methods (locks on `this` or class object) or blocks (locks on specific object). Ensures mutual exclusion.
*   **Volatile**: Ensures visibility of changes across threads but not atomicity.
*   **Locks (java.util.concurrent.locks)**: Explicit locks like `ReentrantLock` offer more advanced features (fairness, tryLock) than implicit monitors.
*   **Atomic Classes**: `AtomicInteger`, `AtomicReference` use CAS (Compare-And-Swap) for non-blocking thread safety.

### 13. What are the different thread states?

*   **NEW**: Created but not yet started.
*   **RUNNABLE**: Executing in JVM (could be running or waiting for CPU).
*   **BLOCKED**: Waiting to acquire a monitor lock.
*   **WAITING**: Waiting indefinitely for another thread to perform an action (e.g., `Object.wait`, `Thread.join`).
*   **TIMED_WAITING**: Waiting for a specified time (e.g., `Thread.sleep`, `Object.wait(timeout)`).
*   **TERMINATED**: Execution completed.

### 14. What is the difference between Runnable and Callable?

*   **Runnable**: Interface (`run()` method) does not return a result and cannot throw checked exceptions. Used for "fire-and-forget" tasks.
*   **Callable**: Interface (`call()` method) returns a result (`V`) and can throw checked exceptions (`Exception`). Used when a computation result is expected.
*   **Execution**: `Runnable` can be run by `Thread` or `ExecutorService`; `Callable` is typically executed by `ExecutorService` returning a `Future`.

### 15. What is thread starvation?

*   **Definition**: A condition where a thread is perpetually denied access to shared resources or CPU time because other higher-priority threads are constantly grabbing them.
*   **Cause**: Often due to greedy thread priorities or unfair locking policies where threads acquire locks for long periods.
*   **Result**: The starved thread is unable to make progress.

### 16. What is the difference between wait(), sleep(), and yield()?

*   **`wait()`**: Defined in `Object`. Releases the lock on the object and puts the thread in WAITING state until notified. Must be called from a synchronized context.
*   **`sleep()`**: Defined in `Thread`. Pauses execution for a specified duration. Does **not** release any locks.
*   **`yield()`**: Defined in `Thread`. Hints to the scheduler that the current thread is willing to yield its current use of a processor to other threads of the same priority. It effectively goes from Running to Runnable state.

### 17. How does the volatile keyword work?

*   **Visibility Guarantee**: It ensures that a write to a `volatile` variable is immediately flushed to main memory, and a read always reads from main memory. This solves the **visibility problem** (caching in CPU registers).
*   **Ordering**: It establishes a "happens-before" relationship, preventing the compiler and CPU from reordering instructions involving the volatile variable.
*   **Limitation**: It ensures visibility but **not atomicity**. It is not sufficient for compound actions like `count++`.

### 18. What is a race condition? How to prevent it?

*   **Definition**: Occurs when multiple threads access and modify shared data concurrently, and the final outcome depends on the unpredictable timing of their execution.
*   **Prevention**:
    *   **Synchronization**: Use `synchronized` blocks/methods.
    *   **Locks**: Use explicit `Lock` objects.
    *   **Atomic Variables**: Use `java.util.concurrent.atomic` classes.
    *   **Immutability**: Use immutable objects where possible.

### 19. Explain ReentrantLock vs synchronized block.

*   **Flexibility**: `ReentrantLock` provides `tryLock()` (attempt to lock without waiting), `lockInterruptibly()` (interrupt waiting thread), and fair locking policies, which `synchronized` does not support.
*   **Explicit vs Implicit**: `ReentrantLock` requires explicit `lock()` and `unlock()` (usually in a `finally` block). `synchronized` is implicit and safer (automatic unlock).
*   **Conditions**: `ReentrantLock` supports multiple `Condition` variables for a single lock, whereas `synchronized` works with a single monitor (wait/notify).

### 20. What is thread pooling and how is it implemented?

*   **Concept**: Reusing a pool of pre-created threads to execute a stream of tasks, rather than creating/destroying, a thread for every single task (which is expensive).
*   **Implementation**: In Java, it is implemented via the `Executor` framework.
*   **Common Pools**: `Executors.newFixedThreadPool(n)` (fixed size), `Executors.newCachedThreadPool()` (creates as needed, reuses idle), `Executors.newSingleThreadExecutor()` (sequential execution).

### 21. What is the Fork/Join framework?

*   **Purpose**: Designed for parallel processing of large tasks (part of `java.util.concurrent`).
*   **Mechanism**: Uses a **Divide and Conquer** approach. A large task is `forked` (split) into smaller subtasks recursively until they are small enough to be solved directly. Results are then `joined` (combined).
*   **Work Stealing**: Uses a work-stealing algorithm where idle threads steal tasks from the back of other busy threads' deques to maximize utilization.

### 22. Explain Stream API with examples.

*   **Concept**: A sequence of elements supporting sequential and parallel aggregate operations. It allows declarative data processing.
*   **Pipelines**: Source -> Intermediate Operations (transformations) -> Terminal Operation (result).
*   **Example**:
    ```java
    List<String> names = Arrays.asList("Alice", "Bob", "Anna");
    names.stream()
         .filter(name -> name.startsWith("A")) // Intermediate
         .map(String::toUpperCase)             // Intermediate
         .collect(Collectors.toList());        // Terminal
    ```

### 23. Difference between map() and flatMap() in Streams?

*   **`map()`**: Applies a function to each element and returns a new element. It performs a **one-to-one** mapping.
    *   `List<String>` -> `map(String::length)` -> `List<Integer>`
*   **`flatMap()`**: Applies a function that returns a stream for each element, and then flattens the resulting streams into a single stream. It performs a **one-to-many** mapping (flattening nested structures).
    *   `List<List<String>>` -> `flatMap(List::stream)` -> `List<String>`

### 24. What are functional interfaces?

*   **Definition**: An interface with **exactly one abstract method**.
*   **Usage**: They form the basis for Lambda expressions and Method References.
*   **Annotation**: `@FunctionalInterface` ensures the contract.
*   **Examples**: `Runnable`, `Callable`, `Comparator`, `Predicate<T>`, `Function<T,R>`, `Supplier<T>`, `Consumer<T>`.

### 25. What is the difference between Optional.of() and Optional.ofNullable()?

*   **`Optional.of(value)`**: Returns an Optional describing the given non-null value. If the value is `null`, it throws a **`NullPointerException`**. Use when you are sure the value is present.
*   **`Optional.ofNullable(value)`**: Returns an Optional describing the given value, if non-null, otherwise returns an empty Optional. It **does not throw NPE** for null values.

### 26. What is method reference? Give examples.

*   **Concept**: A shorthand syntax for a lambda expression that executes just ONE existing method.
*   **Syntax**: `ClassName::methodName`
*   **Types**:
    *   **Static Method**: `Math::max` (equivalent to `(a, b) -> Math.max(a, b)`)
    *   **Instance Method of Object**: `System.out::println` (equivalent to `x -> System.out.println(x)`)
    *   **Constructor**: `ArrayList::new` (equivalent to `() -> new ArrayList()`)

### 27. How does Collectors.groupingBy() work?

*   **Role**: A `Collector` used with Streams to group elements by a classifier function. It is similar to SQL's `GROUP BY`.
*   **Output**: Returns a `Map<K, List<T>>` where K is the classification key and the value is a list of items belonging to that category.
*   **Example**: `employees.stream().collect(Collectors.groupingBy(Employee::getDepartment))` returns a Map of employees grouped by department.

### 28. What is the default method in interfaces?

*   **Definition**: A method in an interface that has an implementation (body), marked with the `default` keyword. Introduced in Java 8.
*   **Purpose**: To enable **Backward Compatibility**. It allows adding new methods to existing interfaces without breaking the classes that implement them (they don't need to override the new method immediately).

### 29. What are sealed classes in Java?

*   **Feature**: Introduced in Java 15/17 to have fine-grained control over inheritance.
*   **Concept**: A sealed class (or interface) explicitly specifies which other classes are permitted to extend (or implement) it.
*   **Syntax**:
    ```java
    public sealed class Shape permits Circle, Square, Rectangle { ... }
    ```
*   **Goal**: Allows modelling fixed hierarchies and exhaustive pattern matching.

### 30. What is a record class in Java?

*   **Feature**: Introduced as a preview in Java 14, standard in Java 16.
*   **Concept**: A transparent carrier for immutable data. It is a class type that automatically generates component accessors, canonical constructor, `equals()`, `hashCode()`, and `toString()` based on defined fields.
*   **Syntax**: `public record Point(int x, int y) {}`
*   **Goal**: To eliminate the boilerplate code associated with "Plain Old Java Objects" (POJOs) or data transfer objects (DTOs).

### 31. Difference between checked and unchecked exceptions.

*   **Checked Exceptions**: Inherit from `Exception` but not `RuntimeException`. They are checked at **compile-time**. You strictly must handle them (using `try-catch`) or declare them (using `throws`).
    *   *Examples*: `IOException`, `SQLException`, `ClassNotFoundException`.
    *   *Use Case*: Recoverable conditions (e.g., file not found).
*   **Unchecked Exceptions**: Inherit from `RuntimeException`. They are checked at **runtime**, not compile-time. Handling them is optional.
    *   *Examples*: `NullPointerException`, `ArrayIndexOutOfBoundsException`, `IllegalArgumentException`.
    *   *Use Case*: Programming errors or unrecoverable conditions.

### 32. Custom exception handling in real-world applications.

*   **Create Custom Class**: Extend `Exception` (for checked) or `RuntimeException` (for unchecked).
*   **Global Handling**: Use `@ControllerAdvice` and `@ExceptionHandler` (in Spring Boot) to catch exceptions globally and return standardized error responses (e.g., JSON with code and message).
*   **Structure**: Include constructors passing `message` and `cause` (chained exceptions).
*   **Example**: `public class UserNotFoundException extends RuntimeException { ... }`

### 33. What is the diamond problem in Java?

*   **Problem**: In multiple inheritance (supported in C++, not Java classes), if a class inherits from two classes that both define the same method, the compiler doesn't know which one to use.
*   **Java's Answer**: Java classes do **not** support multiple inheritance of state/behavior.
*   **Note**: With **Default Methods** in interfaces (Java 8+), a similar conflict can occur if a class implements two interfaces containing the same default method. The compiler forces you to override the method in the implementing class to resolve the ambiguity (e.g., by calling `InterfaceA.super.method()`).

### 34. How does autoboxing/unboxing work?

*   **Autoboxing**: Automatic conversion of a primitive type to its corresponding wrapper class (e.g., `int` to `Integer`). Occurs when assigning a primitive to a wrapper or passing to a method expecting an object.
*   **Unboxing**: Automatic conversion of a wrapper class back to its primitive type (e.g., `Integer` to `int`). Occurs during arithmetic operations or assignments.
*   **Caveat**: Unboxing a `null` wrapper reference results in a `NullPointerException`.

### 35. Explain Enum in Java.

*   **Definition**: A special data type that represents a fixed set of constants.
*   **Features**:
    *   Type-safe.
    *   Can have fields, methods, and constructors.
    *   Can implement interfaces.
    *   Singleton by nature (each constant is a singleton instance).
*   **Usage**: Singleton pattern implementation, defining states, error codes, etc.

### 36. When to use TreeMap vs HashMap?

*   **Order**: Use `TreeMap` when you need keys to be **sorted** (natural order or custom comparator). `HashMap` makes no guarantees about order.
*   **Performance**: `HashMap` is faster (O(1) average time complexity for get/put). `TreeMap` is slower (O(log n)) because it is Red-Black tree-based.
*   **Nulls**: `HashMap` allows one null key. `TreeMap` does **not** allow null keys (it throws NPE because it tries to compare keys).

### 37. Why should hashCode() be consistent with equals()?

*   **Rule**: If two objects are equal according to `equals()`, they MUST have the same `hashCode()`.
*   **Reason**: Hash-based collections (HashMap, HashSet) first use the hash code to find the "bucket" location. If hash codes are different for equal objects, the collection will look in the wrong bucket and fail to retrieve the object, violating the Map contract.

### 38. How to make an object immutable?

1.  Declare the class as `final` (cannot be subclassed).
2.  Make all fields `private` and `final` (initialized once).
3.  Do **not** provide setter methods.
4.  Initialize all fields via the constructor.
5.  If a field refers to a mutable object (e.g., `Date`, `List`), perform a **deep copy** in the constructor and return a copy in the getter (defensive copying) to ensure complete encapsulation.

### 39. What is the use of the transient keyword?

*   **Serialization**: Used effectively during Java Serialization.
*   **Effect**: Marking a field as `transient` instructs the JVM **not to serialize** that particular field when writing the object state to a byte stream. All other non-transient fields are persisted.
*   **Value**: when deserialized, the transient field gets initialized to its default value (e.g., `null` for objects, `0` for int).
*   **Usage**: Passwords, sensitive data, or derived fields that don't need saving.

### 40. What is reflection in Java?

*   **Definition**: A powerful feature that allows a program to inspect and modify its own structure (classes, methods, fields) at **runtime**.
*   **Capabilities**:
    *   Inspect class names, methods, constructors, annotations.
    *   Instantiate objects (`Class.forName()`, `newInstance()`).
    *   Invoke methods dynamically.
    *   Access private fields (breaking encapsulation) using `setAccessible(true)`.
*   **Drawbacks**: Slower performance, security risks, harder to debug. Used heavily by frameworks (Spring, Hibernate).

### 41. What is the difference between static and instance initialization block?

*   **Static Block**: Runs **once** when the class is loaded into memory by the ClassLoader. Used to initialize static variables.
    *   Syntax: `static { ... }`
*   **Instance Block**: Runs **every time** an instance of the class is created, immediately before the constructor. Used to initialize instance variables.
    *   Syntax: `{ ... }`

### 42. Difference between shallow copy and deep copy.

*   **Shallow Copy**: Creates a new object but copies the *references* of the nested objects. Changes to the nested objects in the copy **will reflect** in the original object. Default behavior of `Object.clone()`.
*   **Deep Copy**: Creates a new object and recursively creates copies of all nested objects. The original and the copy are completely independent. Changes to the copy **will not** affect the original.

### 43. What is the use of System.identityHashCode()?

*   **Purpose**: Returns the same hash code for the given object as would be returned by the default `hashCode()` method (based on memory address), regardless of whether the given object's class overrides `hashCode()`.
*   **Use Case**: Useful for checking reference equality or identifying specific object instances in debugging/logging when `hashCode` has been overridden.

### 44. Explain CompletableFuture with example.

*   **Concept**: An enhancement over `Future` (Java 8) that allows asynchronous programming with non-blocking logic. It supports chaining (callbacks), error handling, and combining multiple futures.
*   **Example**:
    ```java
    CompletableFuture.supplyAsync(() -> "Hello")
                     .thenApply(s -> s + " World")
                     .thenAccept(System.out::println); // Prints "Hello World" asynchronously
    ```

### 45. How do you implement a singleton pattern?

*   **Best Practice (Enum)**:
    ```java
    public enum Singleton {
        INSTANCE;
        public void doSomething() { ... }
    }
    ```
*   **Lazy Initialization (Double-Checked Locking)**:
    ```java
    public class Singleton {
        private static volatile Singleton instance;
        private Singleton() {}
        public static Singleton getInstance() {
            if (instance == null) {
                synchronized (Singleton.class) {
                    if (instance == null) instance = new Singleton();
                }
            }
            return instance;
        }
    }
    ```

### 46. What are some ways to break a singleton?

*   **Reflection**: Can set constructor accessibility to true and create a new instance.
*   **Serialization**: Deserializing a singleton creates a new instance (fix by implementing `readResolve()`).
*   **Cloning**: If `clone()` is overridden, a copy can be created (fix by throwing exception in `clone()`).
*   **Multi-threading**: Imperfect lazy loading implementation can create multiple instances.

### 47. What is double-checked locking?

*   **Concept**: A performance optimization for lazy initialization of Singletons.
*   **Mechanism**: First check if the instance is null without locking (fast path). If null, acquire lock. Then check if instance is null *again* (double-check) inside the synchronized block before creating it.
*   **Requirement**: The instance variable must be declared **`volatile`** to prevent instruction reordering issues.

### 48. What are phantom references?

*   **Definition**: The weakest type of reference in Java (`java.lang.ref.PhantomReference`).
*   **Behavior**: An object with only phantom references is eligible for collection. Unlike WeakReference, it is *only* enqueued in a `ReferenceQueue` after the object has been finalized/collected effectively.
*   **Usage**: Used for scheduling post-mortem cleanup actions (a better alternative to `finalize()`) or tracking object removal.

### 49. Why is clone() considered bad practice?

*   **Constructors**: `clone()` bypasses the constructor, which can lead to uninitialized or invalid object states.
*   **Shallow Copy**: Default implementation performs a shallow copy, which is often dangerous for mutable fields.
*   **Exceptions**: It throws a checked exception `CloneNotSupportedException` which is cumbersome.
*   **Marker Interface**: Relies on the empty `Cloneable` interface, which doesn't define the method itself (it's in `Object`).
*   **Better Alternative**: Copy constructors or static factory methods (e.g., `newInstance(oldInstance)`).

### 50. How would you design your own custom collection?

*   **Steps**:
    1.  **Interface**: Implement a standard interface like `List`, `Set`, or `Map` (or extend `AbstractList` etc. to reduce boilerplate).
    2.  **Storage**: Choose a backing data structure (Array, Node, Hash Table).
    3.  **Operations**: Implement core methods (`add`, `remove`, `get`, `size`).
    4.  **Resizing**: Handle logic for growing/shrinkage if dynamic.
    5.  **Iterator**: Implement `Iterable` and provide a custom iterator for changing traversal logic.
    6.  **Edge Cases**: Handle `null` values and concurrency (if needed).

### 51. Explain method overloading vs overriding

*   **Method Overloading (Compile-time Polymorphism)**:
    *   Same method name, **different** parameter list (type, number, order).
    *   Occurs within the **same class** (or subclass).
    *   Return type *can* change (but not sufficient alone to overload).
    *   Decided by compiler (static binding).
*   **Method Overriding (Runtime Polymorphism)**:
    *   Same method name, **same** parameter list, same return type (or covariant).
    *   Occurs in **Parent-Child** class relationship.
    *   Decided by JVM at runtime (dynamic dispatch).

### 52. Explain covariant return types.

*   **Concept**: Since Java 5, when overriding a method in a subclass, the return type does not have to be exactly the same; it can be a **subclass** of the return type declared in the parent method.
*   **Example**:
    ```java
    class Parent { Object get() { ... } }
    class Child extends Parent { @Override String get() { ... } } // Valid: String is a subclass of Object
    ```
*   **Benefit**: Removes the need for type casting in the client code.

### 53. How does Java handle pass-by-value or reference?

*   **Rule**: Java is **strictly pass-by-value**.
    *   **Primitives**: The actual value (e.g., `5`, `true`) is copied and passed.
    *   **Objects**: The **reference** (memory address) to the object is copied and passed.
*   **Implication**: You can modify the *state* of the object inside the method (e.g., `list.add("A")`), and it reflects outside. However, if you reassign the reference itself (e.g., `list = new ArrayList()`), it has **no effect** on the original reference outside the method.

### 54. Can we override private/static/final methods?

*   **Private Methods**: **No**. They are not visible to subclasses, so they cannot be overridden. Defining a same-named method in a subclass is just a *new* method.
*   **Static Methods**: **No**. They belong to the class, not the instance. Re-declaring them in a subclass is called **Method Hiding**, not overriding. The method called depends on the reference type, not the object type.
*   **Final Methods**: **No**. The `final` keyword explicitly prevents overriding logic to ensure the behavior remains constant.

### 55. When would you use an abstract class over interface?

*   **Abstract Class**:
    *   When you need to share **code** or **state** (fields) among closely related classes.
    *   When you need a constructor to initialize state.
    *   When you want to define non-static or non-final fields.
*   **Interface**:
    *   When you want to define a **contract** (capability) for unrelated classes (e.g., `Serializable`, `Comparable`).
    *   When you need **multiple inheritance** (a class can implement multiple interfaces).
    *   When you expect APIs to change (adding default methods is safer than adding abstract methods).

### 56. What is java.lang.instrument used for?

*   **Purpose**: It provides services that allow Java programming language agents to **instrument** programs running on the JVM.
*   **Mechanism**: It allows you to modify the bytecodes of methods at runtime (during class loading).
*   **Use Cases**:
    *   Monitoring and Profiling tools (e.g., New Relic, Datadog agents).
    *   Code coverage analysis.
    *   Logging injection without modifying source code.

### 57. What is Metaspace in Java?

*   **Change**: Introduced in Java 8 to replace the **PermGen** (Permanent Generation) memory space.
*   **Storage**: Stores Class metadata (class definitions, method structures, constants).
*   **Location**: Allocated in **Native Memory** (OS memory), not the Java Heap.
*   **Benefit**: It can auto-resize based on the application's needs (up to `MaxMetaspaceSize`), reducing the frequency of `OutOfMemoryError: PermGen space`.

### 58. How to detect memory leaks in Java?

*   **Symptoms**: Increasing heap usage over time, frequent Full GC cycles, `OutOfMemoryError`.
*   **Tools**:
    *   **VisualVM / JConsole**: Monitor heap usage and GC activity in real-time.
    *   **Heap Dump**: Capture a snapshot of memory (`jmap`).
    *   **Analyzers**: Use **Eclipse MAT** (Memory Analyzer Tool) or **JProfiler** to analyze the heap dump.
*   **Strategy**: Look for the **"Dominator Tree"** to find objects retaining the most memory. Identify objects that should have been collected (e.g., closed connections, unused listeners) but are still referenced.

### 59. What is ClassLoader? Types of class loaders?

*   **Role**: Part of JRE that dynamically loads Java classes into the JVM when they are referenced.
*   **Hierarchy**:
    1.  **Bootstrap ClassLoader**: Loads core Java libraries (from `rt.jar`, `java.base`). Written in native code.
    2.  **Platform/Extension ClassLoader**: Loads platform-specific extensions (from `lib/ext`).
    3.  **System/Application ClassLoader**: Loads classes from the application's **classpath** (environment variable or `-cp`).
*   **Delegation Model**: A loader first delegates the request to its parent. Only if the parent fails does it try to load the class itself.

### 60. What is JIT compiler?

*   **Definition**: Just-In-Time Compiler. It is a component of the JRE inside the JVM.
*   **Function**: It improves performance by compiling **bytecodes** (which are interpreted) into native **machine code** (which runs directly on hardware) *at runtime*.
*   **Hotspots**: It identifies frequently executed methods ("hotspots") and compiles them. It also performs adaptive optimizations like method inlining and dead code elimination.

### 61. How do annotations work internally?

*   **Mechanism**: Annotations are a form of metadata. Internally, they are defined as **Interfaces** that extend `java.lang.annotation.Annotation`.
*   **Retention**: Based on `@Retention` policy (`SOURCE`, `CLASS`, `RUNTIME`), they are stored in the class file or available at runtime.
*   **Proxy**: When you access an annotation at runtime via Reflection, the JVM creates a **dynamic proxy** object that implements the annotation interface.

### 62. How to create custom annotations?

*   **Syntax**: Use `@interface` keyword.
*   **Meta-Annotations**: Use `@Retention` (e.g., `RetentionPolicy.RUNTIME`) and `@Target` (e.g., `ElementType.METHOD`) to define scope.
*   **Code**:
    ```java
    @Retention(RetentionPolicy.RUNTIME)
    @Target(ElementType.METHOD)
    public @interface MyCustomAnnotation {
        String value() default "default";
        int priority();
    }
    ```

### 63. What is annotation processing in Java?

*   **Process**: A compile-time tool (`javax.annotation.processing.Processor`) that scans source code for annotations.
*   **Action**: It can validate code, generate new source files (code generation), or creating configuration files (like XML).
*   **Example**: Lombok (generates getters/setters), Dagger (dependency injection), Hibernate/JPA (metamodel generation).

### 64. What are lambdas and how do they work internally?

*   **Concept**: Anonymous functions used to implement functional interfaces.
*   **Internal**: They are NOT just anonymous inner classes (which create separate .class files).
*   **Bytecode**: The compiler generates an `invokedynamic` instruction. At runtime, the JVM uses the `LambdaMetafactory` to create an instance of the functional interface, often binding it to a generated private static method in the class containing the implementation logic.

### 65. Explain Type Erasure in Generics.

*   **Definition**: The process where the Java compiler removes all generic type information (type parameters like `<T>`, `<String>`) after compilation.
*   **Result**: At runtime, `List<String>` and `List<Integer>` become just `List` (raw type). The compiler inserts necessary type casts for retrieval.
*   **Reason**: To ensure backward compatibility with older Java versions (pre-Java 5) that didn't support generics.

### 66. How are Generics implemented internally?

*   **Mechanism**: Through Type Erasure (as explained above).
*   **Bridge Methods**: Compiler might generate synthetic "bridge methods" to preserve polymorphism (overriding) when type erasure changes method signatures in subclasses.
*   **No Reification**: Generic types are **non-reifiable**, meaning their type information is not fully available at runtime (unlike arrays).

### 67. Explain bounded vs unbounded wildcards.

*   **Unbounded `<?>`**: Represents a list of "unknown" type. Read-only (mostly).
    *   `List<?> list`. You can read `Object`, but cannot add anything (except null).
*   **Upper Bounded `<? extends T>`**: Accepts T or its subclasses. "Producer".
    *   Use when you want to **read** from the list (Get T).
*   **Lower Bounded `<? super T>`**: Accepts T or its superclasses. "Consumer".
    *   Use when you want to **write** to the list (Add T).
*   **PECS**: **P**roducer **E**xtends, **C**onsumer **S**uper.

### 68. What is raw type in Java?

*   **Definition**: A generic class or interface used without a type argument.
    *   Example: `List list = new ArrayList();` instead of `List<String> list...`
*   **Risk**: It bypasses generic type checks, allowing any object to be added, which can lead to `ClassCastException` at runtime.
*   **Advice**: Avoid raw types in modern Java.

### 69. How would you make a list thread-safe?

1.  **Collections.synchronizedList()**: Wraps the list in a synchronized wrapper.
    *   `List<String> syncList = Collections.synchronizedList(new ArrayList<>());`
2.  **CopyOnWriteArrayList**: Thread-safe variant of ArrayList from `java.util.concurrent`. Best for read-heavy scenarios (writes are expensive as they copy the array).
3.  **Vector**: Legacy thread-safe class (avoid due to performance).

### 70. How to avoid deadlock in concurrent programming?

*   **Definition**: A situation where two or more threads are blocked forever, each waiting on a resource held by the other.
*   **Prevention Strategies**:
    *   **Lock Ordering**: Always acquire locks in a consistent, global order (e.g., always Lock A then Lock B).
    *   **Lock Timeout**: Use `tryLock(timeout)` (ReentrantLock) to fail if a lock isn't acquired within a time limit, allowing the thread to back off.
    *   **Minimize Scope**: Keep synchronized blocks as short as possible.

### 71. Difference between Spring and Spring Boot.

*   **Spring Framework**: A comprehensive, modular application framework that provides infrastructure support (DI, AOP, Transaction Management) for developing enterprise Java applications. It requires significant manual configuration (XML or Java-based).
*   **Spring Boot**: An extension of the Spring Framework designed to simplify the bootstrapping and development of new Spring applications. It provides **Auto-Configuration**, **Starter Dependencies**, and an **Embedded Server** (Tomcat/Jetty) to create stand-alone, production-grade applications with minimal configuration.

### 72. What is dependency injection and how is it implemented in Spring?

*   **Definition**: A design pattern (form of Inversion of Control) where the dependencies of a class (objects it needs to function) are "injected" into it from the outside, rather than the class creating them itself.
*   **Implementation**: Spring IoC (Inversion of Control) Container manages the lifecycle and configuration of application objects (Beans).
*   **Types**:
    *   **Constructor Injection** (Recommended for mandatory dependencies).
    *   **Setter Injection** (Optional dependencies).
    *   **Field Injection** (Using `@Autowired` on fields, discouraged due to testing difficulties).

### 73. Difference between @Component, @Service, @Repository, and @Controller.

*   **`@Component`**: Generic stereotype for any Spring-managed component.
*   **`@Controller`**: Specialization of `@Component` for the presentation layer (Spring MVC).
*   **`@Service`**: Specialization for the service layer (business logic). It clarifies intent but currently holds no extra behavior over `@Component`.
*   **`@Repository`**: Specialization for the persistence layer (DAO). It adds automatic **exception translation** (translating raw DB exceptions to Spring's `DataAccessException` hierarchy).

### 74. What is the role of @Autowired and how does it work?

*   **Role**: Marks a dependency (constructor, field, or setter) to be resolved and injected by the Spring container.
*   **Mechanism**:
    1.  **By Type**: Spring first looks for a bean that matches the *type* of the dependency.
    2.  **By Qualifier**: If multiple beans of the same type exist, it uses `@Qualifier` to distinguish.
    3.  **By Name**: If ambiguity persists, it attempts to match the bean name with the variable name.

### 75. How does Spring Boot auto-configuration work?

*   **Magic**: Driven by the `@EnableAutoConfiguration` annotation (part of `@SpringBootApplication`).
*   **Mechanism**: It scans the classpath for dependencies. Based on what jars are present, it automatically configures beans.
*   **Example**: If `spring-boot-starter-web` is on the classpath, Spring constatis that you want a web application and automatically configures Tomcat and Spring MVC.
*   **Conditional**: Uses `@ConditionalOnClass`, `@ConditionalOnMissingBean`, `@ConditionalOnProperty` to ensure it only configures beans if you haven't defined your own.

### 76. What are the starter dependencies in Spring Boot?

*   **Definition**: Curated sets of convenient dependency descriptors that you can include in your application. They aggregate common related dependencies so you don't have to manage versions manually.
*   **Examples**:
    *   `spring-boot-starter-web`: Includes MVC, REST, Tomcat, Jackson.
    *   `spring-boot-starter-data-jpa`: Includes Hibernate, Spring Data JPA, HikariCP.
    *   `spring-boot-starter-test`: Includes JUnit, Mockito, Hamcrest.

### 77. What is @SpringBootApplication composed of?

*   It is a meta-annotation that combines three other annotations:
    1.  **`@Configuration`**: Marks the class as a source of bean definitions.
    2.  **`@EnableAutoConfiguration`**: Tells Boot to start adding beans based on classpath settings.
    3.  **`@ComponentScan`**: Tells Spring to look for other components, configurations, and services in the underlying package.

### 78. How does component scanning work in Spring Boot?

*   **Process**: By default, `@SpringBootApplication` scans the package where it is located and all **sub-packages**.
*   **Action**: It looks for classes annotated with stereotypes (`@Component`, `@Service`, etc.) and registers them as beans in the ApplicationContext.
*   **Customization**: You can specify base packages expressely using `@ComponentScan(basePackages = "com.example")`.

### 79. How do profiles work in Spring Boot?

*   **Purpose**: To segregate parts of the application configuration and make it available only in certain environments (e.g., dev, test, prod).
*   **Usage**:
    *   **Properties**: `application-dev.properties`, `application-prod.properties`.
    *   **Activation**: Set `spring.profiles.active=dev` in application.properties or as a command-line argument.
    *   **Beans**: Use `@Profile("dev")` on a bean/class to instantiate it only when that profile is active.

### 80. What are beans in Spring? Lifecycle?

*   **Definition**: Objects that form the backbone of your application and are managed by the Spring IoC container.
*   ** Lifecycle**:
    1.  **Instantiation**: Container creates the bean instance.
    2.  **Populate Properties**: Dependencies are injected.
    3.  **Initialization**:
        *   `postProcessBeforeInitialization` (BeanPostProcessors).
        *   `@PostConstruct` / `afterPropertiesSet()` (InitializingBean).
        *   `postProcessAfterInitialization`.
    4.  **Use**: Bean is ready for use.
    5.  **Destruction**: `@PreDestroy` / `destroy()` (DisposableBean) when container shuts down.

### 81. Difference between ApplicationContext and BeanFactory.

*   **BeanFactory**: The most basic container, providing DI capabilities. It uses **lazy initialization** (beans are created only when requested `getBean()`). Suitable for lightweight apps (mobile/embedded).
*   **ApplicationContext**: Extends BeanFactory and adds enterprise-specific functionality. It uses **eager initialization** for singletons (creates them on startup).
    *   Features: AOP integration, Message Resource handling (i18n), Event publication, Annotation support.
    *   *Conclusion*: In modern Spring, `ApplicationContext` is used almost exclusively.

### 82. How to define a custom scope?

*   **Standard Scopes**: Singleton, Prototype, Request, Session, GlobalSession.
*   **Custom Scope Implementation**:
    1.  Implement the `org.springframework.beans.factory.config.Scope` interface.
    2.  Create methods like `get()`, `remove()`.
    3.  Register the scope with the `ConfigurableBeanFactory` using `registerScope("myScope", new MyScope())`.
    4.  Use `@Scope("myScope")` on your beans.
*   **Use Case**: A "ThreadScope" or "ConversationScope".

### 83. What is AOP? Explain with use-case.

*   **Definition**: **A**spect-**O**riented **P**rogramming. It is a programming paradigm that aims to increase modularity by allowing the separation of **Cross-Cutting Concerns** (code that spans multiple modules) from the main business logic.
*   **Use-Case**: **Logging**. Instead of writing `log.info("Starting method")` and `log.info("Ending method")` inside every single service method, you define an *Aspect* that intercepts execution and applies this logging logic automatically to all relevant methods.
*   **Other Examples**: Transaction Management, Security, Caching, Error Handling.

### 84. Difference between cross-cutting concern and business logic?

*   **Business Logic**: Core functional requirements (e.g., "Calculate Interest", "Process Order", "Register User"). This code is specific to the application's domain.
*   **Cross-Cutting Concern**: Technical requirements (System services) that affect many parts of the application but are distinct from the domain logic.
    *   Examples: Logging, Audit trails, Security checks, Transaction rollback, Performance monitoring.

### 85. How to implement custom annotations with AOP?

1.  **Create Annotation**: Define an annotation `@interface LogExecutionTime` (Retention: Runtime, Target: Method).
2.  **Create Aspect**: Create a class annotated with `@Aspect` and `@Component`.
3.  **Define Pointcut**: Use `@Around("@annotation(LogExecutionTime)")`.
4.  **Implement Advice**:
    ```java
    @Around("@annotation(LogExecutionTime)")
    public Object logTime(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();
        Object proceed = joinPoint.proceed();
        long executionTime = System.currentTimeMillis() - start;
        System.out.println(joinPoint.getSignature() + " executed in " + executionTime + "ms");
        return proceed;
    }
    ```

### 86. What is the use of @Transactional?

*   **Role**: It is a declarative way to manage database transactions.
*   **Mechanism**: Spring creates a proxy around the class/method.
*   **Behavior**:
    1.  **Start**: Before the method runs, it begins a database transaction.
    2.  **Commit**: If the method completes successfully, it commits the transaction.
    3.  **Rollback**: If an unchecked exception (`RuntimeException`) occurs, it automatically rolls back the transaction. Checked exceptions do *not* trigger rollback by default (unless `rollbackFor = Exception.class` is specified).

### 87. What is the difference between programmatic and declarative transaction management?

*   **Programmatic**: Using code to manage transactions (e.g., `TransactionTemplate` or `PlatformTransactionManager`).
    *   *Pros*: Precise control (start/commit/rollback exactly where needed).
    *   *Cons*: Boilerplate code, tightly couples transaction logic with business logic.
*   **Declarative**: Using annotations (`@Transactional`) or XML configuration.
    *   *Pros*: Clean code, separation of concerns, easy to configure. Most common approach.
    *   *Cons*: Less granular control (method level).

### 88. Explain propagation types in transaction management.

*   **REQUIRED (Default)**: Uses existing transaction if available; otherwise, creates a new one.
*   **REQUIRES_NEW**: Always creates a new transaction. Suspends any existing one.
*   **SUPPORTS**: Uses existing transaction if available; otherwise, executes non-transactionally.
*   **MANDATORY**: Uses existing transaction; throws exception if none exists.
*   **NEVER**: Executes non-transactionally; throws exception if a transaction exists.
*   **NOT_SUPPORTED**: Executes non-transactionally; suspends any existing transaction.

### 89. How does Spring handle circular dependency?

*   **Scenario**: Bean A depends on Bean B, and Bean B depends on Bean A.
*   **Setter/Field Injection**: Spring handles this by creating beans eagerly but injecting dependencies later. It uses a **3-level cache** (singletonObjects, earlySingletonObjects, singletonFactories) to expose partially initialized (proxy) beans.
*   **Constructor Injection**: Circular dependency creates a deadlock (cannot instantiate A without B, B without A). Spring throws `BeanCurrentlyInCreationException`.
    *   *Fix*: Change to Setter injection or use `@Lazy` on one of the constructor arguments.

### 90. What is the difference between @Value, @ConfigurationProperties, and Environment?

*   **`@Value`**: Injects a single property value (e.g., `@Value("${app.timeout}")`). Good for simple, one-off values.
*   **`@ConfigurationProperties`**: Binds a group of properties (e.g., `app.mail.*`) to a POJO (Java Bean). Type-safe, supports validation, and good for hierarchical config.
*   **`Environment`**: An abstraction representing the environment (profiles + properties). Can be injected (`@Autowired Environment env`) to access properties programmatically (`env.getProperty("key")`).

### 91. Explain RestTemplate vs WebClient.

*   **RestTemplate**: The traditional, synchronous, blocking client for making HTTP requests. It uses a thread-per-request model. Deprecated in future versions but still widely used.
*   **WebClient**: The modern, non-blocking, reactive client introduced in Spring 5 (part of Spring WebFlux). It uses relatively few threads (Netty event loop) to handle high concurrency with less resource usage. It supports both synchronous (block()) and asynchronous operations.

### 92. What is reactive programming in Spring?

*   **Definition**: A programming paradigm focused on processing **asynchronous streams of data** with **non-blocking backpressure**.
*   **Goal**: To build more resilient and scalable systems that can handle a massive number of concurrent connections with a small number of threads.
*   **Core Concepts**: Publisher, Subscriber, Subscription, Processor (Reactive Streams Specification).

### 93. Difference between Mono and Flux?

*   **Core Types**: Both are implementations of `Publisher<T>` in Project Reactor (the reactive library used by Spring).
*   **Mono**: Represents a stream of **0 or 1** element.
    *   *Use Case*: Fetching a single user by ID, returning an HTTP response.
*   **Flux**: Represents a stream of **0 to N** elements.
    *   *Use Case*: Fetching a list of users, processing a live feed of stock prices.

### 94. What is Spring WebFlux?

*   **Definition**: The reactive-stack web framework added in Spring 5. It is parallel to Spring MVC.
*   **Architecture**: Runs on non-blocking servers like **Netty**, Undertow, or Servlet 3.1+ containers. Uses an Event Loop architecture.
*   **Programming Model**: Supports both Annotation-based controllers (similar to Spring MVC) and Functional Endpoints (Router/Handler functions).

### 95. How to secure a REST API using Spring Security?

1.  **Dependency**: Add `spring-boot-starter-security`.
2.  **Configuration**: Create a class extending `WebSecurityConfigurerAdapter` (Old) or defining a `SecurityFilterChain` bean (New/Recommended).
3.  **Authentication**: Configure `UserDetailsService` or OAuth2.
4.  **Authorization**: Use `.authorizeHttpRequests()` to verify permissions for URL paths (e.g., `.requestMatchers("/admin/**").hasRole("ADMIN")`).
5.  **State**: For REST APIs, typically disable sessions (`SessionCreationPolicy.STATELESS`) and use tokens (JWT).

### 96. Difference between permitAll() and authenticated()?

*   **`permitAll()`**: Allows **anyone** (including anonymous/unauthenticated users) to access the specified endpoint.
    *   *Example*: Login page, Public home page.
*   **`authenticated()`**: Requires the user to be **logged in** (successfully authenticated) to access the endpoint, regardless of their specific role/authority.

### 97. What is CSRF and how to handle it in Spring?

*   **CSRF**: Cross-Site Request Forgery. An attack where a malicious site tricks a user into performing unwanted actions on a site they are authenticated with.
*   **Handling**:
    *   **Browser-based Apps**: consistently use CSRF tokens (Spring Security enables this by default).
    *   **Stateless REST APIs**: If the API is stateless (using JWT/Tokens/Headers) and not Session/Cookie based, you can explicitly **disable** CSRF protection (`http.csrf().disable()`) because the browser doesn't automatically send custom tokens, mitigating the vector.

### 98. What is AuthenticationManager?

*   **Role**: The main interface for authentication in Spring Security.
*   **Method**: `authenticate(Authentication authentication)`.
*   **Implementation**: The default implementation is `ProviderManager`, which delegates to a list of configured `AuthenticationProvider`s (e.g., DaoAuthenticationProvider, LdapAuthenticationProvider).

### 99. How to implement custom authentication in Spring Security?

1.  Implement `UserDetailsService` interface and override `loadUserByUsername()`.
2.  Fetch user data (username, password, roles) from your custom database/source.
3.  Return a `UserDetails` object (usually an instance of `org.springframework.security.core.userdetails.User`).
4.  Spring Security automatically uses this service to verify credentials during login.

### 100. What are filters and interceptors?

*   **Filter (Servlet Filter)**:
    *   Part of the Servlet API (Java EE / Jakarta EE).
    *   Operates **outside** of Spring MVC context (before the DispatcherServlet).
    *   Good for: Request logging, encoding, security (Spring Security filter chain).
*   **Interceptor (HandlerInterceptor)**:
    *   Part of the Spring MVC Framework.
    *   Access to the **Handler** (Controller method) and `ModelAndView`.
    *   Good for: Application-specific logic like permission checks, adding common model attributes, or modifying the response within the framework.

### 101. What is the difference between Filter and HandlerInterceptor?

*   **Filter**:
    *   Part of the **Servlet API** (server agnostic).
    *   Interceptor logic happens *outside* the SpringMVC context.
    *   Executes before the request reaches the DispatcherServlet.
    *   Main usage: Logging, Security, compression, audit.
*   **HandlerInterceptor**:
    *   Part of the **Spring MVC** framework.
    *   Interceptor logic happens *inside* the SpringMVC context.
    *   Executes after DispatcherServlet but before the controller handle method.
    *   Main usage: Authentication checks, locale changing, theme changing.
    *   Can access the Handler object (the Controller bean).

### 102. How does Spring handle exceptions?

*   **Mechanism**: Through the `HandlerExceptionResolver` interface.
*   **Methods**:
    1.  **`@ExceptionHandler`**: Handling exceptions within a specific controller.
    2.  **`@ControllerAdvice`**: Global handling of exceptions across all controllers.
    3.  **`ResponseStatusException`**: Throwing exceptions with specific HTTP status codes.
    4.  **`DefaultHandlerExceptionResolver`**: Spring's default internal exception handling.

### 103. What is the difference between @ControllerAdvice and @ExceptionHandler?

*   **`@ExceptionHandler`**: Used on methods within a single controller class to catch exceptions. It only applies to requests processed by that specific controller.
*   **`@ControllerAdvice`**: A class-level annotation that serves as a global exception handler. It makes `@ExceptionHandler`, `@InitBinder`, and `@ModelAttribute` methods declared within it applicable to **all** controllers (or a subset via strictions). It avoids code duplication.

### 104. How to return consistent error responses in Spring REST?

1.  **Create a DTO**: Define a standard error structure (e.g., `ApiError(timestamp, status, message, details)`).
2.  **Use @ControllerAdvice**: Create a global exception handler class.
3.  **Implement Handler Methods**: Use `@ExceptionHandler` methods to catch specific exceptions (e.g., `UserNotFoundException`, `MethodArgumentNotValidException`).
4.  **Return Response**: Build and return a `ResponseEntity<ApiError>` containing the error details and appropriate HTTP Status Code.

### 105. How to create custom validators in Spring Boot?

1.  **Define Annotation**: Create a new annotation (e.g., `@StrongPassword`) annotated with `@Constraint`.
2.  **Create Validator**: Implement the `ConstraintValidator<Annotation, Type>` interface. Override the `isValid()` method to put in your custom logic.
3.  **Link**: Specify the validator class in the `@Constraint(validatedBy = StrongPasswordValidator.class)` of your annotation.
4.  **Use**: Annotate your DTO fields with `@StrongPassword`.

### 106. Difference between validation groups and constraints?

*   **Constraints**: These are the actual validation rules applied to fields (e.g., `@NotNull`, `@Size`, `@Email`). They define *what* is valid.
*   **Validation Groups**: These act as a filter to apply only a **subset** of constraints during validation.
    *   *Example*: You might want to validate the `id` field during an "Update" operation (it must not be null) but ignore it during a "Create" operation (it should be null/generated). You use `interface Create extends Default {}` and pass it to `@Validated(Create.class)`.

### 107. What is the use of @Valid and @Validated?

*   **`@Valid`**: Standard **JSR-303/Jakarta Bean Validation** annotation. Used to trigger validation on a nested object properties. It does **not** support validation groups.
*   **`@Validated`**: Spring's variant (`org.springframework.validation.annotation.Validated`). It supports **Validation Groups**. It can also be used at the class level (e.g., in Services) to trigger method parameter validation.

### 108. How to use Swagger/OpenAPI in Spring Boot?

1.  **Dependency**: Add `springdoc-openapi-starter-webmvc-ui` (modern replacement for SpringFox).
2.  **Access**: Run the application and navigate to `/swagger-ui/index.html`.
3.  **Annotations**: Use OpenAPI annotations to enrich documentation:
    *   `@Operation(summary = "Get user by ID")`
    *   `@ApiResponse(responseCode = "200", description = "Found user")`
    *   `@Schema(description = "User data transfer object")`

### 109. Difference between @PathVariable and @RequestParam.

*   **`@PathVariable`**: Extracts values from the **URI path** itself. It identifies a specific resource.
    *   URL: `/users/123` -> `@GetMapping("/users/{id}") get(@PathVariable String id)`
*   **`@RequestParam`**: Extracts values from the **query parameters** (after the `?`). It acts as a filter or option.
    *   URL: `/users?role=admin` -> `@GetMapping("/users") get(@RequestParam String role)`

### 110. What is HATEOAS?

*   **Definition**: **H**ypermedia **A**s **T**he **E**ngine **O**f **A**pplication **S**tate. It is a constraint of the REST application architecture.
*   **Concept**: A client interacts with a network application entirely through hypermedia (links) provided dynamically by the application servers.
*   **Spring HATEOAS**: A library that helps you write REST services that return **links** (`_links` in JSON) along with resource data, guiding the client on what actions (URLs) are available next (e.g., self, update-user, delete-user).

### 111. How does @Async work in Spring Boot?

*   **Enabling**: Annotated with `@EnableAsync` on a configuration class.
*   **Usage**: Annotate a method with `@Async`. When called, the method executes in a **separate thread** (from a task executor), allowing the caller to proceed immediately without waiting.
*   **Return Type**: Can return `void` or `Future<T>` (typically `CompletableFuture<T>`).
*   **Constraint**: Must be called from an external class (self-invocation bypasses the proxy, so async won't work).

### 112. What is Spring Scheduler? Cron jobs?

*   **Enabling**: Annotated with `@EnableScheduling`.
*   **Usage**: Annotate a method with `@Scheduled`.
*   **Attributes**:
    *   `fixedRate`: Execute every X ms (measured from start time).
    *   `fixedDelay`: Execute X ms *after* the previous execution finishes.
    *   `cron`: Unix-like cron expression (e.g., `"0 0 12 * * ?"`) for complex schedules (Seconds, Minutes, Hours, Day, Month, Weekday).

### 113. How to publish and listen to events in Spring?

*   **Define Event**: Create a class extending `ApplicationEvent` (optional in newer Spring).
*   **Publish**: Inject `ApplicationEventPublisher` and call `publisher.publishEvent(new MyEvent(this, data))`.
*   **Listen**: Create a method annotated with `@EventListener` accepting the event as a parameter.
    ```java
    @EventListener
    public void handleEvent(MyEvent event) { ... }
    ```

### 114. Difference between synchronous and asynchronous event publishing.

*   **Synchronous (Default)**: The publisher's thread blocks until all listeners have processed the event. If a listener fails, it can affect the publisher. Useful for transactional consistency.
*   **Asynchronous**: The event is processed in a separate thread. Achieved by annotating the listener method with both `@EventListener` and `@Async`. The publisher continues immediately. Useful for decoupled, non-critical side effects (e.g., sending email).

### 115. How does caching work in Spring Boot?

*   **Abstraction**: Spring provides a Cache Abstraction (`@EnableCaching`) that applies caching to Java methods.
*   **Annotations**:
    *   `@Cacheable("users")`: Checks cache before executing method. If found, returns cached value; else executes and caches result.
    *   `@CachePut`: Always executes method and updates cache.
    *   `@CacheEvict`: Removes entries from the cache (e.g., on delete/update).
*   **Providers**: Takes care of the logic but requires a storage provider (ConcurrentMap, EhCache, Redis, Caffeine).

### 116. How to use Redis for caching?

1.  **Dependency**: Add `spring-boot-starter-data-redis`.
2.  **Config**: Configure host/port in `application.properties` (`spring.data.redis.host=localhost`).
3.  **Enable**: Add `@EnableCaching`.
4.  **Auto-config**: Spring Boot detects Redis and automatically configures a `RedisCacheManager`. Serializes objects (must be `Serializable` or use JSON serializer) to store in Redis keys.

### 117. How to monitor Spring Boot applications?

*   **Endpoints**: Use **Spring Boot Actuator** to expose operational information.
*   **Metrics**: Collect metrics (CPU, Memory, Request latency) using **Micrometer**.
*   **Visualization**: Export metrics to monitoring systems like **Prometheus**, **Grafana**, **Datadog**, or **New Relic**.
*   **Logs**: Centralized logging (ELK Stack - Elasticsearch, Logstash, Kibana).

### 118. What are Spring Boot Actuators?

*   **Definition**: Production-ready features to help you monitor and manage your application.
*   **Endpoints**:
    *   `/actuator/health`: Application health status (UP/DOWN).
    *   `/actuator/info`: Application info (version, git commit).
    *   `/actuator/metrics`: varied metrics.
    *   `/actuator/env`: Environment properties.
    *   `/actuator/loggers`: View and modify log levels at runtime.
*   **Security**: Most endpoints are disabled by default (except health/info). Sensitive endpoints should be secured.

### 119. How to expose custom metrics?

*   **Micrometer**: Spring Boot uses Micrometer facade.
*   **Usage**: Inject `MeterRegistry`.
*   **Types**:
    *   **Counter**: Monotonically increasing numbers (e.g., total requests). `registry.counter("my.counter").increment();`
    *   **Gauge**: Instantaneous value (e.g., queue size).
    *   **Timer**: Measures short-duration latencies and frequency.
*   **Annotation**: Use `@Timed` on methods to automatically track execution time.

### 120. How to configure a datasource manually?

*   **Scenario**: When you need multiple datasources or custom connection pooling settings beyond standard properties.
*   **Steps**:
    1.  Define `@Configuration` class.
    2.  Create a `@Bean` returning `DataSource`.
    3.  Use `DataSourceBuilder`:
        ```java
        @Bean
        @ConfigurationProperties(prefix = "app.datasource")
        public DataSource myDataSource() {
            return DataSourceBuilder.create().build();
        }
        ```
    4.  If using JPA, you also need to manually configure `LocalContainerEntityManagerFactoryBean` and `PlatformTransactionManager`.

### 121. What is Spring Data JPA?

*   **Definition**: A part of the Spring Data family that makes it easy to implement JPA-based repositories.
*   **Goal**: To reduce the boilerplate code required to interact with databases.
*   **Features**:
    *   **Repository Support**: Interfaces `CrudRepository`, `JpaRepository`.
    *   **Derived Queries**: Generates SQL automatically from method names (e.g., `findByName`).
    *   **Pagination & Sorting**: Built-in support.
    *   **Auditing**: Automatically tracks `@CreatedDate`, `@LastModifiedDate`.

### 122. What are derived query methods?

*   **Concept**: A feature where Spring Data resolves the query manually by parsing the method name of the repository interface.
*   **Mechanism**: It strips prefixes like `find`, `read`, `query`, parses the remaining string, and maps properties to SQL clauses.
*   **Examples**:
    *   `findByName(String name)` -> `SELECT * FROM User WHERE name = ?`
    *   `findByAgeGreaterThan(int age)` -> `SELECT * FROM User WHERE age > ?`
    *   `findByEmailAndActiveTrue(String email)` -> `SELECT * FROM User WHERE email = ? AND active = true`

### 123. Difference between CrudRepository, JpaRepository, PagingAndSortingRepository.

*   **`CrudRepository`**: The base interface providing generic CRUD operations (save, findById, findAll, delete, count).
*   **`PagingAndSortingRepository`**: Extends `CrudRepository` and adds methods to retrieve entities using **Pagination** (`Pageable`) and **Sorting** (`Sort`).
*   **`JpaRepository`**: Extends `PagingAndSortingRepository` and adds JPA-specific methods like flushing the persistence context (`flush()`) and batch deleting (`deleteInBatch`). This is the most commonly used interface.

### 124. How to handle pagination in Spring Data?

1.  **Repository**: Extend `PagingAndSortingRepository` or `JpaRepository`.
2.  **Request**: Create a `Pageable` object (usually `PageRequest.of(pageNumber, pageSize, Sort)`).
3.  **Method**: Call `findAll(Pageable pageable)`.
4.  **Response**: The method returns a `Page<T>` object, which contains the list of content, total pages, total elements, and current page metadata.

### 125. What is query-by-example (QBE)?

*   **Definition**: A user-friendly querying technique that allows dynamic query creation.
*   **Mechanism**: You create an instance of the entity (the "probe"), populate the fields you want to search for, and pass it to the repository.
*   **Usage**:
    ```java
    User probe = new User();
    probe.setActive(true); // Search for all active users
    Example<User> example = Example.of(probe);
    List<User> users = userRepository.findAll(example);
    ```
*   **Limitation**: Bad for nested/complex queries (OR, grouping). Good for simple filters.

### 126. How to write native queries in JPA?

*   **Annotation**: Use `@Query`.
*   **Attribute**: Set `nativeQuery = true`.
*   **Syntax**: Write actual SQL (database-specific) instead of JPQL.
*   **Example**:
    ```java
    @Query(value = "SELECT * FROM users u WHERE u.email_address = ?1", nativeQuery = true)
    User findByEmailNative(String email);
    ```

### 127. Difference between EntityManager and JdbcTemplate.

*   **`JdbcTemplate`**:
    *   Part of Spring JDBC.
    *   Low-level. You write raw SQL.
    *   You manually map `ResultSet` to Java Objects (`RowMapper`).
    *   No concept of Persistence Context (caching/tracking).
*   **`EntityManager`**:
    *   Part of JPA (Java Persistence API).
    *   High-level. You work with Entities and JPQL.
    *   ORM framework handles mapping.
    *   Uses **Persistence Context** (First-level cache, Dirty Checking).

### 128. What is @EntityGraph?

*   **Problem**: Solves the **N+1 Select Problem**.
*   **Function**: Allows you to define which related entities (associations) should be fetched **Eagerly** in a specific query, overriding the default Lazy loading strategy.
*   **Usage**:
    ```java
    @EntityGraph(attributePaths = {"roles", "address"}) // Eagerly loads roles and address
    User findByEmail(String email);
    ```
*   **Result**: Generates a single `c LEFT JOIN` query.

### 129. What is lazy vs eager loading?

*   **Eager Loading**: Related entities are fetched **immediately** along with the parent entity.
    *   *Default for*: `@ManyToOne`, `@OneToOne`.
    *   *Risk*: Loading too much data (memory impact).
*   **Lazy Loading**: Related entities are fetched **on-demand**, only when you access the getter method (e.g., `user.getOrders()`).
    *   *Default for*: `@OneToMany`, `@ManyToMany`.
    *   *Risk*: **LazyInitializationException** if accessed outside the transaction (session closed).

### 130. How does dirty checking work in JPA?

*   **Concept**: You don't need to explicitly call `save()` to update an entity derived from the database.
*   **Mechanism**:
    1.  When an entity is loaded, the Persistence Context (Hibernate Session) keeps a snapshot of it.
    2.  If you modify the object (e.g., `user.setName("New Name")`) inside a transaction...
    3.  At flush time (commit), Hibernate compares the current object with the initial snapshot.
    4.  If differences are found, it **automatically** generates and executes an `UPDATE` SQL statement.

### 131. What is the N+1 select problem? Solution?

*   **Problem**: A performance issue where the application executes 1 initial query to fetch N parent entities, and then executes N additional queries (one for each parent) to fetch their related children.
    *   *Example*: Fetching 100 Users (1 query). Looping through them and accessing `user.getAddress()` (100 queries). Total = 101 queries.
*   **Solution**: Use **Join Fetch**.
    *   *JPQL*: `SELECT u FROM User u JOIN FETCH u.address`
    *   *EntityGraph*: Use `@EntityGraph` annotation on the repository method.
    *   *Batch Size*: Use configuration `@BatchSize(size = 10)` to load children in batches (IN clause).

### 132. Difference between optimistic and pessimistic locking.

*   **Optimistic Locking**: Assumes conflicts are rare. Does not lock the database row.
    *   *Mechanism*: Uses a version column (`@Version`). Before updating, it checks if the version in the DB matches the version held by the application. If not, throws `OptimisticLockException`.
    *   *Use Case*: High-concurrency read-heavy applications (e.g., ticket booking).
*   **Pessimistic Locking**: Assumes conflicts are likely. Locks the database row for the duration of the transaction.
    *   *Mechanism*: Database-level locks (`SELECT ... FOR UPDATE`). Prevents other transactions from reading/writing until the lock is released.
    *   *Use Case*: Critical financial transactions where data integrity is paramount.

### 133. What is @DynamicUpdate in Hibernate?

*   **Default Behavior**: When updating an entity, Hibernate includes *all* columns in the `UPDATE` SQL statement, even if only one field changed.
*   **@DynamicUpdate**: An annotation that tells Hibernate to generate the `UPDATE` SQL statement dynamically at runtime, including **only the columns that have actually changed**.
*   **Benefit**: Can improve performance if the table has many columns or huge LOBs but only small fields are updated frequently.

### 134. How does @Inheritance work in JPA?

*   **Strategies**: Defined via `@Inheritance(strategy = ...)` on the parent entity.
    1.  **SINGLE_TABLE (Default)**: All classes in the hierarchy map to a single table. A discriminator column (`DTYPE`) distinguishes the subclass. Fastest but allows nulls.
    2.  **JOINED**: The parent and each subclass have their own tables. Subclass tables contain only their specific fields and a foreign key to the parent. Slower (joins needed) but normalized.
    3.  **TABLE_PER_CLASS**: A table is created for every concrete class, containing all fields (inherited + specific). No foreign keys/joins, but `UNION` is needed for polymorphic queries.

### 135. What is a DTO? Why is it used?

*   **Definition**: **D**ata **T**ransfer **O**bject. A plain Java object used to transfer data between software layers (e.g., Controller to Service, or Service to UI).
*   **Purpose**:
    *   **Decoupling**: Decouples the internal database Entity model from the external API contract. Changes to the DB schema don't break the API.
    *   **Security**: Hides sensitive data (e.g., passwords, internal IDs) present in the Entity.
    *   **Optimization**: Bundles data from multiple sources or sends only the necessary fields to reduce payload size.

### 136. How to map DTO to Entity and vice versa?

*   **Manual Mapping**: Write converter methods (e.g., `toEntity()`, `toDto()`) using Getters and Setters. Full control, no overhead, but verbose.
*   **BeanUtils**: `BeanUtils.copyProperties(source, target)`. Uses reflection. Fast to write but slow execution and brittle (matching names required).
*   **Mapper Libraries**: Use libraries like **MapStruct** or **ModelMapper** to automate the mapping process efficiently.

### 137. What is ModelMapper?

*   **Definition**: A Java library that automates the mapping between objects (typically Entity <-> DTO).
*   **Features**: It intelligently maps fields with similar names. It minimizes the manual `setX(getY())` code.
*   **Comparison**:
    *   **ModelMapper**: Runtime reflection-based. Easy to setup, slightly slower.
    *   **MapStruct**: Compile-time code generation. Generate actual mapper implementations. Much faster (close to manual code performance). *MapStruct is generally preferred in modern Spring Boot apps.*

### 138. What are common performance pitfalls in Spring Boot applications?

1.  **N+1 Select Problem**: Fetching related entities in loops.
2.  **Lack of Connection Pooling**: Using default or poorly configured pool settings.
3.  **Memory Leaks**: Improper use of `ThreadLocal`, static collections, or unclosed resources.
4.  **Excessive Logging**: Logging too much data in production synchronously.
5.  **Synchronization Bottlenecks**: Overusing `synchronized` in high-concurrency paths.
6.  **Loading Unnecessary Data**: Fetching full entities when only a summary is needed (use Projections/DTOs).

### 139. How to use Spring Boot with Docker?

1.  **Dockerfile**: Create a `Dockerfile` in the project root.
    ```dockerfile
    FROM eclipse-temurin:17-jdk-alpine
    COPY target/myapp.jar app.jar
    ENTRYPOINT ["java","-jar","/app.jar"]
    ```
2.  **Build**: `docker build -t myapp .`
3.  **Run**: `docker run -p 8080:8080 myapp`
4.  **Optimization**: Use **Layered Jars** (available in Spring Boot 2.3+) to separate dependencies from application code for better caching.

### 140. How to externalize configurations in Spring Boot?

*   **Mechanism**: Spring Boot loads properties from multiple sources in a predefined order of precedence.
*   **Sources (from lowest to highest priority)**:
    1.  `application.properties` / `application.yml` inside the jar.
    2.  `application.properties` outside the jar (in current directory).
    3.  **Environment Variables** (`export SPRING_DATASOURCE_PASSWORD=secret`).
    4.  **Java System Properties** (`-Dserver.port=9090`).
    5.  **Command Line Arguments** (`--server.port=9090`).
*   **Benefit**: Allows deploying the same artifact (jar) to different environments (Dev, QA, Prod) with different configurations without rebuilding.

### 141. What is Spring Config Server?

*   **Definition**: A centralized configuration management tool for distributed systems.
*   **Problem**: In microservices, managing `application.properties` for 100+ services across multiple environments (Dev, QA, Prod) is chaotic.
*   **Solution**:
    *   **Server**: A standalone Spring Boot app that connects to a backend repository (Git, SVN, Vault) where config files are stored.
    *   **Client**: Microservices connect to the Config Server at startup to fetch their configuration.
*   **Benefit**: Changes to configuration (in Git) can be reflected in services without redeploying them (using `@RefreshScope`).

### 142. Difference between Spring Cloud Config and application.yml?

*   **`application.yml`**: Local configuration file packaged **inside** the jar.
    *   *Usage*: Good for monolithic apps or static properties that never change (e.g., app name).
    *   *Drawback*: Changing a property requires rebuilding and redeploying the application.
*   **Spring Cloud Config**: Remote configuration management.
    *   *Usage*: Microservices architecture.
    *   *Benefit*: Externalizes configuration. Allows dynamic updates, versioning (via Git history), and consistency across services.

### 143. How to use Spring Cloud with Eureka?

1.  **Eureka Server**: Create a Spring Boot app with `@EnableEurekaServer`. This acts as the Service Registry (phonebook).
2.  **Eureka Client**: Add `spring-cloud-starter-netflix-eureka-client` to microservices. Annotate main class with `@EnableDiscoveryClient`.
3.  **Registration**: On startup, clients register their instance (IP, Port, AppName) with the Server.
4.  **Discovery**: Services can look up other services by **Application Name** (e.g., `http://USER-SERVICE/users`) instead of hardcoded URLs. RestTemplate/WebClient uses this to load balance requests.

### 144. What is a circuit breaker in Spring Cloud?

*   **Pattern**: Prevents a network or service failure from cascading to other services.
*   **States**:
    *   **CLOSED**: Normal operation. Requests pass through.
    *   **OPEN**: Failure threshold breached (e.g., 50% errors). Requests are blocked immediately (fail-fast), and a fallback response is returned.
    *   **HALF-OPEN**: After a wait duration, a few test requests are allowed to pass. If successful, reset to CLOSED; otherwise, return to OPEN.
*   **Implementation**: Originally **Hystrix** (now in maintenance mode), now **Resilience4j** is the standard.

### 145. What is Spring Cloud Gateway? Difference with Zuul?

*   **Zuul 1**: Built on Servlet 2.5 (blocking I/O). Uses a thread-per-connection model. Good for simple use cases but limits scalability under heavy load.
*   **Spring Cloud Gateway**: Built on Spring WebFlux (Project Reactor) and Netty (non-blocking I/O).
    *   **Features**: Path rewriting, Circuit Breaker integration, Rate Limiting, Predicates (matching requests), and Filters (modifying requests).
    *   *Performance*: Higher throughput and lower resource usage than Zuul 1. It is the recommended gateway in the Spring Cloud ecosystem.

### 146. How to write filters in Spring Gateway?

*   **Global Filters**: Apply to **all** routes.
    *   Implement `GlobalFilter` interface. Good for logging, metrics, or global auth headers.
*   **Gateway Filters**: Apply to **specific** routes.
    *   Implement `GatewayFilterFactory`.
    *   *Example*: A filter that validating a specific header for the Inventory Service only.
    ```java
    return (exchange, chain) -> {
        ServerHttpRequest request = exchange.getRequest();
        // logic...
        return chain.filter(exchange);
    };
    ```

### 147. What is Resilience4j and how is it integrated?

*   **Definition**: A lightweight, standalone fault tolerance library designed for Java 8 and functional programming.
*   **Modules**:
    *   **Circuit Breaker**: Fault tolerance.
    *   **Rate Limiter**: Limits the number of requests in a period.
    *   **Bulkhead**: Limits concurrent calls to a service (isolation).
    *   **Retry**: Automatic retries for failed capabilities.
*   **Integration**: Using `spring-cloud-starter-circuitbreaker-resilience4j`. You can configure it via `application.yml` or Java Config to wrap your service calls.

### 148. What is Sleuth and Zipkin? How do they work?

*   **Problem**: In microservices, a single user request might traverse 5 different services. Debugging a failure is hard because logs are scattered.
*   **Spring Cloud Sleuth** (now Micrometer Tracing):
    *   Adds **Trace ID** (unique for the whole chain) and **Span ID** (unique for a single service hop) to logs.
    *   Allows you to correlate logs across services for a single request.
*   **Zipkin**:
    *   A distributed tracing system.
    *   Sleuth sends timing data to Zipkin Server.
    *   Zipkin UI visualizes the call graph, showing latency and dependencies (e.g., "Service A took 50ms, called Service B which took 200ms").

### 149. What is Spring Retry?

*   **Definition**: A library that provides declarative retry support for Spring applications.
*   **Usage**:
    1.  Add `@EnableRetry` to configuration.
    2.  Annotate a method with `@Retryable`.
    3.  Define recovery logic with `@Recover`.
*   **Example**:
    ```java
    @Retryable(value = RemoteServiceException.class, maxAttempts = 3, backoff = @Backoff(delay = 1000))
    public String callRemote() { ... }
    
    @Recover
    public String recover(RemoteServiceException e) { return "Fallback"; }
    ```

### 150. What are distributed transactions and how to manage them in Spring?

*   **Definition**: A transaction that spans multiple services/databases. ACID is hard to guarantee across microservices (CAP theorem).
*   **Approaches**:
    1.  **Two-Phase Commit (2PC / XA)**: Traditional, blocking, and heavy. Not recommended for modern microservices due to performance and availability impact.
    2.  **Saga Pattern (Recommended)**: A sequence of local transactions. Each service updates its own DB and publishes an event to trigger the next step.
        *   **Choreography**: Event-based (Services listen to queues).
        *   **Orchestration**: Central coordinator (e.g., Camunda, generic code) directs the flow.
        *   **Compensation**: If a step fails, "compensating transactions" (undo logic) are triggered to reverse previous changes (e.g., "Refund Payment" if "Ship Item" fails).

### 151. What is Saga Pattern?

*   **Definition**: A design pattern for managing data consistency across microservices in distributed transaction scenarios.
*   **Problem**: A single business process (e.g., "Book Trip") spans multiple services (Flight, Hotel, Car). Traditional ACID transactions (2PC) don't scale.
*   **Solution**: Break the transaction into a sequence of local transactions.
    *   **Forward Recovery**: If a step fails, retry it.
    *   **Backward Recovery (Compensation)**: If a step fails, execute a series of compensating transactions to undo the changes made by previous steps (e.g., "Cancel Flight" if "Book Hotel" fails).

### 152. How to implement service discovery?

*   **Client-Side Discovery**: The client (e.g., API Gateway) queries the Service Registry (Eureka) to get the list of available service instances and selects one (load balancing).
    *   *Tools*: Netflix Eureka, Ribbon (Client Load Balancer).
*   **Server-Side Discovery**: The client makes a request to a load balancer (e.g., AWS ELB, NGINX), which then queries the Service Registry and routes the request.
    *   *Tools*: AWS ELB, Kubernetes Service (K8s DNS).

### 153. Difference between Ribbon and Spring Cloud LoadBalancer?

*   **Ribbon**:
    *   Part of Netflix OSS.
    *   Client-side load balancer.
    *   **Blocking**: Built on blocking I/O (not suitable for WebFlux).
    *   **Status**: Maintenance mode.
*   **Spring Cloud LoadBalancer**:
    *   Spring's own replacement for Ribbon.
    *   Supports both blocking (RestTemplate) and non-blocking (WebClient) applications.
    *   Integrates with Service Discovery (Eureka, Consul) or allows static lists.

### 154. What is Hystrix? Why is it deprecated?

*   **Hystrix**: A latency and fault tolerance library from Netflix (Circuit Breaker implementation). It stopped cascading failures and provided fallback options.
*   **Deprecation**: Netflix put Hystrix into maintenance mode.
*   **Reasons**: It was built on RxJava 1 (End of Life) and uses a lot of AOP/Threads which can be heavy.
*   **Replacement**: **Resilience4j**. It is lightweight, built on functional interfaces, modular (pick only what you need), and compatible with standard Java 8 styles.

### 155. What is FeignClient and how does it work?

*   **Definition**: A declarative web service client. It makes writing web clients easier.
*   **Mechanism**:
    1.  Create an Interface.
    2.  Annotate it with `@FeignClient(name = "user-service")`.
    3.  Define methods mapped to REST endpoints using Spring MVC annotations (`@GetMapping("/users/{id}")`).
*   **Magic**: At runtime, Spring creates a dynamic proxy implementation of this interface that uses an underlying HTTP client (like Apache HttpClient or OkHttp) to make the actual network call, handling serialization/deserialization automatically.

### 156. Difference between OpenFeign and RestTemplate?

*   **RestTemplate**:
    *   Imperative style.
    *   Requires boilerplate code to construct URLs, headers, and request bodies manually.
    *   Harder to unit test.
*   **OpenFeign**:
    *   Declarative style (Interface-driven).
    *   Cleaner code; looks like a local method call.
    *   Built-in support for Load Balancing (Eureka integration) and Circuit Breaking (Resilience4j integration).

### 157. How does OAuth2 work with Spring Security?

*   **Roles**:
    *   **Resource Owner**: User.
    *   **Client**: The application trying to access data.
    *   **Authorization Server**: Issues tokens (e.g., Keycloak, Auth0, Google).
    *   **Resource Server**: The API hosting the data.
*   **Spring Security**:
    *   **Client Support**: `spring-boot-starter-oauth2-client` handles the login flow (e.g., "Login with Google") and token acquisition.
    *   **Resource Server Support**: `spring-boot-starter-oauth2-resource-server` handles validating the Access Token (usually JWT) sent by the client in the Authorization header.

### 158. What is JWT? How is it integrated with Spring Boot?

*   **JWT**: JSON Web Token. A compact, URL-safe means of representing claims to be transferred between two parties.
*   **Structure**: Header.Payload.Signature.
*   **Integration**:
    1.  **Dependency**: `spring-boot-starter-oauth2-resource-server`.
    2.  **Config**: In `SecurityFilterChain`, configure `.oauth2ResourceServer(oauth2 -> oauth2.jwt())`.
    3.  **Validation**: Spring Security automatically decodes the JWT, verifies the signature (using the Public Key from the Auth Server), checks expiration, and extracts authorities (roles).

### 159. How to secure microservices with API Gateway?

*   **Pattern**: The API Gateway acts as the single entry point and security enforcement point (Unified Security).
*   **Implementation**:
    1.  **Authentication**: The Gateway validates the Access Token (JWT) on the incoming request. If valid, it forwards the request to the downstream microservice.
    2.  **Token Relay**: The Gateway passes the token to the microservice (in the `Authorization` header) so the service knows *who* is making the request.
    3.  **Scope/Role Checks**: The Gateway can enforce coarse-grained access control (e.g., only "admin" scope can hit `/admin/**`).

### 160. What is Spring Session?

*   **Problem**: In a clustered environment (multiple instances of a service), standard HttpSession is stored in the memory of a single server. If a user's next request hits a different server, they are logged out (Session Stickiness is a hacky fix).
*   **Spring Session**: An API and implementation to manage user session information.
*   **Solution**: It replaces the `HttpSession` implementation with one that stores session data in a **shared external store** like Redis, JDBC, or MongoDB.
*   **Result**: Session clustering becomes transparent. Any server instance can handle the user's request.

### 161. How to implement rate limiting in Spring Boot?

*   **Mechanism**: Restricting the number of requests a user/client can make within a certain timeframe (e.g., 60 requests/minute) to prevent abuse or overload.
*   **Libraries**:
    1.  **Bucket4j**: A Java rate-limiting library based on the Token Bucket algorithm. Highly performant.
    2.  **Resilience4j RateLimiter**: Integrated with Spring Cloud Circuit Breaker.
    3.  **Spring Cloud Gateway RequestRateLimiter**: Uses Redis (Lua scripts) to manage counters across distributed instances.

### 162. What is service registry and how does it help?

*   **Definition**: A dynamic database containing the network locations (IP and Port) of all available service instances.
*   **Problem**: In microservices, instances are ephemeral (they spin up/down with dynamic IPs). Hardcoding URLs is impossible.
*   **Solution**: Services register themselves with the registry (e.g., Eureka, Consul) on startup. Clients query the registry to find the address of a service to call.
*   **Benefit**: Enables client-side load balancing and decoupling.

### 163. How to trace a request across multiple services?

*   **Distributed Tracing**: Assigning a unique ID to a request chain.
*   **Tools**: **Spring Cloud Sleuth** (Micrometer Tracing) and **Zipkin** (or Jaeger).
*   **Mechanism**:
    1.  **Trace ID**: A unique ID generated at the entry point (Gateway/First Service). Passed via HTTP headers (e.g., `b3` or `traceparent`) to all downstream services.
    2.  **Span ID**: A unique ID for each individual unit of work (hop).
    3.  **Aggregation**: Logs/metrics are sent to a centralized server (Zipkin) to visualize the timeline.

### 164. How to implement custom starter in Spring Boot?

1.  **Create Project**: A standard Maven/Gradle project (e.g., `my-library-spring-boot-starter`).
2.  **Dependencies**: `spring-boot-autoconfigure`.
3.  **AutoConfiguration Class**: Write a class annotated with `@Configuration`. Use `@ConditionalOnClass` or `@ConditionalOnProperty` to control when beans are created.
4.  **Register**: Create `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` (Spring Boot 2.7+) or `spring.factories` (older) and list your configuration class.
5.  **Usage**: Other apps just add your starter as a dependency, and the beans are automatically configured.

### 165. How to test Spring Boot applications?

*   **`spring-boot-starter-test`**: The primary dependency. It brings in:
    *   **JUnit 5**: The testing framework.
    *   **Mockito**: For mocking dependencies.
    *   **MockMvc**: For testing web layers.
    *   **AssertJ**: For fluent assertions.
*   **Attributes**:
    *   `@SpringBootTest`: Loads the full ApplicationContext (integration test).
    *   `@WebMvcTest`: Loads only the web layer (controller test).
    *   `@DataJpaTest`: Loads only the JPA layer (repository test).

### 166. What is MockMvc and when to use it?

*   **Definition**: A utility class that allows you to send mock HTTP requests to your Controllers *without* starting a full HTTP server (Tomcat).
*   **Usage**: Unit testing Controllers.
*   **Mechanism**: It invokes the DispatcherServlet directly. You can chain expectations:
    ```java
    mockMvc.perform(get("/users/1"))
           .andExpect(status().isOk())
           .andExpect(jsonPath("$.name").value("John"));
    ```

### 167. How to mock external services in integration tests?

*   **`@MockBean`**: Used to replace a real bean (e.g., `EmailService`, `PaymentGateway`) in the Spring ApplicationContext with a Mockito mock.
    *   *Example*: `given(externalService.call()).willReturn("Mock Response");`
*   **WireMock**: A library to mock an actual HTTP server. Used when your service uses `RestTemplate` or `WebClient` to call an external API. WireMock spins up a lightweight server that returns canned responses.

### 168. What is @DataJpaTest?

*   **Definition**: A "slice test" annotation for testing JPA components.
*   **Features**:
    *   Loads only JPA-related beans (Repositories, EntityManager). Does *not* load Controllers or Services.
    *   Configures an **in-memory database** (H2/HSQL) by default, replacing your real DB configuration.
    *   Automatically **rolls back** transactions at the end of each test to keep the DB clean.

### 169. What is TestContainers and how to use with Spring Boot?

*   **Definition**: A Java library that supports JUnit tests specifically by providing lightweight, throwaway instances of common databases, Selenium web browsers, or anything else that can run in a **Docker container**.
*   **Use Case**: True Integration Testing. Instead of using H2 (which behaves differently than Postgres/MySQL), you spin up a *real* Postgres Docker container for the duration of the test.
*   **Usage**: Annotated with `@Container` and `@Testcontainers`.

### 170. What is the difference between Unit Test and Integration Test in Spring?

*   **Unit Test**:
    *   Tests a single class/method in isolation.
    *   Dependencies are **Mocked** (using Mockito).
    *   Fast execution.
    *   Does NOT load the Spring Context.
*   **Integration Test**:
    *   Tests the interaction between multiple components (e.g., Controller + Service + DB).
    *   Dependencies are **Real** (or selectively mocked).
    *   Slower execution.
    *   Loads the Spring Context (`@SpringBootTest`).

### 171. How is a microservice different from a monolith?

*   **Monolith**:
    *   **Single Unit**: Entire application is built as a single deployable artifact (WAR/JAR).
    *   **Shared Database**: Usually connects to one large database.
    *   **Scaling**: Scales by cloning the entire application (vertical scaling or duplicating instances).
    *   **Technology Stack**: Uniform across the application.
*   **Microservices**:
    *   **Distributed**: Application is broken down into small, independent services.
    *   **Decentralized Data**: Each service manages its own database (Database-per-service pattern).
    *   **Scaling**: Individual services can be scaled independently based on demand.
    *   **Technology Stack**: Each service can use different technologies/languages (Polyglot).

### 172. What are the advantages and disadvantages of microservices?

*   **Advantages**:
    *   **Agility**: Smaller teams can work on services independently.
    *   **Scalability**: Targeted scaling of hot services.
    *   **Resilience**: Failure in one service doesn't necessarily bring down the whole system.
    *   **Technology Freedom**: Can use the best tool for the job.
*   **Disadvantages**:
    *   **Complexity**: Distributed systems are inherently harder to develop, test, and deploy.
    *   **Data Consistency**: Achieving consistency across services is difficult (need Saga/Eventual Consistency).
    *   **Network Latency**: Inter-service communication adds latency.
    *   **Operational Overhead**: Requires mature DevOps (CI/CD, Monitoring, Logging).

### 173. How do microservices communicate?

*   **Synchronous (Blocking)**:
    *   **HTTP/REST**: Most common. Use `RestTemplate` or `WebClient` or `Feign`.
    *   **gRPC**: High-performance, binary protocol (Google).
*   **Asynchronous (Non-blocking)**:
    *   **Message Queues**: RabbitMQ, ActiveMQ. Point-to-point or Publish-Subscribe.
    *   **Event Streams**: Apache Kafka. Log-based storage for high throughput.

### 174. What is service discovery?

*   **Definition**: A pattern that allows services to find each other without hardcoding hostnames and ports.
*   **Mechanism**:
    1.  **Registration**: Services register their network location (IP/Port) with a **Service Registry** upon startup.
    2.  **Discovery**: Clients query the Registry to get the location of a service to call.
    3.  **Health Checks**: The Registry monitors the health of instances and removes unhealthy ones.

### 175. What is Eureka and how does it work?

*   **Eureka**: A REST-based service registry provided by Netflix (part of Spring Cloud Netflix).
*   **Server**: The Registry itself.
*   **Client**: The microservices.
*   **Heartbeat**: Clients send a heartbeat (renew) every 30 seconds to the server. If the server doesn't receive a heartbeat for 90 seconds, it removes the instance from the registry.
*   **Caching**: Clients cache the registry information locally, so they can still function if the Eureka Server goes down temporarily (AP system).

### 176. What is API Gateway in microservices?

*   **Definition**: A server that acts as the single entry point for all clients (Mobile, Web, 3rd Party) into the microservices system.
*   **Functions**:
    *   **Routing**: Forwards requests to the appropriate service.
    *   **Cross-Cutting Concerns**: Authentication, SSL Termination, Rate Limiting, Logging, CORS.
    *   **Protocol Translation**: Can convert HTTP to gRPC/AMQP.
    *   **Backend for Frontend (BFF)**: Aggregating multiple service calls into one response for the client.

### 177. How does Spring Cloud Gateway work?

*   **Architecture**: Built on Spring WebFlux (Reactor) and Netty for non-blocking I/O.
*   **Route**: The basic building block. Defined by an ID, a Destination URI, a collection of Predicates, and a collection of Filters.
*   **Predicate**: Matches the incoming request (e.g., Path matches `/users/**`, Header contains `X-Tech`).
*   **Filter**: Modifies the request or response (e.g., Add Request Header, Strip Path Prefix, Circuit Breaker).

### 178. What are edge services?

*   **Definition**: Services that sit at the boundary (edge) of your internal network and the public internet.
*   **Role**: They are the first line of defense and traffic management.
*   **Examples**:
    *   **API Gateway**: (Zuul, Spring Cloud Gateway).
    *   **Authorization Server**: (OAuth2 Server).
    *   **WAF (Web Application Firewall)**.
    *   **CDN (Content Delivery Network)**.

### 179. Explain the importance of bounded contexts in microservices.

*   **Origin**: A core concept from **Domain-Driven Design (DDD)**.
*   **Definition**: A logical boundary within which a specific domain model is defined and applicable. The terms and concepts inside a bounded context have specific meanings that might differ outside.
*   **Microservices**: Ideal candidates for microservice boundaries.
    *   *Example*: In an E-commerce system, "Product" in the "Catalog Context" (rich description, images) is different from "Product" in the "Inventory Context" (SKU, quantity, location). Instead of one giant `Product` class, you have two smaller, focused models in separate services.

### 180. What is domain-driven design (DDD)?

*   **Definition**: A software design approach that focuses on modeling the software to match the complex domain (business) logic.
*   **Strategic Design**:
    *   **Ubiquitous Language**: A common language shared by developers and domain experts.
    *   **Bounded Contexts**: Defining boundaries.
*   **Tactical Design**:
    *   **Entity**: Object with identity (ID).
    *   **Value Object**: Object defined by its attributes (immutable, no ID).
    *   **Aggregate**: A cluster of domain objects treated as a single unit.
    *   **Repository**: Abstraction for retrieving aggregates.

### 181. What is the difference between orchestration and choreography in microservices?

*   **Orchestration (Centralized Control)**:
    *   **Concept**: A central coordinator (the orchestrator) tells each service what to do.
    *   **Analogy**: An Orchestra Conductor.
    *   **Pros**: Centralized logic, easy to track flow.
    *   **Cons**: Single point of failure, tight coupling.
*   **Choreography (Decentralized Coordination)**:
    *   **Concept**: Each service listens to events and decides what to do. Services react to each other.
    *   **Analogy**: Dancers following the music.
    *   **Pros**: Loose coupling, no central bottleneck.
    *   **Cons**: Harder to track/debug the entire flow (distributed logic).

### 182. What is a distributed transaction?

*   **Definition**: A database transaction that spans two or more network hosts (databases/services).
*   **Challenge**: Ensuring ACID properties (Atomicity, Consistency, Isolation, Durability) across distributed nodes is extremely difficult due to network unreliability (CAP Theorem - Partition Tolerance).
*   **Standard**: XA (eXtended Architecture) used for 2-Phase Commit (2PC). Heavily impacting performance and availability, so often avoided in microservices in favor of eventual consistency.

### 183. How do you achieve eventual consistency?

*   **Concept**: The system guarantees that if no new updates are made to a given data item, eventually all accesses to that item will return the last updated value.
*   **Mechanism**:
    *   **Asynchronous Messaging**: Service A updates its DB and publishes an event ("OrderCreated"). Service B consumes the event and updates its DB (Inventory). There is a lag, but data syncs eventually.
    *   **Reconciliation Jobs**: Background baches that scan for inconsistencies and fix them.

### 184. Explain the Saga pattern with example.

*   **Pattern**: A sequence of local transactions. Each local transaction updates the database and publishes a message/event to trigger the next local transaction in the saga.
*   **Example (Booking a Trip)**:
    1.  **Transaction 1**: `BookFlight` service books a seat. (Success -> publish `FlightBooked`)
    2.  **Transaction 2**: `BookHotel` service reserves a room. (Success -> publish `HotelBooked`, Failure -> trigger `CancelFlight`)
    3.  **Transaction 3**: `ProcessPayment` service charges card. (Failure -> trigger `CancelHotel` then `CancelFlight`)

### 185. How would you handle inter-service communication failures?

*   **Timeouts**: Set strict timeouts so the caller doesn't wait forever, freeing up resources.
*   **Retries**: Automatically retry failed requests (with exponential backoff) for transient errors (network blips).
*   **Circuit Breaker**: Stop calling a failing service to give it time to recover.
*   **Fallbacks**: Return default data or a cached response when the service is unavailable.
*   **Bulkheads**: Isolate resources (thread pools) so a failure in one part doesn't take down the whole system.

### 186. What is circuit breaker pattern?

*   **Concept**: Modeled after an electrical circuit breaker. It detects failures and encapsulates the logic of preventing a failure from constantly recurring (during maintenance, temporary external system failure or unexpected system difficulties).
*   **States**:
    *   **Closed**: Requests flow normally. Counters track failures.
    *   **Open**: Failure threshold reached. Requests fail immediately (Fast Fail).
    *   **Half-Open**: A trial state. Allow limited requests to check if the issue is resolved.

### 187. How does Resilience4j work?

*   **Decorators**: It heavily uses the **Decorator Pattern** and functional interfaces specific to Java 8.
*   **Usage**: You wrap a `Supplier`, `Function`, or `Runnable` with a Circuit Breaker, Rate Limiter, or Retry decorator.
*   **Integration**: In Spring Boot, `spring-cloud-circuitbreaker-resilience4j` provides annotations (`@CircuitBreaker`, `@Retry`) and configuration properties to apply these patterns declaratively.

### 188. What is rate limiting? How do you implement it?

*   **Definition**: Controlling the rate of traffic sent or received by a network interface controller. It prevents DoS attacks and resource starvation.
*   **Algorithms**:
    *   **Token Bucket**: Tokens are added to a bucket at a fixed rate. Requests need a token to proceed.
    *   **Leaky Bucket**: Requests enter a queue and are processed at a constant rate.
    *   **Fixed Window**: Limit requests per fixed time block (e.g., 100 req/min).
*   **Implementation**: Can be done at Gateway (Spring Cloud Gateway with Redis) or Service level (Resilience4j RateLimiter).

### 189. How to design idempotent APIs?

*   **Idempotency**: Making multiple identical requests has the same effect as making a single request.
*   **Methods**:
    *   **GET, PUT, DELETE**: Inherently idempotent (by HTTP spec). `PUT /users/1` with `{name: "A"}` always results in the user's name being "A", no matter how many times called.
    *   **POST**: Not inherently idempotent. `POST /orders` creates a new order every time.
*   **Solution for POST**:
    *   Client generates a unique **Idempotency Key** (UUID) and sends it in the header.
    *   Server checks if it has already processed a request with that key. If yes, return the cached response; if no, process and save the key.

### 190. What is a fallback method in circuit breaker?

*   **Definition**: A method that is executed when the main business logic fails (throws an exception) or when the circuit is OPEN.
*   **Purpose**: To provide a graceful degradation of service. instead of throwing a 500 Internal Server Error, the system returns a default value, a friendly message, or data from a cache.
*   **Requirement**: The fallback method signature must accept the same parameters as the original method plus the Exception that caused the failure.

### 191. What is load balancing? Types?

*   **Definition**: The process of distributing network traffic across multiple servers (instances) to ensure no single server bears too much load.
*   **Types**:
    *   **Layer 4 (Transport Layer)**: Balancing based on IP and Port (e.g., TCP connections). Fast and efficient but limited context.
    *   **Layer 7 (Application Layer)**: Balancing based on HTTP headers, URLs, Cookies, or Data. More intelligent routing but slightly slower.

### 192. Difference between client-side and server-side load balancing.

*   **Server-Side (Traditional)**:
    *   The client sends a request to a Load Balancer (ELB, NGINX).
    *   The Load Balancer determines which server to forward the request to.
    *   *Pros*: Simple client.
    *   *Cons Single point of failure (if not HA), extra hop.*
*   **Client-Side (Microservices)**:
    *   The client queries the Service Registry to get a list of available instances.
    *   The client itself selects an instance (using Round Robin, Random, etc.) and makes the call directly.
    *   *Pros*: No extra hop, resilient.
    *   *Cons*: Complex client logic (Ribbon/Feign).

### 193. What is Ribbon? Is it still used?

*   **Ribbon**: A client-side load balancer library from Netflix OSS. It was the standard in early Spring Cloud versions.
*   **Status**: Maintenance mode (Deprecated).
*   **Reason**: Blocking API design and tight coupling with the Netflix stack.
*   **Replacement**: **Spring Cloud LoadBalancer**.

### 194. What is Spring Cloud LoadBalancer?

*   **Definition**: The modern, official replacement for Ribbon in the Spring ecosystem.
*   **Technology**: Built with Spring Framework primitives.
*   **Features**:
    *   Supports reactive (non-blocking) and imperative (blocking) applications.
    *   Pluggable algorithms (RoundRobin is default).
    *   Service Discovery integration (Eureka, Consul, K8s).
    *   Integrates seamlessly with `WebClient` and `RestTemplate`.

### 195. What is API versioning and how to implement it?

*   **Definition**: Managing changes to your API so that existing clients don't break when you release new features.
*   **Implementation Strategies**:
    1.  **URI Versioning**: `/v1/users` vs `/v2/users`. (Most common, easy to cache/route).
    2.  **Request Param**: `/users?version=1`.
    3.  **Header Versioning**: Custom header `X-API-VERSION: 1`.
    4.  **Content Negotiation (Accept Header)**: `Accept: application/vnd.company.app-v1+json`. (RESTful but complex).

### 196. How to secure microservices using OAuth2?

1.  **Authorization Server**: Set up a centralized Identity Provider (IdP) like Keycloak, Okta, or a custom Spring Auth Server. It issues tokens.
2.  **Resource Server**: Configure microservices as Resource Servers. They trust the IdP.
3.  **Flow**:
    *   Client logs in via IdP -> Gets Access Token (JWT).
    *   Client calls Microservice A with `Authorization: Bearer <token>`.
    *   Microservice A validates the token (signature/expiration) and grants access based on scopes/roles.

### 197. What is JWT? How to use it in microservices?

*   **JWT (JSON Web Token)**: A stateless token containing JSON claims (User ID, Roles, Expiry).
*   **Usage**:
    *   **Stateless Ops**: Services don't need to query a central database to validate the user session (sessionless).
    *   **Validation**: Services only need the **Public Key** of the Authorization Server to verify the token's signature.
    *   **Information**: Can carry user context (email, role) inside the payload, reducing database lookups.

### 198. What is token propagation?

*   **Problem**: User calls Service A -> Service A calls Service B. Service B needs to know *who* the user is to enforce security.
*   **Solution**: Service A must "propagate" (forward) the incoming Access Token to Service B.
*   **Implementation**: Use a `FeignRequestInterceptor` or `WebClient` filter to extract the `Authorization` header from the incoming request context and inject it into the outgoing request to Service B.

### 199. How do you handle secrets in microservices?

*   **Anti-Pattern**: Hardcoding passwords in code or `application.properties` committed to Git.
*   **Best Practices**:
    1.  **Environment Variables**: Inject secrets at runtime.
    2.  **Spring Cloud Config Server**: Encrypt values in the Git repo (using JCE) and decrypt them on the fly provided by the Config Server.
    3.  **Vault (HashiCorp)**: A dedicated secret management tool. Integrates with Spring Cloud Vault to fetch dynamic secrets on startup/refresh.

### 200. What is config server? (Context: Security)

*   (This question reiterates Q141 but with a focus on security/secrets).
*   **Security Role**: A centralized place to store configuration, including **secrets**.
*   **Encryption**: It supports encrypting property values (`{cipher}FK83...`) so that sensitive data is encrypted at rest (in Git) and only decrypted in the memory of the application or the config server itself.

### 201. How to refresh config without restarting services?

*   **Mechanism**:
    1.  Ensure the bean consuming the property is annotated with `@RefreshScope`.
    2.  Update the value in the Git repostiory hooked to Config Server.
    3.  Trigger the refresh:
        *   **Manual**: POST to `/actuator/refresh` endpoint on the service.
        *   **Bus**: Use **Spring Cloud Bus** (with RabbitMQ/Kafka). POST to `/actuator/bus-refresh`. This broadcasts an event to all services to refresh their config automatically.

### 202. What is bootstrap.yml vs application.yml?

*   **`application.yml`**:
    *   Loaded by the standard Spring Boot context.
    *   Used for general configurations.
*   **`bootstrap.yml`**:
    *   Loaded by a parent context (Bootstrap Context) *before* `application.yml`.
    *   **Usage**: Configuring the **Config Server** location (`spring.cloud.config.uri`). The application needs this URL *first* to fetch the rest of its configuration (which replaces/overrides `application.yml`).
    *   *Note*: In Spring Cloud 2020+, `bootstrap.yml` is deprecated in favor of `spring.config.import` in `application.yml`.

### 203. What is centralized logging?

*   **Problem**: In microservices, logs are scattered across 50 servers. SSHing into each to `grep` errors is impossible.
*   **Solution**: Ship all logs to a central location for indexing and searching.
*   **Stack (ELK)**:
    *   **Filebeat**: Agent on the server that forwards log files.
    *   **Logstash**: Ingests, parses, and transforms logs.
    *   **Elasticsearch**: Stores and indexes logs (Search Engine).
    *   **Kibana**: UI to visualize and search logs.
*   **Alternatives**: Splunk, Graylog, Datadog.

### 204. How does distributed tracing work?

*   **Concept**: Reconstructing the path of a request as it travels across multiple microservices.
*   **Mechanism**:
    *   A **Trace ID** is generated at the edge (Gateway).
    *   This ID is passed in HTTP headers (`X-B3-TraceId`) to every downstream service.
    *   Each service logs this ID along with its own logs.
    *   A tracing system aggregates all logs with the same Trace ID to verify the flow and latency.

### 205. What is Sleuth? What is Zipkin?

*   **Spring Cloud Sleuth**:
    *   The **Instrumentation** library.
    *   It automatically adds Trace IDs and Span IDs to your logs (SLF4J/MDC).
    *   It injects these IDs into HTTP headers for outgoing calls (RestTemplate/Feign).
*   **Zipkin**:
    *   The **Visualization** server.
    *   Sleuth sends timing data to Zipkin (via HTTP or Kafka).
    *   Zipkin shows a Gantt chart of the request: "Service A (50ms) -> Service B (200ms) -> Database (10ms)".

### 206. What are span and trace IDs?

*   **Trace ID**:
    *   Unique identifier for the **entire** request chain (End-to-End).
    *   Stays the same across all services for that request.
*   **Span ID**:
    *   Unique identifier for a **single** unit of work (e.g., Service A calling Service B).
    *   Changes with every hop.
    *   Spans have a Parent-Child relationship to form a tree.

### 207. What is an anti-corruption layer?

*   **Context**: Domain-Driven Design (DDD) & Legacy Migration.
*   **Problem**: When a new modern microservice needs to integrate with a messy legacy system (monolith) that has a confusing domain model.
*   **Solution**: Build a layer (adapter/facade) between them.
    *   It translates the Legacy Model into the Modern Model (and vice versa).
    *   It ensures the core domain logic of the new service remains clean and unpolluted by legacy concepts.

### 208. What is the database-per-service pattern?

*   **Definition**: Each microservice has its **own private database** (or schema).
*   **Rule**: No other service can access this database directly. They must use the service's API.
*   **Pros**:
    *   Loose coupling.
    *   Service A can change its DB schema without breaking Service B.
    *   Polyglot persistence (Service A uses SQL, Service B uses MongoDB).
*   **Cons**:
    *   Complex queries (Joins) across services are impossible (Requires API composition).
    *   Distributed transactions (Requires Sagas).

### 209. What are shared-nothing architectures?

*   **Definition**: A distributed computing architecture where each node (server) is independent and self-sufficient.
*   **Characteristics**:
    *   No shared memory.
    *   No shared disk storage (usually).
    *   Communication solely via the network.
*   **Benefit**: Infinite horizontal scalability. Since nodes don't contend for shared resources (locks), adding more nodes linearly increases capacity. Microservices are typically shared-nothing.

### 210. What is CQRS? When to use it?

*   **CQRS**: **C**ommand **Q**uery **R**esponsibility **S**egregation.
*   **Concept**: Separating the model for **Reading** (Query) from the model for **Writing** (Command).
    *   *Standard*: Use same Entity for Save and Get.
    *   *CQRS*:
        *   **Command Model**: Optimized for validation and logic (e.g., highly normalized). Writes to the Primary DB.
        *   **Query Model**: Optimized for reading (e.g., denormalized DTOs). Reads from a Read Replica or Search Index (Elasticsearch).
*   **Usage**: High-traffic systems where Read load >> Write load, or where read queries are complex and slow on the write model.

### 211. What is Event Sourcing?

*   **Traditional**: Store the *current state* of an entity (e.g., `Order: {status: SHIPPED}`).
*   **Event Sourcing**: Store the *sequence of events* that led to the current state (e.g., `OrderCreated`, `OrderPaid`, `OrderShipped`).
*   **Replay**: The current state is derived by replaying all events from the beginning.
*   **Pros**: Complete audit trail, ability to travel back in time (debug), flexible state reconstruction.
*   **Cons**: Complexity (Requires Event Store), eventual consistency, snapshotting needed for performance.

### 212. What is a sidecar pattern?

*   **Definition**: Deploying a helper service (container) alongside your main application container in the same Pod (Kubernetes term).
*   **Purpose**: To abstract infrastructure concerns away from the main application.
*   **Examples**:
    *   **Proxy Sidecar**: (Envoy, Linkerd) Handles networking, SSL, retries, metrics.
    *   **Logging Sidecar**: (Fluentd) Collects logs from the app and ships them to ELK.
    *   **Config Sidecar**: Watched for config changes and updates the app.

### 213. What is service mesh? What tools are used?

*   **Definition**: A dedicated infrastructure layer for handling service-to-service communication.
*   **Architecture**: It injects a **Sidecar Proxy** (Data Plane) next to every microservice instance. A central **Control Plane** manages the configuration of these proxies.
*   **Features**: Traffic management (Blue/Green deploy), Security (mTLS), Observability (Metrics/Tracing) without changing application code.
*   **Tools**: **Istio**, **Linkerd**, **Consul Connect**.

### 214. What is Istio and Linkerd?

*   **Istio**: The most feature-rich (and complex) Service Mesh. Backed by Google/IBM. Uses **Envoy** as the sidecar proxy.
*   **Linkerd**: A lighter, faster, Kubernetes-native Service Mesh. Focuses on simplicity and performance. Uses a Rust-based micro-proxy.
*   **Comparison**: Istio is the "enterprise" choice (more knobs); Linkerd is the "developer" choice (easier to run).

### 215. How do you monitor microservices?

*   **Metrics**: CPU, Memory, Latency, Error Rates (Golden Signals). Collected via Prometheus.
*   **Logging**: Centralized logs (ELK/Splunk).
*   **Tracing**: Distributed tracing (Jaeger/Zipkin) to follow requests.
*   **Health Checks**: Liveness and Readiness probes.
*   **Alerting**: Sending notifications (PagerDuty, Slack) when thresholds are breached.

### 216. What is Prometheus and Grafana?

*   **Prometheus**:
    *   A monitoring system and time-series database.
    *   **Pull Model**: It scrapes metrics from application endpoints (`/actuator/prometheus`) at regular intervals.
    *   Stores data efficiently and offers a query language (PromQL).
*   **Grafana**:
    *   A visualization tool.
    *   Connects to data sources (Prometheus, MySQL, Elasticsearch).
    *   Allows creating rich dashboards (Graphs, Gauges, Heatmaps) to visualize the metrics stored in Prometheus.

### 217. What are metrics and observability?

*   **Metrics**: Quantitative data (numbers) measured over time (e.g., "Requests per second = 50"). Good for detecting *that* something is wrong.
*   **Observability**: A superset. It's the ability to ask arbitrary questions about your system to understand *why* it is behaving that way.
*   **Three Pillars of Observability**:
    1.  **Metrics**: "Is it slow?"
    2.  **Logs**: "What happened?" (Textual events).
    3.  **Traces**: "Where did it happen?" (Context/Path).

### 218. What is health check API?

*   **Definition**: An endpoint (usually `/health`) that returns the operational status of the service.
*   **Types**:
    *   **Liveness**: "Am I alive?" If NO, the orchestrator (K8s) kills and restarts the container. (Checks: Deadlocks, memory leaks).
    *   **Readiness**: "Am I ready to accept traffic?" If NO, the load balancer stops sending traffic to this instance. (Checks: DB connection, cache warming).

### 219. How to perform health checks in Spring Boot?

*   **Spring Boot Actuator**: Provides `/actuator/health` out of the box.
*   **Custom Indicators**: Use `HealthIndicator` interface to add custom checks.
    ```java
    @Component
    public class MyServiceHealth implements HealthIndicator {
        @Override
        public Health health() {
            if (checkExternalService()) return Health.up().build();
            return Health.down().withDetail("Error", "Service Unavailable").build();
        }
    }
    ```

### 220. How do you debug issues in a distributed environment?

1.  **Correlation ID (Trace ID)**: Essential to filter logs across all services for a specific request.
2.  **Centralized Logging**: Search for the Error/Exception in Kibana using the Trace ID.
3.  **Distributed Tracing**: Look at the Zipkin/Jaeger trace to identify which service failed or was slow.
4.  **Metrics**: Check Grafana dashboards for spikes in latency or error rates around that time.
5.  **Reproduce**: Try to isolate the failing service and reproduce locally or in a dev environment using the same inputs.

### 221. What are dead-letter queues?

*   **Definition**: A service implementation to store messages that meet one or more of the following criteria:
    1.  Message that is sent to a queue that does not exist.
    2.  Queue length limit exceeded.
    3.  Message size limit exceeded.
    4.  Message is rejected by the consumer (after max retries).
*   **Purpose**: Allows the system to isolate problematic messages for analysis (debugging) without blocking the processing of valid messages.

### 222. How do you manage service versioning?

*   **URI Versioning**: `/v1/orders`, `/v2/orders`. Explicit and easy to route.
*   **Header Versioning**: `Accept: application/vnd.app.v1+json`. Cleaner URLs but harder to test in browser.
*   **Semantic Versioning (SemVer)**: `MAJOR.MINOR.PATCH`.
    *   **Major**: Breaking changes.
    *   **Minor**: New features (backward compatible).
    *   **Patch**: Bug fixes.

### 223. How to maintain backward compatibility?

*   **Strategy**:
    1.  **Additive Changes**: Only add new fields/endpoints; never remove or rename existing ones.
    2.  **Deprecation Policy**: Mark old fields as `@Deprecated`, inform consumers, and announce a sunset date.
    3.  **Consumer-Driven Contracts (CDC)**: Use tools like **Spring Cloud Contract** or **Pact** to ensure your changes don't break the expectations of your consumers.

### 224. How do you deploy multiple microservices together?

*   **Containers**: Dockerize each service.
*   **Orchestration**: Use **Kubernetes (K8s)** or **Docker Swarm**.
    *   Define `Deployment` YAMLs for each service.
    *   Define `Service` YAMLs for networking.
    *   Use **Helm Charts** to package and deploy the entire suite as a release.
*   **CI/CD**: Configuring pipelines (Jenkins/GitLab CI) to build images and apply manifests to the cluster automatically.

### 225. What is blue-green deployment?

*   **Definition**: A release technique that reduces downtime and risk by running two identical production environments called Blue and Green.
*   **Mechanism**:
    1.  **Blue** is currently live serving all traffic.
    2.  Deploy the new version to **Green**.
    3.  Test Green.
    4.  Switch the Load Balancer/Router to point to Green.
*   **Rollback**: Instant. Switch the router back to Blue if issues arise.

### 226. What is canary deployment?

*   **Definition**: Releasing a new version to a small subset of users (e.g., 5%) to test it in production before rolling it out to everyone.
*   **Mechanism**:
    1.  Deploy v2 alongside v1.
    2.  Configure the Load Balancer (Istio/Nginx) to send 5% of traffic to v2.
    3.  Monitor metrics (Errors, Latency).
    4.  If good, gradually increase traffic (10%, 50%, 100%).
*   **Benefit**: Limits the blast radius of a bad release.

### 227. How to rollback a faulty microservice?

*   **Kubernetes**: `kubectl rollout undo deployment/my-service`.
    *   K8s keeps a history of `ReplicaSets`. It effectively changes the image tag back to the previous stable version and restarts pods.
*   **Blue-Green**: Switch the router back to the old environment.
*   **Database**: This is the hard part. If the failed version migrated the DB schema in a backward-incompatible way, code rollback might fail. (Always prefer additive DB changes).

### 228. What are the common microservices pitfalls?

1.  **Distributed Monolith**: Services are tightly coupled (too much chatter, shared DB).
2.  **Ignoring Network Latency**: Treating remote calls like local method calls.
3.  **Lack of Automation**: Trying to manage 50 services manually without CI/CD or K8s.
4.  **Testing Complexity**: Failing to implement integration/contract tests.
5.  **Logging Chaos**: Not implementing centralized logging/tracing early.

### 229. How would you refactor a monolith into microservices?

*   **Strangler Fig Pattern**:
    1.  Identify a specific domain/functionality (e.g., "Reviews") to extract.
    2.  Build a new microservice for it.
    3.  Put a Gateway/Proxy in front of the monolith.
    4.  Route "Review" traffic to the new service, and everything else to the monolith.
    5.  Repeat until the monolith is gone (strangled).

### 230. What is a shared library in microservices?

*   **Definition**: A JAR containing common code (DTOs, Utils, Security logic) used by multiple services.
*   **Pros**: DRY (Don't Repeat Yourself), consistency.
*   **Cons**:
    *   **Coupling**: If the library changes, all services must be rebuilt and redeployed to get the update.
    *   **Version Hell**: Different services using different versions of the library.
*   **Advice**: Prefer code duplication over coupling, or use Sidecars to offload common logic (e.g., logging/auth) instead of libraries.

### 231. What is API composition?

*   **Problem**: A client (e.g., Mobile App) needs data from multiple microservices (User, Order, Payment) to render a single screen. Making 3 separate calls over the internet is slow (latency).
*   **Solution**:
    *   **API Gateway**: The Gateway makes the 3 calls internally (parallel) and aggregates the results into a single JSON response for the client.
    *   **BFF (Backend for Frontend)**: A specific service layer dedicated to aggregating data for a specific UI.

### 232. What is service granularity?

*   **Definition**: The scope of functionality a microservice covers.
*   **Coarse-Grained**: A service covers a large domain (e.g., "E-commerce Service"). Easy to manage but looks like a monolith.
*   **Fine-Grained**: A service covers a tiny function (e.g., "Tax Calculation Service"). Highly decoupled but creates a "chatty" network with high latency and complexity.
*   **Goal**: Find the sweet spot (Bounded Context).

### 233. How do you manage dependencies between microservices?

*   **Loose Coupling**: Services should interact via APIs, not shared databases or libraries.
*   **Backward Compatibility**: Services must evolve without breaking consumers (Versioning).
*   **Service Discovery**: Use Registry to handle location changes.
*   **Async Communication**: Prefer events over direct HTTP calls where possible to reduce runtime dependencies.

### 234. How to test microservices independently?

*   **Unit Tests**: Test logic inside the service using Mockito.
*   **Integration Tests**: Test Interaction with DB and Message Broker using **TestContainers**.
*   **Component Tests**: Test the service APIs in isolation by mocking external dependencies (other services) using **WireMock**.
*   **Contract Tests**: Ensure the service adheres to the API contract expected by consumers.

### 235. What is consumer-driven contract testing (CDC)?

*   **Concept**:
    *   **Consumer** (e.g., Frontend or Service A) defines the contract: "I expect `GET /users/1` to return `{id, name}`".
    *   **Provider** (Service B) verifies this contract against its implementation.
*   **Benefit**: It ensures that a change in the Provider (Service B) doesn't break the Consumer (Service A) effectively catching breaking changes at build time, long before deployment.

### 236. What is Pact and how does it work?

*   **Tool**: A popular framework for CDC testing.
*   **Workflow**:
    1.  **Consumer Test**: Runs a unit test against a mock provider. Finds success. Generates a "Pact File" (JSON contract).
    2.  **Broker**: The Pact file is uploaded to a Pact Broker.
    3.  **Provider Test**: The Provider downloads the Pact file and replays the requests against itself to verify it meets the contract.

### 237. How do you handle timeouts in microservices?

*   **Importance**: Without timeouts, a slow service can hold up threads in the caller indefinitely, causing resource exhaustion (cascading failure).
*   **Configuration**:
    *   **Connection Timeout**: Time to establish TCP handshake.
    *   **Read Timeout (Socket Timeout)**: Time waiting for data after connection.
    *   *Example (RestTemplate)*: `ConnectTimeout: 1000ms`, `ReadTimeout: 3000ms`.
*   **Handling**: If timeout occurs, trigger Circuit Breaker fallback or return a default error.

### 238. What is asynchronous communication?

*   **Mechanism**: The sender sends a message and continues its work without waiting for a response.
*   **Tools**: Message Brokers (RabbitMQ, Kafka, ActiveMQ).
*   **Patterns**:
    *   **Fire and Forget**: "Email Sent".
    *   **Publish/Subscribe**: "Order Created" -> Inventory, Shipping, Email services all listen.

### 239. When to use synchronous vs asynchronous communication?

*   **Synchronous (HTTP/REST)**:
    *   When the client **needs** the answer immediately to proceed (e.g., "Login", "Get User Profile").
    *   Simple, real-time feedback.
*   **Asynchronous (Messaging)**:
    *   Long-running jobs (e.g., "Generate PDF Report").
    *   Decoupling systems (e.g., "Order Placed" -> "Send Email").
    *   Handling spikes in traffic (Buffering in queue).

### 240. What is eventual consistency vs strong consistency?

*   **Strong Consistency (ACID)**:
    *   Data is consistent immediately after write.
    *   *Example*: Saving to a single RDBMS.
    *   *Trade-off*: Reduced availability or higher latency (CAP Theorem).
*   **Eventual Consistency (BASE)**:
    *   Data will become consistent *at some point* in the future.
    *   *Example*: Updating a User in Service A, and waiting for the event to update the cache in Service B.
    *   *Trade-off*: Temporary inconsistency is accepted for higher system availability and performance.

### 241. How to handle large payloads in microservices?

*   **Avoid**: Sending large JSON/XML blobs (e.g., 50MB) directly over HTTP REST calls. It blocks threads and causes OutOfMemory errors.
*   **Strategies**:
    1.  **Compression**: Use GZIP compression for payloads.
    2.  **Pagination**: Break large lists into smaller chunks.
    3.  **Claim Check Pattern**: Store the large payload (e.g., image, document) in an external Blob Storage (S3, MinIO) and pass only the **reference URL** (claim check) in the message/API call.
    4.  **Streaming**: Use Reactive Streams (WebFlux) to process data chunk-by-chunk.

### 242. How to implement file upload in a microservice?

*   **Multipart Request**: Use `MultipartFile` in Spring Boot (`@RequestParam("file") MultipartFile file`).
*   **Storage**: DO NOT store files on the local disk of the container (containers are ephemeral).
*   **Pattern**:
    1.  Receive file stream.
    2.  Upload stream directly to Object Storage (S3).
    3.  Save metadata (S3 key, size, type) in the database.
*   **Optimization**: Generate a **Presigned URL** from S3. Let the client upload directly to S3. This bypasses your microservice entirely, saving bandwidth and CPU.

### 243. What is throttling?

*   **Definition**: The process of controlling the usage of a service by a client.
*   **Difference from Rate Limiting / Circuit Breaker**:
    *   **Rate Limiting**: Rejects requests exceeding a limit (Error 429). "Stop calling me."
    *   **Throttling**: Intentionally slows down processing (queuing) or degrades service quality to manage load. "Wait a bit."
    *   **Circuit Breaker**: Stops outgoing calls when *downstream* is down. "I won't call them."

### 244. How do you scale a microservice?

*   **X-Axis (Horizontal Scaling)**: Running multiple instances (clones) behind a load balancer. (Most common).
*   **Y-Axis (Functional Decomposition)**: Splitting the service into smaller services based on verbs/functions (e.g., separating "Checkout" from "Order Management").
*   **Z-Axis (Data Partitioning)**: Running instances that only handle a subset of data (Sharding by User ID).

### 245. What is horizontal vs vertical scaling?

*   **Vertical Scaling (Scale Up)**:
    *   Adding more power to existing machine (CPU, RAM).
    *   *Limit*: Hardware ceiling. Requires downtime to upgrade. Expensive.
*   **Horizontal Scaling (Scale Out)**:
    *   Adding more machines (nodes) to the pool.
    *   *Limit*: Practically infinite. No downtime. Cheaper (commodity hardware). Resilient.

### 246. What is container orchestration?

*   **Definition**: The automated management of the lifecycle of containerized applications.
*   **Responsibilities**:
    *   **Provisioning**: Scheduling containers on available nodes.
    *   **Redundancy**: Keeping X replicas running. Rescheduling dead ones.
    *   **Networking**: Service discovery, load balancing.
    *   **Health Monitoring**: Liveness checks.
    *   **Scaling**: Auto-scaling based on CPU/Memory.

### 247. How does Kubernetes support microservices?

*   **Pods**: The atomic unit of deployment (one or more containers).
*   **Services**: Stable network endpoint (Virtual IP) for a set of Pods. Handles Load Balancing and Discovery.
*   **ConfigMaps & Secrets**: External config management.
*   **Deployments**: Manages rolling updates and rollbacks.
*   **Ingress**: API Gateway functionality (routing external traffic to services).

### 248. What is the difference between microservices and SOA?

*   **SOA (Service Oriented Architecture)**:
    *   **Scope**: Enterprise-wide.
    *   **Communication**: Enterprise Service Bus (ESB) - smart pipes. Logic in the bus.
    *   **Protocol**: SOAP/XML (Heavy).
    *   **Data**: Often shared databases.
*   **Microservices**:
    *   **Scope**: Application-wide.
    *   **Communication**: Rest/gRPC - dumb pipes, smart endpoints. Logic in the service.
    *   **Protocol**: JSON/ProtoBuf (Light).
    *   **Data**: Database-per-service.

### 249. What is a backend-for-frontend (BFF) pattern?

*   **Problem**: A Desktop Web App needs detailed data. A Mobile App needs minimal data (to save battery/bandwidth). Use one generic API? No.
*   **Solution**: Create a specific API Gateway (BFF) for each client type.
    *   `web-bff`: Aggregates data for the browser.
    *   `mobile-bff`: Aggregates, filters, and formats data specifically for the mobile app.
*   **Benefit**: Optimized Experience, decreased chatter for mobile.

### 250. What is the role of a message broker in microservices?

*   **Decoupling**: Sender doesn't need to know who the receiver is or if they are online.
*   **Buffering**: Handles spikes in load. Use a queue to store messages until consumers can process them (Load Leveling).
*   **Asynchronous Processing**: Fire and forget.
*   **Reliability**: Brokers persist messages. If a consumer dies, the message stays in the queue until it restarts.

### 251. What are the best practices for microservice architecture?

*   **Database-per-Service**: Each service owns its data.
*   **API Composition**: Use Gateways/BFFs for aggregation, don't chain service calls if possible.
*   **Asynchronous Communication**: Use events for decoupling.
*   **Observability**: Implement centralized logging, tracing, and metrics from day one.
*   **Automation**: CI/CD and Infrastructure as Code are mandatory.
*   **Fault Tolerance**: Design for failure (Circuit breakers, Retries).

### 252. What is a service mesh used for?

*   **Traffic Management**: Routing, splitting traffic, retries, timeouts (without code changes).
*   **Security**: Enforcing mTLS (mutual TLS) between services automatically.
*   **Observability**: Generating metrics and traces for all network traffic.
*   **Resiliency**: Implementing circuit breakers and rate limits at the network layer.

### 253. Explain the Ambassador pattern in microservices.

*   **Definition**: A container that creates a proxy connection for the application to the outside world.
*   **Role**: It acts as an "ambassador" or helper for the main app.
*   **Use Case**:
    *   Connecting to a database with a complex connection protocol.
    *   Handling security/authentication for 3rd party APIs.
    *   Offloading logic (like retry implementation) out of the legacy application code.

### 254. What are the 12 factors of microservices?

*   **The 12-Factor App Methodology**:
    1.  **Codebase**: One codebase tracked in revision control, many deploys.
    2.  **Dependencies**: Explicitly declare and isolate dependencies.
    3.  **Config**: Store config in the environment.
    4.  **Backing Services**: Treat backing services as attached resources.
    5.  **Build, Release, Run**: Strictly separate build and run stages.
    6.  **Processes**: Execute the app as one or more stateless processes.
    7.  **Port Binding**: Export services via port binding.
    8.  **Concurrency**: Scale out via the process model.
    9.  **Disposability**: Maximize robustness with fast startup and graceful shutdown.
    10. **Dev/Prod Parity**: Keep development, staging, and production as similar as possible.
    11. **Logs**: Treat logs as event streams.
    12. **Admin Processes**: Run admin/management tasks as one-off processes.

### 255. What is polyglot persistence?

*   **Definition**: Using different data storage technologies to handle different data storage needs within the same system.
*   **Example**:
    *   **PostgreSQL** for transactional data (Orders).
    *   **MongoDB** for product catalog (Documents).
    *   **Redis** for caching (Key-Value).
    *   **Elasticsearch** for searching (Text).
    *   **Neo4j** for recommendation engines (Graphs).

### 256. What is observability and why is it critical?

*   **Definition**: The measure of how well internal states of a system can be inferred from knowledge of its external outputs (Logs, Metrics, Traces).
*   **Criticality**: In microservices, "debugging in production" is the norm. You cannot attach a debugger to 100 running instances. You need observability to answer "Why is the cart slow?" without guessing.

### 257. How do you ensure microservices are resilient?

*   **Timeouts**: Fail fast.
*   **Circuit Breakers**: Prevent cascading failure.
*   **Retry with Backoff**: Handle transient errors.
*   **Bulkheads**: Isolate resources.
*   **Redundancy**: Run multiple replicas of every service.
*   **Statelessness**: Assume any instance can die at any time.

### 258. What’s the difference between telemetry, tracing, and logging?

*   **Logging**: Records discrete events (e.g., "Error: NullPointer"). "What happened?"
*   **Metrics (Telemetry)**: Aggregated numerical data (e.g., "CPU Usage: 80%"). "Is it healthy?"
*   **Tracing**: records the flow and timing of a request through the system. "Where did it go and how long did it take?"

### 259. What is shadow traffic?

*   **Definition**: A release testing technique where production traffic is duplicated (mirrored) and sent to a new version of the service (Shadow Version) *without* affecting the real user.
*   **Benefit**: Allows testing the new version under real load and with real data usage patterns without any risk to the user (the shadow response is ignored). Tools like Istio support this.

### 260. How do you handle API deprecation in microservices?

1.  **Notice**: Add `@Deprecated` annotation and a warning header (`Warning: 299 - "This API is deprecated"`).
2.  **Communication**: Inform consumers via documentation/email with a timeline.
3.  **Sunset Header**: Use standard `Sunset` header (`Sunset: Sat, 31 Dec 2026 23:59:59 GMT`).
4.  **Monitoring**: Track usage of the deprecated endpoint.
5.  **Brownouts**: Intentionally degrade performance or shut down the endpoint for short periods to force users to migrate.

### 261. How do you build a microservice SDK?

*   **SDK (Software Development Kit)**: A library provided by a service owner to consumers to simplify integration.
*   **Best Practices**:
    1.  **Keep it Thin**: It should only be a thin wrapper around the HTTP/gRPC client (DTOs + Client Interface). Avoid heavy logic.
    2.  **Versioning**: Version the SDK independently (SemVer).
    3.  **Auto-Configuration**: For Spring Boot, include `@Configuration` to automatically set up the `WebClient` or `FeignClient` bean.
    4.  **No Transitive Dependency Hell**: Minimize dependencies. Shade dependencies if necessary.

### 262. What is the difference between REST and gRPC?

*   **REST (Representational State Transfer)**:
    *   **Protocol**: HTTP/1.1 (Text-based JSON).
    *   **Communication**: Request-Response (Unary).
    *   **Readability**: Human-readable. Easy to debug (Browser/Postman).
    *   **Performance**: Overhead of JSON serialization/deserialization.
*   **gRPC (Remote Procedure Call)**:
    *   **Protocol**: HTTP/2 (Binary Protobuf).
    *   **Communication**: Unary, Server Streaming, Client Streaming, Bidirectional Streaming.
    *   **Readability**: Binary (not human-readable). Requires contract (`.proto` file).
    *   **Performance**: Extremely fast/compact serialization. Great for internal microservice chatter.

### 263. How do you integrate GraphQL in microservices?

*   **GraphQL**: A query language for APIs where clients ask for exactly what they need.
*   **Integration**:
    *   **Schema Stitching / Federation**: Each microservice exposes a GraphQL endpoint (subgraph). A central "Gateway" stitches these schemas together into a single "Supergraph".
    *   **Apollo Federation**: The standard for distributed GraphQL. Services annotate their entities (`@key`) to link data across services.
*   **Challenge**: Solving the N+1 problem in a distributed environment (requires DataLoaders and batching).

### 264. What is a lightweight vs heavyweight service?

*   **Lightweight**:
    *   Small memory footprint (e.g., Go, Rust, Quarkus).
    *   Fast startup (Milliseconds).
    *   Single responsibility.
    *   Ideal for Serverless/Lambda or high-scale microservices.
*   **Heavyweight**:
    *   Large footprint (e.g., Legacy Java EE, Rails).
    *   Slow startup.
    *   Complex logical domains.
    *   Often monolithic or "Macroservices".

### 265. What is head-of-line blocking?

*   **Definition**: A performance issue where a line of packets is held up by the first packet.
*   **Context (HTTP/1.1)**: Browsers limit parallel connections (e.g., 6). If one request takes long, others queued behind it wait, even if bandwidth is available.
*   **Context (Switching)**: A packet at the front of the queue blocks others destined for different output ports.
*   **Solution**: HTTP/2 (Multiplexing) solves this by allowing multiple requests/responses to be interleaved on a single TCP connection.

### 266. What is a correlation ID and how is it useful?

*   (See also Q204, Q206 - Repeated concept, reinforced context).
*   **Definition**: A unique identifier attached to a request at the system entry point.
*   **Flow**: It is passed to every downstream service in HTTP headers (`X-Correlation-ID`).
*   **Usefulness**: It is the *only* way to stitch together logs from 10 different services to debug a single user request. Without it, distributed debugging is impossible.

### 267. How to design authentication in a microservice ecosystem?

*   **Centralized Identity Provider (IdP)**: (Keycloak, Auth0). Handles login.
*   **Token-Based (Stateless)**:
    1.  User logs in -> IdP returns JWT.
    2.  User sends JWT to Gateway.
    3.  Gateway validates signature (CPU cheap) or invokes Auth Service.
    4.  Gateway forwards request + User Info (headers) to downstream services.
*   **Service-to-Service**:
    *   **Client Credentials Flow**: Service A authenticates with IdP to get its own token to call Service B.
    *   **mTLS**: Mutual TLS certificates for identity.

### 268. What is the strangler pattern in microservices migration?

*   **Metaphor**: Strangler figs grow around a host tree, eventually replacing it.
*   **Strategy**:
    1.  Put a Proxy/Gateway in front of the Legacy Monolith.
    2.  Build a new Microservice for *one* feature (e.g., Search).
    3.  Update Proxy to route "Search" traffic to the new Microservice.
    4.  Legacy Monolith still handles everything else.
    5.  Repeat until Monolith is strangled (empty).

### 269. Explain real-world microservice monitoring setup using Spring Boot + Sleuth + Zipkin + Prometheus + Grafana.

*   **The Stack**:
    1.  **Spring Boot**: The application.
    2.  **Micrometer (Sleuth)**: The library inside the app. It measures timings (Trace) and counts (Metrics) and exposes them.
    3.  **Prometheus**: The database. It *polls* the app every 15s to grab the metrics.
    4.  **Zipkin**: The trace server. The app *pushes* trace data (Spans) to Zipkin async (often via Kafka).
    5.  **Grafana**: The dashboard. It queries Prometheus to draw charts ("CPU usage") and links to Zipkin for traces ("Why was 2:00 PM slow?").

### 270. What is the difference between WHERE and HAVING?

*   **WHERE**:
    *   Filters rows **before** grouping (Aggregation).
    *   Acts on individual records.
    *   *Example*: `SELECT * FROM users WHERE age > 18`
*   **HAVING**:
    *   Filters groups **after** grouping.
    *   Acts on the result of an aggregate function (`COUNT`, `SUM`, `AVG`).
    *   *Example*: `SELECT city, COUNT(*) FROM users GROUP BY city HAVING COUNT(*) > 100` (Find cities with more than 100 users).

### 271. What is indexing? How does it improve performance?

*   **Definition**: A data structure (usually B-Tree) that improves the speed of data retrieval operations on a database table.
*   **Analogy**: The index at the back of a book. Instead of reading every page to find "Java", you look up "Java" in the index and go directly to page 42.
*   **Trade-off**: Improves **READ** performance but degrades **WRITE** (Insert/Update/Delete) performance, because the index must be updated whenever data changes.

### 272. What is a composite index?

*   **Definition**: An index created on two or more columns of a table.
*   **Usage**: Useful when queries filter by multiple columns together.
*   **Rule**: The **Leftmost Prefix Rule** applies. If you have an index on `(A, B, C)`, the index is used for queries on `A`, `A+B`, and `A+B+C`. It is **NOT** used for queries on `B` or `C` alone.

### 273. What are clustered and non-clustered indexes?

*   **Clustered Index**:
    *   Determines the **physical order** of data in the table.
    *   There can be only **one** clustered index per table (usually the Primary Key).
    *   Leaf nodes contain the actual data rows.
*   **Non-Clustered (Secondary) Index**:
    *   stored separately from the data.
    *   Contains the column value and a **pointer** (or Primary Key) to the actual data row.
    *   A table can have multiple non-clustered indexes.

### 274. What is normalization? Types?

*   **Definition**: The process of organizing data to minimize redundancy (duplication) and improve data integrity.
*   **Types (Normal Forms)**:
    *   **1NF**: Atomic values (no list/arrays in a cell), unique rows.
    *   **2NF**: 1NF + No partial dependency (all non-key columns depend on the full Primary Key).
    *   **3NF**: 2NF + No transitive dependency (non-key columns depend only on the Key, not on other non-key columns).
    *   **BCNF**: Higher level of 3NF.

### 275. What is denormalization?

*   **Definition**: The process of adding redundancy to a database schema to optimize **read performance**.
*   **Scenario**: In a highly normalized DB, fetching a "User Profile" might require joining 5 tables (User, Address, Job, etc.), which is slow.
*   **Solution**: Duplicate the `City` name into the `User` table to avoid the join.
*   **Trade-off**: Faster reads, but updates are complex (need to update data in multiple places to ensure consistency).

### 276. What is ACID property?

*   **Atomicity**: All or nothing. If one part of the transaction fails, the entire transaction rolls back.
*   **Consistency**: The transaction brings the DB from one valid state to another (constraints/triggers are honored).
*   **Isolation**: Concurrent transactions do not interfere with each other.
*   **Durability**: Once committed, data is permanent (survives power loss).

### 277. What is the difference between TRUNCATE, DELETE and DROP?

*   **DELETE (DML)**:
    *   Deletes specific rows (can use `WHERE`).
    *   Can be rolled back.
    *   Fires triggers.
    *   Slower (logs each row deletion).
*   **TRUNCATE (DDL)**:
    *   Removes **all** rows.
    *   Cannot be rolled back (in some DBs).
    *   Resets identity counters.
    *   Faster (deallocates pages).
*   **DROP (DDL)**:
    *   Removes the **entire table structure** and data.

### 278. What are window functions? Examples?

*   **Definition**: Functions that perform calculations across a set of table rows that are related to the current row. Unlike `GROUP BY`, they do **not** collapse rows.
*   **Syntax**: `FUNCTION() OVER (PARTITION BY ... ORDER BY ...)`
*   **Examples**:
    *   `ROW_NUMBER()`: Assigns a unique sequential integer to rows.
    *   `RANK()`: Assigns a rank with gaps (1, 2, 2, 4).
    *   `DENSE_RANK()`: Assigns a rank without gaps (1, 2, 2, 3).
    *   `LAG()/LEAD()`: Access data from the previous/next row.

### 279. What is CTE?

*   **CTE (Common Table Expression)**: A temporary result set that you can reference within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement.
*   **Syntax**: Defined using the `WITH` clause.
    ```sql
    WITH Sales_CTE AS (
        SELECT SalesPersonID, SUM(TotalDue) as TotalSales
        FROM SalesOrderHeader
        GROUP BY SalesPersonID
    )
    SELECT * FROM Sales_CTE WHERE TotalSales > 10000;
    ```
*   **Benefit**: Makes complex queries more readable compared to nested subqueries.

### 280. How does GROUP BY work internally?

*   **Mechanism**:
    1.  **Scanning**: The DB scans the table (or index).
    2.  **Sorting/Hashing**:
        *   **Sort**: It sorts the rows based on the grouping columns (e.g., `City`). All 'New York' rows come together. Then it aggregates them.
        *   **Hash**: It builds a hash table where keys are the grouping columns and values are the running aggregates.
    3.  **Aggregation**: It calculates functions like `SUM`, `COUNT` for each group.

### 281. What is query optimization?

*   **Definition**: The process of selecting the most efficient way to execute a SQL statement.
*   **Techniques**:
    1.  **Indexing**: Create indexes on columns used in `WHERE`, `JOIN`, and `ORDER BY`.
    2.  **Avoid SELECT \***: Select only necessary columns to reduce I/O and network traffic.
    3.  **Use JOINs over Subqueries**: Modern optimizers handle joins better.
    4.  **Avoid Functions on Columns**: `WHERE YEAR(date_col) = 2023` prevents index usage. Use `WHERE date_col BETWEEN '2023-01-01' AND '2023-12-31'`.
    5.  **Analyze Execution Plan**: Use `EXPLAIN` to see if indexes are being used.

### 282. How to analyze slow queries?

*   **Tools**:
    *   **Slow Query Log**: Enable logging in MySQL/Postgres for queries taking > X seconds.
    *   **EXPLAIN**: Run `EXPLAIN SELECT ...` to see the query execution plan (Full Table Scan vs Index Scan).
    *   **APM Tools**: New Relic, Datadog, or Spring Boot Actuator/Micrometer to identify slow DB calls from the application side.

### 283. What is a transaction isolation level?

*   **Definition**: Defines the degree to which one transaction must be isolated from resource or data modifications made by other transactions.
*   **Levels (Low to High)**:
    1.  **Read Uncommitted**: Dirty reads allowed. Fastest, least safe.
    2.  **Read Committed** (Default): No dirty reads. Phantom reads allowed.
    3.  **Repeatable Read**: No dirty reads, no non-repeatable reads. Phantom reads possible.
    4.  **Serializable**: Strict isolation. Transactions run sequentially. Slowest, most safe.

### 284. Explain deadlocks in SQL and how to resolve.

*   **Definition**: A situation where two transactions are waiting for each other to give up locks.
    *   *Tx1* holds Lock A, wants Lock B.
    *   *Tx2* holds Lock B, wants Lock A.
*   **Resolution**:
    *   **Database**: The DB engine detects the cycle and kills one transaction (victim) with an error.
    *   **Prevention**:
        *   Access resources in the **same order** across all transactions.
        *   Keep transactions **short**.
        *   Use lower isolation levels if possible.

### 285. What are stored procedures? Pros/Cons?

*   **Definition**: Pre-compiled SQL code stored in the database.
*   **Pros**:
    *   **Performance**: Reduced network traffic (one call performs multiple steps).
    *   **Security**: Grants permission to execute procedure without giving access to underlying tables.
*   **Cons**:
    *   **Maintenance**: Version control and debugging are harder than Java code.
    *   **Vendor Lock-in**: Hard to migrate from Oracle to Postgres (PL/SQL vs PL/pgSQL).
    *   **Testing**: Hard to unit test.

### 286. How do you handle migrations in production DB?

*   **Tools**: **Flyway** or **Liquibase**.
*   **Process**:
    1.  Create migration scripts (`V1__Create_User.sql`, `V2__Add_Column.sql`).
    2.  Commit scripts to Git.
    3.  On app startup (or CI/CD pipeline), the tool checks the `schema_version` table.
    4.  It applies only the new scripts in order.
*   **Zero Downtime**:
    *   Day 1: Add new column (nullable). Deploy App v1.
    *   Day 2: Migrate data to new column.
    *   Day 3: Deploy App v2 (uses new column).
    *   Day 4: Drop old column.

### 287. How do ORMs like Hibernate work?

*   **ORM (Object-Relational Mapping)**: Maps Java Classes (Entities) to Database Tables.
*   **Mechanism**:
    1.  **Configuration**: Reads metadata (Annotations/XML) to understand the mapping.
    2.  **Session/EntityManager**: Acts as a bridge.
    3.  **SQL Generation**: Converts Java method calls (`session.save(user)`) into SQL statements (`INSERT INTO users...`) appropriate for the specific database dialect.
    4.  **ResultSet Mapping**: Converts SQL results back into Java objects.

### 288. What is Hibernate’s first-level cache?

*   **Scope**: **Session** (Transaction) scope.
*   **Behavior**:
    *   Enabled by default (cannot be disabled).
    *   When you query an entity (e.g., `findById(1)`), Hibernate stores it in the Session.
    *   If you query `findById(1)` again within the *same* transaction, Hibernate returns the object from memory without hitting the database.
*   **Purpose**: Reduces DB calls and ensures object identity ( `a == b` is true).

### 289. What is the difference between save(), persist(), merge() and update()?

*   **`save()`** (Hibernate): Persists the object. Returns the generated ID.
*   **`persist()`** (JPA): Persists the object. Returns `void`. Part of the specification.
*   **`update()`** (Hibernate): Re-attaches a detached object to the session and forces an SQL UPDATE.
*   **`merge()`** (JPA): Copies the state of a detached object into a persistent object with the same identifier. Returns the managed copy.

### 290. What is the difference between get() and load()?

*   **`get()`**:
    *   Hits the database immediately.
    *   Returns `null` if the object is not found.
    *   Use when you aren't sure if the object exists.
*   **`load()`**:
    *   Returns a **Proxy** (fake object) with the ID populated.
    *   Does *not* hit the database until you access a non-ID property (Lazy Loading).
    *   Throws `ObjectNotFoundException` if the row doesn't exist upon access.
    *   Use when you only need the reference (e.g., to set a foreign key `order.setUser(load(1))`).

### 291. What is LazyInitializationException?

*   **Cause**: You try to access a lazily loaded relationship (e.g., `user.getOrders()`) *after* the Hibernate Session has been closed (usually after the transaction ends in the Service layer).
*   **Solutions**:
    1.  **Join Fetch**: Use `JOIN FETCH` in your JPQL query to load the data eagerly.
    2.  **Hibernate.initialize()**: Call this on the proxy while the session is still open.
    3.  **@Transactional**: Extend the transaction to the View layer (Open Session In View - Anti-pattern but works).
    4.  **EntityGraph**: Define a graph to load specific paths.

### 292. What is the purpose of @JoinColumn and @OneToMany?

*   **`@OneToMany`**: Defines the logical relationship (One User has Many Orders). Usually placed on the parent side.
*   **`@JoinColumn`**: Defines the physical mapping (Foreign Key column).
    *   If used on the `@OneToMany` side (Parent), it creates a unidirectional relationship (Parent knows about Child).
    *   If omitted on `@OneToMany` (and `mappedBy` is used), it implies the relationship is bidirectional and the Foreign Key is managed by the Child entity (where `@ManyToOne` and `@JoinColumn` are usually placed).

### 293. How to handle orphan removal?

*   **Definition**: When you remove a child entity from a parent's collection, you want that child to be deleted from the database automatically.
*   **Usage**: Set `orphanRemoval = true` in `@OneToMany`.
    ```java
    @OneToMany(mappedBy = "user", orphanRemoval = true)
    private List<Order> orders = new ArrayList<>();
    
    // Usage
    user.getOrders().remove(order); // This deletes the order row from DB
    ```

### 294. How does Hibernate manage object states?

*   **Transient**: The object is created (`new User()`) but not associated with a Session and has no representation in the DB.
*   **Persistent**: The object is associated with a Session and has a representation in the DB. Changes to it are automatically saved (Dirty Checking).
*   **Detached**: The object was persistent but the Session is closed. Changes are not tracked.
*   **Removed**: The object is scheduled for deletion.

### 295. What are common Hibernate performance issues?

1.  **N+1 Select Problem**: Fetching a list of parents and then fetching children for each one individually.
2.  **Cartesian Product**: Joining multiple collections eagerly in one query (fetches Rows * M Rows * Z Rows).
3.  **Too Main Roundtrips**: Inserting 1000 rows one by one instead of using JDBC Batch updates.
4.  **Missing Indexes**: Queries are slow due to full table scans.
5.  **Selecting Too Much Data**: Fetching full entities when DTOs (projections) would suffice.

### 296. How does the second-level cache work in Hibernate?

*   **L1 Cache**: Session scoped (Transaction). Short-lived.
*   **L2 Cache**: SessionFactory scoped (Application). Long-lived. Shared across all sessions.
*   **Mechanism**:
    *   When an entity is loaded, it is stored in L2 Cache.
    *   Subsequent requests for the same ID (even from different users) retrieve it from L2 Cache, avoiding a DB hit.
*   **Providers**: EhCache, Hazelcast, Infinispan, Redis.
*   **Use Case**: Read-mostly data (Reference data, Countries, Currencies).

### 297. Difference between Criteria API and JPQL?

*   **JPQL (Java Persistence Query Language)**:
    *   String-based queries (similar to SQL).
    *   Pros: Readable, familiar.
    *   Cons: Not type-safe (errors caught at runtime), hard to build dynamic queries.
*   **Criteria API**:
    *   Programmatic, type-safe way to build queries using Java objects.
    *   Pros: Compile-time checks, great for dynamic search filters.
    *   Cons: Verbose, complex syntax (especially in JPA 2.0+).

### 298. What is flush() and clear()?

*   **`flush()`**: Forces Hibernate to synchronize the in-memory state of the Session with the database (executes pending SQL INSERTs/UPDATEs). It does *not* commit the transaction.
*   **`clear()`**: Detaches all objects from the Session. It clears the L1 Cache. Useful after a batch insert to free up memory.

### 299. What is a natively generated ID vs sequence?

*   **`GenerationType.IDENTITY`**:
    *   Rely on the database's auto-increment feature (MySQL `AUTO_INCREMENT`, SQL Server `IDENTITY`).
    *   *Drawback**: Hibernate cannot batch inserts because it needs to execute the INSERT immediately to get the ID back.
*   **`GenerationType.SEQUENCE`**:
    *   Uses a database sequence (Oracle, Postgres).
    *   Hibernate can fetch a block of IDs (allocationSize) in one go.
    *   *Benefit**: Supports JDBC Batching efficiently.

### 300. What is optimistic locking in JPA?

*   **Concept**: Strategy where you assume conflicts are rare. You don't lock the row during read.
*   **Implementation**:
    1.  Add a `@Version` field (int or timestamp) to your entity.
    2.  When saving, Hibernate checks: `UPDATE table SET name=?, version=2 WHERE id=1 AND version=1`.
    3.  If the row was updated by someone else (version is now 2), the row count returned is 0.
    4.  Hibernate throws `OptimisticLockException`.

### 301. How to implement soft delete in Hibernate?

*   **Definition**: Instead of physically removing the row (`DELETE FROM table`), you mark it as deleted (e.g., `is_deleted = true`). The data remains for audit/recovery.
*   **Implementation**:
    1.  Add a column `@Column(name = "deleted") private boolean deleted = false;`.
    2.  Use `@SQLDelete(sql = "UPDATE user SET deleted = true WHERE id = ?")` on the Entity. Calling `repository.delete(user)` will now execute this UPDATE.
    3.  Use `@Where(clause = "deleted = false")` on the Entity. This automatically filters out deleted rows in all `SELECT` queries.

### 302. How does MongoDB store data?

*   **Format**: BSON (Binary JSON).
*   **Structure**:
    *   **Database**: Container for collections.
    *   **Collection**: Container for documents (Analogy: Table).
    *   **Document**: A BSON record (Analogy: Row).
*   **Schema**: Schema-less (or flexible schema). Different documents in the same collection can have different fields.

### 303. Difference between MongoDB and MySQL?

*   **Structure**:
    *   MySQL: Relational (Tables, Rows, Columns). Enforced Schema.
    *   MongoDB: Document-oriented (Collections, Documents). Flexible Schema.
*   **Joins**:
    *   MySQL: Supports complex joins.
    *   MongoDB: No joins (traditionally). Use `$lookup` (aggregation) or embedding.
*   **Transactions**:
    *   MySQL: ACID compliant (Multi-row).
    *   MongoDB: ACID compliant (Multi-document support added in v4.0, but performance penalty exists).
*   **Scaling**:
    *   MySQL: Vertical scaling is easier. Horizontal (Sharding) is hard.
    *   MongoDB: Horizontal scaling (Sharding) is built-in.

### 304. What are documents and collections?

*   **Document**: The basic unit of data in MongoDB. It is an ordered set of key-value pairs (BSON). Complex structures (arrays, nested objects) are first-class citizens.
*   **Collection**: A grouping of MongoDB documents. It is the equivalent of an RDBMS table. A collection exists within a single database.

### 305. How to model one-to-many relationship in MongoDB?

1.  **Embedding (Denormalization)**:
    *   Store the "Many" side inside the "One" side.
    *   *Usage*: When the child data is always accessed with the parent and is bounded (e.g., User -> Addresses).
    *   `{ name: "John", addresses: [ { city: "NY" }, { city: "LA" } ] }`
2.  **Referencing (Normalization)**:
    *   Store the ID of the "One" side in the "Many" side (like SQL Foreign Key).
    *   *Usage*: When the "Many" side is large/unbounded (e.g., User -> 10,000 Order History).
    *   User: `{ _id: 1, name: "John" }`
    *   Order: `{ _id: 100, user_id: 1, amount: 50 }`

### 306. What is aggregation framework in MongoDB?

*   **Definition**: A pipeline for data processing. Documents enter a multi-stage pipeline that transforms the documents into an aggregated result.
*   **Stages**:
    *   `$match`: Filter documents (WHERE).
    *   `$group`: Group documents (GROUP BY).
    *   `$project`: Select/Rename fields (SELECT).
    *   `$sort`: Sort results (ORDER BY).
    *   `$limit`/`$skip`: Pagination.

### 307. What is sharding?

*   **Definition**: Distributing data across multiple machines (Shards) to support very large datasets and high throughput operations.
*   **Mechanism**: MongoDB uses a **Shard Key** to partition data chunks.
    *   *Example*: If Shard Key is `ZipCode`, then Zip 00000-50000 go to Server A, 50001-99999 go to Server B.
*   **Components**:
    *   **Shard**: Stores data.
    *   **Mongos**: Query Router (App connects here).
    *   **Config Server**: Stores metadata (mapping of chunks to shards).

### 308. What are indexes in MongoDB?

*   Similar to RDBMS indexes (B-Tree).
*   **Types**:
    *   **Single Field**: Index on `name`.
    *   **Compound**: Index on `name` + `age`.
    *   **Multikey**: Index on an **array** field (indexes every element in the array).
    *   **Text**: For search.
    *   **Geospatial**: For location queries (`$near`).

### 309. How does Redis work?

*   **In-Memory**: Stores all data in RAM (Random Access Memory), making read/write operations usually fast (Microseconds).
*   **Data Structures**: Not just strings. Supports Lists, Sets, Sorted Sets, Hashes, Bitmaps, Streams.
*   **Persistence**:
    *   **RDB (Snapshot)**: Saves DB to disk every X minutes.
    *   **AOF (Append Only File)**: Logs every write command to disk.
*   **Single Threaded**: The event loop is single-threaded (no context switching/locking overhead), but I/O is handled efficiently.

### 310. What is TTL in Redis?

*   **TTL (Time To Live)**: A mechanism to automatically expire (delete) a key after a specified time.
*   **Command**: `EXPIRE session_id 3600` (Delete after 1 hour).
*   **Usage**: Caching, Session Management (User logs out automatically after inactivity).

### 311. Difference between Redis and Memcached?

*   **Redis**:
    *   **Data Types**: Supports complex types (Lists, Sets, Hashes, Sorted Sets).
    *   **Persistence**: Yes (RDB, AOF).
    *   **Replication**: Built-in master-slave replication.
    *   **Transactions**: Supports (MULTI/EXEC).
    *   **Pub/Sub**: Yes.
*   **Memcached**:
    *   **Data Types**: Keys and Values are simple Strings/Objects (binary blobs).
    *   **Persistence**: No (Purely in-memory).
    *   **Multithreaded**: Yes (Redis is single-threaded).
    *   **Use Case**: Simple key-value caching where multithreading throughput on large machines is needed.

### 312. What are common use cases of Redis?

1.  **Caching**: Reducing database load.
2.  **Session Store**: Storing user session data (JWT blacklist, Login info).
3.  **Leaderboard**: Using Sorted Sets (`ZADD`) for real-time ranking.
4.  **Pub/Sub**: Real-time messaging/chat.
5.  **Queues**: Using Lists (`LPUSH`/`RPOP`) for job queues (Sidekiq/Celery).
6.  **Rate Limiting**: Using increment and expiry to limit API calls.

### 313. How to store sessions in Redis?

*   **Spring Boot**: Use `spring-session-data-redis`.
*   **Mechanics**:
    1.  Add dependency.
    2.  Configure `application.properties`: `spring.session.store-type=redis`.
    3.  Spring automatically intercepts `bHttpSession` and stores the attributes in Redis instead of the Tomcat memory.
*   **Benefit**: Allows stateless application servers. Any server can handle the request because the session is in a shared Redis.

### 314. What is persistence in Redis?

*   (See Q309)
*   **RDB (Redis Database File)**: Point-in-time snapshots. Good for backups. Faster restart. Potential data loss if crash occurs between snapshots.
*   **AOF (Append Only File)**: Logs every write operation. Higher durability (fsync every second). Slower restart (replay logs).
*   **Hybrid**: Use both RDB for fast restart and AOF for durability.

### 315. How does Redis pub/sub work?

*   **Model**: Publishers send messages to channels. Subscribers listen to channels.
*   **Decoupled**: Publishers don't know who subscribers are.
*   **Fire & Forget**: Messages are **not** persisted. If a subscriber is offline, it misses the message. (For persistent messaging, use Redis Streams or RabbitMQ/Kafka).
*   **Commands**: `SUBSCRIBE channel1`, `PUBLISH channel1 "Hello"`.

### 316. What are Redis data types?

1.  **String**: Basic key-value (text, int, binary).
2.  **List**: Linked list of strings (Queue/Stack).
3.  **Set**: Unordered collection of unique strings.
4.  **Sorted Set (ZSet)**: Set where every member has a score (Ranking).
5.  **Hash**: Map within a key (good for Objects).
6.  **Bitmap**: Bit-level operations.
7.  **HyperLogLog**: Probabilistic cardinality count (e.g., unique visitors).
8.  **Geospatial**: Lat/Long coordinates.

### 317. How to avoid cache stampede?

*   **Problem**: A hot key expires. 1000 requests hit the cache simultaneously, find it missing, and all 1000 hit the DB to regenerate it. DB crashes.
*   **Solutions**:
    1.  **Mutex Lock**: Only let 1 thread regenerate the cache. Others wait.
    2.  **Probabilistic Early Expiration**: Return the value, but if it is *close* to expiry, trigger an async regeneration.
    3.  **Logical Expiry**: Don't use Redis TTL. Store expiry in the value. If expired, return old value but trigger async update.

### 318. How does cache eviction work in Redis?

*   **Maxmemory Policy**: What happens when memory is full?
    1.  `noeviction`: Returns error on write.
    2.  `allkeys-lru`: Evict Least Recently Used keys (any key).
    3.  `volatile-lru`: Evict LRU keys that have an expire set.
    4.  `allkeys-random`: Random eviction.
    5.  `volatile-ttl`: Evict keys with shortest time-to-live.

### 319. What is write-through vs write-behind cache?

*   **Write-Through**:
    *   App writes to Cache AND DB synchronously.
    *   Pros: Data consistency.
    *   Cons: Higher write latency (2 writes).
*   **Write-Behind (Write-Back)**:
    *   App writes to Cache only. Cache async writes to DB later.
    *   Pros: Fast writes.
    *   Cons: Data loss risk if cache crashes before syncing.
*   **Cache-Aside (Lazy Loading)**: (Most common)
    *   App checks Cache. If miss, read DB, update Cache.
    *   App updates DB, deletes Cache key (to invalidate).

### 320. When would you use NoSQL over SQL?

1.  **Flexible Schema**: Data structure changes frequently (e.g., Content Management, User Profiles with dynamic fields).
2.  **High Throughput**: Need massive write performance (IoT sensor data). NoSQL often scales writes better.
3.  **Volume**: Billions of rows where sharding MySQL is painful.
4.  **Specific Data Models**: Graph data (Social Network -> Neo4j), Document data (Catalog -> MongoDB).
5.  **No ACID Requirement**: Eventual consistency is acceptable.

### 353. What is CI/CD? Explain the flow.

*   **CI (Continuous Integration)**: Developers merge their changes back to the main branch as often as possible. The changes are validated by creating a build and running automated tests against the build.
    *   *Flow*: Code Commit -> Build (Compile) -> Unit Tests -> Static Analysis (SonarQube).
*   **CD (Continuous Delivery)**: An extension of CI. Changes are automatically built, tested, and prepared for a release to production.
    *   *Flow*: Package (Docker Image) -> Deploy to Staging -> Run Integration/E2E Tests -> Wait for Approval.
*   **CD (Continuous Deployment)**: Goes one step further. Every change that passes all stages of the production pipeline is released to customers *automatically*. No human intervention.

### 354. What tools are used in CI/CD?

*   **Jenkins**: The classic, open-source automation server.
*   **GitHub Actions**: Integrated directly into GitHub repositories.
*   **GitLab CI/CD**: Integrated into GitLab.
*   **CircleCI / Travis CI**: SaaS-based CI/CD platforms.
*   **ArgoCD**: For GitOps (Kubernetes).

### 355. Difference between Jenkins, GitHub Actions, and GitLab CI?

*   **Jenkins**:
    *   Self-hosted (usually).
    *   Highly customizable via thousands of plugins.
    *   Requires maintenance (updates, security).
*   **GitHub Actions / GitLab CI**:
    *   SaaS (Cloud-based, though self-hosted runners are possible).
    *   Configuration is part of the code (`.yml` files in repo).
    *   Zero maintenance overhead for the server itself.
    *   Deep integration with the Version Control System.

### 356. How to automate Spring Boot builds with Maven and Jenkins?

1.  **Install Plugins**: Maven Integration plugin in Jenkins.
2.  **Configure Tool**: Set up JDK and Maven paths in "Global Tool Configuration".
3.  **Create Job**: New "Freestyle Project" or "Pipeline".
4.  **Source Code Management**: Point to Git repository URL.
5.  **Build Step**: Add "Invoke top-level Maven targets". Goal: `clean install`.
6.  **Post-build Actions**: Archive artifacts (`target/*.jar`).

### 357. What is a Jenkins pipeline?

*   **Definition**: A suite of plugins which supports implementing and integrating *continuous delivery pipelines* into Jenkins.
*   **Jenkinsfile**: The definition of a Jenkins Pipeline is typically written into a text file (called a `Jenkinsfile`) which in turn is checked into a source control repository.
*   **Stages**: Define distinct phases like `Build`, `Test`, `Deploy`.

### 358. What is the difference between scripted and declarative pipeline?

*   **Scripted Pipeline**:
    *   Based on Groovy.
    *   Imperative syntax (Control structures: `if`, `for`, `try/catch`).
    *   More flexibility but complex.
*   **Declarative Pipeline**:
    *   Structured syntax (`pipeline { agent any ... }`).
    *   Easier to read and write.
    *   Opinionated (Enforces structure).
    *   Preferred for most modern use cases.

### 359. How do you trigger builds automatically on git push?

1.  **Webhook**: Configure a Webhook in the Git provider (GitHub/GitLab) pointing to the Jenkins URL (`https://jenkins.example.com/github-webhook/`).
2.  **Event**: On `push` event, Git provider sends a POST request to Jenkins.
3.  **Jenkins Job**: Check "GitHub hook trigger for GITScm polling" in the job configuration.
4.  **Result**: Jenkins receives the hook and starts the build immediately.

### 360. What is the use of .gitlab-ci.yml or .github/workflows?

*   **Definition**: These are YAML configuration files that define the CI/CD pipeline logic.
*   **Location**: They reside in the root of the source code repository.
*   **Role**: They tell the CI runner what to do (e.g., "Use Java 17 image", "Run `mvn test`", "Build Docker image").
*   **Benefit**: "Pipeline as Code". The build logic is versioned along with the application code.

### 361. What is artifact management? Use of Nexus/Artifactory?

*   **Artifacts**: Binary files produced by the build process (JARs, WARs, Docker Images).
*   **Repository Manager (Nexus/Artifactory)**:
    *   **Proxy**: Caches external dependencies (from Maven Central) locally. Speeds up builds and works offline.
    *   **Hosting**: Stores internal artifacts (your company's libraries) to be shared across teams.
    *   **Versioning**: Keeps track of `1.0.0`, `1.0.1-SNAPSHOT` releases securely.

### 362. How do you perform zero-downtime deployments?

*   **Rolling Updates (Kubernetes Default)**:
    *   Replaces Pods one by one.
    *   Service (Load Balancer) only sends traffic to "Ready" pods.
    *   Users might see a mix of v1 and v2 during the rollout.
*   **Blue-Green Deployment**:
    *   Spin up a full new environment (Green).
    *   Switch Load Balancer instantly.
    *   Zero downtime, but requires double the resources.

### 363. What is a rollback deployment strategy?

*   **Definition**: Reverting to the previous stable version when a critical bug is found after deployment.
*   **Strategies**:
    *   **Re-deploy Old Artifact**: Trigger the CI/CD pipeline to deploy the previous tag (e.g., `v1.2.0` instead of `v1.3.0`).
    *   **Toggle Feature Flag**: If the bug is behind a flag, just turn it off. No redeploy needed.
    *   **Kubernetes Rollback**: `kubectl rollout undo deployment/my-app`.

### 364. How do you manage secrets in CI/CD?

*   **Rule #1**: **NEVER** commit secrets (API keys, DB passwords) to the Git repository.
*   **Solutions**:
    *   **Jenkins Credentials**: Store secrets securely in Jenkins. Inject them as environment variables during the build.
    *   **GitHub Secrets**: Encrypted secrets in GitHub repo settings.
    *   **HashiCorp Vault**: Centralized secret management. The pipeline fetches secrets dynamically at runtime using a temporary token.

### 365. How do you deploy a Spring Boot app using Jenkins?

1.  **Checkout**: Pull code from Git.
2.  **Build**: Run `mvn clean package` to generate the JAR.
3.  **Dockerize**: Run `docker build -t my-app:v1 .`.
4.  **Publish**: Run `docker push my-repo/my-app:v1`.
5.  **Deploy**:
    *   *SSH*: Copy JAR/Docker command to the production server and restart.
    *   *Kubernetes*: Update the deployment manifest with the new image tag and apply.

### 366. What is blue-green deployment? How to implement it?

*   **Implementation**:
    1.  **Infrastructure**: Two identical environments (Blue=Live, Green=Idle).
    2.  **Router**: A Load Balancer (Nginx/HAProxy/AWS ALB) points to Blue.
    3.  **Deploy**: Deploy the new version to Green.
    4.  **Verify**: Run smoke tests on Green (using a private URL/port).
    5.  **Switch**: Update the Router configuration to point to Green.
    6.  **Monitor**: If errors spike, switch back to Blue immediately.

### 367. What are stages in a pipeline?

*   **Commit**: Developer pushes code.
*   **Build**: Compile code and run Unit Tests. (Fail fast).
*   **Quality Analysis**: SonarQube scan for bugs/vulnerabilities.
*   **Package**: Create Docker Image / JAR.
*   **Deploy to Staging**: Automated deployment to a test environment.
*   **Acceptance Test**: Run Integration/E2E tests data on Staging.
*   **Deploy to Production**: Manual approval or automated rollout.

### 368. How to run integration tests during a pipeline?

*   **Pre-requisite**: Integration tests need a running database/message broker.
*   **Approach 1 (Testcontainers)**: The tests themselves spin up Docker containers for DB/Kafka anywhere (even in the CI runner). This is the modern, preferred way.
*   **Approach 2 (Ephemeral Environment)**: The pipeline deploys a temporary DB container, runs tests against it, and then destroys it.
*   **Results**: Publish test reports (JUnit XML) to the CI dashboard.

### 369. How to deploy microservices to Kubernetes using CI/CD?

*   The **CD** part of the pipeline:
    1.  **Templating**: Use **Helm** or **Kustomize** to manage K8s YAML files (replace `IMAGE_TAG` with the new build version).
    2.  **Authentication**: The CI runner needs a `kubeconfig` or Service Account token to talk to the K8s API Server.
    3.  **Command**: Run `helm upgrade --install my-release ./charts` or `kubectl apply -f deployment.yaml`.
    4.  **Verification**: Wait for `kubectl rollout status deployment/my-app` to ensure pods are ready.

### 370. What is infrastructure as code (IaC)?

*   **Definition**: Managing and provisioning computing infrastructure (Servers, Networks, Load Balancers) through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools.
*   **Tools**: **Terraform** (Cloud-agnostic), **AWS CloudFormation**, **Ansible** (Configuration Management).
*   **Benefits**:
    *   **Version Control**: Infrastructure changes are tracked in Git.
    *   **Consistency**: No "configuration drift" (manual changes on servers).
    *   **Reproducibility**: Spin up a new duplicate environment (Staging/Dev) in minutes.

### 371. How do you use Terraform in CI/CD?

*   **Process**:
    1.  **Code**: Define infrastructure in `.tf` files.
    2.  **Plan**: In CI, run `terraform plan`. This shows what *will* change.
    3.  **Apply**: On approval (or merge to main), run `terraform apply -auto-approve`.
*   **State**: The `terraform.tfstate` file must be stored remotely (e.g., S3 Bucket with DynamoDB locking) so the CI runner can access the current state of the infrastructure.

### 372. What is Ansible and how does it compare with Chef/Puppet?

*   **Ansible**:
    *   **Agentless**: No software needed on the target servers (uses SSH).
    *   **Push Model**: The controller pushes config to servers.
    *   **YAML**: Uses simple YAML playbooks.
*   **Chef/Puppet**:
    *   **Agent-based**: Requires installing an agent on every server.
    *   **Pull Model**: Agents poll the master for updates.
    *   **Ruby/DSL**: Uses complex Domain Specific Languages.

### 373. What is Helm and how is it used?

*   **Definition**: The package manager for Kubernetes (like `apt` or `yum` for OS).
*   **Charts**: Packages are called **Charts**. A Chart contains templates for K8s YAMLs (Deployment, Service, ConfigMap).
*   **Usage**: Instead of applying 10 separate YAML files, you run `helm install my-app ./my-chart --set image.tag=v1`. It renders the templates with values and applies them to the cluster.

### 374. What is GitOps?

*   **Definition**: A paradigm where the **Git repository** is the single source of truth for infrastructure and application configuration.
*   **Mechanism**:
    *   You don't run `kubectl apply` manually.
    *   You commit a change to the Git repo (e.g., change `replicas: 2` to `replicas: 3`).
    *   A **GitOps operator** (like ArgoCD or Flux) running in the cluster detects the drift between Git and the Cluster, and automatically synchronizes (applies) the change.

### 375. How do you manage environment-specific configuration in CI/CD?

*   **Externalize Config**: Use profiles (Spring Boot) or ConfigMaps (K8s).
*   **CI/CD Injection**:
    *   Store values in the CI/CD Variable system (e.g., distinct variables for `STAGING_DB_URL` and `PROD_DB_URL`).
    *   During deployment, inject these values as Environment Variables into the Docker container or generate a `config.yaml` file specific to the target environment.

### 376. What is a canary release?

*   **Concept**: rollout a change to a small subset of users (canaries) before rolling it out to the entire infrastructure.
*   **Implementation**:
    *   Deploy version B alongside version A.
    *   Direct 10% of traffic to version B.
    *   Monitor metrics (error rate, latency).
    *   If successful, gradually increase traffic to 100%.

### 377. What are Docker images and how are they pushed in CI/CD?

*   **Definition**: A lightweight, executable package that includes everything needed to run a piece of software (code, runtime, libraries, environment variables, and config files).
*   **Push Flow**:
    1.  `docker build -t my-app:hash .` (Builds the image).
    2.  `docker login` (Authenticates with registry).
    3.  `docker push my-app:hash` (Uploads layers to the registry like Docker Hub or ECR).

### 378. How do you tag Docker images automatically?

*   **Strategies**:
    *   **Git Commit Hash**: `my-app:a1b2c3d` (Precise link to code).
    *   **SemVer**: `my-app:1.0.2` (Human readable).
    *   **Build Number**: `my-app:build-105` (Sequential).
*   **Best Practice**: DO NOT use `latest` tag in production. It is ambiguous and makes rollbacks hard.

### 379. What is build caching?

*   **Problem**: Downloading Maven/NPM dependencies every time takes 5 minutes.
*   **Solution**:
    *   The CI runner caches the local repository (`~/.m2` or `node_modules`).
    *   Before the build, it restores the cache.
    *   After the build, it saves the cache (if `pom.xml` changed).
    *   Result: Builds take seconds instead of minutes.

### 380. What is a webhook?

*   **Definition**: A user-defined HTTP callback.
*   **Mechanism**: System A checks for an event (e.g., "Code Pushed"). When it happens, System A makes an HTTP POST request to a URL configured by System B, passing data payload.
*   **Usage in CI/CD**: GitHub triggers Jenkins via webhook to start a build immediately after a commit.

### 381. How do you monitor CI/CD pipelines?

*   **Dashboards**: Visualize pipeline status (Red/Green) in Jenkins/GitLab UI.
*   **Metrics**: Track "Mean Time to Recovery" (MTTR), "Change Failure Rate", "Deployment Frequency".
*   **Alerts**: Integrate with Slack/Email to notify the team immediately upon build failure.
*   **Logs**: Analyze build logs to identify flaky tests or slow build steps.

### 382. What is the use of a staging environment?

*   **Definition**: A mirror of the production environment (same hardware, OS, scale) but isolated.
*   **Purpose**:
    *   Test deployment scripts and database migrations before they hit production.
    *   Run Load Tests and UAT (User Acceptance Testing) with real-like data.
    *   Ensure configuration (environment variables) is correct.
*   **Rule**: If it works in Staging, it *should* work in Production.

### 383. How to use SonarQube in your CI pipeline?

1.  **Install SonarScanner**: Add the plugin to Jenkins or the Action to GitHub Workflow.
2.  **Configuration**: Provide `sonar-project.properties` (project key, source directories).
3.  **Execute**: Run the scan step after the build/test step.
4.  **Quality Gate**: Configure the pipeline to **fail** if the Quality Gate (e.g., "New Bugs > 0" or "Coverage < 80%") is not met.

### 384. How to ensure code quality and security before deployment?

*   **Linting**: Static analysis for style (Checkstyle, ESLint).
*   **Unit Tests**: Validate logic (JUnit).
*   **SAST (Static Application Security Testing)**: Scan source code for vulnerabilities (SonarQube, Fortify).
*   **SCA (Software Composition Analysis)**: Scan dependencies for CVEs (Snyk, OWASP Dependency Check).
*   **DAST (Dynamic Application Security Testing)**: Scan running app for vulnerabilities (OWASP ZAP).

### 385. What are test, build, deploy, and post-deploy hooks?

*   **Hooks**: Scripts that run at specific points in the lifecycle.
*   **Pre-Commit (Git)**: Run linter locally.
*   **Pre-Build**: Clean artifacts, download dependencies.
*   **Post-Build**: Archive artifacts, tag Docker image.
*   **Pre-Deploy**: Run DB migrations (`Flyway`).
*   **Post-Deploy**: Run smoke tests (`curl /health`), notify Slack, warm up cache.

### 386. What is Docker? Why is it used?

*   **Definition**: A platform for developing, shipping, and running applications in **containers**.
*   **Problem Solved**: "It works on my machine".
*   **How**: Bundles the code + runtime + libraries + OS settings into a single immutable artifact (Image).
*   **Benefits**: Portability, Isolation, Efficiency (lighter than VMs), Scalability.

### 387. What is the difference between a container and an image?

*   **Image (Class)**:
    *   A read-only template with instructions for creating a container.
    *   Built from a Dockerfile.
    *   Analogy: Java Class.
*   **Container (Object)**:
    *   A runnable instance of an image.
    *   Has a writable layer on top of the image.
    *   Analogy: Java Object (Instance).

### 388. What is a Dockerfile? Common instructions?

*   **Definition**: A text document that contains all the commands a user could call on the command line to assemble an image.
*   **Instructions**:
    *   `FROM openjdk:17`: Base image.
    *   `WORKDIR /app`: Set working directory.
    *   `COPY target/app.jar app.jar`: Copy files from host to image.
    *   `RUN apt-get update`: Run commands during build.
    *   `EXPOSE 8080`: Document the listening port.
    *   `CMD ["java", "-jar", "app.jar"]`: Command to run when container starts. (Can be overridden).
    *   `ENTRYPOINT`: Main command (Arguments appended).

### 389. How to build and run a Docker image?

1.  **Build**: `docker build -t my-app:v1 .` (Looks for `Dockerfile` in current dir).
2.  **Run**: `docker run -d -p 8080:8080 --name my-container my-app:v1`
    *   `-d`: Detached mode (background).
    *   `-p`: Map host port to container port.

### 390. How to connect containers using Docker network?

*   **Default**: Containers are isolated.
*   **User-defined Bridge**:
    1.  Create network: `docker network create my-net`.
    2.  Run App: `docker run --net my-net --name app my-app`.
    3.  Run DB: `docker run --net my-net --name db mysql`.
*   **DNS**: Docker provides automatic DNS resolution. The "app" container can connect to the database using the hostname `db` (e.g., `jdbc:mysql://db:3306/...`).

### 391. What is a Docker volume?

*   **Definition**: A mechanism to persist data used by Docker containers. Data in a container is ephemeral (lost when container is removed). Volumes store data on the Host OS.
*   **Types**:
    *   **Named Volume**: Managed by Docker (`/var/lib/docker/volumes/`). `docker volume create my-vol`.
    *   **Bind Mount**: Maps a specific host path to a container path. `-v /home/user/data:/app/data`.
*   **Use Case**: Database storage, Log files.

### 392. How do you pass environment variables to a container?

*   **Command Line**: `docker run -e DB_URL=jdbc:mysql://... my-app`.
*   **File**: `docker run --env-file .env my-app`.
*   **Docker Compose**:
    ```yaml
    environment:
      - DB_URL=jdbc:mysql://...
    ```
*   **Dockerfile**: `ENV APP_HOME=/usr/app` (Sets default, can be overridden).

### 393. What is Docker Compose?

*   **Definition**: A tool for defining and running multi-container Docker applications.
*   **Configuration**: Uses a YAML file (`docker-compose.yml`) to configure the application's services, networks, and volumes.
*   **Command**: `docker-compose up -d` starts all services (App + DB + Redis) in the correct order with one command.

### 394. How do you containerize a Spring Boot application?

*   **Dockerfile**:
    1.  Start with base image: `FROM openjdk:17-alpine`.
    2.  Copy JAR: `COPY target/my-app.jar app.jar`.
    3.  Entrypoint: `ENTRYPOINT ["java", "-jar", "/app.jar"]`.
*   **Optimization**: Use **Layered Jar** mode (Spring Boot 2.3+) to separate dependencies from application code for better caching.

### 395. How to optimize Docker image size?

1.  **Minimal Base Image**: Use `alpine` (5MB) or `gcr.io/distroless/java` instead of full Debian/Ubuntu.
2.  **Multi-Stage Builds**: Compile code in a `maven` image, copy *only* the JAR to a `jre-alpine` runtime image.
3.  **Minimize Layers**: Combine `RUN apt-get update && apt-get install ... && rm -rf /var/lib/apt/lists/*` into one line to clean up cache in the same layer.
4.  **.dockerignore**: Exclude `.git`, `target`, `node_modules` from build context.

### 396. What is the difference between ENTRYPOINT and CMD?

*   **CMD**:
    *   Sets default commands and/or parameters.
    *   Easily overridden from command line. `docker run my-image echo "Override"`.
*   **ENTRYPOINT**:
    *   Configures a container that will run as an executable.
    *   Hard to override (need `--entrypoint`).
    *   Arguments from command line are *appended* to ENTRYPOINT.
*   **Best Practice**: Use `ENTRYPOINT` for the command (`java -jar`) and `CMD` for default args.

### 397. What is a multi-stage build in Docker?

*   **Definition**: A method to organize a Dockerfile to use multiple `FROM` instructions.
*   **Purpose**: To separate the build environment from the runtime environment.
*   **Example**:
    ```dockerfile
    # Stage 1: Build
    FROM maven:3.8 AS build
    COPY . .
    RUN mvn package

    # Stage 2: Run
    FROM openjdk:17-alpine
    COPY --from=build /target/app.jar app.jar
    ENTRYPOINT ["java", "-jar", "app.jar"]
    ```
*   **Result**: The final image does not contain Maven or Source Code, only the JAR and JRE. Drastically smaller size.

### 398. How to persist logs in a Docker container?

*   **Standard Output**: Apps should write logs to `stdout/stderr`. Docker captures this.
*   **Logging Drivers**: Configure Docker daemon to send logs to `json-file` (default), `syslog`, `splunk`, `gelf`, or `awslogs` (CloudWatch).
*   **Volumes**: Mount a host directory to the container's log directory (`-v /var/log/myapp:/app/logs`) if the app writes to files.

### 399. What are Docker health checks?

*   **Definition**: An instruction in Dockerfile to tell Docker how to test if the container is still working.
*   **Syntax**: `HEALTHCHECK CMD curl -f http://localhost:8080/actuator/health || exit 1`.
*   **Behavior**: If the check fails (exit code 1) X times, Docker marks the container as `unhealthy`. Orchestrators (Swarm/K8s) can then restart it.

### 400. What is the role of .dockerignore?

*   **Role**: Similar to `.gitignore`. It tells the Docker CLI which files to exclude when sending the **build context** to the Docker daemon.
*   **Benefits**:
    1.  **Security**: Prevent `secret.txt` or `.env` from accidentally ending up in the image.
    2.  **Performance**: Reduces upload size/time (avoid sending 500MB `target/` folder or `node_modules`).
    3.  **Cache Invalidation**: Prevents unnecessary cache busting if irrelevant files change.

### 401. What is Apache Kafka?

*   **Definition**: A distributed event streaming platform used for high-performance data pipelines, streaming analytics, data integration, and mission-critical applications.
*   **Core Capabilities**:
    1.  **Publish/Subscribe**: To streams of records.
    2.  **Store**: Streams of records in a fault-tolerant durable way.
    3.  **Process**: Streams of records as they occur.

### 402. How does Kafka work internally?

*   **Log-based**: Kafka is essentially a distributed commit log.
*   **Producer**: Appends messages to the end of a log (file on disk).
*   **Consumer**: Reads messages from the log sequentially.
*   **Broker**: The server that stores the log files.
*   **Zero-Copy**: Kafka relies on the OS kernel (sendfile) to move data from disk to network without copying it into application memory, making it extremely fast.

### 403. What is a Kafka topic and partition?

*   **Topic**: A category or feed name to which records are published (Logical concept). E.g., `orders`, `user-signups`.
*   **Partition**: A topic is split into multiple partitions (Physical concept).
    *   Each partition is an ordered, immutable sequence of records.
    *   Partitions allow Kafka to scale (parallel processing). 3 partitions = 3 consumers can read simultaneously.

### 404. Difference between Kafka consumer groups and individual consumers?

*   **Consumer Group**:
    *   A set of consumers working together to consume a topic.
    *   **Load Balancing**: Partitions are divided among the consumers in the group. Use this for standard high-scale processing.
*   **Individual Consumers (Broadcast)**:
    *   If multiple consumers are in *different* groups, they *all* get a copy of the message. Use this for Pub/Sub broadcasting.

### 405. How do you ensure message ordering in Kafka?

*   **Constraint**: Kafka guarantees ordering **only within a partition**, not across the entire topic.
*   **Solution**: To ensure all messages for "Order 123" are processed in order:
    *   Use the `Order ID` as the **Partition Key** when producing the message.
    *   Kafka hashes the key and ensures all messages with Key "123" go to the *same* partition.

### 406. What is the role of Kafka brokers and zookeepers?

*   **Broker**: The worker. Receives messages, stores them on disk, and serves them to consumers.
*   **Zookeeper**: The coordinator (Legacy).
    *   Maintains cluster metadata (Which broker is the leader for Partition 1?).
    *   Tracks controller election.
    *   *Note*: Modern Kafka (KRaft mode) removes Zookeeper dependency.

### 407. How to consume messages from Kafka using Spring Boot?

*   **Dependency**: `spring-kafka`.
*   **Annotation**: Use `@KafkaListener`.
    ```java
    @KafkaListener(topics = "orders", groupId = "inventory-group")
    public void listen(String message) {
        System.out.println("Received Message: " + message);
    }
    ```
*   **Configuration**: Set `bootstrap-servers`, `group-id`, `key/value-deserializer` in `application.yml`.

### 408. What is Kafka offset? How is it managed?

*   **Definition**: A unique integer that identifies the position of a message within a partition.
*   **Management**:
    *   Kafka enables "dumb broker, smart consumer". The consumer tracks *its own* progress.
    *   Consumers periodically commit their current offset to a special internal topic called `__consumer_offsets`.
    *   If a consumer crashes and restarts, it reads from the last committed offset.

### 409. What is the difference between at-most-once, at-least-once, and exactly-once delivery?

*   **At-most-once**: Fire/Forget. Message might be lost, but never duplicated. (Fastest).
*   **At-least-once** (Default): Message is guaranteed to be delivered, but might be duplicated (e.g., if consumer processes but crashes before committing offset). Application must be idempotent.
*   **Exactly-once**: Guaranteed delivery without duplication. Requires transactional support in Kafka Producers/Consumers (`enable.idempotence=true`).

### 410. How do you handle backpressure in Kafka consumers?

*   **Scenario**: The consumer cannot keep up with the producer.
*   **Kafka's Nature**: Kafka is a *pull-based* system. The consumer controls the flow. It's naturally resilient to backpressure because it only asks for data when it's ready.
*   **Tuning**:
    *   `max.poll.records`: Reduce the number of records fetched in one go (e.g., from 500 to 50).
    *   Pause/Resume: Programmatically pause the `MessageListenerContainer` if the processing queue is full.

### 411. Design an Aadhaar Registration System (like UIDAI).

*   **Key Challenges**: Biometric deduplication (1.4 Billion users), High availability (OTP generation), Security.
*   **Architecture**:
    *   **Enrollment**: Offline capable desktop apps syncing to central servers.
    *   **Deduplication**: Use a biometric matching engine (ABIS). Needs sharding by biometric features.
    *   **Authentication**: High-throughput read API (e-KYC).
    *   **Data Store**: Hadoop/HBase for massive storage of biometric blobs.

### 412. Design a UPI transaction system.

*   **Flow**: Payer App -> Payer Bank -> NPCI Switch -> Payee Bank -> Payee App.
*   **Key Components**:
    *   **PSP (Payment Service Provider)**: GooglePay, PhonePe.
    *   **Switch (NPCI)**: Routes transactions.
    *   **CBS (Core Banking System)**: The actual bank ledger.
*   **Challenges**: Atomic transaction across 4 entities. Timeout handling (Reversal logic). High concurrency on CBS.

### 413. Design a URL shortener like Bitly.

*   **Functional Requirement**: Convert long URL to short implementation (7 chars). Redirect short to long.
*   **Algorithm**:
    *   **Base62 Encoding**: Use [a-z, A-Z, 0-9] characters.
    *   **ID Generation**: Use a distributed ID generator (Snowflake or KGS - Key Generation Service) to get a unique integer ID, then convert to Base62.
    *   `1000000000` -> `bQ8e3`
*   **Storage**: Key-Value store (NoSQL). Read heavy.
*   **Redirect**: Return HTTP 301 (Permanent) or 302 (Temporary).

### 414. Design a rate limiter service.

*   **Algorithms**:
    *   **Token Bucket**: Allow bursts.
    *   **Leaky Bucket**: Constant rate.
    *   **Fixed Window**: Simple, edge case issues (double rate at boundary).
    *   **Sliding Window Log**: Precise, high storage cost.
*   **Implementation**:
    *   Use **Redis** (Lua script) to atomically decrement counters.
    *   API Gateway (Zuul/Kong) invokes Rate Limiter before forwarding request.

### 415. Design an email notification system.

*   **Features**: Templates, Scheduling, Priority, Unsubscribe management.
*   **Architecture**:
    1.  **Client**: Sends "Send Email" event to Kafka.
    2.  **Notification Service**: Consumes event.
    3.  **Template Engine**: Merges data with HTML template (Thymeleaf/Freemarker).
    4.  **Vendor Router**: Routes to SendGrid/SES based on cost/success rate.
    5.  **Tracker**: Updates status (Sent/Failed/Clicked) via Webhooks from vendor.

### 416. Design a payment gateway like Razorpay.

*   **Role**: Broker between Merchant and Bank.
*   **Key Requirements**:
    *   **Idempotency**: Ensure charging users only once.
    *   **Security**: PCI-DSS compliance (Tokenization of card numbers).
    *   **Reconciliation**: Matching bank statements with internal ledger.
    *   **Reliability**: Circuit breaker for failing banks.

### 417. Design an order management system (OMS).

*   **Workflow**: Order Created -> Inventory Reserve -> Payment -> Confirmed -> Packing -> Shipping -> Delivered.
*   **Implementation**: State Machine Pattern.
*   **Concurrency**:
    *   Prevent overselling. Use Optimistic Locking on Inventory table (`UPDATE products SET stock = stock - 1 WHERE id = 1 AND stock > 0`).
    *   Distributed Locking (Redlock) if using NoSQL.

### 418. Design a social media platform like Twitter.

*   **Read Heavy**: 1000 reads : 1 write.
*   **Timeline Generation**:
    *   **Pull Model**: Query DB for all tweets from followings on load. (Slow).
    *   **Push Model (Fan-out)**: When User A tweets, push ID to timelines of all followers in Redis. (Fast Read, Slow Write for celebrities).
    *   **Hybrid**: Push for normal users, Pull for celebrities.

### 419. Design a ride-sharing app backend like Uber.

*   **Core**: Location tracking and matching.
*   **Geo-spatial Indexing**:
    *   **QuadTree**: Divide map into grids.
    *   **Geohash**: String representation of lat/long.
*   **Driver Updates**: Drivers send location every 3s via WebSocket to Location Service (Redis Geo).
*   **Matching**: Find nearest drivers within radius (Redis `GEORADIUS`), filter by availability, send request.

### 420. Design a cab allocation algorithm.

*   **Goal**: Assign a boooking to the best available driver.
*   **Factors**: Distance, Traffic, Driver Rating, Batching.
*   **Approaches**:
    *   **Greedy**: Assign to the nearest driver. (Simple, strictly suboptimal globally).
    *   **Bipartite Matching**: Wait for a window (e.g., 30s), collect all requests and drivers, and run strict matching algorithm (Hungarian Algorithm) to minimize total wait time for everyone.

### 421. Design a stock trading system.

*   **Key Requirements**: Low latency, High Throughput, ACID compliance for balances.
*   **Architecture**:
    *   **Matching Engine**: In-memory (LMAX Disruptor pattern). Single-threaded for sequential consistency or sharded by Ticker Symbol.
    *   **Order Gateway**: Validates requests (authentication, limits).
    *   **Market Data**: Multicast UDP for broadcasting price updates.
    *   **Ledger**: Asynchronous persistence to DB (Snapshotting + WAL).

### 422. Design a distributed caching system (like Redis).

*   **Partitioning**: Consistent Hashing (Ring) to distribute keys across N nodes.
*   **Replication**: Master-Slave for high availability. Async replication.
*   **Eviction**: LRU (Least Recently Used) policy using a Doubly Linked List + HashMap.
*   **Discovery**: Gossip Protocol (Cluster mode) so nodes know about each other's state.

### 423. Design a scalable file storage service like Dropbox.

*   **Components**:
    *   **Client**: Chunking files (4MB blocks), Hashing (SHA-256) for deduplication.
    *   **Block Server**: Stores physical blocks in S3/HDFS.
    *   **Metadata DB**: Maps `FileID` -> `List<BlockID>`. (NoSQL).
    *   **Synchronization**: Long polling / WebSockets to notify other devices of changes.

### 424. Design a newsfeed algorithm like Facebook.

*   **Feed Generation**:
    *   **Fan-out on Write**: When User A posts, push ID to the pre-computed feed list of all friends. Fast read, slow write.
    *   **Fan-out on Read**: Pull latest posts from all friends at query time. Slow distinct read.
*   **Ranking**: EdgeRank algorithm. Score = `Affinity * Weight * Decay`.
    *   *Affinity*: How close you are to the author.
    *   *Weight*: Type of content (Video > Image > Text).
    *   *Decay*: Time since posted.

### 425. Design a job scheduler system.

*   **Requirements**: Execute tasks at specific times (once or recurring).
*   **Architecture**:
    *   **DB**: Store jobs with `next_run_time`.
    *   **Poller**: Threads wake up every minute, query DB for `next_run_time < now`, and push to Queue.
    *   **Workers**: Consume from Queue and execute.
    *   **Distributed Lock**: Ensure only one poller picks up a job (e.g., Quartz Cluster with DB lock).

### 426. Design an e-commerce checkout system.

*   **Phases**:
    1.  **Cart**: Redis (Session based).
    2.  **Checkout**: Validate Inventory (Locking), Calculate Tax/Shipping.
    3.  **Payment**: Call Gateway. Idempotency is key.
    4.  **Order Placement**: Save to DB.
*   **Failure Handling**:
    *   If Payment fails -> Rollback Inventory.
    *   If Save Order fails -> Refund Payment (Saga Pattern).

### 427. Design a multi-tenant SaaS app.

*   **Models**:
    1.  **Database per Tenant**: Highest isolation, expensive.
    2.  **Schema per Tenant**: Shared DB, separate schemas. Good balance.
    3.  **Shared Schema (Discriminator)**: All data in one table with `tenant_id` column. Cheapest, hardest to isolate/backup.
*   **Routing**: Subdomain (`tenant1.app.com`) identifies the tenant context filter.

### 428. Design a chat messaging system (WhatsApp).

*   **Protocol**: WebSocket or MQTT (lightweight, persistent connection).
*   **Flow**: User A -> LB -> Gateway -> Message Service -> DB (Cassandra/HBase) -> User B.
*   **Status**:
    *   *Sent*: Saved to Server.
    *   *Delivered*: Pushed to User B's device.
    *   *Read*: User B opened chat (Send Ack).
*   **Storage**: Time-series modification. HBase/Cassandra is ideal for write-heavy chat logs.

### 429. Design a calendar booking system (Calendly).

*   **Core**: Availability management.
*   **Conflict Detection**:
    *   Store appointments: `[Start, End]`.
    *   Check: `SELECT count(*) FROM slots WHERE start < req_end AND end > req_start`.
    *   If count == 0, insert. Use `SERIALIZABLE` isolation or optimistic locking to prevent double booking.

### 430. Design a scalable search engine.

*   **Write Path**:
    1.  Crawler fetches documents.
    2.  Indexer tokenizes and removes stop words.
    3.  Builds **Inverted Index** (Map: Word -> List of Document IDs).
*   **Read Path**:
    1.  Query Parser.
    2.  Lookup words in Inverted Index.
    3.  Intersect lists (AND query).
    4.  Rank results (TF-IDF or PageRank).
*   **Scaling**: Shard the index by Document ID. Scatter-gather queries.

### 431. Design a log aggregation system.

*   **Components**:
    *   **Sidecar (Filebeat/Fluentd)**: Reads log files from containers/VMs.
    *   **Buffer (Kafka)**: Handles high throughput spikes of logs.
    *   **Ingester (Logstash/Vector)**: Parses, filters, and formats logs.
    *   **Storage (Elasticsearch/Loki)**: Indexes logs for search.
    *   **UI (Kibana/Grafana)**: Visualization.
*   **Challenge**: Managing storage costs. Use index lifecycle management (Hot -> Warm -> Cold -> Delete).

### 432. Design a fraud detection system for bank transactions.

*   **Real-time**:
    *   **Rule Engine (Drools)**: Checks simple rules (e.g., "Transaction > $10k").
    *   **ML Model Inference**: Scores the transaction probability of fraud.
*   **Batch**:
    *   **Graph DB**: Detects circular transactions or large rings of money movement.
    *   **Anomaly Detection**: Identify patterns deviating from user's history.
*   **Action**: If Score > Threshold -> Block or Challenge (OTP).

### 433. Design a real-time bidding system (AdTech).

*   **Constraints**: Entire bidding process must finish in < 100ms.
*   **Architecture**:
    *   **DSP (Demand Side Platform)**: Advertisers' agents.
    *   **SSP (Supply Side Platform)**: Publishers' agents.
    *   **Ad Exchange**: Facilitates the auction.
*   **Tech Stack**: C++/Rust/Go for low latency. In-memory data grids (Aerospike) for user profiles. No SQL DB in the critical path.

### 434. Design a student registration portal for an academy.

*   **Workflow**: Student applies -> Exam/Interview -> Selection -> Fee Payment -> Enrollment.
*   **Concurrency**: Handling thousands of students applying at 10 AM.
*   **Solution**:
    *   **Queue**: Put applications in a queue (RabbitMQ) to process asynchronously.
    *   **Cache**: Store course availability in Redis. 
    *   **Rate Limiting**: Prevent abuse.

### 435. Design a document approval workflow.

*   **Pattern**: **Saga** or **State Machine**.
*   **States**: DRAFT -> SUBMITTED -> MANAGER_APPROVED -> DIRECTOR_APPROVED -> PUBLISHED.
*   **Engine**: Use **Camunda** or **Zeebe** (BPMN engines) or custom State pattern in Java.
*   **Audit**: Store every state transition with timestamp and actor ID in an immutable ledger (Append-only table).

### 436. Design a notification aggregator.

*   **Problem**: Don't spam users with 50 "Like" notifications. Send "50 people liked your post".
*   **Mechanism**:
    *   **Windowing**: When an event occurs, store it in Redis buffer.
    *   **Debounce**: Wait for X minutes of inactivity or Y max minutes.
    *   **Aggregation**: Group events by type and object ID.
    *   **Dispatch**: Send one summarized email/push.

### 437. Design an online exam portal.

*   **Challenges**:
    *   **Security**: Prevent copy-paste (Lockdown browser), Proctoring (Webcam stream analysis).
    *   **Reliability**: Auto-save answers every 30 seconds to Redis/Local Storage.
    *   **Submission**: Handle burst traffic at the end of the exam.
*   **DB**: Store Questions (Relational/NoSQL) and Answers (NoSQL for flexibility).

### 438. Design a microservice for user identity management (IAM).

*   **Capabilities**: Registration, Login, Forgot Password, MFA, OAuth2 Provider.
*   **Security**:
    *   **Password Hashing**: Argon2 or BCrypt.
    *   **Tokens**: Issue JWTs (Access Token) and Opaque Strings (Refresh Token).
    *   **Lockout**: Lock account after 5 failed attempts (Redis counter).
*   **Standards**: Implement OIDC (OpenID Connect).

### 439. Design a task scheduling system.

*   (See Q425 - Similar concept, checking for variations).
*   **Key**: Priority Queues.
*   **Architecture**:
    *   **Scheduler**: Scans DB for due tasks. Pushes to Kafka topics based on priority (`high-priority`, `low-priority`).
    *   **Workers**: Scale workers based on queue depth (KEDA).
    *   **Idempotency**: Ensure tasks can be retried without side effects.

### 440. Design a content moderation system.

*   **Pipeline**:
    1.  **User Upload**: Image/Text.
    2.  **Automated Check**:
        *   **Text**: Keyword filter (Regex), NLP Sentiment analysis.
        *   **Image**: Hash matching (MD5) against known bad images. AI Vision API (NSFW detection).
    3.  **Manual Review**: If AI confidence is low (e.g., 40-80%), send to human moderator queue.
    4.  **Action**: Delete content, Ban user.

### 441. Design an IoT telemetry processing service.

*   **Ingestion**: Use **MQTT** (lightweight protocol) -> MQTT Broker (Mosquitto/HiveMQ).
*   **Buffer**: Kafka to handle bursts of sensor data.
*   **Processing**: Stream processing (Flink/Kafka Streams) for real-time alerts (e.g., Temp > 50°C).
*   **Storage**: **Time-Series DB** (InfluxDB or TimescaleDB) optimized for writing timestamped data.

### 442. Design a language translation service (Google Translate).

*   **API**: `POST /translate {text, source, target}`.
*   **Async Processing**:
    *   Push request to Queue. Return `JobId`.
    *   **Worker** picks up text, feeds to ML Model (TensorFlow Serving).
    *   Callback/Webhook to client when done, or Client polls `/status/{JobId}`.
*   **Caching**: Store hash of input text (`SHA256(text+lang)`) in Redis to avoid re-translating common phrases.

### 443. Design a product catalog service (Amazon).

*   **Data Model**:
    *   Relational DB for fixed attributes (SKU, Price).
    *   **NoSQL (MongoDB/DynamoDB)** for flexible attributes (Shirt has Size/Color, Laptop has RAM/CPU). Store as JSON.
*   **Search**: Sync data to **Elasticsearch** for full-text search and faceting.
*   **Caching**: Heavy caching (CDN for images, Redis for product details). Read-heavy system.

### 444. Design a document versioning service (Google Docs/Drive).

*   **Storage**:
    *   **Blob Store (S3)**: Store the actual file content. Immutable (New version = New object or Versioned Object).
    *   **Metadata DB**: `FileID`, `VersionNumber`, `S3Path`, `Author`, `Timestamp`.
*   **Optimization**:
    *   **Differential Sync**: Store only the *delta* (changes) between v1 and v2 is efficient for text files.
    *   **Deduplication**: If two users upload the same PDF, store once, reference twice (Content Addressable Storage).

### 445. Design a survey application (SurveyMonkey).

*   **Dynamic Schema**: Questions can be Text, Radio, Checkbox.
    *   Store Survey definition as a JSON blob in NoSQL.
    *   Store Responses as JSON documents.
*   **Analytics**:
    *   Aggregation pipeline (MongoDB aggregations) to calculate "60% matched Option A".
    *   Export to CSV feature (Batch Job).

### 446. Design a hotel booking system.

*   **Inventory Management**:
    *   `RoomType: {Double, King}`.
    *   `Inventory: {Date, RoomType, TotalCount, BookedCount}`.
*   **Concurrency**:
    *   **Overbooking**: Allow `BookedCount > TotalCount` by 10% (business logic).
    *   **Locking**: Optimistic Locking on the specific Date+Type row.
*   **Search**: "Find rooms available from Oct 1-5". Querying availability across a range is complex in SQL. Use a specialized availability bit-map or intervals table.

### 447. Design a cloud storage system (Google Drive).

*   **Architecture**:
    *   **Block Server**: Splits large files (1GB) into 4MB blocks. Compresses and encrypts.
    *   **Block Store**: S3/HDFS.
    *   **Metadata DB**: Maps `File Path` -> `List<BlockIDs>`.
*   **Sync Client**: Watch file system changes. Upload only modified blocks.

### 448. Design a recommendation engine (Netflix).

*   **Data Sources**: User watch history, Ratings, Demographics.
*   **Algorithms**:
    *   **Collaborative Filtering**: "Users similar to you liked X".
    *   **Content-based**: "You liked Sci-Fi, here is more Sci-Fi".
    *   **Vector Search**: Embed users and movies into vector space. Find nearest neighbors (FAISS/Milvus).
*   **Architecture**: Offline Batch Job computes recommendations nightly -> Stores in Redis/Cassandra -> API serves in < 50ms.

### 449. Design an OTP verification system.

*   **Flow**:
    1.  User enters Phone.
    2.  Server generates random 6 digit `123456`.
    3.  Store `Key: Phone, Value: 123456` in **Redis** with **TTL 5 minutes**.
    4.  Send SMS via Gateway (Twilio).
*   **Verification**:
    1.  User enters Code.
    2.  Values match? -> Success + Delete Key.
    3.  Mismatch? -> Fail. Limit retries using a separate counter in Redis.

### 450. Design a distributed rate limiter using Redis.

*   **Algorithm**: Sliding Window Log or Fixed Window Counter.
*   **Implementation (Lua Script)**:
    1.  Key: `ratelimit:{user_id}`.
    2.  `current = GET key`.
    3.  `if current > limit return 429`.
    4.  `INCR key`.
    5.  `if key is new, EXPIRE key 60s`.
*   **Race Conditions**: Using Lua ensures atomicity (Check + Increment happens as one step).

### 451. What is scalability? Vertical vs Horizontal?

*   **Vertical Scaling (Scale Up)**: Adding more power (CPU, RAM) to an existing machine.
    *   *Pros*: Easy (no code change).
    *   *Cons*: Hardware limit, single point of failure.
*   **Horizontal Scaling (Scale Out)**: Adding more machines to the pool.
    *   *Pros*: Unlimited scale, resilience.
    *   *Cons*: Complex (requires load balancing, distributed data management).

### 452. What is latency vs throughput?

*   **Latency**: The time taken to process a *single* request (Response Time). Measured in milliseconds (ms).
*   **Throughput**: The number of requests the system can process per unit of time. Measured in RPS (Requests Per Second) or QPS.
*   *Goal*: Low Latency and High Throughput.

### 453. What is availability? What is reliability?

*   **Availability**: The percentage of time the system is operational and accessible. (e.g., 99.99% uptime).
*   **Reliability**: The probability that the system produces correct outputs and does not fail under expected load. A system can be available but unreliable (returning 500 errors).

### 454. What is eventual consistency?

*   **Definition**: A consistency model where, if no new updates are made to a given data item, eventually all accesses to that item will return the last updated value.
*   **Trade-off**: Sacrifices strong consistency for high availability (BASE model).
*   *Example*: Updating a Facebook post caption. It might take a few seconds to reflect on your friend's feed.

### 455. What is a CAP theorem?

*   **Theorem**: In a distributed data store, you can only guarantee 2 out of 3:
    1.  **Consistency (C)**: Every read receives the most recent write or an error.
    2.  **Availability (A)**: Every request receives a (non-error) response, without the guarantee that it contains the most recent write.
    3.  **Partition Tolerance (P)**: The system continues to operate despite an arbitrary number of messages being dropped/delayed by the network.
*   **Reality**: In distributed systems, P is mandatory. You must choose between CP (Consistency) and AP (Availability).

### 456. What is partition tolerance?

*   **Definition**: The cluster continues to function even if communication between two nodes is broken (network partition).
*   **Handling**:
    *   **CP System**: If link breaks, stop accepting writes to ensure consistency.
    *   **AP System**: If link breaks, allow writes to both sides, deal with conflicts later (Eventual Consistency).

### 457. What is sharding?

*   **Definition**: A method of splitting and storing a single logical dataset in multiple databases.
*   **Horizontal Partitioning**: Splitting rows by a key (e.g., `User ID`). Users 1-1000 go to DB1, 1001-2000 go to DB2.
*   **Pros**: Infinite write scalability.
*   **Cons**: Complex to query across shards (Joins), re-balancing data is hard.

### 458. What is replication? Master-slave vs multi-master?

*   **Master-Slave**:
    *   One writer (Master), multiple readers (Slaves).
    *   Slaves sync from Master asynchronously.
    *   *Pros*: Simple, Good for Read-heavy.
*   **Multi-Master (Leaderless)**:
    *   Multiple nodes accept writes.
    *   *Pros*: High write availability.
    *   *Cons*: Write conflicts (Two users edit same doc at same time).

### 459. What is quorum in distributed systems?

*   **Definition**: The minimum number of votes that a distributed transaction has to obtain in order to be allowed to perform an operation.
*   **Formula**: `R + W > N`.
    *   `N` = Total nodes.
    *   `R` = Nodes needed for Read.
    *   `W` = Nodes needed for Write.
*   **Example**: N=3, W=2, R=2. You write to 2 nodes. You read from 2 nodes. Guaranteed to see the latest write.

### 460. What is a leader election?

*   **Problem**: In a distributed system (like a cluster of schedulers), you need *one* node to be the coordinator to avoid duplicate work.
*   **Algorithms**:
    *   **Bully Algorithm**: Node with highest ID wins.
    *   **Raft / Paxos**: Consensus algorithms (used by Etcd/Consul).
    *   **Zookeeper/Redis**: Use an external lock service. `SET resource_name my_id NX EX 10`. Whoever gets the lock is the leader.

### 461. What are consistent hashing and its use?

*   **Problem**: In normal hashing (`key % n`), if `n` changes (server added/removed), almost all keys are remapped.
*   **Solution**: Map both Servers and Keys to a circle (ring) [0-360°]. A key is assigned to the next server in clockwise direction.
*   **Benefit**: Adding/Removing a node only affects the keys in the immediate neighbor segment (1/n keys), not all keys. Used in Cassandra, DynamoDB, Distributed Caches.

### 462. What is cache invalidation?

*   **Definition**: The process of removing or updating stale data in the cache when the underlying data source (DB) changes.
*   **Policies**:
    *   **TTL (Time To Live)**: Auto-expire after X seconds. (Eventual consistency).
    *   **Explicit Deletion**: App deletes cache key on DB update. (Cache-Aside).
*   **Quote**: "There are only two hard things in Computer Science: cache invalidation and naming things." - Phil Karlton.

### 463. How to handle cache synchronization across nodes?

*   **Local Cache (EhCache)**: If Node A updates a record, Node B's local cache is stale.
*   **Solutions**:
    *   **Distributed Cache (Redis)**: Best solution. All nodes read from shared Redis. No sync needed.
    *   **Pub/Sub**: Publish "Invalidate Key X" event to a topic. All nodes listen and clear local cache (Message Broadcasting).

### 464. What is a load balancer? How does it work?

*   **Definition**: A device that acts as a reverse proxy and distributes network or application traffic across a number of servers.
*   **Types**:
    *   **L4 (Transport)**: Balances based on IP/Port (TCP). Very fast. (AWS NLB).
    *   **L7 (Application)**: Balances based on HTTP Headers, URL paths. (AWS ALB, Nginx).
*   **Algorithms**: Round Robin, Least Connections, IP Hash.

### 465. What is sticky session?

*   **Definition**: A load balancing technique where requests from a specific client are always routed to the *same* server for the duration of the session.
*   **Mechanism**: LB sets a cookie (`SERVERID=NodeA`).
*   **Use Case**: Legacy apps storing Session in process memory. Modern apps should be stateless (Session in Redis) and avoid sticky sessions.

### 466. What is a CDN? How does it improve performance?

*   **CDN (Content Delivery Network)**: A network of geographically distributed servers (Edge locations).
*   **Function**: Caches static content (Images, CSS, JS, Videos) closer to the user.
*   **Benefit**:
    *   Lower Latency (User in London fetches from London Edge, not US Origin).
    *   Reduced Load on Origin Server.

### 467. What are API rate limits and why needed?

*   **Definition**: Restricting the number of requests a user/client can make within a time window (e.g., 100 req/min).
*   **Why**:
    *   **Prevent Abuse**: DDOS attacks, Brute force scanning.
    *   **Fair Usage**: Prevent one tenant from hogging resources.
    *   **Cost Management**: Control reliance on downstream paid APIs.
*   **Headers**: `X-RateLimit-Limit`, `X-RateLimit-Remaining`, `Retry-After`.

### 468. What is message deduplication?

*   **Problem**: In distributed systems, retries cause duplicate messages.
*   **Consumer Side**: Store processed Message IDs in a DB/Redis. Before processing, check `EXISTS(msg_id)`.
*   **Producer Side (Kafka)**: Use Idempotent Producer (`enable.idempotence=true`) which assigns sequence numbers to batches to prevent duplicate commits during network errors.

### 469. What is idempotency?

*   **Definition**: An operation is idempotent if applying it multiple times has the same effect as applying it once.
*   **Examples**:
    *   `GET`, `PUT`, `DELETE` are idempotent.
    *   `POST` is NOT idempotent (creates multiple resources).
*   **Implementation**: Client sends a unique `Idempotency-Key` header (UUID). Server checks if Key exists. If yes, return cached response; else process.

### 470. What is a distributed lock?

*   **Problem**: Ensuring only one node performs a critical task (e.g., generating a daily report) in a cluster.
*   **Solutions**:
    *   **Redis (Redlock)**: `SET key value NX PX 10000`. Set if Not Exists, with Expiry.
    *   **Zookeeper**: Create an Ephemeral Sequential node. Node with lowest sequence gets lock.
    *   **Database**: `SELECT * FROM locks WHERE name='report' FOR UPDATE`.

### 481. What is gRPC and when is it better than REST?

*   **gRPC (Google Remote Procedure Call)**:
    *   **Protocol**: Uses HTTP/2 (Multiplexing, Streaming).
    *   **Data Format**: Protobuf (Binary, strongly typed, smaller size).
    *   **Contract**: Strict .proto file definition.
*   **vs REST**:
    *   gRPC is faster (binary serialization).
    *   Better for internal microservices communication.
    *   REST (JSON/HTTP1.1) is better for public APIs (browser compatibility).

### 482. What is API Gateway and what are its roles?

*   **Definition**: A server that acts as an entry point into a system (e.g., Zuul, Spring Cloud Gateway, Kong, AWS API Gateway).
*   **Roles**:
    *   **Routing**: `/users` -> User Service, `/orders` -> Order Service.
    *   **Authentication**: Verify JWT token once at entry.
    *   **Rate Limiting**: Throttling requests.
    *   **Aggregation**: Call multiple services and combine results (BFF Pattern).
    *   **Protocol Translation**: HTTP -> gRPC/AMQP.

### 483. How do you ensure observability in distributed systems?

*   **Three Pillars**:
    1.  **Logs**: "What happened?" (ELK Stack, Splunk). structured JSON logs with `traceId`.
    2.  **Metrics**: "Is it healthy?" (Prometheus, Grafana). CPU, RAM, Response Time, Error Rate.
    3.  **Traces**: "Where did it happen?" (Jaeger, Zipkin). Follow a request across microservices using a Correlation ID.

### 484. What are retries and exponential backoff?

*   **Retry**: Re-executing a failed operation (e.g., DB connection, API call).
*   **Problem**: Immediate retry can overload a struggling service (Thundering Herd).
*   **Exponential Backoff**: Wait longer between retries.
    *   Attempt 1: Wait 1s.
    *   Attempt 2: Wait 2s.
    *   Attempt 3: Wait 4s.
*   **Jitter**: Add random noise (e.g., Wait 4s + random(100ms)) to prevent synchronized retries.

### 485. How to achieve fault tolerance in microservices?

1.  **Circuit Breaker**: Fail fast if downstream is down (Resilience4j).
2.  **Bulkhead**: Isolate resources (Thread pools) so one failure doesn't crash the whole system.
3.  **Timeouts**: Never wait indefinitely.
4.  **Fallback**: Return default value or cached data on failure.
5.  **Retry**: For transient errors.

### 486. How to horizontally scale a database?

*   **Sharding**: Split data across multiple nodes based on a Shard Key.
    *   *Read/Write Scale*: Both increase linearly with nodes.
*   **Read Replicas**: Master Node (Write) + N Slave Nodes (Read).
    *   *Read Scale*: Increases.
    *   *Write Scale*: Limited to Master capacity.

### 487. What is an outbox pattern?

*   **Problem**: Dual Write. Writing to DB and publishing to Kafka must be atomic. If DB commits but Kafka fails, data is inconsistent.
*   **Solution**:
    1.  Start Transaction.
    2.  Insert Entity into `Orders` table.
    3.  Insert Event into `Outbox` table in the *same* DB transaction.
    4.  Commit Transaction (Atomic).
    5.  **Relay Process**: A separate process (Debezium/Poller) reads `Outbox` table and pushes to Kafka.

### 488. What is eventual consistency using Kafka?

*   **Scenario**: Order Service creates order -> Publishes `OrderCreated` event -> Inventory Service consumes it -> Updates Stock.
*   **State**: The system is inconsistent for a few milliseconds (Order created, but Stock not yet deducted).
*   **Eventual**: Once the message is processed, both systems will be consistent.
*   **Design**: UI should reflect "Processing" state or use optimistic updates.

### 489. How to maintain ACID in distributed systems?

*   **Hard Truth**: You generally assume BASE (Eventual Consistency).
*   **If ACID is must**:
    *   **2PC (Two-Phase Commit)**: Coordinator asks all nodes "Can you commit?". If all say yes, tells them "Commit". (Slow, blocking).
    *   **Saga Pattern**:
        *   **Choreography**: Service A emits event, B listens.
        *   **Orchestration**: Central coordinator tells A then B what to do.
        *   **Compensation**: If Step 2 fails, trigger "Undo Step 1" transaction.

### 490. What is data deduplication?

*   **Storage Level**: Identifying identical blocks of data (in backups/storage) and storing only one copy + references.
*   **Application Level**:
    *   **Bloom Filter**: Probabilistic data structure to quickly check "Have I seen this before?". False positives possible, false negatives impossible.
    *   **Hash Check**: Store SHA-256 of payload in DB.

### 491. What are shadow writes and reads?

*   **Shadow Write**: A deployment strategy where incoming traffic is duplicated and sent to both the existing (Live) version and the new (Shadow) version.
    *   *Purpose*: Test the new version under real load conditions without affecting actual users (Shadow responses are discarded).
*   **Shadow Read**: Reading from a new data store concurrently with the old one to verify data consistency during migration.

### 492. What is a quorum write/read?

*   (See Q459)
*   **Definition**: A consensus mechanism ensuring consistency in distributed systems.
*   **Write Quorum (W)**: Write is successful only if acknowledged by W nodes.
*   **Read Quorum (R)**: Read is successful only if R nodes agree on the value.
*   **Condition**: `R + W > N` guarantees reading the latest write (Strong Consistency).

### 493. What are the tradeoffs of NoSQL vs SQL?

*   **SQL (RDBMS)**:
    *   *Pros*: ACID Compliance, Structured Data, Complex JOINs, Standardized language.
    *   *Cons*: Hard to scale horizontally (Sharding is manual/complex), Rigid schema.
*   **NoSQL**:
    *   *Pros*: Flexible schema, Easy horizontal scaling, High write throughput.
    *   *Cons*: Eventual consistency (usually), Limited query capabilities (No complex JOINs).

### 494. How do you scale a notification service?

*   **Components**:
    *   **Queue (Kafka/RabbitMQ)**: Buffer incoming requests (`SendEmail`, `SendPush`).
    *   **Worker Pool**: Stateless consumers that pick tasks and call 3rd party APIs (FCM, SendGrid).
    *   **State Management**: Redis to store `MessageID` status (Deduplication).
    *   **Rate Limiting**: To prevent getting banned by 3rd party providers.

### 495. What is system resiliency?

*   **Definition**: The ability of a system to recover from failures and continue to function.
*   **Techniques**:
    *   **Redundancy**: No single point of failure (Deploy 2+ instances).
    *   **Graceful Degradation**: If Search Service is down, show "Recent Items" instead of error.
    *   **Self-Healing**: Kubernetes restarts crashed pods automatically.

### 496. What are retries vs compensation?

*   **Retry**: Re-doing the *same* operation assuming the failure was transient (e.g., Network timeout). Best for Idempotent operations.
*   **Compensation (Undo)**: Doing the *inverse* operation to revert state because the original operation failed permanently or business logic requires rollback (Saga Pattern).
    *   *Example*: `BookFlight` failed -> Start `RefundPayment`.

### 497. What is a read replica? When to use it?

*   **Definition**: A read-only copy of the primary (master) database.
*   **Sync**: Updates from Master are replicated asynchronously to Replicas.
*   **Use Case**:
    *   **Read-Heavy Workloads**: Reporting, Analytics, User Feeds.
    *   **Offloading**: Move complex `SELECT` queries to replica to keep Master free for critical `INSERT/UPDATE`s.

### 498. How do you implement distributed tracing?

*   **Mechanism**:
    1.  **Trace ID**: Generated at the entry point (Gateway/Load Balancer).
    2.  **Span ID**: Generated for each service call.
    3.  **Propagation**: Pass `Trace-ID` and `Span-ID` in HTTP Headers (`X-B3-TraceId`) across all microservices.
    4.  **Collection**: Each service sends async logs to a collector (Zipkin/Jaeger).

### 499. What is service orchestration vs choreography?

*   **Orchestration (Conductor)**:
    *   Central Coordinator (Order Service) tells everyone what to do.
    *   *Pros*: Easy to visualize flow.
    *   *Cons*: Tight coupling, Coordinator is a bottleneck.
*   **Choreography (Dance)**:
    *   No central coordinator. Services react to events.
    *   Order Service emits `OrderPlaced`. Inventory Service listens and emits `StockReserved`.
    *   *Pros*: Decoupled.
    *   *Cons*: Hard to track workflow status.

### 500. How do you handle schema evolution in microservices?

*   **Forward Compatibility**: Old code can read new data. (Add optional fields).
*   **Backward Compatibility**: New code can read old data. (Don't rename/delete fields).
*   **Strategy**:
    1.  **Protobuf/Avro**: Use numbered fields. Never reuse tags.
    2.  **Database**:
        *   Add new column (nullable).
        *   Deploy Code to write to both (Dual Write).
        *   Backfill old rows.
        *   Remove old column support in next version.
