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

## 171. What is Inversion of Control?

**Answer:**
**Inversion of Control (IoC)** is a design principle where the control of object creation and management is transferred from the programmer to a container (framework).
*   **Traditional:** App code calls Library. (You control flow).
*   **IoC:** Framework calls App code. (Framework controls flow - "Don't call us, we'll call you").
*   **Implementation:** Dependency Injection (DI) is the most common way to implement IoC.

---

## 172. What is Dependency Injection?

**Answer:**
**Dependency Injection (DI)** is a design pattern used to implement IoC.
*   **Concept:** Instead of an object creating its own dependencies (e.g., `new Service()`), the dependencies are "injected" into the object by an external entity (the Sprng Container).
*   **Benefit:** Loose coupling, easier unit testing (can mock dependencies), and cleaner code.

---

## 173. Constructor vs Setter injection?

**Answer:**

| Feature | Constructor Injection | Setter Injection |
| :--- | :--- | :--- |
| **Use Case** | **Mandatory** dependencies. | **Optional** dependencies. |
| **Immutability** | Fields can be `final`. | Fields cannot be `final`. |
| **Safety** | Object is valid/fully initialized when created. | Object might be in partial state until setters are called. |
| **Preference** | **Recommended** (Spring team preferred). | Use sparingly. |

---

## 174. Field injection drawbacks?

**Answer:**
Field Injection (`@Autowired` directly on field) is generally **discouraged**.
*   **Drawbacks:**
    1.  **Testing:** Hard to unit test because you cannot inject mocks without a Spring Context (or using Reflection).
    2.  **Immutability:** Fields cannot be `final`.
    3.  **Hiding Dependencies:** A class can easily become bloated with too many dependencies without noticing (Constructor arguments makes it obvious).
    4.  **Circular Dependencies:** Easier to accidentally create them.

---

## 175. What is ApplicationContext?

**Answer:**
**ApplicationContext** is the central interface to the Spring IoC Container.
*   **Role:** It instantiates, configures, and assembles beans.
*   **Functionality:** It provides advanced features like:
    *   Internationalization (i18n).
    *   Event publication (ApplicationEvent).
    *   AOP integration.
    *   Transaction management.

---

## 176. BeanFactory vs ApplicationContext?

**Answer:**

| Feature | BeanFactory | ApplicationContext |
| :--- | :--- | :--- |
| **Type** | Basic IoC Container. | Advanced IoC Container (Extends BeanFactory). |
| **Loading** | **Lazy** (Loads beans only when requested `getBean`). | **Eager** (Pre-instantiates all Singletons at startup). |
| **Features** | Basic DI support. | DI + AOP + Messaging + Web support + i18n. |
| **Use Case** | Resource-constrained mobile/embedded apps. | Enterprise Web Applications (Standard). |

---

## 177. What is Bean lifecycle?

**Answer:**
The lifecycle of a Spring Bean:
1.  **Instantiate:** Create object (Constructor).
2.  **Populate Properties:** Inject dependencies (Setters/Fields).
3.  **Aware Interfaces:** setBeanName, setBeanFactory using `BeanNameAware`, etc.
4.  **Pre-Initialization:** `BeanPostProcessor.postProcessBeforeInitialization()`.
5.  **Initialize:** `@PostConstruct`, `InitializingBean.afterPropertiesSet()`, custom `init-method`.
6.  **Post-Initialization:** `BeanPostProcessor.postProcessAfterInitialization()` (AOP Proxies created here).
7.  **Ready:** Bean is ready to use.
8.  **Destroy:** `@PreDestroy`, `DisposableBean.destroy()`, custom `destroy-method` (When context closes).

---

## 178. What are Bean scopes?

**Answer:**
Spring Beans have 6 standard scopes:
1.  **Singleton (Default):** One instance per container.
2.  **Prototype:** New instance every time it is requested.
3.  **Request:** One instance per HTTP Request (Web only).
4.  **Session:** One instance per HTTP Session (Web only).
5.  **Application:** One instance per `ServletContext` (Web only).
6.  **WebSocket:** One instance per WebSocket (Web only).

---

## 179. Singleton vs Prototype?

**Answer:**
*   **Singleton:** Shared instance. **Stateless** beans (Services, DAO, Controllers) should be Singletons. Thread-safety must be handled if state is maintained.
*   **Prototype:** Independent instances. **Stateful** beans (Users, ShoppingCarts) can be Prototypes.
*   **Injection:** If a Singleton bean has a Prototype dependency, the Prototype is injected **once** (at creation time), effectively becoming a Singleton. (Solution: Use `Lookup Method Injection` or `Provider<Prototype>`).

---

## 180. What is @ComponentScan?

**Answer:**
`@ComponentScan` tells Spring where to look for annotated components (beans).
*   **Usage:** `@ComponentScan(basePackages = "com.example")`.
*   **Mechanism:** It scans the specified packages for classes annotated with `@Component` (and its stereotypes `@Service`, `@Repository`, `@Controller`, `@Configuration`) and registers them as beans in the ApplicationContext.
*   **Spring Boot:** `@SpringBootApplication` includes `@ComponentScan` implicitly for the current package and sub-packages.

---

## 181. What is @Component, @Service, @Repository?

