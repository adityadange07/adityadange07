Here are the **Top 50 Core Java Interview Questions and Answers** tailored for someone with **5 years of experience**. These cover a range of **intermediate to advanced Core Java concepts** and are commonly asked in interviews.

---

### ✅ **Core Java Interview Questions for 5 Years Experience**

#### **1. What are the main features of Java?**
- Object-Oriented
- Platform Independent
- Robust and Secure
- High Performance (JIT)
- Multithreaded
- Automatic memory management via Garbage Collection

#### **2. Difference between JDK, JRE, and JVM?**
- **JVM**: Java Virtual Machine, runs Java bytecode.
- **JRE**: Java Runtime Environment, JVM + libraries.
- **JDK**: Java Development Kit, JRE + development tools.

#### **3. What is the difference between `==` and `.equals()`?**
- `==`: compares object references.
- `.equals()`: compares values (can be overridden).

#### **4. What is the difference between `HashMap` and `Hashtable`?**
- `HashMap` is not synchronized, allows `null` keys and values.
- `Hashtable` is synchronized, does not allow `null`.

#### **5. What are the access modifiers in Java?**
- `private`, `default`, `protected`, `public`

#### **6. Explain the concept of OOPs in Java.**
- **Encapsulation, Inheritance, Polymorphism, Abstraction**

#### **7. What is the difference between `Abstract class` and `Interface`?**
- Abstract class: can have constructor, state, and method implementations.
- Interface: pure abstraction until Java 8 (after which it can have default/static methods).

#### **8. What is method overloading and overriding?**
- **Overloading**: Same method name, different parameters (compile-time).
- **Overriding**: Subclass provides a specific implementation (runtime).

#### **9. What is the final keyword in Java?**
- Can be used with **variable (constant), method (no override), class (no subclass)**.

#### **10. What is a static keyword?**
- Belongs to the class rather than an instance.

---

#### **11. Difference between String, StringBuffer, and StringBuilder?**
- **String**: Immutable
- **StringBuffer**: Mutable and thread-safe
- **StringBuilder**: Mutable, not thread-safe (faster)

#### **12. What is Java Exception Handling?**
- Handling runtime errors using `try-catch-finally`, `throw`, `throws`.

#### **13. Difference between Checked and Unchecked Exceptions?**
- **Checked**: checked at compile time (IOException)
- **Unchecked**: at runtime (NullPointerException)

#### **14. What is a Java Package and its benefits?**
- Groups related classes and interfaces to avoid naming conflicts and control access.

#### **15. What is the difference between `this` and `super`?**
- `this`: refers to the current object
- `super`: refers to the parent class object

---

#### **16. What are wrapper classes in Java?**
- Convert primitives to objects: `int` -> `Integer`, etc.

#### **17. What is Autoboxing and Unboxing?**
- **Autoboxing**: Primitive to wrapper
- **Unboxing**: Wrapper to primitive

#### **18. Explain Garbage Collection in Java.**
- JVM automatically deallocates memory using GC. `System.gc()` can suggest it.

#### **19. What is the `transient` keyword?**
- Used to prevent serialization of a field.

#### **20. What is the `volatile` keyword?**
- Ensures visibility of changes to variables across threads.

---

#### **21. Explain Java Memory Model (Heap, Stack, etc.)**
- **Heap**: Objects
- **Stack**: Method calls, local variables
- **PermGen/MetaSpace**: Class metadata

#### **22. What is a class loader in Java?**
- Loads classes into memory during runtime.

#### **23. What is the Singleton design pattern?**
- Ensures only one instance of a class exists. Commonly used in caching, logging.

#### **24. Explain `equals()` and `hashCode()` contract.**
- If two objects are equal, they must have the same hashCode.

#### **25. Difference between Array and ArrayList?**
- Array is fixed size; ArrayList is resizable and part of the Collections framework.

---

#### **26. What is the use of `instanceof` keyword?**
- Checks if an object is an instance of a class or subclass.

#### **27. Explain the concept of immutability in Java.**
- Once created, object's state cannot be changed. E.g., `String`.

#### **28. What are functional interfaces?**
- Interfaces with a single abstract method (SAM). Used in Lambda expressions.

#### **29. What is a Lambda expression?**
- A concise way to represent functional interfaces using syntax like `(a, b) -> a + b`.

#### **30. What are Streams in Java 8?**
- Provides functional-style operations for processing sequences of elements.

---

#### **31. What is Optional in Java 8?**
- A container object that may or may not contain a non-null value. Prevents `NullPointerException`.

#### **32. Explain method reference in Java.**
- Used to refer to a method without executing it: `ClassName::methodName`.

#### **33. What is an Enum in Java?**
- Special class to represent constant values.

#### **34. Difference between `wait()`, `notify()`, and `notifyAll()`?**
- Used in multithreading for inter-thread communication.

#### **35. What is a deadlock in Java?**
- Two or more threads wait indefinitely for resources locked by each other.

---

#### **36. How to create a custom exception in Java?**
```java
public class MyException extends Exception { }
```

#### **37. What is the difference between `Comparable` and `Comparator`?**
- `Comparable`: natural order; single sort sequence
- `Comparator`: custom sort logic

#### **38. What is serialization in Java?**
- Converting an object into a byte stream for storage or transmission.

#### **39. What is the difference between `Collection` and `Collections`?**
- `Collection`: Interface
- `Collections`: Utility class with static methods

#### **40. What is the diamond problem in Java?**
- Multiple inheritance conflict. Solved using interfaces and default methods.

---

#### **41. What are generics in Java?**
- Provides compile-time type safety and reduces `ClassCastException`.

#### **42. What is reflection in Java?**
- Allows inspection and manipulation of classes, fields, methods at runtime.

#### **43. What is the use of `finalize()` method?**
- Called before garbage collection. Deprecated in Java 9+.

#### **44. What are the best practices for writing Java code?**
- Code conventions, exception handling, avoiding memory leaks, use logging frameworks.

#### **45. What is the difference between shallow copy and deep copy?**
- Shallow: copies references
- Deep: copies actual values

---

#### **46. How does Java achieve platform independence?**
- Compiles code into bytecode, which is interpreted by JVM on any OS.

#### **47. What is the marker interface in Java?**
- An empty interface used to signal special behavior (e.g., `Serializable`, `Cloneable`).

#### **48. What is the Thread Lifecycle in Java?**
- New → Runnable → Running → Blocked/Waiting → Terminated

#### **49. How to handle thread safety in Java?**
- Use `synchronized`, `Locks`, or concurrent collections.

#### **50. What is the difference between `ExecutorService` and `Thread`?**
- `ExecutorService`: manages thread pool, better resource management.
- `Thread`: manual thread creation.

---

Let me know if you want this as a **PDF**, or want **coding examples** with some of these questions. I can also give **Spring Boot** or **Microservices** questions next.