## 01. Explain OOP principles with real-time examples.

**Answer:**
Object-Oriented Programming (OOP) revolves around four main pillars:
1.  **Encapsulation:** Wrapping data (variables) and code (methods) together as a single unit. It hides internal details and protects data.
    *   *Real-time Example:* A **Medical Capsule** wraps different medicines inside, hiding the complexity of the chemical mix.
2.  **Inheritance:** Mechanism where a child class acquires properties and behaviors of a parent class. Promotes code reuse.
    *   *Real-time Example:* A **Child** inherits genetic traits (eye color, height) from their **Parents**.
3.  **Polymorphism:** "Many forms." Ability of a method to do different things based on the object it is acting upon.
    *   *Real-time Example:* A **Person** behaves differently in different roles: as a Student in school, a Customer in a mall, and a Passenger in a bus.
4.  **Abstraction:** Hiding implementation details and showing only functionality to the user.
    *   *Real-time Example:* A **Car Dashboard**. You use the steering wheel and pedals (interface) without knowing how the engine's internal combustion works (implementation).

**Code Snippet:**
```java
// Encapsulation
class Account {
    private double balance; // Hidden data
    public void deposit(double amount) { balance += amount; } // Controlled access
}

// Inheritance & Polymorphism
class Animal { void sound() { System.out.println("Animal sound"); } }
class Dog extends Animal { void sound() { System.out.println("Bark"); } } // Overriding

// Abstraction
abstract class Vehicle { abstract void start(); }
class Car extends Vehicle { void start() { System.out.println("Key turn"); } }
```

---

## 02. Difference between abstraction and encapsulation.

**Answer:**
*   **Encapsulation** is about **hiding data** (information hiding) and bundling it with methods. It solves the problem of implementation level. It shields the internal state from unauthorized access.
*   **Abstraction** is about **hiding complexity** (implementation details) and showing only the essential features. It solves the problem at the design level.

| Feature | Encapsulation | Abstraction |
| :--- | :--- | :--- |
| **Focus** | "How" to contain/secure data. | "What" the object does. |
| **Implementation** | `private`, `protected` modifiers, getters/setters. | `abstract` classes, `interfaces`. |
| **Goal** | Security & Modularity. | Simplicity & Interface design. |

**Code Snippet:**
```java
// Encapsulation: Hiding 'balance'
public class ATM {
    private double balance;
    public double getBalance() { return balance; }
}

// Abstraction: Hiding logic of 'withdraw'
interface BankOperation {
    void withdraw(double amount); // User knows THIS exists, not HOW it works
}
```

---

## 03. What is polymorphism? Compile-time vs runtime.

**Answer:**
Polymorphism allows an object to take many forms.
1.  **Compile-time Polymorphism (Static Binding):** Handled by **Method Overloading**. The compiler determines which method to call based on the method signature (arguments) at compile time.
2.  **Runtime Polymorphism (Dynamic Binding):** Handled by **Method Overriding**. The JVM determines which method to call based on the actual object type (not the reference type) at runtime.

**Code Snippet:**
```java
class Calculator {
    // Compile-time (Overloading)
    int add(int a, int b) { return a + b; }
    double add(double a, double b) { return a + b; }
}

class Parent { void show() { System.out.println("Parent"); } }
class Child extends Parent { void show() { System.out.println("Child"); } }

public class Test {
    public static void main(String[] args) {
        Parent obj = new Child(); 
        obj.show(); // Runtime (Overriding) -> Output: Child
    }
}
```

---

## 04. What is method overloading vs overriding?

**Answer:**
*   **Method Overloading:** Same method name, different parameter list (number or type of args) within the **same class**. It improves code readability. Return type alone cannot distinguish overloaded methods.
*   **Method Overriding:** Same method name, same parameter list, same return type (or covariant) in a **subclass** (parent-child relationship). It is used to provide a specific implementation of a method already defined in the parent class.

