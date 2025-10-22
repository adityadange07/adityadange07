Here are the **Top 50 Core Java Interview Questions with Answers** tailored for someone with **3 years of experience**. These cover key concepts that are often asked in interviews at that level:

---

### ✅ **1. What are the main features of Java?**
- Object-Oriented, Platform Independent, Simple, Secure, Robust, Multithreaded, High Performance (JIT), Portable.

---

### ✅ **2. What is the difference between JDK, JRE, and JVM?**
- **JDK (Java Development Kit):** Includes JRE + development tools (compiler, debugger).
- **JRE (Java Runtime Environment):** JVM + libraries for running Java apps.
- **JVM (Java Virtual Machine):** Executes Java bytecode and provides platform independence.

---

### ✅ **3. What is the difference between == and `.equals()` in Java?**
- `==` compares object **references**, `.equals()` compares object **values** (if overridden).

---

### ✅ **4. What is a Class and an Object?**
- **Class:** Blueprint for objects.
- **Object:** Instance of a class with state and behavior.

---

### ✅ **5. What is the purpose of the `static` keyword in Java?**
- Belongs to the class, not instances. Shared across all objects. Used for methods, variables, and blocks.

---

### ✅ **6. What are the different types of memory areas allocated by JVM?**
- Method Area, Heap, Stack, Program Counter Register, Native Method Stack.

---

### ✅ **7. What is the difference between Heap and Stack memory?**
- **Heap:** Stores objects; shared memory.
- **Stack:** Stores method calls, local variables; per thread.

---

### ✅ **8. What is method overloading and overriding?**
- **Overloading:** Same method name, different parameters (compile-time).
- **Overriding:** Subclass provides specific implementation of a superclass method (run-time).

---

### ✅ **9. Can you override a static method?**
- No, static methods belong to the class, not objects. You can **hide**, but not **override** them.

---

### ✅ **10. What is constructor chaining?**
- Calling one constructor from another using `this()` or `super()`.

---

### ✅ **11. What are the types of constructors in Java?**
- Default constructor, Parameterized constructor, Copy constructor (custom).

---

### ✅ **12. What is the difference between `final`, `finally`, and `finalize()`?**
- **final:** Keyword to restrict (no modification).
- **finally:** Block used for cleanup.
- **finalize():** Method called by GC before object removal (deprecated).

---

### ✅ **13. What is the difference between abstract class and interface?**
| Feature          | Abstract Class       | Interface             |
|------------------|----------------------|------------------------|
| Inheritance      | Single               | Multiple              |
| Methods          | Can have both        | Only abstract (Java 7)|
| Variables        | Instance vars        | Only constants         |

---

### ✅ **14. What is the difference between `this` and `super`?**
- `this`: Refers to current class instance.
- `super`: Refers to parent class.

---

### ✅ **15. What is polymorphism in Java?**
- Ability to take many forms. Two types:
    - Compile-time (method overloading)
    - Runtime (method overriding)

---

### ✅ **16. What is encapsulation?**
- Wrapping data and code into a single unit and restricting access using access modifiers.

---

### ✅ **17. What is inheritance in Java?**
- Acquiring properties and behavior from another class using `extends` or `implements`.

---

### ✅ **18. What is abstraction?**
- Hiding implementation details and showing only functionality.

---

### ✅ **19. What is a marker interface?**
- An interface with no methods or fields, e.g., `Serializable`.

---

### ✅ **20. What is the use of the `transient` keyword?**
- Prevents serialization of a field.

---

### ✅ **21. What is the purpose of `volatile` keyword?**
- Ensures visibility of changes to variables across threads.

---

### ✅ **22. What is synchronization in Java?**
- Controlling access of multiple threads to shared resources.

---

### ✅ **23. What is the difference between `wait()`, `sleep()`, and `join()`?**
- `wait()`: Releases lock, pauses thread until `notify()`.
- `sleep()`: Pauses thread but holds lock.
- `join()`: Waits for a thread to die.