**Answer:**
These are Stereotype Annotations used to register beans in the Spring Container.
*   **@Component:** Generic stereotype for any Spring-managed component.
*   **@Service:** Semantically indicates the class holds **Business Logic**. It doesn't add extra behavior over @Component (except for AOP pointcuts).
*   **@Repository:** Indicates a **Data Access Object (DAO)**. It adds automatic **Exception Translation** (converts SQL exceptions to Spring's `DataAccessException` hierarchy).
*   **@Controller:** Indicates a Spring MVC Controller.

---

## 182. What is @Configuration?

**Answer:**
`@Configuration` indicates that a class allows definition of bean methods (annotated with `@Bean`).
*   **Full Mode (Default):** The class is proxied by CGLIB. Calls to `@Bean` methods within the class are intercepted to ensure **dependency injection** and **singleton scope** are respected (calling a bean method twice returns the *same* instance).
*   **Lite Mode:** (`proxyBeanMethods = false`). No CGLIB proxy. Faster startup, but inter-bean method calls create *new instances*.

---

## 183. What is @Bean annotation?

**Answer:**
`@Bean` is a method-level annotation used in a `@Configuration` class to manually define a bean.
*   **Mechanism:** The return value of the method is registered as a bean in the BeanFactory.
*   **ID:** The bean ID is the method name (unless customized `@Bean("myBean")`).
*   **Lifecycle:** Supports `initMethod` and `destroyMethod` attributes.

---

## 184. What is @Primary?

**Answer:**
`@Primary` indicates that a bean should be given **preference** when multiple candidates are qualified to autowire a single-valued dependency.
*   **Use Case:** You have two implementations of `PaymentService` (`CreditCard`, `PayPal`). Mark `CreditCard` as `@Primary` to inject it by default when `@Autowired PaymentService` is used without a qualifier.

---

## 185. What is @Qualifier?

**Answer:**
`@Qualifier` is used for **fine-grained control** over dependency injection when multiple beans of the same type exist.
*   **Usage:** Combined with `@Autowired`.
*   **Example:**
    ```java
    @Autowired
    @Qualifier("payPalService")
    private PaymentService paymentService;
    ```
*   **Difference:** `@Primary` is a default valid for all injection points. `@Qualifier` overrides the default for a *specific* injection point.

---

## 186. What is circular dependency?

**Answer:**
A **Circular Dependency** occurs when Bean A depends on Bean B, and Bean B depends on Bean A.
*   **Result:** The container cannot instantiate either bean because it needs the other one first.
*   **Spring Handling:** Spring can resolve this *only* for **Singleton** beans interacting via **Setter/Field Injection**. It fails for **Constructor Injection** or Prototype beans.

---

## 187. How does Spring resolve circular dependency?

**Answer:**
Spring resolves circular dependencies for singletons using **Three-Level Caching**:
1.  **Singleton Objects (Level 1):** Fully initialized beans.
2.  **Early Singleton Objects (Level 2):** Raw bean instances (instantiated but not populated/initialized).
3.  **Singleton Factories (Level 3):** Object factories to create the bean (or proxy).
*   **Process:** Bean A is created (raw) and exposed in Level 3. Bean B is created, asks for A. It gets the "Early" A reference. B finishes. A finishes.

---

## 188. What is lazy initialization?

**Answer:**
**Lazy Initialization** means the bean is created **only when it is first requested**, not at application startup.
*   **Annotation:** `@Lazy`.
*   **Scope:** Can be applied to a `@Configuration` class (all beans lazy), a specific `@Bean`, or an `@Autowired` injection point (injects a proxy).
*   **Pros:** Faster startup time.
*   **Cons:** Errors (misconfiguration) are discovered at runtime instead of startup.

---

## 189. What is BeanPostProcessor?

**Answer:**
`BeanPostProcessor` (BPP) is a powerful interface that allows custom modification of new bean instances.
*   **Methods:**
    1.  `postProcessBeforeInitialization()`: Runs *after* dependency injection but *before* init methods (`@PostConstruct`).
    2.  `postProcessAfterInitialization()`: Runs *after* init methods.
*   **Use Cases:** Checking marker interfaces, wrapping beans with Proxies (AOP), modifying bean properties.

---

## 190. What is InitializingBean?

**Answer:**
`InitializingBean` is a callback interface with a single method: `afterPropertiesSet()`.
*   **Execution:** Called by the container after all properties are set (DI is complete).
*   **Usage:** Performing custom initialization logic (validating configuration, opening connections).
*   **Alternative:** `@PostConstruct` annotation (JSR-250) is generally preferred over implementing this Spring-specific interface.

---


---

## 191. What is AOP?

**Answer:**
**AOP (Aspect-Oriented Programming)** is a programming paradigm that aims to increase modularity by allowing the separation of **cross-cutting concerns**.
*   **Cross-cutting concerns:** Functions that span multiple points of an application (e.g., Logging, Security, Transaction Management).
*   **Goal:** To keep business logic clean and separate from system services.

---

## 192. What is aspect?

**Answer:**
An **Aspect** is a modularization of a cross-cutting concern.
*   **Analogy:** In OOP, a key unit of modularity is the `Class`. In AOP, it is the `Aspect`.
*   **Implementation:** In Spring AOP, aspects are implemented using regular classes annotated with `@Aspect` (or XML configuration).
*   **Example:** A `LoggingAspect` class.

---

## 193. What is advice?

**Answer:**
**Advice** is the action taken by an aspect at a particular **Join Point**.
*   **Concept:** It is the actual code (method) that executes when a specific point in the application is reached.
*   **Example:** "Log this message" or "Begin transaction".

---

## 194. Types of advice?

**Answer:**
Spring AOP supports 5 types of advice:
1.  **@Before:** Executes *before* a join point.
2.  **@AfterReturning:** Executes *after* a join point completes normally.
3.  **@AfterThrowing:** Executes if a method exits by throwing an exception.
4.  **@After (Finally):** Executes *after* a join point regardless of the outcome (normal or exception).
5.  **@Around:** The most powerful advice. It surrounds the join point (can perform custom behavior before and after invocation, or even skip invocation).

---

## 195. What is pointcut?

**Answer:**
A **Pointcut** is a predicate (expression) that matches **Join Points**.
*   **Role:** Advice is associated with a pointcut expression and runs at any join point matched by the pointcut.
*   **Expression Language:** Spring uses the AspectJ pointcut expression language.
*   **Example:** `execution(* com.example.service.*.*(..))` (Matches all methods in service package).

---

## 196. What is join point?

**Answer:**
A **Join Point** is a point during the execution of a program, such as the **execution of a method** or the handling of an exception.
*   **Scope:** In Spring AOP, a join point *always* represents a **method execution**.
*   **Info:** You can access join point details (method name, arguments) via the `JoinPoint` parameter in the advice method.

---

## 197. What is weaving?

**Answer:**
**Weaving** is the process of linking aspects with other application types or objects to create an advised object.
*   **Time:** Can occur at:
    *   **Compile Time:** (using AspectJ compiler).
    *   **Load Time:** (using AspectJ loader).
    *   **Runtime:** (Spring AOP default). Spring creates proxies at runtime.

---

## 198. Proxy-based AOP vs AspectJ?

**Answer:**

| Feature | Spring AOP | AspectJ |
| :--- | :--- | :--- |
| **Weaving** | **Runtime** (Proxy). | **Compile-time** / Load-time / Post-compile. |
| **Scope** | Only **Method Execution** on Spring Beans. | Constructor, Field access, Static methods, Final classes. |
| **Performance** | Good (Sufficient for most enterprise needs). | Much Faster (No runtime overhead of proxy creation). |
| **Complexity** | Simple (Pure Java). | Complex (Requires separate compiler/agent). |

---

## 199. What is @Transactional internally?

**Answer:**
`@Transactional` works using **Spring AOP**.
1.  Spring creates a **Proxy** around the bean.
2.  When a method is called, the Proxy's **Around Advice** intercepts it.
3.  It opens a DB Transaction (from TransactionManager).
4.  It executes the actual method.
5.  If success -> **Commit**. If RuntimeException -> **Rollback**.

---

## 200. What are common AOP use cases?

**Answer:**
1.  **Declarative Transaction Management:** (`@Transactional`).
2.  **Logging/Tracing:** Log every method entry/exit or execution time.
3.  **Security:** checking roles before method execution (`@PreAuthorize`).
4.  **Caching:** (`@Cacheable`).
5.  **Error Handling:** Global exception handling.

---

## 201. What is Spring Boot?

**Answer:**
**Spring Boot** is an opinionated framework built on top of the Spring Framework.
*   **Goal:** To simplify the bootstrapping and development of new Spring applications.
*   **Key Features:**
    1.  **Auto-Configuration:** Automatically configures your application based on jar dependencies.
    2.  **Standalone:** Creates stand-alone Spring applications with embedded servers (Tomcat, Jetty).
    3.  **Opinionated:** Provides "Starter" dependencies to simplify build configuration.
    4.  **Production-ready:** Includes metrics, health checks, and externalized configuration.

---

## 202. What is auto-configuration?

**Answer:**
**Auto-configuration** attempts to automatically configure your Spring application based on the jar dependencies that you have added.
*   **Mechanism:** It uses `@EnableAutoConfiguration` (part of `@SpringBootApplication`).
*   **Example:** If `HSQLDB` is on your classpath, and you haven't manually configured any database connection beans, Spring Boot auto-configures an in-memory database.
*   **Debug:** Use `debug=true` in `application.properties` to see the **Positive matches** (applied configs) and **Negative matches** (skipped configs).

---

## 203. How does @SpringBootApplication work?

**Answer:**
`@SpringBootApplication` is a convenience annotation that combines three valid annotations:
1.  **@Configuration:** Allows Java-based configuration.
2.  **@EnableAutoConfiguration:** Enables Spring Boot's auto-configuration mechanism.
3.  **@ComponentScan:** Scans for components in the current package and its sub-packages.

---

## 204. What is starter dependency?

**Answer:**
**Starters** are a set of convenient dependency descriptors that you can include in your application.
*   **Benefit:** Instead of copying sample dependency code for 10 different libraries, you include one "starter".
*   **Example:** `spring-boot-starter-web` imports:
    *   Spring MVC
    *   Jackson (JSON)
    *   Tomcat (Embedded Server)
    *   Validation API

---

## 205. What is embedded server?

**Answer:**
An **Embedded Server** means the HTTP server (like Tomcat, Jetty, Undertow) is packaged **inside** your application JAR.
*   **Traditional:** You build a WAR file and deploy it into an external Tomcat server.
*   **Spring Boot:** You build an executable JAR. When you run `java -jar app.jar`, it starts the embedded Tomcat, which then hosts your application.
*   **Default:** Tomcat (Port 8080).

---

## 206. How to change server port?

**Answer:**
You can change the embedded server port in `application.properties` (or `application.yml`):
```properties
server.port=8081
```
Or via command line argument:
```bash
java -jar app.jar --server.port=8081
```

---

## 207. What is application.properties vs YAML?

**Answer:**
Both are used for external configuration.
*   **Properties:** Standard Java format (`key=value`), flat structure.
*   **YAML (.yml):** Hierarchical structure (indentation-based), more readable for complex configurations (lists, maps).
*   **Precedence:** If both exist, properties usually override YAML (implementation detail, but good to know).

---

## 208. What is profiles in Spring Boot?

**Answer:**
**Profiles** provide a way to segregate parts of your application configuration and make it be available only in certain environments.
*   **Usage:** `application-dev.properties`, `application-prod.properties`.
*   **Activation:**
    *   `spring.profiles.active=dev` in `application.properties`.
    *   `--spring.profiles.active=prod` command line argument.

---

## 209. What is actuator?

**Answer:**
**Spring Boot Actuator** adds production-ready features to your application to help you **monitor and manage** it.
*   **Endpoints:** Exposes HTTP (or JMX) endpoints to check health, metrics, environment, beans, etc.
*   **Dependency:** `spring-boot-starter-actuator`.

---

## 210. Important actuator endpoints?

**Answer:**
*   `/actuator/health`: Application health status (UP/DOWN).
*   `/actuator/info`: Arbitrary application info.
*   `/actuator/metrics`: JVM, CPU, Memory metrics.
*   `/actuator/loggers`: View and modify logging levels at runtime.
*   `/actuator/env`: Environment variables and properties.
*   `/actuator/beans`: List of all Spring beans.
*   `/actuator/threaddump`: Thread dump.
*   `/actuator/heapdump`: Heap dump.

---

## 211. What is Spring Boot DevTools?

**Answer:**
**Spring Boot DevTools** is a module that improves the development experience.
*   **Automatic Restart:** Automatically restarts the application when classes on the classpath change (faster than full cold start).
*   **LiveReload:** Triggers a browser refresh when resources change, provided the LiveReload browser extension is installed.
*   **Property Defaults:** Disables caching for templates (Thymeleaf/Freemarker) to see changes immediately.

---

## 212. What is CommandLineRunner?

**Answer:**
`CommandLineRunner` is a functional interface used to run code **once** after the Spring Boot application has started.
*   **Method:** `void run(String... args)`.
*   **Usage:** Database initialization, seeding data, or checking system integrity at startup.
*   **Alternative:** `ApplicationRunner` (Same purpose, but receives arguments as an `ApplicationArguments` object instead of raw String array).

---

## 213. What is @ConfigurationProperties?

**Answer:**
`@ConfigurationProperties` is used to bind external configuration properties (from `application.properties`) to a Java Bean.
*   **Type-safe:** Provides strongly typed configuration with validation.
*   **Structure:** Can map hierarchical data (lists, maps, nested objects).
*   **Usage:**
    ```java
    @ConfigurationProperties(prefix = "app.mail")
    @Component
    public class MailConfig {
        private String host;
        private int port;
        // getters/setters
    }
    ```

---

## 214. How to externalize configuration?

**Answer:**
Spring Boot lets you externalize configuration so you can work with the same code in different environments.
**Priority Order (High to Low):**
1.  Command line arguments (`--server.port=9000`).
2.  Java System properties (`-Dserver.port=9000`).
3.  OS Environment variables.
4.  `application-profile.properties` (outside jar).
5.  `application-profile.properties` (inside jar).
6.  `application.properties` (outside/inside jar).

---

## 215. What is logging configuration?

**Answer:**
Spring Boot uses **Commons Logging** for all internal logging but leaves the underlying log implementation open.
*   **Default:** **Logback**.
*   **Console Output:** Enabled by default.
*   **File Output:** Set `logging.file.name` or `logging.file.path`.
*   **Levels:** `logging.level.com.example=DEBUG`.
*   **Custom:** Add `logback-spring.xml` or `log4j2.xml` to the classpath for advanced control.

---

## 216. How to secure actuator endpoints?

**Answer:**
Since Actuator endpoints expose sensitive data, they should be secured using **Spring Security**.
1.  **Exclude Sensitivity:** By default, only `/health` and `/info` are exposed over HTTP.
2.  **Enable All:** `management.endpoints.web.exposure.include=*`.
3.  **Security Config:**
    ```java
    http.requestMatchers(EndpointRequest.toAnyEndpoint())
        .hasRole("ADMIN")
    ```

---

## 217. What is Spring Boot caching support?

**Answer:**
Spring Boot provides an abstraction for transparent caching.
*   **Enable:** `@EnableCaching`.
*   **Annotate:** `@Cacheable("users")` on methods.
*   **Providers:** Auto-configures providers like **Redis**, **Caffeine**, **EhCache**, or **Hazelcast** if they are on the classpath.
*   **Fallback:** Uses a `ConcurrentHashMap` if no provider is found.

---

## 218. What is Spring Boot CLI?

**Answer:**
**Spring Boot CLI** (Command Line Interface) is a command-line tool for prototyping with Spring.
*   **Groovy:** It allows running **Groovy** scripts that look like Java without boilerplate (no imports, no `public class`, no `main` method).
*   **Usage:** Swiftly testing code snippets or writing simple scripts.

---

## 219. What is custom auto-configuration?

**Answer:**
You can create your own starter libraries that auto-configure beans for other applications.
*   **Steps:**
    1.  Create a standard `@Configuration` class.
    2.  Use `@Conditional` annotations (`@ConditionalOnClass`, `@ConditionalOnMissingBean`) to define when configuration should apply.
    3.  Register the config class in `META-INF/spring.factories` (or `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` in newer versions).

---

## 220. How to create fat jar?

**Answer:**
A **Fat Jar** (or Uber Jar) contains the compiled application classes AND all dependency JARs.
*   **Plugin:** The **Spring Boot Maven Plugin** (or Gradle plugin) Repackages the standard jar.
*   **Command:** `mvn clean package`.
*   **Result:** A runnable jar file that can be executed via `java -jar application.jar` without needing an external classpath setup.

---

## 221. How to run Spring Boot app in production?

**Answer:**
1.  **Executable JAR:** `java -jar app.jar` (simplest).
2.  **Docker:** Create a Docker image and run it in a container orchestrator (Kubernetes).
3.  **Systemd Service:** Run as a Linux service (background process) managed by `systemd`.
4.  **WAR Deployment:** Deploy to an external Tomcat/Wildfly/WebLogic server (Legacy).

---

## 222. How to enable HTTPS?

**Answer:**
You need an SSL certificate (PKCS12 or JKS). Configure it in `application.properties`:
```properties
server.ssl.key-store=classpath:keystore.p12
server.ssl.key-store-password=changeit
server.ssl.key-store-type=PKCS12
server.ssl.key-alias=tomcat
server.port=8443
```

---

## 223. How to configure multiple datasources?

**Answer:**
1.  **Properties:** Define two sets of properties (e.g., `app.datasource.primary`, `app.datasource.secondary`).
2.  **Beans:** Create two `DataSource` beans. Mark one as `@Primary`.
3.  ** EntityManager:** If using JPA, you also need to configure two `EntityManagerFactory` and `TransactionManager` beans, pointing to respective datasources and package scans.

---

## 224. How to enable async in Spring Boot?

**Answer:**
1.  **Enable:** Add `@EnableAsync` to a configuration class.
2.  **Usage:** Annotate a method with `@Async`.
3.  **Behavior:** The method executes in a separate thread (from a helper TaskExecutor).
4.  **Return Type:** `void` or `Future<T>` / `CompletableFuture<T>`.

---

## 225. How to implement global exception handling?

**Answer:**
Use **@ControllerAdvice** (or `@RestControllerAdvice`) and **@ExceptionHandler**.
*   **Mechanism:** It acts as an interceptor for exceptions thrown by any controller.
*   **Example:**
    ```java
    @RestControllerAdvice
    public class GlobalExceptionHandler {
        @ExceptionHandler(UserNotFoundException.class)
        public ResponseEntity<String> handleUserNotFound(Exception ex) {
            return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
        }
    }
    ```

---

## 226. What is DispatcherServlet?

**Answer:**
**DispatcherServlet** is the **Front Controller** in Spring MVC.
*   **Role:** It receives **all** incoming HTTP requests and delegates them to the appropriate controllers.
*   **Workflow:**
    1.  Receive Request.
    2.  Consult `HandlerMapping` to find the correct Controller.
    3.  Call the Controller method.
    4.  Receive Model and View name.
    5.  Consult `ViewResolver` to find the physical view file (JSP/Thymeleaf).
    6.  Render the view and return the response.

---

## 227. Explain Spring MVC architecture.

**Answer:**
Spring MVC is request-driven, designed around a central servlet that dispatches requests to controllers.
1.  **Request** -> **DispatcherServlet**
2.  **DispatcherServlet** -> **HandlerMapping** (Which controller?)
3.  **DispatcherServlet** -> **Controller** (Execute logic)
4.  **Controller** -> **DispatcherServlet** (Return Model & View Name)
5.  **DispatcherServlet** -> **ViewResolver** (Which file?)
6.  **DispatcherServlet** -> **View** (Render HTML)
7.  **Response** -> **Client**

---

## 228. What is @Controller?

**Answer:**
`@Controller` is a stereotype annotation used to mark a class as a Spring MVC Controller.
*   **Component:** It is a specialization of `@Component`, so it is auto-detected by component scanning.
*   **Role:** Handles web requests.
*   **Return Value:** By default, methods return a **String** representing the **View Name** (e.g., "home" -> `home.jsp`), which needs a ViewResolver.

---

## 229. What is @RestController?

**Answer:**
`@RestController` is a convenience annotation that combines `@Controller` and `@ResponseBody`.
*   **Purpose:** Used for creating **RESTful Web Services**.
*   **Return Value:** Methods return **Data** (domain objects/collections) directly written to the HTTP response body as JSON/XML (not a View Name).
*   **Equivalence:** `@RestController` = `@Controller` + `@ResponseBody`.

---

## 230. What is @RequestMapping?

**Answer:**
`@RequestMapping` is used to map HTTP requests to handler methods of MVC and REST controllers.
*   **Attributes:**
    *   `value` / `path`: URL pattern (`/users`).
    *   `method`: HTTP method (`GET`, `POST`).
    *   `consumes`: Content-Type accepted (`application/json`).
    *   `produces`: Content-Type returned.
*   **Shortcuts:** `@GetMapping`, `@PostMapping`, `@PutMapping`, `@DeleteMapping`, `@PatchMapping`.

---



---

## 231. Difference between GET and POST mapping?

**Answer:**
*   **@GetMapping:** Maps HTTP GET requests. Used for **retrieving** data. Safe and Idempotent.
*   **@PostMapping:** Maps HTTP POST requests. Used for **creating** new resources. Not Idempotent.
*   **Technical:** `@GetMapping` is a shortcut for `@RequestMapping(method = RequestMethod.GET)`.

---

## 232. What is @PathVariable?

**Answer:**
**@PathVariable** extracts values from the URI path segment.
*   **Usage:** When the URL contains dynamic values identifying a resource.
*   **Example:**
    ```java
    @GetMapping("/users/{id}")
    public User getUser(@PathVariable("id") Long id) { ... }
    ```
    URL: `/users/101` -> `id = 101`.

---

## 233. What is @RequestParam?

**Answer:**
**@RequestParam** extracts query parameters from the URL.
*   **Usage:** Filtering, sorting, or optional parameters.
*   **Example:**
    ```java
    @GetMapping("/users")
    public List<User> search(@RequestParam("name") String name) { ... }
    ```
    URL: `/users?name=John` -> `name = "John"`.

---

## 234. What is @RequestBody?

**Answer:**
**@RequestBody** maps the **HTTP Request Body** to a Java Object.
*   **Usage:** Typically used in POST/PUT methods to send complex data (JSON/XML).
*   **Converter:** Uses `HttpMessageConverter` (like Jackson) to deserialize JSON to Java.

---

## 235. What is @ResponseBody?

**Answer:**
**@ResponseBody** indicates that the return value of a method should be written directly to the **HTTP Response Body** rather than resolving to a view.
*   **Usage:** REST APIs returning JSON/XML.
*   **Default:** implicitly added in `@RestController`.

---

## 236. What is ResponseEntity?

**Answer:**
**ResponseEntity** represents the entire HTTP response: **Status Code**, **Headers**, and **Body**.
*   **Control:** It gives you full control over the response.
*   **Example:**
    ```java
    return ResponseEntity.status(HttpStatus.CREATED)
            .header("Custom-Header", "foo")
            .body(newUser);
    ```

---

## 237. What is HttpMessageConverter?

**Answer:**
**HttpMessageConverter** is a strategy interface that converts data between HTTP requests/responses and Java objects.
*   **Serialization:** Object -> JSON/XML (Response).
*   **Deserialization:** JSON/XML -> Object (Request).
*   **Common Impls:** `MappingJackson2HttpMessageConverter` (JSON), `StringHttpMessageConverter`.
*   **Trigger:** Automatically selected based on `Content-Type` and `Accept` headers.

---

## 238. What is content negotiation?

**Answer:**
**Content Negotiation** is the mechanism to determine the best representation for a given resource when multiple representations are available.
*   **Driver:** The Client sends an `Accept` header (e.g., `application/json` or `application/xml`).
*   **Server:** Spring MVC checks the `Accept` header and uses the appropriate `HttpMessageConverter` to produce the response.

---

## 239. What is @ModelAttribute?

**Answer:**
**@ModelAttribute** binds a method parameter or method return value to a named model attribute, exposed to a web view.
*   **Parameter:** Maps form data / query params to a Java bean. `public String save(@ModelAttribute User user)`.
*   **Method:** Populates the model with attributes before controller methods run. `@ModelAttribute("categories") public List<String> getCategories() { ... }`.

---

## 240. What is data binding?

**Answer:**
**Data Binding** is the process of binding HTTP request parameters (strings) to Java Objects (typed fields).
*   **Component:** `DataBinder`.
*   **Mechanism:** It uses PropertyEditors or Converters to convert String values (from URL/Form) to types like `int`, `Date`, `boolean`.
*   **Errors:** Validation errors are captured in `BindingResult`.

---

## 241. What is validation in Spring MVC?

**Answer:**
**Validation** ensures that the data received from the client meets specific criteria before processing.
*   **JSR-303/JSR-380 (Bean Validation):** Standard API (Hibernate Validator is the reference implementation).
*   **Annotations:** `@NotNull`, `@Size`, `@Email`, `@Min`, `@Max`.
*   **Usage:** Annotate fields in your DTO/Model, and use `@Valid` in the controller method.

---

## 242. What is @Valid vs @Validated?

**Answer:**
*   **@Valid:** Standard JSR-303 annotation. Put it on a method parameter to trigger validation.
*   **@Validated:** Spring's variant.
    *   **Features:** Supports **Validation Groups** (validate different fields for Create vs Update).
    *   **Scope:** Can be used on **Class level** (for validating `@RequestParam`/`@PathVariable`) which `@Valid` cannot handle directly.

---

## 243. What is BindingResult?

**Answer:**
**BindingResult** is a Spring object that holds the result of the validation and binding and contains any errors that may have occurred.
*   **Order:** It **must** immediately follow the model object being validated in the method signature.
*   **Usage:**
    ```java
    public String save(@Valid User user, BindingResult result) {
        if (result.hasErrors()) {
            return "error-page";
        }
        // ...
    }
    ```

---

## 244. What is @ExceptionHandler?

**Answer:**
**@ExceptionHandler** is an annotation used to handle exceptions thrown during the execution of request handlers.
*   **Scope:** By default, it handles exceptions only from the **same controller**.
*   **Usage:** Define a method that takes the Exception type as an argument and returns an appropriate error response/view.

---

## 245. What is @ControllerAdvice?

**Answer:**
**@ControllerAdvice** allows you to share `@ExceptionHandler`, `@InitBinder`, and `@ModelAttribute` methods across **multiple controllers**.
*   **Purpose:** Global Exception Handling.
*   **Benefit:** Centralized error handling logic, reducing code duplication in individual controllers.

---

## 246. What is Interceptor in Spring?

**Answer:**
**HandlerInterceptor** intercepts requests **before** they reach the DispatcherServlet's handler (Controller) and **after** the handler finishes.
*   **Methods:**
    1.  `preHandle()`: Before controller. Return `false` to abort request.
    2.  `postHandle()`: After controller, before view render.
    3.  `afterCompletion()`: After view render (cleanup).
*   **Use Case:** Logging, authentication, modifying the model globally.

---

## 247. Filter vs Interceptor difference?

**Answer:**

| Feature | Filter (Servlet) | Interceptor (Spring) |
| :--- | :--- | :--- |
| **Level** | **Low-level** (Servlet Container). | **High-level** (Spring Context). |
| **Scope** | Runs for *all* web requests (including static resources). | Runs only for requests handled by **DispatcherServlet**. |
| **Access** | `ServletRequest`, `ServletResponse`. | `HttpServletRequest`, `HttpServletResponse`, plus **Handler** (Controller bean) and **ModelAndView**. |
| **Dependency Injection** | Harder (historically), now easier in Boot. | Native Spring Bean (Easy DI). |

---

## 248. How does Spring handle CORS?

**Answer:**
**CORS (Cross-Origin Resource Sharing)** is handled via:
1.  **@CrossOrigin:** Annotation on Controller class or method.
    *   `@CrossOrigin(origins = "http://localhost:3000")`
2.  **Global Configuration:** Override `addCorsMappings` in `WebMvcConfigurer`.
    *   `registry.addMapping("/api/**").allowedOrigins("*")`

---

## 249. How to handle file upload?

**Answer:**
Use `MultipartFile` to handle uploaded files.
*   **Configuration:** `spring.servlet.multipart.max-file-size` (default 1MB).
*   **Controller:**
    ```java
    @PostMapping("/upload")
    public void upload(@RequestParam("file") MultipartFile file) {
        // file.getInputStream() or file.transferTo(dest)
    }
    ```

---

## 250. What is view resolver?

**Answer:**
**ViewResolver** translates a logical view name (returned by Controller) into a physical view resource.
*   **Example:** Returns "home" -> Resolves to `/WEB-INF/templates/home.html` (Thymeleaf) or `/WEB-INF/jsp/home.jsp` (InternalResourceViewResolver).
*   **Chain:** You can chain multiple resolvers (e.g., check for explicit bean name first, then JSP).

---

## 251. What is ORM?

**Answer:**
**ORM (Object-Relational Mapping)** is a technique that lets you query and manipulate data from a database using an object-oriented paradigm.
*   **Concept:** Maps Java Objects (Entities) to Database Tables.
*   **Benefit:** Developers focus on Java logic instead of writing complex SQL queries.
*   **Tools:** Hibernate, EclipseLink, OpenJPA.

---

## 252. What is JPA?

**Answer:**
**JPA (Java Persistence API)** is a **Specification** (Interface) for accessing, persisting, and managing data between Java objects and a relational database.
*   **Nature:** It is just a set of rules and interfaces (`javax.persistence.*` or `jakarta.persistence.*`). It is **not** an implementation.
*   **Role:** Defines *how* ORM should work in Java.

---

## 253. What is Hibernate?

**Answer:**
**Hibernate** is an **Implementation** of the JPA specification.
*   **Role:** It is the actual framework that performs the mapping and generates SQL.
*   **Features:** It implements JPA but also offers proprietary features (Hibernate Query Language - HQL, Criteria API, Native SQL).

---

## 254. Difference between JPA and Hibernate?

**Answer:**

| Feature | JPA | Hibernate |
| :--- | :--- | :--- |
| **Type** | Specification (Interface). | Implementation (Provider). |
| **Usage** | Cannot be used alone. | Can be used alone or via JPA. |
| **Switching** | Code written against JPA interfaces can easily switch providers. | Code using Hibernate-specific features is locked to Hibernate. |
| **Analogy** | Like JDBC Interface. | Like Oracle JDBC Driver. |

---

## 255. What is Entity?

**Answer:**
An **Entity** is a lightweight, persistent domain object.
*   **Mapping:** It represents a table in a relational database.
*   **Instance:** Each instance of an entity corresponds to a row in that table.
*   **Annotation:** Marked with `@Entity`.
*   **Requirement:** Must have a no-arg constructor and a primary key (`@Id`).

---

## 256. What is @Id and @GeneratedValue?

**Answer:**
*   **@Id:** Specifies the primary key of an entity.
*   **@GeneratedValue:** Provides for the specification of generation strategies for the values of primary keys.
    *   Unlike manually checking max ID and incrementing, this delegates ID generation to the database or provider.

---

## 257. GenerationType strategies?

**Answer:**
1.  **AUTO (Default):** Persistence provider picks the best strategy based on the DB (often SEQUENCE or TABLE).
2.  **IDENTITY:** Relies on an auto-increment column in the DB (MySQL, SQL Server). ID is available only *after* insert.
3.  **SEQUENCE:** Uses a database sequence (Oracle, PostgreSQL). Efficient (can pre-fetch IDs).
4.  **TABLE:** Uses a separate table to keep the next ID. Slow (locking issues), generally avoided.

---

## 258. What is persistence context?

**Answer:**
The **Persistence Context** is a set of entity instances in which for every persistent identity directly referred to, there is a unique entity instance.
*   **Management:** It manages the lifecycle of entities (New, Manage, Detached, Removed).
*   **Scope:** Usually bound to a Transaction.
*   **Visual:** Think of it as the "First-Level Cache" where Hibernate stores objects it is currently tracking.

---

## 259. What is EntityManager?

**Answer:**
**EntityManager** is the primary JPA interface for interacting with the persistence context.
*   **Role:** Used to create, read, and remove operations for entities.
*   **Methods:** `persist()`, `merge()`, `remove()`, `find()`, `createQuery()`.
*   **Spring:** In Spring, you typically inject it via `@PersistenceContext`.

---

## 260. What is first-level cache?

**Answer:**
**First-Level Cache** is the session-level cache associated with the `EntityManager` (or Hibernate `Session`).
*   **Scope:** Transactional. Valid only while the EntityManager is open.
*   **Behavior:** If you request an entity with the same ID twice in the same transaction, Hibernate returns the object from cache (no second SQL query).
*   **Mandatory:** It is enabled by default and cannot be disabled.

---

## 261. Entity lifecycle states?

**Answer:**
JPA defines 4 states for an entity:
1.  **Transient (New):** Object created (`new User()`) but not associated with any EntityManager. No ID (mostly).
2.  **Managed (Persistent):** Associated with an EntityManager and has an ID. Changes are tracked and synced to DB.
3.  **Detached:** Previously managed, but the EntityManager is closed or `detach()` was called. Changes are **not** tracked.
4.  **Removed:** Scheduled for deletion from the DB.

---

## 262. What is detached entity?

**Answer:**
A **Detached Entity** is an object that has a database identity (ID) but is no longer connected to an active Persistence Context.
*   **Cause:** Transaction ended, Session closed, or explicit `em.detach(entity)`.
*   **Effect:** Modifying this object will **not** update the database unless it is re-attached (merged).

---

## 263. What is merge()?

**Answer:**
**merge()** is used to re-attach a detached entity to the persistence context.
*   **Behavior:**
    1.  It loads the entity with the same ID from the database (or cache).
    2.  It copies the fields from the detached object to the managed object.
    3.  It returns the **managed** instance.
*   **Note:** The original object passed to `merge()` remains detached.

---

## 264. What is persist()?

**Answer:**
**persist()** is used to make a transient instance **managed** and persistent.
*   **Effect:** It executes an `INSERT` statement (immediately or at flush time).
*   **Constraint:** If the entity already has an ID (generated strategy), calling `persist()` might throw an exception (depending on strategy).

---

## 265. What is remove()?

**Answer:**
**remove()** deletes the entity instance.
*   **State:** Transitions a managed entity to the **Removed** state.
*   **Effect:** It executes a `DELETE` statement at flush time.
*   **Constraint:** You can only remove **managed** entities. If you have a detached entity, you must `merge()` it first (or `getReference()`), then `remove()`.

---

## 266. What is flush()?

**Answer:**
**flush()** forces the EntityManager to synchronize the persistence context with the database.
*   **Action:** Executes pending SQL statements (INSERT, UPDATE, DELETE) immediately.
*   **Auto-flush:** Hibernate usually flushes automatically before a query execution (to ensure query sees latest data) and at transaction commit.

---

## 267. What is dirty checking?

**Answer:**
**Dirty Checking** is a feature where Hibernate automatically detects changes made to **managed** entities and updates the database.
*   **Mechanism:** When you load an entity, Hibernate keeps a snapshot. At flush time, it compares the current state with the snapshot. If different, it generates an `UPDATE` statement.
*   **Benefit:** You don't need to explicitly call `save()` or `update()` for managed objects.

---

## 268. What is cascading?

**Answer:**
**Cascading** allows operations performed on a parent entity to be automatically propagated to its child entities.
*   **Usage:** Configured via `cascade` attribute in relationships (`@OneToMany(cascade = CascadeType.ALL)`).
*   **Example:** if `User` has `List<Address>`, deleting `User` should delete all `Address` records.

---

## 269. Cascade types?

**Answer:**
Standard JPA Cascade Types:
1.  **PERSIST:** Propagates `persist()`.
2.  **MERGE:** Propagates `merge()`.
3.  **REMOVE:** Propagates `remove()`.
4.  **REFRESH:** Propagates `refresh()`.
5.  **DETACH:** Propagates `detach()`.
6.  **ALL:** All of the above.

---

## 270. What is orphanRemoval?

**Answer:**
**orphanRemoval** is a special feature (specific to `@OneToMany` and `@OneToOne`) that cleans up "orphaned" entities.
*   **Behavior:** If you remove a child entity from the collection of the parent, Hibernate automatically deletes that child from the database.
*   **Diff from Cascade.REMOVE:** `Cascade.REMOVE` only deletes children if the *Parent* is deleted. `orphanRemoval=true` deletes children if they are *disconnected* from the Parent.

---

## 271. @OneToOne vs @OneToMany?

**Answer:**
*   **@OneToOne:** Each row in Table A links to exactly one row in Table B.
    *   Example: `User` and `UserProfile`.
*   **@OneToMany:** Each row in Table A links to multiple rows in Table B.
    *   Example: `User` and `Orders`.
    *   Usually paired with `@ManyToOne` on the child side for bidirectional navigation.

---

## 272. Owning side vs inverse side?

**Answer:**
In a bidirectional relationship:
*   **Owning Side:** The side that **physically contains the foreign key** in the database.
    *   This side is responsible for updating the relationship in the DB.
*   **Inverse Side:** The other side, strictly for object navigation.
    *   Marked with `mappedBy`.
    *   Changes to the inverse side collection are **ignored** by Hibernate unless the owning side is also updated.

---

## 273. What is mappedBy?

**Answer:**
**mappedBy** is an attribute used on the **Inverse Side** of a relationship (usually `@OneToMany` or `@OneToOne`).
*   **Meaning:** "I am not responsible for this relationship. Look at the field named 'X' in the other class to find the configuration."
*   **Rule:** If you don't use `mappedBy` on a `@OneToMany`, Hibernate creates a separate Join Table by default instead of using a standard Foreign Key.

---

## 274. FetchType LAZY vs EAGER?

**Answer:**
*   **EAGER:** The related data is loaded **immediately** with the parent entity (often using a JOIN).
    *   Default for `@ManyToOne`, `@OneToOne`.
*   **LAZY:** The related data is loaded **on demand** (only when you call `getOrders()`).
    *   Default for `@OneToMany`, `@ManyToMany`.
    *   **Best Practice:** Prefer LAZY to avoid performance issues (loading too much data).

---

## 275. What is N+1 problem?

**Answer:**
The **N+1 Select Problem** occurs when you fetch a list of **N** parent entities, and then iterate over them to fetch a related child entity (Lazy Loaded).
*   **Query 1:** Fetch N Parents (`SELECT * FROM User`).
*   **Queries N:** Fetch Child for each Parent (`SELECT * FROM Address WHERE user_id = ?`).
*   **Total:** 1 + N queries. This kills performance for large details.

---

## 276. How to solve N+1?

**Answer:**
1.  **Join Fetch:** Use `JOIN FETCH` in JPQL/HQL.
    *   `SELECT u FROM User u JOIN FETCH u.addresses`.
    *   This forces a single SQL JOIN query.
2.  **EntityGraph:** Use `@EntityGraph` in JPA 2.1 to define fetch plans.
3.  **BatchFetching:** `@BatchSize(size = 10)` loads children in batches (IN clause) rather than one by one.

---

## 277. What is @JoinColumn?

**Answer:**
**@JoinColumn** specifies the Foreign Key column name in the database.
*   **Location:** Placed on the **Owning Side** of the relationship.
*   **Example:**
    ```java
    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;
    ```

---

## 278. What is @JoinTable?

**Answer:**
**@JoinTable** is used to map a relationship using a separate **Link Table** (Association Table).
*   **Default:** Default for `@ManyToMany`.
*   **Optional:** Can be used for `@OneToMany` if you don't want a foreign key in the child table (clean schema).
*   **Attributes:** `joinColumns` (FK to source), `inverseJoinColumns` (FK to target).

---

## 279. What is @Embeddable?

**Answer:**
**@Embeddable** marks a class whose instances are stored as an intrinsic part of an owning entity and share the identity of the entity.
*   **Usage:** Value Objects (e.g., `Address` with street, city, zip).
*   **@Embedded:** Used in the parent entity to include the embeddable.
*   **DB:** Fields define columns in the *same table* as the parent entity.

---

## 280. What is inheritance mapping strategies?

**Answer:**
JPA supports mapping inheritance hierarchies to DB tables:
1.  **SINGLE_TABLE (Default):** One table for the whole hierarchy. Uses a "Discriminator Column" (DTYPE). Fast, but nullable columns.
2.  **JOINED:** Base table + separate table for each subclass (with FK). Normalized, but slow (JOINs).
3.  **TABLE_PER_CLASS:** Separate table for each concrete class. No shared table. Unions are slow.

---

## 281. What is JPQL?

**Answer:**
**JPQL (Java Persistence Query Language)** is an object-oriented query language defined in the JPA specification.
*   **Target:** It queries **Entity Objects** and their attributes, not database tables.
*   **Portability:** It is database-independent. The provider translates JPQL to SQL for the specific DB dialect.
*   **Example:** `SELECT u FROM User u WHERE u.age > 18`.

---

## 282. JPQL vs Native Query?

**Answer:**
*   **JPQL:** Operates on Entities. Database agnostic. Preferred for standard CRUD and business logic.
*   **Native Query:** Operates on Tables (SQL). Database specific.
    *   **Use Case:** When you need ultra-specific SQL features (Window functions, complex joins, stored procedure calls) not supported by JPQL.
    *   **Risk:** Ties your code to a specific database vendor.

---

## 283. What is Criteria API?

**Answer:**
**Criteria API** is a programmatic, type-safe way to define dynamic queries.
*   **Mechanism:** You build the query object using Java methods (`cb.equal()`, `cb.greaterThan()`) instead of string concatenation.
*   **Advantage:** Errors are caught at compile time. Useful for dynamic search filters (e.g., search screen with 10 optional fields).

---

## 284. What is named query?

**Answer:**
A **Named Query** is a statically defined query with a predefined unchangeable query string.
*   **Definition:** Defined on the Entity class using `@NamedQuery`.
*   **Performance:** Validated and parsed at application startup (fail-fast), creating a slight performance boost over dynamic JPQL.
*   **Usage:** `em.createNamedQuery("User.findAll").getResultList()`.

---

## 285. What is @Query annotation?

**Answer:**
In **Spring Data JPA**, `@Query` allows you to define JPQL or Native SQL directly on the Repository interface method.
*   **JPQL:** `@Query("SELECT u FROM User u WHERE u.email = ?1")`
*   **Native:** `@Query(value = "SELECT * FROM users WHERE email = ?1", nativeQuery = true)`

---

## 286. What is query derivation?

**Answer:**
**Query Derivation** (or Query Creation from Method Names) is a Spring Data JPA feature where the framework automatically generates the SQL based on the method name.
*   **Convention:** `findBy[Property][Condition]`.
*   **Examples:**
    *   `findByEmail(String email)`
    *   `findByAgeGreaterThan(int age)`
    *   `findByLastnameAndFirstname`

---

## 287. What is pagination?

**Answer:**
**Pagination** allows fetching large datasets in chunks (pages) rather than all at once.
*   **Interface:** `Pageable` and `Page<T>`.
*   **Usage:**
    ```java
    Pageable pageable = PageRequest.of(0, 10); // Page 0, Size 10
    Page<User> page = userRepository.findAll(pageable);
    List<User> users = page.getContent();
    ```

---

## 288. What is sorting in JPA?

**Answer:**
Sorting can be achieved via the `Sort` object or directly within `Pageable`.
*   **Usage:**
    ```java
    Sort sort = Sort.by(Sort.Direction.ASC, "lastname");
    List<User> users = userRepository.findAll(sort);
    ```

---

## 289. What is projection?

**Answer:**
**Projection** allows fetching only a **subset of attributes** (selective columns) instead of the entire Entity.
*   **Interface-based:** Define an interface with getter methods for the fields you want.
    ```java
    interface UserSummary {
        String getFirstname();
        String getLastname();
    }
    ```
*   Spring Data JPA automatically implements this interface and populates it.

---

## 290. What is DTO projection?

**Answer:**
**DTO (Data Transfer Object) Projection** maps the query result directly to a DTO class.
*   **Constructor Expression:** Used in JPQL.
    ```java
    @Query("SELECT new com.example.dto.UserDTO(u.firstname, u.lastname) FROM User u")
    List<UserDTO> findAllUserDTOs();
    ```
*   **Benefit:** Optimized read performance (fetches fewer columns) and decouples API response from DB Entity.

---

## 291. What is @Transactional propagation?

**Answer:**
**Propagation** defines how a business method relates to existing transactions.
*   **Definition:** "If a transaction exists, what should I do? If not, what should I do?"
*   **Usage:** `@Transactional(propagation = Propagation.REQUIRED)`.

---

## 292. Propagation types?

**Answer:**
1.  **REQUIRED (Default):** Use existing transaction if available, else create a new one.
2.  **REQUIRES_NEW:** Suspends current transaction and creates a new independent one.
3.  **MANDATORY:** Support current transaction; throw exception if none exists.
4.  **NEVER:** Throw exception if a transaction exists.
5.  **SUPPORTS:** Execute non-transactionally if none exists; else use existing.
6.  **NOT_SUPPORTED:** Suspend current transaction and execute non-transactionally.
7.  **NESTED:** Executes within a nested transaction (savepoint) if a current transaction exists.

---

## 293. Isolation levels?

**Answer:**
Isolation defines how one transaction sees the changes made by other concurrent transactions.
1.  **READ_UNCOMMITTED:** Dirty reads allowed (lowest isolation).
2.  **READ_COMMITTED:** Dirty reads prevented. Non-repeatable reads possible (Default for Postgres, SQL Server, Oracle).
3.  **REPEATABLE_READ:** Non-repeatable reads prevented. Phantom reads possible (Default for MySQL).
4.  **SERIALIZABLE:** Strongest. Transactions run sequentially (no concurrency side effects).

---

## 294. What is optimistic locking?

**Answer:**
**Optimistic Locking** assumes conflicts are rare. It prevents lost updates without database locks.
*   **Mechanism:** Adds a `@Version` field (number/timestamp) to the entity.
*   **Update:**
    *   Read entity (version = 1).
    *   Update entity.
    *   Save: `UPDATE table SET ..., version = 2 WHERE id = 1 AND version = 1`.
    *   If 0 rows updated (version changed by someone else), throw `OptimisticLockException`.

---

## 295. What is pessimistic locking?

**Answer:**
**Pessimistic Locking** assumes conflicts are likely. It locks the database row when reading data.
*   **Mechanism:** `SELECT ... FOR UPDATE`.
*   **Types:**
    *   `PESSIMISTIC_READ`: Shared lock.
    *   `PESSIMISTIC_WRITE`: Exclusive lock.
*   **Usage:** `entityManager.find(User.class, 1L, LockModeType.PESSIMISTIC_WRITE)`.

---

## 296. What is @Version?

**Answer:**
**@Version** is used to enable **Optimistic Locking** for an entity.
*   **Field types:** `int`, `Integer`, `short`, `Short`, `long`, `Long`, `Timestamp`.
*   **Automatic:** JPA provider automatically manages this field. You should **not** set it manually.

---

## 297. What is transaction rollback rules?

**Answer:**
By default, Spring rolls back a transaction only for **Unchecked Exceptions** (`RuntimeException` and `Error`).
*   **Checked Exceptions:** It commits even if a checked rules exception is thrown (`SQLException`, `IOException`).
*   **Customization:**
    *   `@Transactional(rollbackFor = Exception.class)` (Rollback for all).
    *   `@Transactional(noRollbackFor = SpecificException.class)`.

---

## 298. What is readOnly transaction?

**Answer:**
`@Transactional(readOnly = true)` is a hint to the transaction manager that the transaction will only read data.
*   **Optimizations:**
    *   **Hibernate:** Disables dirty checking (performance boost).
    *   **Database:** May omit locking or use a read replica.
*   **Safety:** Writing data typically fails (depending on implementation).

---

## 299. What is Open Session in View?

**Answer:**
**Open Session In View (OSIV)** is a pattern (enabled by default in Spring Boot) that keeps the Hibernate `Session` open until the view is rendered.
*   **Pro:** Prevents `LazyInitializationException` in the Controller/View layer.
*   **Con:** Keeps database connection held for longer (during view rendering). Can cause performance issues under load.
*   **Best Practice:** Disable it (`spring.jpa.open-in-view=false`) and use DTOs/Join Fetch in the Service layer.

---

## 300. How to improve JPA performance?

**Answer:**
1.  **Solve N+1:** Use `JOIN FETCH` or `@EntityGraph`.
2.  **Lazy Loading:** Prefer `Lazy` fetch type over `Eager`.
3.  **Projections:** Fetch only needed columns (DTOs).
4.  **Read-Only:** Use `@Transactional(readOnly = true)`.
5.  **Batching:** Enable JDBC batching (`spring.jpa.properties.hibernate.jdbc.batch_size=30`).
6.  **Caching:** Use 2nd Level Cache (EhCache, Redis) for read-heavy data.
7.  **Connection Pooling:** Use HikariCP (default in Boot).

---

## 301. Second-level cache?

**Answer:**
**Second-Level Cache (L2 Cache)** is a session factory-level cache shared across all sessions/transactions.
*   **Scope:** Application-wide.
*   **Providers:** EhCache, Hazelcast, Infinispan, Redis.
*   **Usage:** Used for data that is read frequently but modified rarely (e.g., Reference Data, Product Catalog).
*   **Config:** Enabled via `spring.jpa.properties.hibernate.cache.use_second_level_cache=true` along with `@Cacheable` entities.

---

## 302. Query cache?

**Answer:**
**Query Cache** stores the **results of a query** (List of IDs) based on the query string and parameters.
*   **Dependency:** Requires L2 Cache to be enabled.
*   **Mechanism:**
    1.  Query executes -> returns IDs.
    2.  Hibernate looks up entities by ID in L2 Cache.
*   **Warning:** Can be harmful if the underlying tables are updated frequently (invalidates the cache often).

---

## 303. What is Hibernate interceptor?

**Answer:**
**Interceptor** allows the application to inspect and/or manipulate properties of a persistent object before it is saved, updated, deleted, or loaded.
*   **Interface:** `org.hibernate.Interceptor`.
*   **Methods:** `onSave`, `onFlushDirty`, `onDelete`.
*   **Use Case:** Auditing (setting `created_by`, `updated_at`), Logging, Multi-tenancy filters.

---

## 304. What is event listener?

**Answer:**
The Hibernate **Event System** is a more granular alternative to Interceptors.
*   **Mechanism:** You can register listeners for specific events (e.g., `PostInsertEvent`, `PreUpdateEvent`).
*   **Benefit:** Access to the `Event` object containing detailed context.
*   **Spring:** Spring Data simplifies this with `@EntityListeners` (e.g., `AuditingEntityListener`).

---

## 305. What is batch fetching?

**Answer:**
**Batch Fetching** is an optimization strategy to solve the N+1 problem by fetching multiple initialized proxies in a single query.
*   **Annotation:** `@BatchSize(size = 10)`.
*   **Scenario:** If you iterate over a list of 10 users and access their lazy-loaded `orders`, Hibernate will execute 1 query to fetch orders for *all 10 users* (using `WHERE user_id IN (?, ?, ...)`), instead of 10 separate queries.

---

## 306. What is stateless session?

**Answer:**
**StatelessSession** is a command-oriented API that does **not** keep a persistence context (first-level cache).
*   **Behavior:** No write-behind, no dirty checking, no cascading. Changes are immediate.
*   **Use Case:** Bulk data operations (Import/Export) where you want to avoid OutOfMemoryErrors caused by a massive First-Level Cache.

---

## 307. What is fetch join?

**Answer:**
`JOIN FETCH` is a JPQL/HQL syntax to eagerly load associated entities in a single query.
*   **Syntax:**
    ```sql
    SELECT u FROM User u JOIN FETCH u.department
    ```
*   **Effect:** Overrides the `FetchType.LAZY` setting for that specific query, ensuring the associated `department` is initialized.

---

## 308. What is entity graph?

**Answer:**
**Entity Graph** is a JPA standard for defining a graph of entities to be fetched.
*   **Role:** Acts as a dynamic "Fetch Plan".
*   **Usage:**
    ```java
    @EntityGraph(attributePaths = {"orders", "orders.items"})
    User findWithOrdersByEmail(String email);
    ```
*   **Result:** Generates a single SQL query with necessary JOINs.

---

## 309. What is multi-tenancy?

**Answer:**
**Multi-tenancy** is an architecture where a single instance of software runs on a server and serves multiple organizations (tenants).
*   **Strategies in Hibernate:**
    1.  **Separate Database:** One DB per tenant (safest).
    2.  **Separate Schema:** One Schema per tenant (shared DB).
    3.  **Discriminator Column:** Shared table with a `tenant_id` column (cheapest, strictly logic-based separation).

---

## 310. How to handle large datasets efficiently?

**Answer:**
1.  **Use Pagination:** Never fetch `findAll()`.
2.  **StatelessSession:** Bypass the first-level cache overhead.
3.  **DTOs:** Read-only DTOs are faster than managed Entities.
4.  **ScrollableResults:** Stream results from the DB cursor instead of loading all into memory.
5.  **Bulk Operations:** Use JPQL `UPDATE`/`DELETE` (`em.createQuery("UPDATE...").executeUpdate()`) instead of modifying entities one by one.

---

## 311. What is microservices architecture?

**Answer:**
**Microservices Architecture** is an architectural style that structures an application as a collection of loose coupled services.
*   **Characteristics:**
    *   Highly maintainable and testable.
    *   Loosely coupled.
    *   Independently deployable.
    *   Organized around business capabilities.
    *   Owned by a small team.

---

## 312. Microservices vs monolith?

**Answer:**

| Feature | Monolith | Microservices |
| :--- | :--- | :--- |
| **Structure** | Single codebase, single deployment unit (WAR/JAR). | Multiple codebases, multiple deployment units. |
| **Scaling** | Scale the entire app (duplicate the whole server). | Scale individual services (only the busy ones). |
| **Complexity** | Simple to develop initially, hard to maintain as it grows. | Complex to manage (distributed system fallacies), easier to maintain per service. |
| **Technology** | Bound to one technology stack. | Polgyglot (can use different tech for different services). |

---

## 313. Advantages & disadvantages of microservices?

**Answer:**
*   **Advantages:**
    *   **Agility:** Faster deployment cycles.
    *   **Scalability:** Targeted scaling.
    *   **Resilience:** Failure in one service doesn't crash the whole system.
    *   **Freedom:** Freedom to choose technology.
*   **Disadvantages:**
    *   **Complexity:** Distributed systems are hard (Network latency, consistency, distributed transactions).
    *   **Operational Overhead:** Needs robust DevOps/Infrastructure (Docker, K8s).
    *   **Testing:** End-to-end testing is harder.

---

## 314. What is service discovery?

**Answer:**
**Service Discovery** is a mechanism that allows services to find each other dynamically without hardcoding IP addresses and ports.
*   **Problem:** In cloud environments, IP addresses change frequently (dynamic scaling).
*   **Solution:** Services register themselves with a "Registry" (Server). Clients ask the Registry for the address of a service.
*   **Tools:** Netflix Eureka, Consul, Zookeeper, Kubernetes (built-in).

---

## 315. What is Eureka?

**Answer:**
**Netflix Eureka** is a Service Registry (Discovery Server) from the Spring Cloud Netflix stack.
*   **Eureka Server:** The central registry where all services register.
*   **Eureka Client:** The microservices that register with the server and fetch the registry to find other services.
*   **Heartbeat:** Clients send heartbeats every 30s to renew their lease. If missing, they are evicted.

---

## 316. What is API Gateway?

**Answer:**
An **API Gateway** is a server that acts as a single entry point into the system.
*   **Role:** It routes requests to the appropriate backend microservice.
*   **Features:**
    *   **Routing:** (e.g., `/user/**` -> User Service).
    *   **Security:** Authentication/Authorization (OAuth2).
    *   **Rate Limiting:** Prevent abuse.
    *   **Monitoring/Logging:** Centralized traffic analysis.

---

## 317. What is Spring Cloud Gateway?

**Answer:**
**Spring Cloud Gateway** is the modern API Gateway built on Spring 5, Spring Boot 2, and Project Reactor (Non-blocking).
*   **Successor:** It replaced Netflix Zuul (Blocking).
*   **Components:**
    *   **Route:** Destination URI + Predicates.
    *   **Predicate:** Matches request (e.g., Path=/api/**, Header=X).
    *   **Filter:** Modifies request/response (e.g., AddHeader, StripPrefix).

---

## 318. What is load balancing?

**Answer:**
**Load Balancing** distributes incoming network traffic across multiple servers (instances of a microservice) to ensure no single server is overwhelmed.
*   **Server-Side LB:** Hardware/Nginx receives traffic and distributes it.
*   **Client-Side LB:** The **Client** (Microservice A) knows the list of available instances of Service B (from Discovery Service) and picks one itself.
    *   **Tool:** **Spring Cloud LoadBalancer** (Replaced Netflix Ribbon).

---

## 319. What is circuit breaker?

**Answer:**
**Circuit Breaker** is a pattern to prevent cascading failures.
*   **Concept:** If a service (Service B) is slow or down, the caller (Service A) should stop calling it ("Trip the circuit") and return a fallback response immediately, instead of waiting for a timeout.
*   **States:**
    *   **Closed:** Requests pass through (Happy path).
    *   **Open:** Requests fail fast (Fallback).
    *   **Half-Open:** Allow a few requests to check if the service recovered.

---

## 320. What is Resilience4j?

**Answer:**
**Resilience4j** is a lightweight fault tolerance library designed for Java 8 and functional programming.
*   **Successor:** It replaced Netflix Hystrix (Deprecated).
*   **Modules:**
    *   **CircuitBreaker:** Stop calls to failing services.
    *   **RateLimiter:** Limit number of requests.
    *   **Retry:** Automatic retries for transient failures.
    *   **Bulkhead:** Limit concurrent calls to a specific service.
    *   **TimeLimiter:** Timeout limits.

---

## 321. What is distributed configuration?

**Answer:**
**Distributed Configuration** is the practice of managing configuration properties (DB URLs, credentials, feature flags) for all microservices in a centralized place, rather than hardcoding them in each service's `application.properties`.
*   **Benefit:** Change configuration without redeploying the service.
*   **Security:** Secrets can be encrypted.

---

## 322. What is Spring Cloud Config?

**Answer:**
**Spring Cloud Config** provides server-side and client-side support for externalized configuration in a distributed system.
*   **Config Server:** A central place to manage external properties for applications across all environments. It usually builds on top of a **Git** repository.
*   **Config Client:** Microservices that connect to the Config Server on startup to fetch their configuration.

---

## 323. What is centralized logging?

**Answer:**
**Centralized Logging** aggregates logs from all microservices into a single location for searching and analysis.
*   **Problem:** In microservices, checking logs on 50 different servers via SSH is impossible.
*   **Stack:** **ELK Stack** (Elasticsearch, Logstash, Kibana) or **EFK Stack** (Elasticsearch, Fluentd, Kibana).

---

## 324. What is distributed tracing?

**Answer:**
**Distributed Tracing** is a method used to profile and monitor applications, especially those built using a microservices architecture.
*   **Goal:** To track a single request as it propagates across multiple services.
*   **Key Concepts:**
    *   **Trace ID:** Unique ID for the whole workflow.
    *   **Span ID:** Unique ID for a specific operation within a service.

---

## 325. What is Zipkin?

**Answer:**
**Zipkin** is a distributed tracing system.
*   **Purpose:** It helps gather timing data needed to troubleshoot latency problems in service architectures.
*   **UI:** Provides a dashboard to visualize the dependency graph and the timeline of a request trace.

---

## 326. What is Sleuth?

**Answer:**
**Spring Cloud Sleuth** implements a distributed tracing solution for Spring Cloud.
*   **Role:** It automatically adds **Trace ID** and **Span ID** to your logs (SLF4J/MDC).
*   **Integration:** It integrates with Zipkin to send traces for visualization.
*   **Note:** In Spring Boot 3, Sleuth is replaced by **Micrometer Tracing**.

---

## 327. What is observability?

**Answer:**
**Observability** is the measure of how well you can understand the internal states of a system from its external outputs.
*   **Three Pillars:**
    1.  **Logs:** (Discrete events) "What happened?"
    2.  **Metrics:** (Aggregatable data) "Is it healthy? What is the trend?" (Prometheus/Grafana).
    3.  **Traces:** (Request flow) "Where did it happen? How long did it take?"

---

## 328. What is health check?

**Answer:**
A **Health Check** is an endpoint (e.g., `/actuator/health`) that monitoring systems or load balancers ping to determine if an application instance is running and able to accept traffic.
*   **Status:** UP, DOWN, OUT_OF_SERVICE.

---

## 329. What is liveness vs readiness probe?

**Answer:**
Concepts used in **Kubernetes**:
*   **Liveness Probe:** "Is the container running?"
    *   If fails: Kubernetes **restarts** the container (assumes deadlock).
*   **Readiness Probe:** "Is the container ready to accept traffic?"
    *   If fails: Kubernetes **stops sending traffic** to this pod (removes from Load Balancer) until it passes. Usage: Waiting for DB connection or cache warming.

---

## 330. What is container orchestration?

**Answer:**
**Container Orchestration** automates the deployment, management, scaling, and networking of containers.
*   **Tool:** **Kubernetes (K8s)** is the industry standard.
*   **Responsibilities:**
    *   Provisioning and deployment.
    *   Scaling (up and down).
    *   Load balancing.
    *   Self-healing (restarting failed containers).

---

## 331. What is Saga pattern?

**Answer:**
**Saga Pattern** is a failure management pattern for distributed transactions.
*   **Problem:** ACID transactions don't span across multiple microservices (2PC is slow/complex).
*   **Solution:** A sequence of local transactions. Each local transaction updates the DB and publishes a message/event to trigger the next transaction.
*   **Compensation:** If a step fails, the Saga executes **compensating transactions** (undo operations) to reverse the changes made by previous steps.

---

## 332. Orchestration vs choreography?

**Answer:**
Two ways to implement Saga:
*   **Choreography (Decentralized):** Services exchange events without a central coordinator. Service A says "Order Created", Service B listens and does "Reserve Stock".
    *   *Pro:* Simple, loose coupling. *Con:* Hard to track complex flows.
*   **Orchestration (Centralized):** A central Orchestrator (service) tells participants what to do.
    *   *Pro:* Easy to manage/visualize. *Con:* Single point of failure/logic concentration.

---

## 333. What is eventual consistency?

**Answer:**
**Eventual Consistency** is a consistency model used in distributed systems (AP in CAP theorem).
*   **Concept:** Data is not immediately consistent across all nodes/services.
*   **Guarantee:** If no new updates are made, eventually all accesses will return the last updated value.
*   **Trade-off:** We accept temporary inconsistency for higher availability and partition tolerance.

---

## 334. What is idempotency?

**Answer:**
**Idempotency** means that making multiple identical requests has the same effect as making a single request.
*   **Context:** Crucial in microservices (retries due to network failure).
*   **Example:** `DELETE /user/1` is idempotent (result is "user deleted" whether called 1 or 10 times). `POST /user` is **not** idempotent (creates 10 users).
*   **Solution:** Use unique request IDs to de-duplicate operations.

---

## 335. What is API versioning?

**Answer:**
**API Versioning** allows you to alter the API logic/structure without breaking existing clients.
*   **Strategies:**
    1.  **URI Versioning:** `/api/v1/users` (Most common, clear).
    2.  **Header Versioning:** `Accept-Version: v1` (Clean URL, harder to test in browser).
    3.  **Media Type Versioning:** `Accept: application/vnd.company.v1+json`.

---

## 336. What is blue-green deployment?

**Answer:**
**Blue-Green Deployment** is a release strategy to reduce downtime and risk.
*   **Setup:** Two identical environments (Blue = Live, Green = Idle/Staging).
*   **Process:** Deploy new version to Green. Test it.
*   **Switch:** Switch the Load Balancer/Router to point traffic from Blue to Green.
*   **Rollback:** Switch back to Blue instantly if issues arise.

---

## 337. What is canary release?

**Answer:**
**Canary Release** is a technique to reduce the risk of introducing a new software version in production.
*   **Process:** Roll out the change to a **small subset of users** (e.g., 5%) first.
*   **Monitor:** Watch metrics (errors, latency).
*   **Propagate:** If successful, gradually increase traffic to 100%.

---

## 338. What is service mesh?

**Answer:**
**Service Mesh** is a dedicated infrastructure layer for handling service-to-service communication.
*   **Tool:** **Istio**, **Linkerd**.
*   **Features:** Traffic management, Security (mTLS), Observability (Tracing).
*   **Implementation:** Usually implemented as a lightweight network proxy (**Sidecar**) deployed alongside the application code.

---

## 339. What is sidecar pattern?

**Answer:**
**Sidecar Pattern** deploys components of an application into a separate process or container (Sidecar) to provide isolation and encapsulation.
*   **Analogy:** A motorcycle sidecar attached to the main bike.
*   **Usage:** Logging agents, Configuration proxies (Envoy), Service Mesh proxies. The main app focuses on business logic; the sidecar handles infrastructure concerns.

---

## 340. How do you secure microservices?

**Answer:**
**Security** in microservices involves multiple layers:
1.  **Edge Security:** API Gateway handles Authentication (OAuth2/OIDC) and acts as the entry point.
2.  **Service-to-Service:**
    *   **mTLS (Mutual TLS):** Encrypts traffic and verifies identity (Service Mesh).
    *   **Token Relay:** Pass the JWT token from the Gateway downstream to other services.
3.  **Network:** Private VPCs, firewalls.

---

## 341. How to handle distributed transactions?

**Answer:**
Handling distributed transactions (transactions spanning multiple services/DBs) is complex. Common strategies:
1.  **Saga Pattern (Preferred):** Sequence of local transactions with compensating actions.
2.  **Two-Phase Commit (2PC):** Strict consistency but poor performance/availability.
3.  **Eventual Consistency:** Accept that data might be out of sync for a few milliseconds, reconciling later via background processes.

---

## 342. What is 2PC?

**Answer:**
**Two-Phase Commit (2PC)** is a protocol for distributed transactions.
*   **Phase 1 (Prepare):** Identify a Coordinator. The Coordinator asks all participants: "Can you commit?". Participants lock resources and vote "Yes" or "No".
*   **Phase 2 (Commit/Rollback):**
    *   If all vote "Yes": Coordinator sends "Commit".
    *   If any vote "No": Coordinator sends "Rollback".

---

## 343. Why avoid 2PC in microservices?

**Answer:**
*   **Blocking:** It is a blocking protocol. If the Coordinator crashes during Phase 2, resources remain locked indefinitely.
*   **Performance:** High latency due to multiple round-trips and locking.
*   **Coupling:** Tightly couples services (they all must be up).
*   **CAP Theorem:** It favors Consistency over Availability, which contradicts the goal of highly available microservices.

---

## 344. What is bulkhead pattern?

**Answer:**
**Bulkhead Pattern** isolates elements of an application into pools so that if one fails, the others continue to function.
*   **Analogy:** A ship's hull is divided into bulkheads. If one section floods, the ship doesn't sink.
*   **Implementation:** Separate thread pools for different downstream services. If Service A is slow and exhausts its thread pool, Service B's thread pool remains unaffected.

---

## 345. What is retry pattern?

**Answer:**
**Retry Pattern** automatically retries a failed operation (hoping the failure was transient/temporary).
*   **Config:**
    *   **Max Attempts:** How many times to retry (e.g., 3).
    *   **Backoff:** How long to wait between retries (e.g., Fixed 1s, or Exponential).
*   **Caution:** Only retry **idempotent** operations. Avoid "Retry Storms" (DDoS-ing your own services).

---

## 346. What is timeout handling?

**Answer:**
**Timeout Handling** ensures that a request doesn't wait forever for a response.
*   **Reason:** Prevent threads from being blocked indefinitely by a slow dependency.
*   **Practice:** Always set a timeout (e.g., 2 seconds) for any external call (DB, HTTP). If the timeout is reached, abort and return a fast failure or fallback.

---

## 347. What is rate limiting?

**Answer:**
**Rate Limiting** controls the rate of traffic sent or received by a network interface controller.
*   **Purpose:** Protect services from being overwhelmed (DoS protection, fair usage policy).
*   **Algorithms:** Token Bucket, Leaky Bucket, Fixed Window.
*   **Tools:** Redis (distributed counter), Resilience4j, API Gateway.

---

## 348. How to handle database per service?

**Answer:**
**Database per Service** is a core microservice pattern where each service has its *own* private database.
*   **Challenge:** Joining data across services.
*   **Solution:**
    *   **API Composition:** Calls Service A and Service B, then combines results in memory (API Gateway/BFF).
    *   **Data Replication (CQRS):** Service A publishes an event on update; Service B consumes it and updates a read-only local copy of A's data.

---

## 349. How to manage inter-service communication?

**Answer:**
1.  **Synchronous (REST/gRPC):** Simple, real-time query. Good for "Read" operations. Tightly coupled.
2.  **Asynchronous (Messaging - RabbitMQ/Kafka):** Decoupled, eventual consistency. Good for "Write" operations (e.g., "Order Placed" event).
3.  **Hybrid:** Use Sync for queries and Async for updates.

---

## 350. Common production issues in microservices?

**Answer:**
1.  **Network Latency:** Too many "chatty" calls.
2.  **Distributed Traceability:** Hard to debug issues spanning 5 services (needs Zipkin).
3.  **Configuration Drift:** Environments going out of sync (needs Spring Cloud Config).
4.  **Cascading Failures:** One service crashing causes others to crash (needs Circuit Breakers).
5.  **Data Consistency:** Maintaining integrity across databases.

---

## 351. What is REST?

**Answer:**
**REST (Representational State Transfer)** is an architectural style for designing networked applications.
*   **Key Principles:**
    1.  **Client-Server:** Decoupled UI and data storage.
    2.  **Stateless:** No session data on server; every request must contain all info.
    3.  **Cacheable:** Responses must define themselves as cacheable or not.
    4.  **Uniform Interface:** Resources identified by URLs, manipulated by HTTP methods.
    5.  **Layered System:** Client doesn't know if it's connected to end server or load balancer.

---

## 352. REST vs SOAP?

**Answer:**

| Feature | REST | SOAP |
| :--- | :--- | :--- |
| **Protocol** | Architectural Style (uses HTTP). | Protocol. |
| **Format** | JSON, XML, Plain Text, HTML. | XML only. |
| **Performance** | Lightweight (JSON), caching support. | Heavyweight (XML envelope, parsing). |
| **Security** | HTTPS, OAuth2. | WS-Security (Built-in). |
| **Usage** | Web APIs, Mobile apps. | Enterprise, Banking, Legacy systems. |

---

## 353. What are HTTP methods?

**Answer:**
Common HTTP verbs used in REST:
1.  **GET:** Retrieve a resource (Safe, Cacheable).
2.  **POST:** Create a new resource (Not Idempotent).
3.  **PUT:** Update/Replace a resource (Idempotent).
4.  **PATCH:** Partial update of a resource.
5.  **DELETE:** Remove a resource (Idempotent).

---

## 354. What is idempotent method?

**Answer:**
An **Idempotent** HTTP method is one that can be called multiple times without changing the result beyond the initial application.
*   **Idempotent:** `GET`, `PUT`, `DELETE`, `HEAD`, `OPTIONS`.
    *   `DELETE /user/1`: First call deletes it. Second call returns 404 (or 200), but the server state (user is gone) remains the same.
*   **Not Idempotent:** `POST`.
    *   `POST /user`: Calling it twice creates two users.

---

## 355. What are HTTP status codes?

**Answer:**
*   **2xx (Success):**
    *   `200 OK`: Success.
    *   `201 Created`: Resource created (POST).
    *   `204 No Content`: Success but no body (DELETE/PUT).
*   **4xx (Client Error):**
    *   `400 Bad Request`: Invalid input.
    *   `401 Unauthorized`: Authentication missing.
    *   `403 Forbidden`: Authorization missing (Role).
    *   `404 Not Found`: Resource doesn't exist.
    *   `405 Method Not Allowed`: Wrong HTTP verb.
*   **5xx (Server Error):**
    *   `500 Internal Server Error`: Bug/Exception.
    *   `503 Service Unavailable`: Server overloaded/down.

---

## 356. What is statelessness?

**Answer:**
**Statelessness** means the server does **not** store any client context (Session) between requests.
*   **Mechanism:** Every request from the client must contain all the information necessary to understand and process the request (e.g., Auth Token in header).
*   **Benefit:** Allows the server to scale horizontally easily (any server can handle any request).

---

## 357. What is HATEOAS?

**Answer:**
**HATEOAS (Hypermedia As The Engine Of Application State)** is a constraint of REST.
*   **Concept:** The API response should include **links** to related actions/resources, guiding the client on "what to do next".
*   **Example:**
    ```json
    {
      "id": 1,
      "name": "John",
      "_links": {
        "self": { "href": "/users/1" },
        "orders": { "href": "/users/1/orders" }
      }
    }
    ```

---

## 358. What is content negotiation?

**Answer:**
**Content Negotiation** is the mechanism used for serving different representations of a resource at the same URI, so that the user agent can specify which is best suited for the user.
*   **Headers:**
    *   `Accept`: Client tells Server what format it wants (e.g., `application/json` or `application/xml`).
    *   `Content-Type`: Client tells Server what format it is sending.

---

## 359. What is API versioning strategies?

**Answer:**
Since APIs evolve, versioning is crucial to avoid breaking changes.
1.  **URI Versioning:** `/api/v1/products` (Easiest to read/cache).
2.  **Request Param:** `/api/products?version=1` (Avoids valid URI pollution).
3.  **Header Versioning:** `X-API-VERSION: 1` (Keeps URL clean).
4.  **Media Type (Content Negotiation):** `Accept: application/vnd.myapi.v1+json`.

---

## 360. What is OpenAPI/Swagger?

**Answer:**
**OpenAPI Specification (OAS)** is a standard for documenting REST APIs. **Swagger** is a set of tools implementing OAS.
*   **Purpose:**
    1.  **Documentation:** Generates interactive UI (`/swagger-ui.html`) to test endpoints.
    2.  **Code Gen:** Generate client SDKs from the YAML/JSON spec.
*   **Spring Boot:** Use `springdoc-openapi` library to automatically generate docs from code annotations.

---

## 361. What is synchronous communication?

**Answer:**
**Synchronous Communication** is when the client sends a request and **waits** (blocks) for the response from the service.
*   **Protocol:** HTTP/REST, gRPC.
*   **Pros:** Simple to understand, real-time consistency.
*   **Cons:** Blocking (resource waste), cascading failures if downstream is slow, tight coupling.

---

## 362. What is asynchronous communication?

**Answer:**
**Asynchronous Communication** is when the client sends a message and **does not wait** for an immediate response.
*   **Protocol:** AMQP (RabbitMQ), Kafka.
*   **Pros:** Non-blocking, decoupled, handles spikes (buffering), better resilience.
*   **Cons:** Complexity (eventual consistency), harder to debug.

---

## 363. REST vs gRPC?

**Answer:**

| Feature | REST | gRPC |
| :--- | :--- | :--- |
| **Protocol** | HTTP/1.1 (mostly). | HTTP/2 (Binary). |
| **Format** | JSON (Text). | Protocol Buffers (Binary). |
| **Performance** | Slower (parsing text). | Faster (compact binary, multiplexing). |
| **Streaming** | Limited (Server-Sent Events). | Full support (Bi-directional streaming). |
| **Usage** | Public APIs (Browser compatible). | Internal Microservices communication. |

---

## 364. What is Feign Client?

**Answer:**
**Spring Cloud OpenFeign** is a declarative REST client.
*   **How:** You define an interface and annotate it with `@FeignClient`. Spring generates the implementation at runtime.
*   **Benefit:** Removes boilerplate code required when using `RestTemplate`.
*   **Integration:** Integrates with Eureka (Load Balancing) and Resilience4j (Circuit Breaker).

---

## 365. What is RestTemplate?

**Answer:**
**RestTemplate** is a synchronous client to perform HTTP requests in Spring.
*   **Status:** In maintenance mode (deprecated features).
*   **Usage:**
    ```java
    String result = restTemplate.getForObject("http://user-service/users/1", String.class);
    ```

---

## 366. What is WebClient?

**Answer:**
**WebClient** is a reactive, non-blocking HTTP client introduced in Spring WebFlux.
*   **Features:** Supports both Sync and Async operations.
*   **Future:** It is the recommended replacement for `RestTemplate`.
*   **Usage:**
    ```java
    Mono<String> result = webClient.get().uri("/users/1").retrieve().bodyToMono(String.class);
    ```

---

## 367. What is connection timeout vs read timeout?

**Answer:**
*   **Connection Timeout:** The time limit to **establish a connection** (TCP handshake) with the server. If server is down/unreachable, this triggers.
*   **Read Timeout:** The time limit to **receive data** (the response) after the connection is established. If server is slow processing, this triggers.

---

## 368. What is retry mechanism?

**Answer:**
A **Retry Mechanism** re-executes a failed request automatically.
*   **Policies:**
    *   **Simple:** Retry 3 times.
    *   **Backoff:** Wait 1s, then 2s, then 4s (Exponential).
    *   **Jitter:** Add random delay to prevent "thundering herd" problem.
*   **Tools:** Spring Retry, Resilience4j.

---

## 369. What is idempotency key?

**Answer:**
An **Idempotency Key** is a unique value (UUID) sent in the HTTP Header (`Idempotency-Key`) by the client to ensure idempotency for non-idempotent operations (like POST).
*   **Flow:**
    1.  Client POSTs with `Key: 123`.
    2.  Server processes and saves result mapped to `123`.
    3.  Network fails. Client retries POST with `Key: 123`.
    4.  Server sees `123` is already processed. Returns cached result instead of creating duplicate.

---

## 370. What are common REST best practices?

**Answer:**
1.  **Nouns for Resources:** Use `/users`, not `/getUsers`.
2.  **Plural Nouns:** `/users/1` instead of `/user/1`.
3.  **HTTP Status Codes:** Use correct codes (201 Created, 400 Bad Request) instead of 200 for everything.
4.  **Versioning:** Always version your API (`/v1`).
5.  **Pagination:** Limit result sizes.
6.  **SSL:** Always use HTTPS.

---

## 371. What is messaging system?

**Answer:**
A **Messaging System** allows different software systems to communicate and exchange data (messages) asynchronously.
*   **Role:** Decouples the sender (Producer) from the receiver (Consumer).
*   **Models:**
    1.  **Point-to-Point (Queue):** Message is consumed by exactly one consumer (e.g., RabbitMQ Queue).
    2.  **Publish-Subscribe (Topic):** Message is broadcast to all active subscribers (e.g., Kafka Topic).

---

## 372. Kafka vs RabbitMQ?

**Answer:**

| Feature | Kafka | RabbitMQ |
| :--- | :--- | :--- |
| **Model** | Distributed Streaming Platform (Log-based). | Message Broker (Queue-based). |
| **Throughput** | Extremely High (Millions/sec). | High (Thousands/sec). |
| **Persistence** | Durable (Stores messages for days/weeks). | Transient (Deletes after consumption). |
| **Consumption** | Pull-based (Consumer polls). | Push-based (Broker pushes). |
| **Use Case** | Event sourcing, Stream processing, Logs. | Complex routing, Real-time messaging. |

---

## 373. What is topic in Kafka?

**Answer:**
A **Topic** is a category or feed name to which records are stored and published.
*   **Analogy:** A folder in a filesystem or a table in a database.
*   **Structure:** Topics are partitioned and replicated.
*   **Retention:** Messages are stored for a configurable period (e.g., 7 days) regardless of whether they have been consumed.

---

## 374. What is partition?

**Answer:**
A **Partition** is an ordered, immutable sequence of records that is continually appended to—a structured commit log.
*   **Purpose:** Scalability. A topic can be split into multiple partitions hosted on different brokers.
*   **Ordering:** Guaranteed *within* a partition, but not across the entire topic.

---

## 375. What is offset?

**Answer:**
An **Offset** is a unique sequential integer ID assigned to each record within a partition.
*   **Purpose:** It uniquely identifies a message in a partition.
*   **Consumer Tracking:** Consumers track their progress by storing the offset of the last consumed message.

---

## 376. What is consumer group?

**Answer:**
A **Consumer Group** is a set of consumers that cooperate to consume data from a topic.
*   **Mechanism:** Kafka ensures that each partition is consumed by **exactly one** consumer within the group.
*   **Scaling:** To scale reading, add more consumers to the group (up to the number of partitions).

---

## 377. What is producer acknowledgement?

**Answer:**
**ACKS** (Acknowledgements) determine when the producer considers a request complete.
*   `acks=0`: Producer sends and forgets (Low latency, data loss risk).
*   `acks=1`: Leader receives and writes to local log (Default).
*   `acks=all`: Leader and all ISR (In-Sync Replicas) acknowledge (Highest durability).

---

## 378. What is ISR?

**Answer:**
**ISR (In-Sync Replica)** is a set of replica brokers that are caught up with the leader partition.
*   **Role:** Only members of the ISR are eligible to be elected as a new leader if the current leader fails.
*   **Lag:** If a replica lags too far behind, it is removed from the ISR.

---

## 379. What is replication factor?

**Answer:**
**Replication Factor** determines how many copies of a partition are stored across the cluster.
*   **Default:** Typically 3 (1 Leader + 2 Followers).
*   **Benefit:** Fault tolerance. If N-1 brokers fail, the data is still available.

---

## 380. What is exactly-once semantics?

**Answer:**
**Exactly-Once Semantics (EOS)** guarantees that each message is delivered and processed exactly once, even in the event of failures.
*   **Kafka:** Achieved using **Idempotent Producer** (`enable.idempotence=true`) and **Transactional API** (atomic write across multi-partitions).
*   **Difficulty:** Standard messaging is usually "At-least-once".

---

## 381. What is Redis?

**Answer:**
**Redis (Remote Dictionary Server)** is an open-source, in-memory data structure store.
*   **Role:** Used as a database, cache, and message broker.
*   **Key Features:**
    *   **In-Memory:** Extremely fast (Sub-millisecond latency).
    *   **Persistence:** Can save data to disk (RDB/AOF).
    *   **Data Structures:** Supports more than just strings (Lists, Sets, Sorted Sets).

---

## 382. What data structures Redis supports?

**Answer:**
Redis is not just a Key-Value store; it supports complex data structures:
1.  **String:** Basic text or binary data (up to 512MB).
2.  **List:** Linked lists of strings (e.g., Queue/Stack).
3.  **Set:** Unordered collection of unique strings.
4.  **Sorted Set (ZSet):** Set ordered by a score (e.g., Leaderboard).
5.  **Hash:** Map of fields and values (like a Java Map).
6.  **Bitmap/HyperLogLog:** For advanced analytics.

---

## 383. What is TTL?

**Answer:**
**TTL (Time To Live)** is a setting that defines how long a key should exist in the cache before it is automatically deleted (expired).
*   **Command:** `EXPIRE key seconds` (e.g., `EXPIRE session:123 60`).
*   **Purpose:** Prevents stale data and frees up memory.

---

## 384. What is cache eviction policy?

**Answer:**
When Redis memory is full, the **Eviction Policy** determines which keys to remove to make space for new data.
*   **Policies:**
    *   `noeviction`: Returns error (Default).
    *   `allkeys-lru`: Evict Least Recently Used keys.
    *   `volatile-lru`: Evict Least Recently Used keys *that have an expiration set*.
    *   `allkeys-lfu`: Evict Least Frequently Used keys.
    *   `allkeys-random`: Random removal.

---

## 385. What is cache aside pattern?

**Answer:**
**Cache Aside (Lazy Loading)** is the most common caching strategy.
1.  **Read:** Application checks Cache.
    *   If **Hit**: Return data.
    *   If **Miss**: Load from DB, write to Cache, return data.
2.  **Write:** Application updates DB, then **invalidates** (deletes) the key in Cache. Next read will re-load fresh data.

---

## 386. What is Write-Through vs Write-Back?

**Answer:**
*   **Write-Through:** Application writes to the Cache and the DB *simultaneously*.
    *   *Pro:* Consistency. *Con:* Slower write latency.
*   **Write-Back (Write-Behind):** Application writes *only* to Cache. The Cache writes to DB asynchronously later.
    *   *Pro:* Fast writes. *Con:* Data loss risk if cache crashes before syncing.

---

## 387. What is Cache Penetration?

**Answer:**
**Cache Penetration** occurs when a client repeatedly requests data that **does not exist** in either the Cache or the DB.
*   **Problem:** Every request hits the DB (bypassing cache), potentially Crashing it.
*   **Solution:**
    *   Cache `null` values (with short TTL).
    *   Use **Bloom Filters** to check if data *might* exist before ensuring DB call.

---

## 388. What is Cache Breakdown?

**Answer:**
**Cache Breakdown (Hot Key Expiration)** happens when a **single hot key** (accessed frequently) expires.
*   **Problem:** Suddenly, thousands of concurrent requests hit the DB simultaneously to reload that one key.
*   **Solution:**
    *   Use Mutex Locks (only 1 thread loads data).
    *   "Logical Expiration": Store expiry time in value, and reload asynchronously before it physically expires.

---

## 389. What is Cache Avalanche?

**Answer:**
**Cache Avalanche** occurs when **many keys expire at the same time** (or Redis crashes).
*   **Problem:** Massive spike in DB load as all keys need reloading.
*   **Solution:**
    *   Add random jitter to TTLs (so they don't all expire at once).
    *   Use Redis Cluster (High Availability).

---

## 390. RDB vs AOF (Redis Persistence)?

**Answer:**
Redis persists in-memory data to disk using two methods:
1.  **RDB (Redis Database):** Periodic "snapshots" of the dataset at intervals (e.g., every 5 mins).
    *   *Pro:* Faster startup, compact. *Con:* Potential data loss of last 5 mins.
2.  **AOF (Append Only File):** Logs every write operation received.
    *   *Pro:* Durable (1s data loss max). *Con:* Larger file size, slower restart.

---

## 391. Redis vs Memcached?

**Answer:**

| Feature | Redis | Memcached |
| :--- | :--- | :--- |
| **Data Types** | Rich (String, List, Set, Hash, etc.). | Simple Key-Value (String only). |
| **Persistence** | Yes (RDB, AOF). | No (In-memory only). |
| **Replication** | Master-Slave replication. | No native replication. |
| **Threads** | Single-threaded. | Multi-threaded. |
| **Use Case** | Complex caching, Message Broker, DB. | Simple, high-throughput string caching. |

---

## 392. What is Redis Sentinel?

**Answer:**
**Redis Sentinel** provides high availability for Redis.
*   **Role:** Monitoring. It checks if Master and Slave instances are working.
*   **Failover:** If the Master goes down, Sentinel automatically promotes a Slave to be the new Master.
*   **Notification:** Alerts system administrators or other applications about the failure.

---

## 393. What is Redis Clustering?

**Answer:**
**Redis Cluster** provides a way to run a Redis installation where data is automatically sharded across multiple Redis nodes.
*   **Sharding:** Data is split into 16,384 "hash slots". Each node holds a subset of these slots.
*   **Scalability:** Allows horizontal scaling (adding more nodes) to handle more data and traffic.
*   **No Central Proxy:** Clients connect directly to any node, which redirects them to the correct node if needed.

---

## 394. What is Pub/Sub in Redis?

**Answer:**
**Publish/Subscribe** is a messaging pattern in Redis.
*   **Mechanism:** Senders (Publishers) send messages to channels, without knowing who will receive them. Receivers (Subscribers) listen to channels.
*   **Ephemeral:** Messages are **fire-and-forget**. If a subscriber is offline, it misses the message (unlike Kafka).
*   **Use Case:** Real-time chat, notifications.

---

## 395. How to implement distributed locking in Redis?

**Answer:**
To ensure only one service instance performs a critical task (e.g., generating a report):
*   **Simple:** `SET lock:report 1 NX EX 10` (Set if Not Exists, Expire in 10s).
*   **Redlock Algorithm:** For distributed Redis (safer).
    1.  Acquire lock in N/2 + 1 nodes.
    2.  Check time elapsed (must be < TTL).

---

## 396. When NOT to use cache?

**Answer:**
1.  **Data changes frequently:** Cache invalidation overhead outweighs read benefits.
2.  **Consistency is critical:** Stale data is unacceptable (e.g., Bank balance).
3.  **Data is rarely read:** No point caching data that is read once a week.
4.  **Complex Queries:** Redis is not a search engine (unless using RediSearch module).

---

## 397. What is Redis Pipelining?

**Answer:**
**Pipelining** allows a client to send multiple commands to the server without waiting for the replies individually.
*   **Benefit:** Reduces RTT (Round Trip Time). Instead of 10 network calls for 10 commands, you do 1 network call.
*   **Throughput:** Massive performance improvement for batch operations.

---

## 398. What is Redis Single-threaded model?

**Answer:**
Redis uses a **single-threaded** event loop (Reactor pattern) to handle file events (requests).
*   **Why fast?** It runs in-memory (no disk I/O blocking) and uses non-blocking I/O multiplexing.
*   **Implication:** Avoid O(N) commands (like `KEYS *`) on large datasets, as they block the entire server for everyone.

---

## 399. What is Geo-spatial data in Redis?

**Answer:**
Redis supports **Geo-spatial** data types (`GEOADD`, `GEORADIUS`).
*   **Function:** Store longitude/latitude pairs.
*   **Query:** "Find all users within 5km of this point" or "Calculate distance between two cities".
*   **Implementation:** Internally uses Sorted Sets (ZSet) with Geohash.

---

## 400. What is a Bloom Filter?

**Answer:**
A **Bloom Filter** is a probabilistic data structure used to test whether an element is a member of a set.
*   **Properties:**
    1.  **False Positive:** Might say "Yes" when element is not there.
    2.  **False Negative:** Never says "No" if element is there (100% accurate on "No").
*   **Use Case:** Rapidly check if a username is taken, or preventing **Cache Penetration** (check bloom filter before DB).

---

## 401. What is normalization?

**Answer:**
**Normalization** is the process of organizing data in a database to avoid data redundancy and modification anomalies (Update, Insertion, Deletion).
*   **Goal:** Divide larger tables into smaller tables and link them using relationships.
*   **Benefit:** Reduces data duplication, ensures data consistency.

---

## 402. Explain 1NF, 2NF, 3NF, BCNF.

**Answer:**
*   **1NF (First Normal Form):** Atomic values. Each cell contains a single value (no comma-separated lists), and each record is unique.
*   **2NF:** 1NF + No Partial Dependency. All non-key attributes must depend on the *entire* Primary Key (not just part of a composite key).
*   **3NF:** 2NF + No Transitive Dependency. Non-key attributes must depend *only* on the Candidate Key (Primary Key), not on other non-key attributes.
*   **BCNF (Boyce-Codd keys Normal Form):** A stricter 3NF. For every functional dependency X -> Y, X must be a superkey.

---

## 403. What is denormalization?

**Answer:**
**Denormalization** is the process of adding redundant data to an already normalized database to improve read performance.
*   **Trade-off:** Faster reads (fewer JOINS) vs Slower writes (update data in multiple places) and higher storage.
*   **Use Case:** Data Warehousing, Reporting.

---

## 404. What is primary key?

**Answer:**
A **Primary Key** is a column (or set of columns) that uniquely identifies each row in a table.
*   **Constraints:** Must be UNIQUE and NOT NULL.
*   **Limit:** Only one Primary Key per table.

---

## 405. What is composite key?

**Answer:**
A **Composite Key** is a Primary Key that consists of two or more columns.
*   **Example:** In a `Student_Course` table, neither `student_id` nor `course_id` is unique alone, but the combination (`student_id`, `course_id`) is unique.

---

## 406. What is foreign key?

**Answer:**
A **Foreign Key** is a column that establishes a link between data in two tables.
*   **Role:** It refers to the Primary Key of another table.
*   **Constraint:** Enforces **Referential Integrity** (cannot have a foreign key value that doesn't exist in the parent table).

---

## 407. What is unique constraint?

**Answer:**
A **Unique Constraint** ensures that all values in a column are distinctive.
*   **Difference from Primary Key:**
    1.  A table can have **multiple** Unique Constraints.
    2.  Unique Constraint columns **can** contain NULL values (usually one NULL allowed per column, depending on DB).

---

## 408. What is indexing?

**Answer:**
**Indexing** is a data structure technique used to quickly locate and access the data in a database table.
*   **Structure:** Usually B-Trees or Hash tables.
*   **Trade-off:** Speeds up `SELECT` queries (WHERE clause) but slows down `INSERT`/`UPDATE` (as index must be updated too).

---

## 409. Types of indexes in MySQL?

**Answer:**
1.  **B-Tree Index:** Default. Good for range queries (`>`, `<`) and equality.
2.  **Hash Index:** Extremely fast for exact lookups (`=`), but no range support.
3.  **Full-text Index:** For text searching.
4.  **Spatial Index (R-Tree):** For geographic data.

---

## 410. What is clustered index?

**Answer:**
*   **Clustered Index:** Defines the physical order of data in the table.
    *   The "Leaf Nodes" contain the **actual data rows**.
    *   **Limit:** Only 1 per table (usually the Primary Key).
*   **Non-Clustered Index:** Stored separately from data.
    *   Leaf nodes contain a pointer to the data row (or Primary Key).
    *   Can have multiple per table.

---

## 411. What is EXPLAIN plan?

**Answer:**
**EXPLAIN** is a keyword in SQL (e.g., MySQL, PostgreSQL) used to analyze how the database executes a query.
*   **Output:** It shows the execution plan: which indexes are used, how tables are joined, and estimated row counts.
*   **Usage:** Crucial for optimizing slow queries.

---

## 412. What is query optimization?

**Answer:**
**Query Optimization** is the process of improving the execution speed of SQL queries.
*   **Techniques:**
    1.  **Indexing:** Ensure `WHERE`, `JOIN`, and `ORDER BY` columns are indexed.
    2.  **Avoid SELECT *:** Retrieve only necessary columns.
    3.  **Analyze EXPLAIN plan:** Identify bottlenecks (e.g., Full Table Scans).
    4.  **Denormalization:** For read-heavy systems.

---

## 413. What is full table scan?

**Answer:**
A **Full Table Scan** occurs when the database reads **every row** in the table to find the desired results.
*   **Cause:** Missing indexes or using functions on indexed columns (e.g., `WHERE YEAR(date_col) = 2023`).
*   **Performance:** Very slow for large tables. Always aim to convert these to **Index Scans**.

---

## 414. What is covering index?

**Answer:**
A **Covering Index** is an index that contains (covers) **all** the columns required by the query (both in `WHERE` and `SELECT` clauses).
*   **Benefit:** The DB can retrieve the data directly from the index structure without looking up the actual table rows (Clustered Index). This is extremely fast.

---

## 415. What is composite index?

**Answer:**
A **Composite Index** is an index on multiple columns (e.g., `INDEX(last_name, first_name)`).
*   **Rule:** **Leftmost Prefix Rule**. The index is effective only if the query uses the leftmost columns.
    *   Query on `last_name` -> Uses Index.
    *   Query on `last_name` AND `first_name` -> Uses Index.
    *   Query on `first_name` -> **Does NOT** use Index.

---

## 416. What is cardinality?

**Answer:**
**Cardinality** refers to the uniqueness of data values in a column.
*   **High Cardinality:** Many unique values (e.g., Email, UUID). **Good for indexing**.
*   **Low Cardinality:** Few unique values (e.g., Gender, Boolean). **Bad for indexing** (DB prefers Full Table Scan).

---

## 417. What is slow query log?

**Answer:**
**Slow Query Log** is a database feature (available in MySQL, Postgres) that records queries taking longer than a specified threshold (e.g., 2 seconds).
*   **Purpose:** Helps identify which queries need optimization.

---

## 418. What is query cache?

**Answer:**
**Query Cache** stores the text of a `SELECT` statement together with the corresponding result used.
*   **Mechanism:** If an identical query is received, the DB serves the result from the cache.
*   **Note:** Deprecated/Removed in MySQL 8.0 because it creates contention locks and is invalidated too frequently.

---

## 419. What is partitioning?

**Answer:**
**Partitioning** splits a large table into smaller, more manageable pieces (partitions), while still treating it as a single logical table.
*   **Types:**
    1.  **Range:** By date (e.g., `orders_2022`, `orders_2023`).
    2.  **List:** By discrete values (e.g., Region: `US`, `EU`).
    3.  **Hash:** Random distribution.

---

## 420. What is sharding?

**Answer:**
**Sharding** is a horizontal scaling strategy where data is distributed across **multiple database servers** (shards).
*   **Difference from Partitioning:** Partitioning is on the *same* server; Sharding is on *different* servers.
*   **Complexity:** Application needs to know which shard to query (e.g., `User ID % 4`). Handling joins across shards is very difficult.

---

## 421. What is ACID?

**Answer:**
**ACID** is a set of properties that guarantee valid database transactions.
1.  **Atomicity:** All or nothing. The transaction either completes entirely or fails entirely (Rollback).
2.  **Consistency:** The DB goes from one valid state to another (constraints respected).
3.  **Isolation:** Concurrent transactions don't interfere with each other.
4.  **Durability:** Once committed, data is permanent (persisted to disk), even if power fails.

---

## 422. What are isolation levels?

**Answer:**
**Isolation Levels** define the degree to which a transaction is isolated from others.
1.  **Read Uncommitted:** Lowest. Allows Dirty Reads.
2.  **Read Committed:** Default in many DBs (Oracle, Postgres). Prevents Dirty Reads.
3.  **Repeatable Read:** Default in MySQL. Prevents Dirty and Non-repeatable Reads.
4.  **Serializable:** Highest. Strict serial execution. Prevents all anomalies but slow.

---

## 423. What is dirty read?

**Answer:**
**Dirty Read** occurs when a transaction reads data that has been modified by another transaction but **not yet committed**.
*   **Risk:** If the other transaction rolls back, the first transaction has read invalid data.

---

## 424. What is non-repeatable read?

**Answer:**
**Non-Repeatable Read** occurs when a transaction reads the **same row twice** and gets different values.
*   **Cause:** Another transaction modified or deleted that row and committed in between the two reads.

---

## 425. What is phantom read?

**Answer:**
**Phantom Read** occurs when a transaction reads a set of rows satisfying a condition (e.g., `WHERE age > 10`) twice and gets a **different number of rows**.
*   **Cause:** Another transaction **inserted** or **deleted** rows that match the condition in between the reads.

---

## 426. What is MVCC?

**Answer:**
**MVCC (Multi-Version Concurrency Control)** is a method used by databases (Postgres, MySQL/InnoDB) to handle concurrency without locking the entire database.
*   **Mechanism:** It keeps multiple versions of the data. Readers read an older version ("snapshot") while writers create a new version.
*   **Benefit:** **Readers don't block Writers**, and Writers don't block Readers.

---

## 427. What is row-level locking?

**Answer:**
**Row-Level Locking** locks only the specific rows being accessed or modified by a transaction.
*   **Pro:** High concurrency (many users can edit different rows in the same table).
*   **Con:** High memory overhead (managing millions of locks).

---

## 428. What is table-level locking?

**Answer:**
**Table-Level Locking** locks the entire table.
*   **Pro:** Low overhead (just 1 lock). Fast for bulk updates.
*   **Con:** Poor concurrency (only 1 user can write to the table at a time).

---

## 429. What is deadlock in DB?

**Answer:**
A **Deadlock** happens when two or more transactions are waiting for each other to give up locks.
*   **Scenario:**
    *   Tx1 holds Lock A, waits for Lock B.
    *   Tx2 holds Lock B, waits for Lock A.
*   **Result:** Neither can proceed. The DB eventually kills one transaction to break the cycle.

---

## 430. How to prevent DB deadlocks?

**Answer:**
1.  **Consistent Order:** Always access resources (tables/rows) in the same order in all transactions.
2.  **Keep Tx Short:** Reduce the time locks are held.
3.  **Lock Escalation:** Lock the parent (e.g., Table) if modifying many children rows to avoid row-lock limit.
4.  **Timeouts:** Configure lock wait timeouts.

---

## 431. Vertical vs horizontal scaling?

**Answer:**
*   **Vertical Scaling (Breadth-First):** Adding more power (CPU, RAM, SSD) to an existing server.
    *   *Limit:* Hardware constraints. Single Point of Failure.
*   **Horizontal Scaling (Scale-Out):** Adding more machines (servers) to the resource pool.
    *   *Limit:* Complexity (needs load balancing, distributed consensus). Unlimited theoretical scale.

---

## 432. What is replication?

**Answer:**
**Replication** is the process of copying data from one database server to one or more other servers.
*   **Goal:**
    1.  **Redundancy:** If one node fails, data is safe.
    2.  **Performance:** Distribute read queries to multiple nodes.

---

## 433. Master-slave replication?

**Answer:**
**Master-Slave Replication** is a common architecture.
*   **Master:** Handles all **writes** (INSERT, UPDATE, DELETE) and replicates updates to slaves.
*   **Slave:** Handles **read only** queries.
*   **Lag:** Slaves might be slightly behind the Master (Eventual Consistency).

---

## 434. What is read replica?

**Answer:**
A **Read Replica** is a copy of the primary database used exclusively for read operations.
*   **Use Case:** Offload reporting queries or high-volume reads from the Master database to improve overall performance.

---

## 435. What is failover?

**Answer:**
**Failover** is the automatic process of switching to a redundant or standby database server upon the failure of the primary server.
*   **Mechanism:** If Master is unreachable, a monitoring system/tool (like Orchestrator or AWS RDS) promotes a Slave to be the new Master.

---

## 436. What is connection pooling?

**Answer:**
**Connection Pooling** is a cache of database connections maintained so that the connections can be reused when future requests to the database are required.
*   **Why?** Creating a new DB connection is expensive (TCP Handshake, Auth).
*   **Tool:** **HikariCP** (Default in Spring Boot).

---

## 437. What is database migration?

**Answer:**
**Database Migration** is the process of managing incremental, reversible changes to relational database schemas.
*   **Concept:** Treat DB schema changes like code (Version Control).
*   **Benefit:** Consistency across environments (Dev, Test, Prod).

---

## 438. What is Flyway/Liquibase?

**Answer:**
They are **Database Migration Tools** used in Java.
*   **Flyway:** Uses SQL files (e.g., `V1__init.sql`). Simple and favors SQL.
*   **Liquibase:** Uses abstract formats (XML, YAML, JSON) or SQL. Better for database independence.
*   **Mechanism:** They create a table (e.g., `flyway_schema_history`) to track which scripts have already run.

---

## 439. How to design high-traffic DB?

**Answer:**
1.  **Caching:** Use Redis to reduce DB load.
2.  **Read Replicas:** Scale reads horizontally.
3.  **Indexing:** Optimize queries.
4.  **Partitioning/Sharding:** Split large tables.
5.  **Denormalization:** Avoid complex joins for critical paths.
6.  **Connection Pooling:** Efficient resource usage.

---

## 440. When to use NoSQL?

**Answer:**
Use **NoSQL** (MongoDB, Cassandra) when:
1.  **Schema is flexible/dynamic:** Adding fields without migrations.
2.  **Massive Scale:** Needs effortless horizontal scaling (Sharding built-in).
3.  **Unstructured Data:** JSON documents, Graphs.
4.  **High Write Throughput:** Log ingestion, IoT data.

---

## 441. What is stored procedure?

**Answer:**
A **Stored Procedure** is a prepared SQL code that you can save so the code can be reused over and over again.
*   **Pros:** Reduces network traffic (logic runs on DB server), centralized logic, maintainability.
*   **Cons:** Hard to debug/version control, vendor lock-in (PL/SQL vs T-SQL), increases load on DB server.

---

## 442. What is trigger?

**Answer:**
A **Trigger** is a set of SQL statements that automatically executes (fires) in response to certain events on a particular table.
*   **Events:** `INSERT`, `UPDATE`, `DELETE`.
*   **Timing:** `BEFORE`, `AFTER` (e.g., `BEFORE INSERT`).
*   **Use Case:** Audit trails, enforcing complex constraints, automating actions (updating a `last_modified` timestamp).

---

## 443. What is view?

**Answer:**
A **View** is a virtual table based on the result-set of an SQL statement.
*   **Storage:** It does **not store data** itself; it only stores the query definition.
*   **Use Case:** Simplify complex queries (hide joins), restrict access to specific columns (security).

---

## 444. What is materialized view?

**Answer:**
A **Materialized View** is a view that **physically stores** the result set on disk.
*   **Difference from View:** It is not virtual. It calculates the data beforehand.
*   **Pros:** Extremely fast reads for expensive aggregations.
*   **Cons:** Data is not real-time (must be refreshed). Good for reporting/warehousing.

---

## 445. What is indexing strategy for large tables?

**Answer:**
1.  **Cardinality Analysis:** Only index high-cardinality columns.
2.  **Composite Indexes:** Use multi-column indexes for common `WHERE` clauses (remember Leftmost Prefix).
3.  **Covering Indexes:** Include selected columns in the index to avoid table lookups.
4.  **Partial Indexes:** Index only a subset of rows (e.g., `WHERE active = true`).
5.  **Write Overhead:** Don't over-index; writes become slow.

---

## 446. What is composite vs multiple index?

**Answer:**
*   **Composite Index:** One index on multiple columns `(A, B)`.
    *   Good for `WHERE A=1 AND B=1`.
    *   Good for `WHERE A=1`.
    *   **Bad** for `WHERE B=1` (cannot use index).
*   **Multiple Indexes:** Separate indexes on `A` and `B`.
    *   DB might use "Index Merge" (use both and intersect), but usually less efficient than a proper Composite Index for combined queries.

---

## 447. What is pagination performance issue?

**Answer:**
Using `OFFSET` and `LIMIT` becomes very slow for large offsets (e.g., `LIMIT 10 OFFSET 1000000`).
*   **Why?** The DB must read and discard the first 1,000,000 rows to find the next 10.
*   **Time Complexity:** O(N) where N is the offset.

---

## 448. What is cursor-based pagination?

**Answer:**
**Cursor-based (Keyset) Pagination** solves the `OFFSET` problem by using a unique column (like ID or Timestamp) to find the "next" page.
*   **Query:** `SELECT * FROM users WHERE id > :last_seen_id ORDER BY id ASC LIMIT 10`.
*   **Benefit:** Is instantaneous (O(1) or O(log N) with index) regardless of how deep the page is.
*   **Drawback:** Cannot jump to specific page (e.g., "Go to Page 50").

---

## 449. What is data archiving?

**Answer:**
**Data Archiving** is the process of moving data that is no longer actively used to a separate storage device for long-term retention.
*   **Goal:** Keep the "Hot" database small and fast.
*   **Strategy:** Move "Cold" data (e.g., orders older than 1 year) to an Archive DB or Data Warehouse (S3/Snowflake) via ETL jobs.

---

## 450. How to handle millions of records?

**Answer:**
1.  **Indexing:** Essential for retrieval.
2.  **Partitioning:** Break table by date/ID range.
3.  **Sharding:** Distribute across servers.
4.  **Batch Processing:** Process updates in chunks (Batch size 1000), not one-by-one.
5.  **Asynchronous Processing:** Use queues (Kafka) to decouple ingestion from processing.
6.  **Caching:** Cache frequent reads.

---

## 451. Design schema for e-commerce system.

**Answer:**
**Core Tables:**
1.  `Users`: `id`, `email`, `password_hash`, `role`.
2.  `Products`: `id`, `name`, `description`, `price`, `stock_quantity`, `category_id`.
3.  `Categories`: `id`, `name`, `parent_id` (for hierarchy).
4.  `Orders`: `id`, `user_id`, `total_amount`, `status`, `created_at`.
5.  `OrderItems`: `id`, `order_id`, `product_id`, `quantity`, `price_at_purchase`.
6.  `Cart`: `id`, `user_id`. `CartItems` link to Products.

---

## 452. Design schema for order management.

**Answer:**
Focus on **state transitions** and **history**:
1.  `Orders`: The header information.
2.  `OrderHistory`: `id`, `order_id`, `status_from`, `status_to`, `changed_by`, `timestamp`. Essential for tracking lifecycle (Created -> Paid -> Shipped).
3.  `Payments`: `id`, `order_id`, `transaction_id`, `amount`, `status`, `provider` (Stripe/PayPal).
4.  `Shipments`: `id`, `order_id`, `tracking_number`, `courier`.

---

## 453. How to handle soft delete?

**Answer:**
**Soft Delete** marks a record as deleted without physically removing it from the database.
*   **Column:** Add `is_deleted` (BOOLEAN) or `deleted_at` (TIMESTAMP) to the table.
*   **Query:** All queries must filter `WHERE is_deleted = false`.
*   **Pros:** Data recovery, audit history.
*   **Cons:** Complexity in unique indexes (unique constraint on `email` + `deleted_at` needed), increased storage.

---

## 454. How to handle audit fields?

**Answer:**
Every table should ideally have:
1.  `created_at`: Timestamp.
2.  `created_by`: User ID.
3.  `updated_at`: Timestamp.
4.  `updated_by`: User ID.
*   **Implementation:** Use JPA `@PrePersist` and `@PreUpdate` or Hibernate Envers for full revision history (separate audit tables).

---

## 455. How to design multi-tenant DB?

**Answer:**
1.  **Database per Tenant:** Secure, isolated, expensive to maintain.
2.  **Schema per Tenant:** Shared DB, separate schemas. Good balance.
3.  **Shared Schema (Discriminator Column):** Add `tenant_id` to **every** table.
    *   *Pro:* Cheap, easy to scale.
    *   *Con:* Developer error (forgetting `WHERE tenant_id = ?`) causes data leaks. Use Hibernate Filters to enforce automatically.

---

## 456. How to prevent duplicate data?

**Answer:**
1.  **Database Constraints:** Use `UNIQUE` constraints (e.g., on `email` or composite key). This is the last line of defense.
2.  **Application Logic:** Check before insert (Race conditions possible).
3.  **Idempotency Keys:** For API requests.
4.  **Locks:** Pessimistic locking during check-then-insert.

---

## 457. How to handle transactional consistency?

**Answer:**
*   **Within one DB:** Use `@Transactional`.
*   **Across Microservices (Distributed):**
    1.  **Two-Phase Commit (2PC):** Strict but slow.
    2.  **Saga Pattern:** Choreography or Orchestration using compensating transactions (Undo actions) and Eventual Consistency.

---

## 458. How to design for high write throughput?

**Answer:**
1.  **Remove Secondary Indexes:** Indexes slow down writes.
2.  **Batch Inserts:** Insert 1000 rows in 1 query.
3.  **Partitioning:** Distribute writes across partitions.
4.  **NoSQL:** Cassandra/DynamoDB are optimized for writes (LSM Trees).
5.  **Asynchronous:** Write to a Queue (Kafka) first, then consume and interact with DB at a controlled pace.

---

## 459. How to reduce DB load?

**Answer:**
1.  **Caching:** Redis for frequent reads.
2.  **Read Replicas:** Move read operations to slaves.
3.  **Optimize Queries:** Indexing, avoiding wildcard scans.
4.  **CDN:** Serve static assets (images) away from your servers.
5.  **Archive:** Move old data out.

---

## 460. How to handle schema evolution?

**Answer:**
**Schema Evolution** handling changes without downtime:
1.  **Backward Compatibility:** New columns must be nullable or have defaults.
2.  **Deprecation:** Never delete a column immediately.
    *   Step 1: Renamed/Ignore in code.
    *   Step 2: Deploy code that doesn't use it.
    *   Step 3: Drop column in next release.
3.  **Tools:** Liquibase/Flyway for versioned DDL.

---

## 461. DB CPU is high – how to debug?

**Answer:**
1.  **Check Active Queries:** Use `SHOW PROCESSLIST` (MySQL) or `pg_stat_activity` (Postgres) to find running queries.
2.  **Slow Query Log:** Check if a specific query is appearing frequently.
3.  **Explain Plan:** Analyze the top resource-consuming queries for Full Table Scans.
4.  **Connection Count:** High concurrency might cause context switching overhead.

---

## 462. DB connections exhausted – solution?

**Answer:**
**Symptoms:** Application throws `ConnectionPoolExhaustedException`.
*   **Immediate Fix:** Increase pool size (temporarily).
*   **Root Cause Analysis:**
    1.  **Connection Leak:** App not closing connections (check `finally` block).
    2.  **Long Transactions:** Connections held too long.
    3.  **Scale:** Need `HikariCP` tuning or add Read Replicas.

---

## 463. Slow insert issue – possible causes?

**Answer:**
1.  **Too many indexes:** Every insert requires updating all indexes.
2.  **Lock Contention:** High concurrency on the same table/page.
3.  **Hardware Limits:** Disk I/O (IOPS) saturation.
4.  **Triggers:** Heavy logic executing on every insert.
5.  **Foreign Key Checks:** DB checks referential integrity.

---

## 464. Index not being used – why?

**Answer:**
Even if an index exists, the optimizer might ignore it:
1.  **Low Cardinality:** If the value matches 30%+ of rows, a Full Table Scan is faster.
2.  **Functions on Columns:** `WHERE YEAR(date)` invalidates the index.
3.  **Data Type Mismatch:** Comparing String to Int.
4.  **OR Condition:** Using `OR` on non-indexed columns.
5.  **Leftmost Prefix Violation:** In `(A, B)`, querying on `B` only.

---

## 465. Long-running transaction impact?

**Answer:**
1.  **Locks:** Holds locks on rows/tables, blocking other writers (and potentially readers).
2.  **Undo Log Growth:** In MVCC, old versions must be kept until the transaction finishes, bloating storage.
3.  **Replication Lag:** Slaves cannot replay the transaction until it commits on Master.

---

## 466. Lock wait timeout – causes?

**Answer:**
The application fails with `LockWaitTimeoutException`.
*   **Causes:**
    1.  **Deadlocks:** Two tx waiting for each other.
    2.  **Long Transactions:** Tx A holds lock for 50s; Tx B waits and times out (default 50s in MySQL).
    3.  **Uncommitted Tx:** Developer ran a query manually and forgot to `COMMIT`.

---

## 467. Data inconsistency in distributed system?

**Answer:**
**Scenario:** Order service says "Paid", but Delivery service says "Payment Pending".
*   **Causes:**
    1.  **Network Partition:** Event failed to publish to Kafka.
    2.  **Distributed Tx Failure:** Commit failed in one service but succeeded in another.
    3.  **Replication Lag:** Reading from a stale slave.
*   **Fix:** Reconciliation jobs (Cron) or Saga Pattern (Compensating transactions).

---

## 468. Large join performance issue?

**Answer:**
Queries joining huge tables (Millions of rows) are slow.
*   **Fixes:**
    1.  **Indexing:** Ensure Join Keys (`ON t1.id = t2.id`) are indexed.
    2.  **Reduce Set:** Filter (`WHERE`) *before* joining.
    3.  **Denormalization:** Store required fields in one table to avoid the join.
    4.  **Application Join:** Fetch IDs and join in Java (sometimes faster).

---

## 469. Missing index issue?

**Answer:**
**Symptom:** API is slow (2s+), CPU high.
*   **Diagnosis:** Run `EXPLAIN` on the query. Look for `type: ALL` (Full Table Scan) or `rows: 1000000`.
*   **Fix:** Create the appropriate index. Note that creating an index on a large live table can accept locks (use Online DDL).

---

## 470. Real production DB issue you handled?

**Answer:**
*   **Situation:** Black Friday access spike caused DB CPU to hit 100%.
*   **Analysis:** `SHOW PROCESSLIST` revealed thousands of identical `SELECT * FROM products` queries.
*   **Root Cause:** A new feature introduced an N+1 query problem, fetching product details in a loop.
*   **Resolution:** Hotfix to cache the data in Redis and refactor code to use `IN` clause (Batch fetching).

---

## 471. What is AWS?

**Answer:**
**AWS (Amazon Web Services)** is a secure cloud services platform, offering compute power, database storage, content delivery, and other functionality.
*   **Infrastructure as a Service (IaaS):** Provides virtualized computing resources over the internet.
*   **Benefits:** Scalability, Pay-as-you-go pricing, Global reliability.

---

## 472. What is EC2?

**Answer:**
**EC2 (Elastic Compute Cloud)** is a web service that provides secure, resizable compute capacity in the cloud.
*   **Instance:** Virtual server.
*   **Types:** General Purpose (T3, M5), Compute Optimized (C5), Memory Optimized (R5).
*   **Role:** Running applications, backend servers, microservices.

---

## 473. What is S3?

**Answer:**
**S3 (Simple Storage Service)** is an object storage service.
*   **Object:** File + Metadata (not a block store).
*   **Structure:** Data is stored in **Buckets**.
*   **Use Case:** Storing backups, static website hosting, media files, data lakes.
*   **Durability:** 99.999999999% (11 9s).

---

## 474. What is RDS?

**Answer:**
**RDS (Relational Database Service)** makes it easy to set up, operate, and scale a relational database in the cloud.
*   **Engines:** MySQL, PostgreSQL, MariaDB, Oracle, SQL Server, Aurora.
*   **Managed Features:** Automated backups, patching, Multi-AZ deployment (High Availability), Read Replicas.

---

## 475. What is IAM?

**Answer:**
**IAM (Identity and Access Management)** enables you to manage access to AWS services and resources securely.
*   **Users:** People/Applications.
*   **Groups:** Collections of users.
*   **Roles:** Permissions assigned to trusted entities (e.g., EC2 instance accessing S3).
*   **Policies:** JSON documents defining permissions (Allow/Deny).

---

## 476. What is VPC?

**Answer:**
**VPC (Virtual Private Cloud)** is a logically isolated section of the AWS Cloud where you can launch resources in a virtual network that you define.
*   **Control:** You control IP ranges, subnets, route tables, and gateways.
*   **Goal:** Security and Network isolation.

---

## 477. What is subnet?

**Answer:**
A **Subnet** is a range of IP addresses in your VPC.
*   **Public Subnet:** Has a route to the Internet Gateway (can access internet). Used for Load Balancers, Bastion Hosts.
*   **Private Subnet:** No direct route to the Internet. Used for App Servers, Databases (Security best practice).

---

## 478. What is security group?

**Answer:**
A **Security Group** acts as a **virtual firewall** for your instance to control inbound and outbound traffic.
*   **Stateful:** If you allow an incoming request, the response is automatically allowed.
*   **Scope:** Applied at the **Instance level**.
*   **Default:** Deny all inbound, Allow all outbound.

---

## 479. What is NACL?

**Answer:**
**NACL (Network Access Control List)** is an optional layer of security for your VPC that acts as a firewall for controlling traffic in and out of one or more subnets.
*   **Stateless:** You must explicitly allow both inbound and outbound traffic.
*   **Scope:** Applied at the **Subnet level**.

---

## 480. What is Elastic Load Balancer?

**Answer:**
**ELB (Elastic Load Balancer)** automatically distributes incoming application traffic across multiple targets, such as EC2 instances, containers, and IP addresses.
*   **Types:**
    1.  **ALB (Application Load Balancer):** Layer 7 (HTTP/HTTPS). Path-based routing.
    2.  **NLB (Network Load Balancer):** Layer 4 (TCP/UDP). High performance.
    3.  **CLB (Classic Load Balancer):** Legacy.

---

## 481. What is Auto Scaling?

**Answer:**
**Auto Scaling** monitors your applications and automatically adjusts capacity to maintain steady, predictable performance at the lowest possible cost.
*   **Scale Out:** Add EC2 instances when CPU > 70%.
*   **Scale In:** Remove EC2 instances when CPU < 20%.
*   **Group:** **ASG (Auto Scaling Group)** manages the collection of EC2 instances.

---

## 482. What is Route 53?

**Answer:**
**Route 53** is a highly available and scalable **DNS (Domain Name System)** web service.
*   **Function:** Translates domain names (`www.example.com`) to IP addresses (`192.0.2.1`).
*   **Features:** Health checks, Failover routing, Latency-based routing, Geo-location routing.

---

## 483. What is CloudFront?

**Answer:**
**CloudFront** is a global **CDN (Content Delivery Network)** service that delivers data, videos, applications, and APIs to customers globally with low latency.
*   **Mechanism:** Caches content at **Edge Locations** closer to the user.
*   **Benefit:** Reduces load on the origin server (S3/EC2) and speeds up content delivery.

---

## 484. What is ECR?

**Answer:**
**ECR (Elastic Container Registry)** is a fully managed Docker container registry.
*   **Role:** Stores, manages, and deploys Docker container images.
*   **Integration:** Works seamlessly with ECS and EKS.

---

## 485. What is ECS?

**Answer:**
**ECS (Elastic Container Service)** is a fully managed container orchestration service.
*   **Role:** Runs and manages Docker containers on a cluster of EC2 instances (or Fargate).
*   **Simplicity:** Easier to set up than Kubernetes but less flexible.

---

## 486. What is EKS?

**Answer:**
**EKS (Elastic Kubernetes Service)** is a managed service to run **Kubernetes** on AWS.
*   **Role:** Runs K8s control plane and worker nodes.
*   **Use Case:** Standard way to run K8s applications, migrating existing K8s workloads.

---

## 487. What is Lambda?

**Answer:**
**Lambda** is a **Serverless** compute service that lets you run code without provisioning or managing servers.
*   **Trigger:** Responds to events (S3 upload, API Gateway request, DynamoDB update).
*   **Pricing:** Pay only for the compute time you consume (millis).
*   **Limit:** Execution time limit (15 mins).

---

## 488. What is API Gateway?

**Answer:**
**API Gateway** is a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs.
*   **Role:** Acts as a "front door" for applications to access data/logic from backend services (Lambda, EC2).
*   **Features:** Throttling, Caching, Authentication (Cognito/IAM), API Keys.

---

## 489. What is CloudWatch?

**Answer:**
**CloudWatch** is a **monitoring** and observability service.
*   **Metrics:** CPU utilization, Disk I/O, Network traffic.
*   **Logs:** Collects and stores logs from EC2, Lambda, etc.
*   **Alarms:** Send notifications (SNS) when a threshold is breached (e.g., CPU > 80%).

---

## 490. What is CloudTrail?

**Answer:**
**CloudTrail** provides **auditing**, security monitoring, and operational troubleshooting.
*   **Function:** Records **API calls** made on your account.
*   **Use Case:** "Who deleted this S3 bucket?" "Who terminated this EC2 instance?" - CloudTrail has the answer.

---

## 491. What is blue-green deployment in AWS?

**Answer:**
**Blue-Green Deployment** is a technique that reduces downtime and risk by running two identical production environments.
*   **Blue:** Current live environment.
*   **Green:** New version of the application.
*   **Switch:** Once Green is tested, you switch the Load Balancer/DNS to point to Green. Blue becomes idle.
*   **Rollback:** Instant. Just switch back to Blue.

---

## 492. What is rolling deployment?

**Answer:**
**Rolling Deployment** updates instances with the new version incrementally.
*   **Process:** Update 2 instances -> Wait for health check -> Update next 2 -> Repeat.
*   **Pros:** Zero downtime, no need for double capacity (like Blue-Green).
*   **Cons:** Application runs in mixed versions during the deployment window.

---

## 493. What is infrastructure as code?

**Answer:**
**IaC (Infrastructure as Code)** is the practice of managing and provisioning infrastructure through machine-readable definition files, rather than physical hardware configuration or interactive configuration tools.
*   **Tools:** Terraform, AWS CloudFormation, Ansible.
*   **Benefits:** Consistency, Version Control (Git), Reproducibility.

---

## 494. What is CloudFormation?

**Answer:**
**AWS CloudFormation** is a service that gives developers an easy way to create a collection of related AWS resources (stack) using templates (JSON/YAML).
*   **Native:** deeply integrated with AWS.
*   **State:** Manages the state of your stack automatically.

---

## 495. What is Terraform?

**Answer:**
**Terraform** is an open-source IaC tool by HashiCorp that allows you to define cloud and on-prem resources in human-readable configuration files (HCL).
*   **Cloud Agnostic:** Works with AWS, Azure, GCP.
*   **State Management:** Uses a state file (`terraform.tfstate`) to map resources to configuration.

---

## 496. How to deploy Spring Boot in AWS?

**Answer:**
1.  **EC2:** Copy JAR, run `java -jar app.jar`. Manual or via User Data script.
2.  **Elastic Beanstalk:** Upload JAR, AWS manages OS/Tomcat/Scaling.
3.  **ECS/EKS:** Dockerize app, push to ECR, deploy as a Task/pod.
4.  **Lambda:** Deploy as a Serverless function (SnapStart for faster cold starts).

---

## 497. How to secure application in AWS?

**Answer:**
1.  **VPC:** Deploy app in Private Subnets.
2.  **Security Groups:** Allow traffic only from Load Balancer (port 80/443).
3.  **IAM:** Use Roles (not Access Keys) for EC2 to access S3/DB. **Least Privilege** principle.
4.  **WAF (Web App Firewall):** Protect against SQLi, XSS.
5.  **HTTPS:** Use ACM (Amazon Certificate Manager) for SSL.

---

## 498. What is SSL termination?

**Answer:**
**SSL Termination** is the process of decrypting encrypted traffic (HTTPS) at the Load Balancer (ELB) before sending it to the backend servers (over HTTP).
*   **Benefit:** Offloads the CPU-intensive decryption work from the application servers, allowing them to focus on logic.

---

## 499. How to configure autoscaling?

**Answer:**
1.  **Launch Template:** Define "What" to launch (AMI, Instance Type, Security Groups).
2.  **Auto Scaling Group (ASG):** Define "Where" (VPC, Subnets) and "How many" (Min: 2, Max: 10).
3.  **Scaling Policies:**
    *   **Target Tracking:** Keep CPU at 50%.
    *   **Step/Simple:** If Alarm > 80%, add 2 instances.

---

## 500. Production deployment checklist?

**Answer:**
1.  **Code:** Unit/Integration tests passed? Code reviewed?
2.  **Config:** Env variables set? Secrets (DB params) in Secrets Manager?
3.  **Database:** Migrations (Flyway) tested? backup taken?
4.  **Infrastructure:** Autoscaling configured? Health checks (Liveness/Readiness) active?
5.  **Security:** HTTPS enabled? Security Groups tight?
6.  **Observability:** Logging (CloudWatch/Splunk) and Monitoring (NewRelic/Datadog) enabled?
7.  **Rollback Strategy:** Is Blue-Green or Rolling enabled?

---

## 501. Design highly available architecture in AWS.

**Answer:**
**Goal:** Eliminate Single Points of Failure (SPOF).
1.  **Region:** Choose a region (e.g., us-east-1).
2.  **VPC:** Multi-AZ deployment.
3.  **Compute:** Auto Scaling Group spanning at least 2 **Availability Zones (AZs)**.
4.  **Database:** RDS Multi-AZ (Primary in AZ A, Standby in AZ B).
5.  **Load Balancing:** ALB distributing traffic across instances in all AZs.

---

## 502. Multi-region deployment strategy?

**Answer:**
**Goal:** Global low latency and Disaster Recovery.
1.  **Active-Active:** Traffic goes to both regions (Route 53 Geo Routing). DynamoDB Global Tables or Aurora Global Database sync data.
2.  **Active-Passive:** Traffic goes to Region A. Region B is cold/warm standby.

---

## 503. Disaster recovery strategy?

**Answer:**
RPO (Recovery Point Objective - Data Loss) vs RTO (Recovery Time Objective - Downtime).
1.  **Backup & Restore:** Cheapest, highest RTO/RPO.
2.  **Pilot Light:** DB data is live in DR region, app servers are off.
3.  **Warm Standby:** Scaled-down version running in DR region.
4.  **Multi-Site Active/Active:** Zero downtime, most expensive.

---

## 504. Backup strategy?

**Answer:**
1.  **RDS:** Enable Automated Backups (Retention 7-35 days). Manual Snapshots before major changes.
2.  **S3:** Enable Versioning and Cross-Region Replication (CRR) for critical buckets.
3.  **EBS:** AWS Backup service to automate volume snapshots.
4.  **DynamoDB:** Point-In-Time Recovery (PITR).

---

## 505. High traffic scaling strategy?

**Answer:**
1.  **CDN (CloudFront):** Offload static assets.
2.  **Caching (ElastiCache):** Offload DB reads.
3.  **Auto Scaling (ASG):** Scale compute based on traffic.
4.  **DB Scaling:** Read Replicas for reads, Sharding for writes.
5.  **Async Processing:** Use SQS/Kinesis to buffer writes during spikes.

---

## 506. Secure microservices in AWS?

**Answer:**
1.  **Private Subnets:** No direct internet access.
2.  **Internal ALB:** Use internal load balancers for inter-service comms.
3.  **Security Groups:** Service A SG allows traffic only from Service B SG.
4.  **IAM Roles:** Services use IAM roles (IRSA for EKS) to access resources.
5.  **mTLS:** Use App Mesh or Istio for encrypted service-to-service communication.

---

## 507. Deploy Kafka in AWS?

**Answer:**
1.  **MSK (Managed Streaming for Kafka):** Fully managed, High Availability, auto-patching. Best for production.
2.  **EC2:** Install Kafka on EC2. Full control, but high maintenance (Zookeeper management, OS patching).

---

## 508. Deploy Redis in AWS?

**Answer:**
1.  **ElastiCache for Redis:** Fully managed.
    *   **Cluster Mode Enabled:** Sharding for write scaling.
    *   **Multi-AZ:** Auto-failover.
2.  **EC2:** Self-managed Redis (Avoid unless necessary).

---

## 509. RDS performance tuning?

**Answer:**
1.  **Instance Class:** Upgrade CPU/RAM (Vertical Scaling).
2.  **IOPS:** Switch storage type to **Provisioned IOPS (io1/io2)** for high disk throughput.
3.  **Performance Insights:** Use AWS tool to find slow SQL.
4.  **Read Replicas:** Offload reads.
5.  **Parameter Group:** Tune MySQL/PG params (e.g., `innodb_buffer_pool_size`).

---

## 510. Cost optimization strategies?

**Answer:**
1.  **Reserved Instances (RI) / Savings Plans:** Commit for 1-3 years for ~70% discount.
2.  **Spot Instances:** Use for fault-tolerant batch jobs (~90% discount).
3.  **Right Sizing:** Compute Optimizer acts to downgrade oversized instances.
4.  **S3 Lifecycle Policies:** Move old logs to S3 Glacier.
5.  **Stop Idle Resources:** Lambda script to stop Dev instances at night.

---

## 511. How to monitor production apps?

**Answer:**
**Observability Trinity:**
1.  **Metrics:** "What is happening?" (CPU is 90%).
2.  **Logs:** "Why is it happening?" (Exception stack trace).
3.  **Traces:** "Where is it happening?" (Microservice A -> B -> C).

---

## 512. What metrics do you track?

**Answer:**
**USE Method (for Infrastructure):**
1.  **Utilization:** % time busy (CPU use).
2.  **Saturation:** Queue length (Disk I/O wait).
3.  **Errors:** Count of error events.

**RED Method (for Services):**
1.  **Rate:** Requests per second (RPS).
2.  **Errors:** Failed requests per second (HTTP 500s).
3.  **Duration:** Latency (p95, p99).

---

## 513. Log aggregation tools?

**Answer:**
Tools to collect logs from multiple servers into a central search engine.
1.  **ELK Stack:** Elasticsearch, Logstash, Kibana.
2.  **Splunk:** Enterprise log management.
3.  **CloudWatch Logs:** AWS native.
4.  **Datadog/NewRelic:** SaaS observability platforms.

---

## 514. What is centralized logging?

**Answer:**
**Centralized Logging** aggregates logs from all microservices/servers into a single location.
*   **Why?** In a distributed system, you can't SSH into 50 different servers to `grep` logs.
*   **Structure:** Uses a correlation ID (Trace ID) to stitch logs across services.

---

## 515. How to debug production issue in AWS?

**Answer:**
1.  **Check Dashboards:** CloudWatch/Datadog to identify the spike/error.
2.  **Check Logs:** Query Centralized Logs using the Trace ID.
3.  **Check Traces:** Distributed Tracing (X-Ray/Jaeger) to find the slow component.
4.  **Reproduce:** Try to reproduce in Staging.

---

## 516. How to configure alerts?

**Answer:**
Alerts notify engineers when things go wrong.
*   **Threshold:** "Alert if CPU > 80% for 5 mins".
*   **Anomaly Detection:** "Alert if traffic drops by 50% compared to last week".
*   **Channels:** Slack, Email, PagerDuty (for urgent incidents).

---

## 517. How to reduce downtime?

**Answer:**
1.  **Redundancy:** Multi-AZ/Multi-Region.
2.  **Failover:** Automated health checks and DNS failover.
3.  **Circuit Breakers:** Prevent cascading failures.
4.  **Rate Limiting:** Prevent DDOS/Accidental overload.
5.  **Rollback:** Quick rollback mechanism for bad deployments.

---

## 518. What is SLA vs SLO?

**Answer:**
*   **SLA (Service Level Agreement):** Contract with the customer. "We promise 99.9% uptime or we pay you."
*   **SLO (Service Level Objective):** Internal goal. "We aim for 99.95% uptime." (Stricter than SLA).
*   **SLI (Service Level Indicator):** The actual metric. "Current uptime is 99.99%."

---

## 519. What is error budget?

**Answer:**
**Error Budget** is the amount of unreliability you are allowed to have.
*   **Calculation:** 100% - SLO (e.g., 100% - 99.9% = 0.1% budget).
*   **Use:** If you have budget left, you can ship risky features. If budget is exhausted, freeze changes and focus on stability.

---

## 520. What is autoscaling metric selection?

**Answer:**
Choosing the right metric to trigger scaling:
1.  **CPU Utilization:** Good for compute-heavy apps.
2.  **Request Count:** Good for I/O bound web apps.
3.  **SQS Queue Depth:** Good for worker services processing jobs.
4.  **Memory:** Rarely used (Java GC complicates this), but useful for memory leaks.

---

## 521. IAM best practices?

**Answer:**
1.  **Least Privilege:** Grant only necessary permissions.
2.  **MFA:** Enable Multi-Factor Authentication for Root and IAM users.
3.  **Roles over User:** Use IAM Roles for EC2/Lambda instead of long-term credentials (Access Keys).
4.  **Rotate Credentials:** Rotate Access Keys every 90 days.
5.  **No Root:** Never use the Root account for daily tasks.

---

## 522. How to protect secrets?

**Answer:**
Never hardcode secrets (DB passwords, API Keys) in code.
1.  **AWS Secrets Manager:** Automatic rotation, centralized management.
2.  **AWS Systems Manager Parameter Store:** Cheaper alternative for config/secrets (SecureString).
*   **Access:** App retrieves secret at runtime using IAM Role.

---

## 523. What is KMS?

**Answer:**
**KMS (Key Management Service)** is a managed service to create and control cryptographic keys.
*   **CMK (Customer Master Key):** Used to encrypt/decrypt data encryption keys.
*   **Integration:** Integrated with S3, EBS, RDS for "Encryption at Rest".

---

## 524. What is WAF?

**Answer:**
**WAF (Web Application Firewall)** protects web applications from common exploits.
*   **Layer:** Layer 7 (HTTP).
*   **Rules:** Block SQL Injection, XSS, Geo-blocking (block traffic from specific countries), Rate-based rules (DDoS).

---

## 525. DDoS protection?

**Answer:**
1.  **AWS Shield Standard:** Free, protects against L3/L4 attacks (SYN floods).
2.  **AWS Shield Advanced:** Paid, protects against sophisticated L7 attacks, provides 24/7 access to DRT (DDoS Response Team).
3.  **CloudFront/WAF:** Absorbs traffic at the edge.

---

## 526. How to restrict S3 bucket?

**Answer:**
1.  **Block Public Access:** Enable "Block all public access" setting.
2.  **Bucket Policy:** JSON policy to explicitly allow/deny access (e.g., only allowing CloudFront OAI).
3.  **ACLs:** (Legacy) Access Control Lists.
4.  **IAM Policy:** Control which users/roles can access the bucket.

---

## 527. How to encrypt data at rest?

**Answer:**
Encryption of data when it is stored on disk.
*   **S3:** Server-Side Encryption (SSE-S3, SSE-KMS).
*   **EBS/RDS:** Enable encryption checkbox during creation (uses KMS).
*   **DynamoDB:** Encrypted by default.

---

## 528. How to encrypt data in transit?

**Answer:**
Encryption of data as it moves between client and server.
*   **HTTPS (TLS/SSL):** Use ACM certificates on Load Balancers/CloudFront.
*   **VPN/Direct Connect:** Encrypted tunnel between on-prem and AWS.

---

## 529. Key rotation strategy?

**Answer:**
1.  **KMS:** Enable automatic key rotation (changes backing key material every year).
2.  **Secrets Manager:** Configured to rotate DB passwords automatically (calls a Lambda function to update DB and Secret).
3.  **IAM Access Keys:** Enforce policy to rotate every 90 days.

---

## 530. Secure CI/CD pipeline?

**Answer:**
1.  **Least Privilege:** CI/CD role should only have permission to deploy to specific resources using `AssumeRole`.
2.  **Scan Artifacts:** Scan Docker images (ECR) and Code (SonarQube) for vulnerabilities.
3.  **No Secrets in Repo:** Use OIDC (OpenID Connect) for git provider (GitHub Actions) to auth with AWS without long-lived keys.
4.  **Audit:** Enable CloudTrail to track deployment activities.

---

## 531. What is Docker?

**Answer:**
**Docker** is an open platform for developing, shipping, and running applications.
*   **Concept:** It separates your applications from your infrastructure using **containers**.
*   **Benefit:** "Build once, run anywhere" (Eliminates "It works on my machine" problem).

---

## 532. Docker vs VM?

**Answer:**
*   **Docker (Containers):** Virtualizes the **OS**. Shares the host kernel. Lightweight (MBs), starts in milliseconds.
*   **VM (Virtual Machine):** Virtualizes the **Hardware**. Needs a full Guest OS. Heavyweight (GBs), starts in minutes.

---

## 533. What is image?

**Answer:**
A **Docker Image** is a read-only template with instructions for creating a Docker container.
*   **Composition:** Layers of files (OS, Code, Dependencies).
*   **Analogy:** It's like a Java `Class` (Blueprint).

---

## 534. What is container?

**Answer:**
A **Container** is a runnable instance of an image.
*   **Key:** It is isolated from other containers and the host machine.
*   **Analogy:** It's like a Java `Object` (Running instance).

---

## 535. What is Dockerfile?

**Answer:**
A **Dockerfile** is a text document that contains all the commands a user could call on the command line to assemble an image.
*   **Key Commands:** `FROM` (Base image), `COPY` (Add code), `RUN` (Install builds), `CMD` (Start command).

---

## 536. What is Docker layer caching?

**Answer:**
Docker builds images in layers. If a layer hasn't changed (e.g., `FROM openjdk:17`), Docker reuses the cached layer instead of rebuilding it.
*   **Optimization:** Put stable commands (like installing dependencies) **before** volatile commands (copying source code) in Dockerfile to maximize cache hits.

---

## 537. What is multi-stage build?

**Answer:**
**Multi-stage builds** allow you to use multiple `FROM` statements in a single Dockerfile.
*   **Goal:** Create a small final image.
*   **Pattern:**
    1.  **Stage 1 (Build):** Install Maven, download deps, compile code (Large image).
    2.  **Stage 2 (Run):** Copy only the JAR from Stage 1. Discard Maven/Src (Tiny image).

---

## 538. What is docker-compose?

**Answer:**
**Docker Compose** is a tool for defining and running multi-container Docker applications.
*   **File:** `docker-compose.yaml`.
*   **Use Case:** Spin up App + DB + Redis with a single command: `docker-compose up`.

---

## 539. What is volume?

**Answer:**
**Volumes** are the preferred mechanism for persisting data generated by and used by Docker containers.
*   **Problem:** When a container is deleted, its file system is gone.
*   **Solution:** Mount a volume (`-v /data`) to store DB files on the host machine, independent of the container lifecycle.

---

## 540. What is network in Docker?

**Answer:**
Docker networking allows containers to communicate with each other and the outside world.
*   **Bridge (Default):** Containers on the same bridge network can talk via IP/Hostname.
*   **Host:** Container creates no isolation; uses Host's network stack directly.
*   **None:** No networking.

---

## 541. How to optimize Docker image size?

**Answer:**
1.  **Multi-Stage Builds:** Discard build tools (Maven/Grade) in final image.
2.  **Base Image:** Use smaller base images like `alpine` or `frolvlad/alpine-java`.
3.  **Layer Ordering:** Place frequent changes (code) at the bottom, infrequent (OS deps) at the top.
4.  **Chain Commands:** Combine `RUN apt-get update && apt-get install ...` to reduce layers.
5.  **Dockerignore:** Exclude `.git`, `target`, `node_modules` from context.

---

## 542. What is healthcheck in Docker?

**Answer:**
**Healthcheck** instruction tells Docker how to test a container to check that it is still working.
*   **Command:** `HEALTHCHECK CMD curl -f http://localhost:8080/actuator/health || exit 1`.
*   **Status:** Starts as `starting`, becomes `healthy` or `unhealthy`.
*   **Action:** Orchestrators (K8s/Swarm) restart unhealthy containers.

---

## 543. What is ENTRYPOINT vs CMD?

**Answer:**
*   **ENTRYPOINT:** The command that **always** runs when container starts. Hard to override.
    *   *Example:* `ENTRYPOINT ["java", "-jar", "app.jar"]`.
*   **CMD:** Default arguments passed to the ENTRYPOINT. Easy to override.
    *   *Example:* `CMD ["--server.port=80"]`.
*   **Combined:** `java -jar app.jar --server.port=80`.

---

## 544. What is container orchestration?

**Answer:**
**Orchestration** manages the lifecycle of containers, especially in large, dynamic environments.
*   **Responsibilities:** Provisioning, Deployment, Scaling, Networking, Load Balancing, Health Monitoring.
*   **Tools:** Kubernetes (Standard), Docker Swarm (Simple), Nomad.

---

## 545. What is Kubernetes?

**Answer:**
**Kubernetes (K8s)** is an open-source system for automating deployment, scaling, and management of containerized applications.
*   **Origin:** Google (Borg).
*   **Architecture:** Master Node (Control Plane) + Worker Nodes.

---

## 546. What is Pod?

**Answer:**
A **Pod** is the smallest deployable unit in Kubernetes.
*   **Concept:** Represents a single instance of a running process in your cluster.
*   **Content:** Usually contains **one** container (e.g., Spring Boot app).
*   **Sidecar:** Can contain helper containers (e.g., Logging agent) sharing the same IP/Volume.

---

## 547. What is Deployment?

**Answer:**
A **Deployment** manages a set of replicated Pods.
*   **Role:** Ensures the desired number of pods are running (ReplicaSet).
*   **Features:** Self-healing (restarts failed pods), Scaling (scale up/down), Rolling Updates (zero downtime).

---

## 548. What is Service in Kubernetes?

**Answer:**
A **Service** provides a stable IP address and DNS name to a set of dynamic Pods.
*   **Why?** Pod IPs change when they restart. Service IP is static.
*   **Types:**
    1.  **ClusterIP:** Internal only (Default).
    2.  **NodePort:** Exposes port on each Node IP.
    3.  **LoadBalancer:** Provisions cloud LB (AWS ALB).

---

## 549. What is ConfigMap?

**Answer:**
**ConfigMap** is an API object used to store non-confidential data in key-value pairs.
*   **Use Case:** Externalize configuration (application.properties) from the image.
*   **Injection:** As Environment Variables or Mounted Volume.

---

## 550. What is Secret in K8s?

**Answer:**
**Secret** is an object that contains a small amount of sensitive data such as passwords, tokens, or keys.
*   **Encoding:** Stored as Base64 encoded strings (Not encrypted by default!).
*   **Security:** Should be encrypted at rest (Etcd encryption) and restricted via RBAC.

---

## 551. What is CI/CD?

**Answer:**
**CI/CD** is a method to frequently deliver apps to customers by introducing automation into the stages of app development.
*   **CI (Continuous Integration):** Developers merge code changes into a central repository where automated builds and tests run.
*   **CD (Continuous Delivery):** Automatically release to repository/staging.
*   **CD (Continuous Deployment):** Automatically deploy to production without manual intervention.

---

## 552. What is Jenkins?

**Answer:**
**Jenkins** is an open-source automation server helping to automate the parts of software development related to building, testing, and deploying.
*   **Key:** Highly plugin-based (1000+ plugins).
*   **Architecture:** Master-Agent (Master schedules builds, Agents execute them).

---

## 553. What is GitHub Actions?

**Answer:**
**GitHub Actions** is a CI/CD platform deeply integrated with GitHub.
*   **Workflow:** Defined in `.github/workflows/*.yml`.
*   **Benefit:** No separate server to manage (unlike Jenkins). Runners are provided by GitHub (or self-hosted).

---

## 554. What is GitLab CI?

**Answer:**
**GitLab CI/CD** is a tool built into GitLab for software development.
*   **Config:** Defined in `.gitlab-ci.yml`.
*   **Runner:** Applications that run jobs in a pipeline.
*   **Feature:** Strong integration with Kubernetes (Auto DevOps).

---

## 555. What is pipeline as code?

**Answer:**
**Pipeline as Code** defines the deployment pipeline through code (e.g., Jenkinsfile), rather than configuring it through a GUI.
*   **Benefits:** Version controlled, reviewed, audit trail, reusability.

---

## 556. What are pipeline stages?

**Answer:**
Typical stages in a CI/CD pipeline:
1.  **Checkout:** Get code from Git.
2.  **Build:** Compile code (Maven `mvn clean package`).
3.  **Test:** Run Unit/Integration tests.
4.  **Scan:** Code Quality (SonarQube) / Security (Snyk).
5.  **Package:** Build Docker Image / JAR.
6.  **Deploy:** Push to Dev/Stage/Prod.

---

## 557. What is artifact repository?

**Answer:**
An **Artifact Repository** manages binary components (JARs, WARs, Docker Images) generated by the build process.
*   **Tools:** Nexus, Artifactory.
*   **Role:** Caches dependencies (Maven Central) and stores internal build artifacts for deployment.

---

## 558. What is SonarQube?

**Answer:**
**SonarQube** is a tool for automatic code review and static analysis to detect bugs, vulnerabilities, and code smells.
*   **Quality Gate:** Blocks the pipeline if code quality doesn't meet the threshold (e.g., Code Coverage < 80%).

---

## 559. What is code coverage?

**Answer:**
**Code Coverage** is a metric used to measure the percentage of code lines executed during automated tests.
*   **Tool:** JaCoCo (Java Code Coverage).
*   **Goal:** High coverage (e.g., >80%) reduces the risk of undetected bugs.

---

## 560. What is automated deployment?

**Answer:**
**Automated Deployment** is the process of releasing software to an environment (Test/Prod) without manual intervention.
*   **Mechanism:** CI tool (Jenkins) triggers a script (Ansible/Kubectl) to update the running application with the new artifact.

---

## 561. What is blue-green in CI/CD?

**Answer:**
**Blue-Green Deployment** reduces downtime by running two identical production environments.
*   **Blue:** Live version.
*   **Green:** New version (Idle).
*   **Switch:** Router switches traffic from Blue to Green.
*   **Benefit:** Instant rollback if Green fails.

---

## 562. What is canary in CI/CD?

**Answer:**
**Canary Deployment** releases code to a small percentage of users before a full rollout.
*   **Process:** 10% traffic -> Green (New), 90% -> Blue (Old).
*   **Monitor:** If errors spike, route 100% back to Blue. If stable, increase to 100% Green.

---

## 563. What is rollback strategy?

**Answer:**
A plan to revert to the previous stable version if a deployment fails.
*   **Automated:** Pipeline triggers rollback if health checks fail within 5 mins.
*   **Manual:** Re-deploy the previous Docker tag (`v1.0`).

---

## 564. How to secure pipeline?

**Answer:**
1.  **Secrets Management:** Use Vault/AWS Secrets Manager, never hardcode in git.
2.  **Least Privilege:** CI runners should only have permissions they need.
3.  **Scan Images:** Scan Docker images for CVEs (Trivy/Clair).
4.  **Signed Commits:** Ensure code integrity.

---

## 565. How to manage environment variables?

**Answer:**
*   **Code:** Use placeholders (`${DB_URL}`).
*   **CI/CD:** Inject values during deployment (ConfigMaps/Secrets).
*   **Runtime:** Application reads from OS environment variables.

---

## 566. What is trunk-based development?

**Answer:**
**Trunk-Based Development** is a branching strategy where developers merge small, frequent updates to a core "main" (trunk) branch.
*   **Goal:** Avoid "Merge Hell".
*   **Requirement:** Strong automated tests and Feature Flags.

---

## 567. What is feature branch workflow?

**Answer:**
**Feature Branch Workflow** creates a new branch for every feature.
*   **Process:** Branch -> Commit -> Pull Request (Review) -> Merge to Main.
*   **Goal:** Code review isolation.

---

## 568. What is GitOps?

**Answer:**
**GitOps** uses Git as the "single source of truth" for declarative infrastructure and applications.
*   **Tool:** ArgoCD, Flux.
*   **Flow:** Developer pushes to Git -> ArgoCD sees change -> ArgoCD syncs Cluster to match Git state.

---

## 569. What is immutable infrastructure?

**Answer:**
**Immutable Infrastructure** means servers are never modified after deployment.
*   **Update:** To update, you build a NEW server/image and replace the old one.
*   **Benefit:** No configuration drift (Snowflake servers).

---

## 570. How to handle zero downtime deployment?

**Answer:**
1.  **Rolling Updates:** Replace pods one by one.
2.  **Readiness Probes:** K8s doesn't send traffic to a new pod until it's ready.
3.  **Graceful Shutdown:** App finishes current requests before stopping (`SIGTERM` handling).
4.  **Database:** Backward-compatible schema changes (e.g., add column, don't rename yet).

---

## 571. Common Docker production issues?

**Answer:**
1.  **OOMKilled:** Container consumes more memory than limit -> Kernel kills it.
2.  **Slow Startup:** Java app takes too long -> Liveness probe kills it loop.
3.  **Disk Full:** Logs/Volumes fill up node disk.
4.  **Networking:** DNS failures between containers.
5.  **Zombie Processes:** PID 1 doesn't reap zombie children.

---

## 572. Debug container crash?

**Answer:**
1.  **Status:** `docker ps -a` (Check `Exit Code`).
    *   `137` = OOMKilled (Memory).
    *   `1` = Application Error.
2.  **Logs:** `docker logs <container_id>`.
3.  **Inspect:** `docker inspect <container_id>` to see State/Reason.
4.  **Events:** `kubectl get events` (if K8s) to see scheduling/probe errors.

---

## 573. Image vulnerability scanning?

**Answer:**
Process of analyzing Docker images for known security vulnerabilities (CVEs).
*   **Tools:** Trivy, Clair, AWS ECR Scanning, Snyk.
*   **Best Practice:** Block deployment if Critical CVE > 0.

---

## 574. Container memory limit?

**Answer:**
**Memory Limit** restricts how much RAM a container can use.
*   **Hard Limit:** If exceeded, container is **Killed** (OOM).
*   **Soft Limit:** If exceeded, container might be throttled or killed under pressure.
*   **Java:** ensure JVM knows limits (`-XX:+UseContainerSupport`, `-XX:MaxRAMPercentage=75`).

---

## 575. How to monitor containers?

**Answer:**
1.  **cAdvisor:** Google tool that provides resource usage (CPU/Mem) of running containers.
2.  **Prometheus:** Scrapes metrics from cAdvisor/Application.
3.  **Grafana:** Visualizes metrics.
4.  **CloudWatch Container Insights:** AWS managed solution.

---

## 576. K8s autoscaling?

**Answer:**
1.  **HPA (Horizontal Pod Autoscaler):** Adds more Pods based on CPU/Memory.
2.  **VPA (Vertical Pod Autoscaler):** Increases CPU/Memory limit of existing Pods.
3.  **Cluster Autoscaler:** Adds more Nodes (VMs) when Pods can't be scheduled (Pending state).

---

## 577. Liveness vs readiness probe?

**Answer:**
*   **Liveness Probe:** "Is the app alive/dead?"
    *   If fails: **Restart** the container.
    *   Use for deadlock/crash recovery.
*   **Readiness Probe:** "Is the app ready to serve traffic?"
    *   If fails: **Stop sending traffic** (Remove from Service endpoint).
    *   Use for startup loading/db connection check.

---

## 578. Rolling update in Kubernetes?

**Answer:**
**Rolling Update** is the default deployment strategy in K8s.
*   **Logic:** Replaces old Pods with new ones gradually.
*   **Parameters:**
    *   `maxUnavailable`: How many pods can be down during update (e.g., 25%).
    *   `maxSurge`: How many extra pods can be created (e.g., 25%).

---

## 579. How to expose K8s service?

**Answer:**
1.  **ClusterIP:** Internal only (Default).
2.  **NodePort:** Opens port on every Node (Good for dev, not prod).
3.  **LoadBalancer:** Cloud LB (Expensive for every service).
4.  **Ingress:** HTTP/HTTPS Router (Nginx) that sits in front of services. Single IP for multiple services based on path (`/app1`, `/app2`).

---

## 580. Production checklist for containerized app?

**Answer:**
1.  **Limits:** CPU/Memory requests & limits defined?
2.  **Probes:** Liveness & Readiness probes configured?
3.  **Security:** Non-root user? Read-only Root FS?
4.  **Logging:** JSON logging to stdout/stderr?
5.  **Graceful Shutdown:** SIGTERM handled?
6.  **Tagging:** Use specific tags (`v1.2`), never `latest`.

---

## 581. What is system design?

**Answer:**
**System Design** is the process of defining the architecture, components, modules, interfaces, and data for a system to satisfy specified requirements.
*   **Goal:** Build systems that are scalable, reliable, and maintainable.

---

## 582. What is scalability?

**Answer:**
**Scalability** is the ability of a system to handle growing amounts of work by adding resources.
*   **Vertical (Scale Up):** Add more power (CPU/RAM) to an existing machine.
*   **Horizontal (Scale Out):** Add more machines to the pool.

---

## 583. What is availability?

**Answer:**
**Availability** is the percentage of time a system remains operational and accessible.
*   **Metric:** "Nines" (e.g., 99.9% uptime = 8.7 hours downtime/year; 99.999% = 5 mins/year).
*   **Strategy:** Redundancy, Failover, Replication.

---

## 584. What is reliability?

**Answer:**
**Reliability** is the probability that a system will perform its intended function without failure for a specified time.
*   **Key:** A system can be available (respond 200 OK) but unreliable (return wrong data).

---

## 585. What is CAP theorem?

**Answer:**
In a distributed system, you can only guarantee **two** of the following three:
1.  **Consistency (C):** All nodes see the same data at the same time.
2.  **Availability (A):** Every request receives a response (succeed/fail).
3.  **Partition Tolerance (P):** System continues to operate despite network failures (partitions).
*   **Reality:** In distributed systems, **P** is mandatory. You chose between **CP** (Consistency/MongoDB) or **AP** (Availability/Cassandra).

---

## 586. What is consistency model?

**Answer:**
Defines the rules for the apparent order and expected visibility of updates.
*   **Strong Consistency:** Updates are visible immediately to all (like a single machine).
*   **Eventual Consistency:** Updates will propagate to all nodes *eventually*.
*   **Causal Consistency:** Causally related operations are seen in order.

---

## 587. What is strong vs eventual consistency?

**Answer:**
*   **Strong:** Higher latency (wait for replication), limits availability (if replica down, write fails). Good for Banking.
*   **Eventual:** Low latency (return immediately), high availability. Good for Social Media feeds (it's okay if a post appears 1s later).

---

## 588. What is horizontal scaling?

**Answer:**
**Horizontal Scaling (Scaling Out):**
*   **Action:** Adding more servers (nodes) to the cluster.
*   **Pros:** Theoretically infinite scaling, cheaper commodity hardware, better fault tolerance.
*   **Cons:** Complex (requires Load Balancer, distributed data handling).

---

## 589. What is vertical scaling?

**Answer:**
**Vertical Scaling (Scaling Up):**
*   **Action:** Upgrade the server (t2.micro -> t2.large).
*   **Pros:** Simple (no code change).
*   **Cons:** Hard limit (finite hardware capacity), Single Point of Failure, Expensive.

---

## 590. What is load balancing?

**Answer:**
**Load Balancing** distributes incoming network traffic across multiple servers (backend).
*   **Algorithms:** Round Robin, Least Connections, IP Hash.
*   **Layer 4 (L4):** Transport Layer (TCP/UDP) - Fast.
*   **Layer 7 (L7):** Application Layer (HTTP/HTTPS) - Smart (can route based on URL path).

---

## 591. Design URL shortener.

**Answer:**
*   **Core:** Map a long URL to a short alphanumeric key.
*   **Algorithm:** Base62 encoding of a unique Database ID (or Snowflake ID).
*   **Database:** NoSQL (DynamoDB/Cassandra) for high write throughput.
*   **Redirect:** HTTP 301 (Permanent) (if analytics not needed) or 302 (Found) (if analytics needed).
*   **Scale:** Cache hot URLs (Redis).

---

## 592. Design rate limiter.

**Answer:**
*   **Goal:** Prevent abuse.
*   **Algorithms:** Token Bucket, Leaky Bucket, Fixed Window, Sliding Window Log.
*   **Storage:** Redis (fast increment/read).
*   **Implementation:** Middleware or API Gateway (Kong/AWS API Gateway).
*   **Response:** HTTP 429 Too Many Requests.

---

## 593. Design notification system.

**Answer:**
*   **Core:** Decouple trigger from delivery.
*   **Flow:** Service A -> Kafka -> Notification Service -> 3rd Party (SendGrid/Twilio/FCM).
*   **Features:** User Preferences (Opt-out), Rate Limiting (Don't spam), Retry mechanism (Dead Letter Queue).

---

## 594. Design chat system.

**Answer:**
*   **Protocol:** WebSocket (Bi-directional, low latency).
*   **Storage:** Cassandra/HBase (Write-heavy, time-series data).
*   **Real-time:** Redis Pub/Sub to broadcast messages across WebSocket servers.
*   **Status:** User Presence (Online/Offline) via Heartbeats in Redis.

---

## 595. Design file storage system.

**Answer:**
*   **Core:** Like Google Drive/Dropbox.
*   **Storage:** Object Storage (S3) for files.
*   **Metadata:** SQL/NoSQL for file hierarchy (Parent ID), Owner, Permissions.
*   **Upload:** Generate Presigned URL so client uploads directly to S3 (offload traffic from server).
*   **Sync:** Block-level deduplication to save bandwidth.

---

## 596. Design payment system.

**Answer:**
*   **Key:** **Consistency** is paramount (ACID).
*   **Database:** SQL (PostgreSQL/Oracle) with Strong Consistency.
*   **Idempotency:** Ensure retries don't charge twice (Use unique `idempotency_key`).
*   **Distributed Transactions:** Two-Phase Commit (2PC) or Saga Pattern (Compensating transactions).
*   **Reconciliation:** Background job to verify internal DB vs Payment Gateway records.

---

## 597. Design logging system.

**Answer:**
*   **Collection:** Filebeat/Fluentd sidecars on pods.
*   **Aggregation:** Kafka (buffer logs during spikes).
*   **Indexing:** Elasticsearch (Searchable).
*   **Visualization:** Kibana.
*   **Retention:** Move old logs to S3 (Cold storage) to save costs.

---

## 598. Design API gateway.

**Answer:**
*   **Role:** Entry point for all client traffic.
*   **Features:** Authentication (JWT validation), Rate Limiting, Routing (Path-based), Protocol Translation (REST -> gRPC), Caching, Logging.
*   **Tools:** Netflix Zuul, Spring Cloud Gateway, Nginx, Kong.

---

## 599. Design distributed cache.

**Answer:**
*   **Algo:** Consistent Hashing to distribute keys across nodes.
*   **Eviction:** LRU (Least Recently Used), LFU.
*   **Consistency:** Cache-Aside (Lazy Loading) vs Write-Through vs Write-Back.
*   **Thundering Herd:** Use locking or random expiration times to prevent all keys expiring at once.

---

## 600. Design search service.

**Answer:**
*   **Core:** Inverted Index (Map words to document IDs).
*   **Tool:** Elasticsearch / Solr / Apache Lucene.
*   **Ingestion:** CDC (Change Data Capture) from main DB -> Kafka -> Elasticsearch.
*   **Query:** Support fuzzy search, synonyms, ranking algorithms (TF-IDF).

---

## 601. How to design high QPS system?

**Answer:**
1.  **Stateless:** Apps should be stateless to scale horizontally.
2.  **Caching:** Use Redis/Memcached to offload DB (Read-heavy).
3.  **Async:** Use Kafka/RabbitMQ to buffer writes (Write-heavy).
4.  **Database:** Sharding (Partition data) and Read Replicas.
5.  **CDN:** Serve static content from edge locations.

---

## 602. How to design id generation?

**Answer:**
Requirements: Unique, Numerical, Sortable by time.
1.  **UUID:** Simple, but not numerical/sortable, large (128-bit).
2.  **Database Auto-Increment:** Simple, but SPOF in distributed system.
3.  **Snowflake ID:** Distributed, unique, time-sortable, 64-bit long.

---

## 603. What is snowflake ID?

**Answer:**
Twitter's **Snowflake ID** is a 64-bit integer composed of:
*   **Sign bit:** 1 bit (unused).
*   **Timestamp:** 41 bits (milliseconds since epoch).
*   **Machine ID:** 10 bits (supports 1024 nodes).
*   **Sequence:** 12 bits (supports 4096 IDs per millisecond per node).

---

## 604. What is CDN?

**Answer:**
**CDN (Content Delivery Network)** is a network of geographically distributed servers that serve static content (Images, CSS, JS) to users from the nearest edge location.
*   **Benefits:** Lower latency, reduced load on origin server.
*   **Providers:** CloudFront, Akamai, Cloudflare.

---

## 605. What is reverse proxy?

**Answer:**
A **Reverse Proxy** sits between the client and the backend servers.
*   **Functions:** Load Balancing, SSL Termination, Caching, Compression (Gzip), Security (WAF).
*   **Examples:** Nginx, HAProxy.

---

## 606. What is caching strategy?

**Answer:**
1.  **Cache-Aside (Lazy Loading):** App checks cache -> Miss -> Read DB -> Update Cache. most common.
2.  **Read-Through:** App asks Cache -> Cache fetches from DB if miss.
3.  **Write-Through:** App writes to Cache -> Cache writes to DB (Safe but slow).
4.  **Write-Back:** App writes to Cache -> Cache writes to DB asynchronously (Fast but risk of data loss).

---

## 607. What is database scaling?

**Answer:**
1.  **Replication:** Master-Slave architecture. Master handles writes, Slaves handle reads.
2.  **Sharding:** Partitioning data across multiple databases (e.g., Users A-M on DB1, N-Z on DB2).
3.  **Federation:** Splitting tables by function (e.g., User DB, Order DB).

---

## 608. What is read-write separation?

**Answer:**
**Read-Write Separation** splits database traffic.
*   **Writes (INSERT/UPDATE/DELETE):** Go to **Master** node.
*   **Reads (SELECT):** Go to **Slave/Replica** nodes.
*   **Challenge:** Replication Lag (Slave might have stale data for a few ms).

---

## 609. What is queue-based architecture?

**Answer:**
Decoupling components using a Message Queue (Kafka/RabbitMQ).
*   **Scenario:** User uploads video -> **Frontend** pushes job to **Queue** -> **Worker** picks job and transcodes video.
*   **Benefit:** Frontend responds immediately ("Processing..."). Worker scales independently.

---

## 610. What is eventual consistency handling?

**Answer:**
How to deal with data that isn't consistent yet (in distributed systems).
1.  **Read-Your-Writes:** Ensure a user sees their own updates immediately (e.g., pin user to Master for 1 min after write).
2.  **Compensation:** If a background step fails (Saga), run a compensating transaction to undo previous steps.
3.  **Retry:** Idempotent retries for failed messages.

---

## 611. What is data partitioning?

**Answer:**
**Data Partitioning (Sharding)** splits a large dataset into smaller, manageable parts.
*   **Horizontal:** Split by rows (e.g., User ID 1-1000 in DB A, 1001-2000 in DB B).
*   **Vertical:** Split by columns (e.g., User Profile in DB A, User Photos in DB B).
*   **Methods:** Key-Based (Hash), Range-Based, Directory-Based.

---

## 612. What is consistent hashing?

**Answer:**
A technique to distribute keys across a dynamic set of nodes with minimal remapping.
*   **Circle:** Nodes are placed on a ring (0-360 degrees). Keys are hashed to the ring and assigned to the next clockwise node.
*   **Virtual Nodes:** Each physical node has multiple positions on the ring to ensure even distribution.
*   **Benefit:** Adding/Removing a node only affects its immediate neighbors.

---

## 613. What is distributed lock?

**Answer:**
Ensures that only one process across the entire distributed system can access a shared resource at a time.
*   **Tools:** specific tools like **Redis (Redlock)** or **Zookeeper**.
*   **Mechanism:** Acquire lock with TTL (Time To Live). If crash, lock expires automatically.

---

## 614. What is leader election?

**Answer:**
Process of designating a single node as the coordinator/master among a cluster of nodes.
*   **Why?** To avoid data conflicts (Split Brain) and coordinate tasks.
*   **Algorithms:** Paxos, Raft, Bully Algorithm.
*   **Tools:** Zookeeper (Ephemeral Nodes), Etcd.

---

## 615. What is quorum?

**Answer:**
**Quorum** is the minimum number of votes required to perform an operation (Read/Write) in a distributed system.
*   **Formula:** `N/2 + 1` (where N is total nodes).
*   **Example:** In a 5-node cluster, you need 3 successful writes to confirm a "Safe Write".

---

## 616. What is gossip protocol?

**Answer:**
A peer-to-peer communication protocol where nodes periodically share state information with random neighbors.
*   **Analogy:** Viral transmission of information.
*   **Use Case:** Cluster membership (Cassandra), Failure detection.

---

## 617. What is service discovery?

**Answer:**
Mechanism for services to find each other without hardcoding IPs.
1.  **Client-Side:** Client asks Registry (Eureka) for IP, then calls Service.
2.  **Server-Side:** Client calls Load Balancer (Nginx), LB asks Registry and forwards traffic.
*   **Tools:** Netflix Eureka, Consul, Zookeeper, K8s DNS.

---

## 618. What is circuit breaker pattern?

**Answer:**
Prevents an application from repeatedly trying to execute an operation that's likely to fail.
*   **States:**
    *   **Closed:** Requests pass through (Normal).
    *   **Open:** Requests fail immediately (Fast Fail) after threshold errors.
    *   **Half-Open:** Allow limited requests to test if backend is back up.
*   **Tools:** Resilience4j, Hystrix.

---

## 619. What is backpressure?

**Answer:**
A mechanism where a consumer signals the producer to slow down because it cannot keep up with the data rate.
*   **Reactive Streams:** `request(n)` method used to pull only `n` items.
*   **Without Backpressure:** Consumer buffer overflows -> OOM Crash.

---

## 620. What is retry strategy?

**Answer:**
Retrying failed operations to handle transient failures.
*   **Exponential Backoff:** Wait 1s, then 2s, then 4s...
*   **Jitter:** Add random noise to wait time to prevent "Thundering Herd" (all clients retrying at exact same time).
*   **Idempotency:** Ensure retries don't duplicate side effects.

---

## 621. Monitoring & observability in system design?

**Answer:**
**Observability** is how well you can understand the internal state of a system from its external outputs.
*   **Three Pillars:**
    1.  **Logs:** Application events ("User X logged in").
    2.  **Metrics:** Aggregated numbers (CPU usage, Request Count).
    3.  **Traces:** Request lifecycle across services (Zipkin/Jaeger).

---

## 622. How to handle failures?

**Answer:**
Assume everything will fail.
1.  **Fail Fast:** Don't wait for timeout if you know it will fail.
2.  **Fail Safe:** Return a default/fallback response instead of crashing.
3.  **Fail Over:** Switch to a backup server/DB.

---

## 623. How to design fault-tolerant system?

**Answer:**
A system that continues to operate (possibly at reduced level) when components fail.
*   **Redundancy:** Eliminate Single Points of Failure (SPOF) by adding backup nodes.
*   **Isolation:** Use Bulkhead pattern so one failing service doesn't crash others.
*   **Recovery:** Automated restarts (K8s) and data restoration from write-ahead logs.

---

## 624. What is SLA design?

**Answer:**
**Service Level Agreement (SLA):** Contract with users (e.g., 99.9% uptime).
*   **SLO (Objective):** Internal goal (e.g., 99.95%).
*   **SLI (Indicator):** Real metric measured (e.g., Actual Uptime = 99.92%).
*   **Design:** To meet high SLA, you need high redundancy and automatic failover.

---

## 625. What is high availability architecture?

**Answer:**
Architecture that ensures system is operational for a long period.
*   **Active-Active:** Traffic goes to both data centers. Instant failover. Complex data sync.
*   **Active-Passive:** Traffic goes to Primary. Secondary is standby. Slower failover (warm-up time).

---

## 626. What is replication strategy?

**Answer:**
Copying data to multiple machines for availability and durability.
1.  **Sync Replication:** Write to Master -> Write to Slave -> Ack Client. Safe but slow.
2.  **Async Replication:** Write to Master -> Ack Client -> Write to Slave. Fast but risk of data loss on crash.
3.  **Semi-Sync:** Write to Master -> Write to **one** Slave -> Ack.

---

## 627. How to reduce latency?

**Answer:**
1.  **CDN:** Move static content closer to user.
2.  **Caching:** Redis/Memcached.
3.  **Database Indexing:** Optimize queries.
4.  **Compression:** Gzip/Brotli payloads.
5.  **Protocol:** Use HTTP/2 or gRPC instead of HTTP/1.1.
6.  **Connection Pooling:** Reuse DB connections.

---

## 628. What is batching?

**Answer:**
Grouping multiple operations into a single unit of work.
*   **Use Case:** ETL jobs, Payroll processing, Report generation.
*   **Pros:** High throughput, efficient resource usage.
*   **Cons:** High latency (real-time is impossible).

---

## 629. What is streaming system?

**Answer:**
Processing data in real-time as it arrives.
*   **Tools:** Apache Kafka, Flink, Spark Streaming.
*   **Use Case:** Fraud detection, Live Dashboard, Log analysis.
*   **Pros:** Low latency.
*   **Cons:** Complex state management (handling late events).

---

## 630. What is event-driven architecture?

**Answer:**
Architecture where components communicate by producing and consuming events (decoupled).
*   **Producer:** Emits "OrderPlaced".
*   **Consumer:** Reacts (updates Inventory, sends Email).
*   **Broker:** Kafka/RabbitMQ mediates.
*   **Benefit:** Scalability, Decoupling, Async processing.

---

## 631. What are trade-offs in system design?

**Answer:**
There is no perfect design, only trade-offs.
*   **Consistency vs Availability:** (CAP Theorem).
*   **Latency vs Throughput:** Processing one by one (Low Latency) vs Batching (High Throughput).
*   **SQL vs NoSQL:** Structured/Joints vs Flexible/Scalable.
*   **Cost vs Performance:** SSD vs HDD, RAM vs Disk.

---

## 632. How to choose database?

**Answer:**
1.  **Structured Data + ACID?** -> RDBMS (PostgreSQL/MySQL).
2.  **Unstructured/JSON?** -> Document DB (MongoDB).
3.  **Key-Value / Caching?** -> Redis/DynamoDB.
4.  **High Write Throughput (Logs/IoT)?** -> Wide Column (Cassandra).
5.  **Graph Relationships?** -> Neo4j.

---

## 633. How to estimate capacity?

**Answer:**
Back-of-the-envelope calculations to size the system.
1.  **Traffic:** DAU (Daily Active Users), Reads/sec, Writes/sec.
2.  **Storage:** Data generated per user per day * Retention Period.
3.  **Bandwidth:** Inbound/Outbound network traffic.
4.  **Memory:** Cache size (e.g., 20% of hot data).

---

## 634. What is traffic estimation?

**Answer:**
Example: 10M DAU.
*   Each user does 5 requests/day.
*   Total Requests = 50M/day.
*   Seconds in day ≈ 86,400 (round to 100,000 for math).
*   **QPS (Queries Per Second)** = 50,000,000 / 100,000 = **500 QPS**.
*   **Peak QPS:** Usually 2x-5x average => 2,500 QPS.

---

## 635. What is storage estimation?

**Answer:**
Example: Instagram-like app.
*   New Photos: 10 QPS (Writes).
*   Size: 1 MB per photo.
*   Total per second: 10 MB/s.
*   Total per day: 10 MB * 86,400 ≈ **860 GB/day**.
*   Total for 10 years: 860 GB * 365 * 10 ≈ **3 PB (Petabytes)**.

---

## 636. How to design analytics system?

**Answer:**
*   **Ingestion:** Kafka (high throughput).
*   **Processing:** Spark Streaming / Flink (Real-time aggregation).
*   **Storage:** Data Lake (S3 - Raw), Data Warehouse (Snowflake/Redshift - Structured).
*   **Query:** Presto / Athena / ClickHouse (OLAP).

---

## 637. What is OLTP vs OLAP?

**Answer:**
*   **OLTP (Online Transaction Processing):**
    *   Row-oriented (MySQL/Postgres).
    *   Fast reads/writes for user-facing apps.
    *   Unit: Single Transaction.
*   **OLAP (Online Analytical Processing):**
    *   Column-oriented (Redshift/BigQuery).
    *   Complex queries/aggregations for BI/Reporting.
    *   Unit: Batch Analysis.

---

## 638. What is data pipeline?

**Answer:**
A set of automated processes that move data from source to destination.
*   **EtL (Extract, Transform, Load):** Transform before loading (Legacy/Warehouse).
*   **ELT (Extract, Load, Transform):** Load raw data first, then transform (Modern/Data Lake).
*   **Tools:** Apache Airflow (Orchestration).

---

## 639. What is data warehouse?

**Answer:**
A central repository of integrated data from one or more disparate sources, structured for query and analysis.
*   **Schema-on-Write:** Structure defined before data entry.
*   **Examples:** Snowflake, AWS Redshift, Google BigQuery.

---

## 640. What is data lake?

**Answer:**
A centralized repository that allows you to store all your structured and unstructured data at any scale.
*   **Schema-on-Read:** Structure defined when querying.
*   **Examples:** AWS S3, Azure Data Lake, Hadoop HDFS.

---

## 641. Security in system design?

**Answer:**
**Security** must be designed from the start ("Security by Design"), not added later.
*   **Authentication (AuthN):** Verify identity (Who are you?).
*   **Authorization (AuthZ):** Verify permissions (What can you do?).
*   **Data Protection:** Encryption at Rest (AES-256) and in Transit (TLS 1.3).
*   **Audit Logic:** Log who did what and when.

---

## 642. Rate limiting strategies?

**Answer:**
Techniques to control the rate of traffic sent or received.
1.  **User-Based:** Limit by User ID / API Key.
2.  **IP-Based:** Limit by IP address (can block NAT users).
3.  **Endpoint-Based:** Limit specific expensive APIs (`/report/generate`).
4.  **Geographic:** Limit traffic from specific regions.

---

## 643. Token bucket vs leaky bucket?

**Answer:**
*   **Token Bucket:**
    *   Tokens added at constant rate. Request consumes a token.
    *   **Pro:** Allows bursts of traffic (if bucket is full).
*   **Leaky Bucket:**
    *   Requests enter bucket. Leak (process) at constant rate.
    *   **Pro:** Smooths out traffic (constant outflow). No bursts.

---

## 644. What is zero trust architecture?

**Answer:**
A security model that assumes **no one** inside or outside the network is trusted by default.
*   **Principle:** "Never trust, always verify."
*   **Implementation:** mTLS between microservices, strict Identity verification for every request, no implicit trust based on network location (VPN).

---

## 645. What is OAuth2?

**Answer:**
**OAuth 2.0** is an authorization framework that enables apps to obtain limited access to user accounts on an HTTP service.
*   **Roles:** Resource Owner (User), Client (App), Authorization Server (Google/Okta), Resource Server (API).
*   **Flows:** Authorization Code (Server-side apps), Client Credentials (Service-to-Service), Implicit (Legacy).

---

## 646. What is JWT?

**Answer:**
**JSON Web Token (JWT)** is a compact, URL-safe means of representing claims to be transferred between two parties.
*   **Structure:** `Header.Payload.Signature`.
*   **Stateless:** Server doesn't store session; validates signature using secret/public key.
*   **Cons:** Can't revoke easily (needs blacklist/short expiry).

---

## 647. What is RBAC?

**Answer:**
**Role-Based Access Control (RBAC):** Permissions are assigned to **Roles** (Admin, Editor, Viewer), and Roles are assigned to **Users**.
*   **Simple:** Easy to manage for standard org structures.
*   **Example:** "Admins can delete users".

---

## 648. What is ABAC?

**Answer:**
**Attribute-Based Access Control (ABAC):** Permissions are granted based on **Attributes** (User, Resource, Environment).
*   **Dynamic:** "User can view document IF user.dept == doc.dept AND time is between 9am-5pm."
*   **Complex:** More granular than RBAC but harder to implement.

---

## 649. What is API throttling?

**Answer:**
**Throttling** is the intentional slowing down of a service to prevent overuse.
*   **Difference from Rate Limiting:**
    *   **Rate Limiting:** Rejects request (429) if limit exceeded.
    *   **Throttling:** Queues user requests or slows down response to smooth usage.

---

## 650. What is graceful degradation?

**Answer:**
The ability of a system to maintain limited functionality even when a large portion of it is destroyed or inoperative.
*   **Example:** If Recommendation Service fails, e-commerce site shows "Best Sellers" (static list) instead of "Recommended for You" (dynamic), rather than crashing the whole homepage.

---

## 651. What is Singleton?

**Answer:**
**Singleton Pattern** ensures a class has only one instance and provides a global point of access to it.
*   **Use Case:** Logging, Database Connection Pool, Configuration Manager.
*   **Implementation:** Private constructor, static instance, public static method to return instance.

---

## 652. Thread-safe Singleton?

**Answer:**
To make Singleton thread-safe:
1.  **Synchronized Method:** `public static synchronized getInstance()` (Performance hit).
2.  **Double-Checked Locking:** Check for null, synchronize block, check for null again. (Efficient).
3.  **Bill Pugh Singleton:** Use static inner Helper class (Lazy loading + Thread safe by JVM).
4.  **Enum Singleton:** `public enum Singleton { INSTANCE; }` (Simplest, handles serialization).

---

## 653. What is Factory pattern?

**Answer:**
**Factory Method Pattern** defines an interface for creating an object, but lets subclasses decide which class to instantiate.
*   **Goal:** Decouple object creation logic from client code.
*   **Example:** `ShapeFactory.getShape("CIRCLE")` returns `new Circle()`.

---

## 654. What is Abstract Factory?

**Answer:**
**Abstract Factory Pattern** provides an interface for creating families of related or dependent objects without specifying their concrete classes.
*   **Hierarchy:** Factory of Factories.
*   **Example:** `GUIFactory` -> `createButton()`, `createCheckbox()`.
    *   `WinFactory` returns `WinButton`.
    *   `MacFactory` returns `MacButton`.

---

## 655. What is Builder pattern?

**Answer:**
**Builder Pattern** separates the construction of a complex object from its representation.
*   **Use Case:** When an object has many optional parameters (telescoping constructor problem).
*   **Example:** `User.builder().firstName("John").age(30).build()`. (Lombok `@Builder`).

---

## 656. What is Prototype pattern?

**Answer:**
**Prototype Pattern** creates new objects by copying an existing object (Prototype).
*   **Use Case:** When object creation is expensive (e.g., DB call required).
*   **Implementation:** Implement `Cloneable` interface and override `clone()`.

---

## 657. What is Adapter?

**Answer:**
**Adapter Pattern** allows objects with incompatible interfaces to collaborate.
*   **Analogy:** Power adapter (US to EU plug).
*   **Implementation:** Create a class that implements the target interface and wraps the incompatible object (Adaptee).

---

## 658. What is Decorator?

**Answer:**
**Decorator Pattern** attaches new behaviors to objects by placing these objects inside special wrapper objects that contain the behaviors.
*   **Key:** Flexible alternative to subclassing for extending functionality.
*   **Example:** `new BufferedInputStream(new FileInputStream("file.txt"))`.

---

## 659. What is Facade?

**Answer:**
**Facade Pattern** provides a simplified interface to a library, a framework, or any other complex set of classes.
*   **Goal:** Hide complexity.
*   **Example:** `SLF4J` (Facade) vs `Log4j/Logback` (Implementation). A `Car` class that hides `Engine`, `Transmission` logic.

---

## 660. What is Proxy?

**Answer:**
**Proxy Pattern** provides a substitute or placeholder for another object to control access to it.
*   **Types:**
    *   **Lazy Initialization:** Create object only when needed.
    *   **Access Control:** Security check before actual method call.
    *   **Logging/Caching:** Wrap the real service.

---

## 661. What is Composite?

**Answer:**
**Composite Pattern** lets you compose objects into tree structures and then work with these structures as if they were individual objects.
*   **Analogy:** File System (Folder contains Files and Folders).
*   **Key:** Treat Leaf (File) and Composite (Folder) uniformly.

---

## 662. What is Bridge?

**Answer:**
**Bridge Pattern** splits a large class or a set of closely related classes into two separate hierarchies—abstraction and implementation—which can be developed independently.
*   **Goal:** Prefer Composition over Inheritance to avoid class explosion.
*   **Example:** `Shape` (Circle, Square) and `Color` (Red, Blue). Instead of `RedCircle`, `BlueSquare`, you have `Shape` holding a `Color` reference.

---

## 663. What is Flyweight?

**Answer:**
**Flyweight Pattern** lets you fit more objects into the available amount of RAM by sharing common parts of state between multiple objects instead of keeping all of the data in each object.
*   **Key:** Intrinsic State (Shared/Static) vs Extrinsic State (Unique/Context).
*   **Example:** `String` Pool in Java.

---

## 664. What is Observer?

**Answer:**
**Observer Pattern** defines a subscription mechanism to notify multiple objects about any events that happen to the object they're observing.
*   **Analogy:** Newsletter subscription / YouTube Channel Bell.
*   **Key:** Subject (Publisher) maintains a list of Observers (Subscribers) and calls `update()` on them.

---

## 665. What is Strategy?

**Answer:**
**Strategy Pattern** lets you define a family of algorithms, put each of them into a separate class, and make their objects interchangeable.
*   **Goal:** Switch algorithm at runtime.
*   **Example:** `Collections.sort(list, Comparator)`. The `Comparator` is the strategy. Payment methods (CreditCard, PayPal) in a checkout system.

---

## 666. What is Command?

**Answer:**
**Command Pattern** turns a request into a stand-alone object that contains all information about the request.
*   **Use Case:** Queueing operations, Undo/Redo functionality.
*   **Components:** Invoker (Remote), Command (TurnOn), Receiver (Light).

---

## 667. What is Template method?

**Answer:**
**Template Method Pattern** defines the skeleton of an algorithm in the superclass but lets subclasses override specific steps of the algorithm without changing its structure.
*   **Example:** `DataParser` class with `openFile()`, `parseData()`, `closeFile()`. Subclasses (`CSVParser`, `XMLParser`) override `parseData()`.

---

## 668. What is State?

**Answer:**
**State Pattern** lets an object alter its behavior when its internal state changes. It appears as if the object changed its class.
*   **Analogy:** Phone Buttons behave differently when Locked vs Unlocked.
*   **Implementation:** `Context` delegates work to current `State` object.

---

## 669. What is Chain of Responsibility?

**Answer:**
**Chain of Responsibility** passes requests along a chain of handlers. Upon receiving a request, each handler acts on it or passes it to the next.
*   **Example:** Filter Chain in Spring Security, Exception Handling (Try-Catch blocks).

---

## 670. What is Mediator?

**Answer:**
**Mediator Pattern** restricts direct communications between the objects and forces them to collaborate only via a mediator object.
*   **Goal:** Reduce coupling (Many-to-Many becomes One-to-Many).
*   **Analogy:** Air Traffic Controller. Pilots don't talk to each other; they talk to the Tower.

---

## 671. What is Visitor?

**Answer:**
**Visitor Pattern** lets you separate algorithms from the objects on which they operate.
*   **Use Case:** Adding new operations to existing class hierarchy without changing it.
*   **Mechanism:** Double Dispatch (`element.accept(visitor)` -> `visitor.visit(element)`).

---

## 672. What is Interpreter?

**Answer:**
**Interpreter Pattern** provides a way to evaluate language grammar or expressions.
*   **Use Case:** SQL parsers, Regulatory Expression engines, Mathematical expression evaluators.
*   **Structure:** TerminalExpression and NonTerminalExpression.

---

## 673. What is Memento?

**Answer:**
**Memento Pattern** lets you save and restore the previous state of an object without revealing the details of its implementation.
*   **Use Case:** "Undo" (Ctrl+Z) feature in text editors.
*   **Components:** Originator (saves state), Memento (stored state), Caretaker (manages history).

---

## 674. Which pattern used in Spring?

**Answer:**
1.  **Singleton:** Default scope for Beans.
2.  **Factory Method:** `BeanFactory` creating beans.
3.  **Proxy:** AOP (Aspect Oriented Programming), Transaction Management (`@Transactional`).
4.  **Template Method:** `JdbcTemplate`, `RestTemplate`.
5.  **Front Controller:** `DispatcherServlet` (Spring MVC).

---

## 675. Which pattern used in Hibernate?

**Answer:**
1.  **Factory:** `SessionFactory` creates `Session`.
2.  **Proxy:** Lazy loading of entities (Hibernate returns a proxy object first).
3.  **Unit of Work:** `Session` manages a list of changes to be committed.
4.  **Query Object:** `Criteria` API.

---

## 676. Which pattern used in Java Collections?

**Answer:**
1.  **Iterator:** `collection.iterator()` to traverse elements.
2.  **Decorator:** `Collections.synchronizedList(list)`, `Collections.unmodifiableList(list)`.
3.  **Adapter:** `Arrays.asList(array)` (Adapts Array to List interface).
4.  **Strategy:** `Collections.sort(list, comparator)`.

---

## 677. Real example of Strategy pattern?

**Answer:**
`java.util.Comparator`
```java
// Strategies
Comparator<User> byName = (a, b) -> a.getName().compareTo(b.getName());
Comparator<User> byAge = (a, b) -> a.getAge() - b.getAge();

// Context
Collections.sort(users, byName); // Use Name strategy
Collections.sort(users, byAge);  // Use Age strategy
```

---

## 678. Real example of Factory pattern?

**Answer:**
*   `java.util.Calendar.getInstance()`
*   `java.text.NumberFormat.getInstance()`
*   `java.nio.charset.Charset.forName("UTF-8")`
*   `SLF4J: LoggerFactory.getLogger(Class.class)`

---

## 679. Real example of Builder pattern?

**Answer:**
*   `java.lang.StringBuilder`: `new StringBuilder().append("a").append("b").toString()`
*   `java.util.stream.Stream.Builder`
*   **Lombok:** `@Builder` annotation generates a builder class automatically.

---

## 680. When not to use Singleton?

**Answer:**
1.  **Mutable State:** If the object holds state that shouldn't be shared globally.
2.  **Testing:** Hard to mock static instances (unless using PowerMock).
3.  **Tight Coupling:** Code depends on the concrete Singleton class.

---

## 681. Pattern vs anti-pattern?

**Answer:**
*   **Design Pattern:** A proven, reusable solution to a common problem (Good).
*   **Anti-Pattern:** A common response to a recurring problem that is usually ineffective and risks being highly counterproductive (Bad).
    *   **Examples:** God Object (Process huge class), Magic Numbers, Hardcoding, Spaghetti Code.

---

## 682. What is dependency inversion principle?

**Answer:**
**"D" in SOLID.**
High-level modules should not depend on low-level modules. Both should depend on abstractions.
*   **Bad:** `Car` depends on `GasEngine`.
*   **Good:** `Car` depends on `Engine` (Interface). `GasEngine` implements `Engine`.

---

## 683. What is SOLID principles?

**Answer:**
1.  **S - Single Responsibility:** Class should have one reason to change.
2.  **O - Open/Closed:** Open for extension, closed for modification.
3.  **L - Liskov Substitution:** Subtypes must be substitutable for base types.
4.  **I - Interface Segregation:** Client shouldn't depend on methods it doesn't use.
5.  **D - Dependency Inversion:** Depend on abstractions, not concretions.

---

## 684. What is microkernel pattern?

**Answer:**
**Microkernel Pattern (Plug-in Architecture)** separates a minimal core system from extended functionality.
*   **Core System:** Contains basic logic (lifecycle management).
*   **Plug-ins:** Add features and can be installed/uninstalled dynamically.
*   **Example:** Eclipse IDE, VS Code, Chrome Extensions.

---

## 685. What is CQRS?

**Answer:**
**Command Query Responsibility Segregation (CQRS)** separates read and write operations for a data store.
*   **Command:** Mutates state (Create, Update, Delete). No return value (void).
*   **Query:** Reads state. No side effects. Returns DTOs.
*   **Benefit:** Independently scale Read and Write models (e.g., Complex Write Logic vs Fast Read View).

---

## 686. What is Event sourcing?

**Answer:**
**Event Sourcing** stores the state of a business entity as a sequence of state-changing events.
*   **State:** Reconstructed by replaying all events from the beginning.
*   **Audit Trail:** Perfect history of "what happened" (Bank Ledger).
*   **Pairing:** Often used with CQRS.

---

## 687. What is Hexagonal architecture?

**Answer:**
**Hexagonal Architecture (Ports and Adapters)** aims to create loosely coupled application components that can be easily connected to their software environment by means of ports and adapters.
*   **Core:** Domain logic (Center).
*   **Ports:** Interfaces defining entry/exit points (API, Repository Interface).
*   **Adapters:** Implementation of ports (REST Controller, SQL Repository).
*   **Goal:** Test core logic without DB/UI.

---

## 688. What is Clean architecture?

**Answer:**
**Clean Architecture** (Robert C. Martin / Uncle Bob) organizes code into concentric circles, with the most stable rules at the center.
*   **Rule:** Dependencies only point inwards. Inner layers know nothing about outer layers.
*   **Layers:** Entities (Core) -> Use Cases -> Interface Adapters -> Frameworks & Drivers (DB, UI, Web).

---

## 689. What is layered architecture?

**Answer:**
**Layered Architecture (N-Tier)** organizes code into horizontal layers, each with a specific responsibility.
*   **Standard Layers:** Presentation -> Business/Service -> Persistence/DAO -> Database.
*   **Flow:** Requests flow down, responses flow up.
*   **Pros:** Simple, standard for small apps.
*   **Cons:** Tends to become a "Big Ball of Mud" or Anemic Domain Model.

---

## 690. What is DDD?

**Answer:**
**Domain-Driven Design (DDD)** is an approach to software development that centers the design on the deep understanding of the domain logic.
*   **Strategic:** Bounded Contexts, Ubiquitous Language.
*   **Tactical:** Entities, Value Objects, Aggregates, Repositories, Domain Events.

---

## 691. What is bounded context?

**Answer:**
**Bounded Context** is a central pattern in Domain-Driven Design (DDD). It defines the boundaries within which a particular domain model is valid and applicable.
*   **Example:** "User" means different things in the "Sales Context" (Customer) vs "Support Context" (Ticket Requester).
*   **Goal:** Prevent ambiguity and allow different teams to work on different contexts independently.

---

## 692. What is aggregate root?

**Answer:**
**Aggregate Root** is the main entity in a cluster of associated objects (Aggregate) that we treat as a unit for data changes.
*   **Rule:** External objects can hold references only to the Root, not to internal members.
*   **Example:** `Order` is the Root. `OrderItem` is internal. You delete `Order`, you delete all `OrderItems`.

---

## 693. What is repository pattern?

**Answer:**
**Repository Pattern** mediates between the domain and data mapping layers using a collection-like interface for accessing domain objects.
*   **Goal:** Decouple business logic from data access details (SQL, JPA).
*   **Interface:** `save(User)`, `findById(id)`, `findAll()`.

---

## 694. What is unit of work pattern?

**Answer:**
**Unit of Work Pattern** maintains a list of objects affected by a business transaction and coordinates the writing out of changes.
*   **Goal:** Ensure all changes are committed or rolled back as a single atomic unit.
*   **Implementation:** Hibernate `Session`, IPA `EntityManager`.

---

## 695. What is specification pattern?

**Answer:**
**Specification Pattern** allows encapsulation of business rules (validation, selection criteria) into boolean logic objects.
*   **Goal:** Reusable business rules.
*   **Example:** `UserIsActiveSpec.isSatisfiedBy(user)`. Can be chained: `ActiveSpec.and(PremiumSpec)`.

---

## 696. What is decorator vs proxy difference?

**Answer:**
*   **Decorator:** Adds **new functionality/behavior** to an object dynamically (e.g., adding a border to a window, adding buffering to a stream). Client knows it's being decorated.
*   **Proxy:** Controls **access** to an object (e.g., lazy loading, security check). Interface stays exactly the same. Client might not know it's using a proxy.

---

## 697. What is strategy vs state difference?

**Answer:**
*   **Strategy:** Client chooses the algorithm (strategy) to use (e.g., "Sort by Date"). "How to do something".
*   **State:** The object changes its behavior based on its internal state (e.g., "Order is Shipped" -> behaves differently). "What state am I in". Client usually doesn't manually set the state classes.

---

## 698. What is factory vs abstract factory difference?

**Answer:**
*   **Factory Method:** Creates **one** type of object (Product). Uses Inheritance (Subclasses decide).
*   **Abstract Factory:** Creates **families** of related objects (Chair, Sofa, Table). Uses Composition (Factory object passed to client).

---

## 699. What is builder vs factory difference?

**Answer:**
*   **Factory:** Creates an object in **one step**. Good for simple objects / hierarchies.
*   **Builder:** Creates an object in **multiple steps**. Good for complex objects with many optional parameters.

---

## 700. How to choose correct design pattern?

**Answer:**
1.  **Creation problem?** -> Creational (Factory, Builder, Singleton).
2.  **Structure/Assembly problem?** -> Structural (Adapter, Decorator, Facade).
3.  **Communication/Responsibility problem?** -> Behavioral (Observer, Strategy, Command).
*   *Tip:* Start simple. Don't force patterns. Refactor to patterns when "smells" or complexity arises.

---

## 701. What is unit testing?

**Answer:**
**Unit Testing** is a software testing method where individual units or components of a software are tested (in isolation) to validate that each unit performs as expected.
*   **Unit:** The smallest testable part of an application (e.g., a single method or class).
*   **Goal:** Isolate each part of the program and show that the individual parts are correct.

---

## 702. What is JUnit?

**Answer:**
**JUnit** is a unit testing framework for the Java programming language.
*   **Role:** Provides annotations and assertions to write and run repeatable tests.
*   **Integration:** Works with build tools (Maven, Gradle) and IDEs (IntelliJ, Eclipse).

---

## 703. JUnit 4 vs JUnit 5?

**Answer:**
*   **Architecture:** JUnit 5 = Platform + Jupiter (New API) + Vintage (Backwards compatibility).
*   **Annotations:**
    *   `@Before` -> `@BeforeEach`
    *   `@After` -> `@AfterEach`
    *   `@BeforeClass` -> `@BeforeAll`
    *   `@Ignore` -> `@Disabled`
*   **Features:** JUnit 5 supports Lambda expressions, nested tests, and dynamic tests.

---

## 704. What is @Test annotation?

**Answer:**
**`@Test`** marks a method as a test method.
*   **JUnit 4:** `org.junit.Test`.
*   **JUnit 5:** `org.junit.jupiter.api.Test`.
*   **Behavior:** The test runner executes any method annotated with `@Test`.

---

## 705. What is @BeforeEach and @AfterEach?

**Answer:**
*   **`@BeforeEach`:** Executed **before** each test method (e.g., setting up fresh data/mocks). Replaces `@Before`.
*   **`@AfterEach`:** Executed **after** each test method (e.g., cleaning up resources). Replaces `@After`.

---

## 706. What is parameterized test?

**Answer:**
Allows running the same test method multiple times with different arguments.
*   **Annotation:** `@ParameterizedTest` (JUnit 5).
*   **Source:** `@ValueSource`, `@CsvSource`, `@MethodSource`.
*   **Example:** Testing a `isPrime(int n)` method with values 2, 3, 5, 7, 11.

---

## 707. What is assertion?

**Answer:**
**Assertions** accept a boolean condition and throw an error if the condition is false (stopping the test).
*   **Class:** `org.junit.jupiter.api.Assertions`.
*   **Methods:** `assertEquals()`, `assertTrue()`, `assertNotNull()`, `assertThrows()` (Check for exceptions).

---

## 708. What is Mockito?

**Answer:**
**Mockito** is a mocking framework for unit tests in Java.
*   **Goal:** Simulate the behavior of dependencies (e.g., Database, External API) so you can test your service logic in isolation.
*   **Concept:** "Don't access the real DB, just pretend the DB returned this User."

---

## 709. What is @Mock and @InjectMocks?

**Answer:**
*   **`@Mock`:** Creates a mock object (dummy dependency). e.g., `UserRepository`.
*   **`@InjectMocks`:** Creates an instance of the class under test and injects the mocks into it. e.g., `UserService`.
*   **Usage:**
    ```java
    @Mock UserRepository userRepo;
    @InjectMocks UserService userService; // userService.userRepo will be the mock
    ```

---

## 710. What is stubbing?

**Answer:**
**Stubbing** defines the behavior of a mock object.
*   **Syntax:** `when(mock.method()).thenReturn(value);`
*   **Example:**
    ```java
    when(userRepo.findById(1)).thenReturn(Optional.of(new User("Alice")));
    ```
*   **Verification:** `verify(mock).method();` ensures a method was called.

---

## 711. What is verify in Mockito?

**Answer:**
**`verify()`** checks that a method was called with specific arguments on a mock object.
*   **Usage:** `verify(mock).save(user);`
*   **Counts:** `verify(mock, times(2)).call();`, `verify(mock, never()).call();`.
*   **Goal:** Ensure side effects (like sending email, saving to DB) happened.

---

## 712. What is spy vs mock?

**Answer:**
*   **Mock:** A completely dummy object. Methods do nothing (return null/default) unless stubbed.
    *   `@Mock`
*   **Spy:** A wrapper around a **real** object. Spies call real methods unless specifically stubbed.
    *   `@Spy`
    *   **Use Case:** Test a method of a class while mocking other methods of the **same** class.

---

## 713. What is BDD testing?

**Answer:**
**Behavior-Driven Development (BDD)** focuses on the behavior of the application from the end-user's perspective.
*   **Language:** Gherkin (Given, When, Then).
*   **Frameworks:** Cucumber, JBehave.
*   **Goal:** Collaboration between developers, QA, and business stakeholders.

---

## 714. What is TDD?

**Answer:**
**Test-Driven Development (TDD)** is a development process where you write tests **before** writing the actual code.
*   **Cycle:** Red (Write failing test) -> Green (Write minimal code to pass) -> Refactor (Clean up code).
*   **Benefit:** High test coverage, cleaner design, confidence in refactoring.

---

## 715. What is test coverage?

**Answer:**
**Test Coverage** is a metric that measures the amount of code executed by your tests.
*   **Types:** Line coverage, Method coverage, Branch coverage.
*   **Goal:** Identify untested parts of the application. High coverage != Bug-free code.

---

## 716. What is code coverage tools?

**Answer:**
Tools that generate coverage reports during the build process.
*   **Java:** JaCoCo (Java Code Coverage), Cobertura.
*   **Integration:** SonarQube visualizes coverage and sets quality gates (e.g., "Fail build if coverage < 80%").

---

## 717. What is branch coverage?

**Answer:**
**Branch Coverage** checks whether every execution path (branch) in a control structure (if, switch, loops) has been executed.
*   **Example:** For `if (A && B)`, verify tests cover:
    1.  A=true, B=true
    2.  A=false
    3.  A=true, B=false
*   **Significance:** Stronger metric than line coverage.

---

## 718. What is mutation testing?

**Answer:**
**Mutation Testing** evaluates the quality of your **tests** (not code) by introducing small bugs (mutations) into the code and checking if tests fail.
*   **Concept:** If a test passes despite a bug, the test is weak.
*   **Tool:** PITest (PIT).

---

## 719. What is integration testing?

**Answer:**
**Integration Testing** verifies that different modules or services work together correctly.
*   **Scope:** Larger than unit tests. Includes DB, Message Queues, External APIs (often using TestContainers).
*   **Speed:** Slower than unit tests.

---

## 720. What is @SpringBootTest?

**Answer:**
**`@SpringBootTest`** is an annotation for Spring Boot integration tests.
*   **Behavior:** Starts up the full Spring ApplicationContext (Ioc Container).
*   **Usage:** Used to test the interaction between multiple beans or the entire application flow.
*   **Web Environment:** Can mimic a web server using `webEnvironment = WebEnvironment.MOCK` or `RANDOM_PORT`.

---

## 721. What is @WebMvcTest?

**Answer:**
**`@WebMvcTest`** is a specialized test annotation for testing the Spring MVC Controller layer.
*   **Behavior:** Only scans for the Controller and related components (`@ControllerAdvice`, `Converter`, `Filter`). Access to Service/Repository layers must be mocked.
*   **Speed:** Faster than `@SpringBootTest` as it doesn't load whole context.

---

## 722. What is @DataJpaTest?

**Answer:**
**`@DataJpaTest`** is a specialized test annotation for testing the Persistence/Repository layer.
*   **Behavior:**
    *   Configures an in-memory embedded database.
    *   Scans for `@Entity` classes and configured Spring Data JPA repositories.
    *   Transactional (Rolls back at the end of each test).

---

## 723. What is MockMvc?

**Answer:**
**MockMvc** provides support for testing Spring MVC applications without starting a full HTTP server.
*   **Usage:** Perform requests and define expectations.
*   **Example:**
    ```java
    mockMvc.perform(get("/users/1"))
           .andExpect(status().isOk())
           .andExpect(jsonPath("$.name").value("Alice"));
    ```

---

## 724. What is TestRestTemplate?

**Answer:**
**`TestRestTemplate`** is a convenient alternative to `RestTemplate` for integration tests.
*   **Features:**
    *   Fault tolerant (doesn't throw exceptions on 4xx/5xx errors).
    *   Works well with `@SpringBootTest(webEnvironment = RANDOM_PORT)`.
    *   Great for end-to-end HTTP testing against a real server.

---

## 725. What is embedded database?

**Answer:**
An **Embedded Database** runs within the same JVM process as the application during tests.
*   **Examples:** H2, HSQLDB, Derby.
*   **Use Case:** Provides a clean, fast, temporary database for testing without needing an external MySQL/Postgres instance.

---

## 726. What is test profile?

**Answer:**
**Test Profile** allows you to define beans or configurations specifically for the "test" environment.
*   **Usage:** `@ActiveProfiles("test")` on the test class.
*   **Config:** `application-test.yml` (e.g., disable caching, use H2 DB, mock external URLs).

---

## 727. How to test async code?

**Answer:**
Testing `@Async` or `CompletableFuture` requires waiting for the thread to complete.
*   **Awaitility:** A library to express expectations of an asynchronous system in a concise and easy-to-read manner.
    ```java
    await().atMost(5, SECONDS).until(() -> service.getStatus() == "DONE");
    ```

---

## 728. How to test exception scenarios?

**Answer:**
1.  **JUnit 5:** `assertThrows(CustomException.class, () -> service.method());`
2.  **MockMvc:** `.andExpect(status().isBadRequest())` or `.andExpect(result -> assertTrue(result.getResolvedException() instanceof MyException))`.

---

## 729. How to test caching?

**Answer:**
To verify caching (`@Cacheable`), you need to check if the underlying method was called only once.
1.  Enable Caching in Test Config.
2.  Call method twice.
3.  `verify(repo, times(1)).findById(id);` -> If called only once, cache is working.

---

## 730. How to test Kafka listener?

**Answer:**
Use `@EmbeddedKafka` (from `spring-kafka-test`).
1.  **Setup:** `@EmbeddedKafka(partitions = 1, topics = { "test-topic" })`
2.  **Produce:** Send a message to the embedded broker using `KafkaTemplate`.
3.  **Verify:** Use strict waiting (Awaitility) to check if the Listener processed the message (e.g., side effect in DB or CountDownLatch).

---

## 731. What is Postman?

**Answer:**
**Postman** is a popular API client aimed at developers to create, share, test, and document APIs.
*   **Features:** Send requests, view responses, write tests in JavaScript, automate with Newman (CLI), mock servers.

---

## 732. What is RestAssured?

**Answer:**
**RestAssured** is a Java DSL (Domain Specific Language) for simplifying testing of REST based services.
*   **Usage:** Highly maintainable BDD-like syntax.
    ```java
    given().param("key", "value").when().get("/users").then().statusCode(200);
    ```

---

## 733. How to test REST APIs?

**Answer:**
1.  **Status Codes:** Verify 200 OK, 404 Not Found, 400 Bad Request, 500 Server Error.
2.  **Headers:** Check Content-Type, Authorization, Custom Headers.
3.  **Payload:** Validate JSON/XML body structure and data correctness.
4.  **Logic:** Test business rules (e.g., cannot delete active user).

---

## 734. What is contract testing?

**Answer:**
**Contract Testing** verifies that the interaction between two services (Consumer and Provider) adheres to a shared "contract".
*   **Goal:** Ensure that changes in the Provider don't break the Consumer.
*   **Focus:** Messages/API schema, not internal logic.

---

## 735. What is Pact?

**Answer:**
**Pact** is a code-first tool for testing HTTP and message integrations using contract tests.
*   **Consumer-Driven:** The consumer defines expectations (the pact).
*   **Verification:** The provider verifies it meets those expectations.

---

## 736. What is schema validation?

**Answer:**
**Schema Validation** ensures that the JSON/XML response matches a predefined structure (Schema).
*   **JSON Schema:** Defines field types, required fields, and constraints.
*   **RestAssured:** `body(matchesJsonSchemaInClasspath("schema.json"))`.

---

## 737. What is negative testing?

**Answer:**
**Negative Testing** ensures the application handles invalid input or unexpected user behavior gracefully.
*   **Examples:** Sending text in a numeric field, missing required headers, accessing unauthorized resources.
*   **Goal:** Verify proper Error Codes (4xx) and Error Messages.

---

## 738. What is performance testing?

**Answer:**
**Performance Testing** evaluates how a system performs in terms of responsiveness and stability under a particular workload.
*   **Types:** Load, Stress, Endurance, Spike, Volume, Scalability testing.

---

## 739. What is JMeter?

**Answer:**
**Apache JMeter** is a pure Java application designed to load test functional behavior and measure performance.
*   **Capabilities:** Simulate heavy load on a server, group of servers, network, or object to test its strength or to analyze overall performance under different load types.

---

## 740. What is load testing strategy?

**Answer:**
1.  **Baseline:** Test with normal load.
2.  **Spike:** Sudden burst of users.
3.  **Soak/Endurance:** Long duration (e.g., 24h) to find memory leaks.
4.  **Stress:** Test beyond breaking point to see how it fails (Graceful vs Crash).

---

## 741. What is test pyramid?

**Answer:**
**Test Pyramid** is a framework for balancing different types of tests.
1.  **Unit Tests (Base):** Fast, cheap, numerous. (70%)
2.  **Integration Tests (Middle):** Verify interactions. Slower. (20%)
3.  **E2E / UI Tests (Top):** Slow, expensive, fragile. Fewest. (10%)

---

## 742. What is flaky test?

**Answer:**
A **Flaky Test** is a test that sometimes passes and sometimes fails without any changes to the code.
*   **Causes:** Threading issues (race conditions), Network instability, Dependency on unpredictable data (Time, Random), Shared state.

---

## 743. How to reduce flaky tests?

**Answer:**
1.  **Isolation:** No shared state between tests.
2.  **Determinism:** Mock non-deterministic dependencies (Time, Random).
3.  **Wait Mechanisms:** Use dynamic waits (Awaitility) instead of `Thread.sleep()`.
4.  **Containerization:** Use TestContainers for consistent DB/Service environment.

---

## 744. What is mocking external services?

**Answer:**
When your service depends on a 3rd party API (e.g., Stripe, SendGrid), testing against the live API is slow, expensive, and flaky.
*   **Solution:** Create a mock server that simulates the external service's behavior (Stubbing).

---

## 745. What is WireMock?

**Answer:**
**WireMock** is a simulator for HTTP-based APIs.
*   **Usage:** Run a WireMock server in your test, match requests (URL, Method, Body), and return canned responses (Status 200, JSON Body).
*   **Goal:** Test your HTTP client logic without hitting the real internet.

---

## 746. What is TestContainers?

**Answer:**
**TestContainers** is a Java library that supports JUnit tests, providing lightweight, throwaway instances of common databases, Selenium web browsers, or anything else that can run in a Docker container.
*   **Code:** `new PostgreSQLContainer("postgres:15")`.
*   **Benefit:** Real integration test against a real DB (not H2), ensuring compatibility.

---

## 747. What is end-to-end testing?

**Answer:**
**End-to-End (E2E) Testing** validates the entire software flow from start to finish.
*   **Scope:** UI -> Backend -> Database -> 3rd Party.
*   **Tools:** Selenium, Cypress, Playwright.
*   **Goal:** Simulate real user scenarios (e.g., "User logs in, adds item to cart, pays").

---

## 748. What is CI testing?

**Answer:**
**Continuous Integration (CI) Testing** involves running automated tests every time code is committed to the repository.
*   **Pipeline:** build -> unit tests -> integration tests -> report.
*   **Goal:** Catch bugs early (Shift Left).

---

## 749. What is canary testing?

**Answer:**
**Canary Testing** involves rolling out a new version of the application to a small subset of users (Canaries) before a full rollout.
*   **Goal:** Verify reliability in production with minimal impact. If error rate rises, rollback immediately.

---

## 750. What is chaos testing?

**Answer:**
**Chaos Testing (Chaos Engineering)** involves intentionally injecting failures into a system to test its resilience.
*   **Tool:** Chaos Monkey.
*   **Actions:** Kill random pods, add network latency, simulate high CPU.
*   **Goal:** Ensure the system can withstand turbulent conditions in production.

---

## 751. What is fault injection?

**Answer:**
**Fault Injection** is a testing technique which aids in understanding how the system behaves when stressed or subjected to failure.
*   **Examples:** Introducing network latency, packet loss, or service crashes.
*   **Goal:** Improve system robustness and error handling.

---

## 752. What is regression testing?

**Answer:**
**Regression Testing** verifies that recent code changes have not adversely affected existing features.
*   **When:** After every deployment, bug fix, or feature addition.
*   **Automation:** Crucial for regression to be effective (too slow manually).

---

## 753. What is smoke testing?

**Answer:**
**Smoke Testing** (Build Verification Testing) determines if the deployed build is stable or not.
*   **Scope:** Covers critical paths (e.g., Application starts, Login works).
*   **Result:** Pass -> Continue testing. Fail -> Reject build immediately.

---

## 754. What is sanity testing?

**Answer:**
**Sanity Testing** is a subset of regression testing performed after a bug fix to verify that the specific issue is resolved and no related functionality is broken.
*   **Focus:** Narrower and deeper than smoke testing, but faster than full regression.

---

## 755. What is boundary value testing?

**Answer:**
**Boundary Value Analysis** tests the input values at the boundaries of the valid ranges.
*   **Theory:** Bugs are most likely to happen at boundaries (e.g., < 0, 0, 1, 99, 100, > 100).
*   **Example:** For age 18-65, test 17, 18, 19, 64, 65, 66.

---

## 756. What is equivalence partitioning?

**Answer:**
**Equivalence Partitioning** divides input data into partitions of valid and invalid values.
*   **Assumption:** All values in a partition behave similarly. If one works, all work.
*   **Example:** For age 18-65. Valid partition: 30. Invalid partitions: 10, 80.
*   **Goal:** Reduce number of test cases.

---

## 757. What is test data management?

**Answer:**
**Test Data Management (TDM)** involves planning, designing, storing, and managing data used for software testing.
*   **Challenges:** PII protection (masking), data consistency across environments, generating realistic volume.
*   **Tools:** Delphix, synthesized data scripts.

---

## 758. What is parallel test execution?

**Answer:**
**Parallel Test Execution** runs multiple tests simultaneously to reduce the overall execution time.
*   **JUnit 5:** Supports parallel execution config (`junit.jupiter.execution.parallel.enabled=true`).
*   **Risk:** Thread safety issues if tests share state (static variables, same DB rows).

---

## 759. How to test microservices?

**Answer:**
1.  **Unit:** Test internal logic of each service.
2.  **Contact:** Test API compatibility (Pact).
3.  **Integration:** Test service + DB/Broker (TestContainers).
4.  **Component:** Test service in isolation with mocks.
5.  **E2E:** Test flow across multiple services.

---

## 760. How to test distributed transactions?

**Answer:**
Testing **SAGA** or widespread transactions is complex.
*   **Focus:** Consistency and Compensation.
*   **Scenario:** Order Service -> Payment Service -> Inventory Service.
*   **Failure Test:** Simulate Payment failure and assert that Inventory is restored (Compensation triggered).
