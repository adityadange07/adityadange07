# 1000 Java Backend Interview Questions

---

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

---

## 41. What is JDBC architecture?

**Answer:**
JDBC (Java Database Connectivity) is a standard Java API (application programming interface) for database-independent connectivity between the Java programming language and a wide range of databases (SQL).
**Architecture Layers:**
1.  **JDBC API:** Provide standard interfaces (Connection, Statement, ResultSet) for application-to-JDBC Manager communication.
2.  **JDBC Driver Manager:** Manages a list of database drivers. It matches connection requests from the java application with the proper database driver.
3.  **JDBC Driver:** Communicates with the respective database server.

**Code Snippet:**
```java
// Standard Architecture Usage
Class.forName("com.mysql.cj.jdbc.Driver"); // Load Driver
Connection con = DriverManager.getConnection(url, user, password); // Connect
Statement stmt = con.createStatement(); // Create Statement
ResultSet rs = stmt.executeQuery("SELECT * FROM users"); // Execute Query
```

---

## 42. What are JDBC drivers types?

**Answer:**
There are 4 types of JDBC drivers:
1.  **Type-1 (JDBC-ODBC Bridge):** Translates JDBC calls to ODBC calls. Deprecated and removed in Java 8. **Slowest.**
2.  **Type-2 (Native-API Driver):** Converts JDBC calls into native C/C++ API calls of the database. Requires client-side library installation.
3.  **Type-3 (Network Protocol Driver):** Converts JDBC calls into a database-independent network protocol, which is then translated to a database protocol by a middleware server.
4.  **Type-4 (Thin Driver):** Converts JDBC calls directly into the vendor-specific database protocol. Pure Java. **Fastest** and most commonly used today.

**Code Snippet:**
```java
// Type-4 Driver (Most common in modern apps)
// Example: MySQL Connector/J
String url = "jdbc:mysql://localhost:3306/mydb";
// No native libraries needed on client machine.
```

---

## 43. What is connection pooling?

**Answer:**
Connection Pooling is a technique used to enhance performance by maintaining a **cache of database connections**.
*   **Problem:** Creating a new database connection for every request is expensive (network handshake, authentication).
*   **Solution:** A pool of connections is created at startup. When an application needs a connection, it borrows one from the pool, uses it, and returns it to the pool (instead of closing it).
*   **Tools:** HikariCP (Default in Spring Boot), Apache DBCP, C3P0.

**Code Snippet:**
```java
// HikariCP Configuration Example (Conceptual)
HikariConfig config = new HikariConfig();
config.setJdbcUrl("jdbc:mysql://localhost:3306/simpsons");
config.setUsername("bart");
config.setPassword("51mp50n");
config.setMaximumPoolSize(10); // Pool Size

HikariDataSource ds = new HikariDataSource(config);
Connection conn = ds.getConnection(); // Get from pool
// ... use conn ...
conn.close(); // Returns to pool, doesn't actually close
```

---

## 44. What is JNDI?

**Answer:**
JNDI (Java Naming and Directory Interface) is an API that allows applications to look up data and resources (like Databases, EJBs, JMS Queues) via a name.
*   **Use Case:** In a web server (Tomcat/JBoss), you configure the DataSource (DB connection) once in the server configuration. The web application uses JNDI to "lookup" this DataSource by name, decoupling the app from the database configuration.

**Code Snippet:**
```java
// JNDI Lookup in Java Code
Context ctx = new InitialContext();
// "jdbc/MyDataSource" is the name configured in server.xml/context.xml
DataSource ds = (DataSource) ctx.lookup("java:/comp/env/jdbc/MyDataSource");
Connection conn = ds.getConnection();
```

---

## 45. What is servlet lifecycle?

**Answer:**
A Servlet is a Java object that runs on a web server to handle HTTP requests. Its lifecycle is managed by the **Servlet Container** (e.g., Tomcat):
1.  **Loading & Instantiation:** The container loads the class and creates an instance.
2.  **Initialization (`init()`):** Called **once** to initialize resources (db connection, parameters).
3.  **Request Handling (`service()`):** Called **for each request**. It dispatches the request to `doGet()`, `doPost()`, etc. Multi-threaded.
4.  **Destruction (`destroy()`):** Called **once** when the servlet is removed or server shuts down. Used for cleanup.

**Code Snippet:**
```java
public class MyServlet extends HttpServlet {
    public void init() { 
        System.out.println("Servlet Initialized"); 
    }
    public void doGet(HttpServletRequest req, HttpServletResponse res) {
        System.out.println("Handling Request");
    }
    public void destroy() { 
        System.out.println("Servlet Destroyed"); 
    }
}
```

---

## 46. What is filter in servlet?

**Answer:**
A Filter is an object that can transform the request or response (header or content) or intercept the request **before** it reaches the Servlet.
*   **Usage:** Authentication checks, Logging, Data compression, Encryption, input validation.
*   It functions like a "Chain of Responsibility."

**Code Snippet:**
```java
public class AuthFilter implements Filter {
    public void doFilter(ServletRequest request, ServletResponse response, FilterChain chain) 
            throws IOException, ServletException {
        
        System.out.println("Checking Authentication...");
        // If valid, pass to next resource/servlet
        chain.doFilter(request, response);
        System.out.println("Response Generated.");
    }
}
```

---

## 47. What is session management?

**Answer:**
HTTP is a **stateless** protocol (server forgets client after response). Session Management is a mechanism to maintain the state (conversational state) of a user across multiple requests.
**Techniques:**
1.  **Cookies:** Small text data stored on the client browser.
2.  **URL Rewriting:** Appending session ID to the URL (`url;jsessionid=...`).
3.  **Hidden Form Fields:** Storing data in hidden HTML inputs.
4.  **HttpSession API:** Server-side session object (most secure and common).

**Code Snippet:**
```java
// Using HttpSession
HttpSession session = request.getSession(); // Create or Get existing
session.setAttribute("username", "JohnDoe"); // Store data

// In another request
String user = (String) session.getAttribute("username"); // Retrieve data
```

---

## 48. What is JSP lifecycle?

**Answer:**
JSP (JavaServer Pages) pages are eventually compiled into Servlets.
**Lifecycle Phases:**
1.  **Translation:** JSP file (.jsp) is translated into a Servlet source file (.java).
2.  **Compilation:** .java is compiled into .class.
3.  **Loading & Initialization (`jspInit()`):** Servlet class loaded and instance created.
4.  **Execution (`_jspService()`):** Handles requests (generates HTML).
5.  **Destruction (`jspDestroy()`):** Cleanup.

**Code Snippet:**
```jsp
<%-- This JSP code --%>
<html>
<body>
    <% out.println("Hello World"); %>
</body>
</html>

<%-- Becomes a Servlet roughly like: --%>
// public void _jspService(request, response) {
//     out.write("<html><body>");
//     out.print("Hello World");
//     out.write("</body></html>");
// }
```

---

## 49. Difference between forward and redirect.

**Answer:**
Both are used to navigate to a new resource, but they work differently.

| Feature | `request.getRequestDispatcher().forward()` | `response.sendRedirect()` |
| :--- | :--- | :--- |
| **Location** | Server-side (Internal). | Client-side (External). |
| **URL Bar** | **Unchanged**. User doesn't know. | **Changes** to the new URL. |
| **Requests** | Single Request (1 Round trip). | Two Requests (2 Round trips). |
| **Speed** | Faster. | Slower. |
| **Scope** | Can share request attributes. | Cannot share request attributes (new request). |

**Code Snippet:**
```java
// Forward: Pass data internally to JSP
request.setAttribute("msg", "Hi");
request.getRequestDispatcher("welcome.jsp").forward(request, response);

// Redirect: Tell browser to go to Google
response.sendRedirect("https://www.google.com");
```

---

## 50. What is cookie vs session?

**Answer:**

| Feature | Cookie | Session (HttpSession) |
| :--- | :--- | :--- |
| **Storage Location** | Client-side (Browser). | Server-side (Memory/DB). |
| **Security** | Less Secure (Can be edited/stolen). | More Secure (Only ID stored on client). |
| **Capacity** | Limited (~4KB). | Limited by Server Memory. |
| **Expiration** | Can persist indefinitely if set. | Expires after timeout (default 30 mins) or logout. |
| **Usage** | Storing trivial data (preferences, session ID). | Storing sensitive user data (Login state, Cart). |