**Code Snippet:**
```java
class Demo {
    // Overloading
    void print(String s) { System.out.println(s); }
    void print(int i) { System.out.println(i); }
}

class Animal { void eat() { System.out.println("Generic food"); } }
class Cat extends Animal {
    // Overriding
    @Override
    void eat() { System.out.println("Fish"); } 
}
```

---

## 05. What is dynamic method dispatch?

**Answer:**
Dynamic Method Dispatch is the mechanism by which a call to an overridden method is resolved at **runtime** rather than compile-time. This is how Java implements Runtime Polymorphism.
When a parent class reference refers to a child class object (Upcasting), the version of the method executed is determined by the actual object type in the heap.

**Code Snippet:**
```java
class A { void m1() { System.out.println("A's m1"); } }
class B extends A { void m1() { System.out.println("B's m1"); } }

public class Dispatch {
    public static void main(String[] args) {
        A obj = new B(); // Upcasting
        obj.m1(); 
        // Output: "B's m1"
        // Compiler checks A.m1() exists. JVM executes B.m1().
    }
}
```

---

## 06. What is the difference between interface and abstract class?

**Answer:**

| Feature | Abstract Class | Interface |
| :--- | :--- | :--- |
| **Inheritance** | A class can extend only **one** abstract class. | A class can implement **multiple** interfaces. |
| **Members** | Can have instance variables, constructors, non-abstract methods. | Variables are `public static final`. No constructors. Methods are `public abstract` (pre-Java 8). |
| **Purpose** | To share common code/state among related classes ("Is-A"). | To define a contract/capability for unrelated classes ("Can-Do"). |
| **Java 8+** | Normal methods. | Can have `default` and `static` methods. |

**Code Snippet:**
```java
// Abstract Class (Partial implementation)
abstract class Bird {
    String color; // State allowed
    Bird(String c) { this.color = c; } // Constructor allowed
    abstract void fly();
}

// Interface (Contract)
interface Swimmable {
    int SPEED_LIMIT = 10; // Constants only
    void swim();
}
```

---

## 07. Can an abstract class have a constructor?

**Answer:**
**Yes**, an abstract class can have a constructor. Even though you cannot instantiate an abstract class using `new AbstractClass()`, the constructor is used to **initialize common fields** defined in the abstract class.
When a concrete subclass is instantiated, the abstract class constructor is called first (via `super()`) to ensure the parent part of the object is initialized correctly.

**Code Snippet:**
```java
abstract class Base {
    int x;
    Base(int x) { 
        this.x = x; 
        System.out.println("Base Constructor: " + x);
    }
}

class Derived extends Base {
    Derived(int x) {
        super(x); // Calls Base constructor
        System.out.println("Derived Constructor");
    }
}
// new Derived(10); prints Base Constructor: 10, then Derived Constructor.
```

---

## 08. What is multiple inheritance and how Java handles it?

**Answer:**
Multiple Inheritance is a feature where a class can inherit from more than one parent class.
*   **With Classes:** Java does **NOT** support multiple inheritance with classes (e.g., `class C extends A, B`) to avoid the **Diamond Problem** (ambiguity if both A and B have the same method).
*   **With Interfaces:** Java **supports** multiple inheritance with interfaces (e.g., `class C implements X, Y`). If two interfaces have the same method signature (and no implementation), there is no ambiguity because the implementation is provided in the child class C.

**Code Snippet:**
```java
interface Printable { void print(); }
interface Showable { void print(); }

// Allowed: implementing multiple interfaces
class Document implements Printable, Showable {
    @Override
    public void print() {
        System.out.println("Printing document..."); 
        // Resolves both interfaces' requirement
    }
}
```

---

## 09. What is the diamond problem?

**Answer:**
The Diamond Problem occurs in multiple inheritance when a class inherits from two classes that both inherit from a common superclass. If both parents override strictly the same method, the child class wouldn't know which version to inherit.
Java avoids this by disallowing multiple class inheritance.
However, with **Java 8 Default Methods** in interfaces, a similar ambiguity arises (`Diamond Problem with Interfaces`). Java forces the developer to override the conflicting method in the implementing class to resolve the ambiguity.

