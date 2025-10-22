Here are the **Top 50 Core Java Interview Questions** for someone with **2 years of experience**. These cover key concepts that interviewers commonly ask and expect intermediate-level understanding of.

---

### ✅ **Core Java Interview Questions (with Answers)**

---

#### **1. What are the features of Java?**
- Object-Oriented, Platform Independent, Simple, Secure, Robust, Architecture-neutral, Portable, High Performance, Multithreaded, and Distributed.

---

#### **2. What is JVM, JRE, and JDK?**
- **JVM**: Java Virtual Machine – executes Java bytecode.
- **JRE**: Java Runtime Environment – JVM + libraries.
- **JDK**: Java Development Kit – JRE + development tools.

---

#### **3. What are the data types in Java?**
- **Primitive Types**: byte, short, int, long, float, double, boolean, char.
- **Non-Primitive**: String, Arrays, Classes, Interfaces.

---

#### **4. What is the difference between == and .equals()?**
- `==` compares **reference/memory address**.
- `.equals()` compares **actual content** (if overridden properly).

---

#### **5. What is the difference between final, finally, and finalize()?**
- `final`: keyword to restrict inheritance/override.
- `finally`: block that executes after try-catch.
- `finalize()`: method called by GC before object destruction.

---

#### **6. What is method overloading and method overriding?**
- **Overloading**: Same method name with different parameters in the same class.
- **Overriding**: Subclass modifies a method of the superclass.

---

#### **7. What is encapsulation?**
- Binding data and code into a single unit (class), and hiding internal details.

---

#### **8. What is inheritance?**
- Mechanism where one class inherits fields and methods from another.

---

#### **9. What is polymorphism?**
- Ability to take many forms. Two types: Compile-time (overloading), Runtime (overriding).

---

#### **10. What is abstraction?**
- Hiding internal implementation and showing only functionality.

---

#### **11. Difference between abstract class and interface?**
- **Abstract class**: Can have method implementations.
- **Interface**: All methods are abstract by default (until Java 8+ with default methods).

---

#### **12. What is a constructor?**
- Special method used to initialize objects.

---

#### **13. Can we overload constructors?**
- Yes, by defining multiple constructors with different parameter lists.

---

#### **14. What is the default constructor?**
- A no-argument constructor automatically provided if no constructors are defined.

---

#### **15. Can constructors be inherited?**
- No, constructors are not inherited.

---

#### **16. What is static in Java?**
- Static means the variable or method belongs to the class, not instances.

---

#### **17. Can a static method be overridden?**
- No, static methods are bound at compile time (method hiding).

---

#### **18. What is the main() method in Java?**
```java
public static void main(String[] args)
```
- Entry point for Java applications.

---

#### **19. What is the use of the ‘this’ keyword?**
- Refers to the current class instance.

---

#### **20. What is the use of the ‘super’ keyword?**
- Refers to the parent class instance.

---

#### **21. What is an object in Java?**
- An instance of a class.

---

#### **22. What are wrapper classes?**
- Classes that wrap primitive types (e.g., `Integer`, `Double`, etc.).

---

#### **23. What is autoboxing and unboxing?**
- **Autoboxing**: converting primitive to wrapper.
- **Unboxing**: converting wrapper to primitive.

---

#### **24. What is an exception?**
- An unwanted or unexpected event during program execution.

---

#### **25. Difference between checked and unchecked exceptions?**
- **Checked**: Checked at compile time (e.g., IOException).
- **Unchecked**: Checked at runtime (e.g., NullPointerException).

---

#### **26. What is try-catch-finally?**
- Used for exception handling in Java.

---

#### **27. Can we have multiple catch blocks?**
- Yes, to handle different types of exceptions.

---

#### **28. What is throw and throws?**
- **throw**: Used to explicitly throw an exception.
- **throws**: Used to declare exceptions.

---

#### **29. What is the difference between Array and ArrayList?**
- Array has a fixed size and holds primitives or objects.
- ArrayList is resizable and part of Java Collections.

---

#### **30. What is the difference between HashMap and Hashtable?**
- **HashMap** is not synchronized.
- **Hashtable** is synchronized and legacy.

---

#### **31. What is the Collection framework?**
- A unified architecture to store and manipulate groups of objects.

---

#### **32. Difference between List, Set, and Map?**
- **List**: Ordered, allows duplicates.
- **Set**: Unordered, no duplicates.
- **Map**: Key-value pairs, no duplicate keys.

---

#### **33. What is the difference between ArrayList and LinkedList?**
- **ArrayList**: Fast random access, slow insertion/deletion.
- **LinkedList**: Fast insertion/deletion, slow access.

---

#### **34. What is Iterator in Java?**
- Used to traverse collections.

---

#### **35. What is the difference between Iterator and ListIterator?**
- **Iterator**: Forward traversal.
- **ListIterator**: Both forward and backward traversal.

---

#### **36. What is synchronization?**
- Controlling access to shared resources by multiple threads.

---

#### **37. What is a thread in Java?**
- A thread is a lightweight process for multitasking.

---

#### **38. How to create a thread in Java?**
- By extending `Thread` or implementing `Runnable`.

---

#### **39. What is the lifecycle of a thread?**
- New → Runnable → Running → Waiting/Sleeping → Terminated

---

#### **40. What is the difference between wait() and sleep()?**
- `wait()` is used for thread communication (releases lock).
- `sleep()` pauses thread (does not release lock).

---

#### **41. What is deadlock?**
- When two or more threads are waiting for each other to release resources.

---

#### **42. What is the volatile keyword?**
- Ensures visibility of changes to variables across threads.

---

#### **43. What is transient keyword?**
- Prevents serialization of a variable.

---

#### **44. What is serialization in Java?**
- Converting an object into a byte stream.

---

#### **45. What is the singleton pattern?**
- Ensures a class has only one instance and provides global access.

---

#### **46. What are enums in Java?**
- A special class that represents a group of constants.

---

#### **47. What is garbage collection in Java?**
- Automatic memory management process to reclaim unused objects.

---

#### **48. What are the access modifiers in Java?**
- `private`, `default` (package-private), `protected`, `public`.

---

#### **49. What is the difference between == and equals() for strings?**
- `==` checks reference, `equals()` checks content.

---

#### **50. What is a functional interface?**
- An interface with only one abstract method, used in lambda expressions (e.g., Runnable, Comparator).

---

If you'd like, I can provide the **same set in a PDF**, or split these up into **mock interview sets** (like Round 1, Round 2, etc.). Want to continue with **Spring Boot** or another topic next?