**Code Snippet:**
```java
// Cookie
Cookie c = new Cookie("color", "blue");
c.setMaxAge(3600); // 1 hour
response.addCookie(c);

// Session
HttpSession s = request.getSession();
s.setAttribute("color", "blue"); // Stored on server
```

---


---

## 51. What is RMI?

**Answer:**
RMI (Remote Method Invocation) is an API that provides a mechanism to create distributed applications in Java.
*   It allows an object running in one JVM (Client) to invoke methods on an object running in another JVM (Server), possibly on a different machine.
*   **Key Components:**
    1.  **Stub:** Client-side proxy.
    2.  **Skeleton:** Server-side proxy (deprecated in newer versions).
    3.  **RMI Registry:** A directory service where the server registers the object and the client looks it up.

**Code Snippet:**
```java
// Server Interface
public interface Hello extends Remote {
    String sayHello() throws RemoteException;
}

// Client Lookup
Registry registry = LocateRegistry.getRegistry("localhost");
Hello stub = (Hello) registry.lookup("Hello");
String result = stub.sayHello(); // Remote call
```

---

## 52. What is serialization?

**Answer:**
Serialization is the process of converting the **state of an object into a byte stream**.
*   **Purpose:** To save the state of an object (Persistence) or to send it over a network (RMI, JMS).
*   **Mechanism:** The class must implement the `java.io.Serializable` marker interface.
*   **Deserialization:** The reverse process of converting a byte stream back into an object.

**Code Snippet:**
```java
// Serialization
User user = new User(1, "Alice");
ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream("user.ser"));
out.writeObject(user);
out.close();

// Deserialization
ObjectInputStream in = new ObjectInputStream(new FileInputStream("user.ser"));
User u = (User) in.readObject();
```

---

## 53. What is transient keyword?

**Answer:**
The `transient` keyword is used in serialization.
*   If you define any data member as `transient`, it will **not be serialized**.
*   During deserialization, the transient variable gets its **default value** (e.g., `0` for int, `null` for objects), losing its original value.
*   **Use Case:** Security (sensitive fields like passwords) or saving space (calculated fields).

**Code Snippet:**
```java
class User implements Serializable {
    String username;
    transient String password; // Will not be saved

    // Constructor...
}
// After deserialization: username="Alice", password=null
```

---

## 54. What is Externalizable?

**Answer:**
`Externalizable` is an interface that extends `Serializable` and allows you to customize the serialization process.
*   **Control:** Unlike `Serializable` (where JVM handles everything automatically), `Externalizable` gives you full control over what to read/write.
*   **Methods:** You must implement `writeExternal(ObjectOutput out)` and `readExternal(ObjectInput in)`.
*   **Performance:** It can be faster than `Serializable` because you only serialize what is needed.
*   **Requirement:** The class **must** have a public no-arg constructor.

**Code Snippet:**
```java
public class User implements Externalizable {
    String name;
    
    @Override
    public void writeExternal(ObjectOutput out) throws IOException {
        out.writeObject(name); // Manually write fields
    }

    @Override
    public void readExternal(ObjectInput in) throws IOException, ClassNotFoundException {
        name = (String) in.readObject(); // Manually read fields
    }
}
```

---

## 55. What is ClassLoader?

**Answer:**
A ClassLoader is a part of the JRE that dynamically loads Java classes into the JVM during runtime.
*   Java classes are not loaded all at once; they are loaded when required by the application.
*   The `ClassLoader` utilizes the "Delegation Hierarchy Principle" to load classes.

**Code Snippet:**
```java
public class ClassLoaderTest {
    public static void main(String[] args) {
        // App ClassLoader
        System.out.println(ClassLoaderTest.class.getClassLoader()); 
        
        // Bootstrap ClassLoader (Returns null as it's written in C/C++)
        System.out.println(String.class.getClassLoader()); 
    }
}
```

---

## 56. Types of class loaders.

**Answer:**
There are 3 built-in ClassLoaders in Java:
1.  **Bootstrap ClassLoader:** The root. Loads core Java libraries located in `/jre/lib` (e.g., `rt.jar`, `java.lang.*`). Written in native code.
2.  **Extension (Platform) ClassLoader:** Loads extensions from `/jre/lib/ext` directory.
3.  **Application (System) ClassLoader:** Loads user-defined classes from the **Classpath** (environment variable or `-cp` flag).

**Hierarchy:** App -> delegates to Ext -> delegates to Bootstrap.

---

## 57. What is SPI?

**Answer:**
SPI (Service Provider Interface) is a mechanism for loose coupling and extensibility. It allows a service (interface) to have multiple implementations (providers) that can be discovered and loaded at runtime.
*   **Components:** Service Interface, Service Provider, `ServiceLoader` class.
*   **Use Case:** JDBC Drivers (DriverManager uses SPI to find drivers), SLF4J (finding logging implementation).

**Code Snippet:**
```java
// 1. Define Service
public interface PaymentGateway { void pay(); }

// 2. Client uses ServiceLoader to find implementations
ServiceLoader<PaymentGateway> loader = ServiceLoader.load(PaymentGateway.class);
for (PaymentGateway pg : loader) {
    pg.pay();
}
```

---

## 58. What is annotation processing?

**Answer:**
Annotation Processing is a compile-time tool that scans and processes annotations (`@Annotation`) in your source code.
*   **Processor:** A plugin to `javac` that can inspect code and generate new source files (Java, XML, etc.).
*   It **cannot verify** or modify existing methods/code, strictly generates **new** files.
*   **Use Case:** Lombok (generates getters/setters), Dagger (generates dependency injection code), JPA (metamodel generation).

**Code Snippet:**
```java
@SupportedAnnotationTypes("com.example.AutoLog")
public class LogProcessor extends AbstractProcessor {
    @Override
    public boolean process(Set<? extends TypeElement> annotations, RoundEnvironment roundEnv) {
        // Scan for @AutoLog and generate logging code...
        return true;
    }
}
```

---

## 59. What is dynamic proxy?

**Answer:**
Dynamic Proxy allows you to create an implementation of an interface **at runtime**, without writing a concrete class.
*   You provide an `InvocationHandler`. When a method is called on the proxy instance, it is redirected to the `invoke()` method of your handler.
*   It is the backbone of **AOP (Aspect Oriented Programming)** (e.g., Spring Transaction Management).

**Code Snippet:**
```java
interface Service { void execute(); }

Service proxy = (Service) Proxy.newProxyInstance(
    Service.class.getClassLoader(),
    new Class[]{Service.class},
    (proxyObj, method, argsList) -> { // InvocationHandler
        System.out.println("Before method");
        return null; 
    }
);

proxy.execute(); // Prints "Before method"
```

---

## 60. What is Bytecode?

**Answer:**
Bytecode is the instruction set for the Java Virtual Machine (JVM).
*   When you compile a Java file (`javac Test.java`), it produces a `.class` class file containing bytecode.
*   It is **platform-independent**. The same bytecode can run on any OS that has a JVM.
*   The JVM (Interpreter/JIT Compiler) translates this bytecode into machine-native code (binary) for execution.

**Code Snippet:**
```bash
# Compile to Bytecode
javac HelloWorld.java 

# View Bytecode (Human readable)
javap -c HelloWorld.class

# Output snippet:
# 0: getstatic     #2 // Field java/lang/System.out:Ljava/io/PrintStream;
# 3: ldc           #3 // String Hello
# 5: invokevirtual #4 // Method java/io/PrintStream.println:(Ljava/lang/String;)V
```
---

## 61. What is Java Agent?

**Answer:**
A Java Agent is a specialized JVM component that allows you to instrument programs running on the JVM.
*   It utilizes the **Instrumentation API** (`java.lang.instrument`).
*   **Purpose:** To modify bytecode at runtime (e.g., adding logging, performance monitoring, security checks) without changing the original source code.
*   **Execution:** Java Agents run **before** the `main` method of the application (via `premain` method).
*   **Usage:** APM tools (New Relic, AppDynamics), Profilers.

**Code Snippet:**
```java
// Agent Class
public class MyAgent {
    public static void premain(String agentArgs, Instrumentation inst) {
        System.out.println("Java Agent Running...");
        // inst.addTransformer(...) to modify bytecode
    }
}
// Run: java -javaagent:myagent.jar -jar myapp.jar
```

---

## 62. What is NIO?