**Code Snippet:**
```java
interface A { default void hello() { System.out.println("A"); } }
interface B { default void hello() { System.out.println("B"); } }

// Compile Error if hello() is not overridden: "inherits unrelated defaults"
class C implements A, B {
    @Override
    public void hello() {
        A.super.hello(); // Resolve ambiguity manually
    }
}
```

---

## 10. What are marker interfaces?

**Answer:**
A **Marker Interface** (or Tagging Interface) is an interface **with no methods or fields**.
It serves as a "tag" or "metadata" instructions for the JVM or compiler. By implementing it, a class indicates that it belongs to a certain category or allows certain operations.
*   **Examples:** `Serializable` (allows object serialization), `Cloneable` (allows `clone()` method), `Remote` (RMI).

**Code Snippet:**
```java
// Implementing Serializable tells JVM this object can be converted to bytes
class User implements Serializable { 
    // No methods needed to implement
}

// JVM checks:
if (obj instanceof Serializable) {
    // Proceed with serialization
} else {
    throw new NotSerializableException();
}
```

---

## 11. Explain equals() and hashCode() contract.

**Answer:**
The `equals()` and `hashCode()` methods define how objects are compared and stored in hash-based collections (`HashMap`, `HashSet`, `Hashtable`).
*   **equals()**: Checks if two objects are meaningfully equivalent. Reflexive, Symmetric, Transitive, Consistent for non-null refs.
*   **hashCode()**: Returns an integer representation of the object.
    **The Contract**:
1.  If `x.equals(y)` is true, then `x.hashCode() == y.hashCode()` **MUST** be true.
2.  If `x.hashCode() == y.hashCode()`, `x.equals(y)` **might or might not** be true (Collision).
3.  If `x.equals(y)` is false, their hashCodes need not be different, but ideally should be for performance.

**Code Snippet:**
```java
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    User user = (User) o;
    return id == user.id && Objects.equals(name, user.name);
}

@Override
public int hashCode() {
    return Objects.hash(id, name); // Must use same fields as equals
}
```

---

## 12. What is clone() method?

**Answer:**
`clone()` is a method in the `Object` class used to create a copy of an object.
*   The class must implement the `Cloneable` interface (a marker interface), otherwise `super.clone()` throws `CloneNotSupportedException`.
*   The default implementation performs a **Shallow Copy** (copies primitive values and references).
*   For deep cloning, you must override `clone()` and manually copy mutable objects within the clone.

**Code Snippet:**
```java
class Employee implements Cloneable {
    String name;
    
    @Override
    protected Object clone() throws CloneNotSupportedException {
        return super.clone(); // Shallow Copy
    }
}
```

---

## 13. What is deep copy vs shallow copy?

**Answer:**
*   **Shallow Copy:** Creates a new object but copies the referenes of the instance variables. Both the original and the copy point to the same memory objects for non-primitive fields. Changing one affects the other. Default behavior of `clone()`.
*   **Deep Copy:** Creates a new object and recursively creates new copies of all objects referenced by the original object. The original and copy are completely independent.

**Code Snippet:**
```java
// Shallow Copy
List<String> list1 = new ArrayList<>();
List<String> list2 = list1; // Reference copy

// Deep Copy
List<String> list3 = new ArrayList<>();
for(String s : list1) {
    list3.add(new String(s)); // New Object for each element
}
```

---

## 14. What is finalize()? Is it used now?

**Answer:**
`finalize()` was a method in `Object` class called by the Garbage Collector before reclaiming an object's memory. Theoretically used for cleanup (closing files, connections).
*   **Is it used now? NO.** It is **Deprecated** since Java 9 and marked for removal.
*   **Issues:** Unpredictable execution time, performance penalties, can resurrect objects.
*   **Alternative:** Use `try-with-resources` or implement `AutoCloseable` interface for distinct resource management.