---

### ✅ **24. What is a thread?**
- A lightweight subprocess or smallest unit of execution.

---

### ✅ **25. How can you create a thread in Java?**
- Extending `Thread` class or implementing `Runnable` interface.

---

### ✅ **26. What are Checked and Unchecked exceptions?**
- **Checked:** Checked at compile time (IOException).
- **Unchecked:** Occur at runtime (NullPointerException).

---

### ✅ **27. What is the difference between `throw` and `throws`?**
- `throw`: Used to explicitly throw an exception.
- `throws`: Declares exceptions in method signature.

---

### ✅ **28. What is the use of `instanceof` keyword?**
- Checks whether an object is an instance of a specific class.

---

### ✅ **29. What are wrapper classes in Java?**
- Convert primitives to objects (int → Integer, etc.).

---

### ✅ **30. What is autoboxing and unboxing?**
- Autoboxing: Primitive to wrapper.
- Unboxing: Wrapper to primitive.

---

### ✅ **31. What are access modifiers in Java?**
- **private**, **default**, **protected**, **public** – define access scope.

---

### ✅ **32. What is the difference between Array and ArrayList?**
- Array: Fixed size, supports primitives.
- ArrayList: Resizable, only holds objects.

---

### ✅ **33. What is the `StringBuilder` and `StringBuffer` difference?**
- **StringBuilder:** Non-thread-safe, faster.
- **StringBuffer:** Thread-safe, slower.

---

### ✅ **34. What is immutability in Strings?**
- Once created, a `String` object cannot be changed.

---

### ✅ **35. Why is String immutable in Java?**
- For security, synchronization, caching, and performance.

---

### ✅ **36. What is the use of `hashCode()` and `equals()`?**
- Used in collections like `HashMap` to identify and compare objects.

---

### ✅ **37. What are common interfaces in the Java Collections Framework?**
- List, Set, Map, Queue, Deque, Collection.

---

### ✅ **38. Difference between HashMap and Hashtable?**
- HashMap: Non-synchronized, allows nulls.
- Hashtable: Synchronized, no null keys or values.

---

### ✅ **39. What is the difference between ArrayList and LinkedList?**
- ArrayList: Fast access, slow insertion/removal.
- LinkedList: Fast insertion/removal, slow access.

---

### ✅ **40. What is the fail-fast and fail-safe iterator?**
- **Fail-fast:** Throws `ConcurrentModificationException`.
- **Fail-safe:** Doesn’t throw, works on cloned collection (e.g., `CopyOnWriteArrayList`).

---

### ✅ **41. What is the difference between Iterator and ListIterator?**
- **Iterator:** Only forward traversal.
- **ListIterator:** Bi-directional.

---

### ✅ **42. How is memory managed in Java?**
- Through automatic Garbage Collection.

---

### ✅ **43. What are functional interfaces?**
- Interface with a single abstract method (e.g., Runnable, Callable).

---

### ✅ **44. What are lambda expressions?**
- Syntax: `(args) -> expression`
- Used for functional programming and concise code.

---

### ✅ **45. What is the Stream API?**
- Introduced in Java 8 for functional-style operations on collections.

---

### ✅ **46. What is the Optional class in Java 8?**
- Used to avoid `NullPointerException` by wrapping values.

---

### ✅ **47. What are default and static methods in interfaces?**
- Java 8 feature to define methods with body in interfaces.

---

### ✅ **48. What is the diamond problem? Does Java support multiple inheritance?**
- Diamond problem occurs in multiple inheritance; Java solves it using interfaces.

---

### ✅ **49. What is the difference between `Comparable` and `Comparator`?**
- **Comparable:** Natural order, single sort.
- **Comparator:** Custom multiple sort strategies.

---

### ✅ **50. What are enums in Java?**
- Special class representing a group of constants.

---

Let me know if you'd like these in a **PDF format** or if you want the next topic (like Spring Boot, Microservices, etc.).