**Answer:**
NIO (New IO, or Non-blocking IO) is a collection of Java APIs (from Java 1.4) that offer an alternative to standard IO.
*   **Key Components:**
    1.  **Buffers:** Containers for data (e.g., `ByteBuffer`). Data is read into a buffer and written from a buffer.
    2.  **Channels:** Open connections to I/O devices (Files, Sockets). They support non-blocking reads/writes.
    3.  **Selectors:** Allow a single thread to monitor multiple channels for events (Connect, Accept, Read, Write).

**Code Snippet:**
```java
RandomAccessFile file = new RandomAccessFile("data.txt", "r");
FileChannel channel = file.getChannel();
ByteBuffer buffer = ByteBuffer.allocate(48);

int bytesRead = channel.read(buffer); // Read into buffer
```

---

## 63. What is Blocking vs Non-blocking IO?

**Answer:**
*   **Blocking IO (Old IO - `java.io`):** When a thread invokes a read() or write(), it **blocks** (waits) until the data is fully read or written. The thread sits idle during this time. Good for simple apps, bad for scalability (requires one thread per connection).
*   **Non-blocking IO (NIO - `java.nio`):** A thread requests a read/write. If data is ready, it proceeds. If not, the thread **returns immediately** (doesn't wait/block) and can do other work. Ideal for handling thousands of concurrent connections (e.g., Chat servers).

**Code Snippet:**
```java
// Blocking (ServerSocket)
Socket socket = serverSocket.accept(); // Blocks until client connects

// Non-blocking (ServerSocketChannel)
channel.configureBlocking(false);
SocketChannel sc = channel.accept(); 
if (sc != null) { 
    // Connected 
} else { 
    // Not connected yet, continue doing other work 
}
```

---

## 64. What is memory-mapped file?

**Answer:**
A Memory-Mapped File is a feature of Java NIO (`FileChannel.map`) that maps a region of a file directly into the **virtual memory** of the process.
*   **Speed:** It is incredibly fast for large files because the OS handles the actual reading/writing (paging) directly between disk and memory, bypassing the JVM's heap and IO buffers.
*   **Risk:** If the program crashes, the OS eventually syncs data, but explicit `force()` ensures safety.
*   **Use Case:** High-performance DBs, large data processing (Kafka uses this).

**Code Snippet:**
```java
FileChannel channel = FileChannel.open(path, StandardOpenOption.READ, StandardOpenOption.WRITE);
// Map 10 MB file into memory
MappedByteBuffer mbb = channel.map(FileChannel.MapMode.READ_WRITE, 0, 1024 * 1024 * 10);

mbb.put(0, (byte) 97); // Write byte directly to memory/file
```

---

## 65. What is ForkJoin framework?

**Answer:**
The Fork/Join Framework (Java 7) is designed to simplify parallel programming for tasks that can be broken down recursively (Divide and Conquer).
*   **Work-Stealing Algorithm:** Idle threads "steal" tasks from the back of the queue of busy threads, ensuring all CPU cores are utilized efficiently.
*   **Core Classes:** `ForkJoinPool` (Executor), `RecursiveTask` (Task with result), `RecursiveAction` (Task without result).
*   It is the underlying engine for **Java 8 Parallel Streams**.

**Code Snippet:**
```java
class SumTask extends RecursiveTask<Long> {
    // ... splitting logic ...
    @Override
    protected Long compute() {
        if (workload < THRESHOLD) {
            return computeDirectly();
        } else {
            SumTask left = new SumTask(...);
            SumTask right = new SumTask(...);
            left.fork(); // Async execution
            return right.compute() + left.join(); // Wait and Combine
        }
    }
}
```

---

## 66. What is CompletableFuture chaining?

**Answer:**
`CompletableFuture` allows chaining multiple asynchronous steps, where the result of one step is passed to the next.
*   **`thenApply`:** Transform the result (Map). Returns `CompletableFuture<U>`.
*   **`thenCompose`:** Chain another asynchronous operation (FlatMap). Returns `CompletableFuture<U>`.
*   **`thenAccept`:** Consume the result (void return).

**Code Snippet:**
```java
CompletableFuture.supplyAsync(() -> getUser(1)) // Step 1: Get User
    .thenCompose(user -> getOrder(user.id))    // Step 2: Get Order (Async)
    .thenApply(order -> order.totalPrice)      // Step 3: Extract Price
    .thenAccept(price -> System.out.println("Total: " + price)); // Step 4: Print
```

---

## 67. What is reactive programming in Java?

**Answer:**
Reactive Programming is a paradigm focused on **asynchronous data streams** and the propagation of changes.
*   **Core Concept:** Non-blocking, Event-driven, Backpressure (Subscriber tells Publisher how much data it can handle).
*   **Libraries:** **Project Reactor** (Spring WebFlux), **RxJava**.
*   **Java 9 Flow API:** Standardized the interfaces (`Publisher`, `Subscriber`, `Subscription`, `Processor`) but didn't provide a full implementation.

**Code Snippet:**
```java
// Project Reactor Example
Flux.just("Red", "Green", "Blue")
    .map(String::toUpperCase)
    .subscribe(System.out::println); // Output: RED, GREEN, BLUE
```

---

## 68. What is WebSocket?

**Answer:**
WebSocket is a communication protocol that provides full-duplex (two-way) communication channels over a single TCP connection.
*   **Difference from HTTP:** HTTP is request-response (Client asks, Server gives). WebSocket allows the Server to **push** data to the Client anytime.
*   **Handshake:** Starts as an HTTP request with an `Upgrade` header, then switches to WebSocket protocol.
*   **Java Support:** `javax.websocket` (Reference Implementation: Tyrus), Spring WebSocket.

**Code Snippet:**
```java
// Server Endpoint
@ServerEndpoint("/chat")
public class ChatServer {
    @OnMessage
    public void onMessage(String message, Session session) throws IOException {
        System.out.println("Received: " + message);
        session.getBasicRemote().sendText("Echo: " + message);
    }
}
```

---

## 69. What is JMX?

**Answer:**
JMX (Java Management Extensions) is a technology for monitoring and managing Java applications, system objects, and devices.
*   **MBeans (Managed Beans):** Java objects that represent resources (memory, garbage collector, custom app stats) that you want to manage.
*   **JMX Agent:** Managing agent (MBeanServer) that exposes these MBeans.
*   **Client:** Tools like **JConsole** or **VisualVM** connect to the JMX Agent to view stats or invoke operations (e.g., clear cache, change log level runtime).

**Code Snippet:**
```java
// MBean Interface
public interface SystemConfigMBean {
    void setLogLevel(String level);
    String getLogLevel();
}

// Managed Resource
public class SystemConfig implements SystemConfigMBean { 
    // implementation 
}

// Registration
MBeanServer mbs = ManagementFactory.getPlatformMBeanServer();
mbs.registerMBean(new SystemConfig(), new ObjectName("com.example:type=SystemConfig"));
```

---

## 70. What is Java Module System?

**Answer:**
Introduced in **Java 9** (Project Jigsaw), the Java Module System allows grouping packages and resources into a **Module**.
*   **Goals:** Strong encapsulation (hide internal packages), explicit dependencies, smaller runtime images (jlink).
*   **`module-info.java`:** The descriptor file placed at the root of the module.
*   **Keywords:**
    *   `exports com.my.package`: Makes package public to other modules.
    *   `requires java.sql`: Declares dependency on another module.

**Code Snippet:**
```java
// module-info.java
module com.my.app {
    requires java.sql;       // Depends on SQL module
    exports com.my.service;  // Exposes service package
    // com.my.util package is HIDDEN by default (Encapsulation)
}
```

---

---

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

---

## 96. What is thread lifecycle?

**Answer:**
A thread in Java goes through the following states (Lifecycle):
1.  **New:** Created but not yet started (`new Thread()`).
2.  **Runnable:** Ready to run. Waiting for CPU time (`thread.start()`).
3.  **Running:** Typically executing the `run()` method.
4.  **Blocked/Waiting:** Waiting for a resource (lock, I/O) or another thread (`wait()`, `join()`).
5.  **Terminated (Dead):** Finished execution or crashed.

**Code Snippet:**
```java
Thread t = new Thread(() -> {});
System.out.println(t.getState()); // NEW
t.start();
System.out.println(t.getState()); // RUNNABLE
```

---

## 97. Runnable vs Callable.

**Answer:**
| Feature | Runnable | Callable |
| :--- | :--- | :--- |
| **Return Type** | `void`. Cannot return a result. | `V`. Returns a result (Generic). |
| **Exception** | Cannot throw checked exceptions. | Can throw `Exception`. |
| **Package** | `java.lang` | `java.util.concurrent` |
| **Method** | `run()` | `call()` |
| **Usage** | Threads, ExecutorService (`execute()`). | ExecutorService (`submit()`). |

**Code Snippet:**
```java
// Runnable
Runnable r = () -> System.out.println("Running");

// Callable
Callable<Integer> c = () -> { return 42; };

ExecutorService exec = Executors.newFixedThreadPool(1);
exec.execute(r);
Future<Integer> future = exec.submit(c);
```

---

## 98. What is ExecutorService?

**Answer:**
`ExecutorService` is a higher-level replacement for working directly with `Thread`.
*   **Purpose:** It manages a pool of threads and assigns tasks (Runnable/Callable) to them.
*   **Benefits:**
    *   **Thread Reusability:** Avoids overhead of creating new threads for every task.
    *   **Task Scheduling:** Supports delayed and periodic execution (`ScheduledExecutorService`).
    *   **Lifecycle Management:** Provides methods to shut down the pool gracefully (`shutdown()`, `shutdownNow()`).

**Code Snippet:**
```java
ExecutorService es = Executors.newFixedThreadPool(2);
es.submit(() -> System.out.println("Task 1"));
es.submit(() -> System.out.println("Task 2"));
es.shutdown();
```

---

## 99. What is ThreadPool?

**Answer:**
A **Thread Pool** is a collection of pre-initialized threads standing by, ready to execute tasks.
*   **Mechanism:** Instead of creating a new thread for every request (which is expensive in terms of memory and CPU), tasks are submitted to a queue. The pool's threads consume tasks from this queue.
*   **Advantages:**
    *   Control over the number of active threads (prevents resource exhaustion).
    *   Faster response time (threads are already created).

---

## 100. Types of thread pools.

**Answer:**
The `Executors` factory class provides common thread pool configurations:
1.  **FixedThreadPool(n):** Fixed number of threads. Reuses them. Good for steady load.
2.  **CachedThreadPool:** Creates new threads as needed, but reuses idle ones. Threads terminate if idle for 60s. Good for many short-lived tasks.
3.  **SingleThreadExecutor:** Only one thread. Executes tasks sequentially. Good for ordering constraints.
4.  **ScheduledThreadPool:** Supports delayed and periodic execution.
5.  **WorkStealingPool (Java 8):** Creates a pool that uses all available processors (ForkJoinPool).

**Code Snippet:**
```java
ExecutorService fixed = Executors.newFixedThreadPool(5);
ExecutorService cached = Executors.newCachedThreadPool();
ExecutorService single = Executors.newSingleThreadExecutor();
```

---


## 101. What is Future?

**Answer:**
`Future` represents the **result of an asynchronous computation**.
*   **Purpose:** When you submit a task to an `ExecutorService`, it returns a `Future` object immediately. You can use this object to:
    1.  Check if the task is complete (`isDone()`).
    2.  Wait for the result (`get()` - blocks until ready).
    3.  Cancel the task (`cancel()`).
*   **Limitation:** The `get()` method is blocking. You cannot explicitly complete it or chain multiple futures (solved by `CompletableFuture` in Java 8).

**Code Snippet:**
```java
ExecutorService es = Executors.newFixedThreadPool(1);
Future<Integer> future = es.submit(() -> {
    Thread.sleep(1000);
    return 10;
});

// Do other work...
Integer result = future.get(); // Blocks for 1 sec
```

---

## 102. What is synchronization?

**Answer:**
Synchronization is a mechanism to control access to shared resources by multiple threads to prevent **Race Conditions** and ensuring **Thread Safety**.
*   **Monitor Lock:** Java uses an internal entity called a monitor (or lock) for synchronization.
*   **Keywords:**
    *   `synchronized` method: Locks the instance (this) or class (Class object for static methods).
    *   `synchronized` block: Locks a specific object. Preferred for smaller scope (better performance).

**Code Snippet:**
```java
class Counter {
    private int count = 0;
    
    // Only one thread can execute this at a time
    public synchronized void increment() {
        count++;
    }
}
```

---

## 103. What is intrinsic lock?

**Answer:**
Every object in Java has an **Intrinsic Lock** (or Monitor Lock) associated with it.
*   When a thread enters a `synchronized` method or block, it acquires the intrinsic lock of that object.
*   No other thread can acquire the same lock until the first thread releases it (exits the method/block).
*   It ensures **Mutual Exclusion** and **Visibility** of changes.

---

## 104. What is ReentrantLock?

**Answer:**
`ReentrantLock` (from `java.util.concurrent.locks`) is an advanced alternative to the `synchronized` keyword.
*   **Features:**
    *   **Fairness:** Can favor the longest-waiting thread (`new ReentrantLock(true)`).
    *   **TryLock:** Attempt to acquire lock without blocking (`tryLock()`).
    *   **Interruptible:** Can be interrupted while waiting for lock (`lockInterruptibly()`).
    *   **Explicit:** Must manually `lock()` and `unlock()` in a `finally` block.

**Code Snippet:**
```java
Lock lock = new ReentrantLock();
try {
    lock.lock();
    // Critical Section
} finally {
    lock.unlock(); // Always release in finally
}
```

---

## 105. What is ReadWriteLock?

**Answer:**
`ReadWriteLock` maintains a pair of locks: one for **Reading** and one for **Writing**.
*   **Rules:**
    *   **Multiple Readers:** Many threads can hold the Read Lock simultaneously (as long as no thread holds the Write Lock).
    *   **Single Writer:** Only one thread can hold the Write Lock (exclusive).
*   **Benefit:** Improves performance when reads are much more frequent than writes.

**Code Snippet:**
```java
ReadWriteLock rwLock = new ReentrantReadWriteLock();

// Reader
rwLock.readLock().lock();
try { /* Read data */ } finally { rwLock.readLock().unlock(); }

// Writer
rwLock.writeLock().lock();
try { /* Write data */ } finally { rwLock.writeLock().unlock(); }
```

---

## 106. What is volatile?

**Answer:**
The `volatile` keyword guarantees **Visibility** of changes to variables across threads.
*   **Problem:** Threads perform caching (CPU cache). A change by Thread A might not be immediately visible to Thread B.
*   **Solution:** Reads/Writes to a `volatile` variable bypass the cache and go directly to **Main Memory**.
*   **Constraint:** It does **NOT** guarantee Atomicity (e.g., `count++` is not safe with just `volatile`). Use it for flags or status variables.

**Code Snippet:**
```java
private volatile boolean running = true;

public void stop() { running = false; } // Thread safe visibility

public void run() {
    while (running) { // Will see the change immediately
        // Work
    }
}
```

---

## 107. What is happens-before relationship?

**Answer:**
**Happens-Before** is a concept in the Java Memory Model (JMM) that defines the partial ordering of actions.
*   If Action A *happens-before* Action B, then the JMM guarantees that the results of A are **visible** to B.
*   **Rules:**
    1.  **Program Order:** Each action in a thread happens-before later actions in that thread.
    2.  **Monitor Lock:** Unlocking a monitor happens-before locking same monitor.
    3.  **Volatile:** Write to `volatile` happens-before subsequent read of same volatile.
    4.  **Thread Start:** `thread.start()` happens-before any action in the started thread.

---

## 108. What is atomic variable?

**Answer:**
Atomic Variables (in `java.util.concurrent.atomic`) allow thread-safe, lock-free operations on single variables.
*   **Mechanism:** They use low-level CPU instructions like **CAS (Compare-And-Swap)** instead of locks.
*   **Classes:** `AtomicInteger`, `AtomicLong`, `AtomicBoolean`, `AtomicReference`.
*   **Performance:** Generally faster than `synchronized` for simple counters/flags.

**Code Snippet:**
```java
AtomicInteger count = new AtomicInteger(0);

// Thread-safe increment
int newValue = count.incrementAndGet(); // Returns updated value
```

---

## 109. What is CAS?

**Answer:**
**CAS (Compare-And-Swap)** is an atomic instruction supported by modern CPUs used to achieve synchronization without locks (Optimistic Concurrency).
*   **Logic:** It takes 3 operands:
    1.  **Memory Location (V)**
    2.  **Expected Old Value (A)**
    3.  **New Value (B)**
*   **Operation:** "If V == A, update V to B. Otherwise, do nothing."
*   **Loop:** Java loops this operation (retry) until it succeeds.

**Code Snippet:**
```java
// Conceptual implementation of increment()
do {
    int oldVal = get();
    int newVal = oldVal + 1;
} while (!compareAndSet(oldVal, newVal));
```

---

## 110. What is Deadlock?

**Answer:**
Deadlock is a situation where two or more threads are blocked forever, waiting for each other to release a lock.
*   **Scenario:** Thread A holds Lock 1 and waits for Lock 2. Thread B holds Lock 2 and waits for Lock 1.
*   **Prevention:**
    1.  **Lock Ordering:** Always acquire locks in a consistent fixed order (e.g., Lock 1 then Lock 2).
    2.  **Timeouts:** Use `tryLock(timeout)` to avoid waiting indefinitely.
    3.  **Global Lock:** Use a single coarse-grained lock (reduces concurrency).

**Code Snippet:**
```java
// Deadlock Example
Thread 1: synchronized(A) { synchronized(B) { ... } }
Thread 2: synchronized(B) { synchronized(A) { ... } } 
// If both start at same time -> Deadlock.

// Fix (Consistent Order)
Thread 2: synchronized(A) { synchronized(B) { ... } }
```

---

## 111. How to avoid deadlock?

**Answer:**
Deadlock can be avoided by breaking one of the four necessary conditions (Mutual Exclusion, Hold and Wait, No Preemption, Circular Wait).
**Strategies:**
1.  **Avoid Circular Wait:** Acquire locks in a consistent, **fixed global order**. If Thread A and Thread B need locks X and Y, both must acquire X first, then Y.
2.  **Avoid Hold and Wait:** Try to acquire all resources at once or release current locks before waiting for new ones.
3.  **Timeout:** Use `Lock.tryLock(long time, TimeUnit unit)` instead of blocking indefinitely. If the lock isn't acquired, back off and retry.
4.  **Deadlock Detection:** Use tools (JConsole, VisualVM) to detect deadlocks in running applications.

---

## 112. What is starvation?

**Answer:**
**Starvation** describes a situation where a thread is unable to gain regular access to shared resources and is unable to make progress.
*   **Causes:**
    *   **Priority:** Higher priority threads constantly preempt lower priority threads.
    *   **Greedy Threads:** A thread holds a lock for a very long time (e.g., infinite loop in `synchronized` block).
*   **Difference from Deadlock:** In deadlock, *threads are blocked forever waiting for each other*. In starvation, threads are *ready to run but never get selected by the scheduler*.
*   **Solution:** Use **Fair Locks** (`new ReentrantLock(true)`) which grant access in FIFO order.

---

## 113. What is livelock?

**Answer:**
**Livelock** is a situation where two or more threads act in response to each other to resolve a deadlock, but typically end up in a loop of state changes without making actual progress.
*   **Example:** Two people meeting in a narrow corridor. Person A moves left to let B pass, B moves right to let A pass. They block each other. Then A moves right, B moves left. They are *active* (moving), but stuck.
*   **Solution:** Introduce **Randomness** in the retry mechanism (e.g., Ethernet backoff algorithm).

---

## 114. What is ThreadLocal?

**Answer:**
`ThreadLocal` is a class that provides **Thread-Local Variables**.
*   These variables differ from normal variables in that each thread that accesses one (via `get` or `set` method) has its own, independently initialized copy of the variable.
*   **Isolation:** Changes made by one thread are **invisible** to other threads.
*   **Use Case:** Storing User ID, Transaction ID, or Database Connection for the duration of a request without passing it as a parameter to every method.
*   **Warning:** Must be cleaned up (`remove()`) to avoid **Memory Leaks**, especially in thread pools (e.g., Tomcat).

**Code Snippet:**
```java
ThreadLocal<Integer> threadLocalValue = ThreadLocal.withInitial(() -> 1);

new Thread(() -> {
    threadLocalValue.set(100);
    System.out.println(threadLocalValue.get()); // 100
}).start();

new Thread(() -> {
    System.out.println(threadLocalValue.get()); // 1 (Default)
}).start();
```

---

## 115. What is CyclicBarrier?

**Answer:**
`CyclicBarrier` is a synchronization aid that allows a set of threads to wait for each other to reach a common barrier point.
*   **Usage:** Breaking a large task into subtasks. All threads must finish their subtask before *any* thread proceeds to the next step.
*   **Reusable:** Unlike CountDownLatch, CyclicBarrier can be reset and reused after the barrier is broken.
*   **Action:** Can run a "barrier action" (Runnable) once all threads reach the barrier.

**Code Snippet:**
```java
CyclicBarrier barrier = new CyclicBarrier(3, () -> System.out.println("Barrier Broken!"));

Runnable r = () -> {
    System.out.println("Wait...");
    try { barrier.await(); } catch (Exception e) {}
    System.out.println("Proceed");
};
// Start 3 threads running 'r'
```

---

## 116. What is CountDownLatch?

**Answer:**
`CountDownLatch` is a synchronization aid that allows one or more threads to wait until a set of operations being performed in other threads completes.
*   **Mechanism:** Initialized with a `count`. Threads call `countDown()` to decrement. Waiting threads block on `await()` until count reaches zero.
*   **One-Shot:** Once the count reaches zero, it cannot be reset.
*   **Use Case:** Ensuring a server works only after all services (DB, Cache) are initialized.

**Code Snippet:**
```java
CountDownLatch latch = new CountDownLatch(3);

// Service Threads
latch.countDown(); 
latch.countDown();
latch.countDown();

// Main Server Thread
latch.await(); // Blocks until count is 0
System.out.println("All services up!");
```

---

## 117. What is Semaphore?

**Answer:**
`Semaphore` maintains a set of **permits**.
*   **Purpose:** To restrict the number of threads that can access a shared resource (Throttling/Rate Limiting).
*   **Methods:**
    *   `acquire()`: Takes a permit. Blocks if none available.
    *   `release()`: Returns a permit.
*   **Binary Semaphore:** A semaphore with 1 permit acts like a Lock (Mutex).

**Code Snippet:**
```java
Semaphore sem = new Semaphore(3); // Only 3 concurrent accesses

try {
    sem.acquire();
    // Access Resource
} finally {
    sem.release();
}
```

---

## 118. What is Phaser?

**Answer:**
`Phaser` (Java 7) is a reusable synchronization barrier, similar to CyclicBarrier and CountDownLatch, but more **flexible**.
*   **Dynamic:** The number of registered parties can change over time (register/deregister workers).
*   **Phasing:** Supports multiple phases of execution.
*   **Use Case:** Parallel algorithms where the number of tasks varies per phase.

---

## 119. What is parallel stream?

**Answer:**
A `parallelStream()` splits the stream into multiple chunks and processes them concurrently using the **ForkJoinPool.commonPool()**.
*   **Syntax:** `collection.parallelStream()` or `stream.parallel()`.
*   **Benefit:** Faster processing for large datasets on multi-core CPUs.
*   **Warning:**
    *   Order is not guaranteed (use `forEachOrdered` if needed).
    *   Shared mutable state must be synchronized.
    *   Can affect other tasks using the common pool.

**Code Snippet:**
```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);
list.parallelStream()
    .map(n -> n * 2)
    .forEach(System.out::println); // Order is random
```

---

## 120. What is ForkJoinPool?

**Answer:**
`ForkJoinPool` is an `ExecutorService` optimized for **recursive** divide-and-conquer tasks.
*   **Work-Stealing:** Threads that run out of tasks "steal" work from other busy threads' queues (Deques). This keeps all CPU cores busy.
*   **Common Pool:** Java 8 introduces a static common pool (`ForkJoinPool.commonPool()`) used by Parallel Streams and CompletableFuture by default.

**Code Snippet:**
```java
ForkJoinPool pool = new ForkJoinPool();
pool.invoke(new RecursiveTask<Integer>() { ... });
```

---

## 121. Explain JVM architecture in detail.

**Answer:**
The **JVM (Java Virtual Machine)** consists of three main subsystems:
1.  **Class Loader Subsystem:** Loads, links, and initializes class files (`.class`).
2.  **Runtime Data Areas (Memory):**
    *   **Method Area:** Class structures (metadata).
    *   **Heap:** Objects.
    *   **Stack:** Local variables, method calls.
    *   **PC Register:** Current instruction address.
    *   **Native Method Stack:** For native methods.
3.  **Execution Engine:**
    *   **Interpreter:** Reads bytecode line by line and executes.
    *   **JIT Compiler:** Compiles hot code to native code for performance.
    *   **Garbage Collector:** Manages memory.
4.  **JNI (Java Native Interface):** Interacts with Native Method Libraries (C/C++).

---

## 122. What are JVM memory areas?

**Answer:**
JVM memory is divided into 5 parts:
1.  **Heap Area:** Stores objects and arrays. Shared among all threads.
2.  **Java Stack Area:** Stores frames for method execution (local variables, operand stack). Per-thread.
3.  **Method Area (Metaspace):** Stores class structures (constants, fields, method data). Shared.
4.  **PC Register:** Holds the address of the current instruction being executed. Per-thread.
5.  **Native Method Stack:** Stores frames for native methods. Per-thread.

---

## 123. What is Heap vs Stack?

**Answer:**
| Feature | Heap (Memory) | Stack (Memory) |
| :--- | :--- | :--- |
| **Storage** | Objects and Instance Variables. | Local Variables and Method Calls. |
| **Visibility** | **Global** (Shared by all threads). | **Thread-Local** (Private to a thread). |
| **Size** | Large. Managed by Xms, Xmx. | Small. Managed by Xss. |
| **Cleanup** | Garbage Collector (GC). | Automatically when block/method exits (LIFO). |
| **Access** | Slower (Reference access). | Faster. |

**Code Snippet:**
```java
public void method() {
    int x = 10; // Stored in STACK
    Person p = new Person(); // Reference 'p' in STACK, Object in HEAP
}
```

---

## 124. What is Metaspace?

**Answer:**
**Metaspace** is a native memory region that replaced **PermGen** (Permanent Generation) in Java 8.
*   **Purpose:** Stores **Class Metadata** (Structure of classes, methods, fields).
*   **Location:** **Native Heap** (OS Memory), not the JVM Heap.
*   **Advantage:** Unlike PermGen (which had a fixed size leading to `OutOfMemoryError: PermGen space`), Metaspace auto-resizes based on OS memory availability.
*   **Tuning:** `-XX:MaxMetaspaceSize`.

---

## 125. What is Runtime Constant Pool?

**Answer:**
The **Runtime Constant Pool** is a per-class or per-interface runtime representation of the `constant_pool` table in a class file.
*   **Content:** Contains compile-time known numeric literals, method and field references.
*   **Location:** Stored within the **Method Area**.
*   **Resolution:** Symbolic references in the pool are resolved to direct references during runtime (Dynamic Linking).

---

## 126. What is Program Counter Register?

**Answer:**
The **PC (Program Counter) Register** is a small memory area.
*   **Per-Thread:** Each thread has its own PC Register.
*   **Function:** It holds the address of the **current instruction** being executed by the thread.
*   **Native Methods:** If the thread executes a native method, the PC register is undefined.

---

## 127. What is Native Method Stack?

**Answer:**
The **Native Method Stack** is similar to the Java Stack but is used for **Native Methods** (code written in C/C++).
*   **Usage:** Used when the JVM invokes JNI (Java Native Interface) methods.
*   **Allocation:** Usually allocated in C-Stack (native memory).
*   **Error:** Can throw `StackOverflowError` if recursion is too deep.

---

## 128. What is Class Loader subsystem?

**Answer:**
The **Class Loader Subsystem** is responsible for locating, loading, and initializing Java classes from `.class` files.
It performs three major roles:
1.  **Loading:** Finding the binary representation of a class and creating a `Class` object.
2.  **Linking:**
    *   **Verification:** Checks bytecode validity.
    *   **Preparation:** Allocates memory for static variables (default values).
    *   **Resolution:** Replaces symbolic references with direct references.
3.  **Initialization:** Executes static blocks and static variable assignments.

---

## 129. What is parent delegation model?

**Answer:**
The **Parent Delegation Model** is the hierarchy used by ClassLoaders to load a class.
*   **Flow:** When a ClassLoader receives a request to load a class:
    1.  It checks if the class is already loaded.
    2.  If not, it **delegates** the request to its **Parent**.
    3.  This continues up to the **Bootstrap ClassLoader**.
    4.  If the parent cannot find the class, the child ClassLoader attempts to load it.
*   **Hierarchy:** `Bootstrap` -> `Platform (Ext)` -> `App (System)`.
*   **Goal:** Security (prevents replacing core Java classes like `java.lang.String`).

---

## 130. What happens when a class is loaded?

**Answer:**
When a class is first referenced (e.g., `new MyClass()` or `MyClass.staticVar`):
1.  **Loading:** The JVM reads the `.class` file into memory.
2.  **Linking:** Bytecode is verified. Static variables get default memory (e.g., `int=0`).
3.  **Initialization:** The `<clinit>` method executes:
    *   Static initializers run.
    *   Static variables are assigned their actual values.
    *   This happens **only once** per class.

**Code Snippet:**
```java
class Demo {
    static int x = 10;
    static {
        System.out.println("Class Initialized");
    }
}
// Usage: Demo.x; // Loads class, prints "Class Initialized"
```

---



---

## 131. What objects are eligible for GC?

**Answer:**
An object is eligible for Garbage Collection when it is **unreachable** from any **GC Root**.
*   **scenarios:**
    1.  **Nullifying references:** `obj = null;`
    2.  **Reassigning references:** `obj = new Object();`
    3.  **Object created inside a method:** Becomes eligible after method execution completes.
    4.  **Island of Isolation:** Two objects reference each other but are not referenced by any active part of the application.

**Code Snippet:**
```java
public void test() {
    Person p1 = new Person();
    Person p2 = new Person();
    p1.friend = p2;
    p2.friend = p1;
    
    p1 = null;
    p2 = null;
    // Both p1 and p2 are eligible for GC (Island of Isolation)
}
```

---

## 132. How does GC work internally?

**Answer:**
GC works based on the **Generational Hypothesis**: "Most objects die young."
*   **Memory Structure:** Heap is divided into **Young Generation** (Eden, Survivor S0, S1) and **Old Generation** (Tenured).
*   **Process:**
    1.  New objects are created in **Eden**.
    2.  When Eden fills up, **Minor GC** runs. Alive objects move to Survivor spaces.
    3.  Objects that survive multiple GC cycles (threshold age) assume to be long-lived and move to **Old Generation**.
    4.  When Old Gen fills up, **Major/Full GC** runs.

---

## 133. What are GC roots?

**Answer:**
**GC Roots** are objects that are accessible from outside the heap and serve as the starting point for the reachability analysis (Marking phase).
*   **Examples:**
    *   **Class:** Classes loaded by system class loader.
    *   **Stack Local:** Local variables and parameters in the stack of valid threads.
    *   **JNI Local/Global:** References held by native code.
    *   **Synchronization Monitor:** Objects used as a monitor for synchronization.

---

## 134. Minor GC vs Major GC vs Full GC.

**Answer:**
| Type | Region Cleaned | Trigger | Impact |
| :--- | :--- | :--- | :--- |
| **Minor GC** | **Young Generation** (Eden + Survivor). | When Eden space is full. | Very fast. efficient. Frequent. |
| **Major GC** | **Old Generation**. | When Old Gen is full. | Slower than Minor GC. Often triggers Stop-the-world. |
| **Full GC** | **Entire Heap** (Young + Old) + **Metaspace**. | System.gc(), Low Memory. | Very Slow. Heavy "Stop-the-world" pause. |

---

## 135. What are different GC algorithms?

**Answer:**
1.  **Mark-Sweep:** Marks reachable objects, then sweeps (deletes) unreachable ones. **Issue:** Memory Fragmentation.
2.  **Mark-Sweep-Compact:** Marks, Sweeps, then Compacts memory (moves objects together) to solve fragmentation. **Issue:** Higher pause time.
3.  **Copying:** Splits memory into two halves. Copies live objects to the other half. **Used in:** Young Generation (Survivor spaces).

---

## 136. What is Serial GC?

**Answer:**
**Serial GC** is the simplest collector designed for **single-threaded** environments.
*   **Threads:** Uses a single thread for GC (Stop-the-world).
*   **Usage:** Client-side apps, small heaps, single-core CPUs.
*   **Flag:** `-XX:+UseSerialGC`

---

## 137. What is Parallel GC?

**Answer:**
**Parallel GC** (Throughput Collector) is the default in Java 8.
*   **Threads:** Uses **multiple threads** for Young Generation GC (Minor GC) and Old Generation GC (Major GC).
*   **Goal:** Maximize **Throughput** (Total work done / Time).
*   **Usage:** Backend servers where high throughput is prioritized over latency.
*   **Flag:** `-XX:+UseParallelGC`

---

## 138. What is CMS GC?

**Answer:**
**CMS (Concurrent Mark Sweep)** is designed for **Low Latency**.
*   **Mechanism:** It performs most of the GC work (marking) **concurrently** with the application threads (no stop-the-world).
*   **Drawback:** CPU intensive, suffers from memory fragmentation (no compaction).
*   **Status:** Deprecated in Java 9, Removed in Java 14.
*   **Flag:** `-XX:+UseConcMarkSweepGC`

---

## 139. What is G1 GC?

**Answer:**
**G1 (Garbage First) GC** is the default collector in Java 9+.
*   **Structure:** Divides the heap into many small, equal-sized **regions** (instead of contiguous Young/Old generations).
*   **Mechanism:** It prioritizes cleaning regions with the most garbage (Garbage-First).
*   **Goal:** Predictable **Pause Times** (Soft real-time). It compacts memory on the go.
*   **Usage:** Large Heap sizes (>4GB).
*   **Flag:** `-XX:+UseG1GC`

---

## 140. What is ZGC / Shenandoah?

**Answer:**
**ZGC** (Z Garbage Collector) and **Shenandoah** are ultra-low latency collectors.
*   **Goal:** Pause times **< 10ms** (often < 1ms), regardless of heap size (Scalable to Terabytes).
*   **Mechanism:** Performs strictly nearly all work (marking, compaction, relocation) **concurrently**.
*   **Usage:** Time-sensitive applications requiring consistent responsiveness.
*   **Flag:** `-XX:+UseZGC`, `-XX:+UseShenandoahGC`

---

## 141. How to analyze heap dump?

**Answer:**
A **Heap Dump** is a snapshot of the Java memory (Heap) at a specific moment.
*   **Tools:** Eclipse Memory Analyzer (MAT), VisualVM, jhat.
*   **Analysis:**
    1.  **Dominator Tree:** Find largest objects retaining memory.
    2.  **Histogram:** Count of instances per class (e.g., millions of String objects?).
    3.  **Leak Suspects Report:** Automated report identifying potential leaks.
    4.  **Path to GC Roots:** Why is an object being kept alive?

---

## 142. What is memory leak in Java?

**Answer:**
A **Memory Leak** in Java occurs when objects are **no longer needed** by the application but are **still referenced** (often unintentionally), preventing the Garbage Collector from removing them.
*   **Unintentional References:** Static collections (HashMap, List), Unclosed Resources (Streams, Connections), Listener/Callback registration without deregistration.
*   **Result:** `OutOfMemoryError: Java heap space`.

---

## 143. How to detect memory leak?

**Answer:**
1.  **Monitor Heap Usage:** Check visuals in **JConsole** or **VisualVM**. A healthy app has a "sawtooth" pattern (memory rises, GC drops it). A leak shows memory consistently rising until the crash.
2.  **Verbose GC:** Enable GC logging (`-Xlog:gc*`) to see if full GCs are failing to reclaim memory.
3.  **Heap Dump Comparison:** Take two dumps (one at start, one later) and compare instance counts.

---

## 144. What is JVisualVM / JConsole?

**Answer:**
Both are monitoring tools provided with the JDK (up to JDK 8, VisualVM separate later).
*   **JConsole:** Uses JMX (Java Management Extensions) to monitor Memory, Threads, Classes, and MBeans. Good for quick, high-level checks.
*   **VisualVM (jvisualvm):** More powerful "All-in-One". It integrates profiling, thread dumps, heap dumps, and plugins. It provides a better visual interface for CPU and Memory profiling.

---

## 145. What is JProfiler?

**Answer:**
**JProfiler** is a popular, commercial, third-party Java Profiler (alternatives: YourKit, Java Flight Recorder).
*   **Features:** Deep analysis of CPU hotspots, Memory allocations, Database connections (JDBC/JPA/Hibernate), Threads, and Deadlocks.
*   **Advantage:** Much more detailed and user-friendly than free tools. Capable of remote profiling production servers with low overhead.

---

## 146. What is thread dump?

**Answer:**
A **Thread Dump** is a snapshot of the state of all threads in the JVM at a specific moment.
*   **Content:** Thread Name, ID, State (RUNNABLE, BLOCKED, WAITING, TIMED_WAITING), Stack Trace (method calls).
*   **Command:** `jstack <pid>`, `kill -3 <pid>` (Linux), or via VisualVM.

---

## 147. How to analyze thread dump?

**Answer:**
Analyze top-down looking for:
1.  **BLOCKED Threads:** Threads waiting to acquire a lock held by another thread.
2.  **Deadlock:** Two threads cyclically waiting for each other (Dump usually says "Found one Java-level deadlock").
3.  **High CPU:** Look for RUNNABLE threads executing complex code.
4.  **Tools:** `fastthread.io`, TDA (Thread Dump Analyzer), Samurai.

---

## 148. What causes high CPU usage in Java app?

**Answer:**
1.  **Infinite Loops:** `while(true)` without sleep.
2.  **Complex Algorithms:** O(n^2) or worse on large datasets.
3.  **GC Thrashing:** Frequent Full GCs because heap is too small (CPU spent on GC, not app logic).
4.  **Heavy Serialization/Deserialization.**
5.  **Context Switching:** Too many threads competing for CPU.

---

## 149. What is OutOfMemoryError types?

**Answer:**
`java.lang.OutOfMemoryError` has several messages:
1.  **Java heap space:** Heap is full. Solution: Increase `-Xmx` or fix leak.
2.  **GC Overhead limit exceeded:** GC is spending 98% of time reclaiming < 2% of heap. Solution: Check for leaks/inefficient code.
3.  **Metaspace:** Metadata area full (too many classes). Solution: Increase `-XX:MaxMetaspaceSize`.
4.  **Request size bytes for reason. Out of swap space?**: Native memory issue.
5.  **StackOverflowError:** Deep recursion (technically separate error, but related to memory/stack limit `-Xss`).

---

## 150. How to tune JVM parameters?

**Answer:**
Key JVM flags for tuning:
*   **Heap Size:** `-Xms<size>` (Initial), `-Xmx<size>` (Max). Best practice: Set them equal to avoid resizing overhead.
*   **Stack Size:** `-Xss<size>` (Per-thread stack size).
*   **Metaspace:** `-XX:MaxMetaspaceSize=<size>`.
*   **GC Logging:** `-Xlog:gc*` (Java 9+).
*   **Heap Dump:** `-XX:+HeapDumpOnOutOfMemoryError` (Essential for post-mortem analysis).
*   **GC Algorithm:** `-XX:+UseG1GC` (Recommended mostly).

---

## 151. What is JIT compiler?

**Answer:**
The **JIT (Just-In-Time) Compiler** improves performance by compiling bytecode into native machine code at **runtime**.
*   **Process:**
    1.  The JVM initially interprets the bytecode.
    2.  It monitors ("profiles") the code to find "Hot Spots" (frequently executed methods/loops).
    3.  The JIT compiler compiles these hot spots into optimized native code.
    4.  Subsequent calls execute the native code directly, bypassing the interpreter.

---

## 152. What is escape analysis?

**Answer:**
**Escape Analysis** is an optimization technique used by the JIT compiler to determine the scope of a new object.
*   **Scope:** If an object is created in a method and *never escapes* that method (e.g., not returned, not assigned to a static field), it is considered "local".
*   **Result (Stack Allocation):** The JIT may allocate this object on the **Stack** instead of the Heap. This reduces GC pressure significantly.
*   **Result (Scalar Replacement):** It might break the object into its primitive fields and store them in registers.

---

## 153. What is biased locking?

**Answer:**
**Biased Locking** is an optimization for synchronized blocks that are accessed by only **one thread** most of the time.
*   **Concept:** The JVM "biases" the lock towards the first thread that acquires it.
*   **Benefit:** Subsequent lock acquisitions by the *same* thread are extremely cheap (no atomic CAS operations).
*   **Revocation:** If another thread tries to acquire the lock, the bias is revoked, and it upgrades to a normal lightweight lock.
*   **Status:** Deprecated in Java 15 due to complexity and cost of revocation.

---

## 154. What is lock elision?

**Answer:**
**Lock Elision** (or Lock Coarsening) involves removing unnecessary synchronization.
*   **Elision:** If Escape Analysis proves a lock object is local to a thread and never shared, the JIT removes the `synchronized` block entirely (e.g., using `StringBuffer` inside a method).
*   **Coarsening:** If the JIT sees repeated lock/unlock on the same object (e.g., inside a loop), it merges them into a single larger lock block.

---

## 155. What is safepoint?

**Answer:**
A **Safepoint** is a point in execution where the state of the JVM is consistent and known, allowing the JVM to perform maintenance tasks.
*   **Tasks:** Garbage Collection, JIT Deoptimization, Thread Dump, Revoking Biased Locks.
*   **Mechanism:** All application threads are paused (suspended) at a safe point before the JVM operation begins.
*   **Location:** Method exit, Loop back-edge.

---

## 156. What is stop-the-world event?

**Answer:**
A **Stop-The-World (STW)** event is a pause where all application threads are suspended by the JVM.
*   **Reason:** Usually triggered by **Garbage Collection** (specifically Major/Full GC) or other Safepoint operations.
*   **Impact:** The application becomes unresponsive during this time. Minimizing STW pauses is a primary goal of Low-Latency GCs (ZGC, Shenandoah).

---

## 157. What is inline caching?

**Answer:**
**Inline Caching** is an optimization for **Dynamic Dispatch** (virtual method calls).
*   **Concept:** The JVM caches the result of a method lookup (target method address) at the call site.
*   **Morphic:** If the call site always invokes the same implementation (e.g., `list.add` is always `ArrayList.add`), the JIT "inlines" the call, replacing the lookup with a direct call or the method body itself.
*   **Polymorphic:** If it calls different implementations, it falls back to a slower lookup.

---

## 158. What is AOT compilation?

**Answer:**
**AOT (Ahead-Of-Time) Compilation** compiles Java classes to native code **before** the application starts (at build time).
*   **Pros:** faster startup time (no JIT warmup needed), lower memory footprint.
*   **Cons:** Less peak performance than JIT (JIT can optimize based on runtime data which AOT lacks).
*   **Tool:** `jaotc` (Experimental in JDK 9, Removed in JDK 17). GraalVM Native Image is the modern successor.

---

## 159. What is GraalVM?

**Answer:**
**GraalVM** is a high-performance JDK distribution designed to accelerate execution of applications written in Java and other languages.
*   **Key Feature (Native Image):** Compiles Java apps into standalone native binaries (AOT). Instant startup, low memory. Ideal for Microservices/Serverless.
*   **Polyglot:** Allows mixing languages (Java, JS, Python, R) in the same runtime.
*   **Graal Compiler:** A new JIT compiler written in Java (can be used in standard HotSpot via `-XX:+UseJVMCICompiler`).

---

## 160. What is Java Flight Recorder?

**Answer:**
**JFR (Java Flight Recorder)** is a profiling and event collection framework built into the JVM.
*   **Low Overhead:** Designed to run continuously in production (< 1% performance impact).
*   **Data:** Captures GC events, Method execution, I/O latency, Thread stalls, Exceptions, CPU usage.
*   **Analysis:** Recordings (`.jfr` files) are analyzed using **Java Mission Control (JMC)**.


---

## 161. How to improve startup time?

**Answer:**
1.  **Class Data Sharing (CDS):** Share loaded class metadata between JVM processes to reduce loading time.
2.  **AOT Compilation:** Use `GraalVM Native Image` for instant startup.
3.  **Lazy Loading:** Initialize beans/resources only when needed (e.g., Spring `@Lazy`).
4.  **Reduce Classpath Scanning:** Limit the packages scanned by frameworks like Spring.
5.  **Minimize Static Initializers:** Avoid heavy logic in `static {}` blocks.

---

## 162. How to reduce GC pause time?

**Answer:**
1.  **Choice of GC:** Use Low-Latency collectors like **ZGC** or **Shenandoah** (sub-millisecond pauses).
2.  **Heap Size:** A very large heap might increase pause time in older GCs (G1 handles this better).
3.  **Reduce Allocation Rate:** Create fewer temporary objects (Reuse buffers, Flyweight pattern). Less garbage = Less frequent GC.
4.  **Object Pooling:** (Use with caution) Reuse expensive objects (e.g., DB Connections) to avoid churn.

---

## 163. How to optimize large collections?

**Answer:**
1.  **Sizing:** Always set **initial capacity** to avoid resizing overhead (array copying). `new ArrayList<>(10000)`.
2.  **Primitive Collections:** Use library like **Eclipse Collections** or **FastUtil** to avoid Auto-boxing overhead (saving generic `Integer` wrappers).
3.  **Off-Heap:** Store massive data in **DirectByteBuffer** or memory-mapped files to avoid GC overhead entirely.

---

## 164. When to use primitive collections?

**Answer:**
Use **Primitive Collections** (e.g., `IntList` instead of `List<Integer>`) when dealing with **large datasets** (millions of items).
*   **Memory:** `int` takes 4 bytes. `Integer` object takes ~24 bytes (Header + int + Ref). A `List<Integer>` has huge overhead.
*   **Performance:** Avoids CPU cost of **Autoboxing/Unboxing**.
*   **Libraries:** **Eclipse Collections**, **Trove**, **FastUtil**.

---

## 165. How to design memory-efficient objects?

**Answer:**
1.  **Object Header:** Remember every object in Java has a header (~12-16 bytes). Small objects have high overhead.
2.  **Primitives:** Use primitives (`int`, `long`) over wrappers (`Integer`, `Long`).
3.  **Arrays vs Objects:** Arrays have lower overhead than `ArrayList`.
4.  **Flyweight Pattern:** Share common instances (like `Boolean.TRUE`, `Integer.valueOf(1)`).

---

## 166. How to reduce object creation?

**Answer:**
1.  **String Concatenation:** Use `StringBuilder` explicitly in loops, or `String.format` (be careful with regex).
2.  **Reuse Mutable Objects:** Reuse `StringBuilder`, buffers, or arrays instead of creating new ones.
3.  **Singleton:** Use singletons for stateless service classes.
4.  **Canonicalization:** Intern strings/objects if they are duplicates.

---

## 167. How to optimize multi-threaded performance?

**Answer:**
1.  **Minimize Locking:** Use `java.util.concurrent` (ConcurrentHashMap) instead of `synchronized` collections.
2.  **Lock Granularity:** Use **Striped Locking** (e.g., LongAdder) to reduce contention.
3.  **Non-Blocking Algos:** Use **CAS** (Compare-And-Swap) via `AtomicInteger` for counters.
4.  **False Sharing:** Pad variables (`@Contended`) to prevent cache line ping-pong between threads.

---

## 168. What are common production performance issues?

**Answer:**
1.  **Slow Database Queries:** Missing indexes, N+1 problem.
2.  **Memory Leaks:** Unclosed resources, static collections growing indefinitely.
3.  **Thread Pool Exhaustion:** All threads blocked waiting for external service/DB.
4.  **CPU Spikes:** Infinite loops, excessive GC, or extensive crypto/regex operations.

---

## 169. What metrics do you monitor in production?

**Answer:**
Use the **RED** (Rate, Errors, Duration) or **USE** (Utilization, Saturation, Errors) method.
1.  **Latency:** Response time (Average, p95, p99).
2.  **Throughput:** Requests per second (RPS).
3.  **Error Rate:** Percentage of 5xx/4xx errors.
4.  **Saturation:** CPU Usage, Memory Usage, Disk I/O, Thread Pool active count.

---

## 170. How do you perform load testing?

**Answer:**
**Load Testing** simulates real-world usage to check system behavior.
*   **Tools:** **JMeter**, **Gatling**, **Locust**, **K6**.
*   **Types:**
    *   **Load Test:** Expected normal load.
    *   **Stress Test:** Push beyond limits to find breaking point.
    *   **Soak Test:** Run for long duration (24h+) to find memory leaks.
    *   **Spike Test:** Sudden burst of traffic.

---



---