**Code Snippet:**
```java
// Deprecated way (DO NOT USE)
@Override
protected void finalize() throws Throwable {
    try { closeResource(); } 
    finally { super.finalize(); }
}

// Correct way (Java 7+)
try (FileInputStream fis = new FileInputStream("file.txt")) {
    // Use resource
} catch (IOException e) {
    e.printStackTrace();
} // Automatically closed here
```

---

## 15. What is immutability? How to create immutable class?

**Answer:**
Immutability means an object's state cannot be modified after it is created. `String`, `Integer`, `BigDecimal` are immutable.
To create an immutable class:
1.  Declare the class as `final` so it can’t be extended.
2.  Make all fields `private` and `final`.
3.  Do **not** provide setter methods.
4.  Initialize all fields via a constructor.
5.  If fields include mutable objects (like Lists), return a deep copy in getters.

**Code Snippet:**
```java
public final class ImmutableUser {
    private final int id;
    private final String name;

    public ImmutableUser(int id, String name) {
        this.id = id;
        this.name = name;
    }

    public int getId() { return id; }
    public String getName() { return name; }
    // No setters provided
}
```

---

## 16. Why String is immutable?

**Answer:**
1.  **String Constant Pool (SCP):** Java saves heap space by sharing specific string literals. If strings were mutable, changing one reference would affect all other reused references.
2.  **Security:** Strings are used for class loading, network connections, database URLs, usernames/passwords. Immutability prevents tampering.
3.  **Thread Safety:** Immutable objects are inherently thread-safe. They can be shared across threads without synchronization.
4.  **HashCode Caching:** Since the content won't change, the hash code is calculated once and cached, making Strings perfect keys for HashMaps.

**Code Snippet:**
```java
String s1 = "Java";
String s2 = "Java"; // s1 and s2 point to same object in Pool
s1 = "Python";      // Creates "Python", "Java" remains in Pool for s2
System.out.println(s2); // Output: Java
```

---

## 17. Difference between String, StringBuilder, StringBuffer.

**Answer:**
*   **String:** **Immutable**. Modifying it creates a new object. Slow for heavy modification. Stored in String Pool.
*   **StringBuffer:** **Mutable** and **Thread-Safe** (Synchronized methods). Slow due to synchronization overhead. Used in multi-threaded environments.
*   **StringBuilder:** **Mutable** and **Not Thread-Safe**. Fast (no synchronization). The preferred choice for single-threaded string manipulation (Java 5+).

**Code Snippet:**
```java
// Fast string manipulation
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World"); // Modifies existing object
System.out.println(sb); // Output: Hello World
```

---

## 18. What is String Pool?

**Answer:**
The String Pool (String Intern Pool) is a special storage area in the Java Heap memory.
*   When a string literal is created (`String s = "Hello";`), the JVM checks the pool. If "Hello" exists, it returns the reference. If not, it creates a new string in the pool.
*   Strings created with `new` keyword (`new String("Hello")`) force the creation of a new object in the **Heap** (outside the pool), ignoring the pool check. You can move it to the pool manually using `intern()`.

**Code Snippet:**
```java
String s1 = "Cat";              // Pool
String s2 = "Cat";              // Pool (Refers to same object as s1)
String s3 = new String("Cat");  // Heap (Distinct object)

System.out.println(s1 == s2); // true
System.out.println(s1 == s3); // false
System.out.println(s1 == s3.intern()); // true
```

---

## 19. What is reflection in Java?

**Answer:**
Reflection is an API (in `java.lang.reflect` package) that allows a program to inspect and modify the runtime behavior of applications.
*   **Capabilities:** It can inspect classes, interfaces, fields, and methods at runtime, without knowing their names at compile time. It can instantiate objects, invoke methods, and change field values (even private ones).
*   **Drawbacks:** Slower performance, breaks encapsulation security, harder to debug. Used heavily in frameworks (Spring, Hibernate, JUnit).

**Code Snippet:**
```java
class PrivateTest { 
    private String secret = "Hidden Code"; 
}

public class ReflectionDemo {
    public static void main(String[] args) throws Exception {
        PrivateTest obj = new PrivateTest();
        Field field = PrivateTest.class.getDeclaredField("secret");
        field.setAccessible(true); // Bypass private access check
        System.out.println("Secret: " + field.get(obj)); 
    }
}
```

---

## 20. Where are objects stored in memory?

**Answer:**
Java memory is mainly divided into Stack and Heap.
1.  **Heap Memory:** Where all **Objects** (instances of classes) and Arrays are stored. Objects live here until Garbage Collected. It is shared by all threads.
2.  **Stack Memory:** Stores method execution frames, **primitive variables**, and **reference variables** (which point to objects in the Heap). Each thread has its own stack.
3.  **Metaspace:** Stores class definitions (metadata), static variables, and method bytecode.

**Code Snippet:**
```java
public void memoryDemo() {
    int i = 10;                     // Stack (Primitive)
    Employee e = new Employee();    // 'e' reference in Stack, Object in Heap
    // When method ends, Stack frame ('i', 'e') is popped. 
    // Employee object remains in Heap until GC runs.
}
```

---

## 21. Checked vs Unchecked exceptions.

**Answer:**
*   **Checked Exceptions:** Exceptions that are checked at **compile-time**. Ideally used for recoverable conditions (e.g., file not found, network issue). The method must handle them (try-catch) or declare them (throws).
*   **Unchecked Exceptions:** Exceptions that occur at **runtime**. They extend `RuntimeException`. Ideally used for programming errors (e.g., null pointer, index out of bounds). No need to handle or declare explicitly.

| Feature | Checked | Unchecked |
| :--- | :--- | :--- |
| **Parent** | `Exception` | `RuntimeException` |
| **Check** | Compile-Time | Runtime |
| **Rule** | Must Handle/Declare | Optional |
| **Examples** | `IOException`, `SQLException` | `NullPointerException`, `ArithmeticException` |

**Code Snippet:**
```java
// Checked: Compiler forces handling
try {
    FileReader fr = new FileReader("file.txt");
} catch (FileNotFoundException e) {
    e.printStackTrace();
}

// Unchecked: Compiler doesn't complain
int a = 10 / 0; // Throws ArithmeticException at runtime
```

---

## 22. Difference between throw and throws.

**Answer:**
*   **`throw`:** Used generally within a method body to **explicitly throw** an exception instance. It is followed by an object (instance).
*   **`throws`:** Used in a **method signature** to declare that the method *might* throw specific exceptions. It transfers the responsibility of handling to the caller. It is followed by class names.

**Code Snippet:**
```java
// 'throws' declares the possibility
public void readFile() throws IOException {
    // 'throw' explicitly creates the exception
    throw new IOException("File corrupted"); 
}

public void main() {
    try {
        readFile();
    } catch (IOException e) {
        // Handle here
    }
}
```

---

## 23. Can we catch multiple exceptions in one block?

**Answer:**
**Yes**, starting from **Java 7**, we can catch multiple exceptions in a single `catch` block using the pipe (`|`) operator. This reduces code duplication.
*   **Constraint:** The exceptions in the multi-catch block must **not** have a parent-child relationship (e.g., you cannot do `catch (Exception | IOException e)` because `IOException` is redundant).

**Code Snippet:**
```java
try {
    // Code that might throw multiple exceptions
    Class.forName("com.mysql.jdbc.Driver");
    int res = 10 / 0;
} catch (ClassNotFoundException | ArithmeticException e) {
    // Common handling logic
    System.out.println("Error: " + e.getMessage());
    // Note: The variable 'e' effectively final here
}
```

---

## 24. What happens if finally block throws exception?

**Answer:**
If the `finally` block throws an exception:
1.  The original exception (thrown from `try` or `catch`) is **lost/suppressed**.
2.  The new exception from `finally` is propagated up the stack to the caller.
    This is considered a bad practice because the root cause of the error is masked. We should handle exceptions within `finally` to prevent this.

**Code Snippet:**
```java
try {
    throw new RuntimeException("Original Error"); // Lost
} finally {
    throw new RuntimeException("Finally Error"); // Propagated
}
// Caller receives "Finally Error"
```

---

## 25. What is try-with-resources?

**Answer:**
Introduced in **Java 7**, `try-with-resources` allows automatic management of resources (like files, sockets, database connections).
*   Any object that implements `AutoCloseable` or `Closeable` can be declared inside the `try(...)` parenthesis.
*   Java ensures that `close()` is called on these resources automatically at the end of the block, regardless of whether an exception occurred or not.
*   It replaces the concise `try-finally` block for closing resources.

**Code Snippet:**
```java
// Resource declared in try()
try (BufferedReader br = new BufferedReader(new FileReader("test.txt"))) {
    System.out.println(br.readLine());
} catch (IOException e) {
    e.printStackTrace();
} 
// br.close() is called automatically here
```

---

## 26. How to create custom exception?

**Answer:**
To create a custom exception, extend:
*   `Exception` class for a **Checked Exception**.
*   `RuntimeException` class for an **Unchecked Exception**.
    Usually, we provide a constructor that accepts a message and passes it to the superclass constructor.

**Code Snippet:**
```java
// 1. Define Custom Exception
class InsufficientFundsException extends Exception {
    public InsufficientFundsException(String message) {
        super(message);
    }
}

// 2. Use it
public void withdraw(double amount) throws InsufficientFundsException {
    if (amount > 1000) {
        throw new InsufficientFundsException("Limit Exceeded");
    }
}
```

---

## 27. What is suppressed exception?

**Answer:**
Suppressed Exceptions are exceptions that are thrown but "ignored" in favor of another exception.
This typically happens in `try-with-resources`:
1.  An exception is thrown from the `try` block (Primary Exception).
2.  While closing the resource, the `close()` method also throws an exception (Secondary Exception).
3.  Prior to Java 7, the secondary masked the primary.
4.  With `try-with-resources`, the Primary Exception is thrown, and the Secondary Exception is **added as a suppressed exception** to the primary one. You can retrieve it using `getSuppressed()`.

**Code Snippet:**
```java
 try (AutoCloseable r = () -> { throw new Exception("Close Error"); }) {
     throw new Exception("Try Error");
 } catch (Exception e) {
     System.out.println("Primary: " + e.getMessage()); // Try Error
     for (Throwable t : e.getSuppressed()) {
         System.out.println("Suppressed: " + t.getMessage()); // Close Error
     }
 }
```

---

## 28. What is exception chaining?

**Answer:**
Exception Chaining dictates that when one exception causes another exception, we should preserve the original exception (cause) to help with debugging.
The `Throwable` class (and most Exceptions) has a constructor `Exception(String message, Throwable cause)` or method `initCause(Throwable cause)` to link the original exception.

**Code Snippet:**
```java
try {
    // Low-level DB error
    throw new SQLException("Connection Failed");
} catch (SQLException e) {
    // Wrap in High-level exception + Maintain chain
    throw new RuntimeException("Database Service Unavailable", e);
}
// Stack trace will show: RuntimeException caused by SQLException
```

---

## 29. Can we override a method with broader exception?

**Answer:**
**Rule for Overriding (Exception Handling):**
*   **Unchecked Exceptions:** You can throw **any** unchecked exception, regardless of the parent method.
*   **Checked Exceptions:**
    1.  The child method can throw the **same** exception.
    2.  The child method can throw a **subclass** (narrower) of the exception.
    3.  The child method can throw **no** exception.
    4.  **Restrictions:** The child method **CANNOT** throw a **broader** (superclass) checked exception or a **new** checked exception not declared by the parent.

**Code Snippet:**
```java
class Parent {
    void work() throws IOException {} // Declares IOException
}

class Child extends Parent {
    // Valid: IOException, FileNotFoundException, or nothing
    // Invalid: Exception (Broader), SQLException (New)
    @Override
    void work() throws FileNotFoundException {} 
}
```

---

## 30. What is stack unwinding?

**Answer:**
Stack Unwinding is the process of cleaning up stack frames during exception handling.
When an exception creates a scenario where the method cannot continue:
1.  The runtime looks for a matching `catch` block in the current method.
2.  If not found, it pops the current stack frame (effectively returning from the method abruptly) and passes the exception to the caller.
3.  This repeats up the call stack until a handler is found or the main method is exited (program crash).
    During this process, `finally` blocks in each frame are executed before the frame is popped.

**Code Snippet:**
```java
// Method A calls B, B calls C.
// C throws Error.
// C pops -> check B.
// B pops -> check A.
// A catches it.
// This popping process 'unwinds' the stack.
```

---

## 31. What are functional interfaces?

**Answer:**
A **Functional Interface** is an interface that contains **exactly one abstract method**. It can have any number of default or static methods.
*   They form the basis for **Lambda Expressions** in Java.
*   Marked with `@FunctionalInterface` annotation (optional but recommended for compile-time check).
*   **Examples:** `Runnable`, `Callable`, `Comparator`, and the `java.util.function` package interfaces (`Predicate`, `Consumer`, `Supplier`, `Function`).

**Code Snippet:**
```java
@FunctionalInterface
interface Calculator {
    int operate(int a, int b); // Single abstract method
}

// Usage with Lambda
Calculator add = (a, b) -> a + b;
System.out.println(add.operate(5, 3)); // Output: 8
```

---

## 32. What is lambda expression?

**Answer:**
A Lambda Expression is an anonymous function (no name, no return type, no modifiers) that allows you to treat code as data. It provides a concise way to implement a **Functional Interface**.
*   **Syntax:** `(parameters) -> expression` or `(parameters) -> { statements; }`
*   It eliminates the need for bulky anonymous inner classes.

**Code Snippet:**
```java
// Pre-Java 8 (Anonymous Inner Class)
Runnable r1 = new Runnable() {
    @Override
    public void run() { System.out.println("Old Way"); }
};

// Java 8 (Lambda)
Runnable r2 = () -> System.out.println("New Way");
```

---

## 33. How does Stream API work internally?

**Answer:**
Streams are wrappers around a data source (collection, array, I/O) allowing efficient, functional-style operations.
*   **Pipeline:** They typically form a pipeline: Source -> Intermediate Operations (Filter, Map) -> Terminal Operation (Collect, Reduce).
*   **Lazy Evaluation:** Intermediate operations are lazy. They don't run until a terminal operation is invoked.
*   **Internal Iteration:** Unlike Collections (where you use `for-each`), Streams handle iteration internally (potentially in parallel).

**Code Snippet:**
```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");

// Filter names starting with 'C', convert to Upper, then Print
names.stream()
     .filter(n -> n.startsWith("C")) // Intermediate (Lazy)
     .map(String::toUpperCase)       // Intermediate (Lazy)
     .forEach(System.out::println);  // Terminal (Triggers execution)
```

---

## 34. Intermediate vs terminal operations.

**Answer:**
*   **Intermediate Operations:** Return a new Stream. They are lazy (not executed immediately). Examples: `filter()`, `map()`, `sorted()`, `distinct()`, `limit()`.
*   **Terminal Operations:** Produce a result (non-stream) or side-effect. They trigger the pipeline execution and close the stream. Examples: `collect()`, `forEach()`, `reduce()`, `count()`, `anyMatch()`.

**Code Snippet:**
```java
Stream<String> s = Stream.of("A", "B", "C");

// Intermediate: Returns Stream<String>
Stream<String> s2 = s.filter(x -> !x.equals("B")); 

// Terminal: Returns long
long count = s2.count(); 
```

---

## 35. What is Optional?

**Answer:**
`Optional<T>` is a container object introduced in Java 8 to avoid `NullPointerException` (The "Billion Dollar Mistake").
*   It may or may not contain a non-null value.
*   It encourages programmers to handle the "absent value" case explicitly using methods like `isPresent()`, `orElse()`, `orElseGet()`, or `orElseThrow()`.

**Code Snippet:**
```java
public Optional<String> findName() {
    return Optional.ofNullable(null); // Safely wrapping null
}

// Usage
Optional<String> opt = findName();
String name = opt.orElse("Default Name"); // No NPE risk
System.out.println(name);
```

---

## 36. What is method reference?

**Answer:**
Method References are shorthand notation for writing Lambda expressions that just call an existing method. They use the `::` operator.
Four types:
1.  **Static Method:** `String::valueOf` (Equivalent to `x -> String.valueOf(x)`)
2.  **Instance Method of Object:** `System.out::println` (Equivalent to `x -> System.out.println(x)`)
3.  **Instance Method of Type:** `String::toUpperCase` (Equivalent to `(str) -> str.toUpperCase()`)
4.  **Constructor:** `ArrayList::new` (Equivalent to `() -> new ArrayList()`)

**Code Snippet:**
```java
List<String> list = Arrays.asList("a", "b", "c");

// Lambda
list.forEach(s -> System.out.println(s));

// Method Reference
list.forEach(System.out::println);
```

---

## 37. What is default method in interface?

**Answer:**
Prior to Java 8, interfaces could only have abstract methods. `default` methods allow interfaces to have methods with implementation.
*   **Purpose:** Backward compatibility. It allows adding new methods to interfaces without breaking existing implementing classes (e.g., adding `stream()` to `Collection` interface).
*   **Diamond Problem:** If a class implements two interfaces with the same default method, it **must** override the method to resolve conflict.

**Code Snippet:**
```java
interface Vehicle {
    default void honk() {
        System.out.println("Honk!");
    }
}

class Car implements Vehicle {
    // Car gets honk() automatically without code usage
}
```

---

## 38. What is CompletableFuture?

**Answer:**
`CompletableFuture` (Java 8) is an enhancement over `Future` for asynchronous programming.
*   **Non-blocking:** Unlike `Future.get()` which blocks, `CompletableFuture` allows specific callback functions (`thenApply`, `thenAccept`) to run when the task completes.
*   **Chaining:** You can chain multiple asynchronous tasks together.
*   **Composition:** You can combine results of multiple futures (`allOf`, `anyOf`, `thenCombine`).

**Code Snippet:**
```java
CompletableFuture.supplyAsync(() -> "Hello")
    .thenApply(s -> s + " World")
    .thenAccept(System.out::println); // Prints "Hello World" asynchronously
```

---

## 39. What are new Date/Time APIs?

**Answer:**
Java 8 introduced the `java.time` package (based on Joda-Time) to fix issues with `java.util.Date` (mutable, not thread-safe, bad API).
Key Classes (All Immutable & Thread-Safe):
1.  **LocalDate:** Date without time (YYYY-MM-DD).
2.  **LocalTime:** Time without date (HH:mm:ss).
3.  **LocalDateTime:** Both Date and Time.
4.  **ZonedDateTime:** Date and Time with Timezone ISO-8601.
5.  **Period/Duration:** Differences between dates/times.

**Code Snippet:**
```java
LocalDate date = LocalDate.now();
LocalTime time = LocalTime.now();
LocalDateTime dt = LocalDateTime.now();

// Easy Formatting
DateTimeFormatter fmt = DateTimeFormatter.ofPattern("dd-MM-yyyy");
System.out.println(date.format(fmt));
```

---

## 40. What is var in Java?

**Answer:**
`var` (Java 10) allows **Local Variable Type Inference**.
*   The compiler infers the type of the variable based on the initializer.
*   **Usage:** Only for local variables with initializers (loops, try-with-resources).
*   **Cannot use:** For fields, method parameters, return types, or variables without initialization/null.

**Code Snippet:**
```java
var message = "Hello, Java 10"; // Infers String
var list = new ArrayList<String>(); // Infers ArrayList<String>

System.out.println(message.getClass().getName()); // java.lang.String
```