
Here are the **Top 50 Core Java Interview Questions and Answers** tailored for someone with **4 years of experience**. These questions are a mix of theory and practical understanding, commonly asked in real interviews.

---

### ✅ **1. What are the main features of Java?**
- Platform Independent, Object-Oriented, Robust, Secure, Multithreaded, High Performance (JIT), Distributed.

---

### ✅ **2. Explain the Java memory model.**
- Divided into Heap (Objects), Stack (method calls, local variables), Method Area (class metadata), PC Register, and Native Method Stack.

---

### ✅ **3. What is the difference between JDK, JRE, and JVM?**
- **JDK**: Java Development Kit (includes JRE + compiler + tools)
- **JRE**: Java Runtime Environment (JVM + libraries)
- **JVM**: Java Virtual Machine (executes bytecode)

---

### ✅ **4. What are wrapper classes in Java?**
- They convert primitives to objects (autoboxing/unboxing).  
  E.g., `int → Integer`, `double → Double`

---

### ✅ **5. Difference between `==` and `.equals()`?**
- `==`: Checks reference equality
- `.equals()`: Checks value/content equality (can be overridden)

---

### ✅ **6. What is a constructor? Can we override it?**
- A constructor initializes objects. It **cannot be overridden** (not inherited).

---

### ✅ **7. What is method overloading and overriding?**
- **Overloading**: Same method name, different parameters (compile-time polymorphism)
- **Overriding**: Subclass provides specific implementation (runtime polymorphism)

---

### ✅ **8. Can we override a static method?**
- No, static methods belong to the class. It’s **method hiding**, not overriding.

---

### ✅ **9. What is the difference between `final`, `finally`, and `finalize()`?**
- `final`: Constant or prevent inheritance
- `finally`: Executes regardless of exception
- `finalize()`: Cleanup before GC (deprecated in Java 9+)

---

### ✅ **10. What is a Java package?**
- A namespace to group related classes and interfaces. Helps in code organization.

---

### ✅ **11. Explain access modifiers in Java.**
- `private` < `default` < `protected` < `public`

---

### ✅ **12. What is the use of the `this` keyword?**
- Refers to the current object of a class.

---

### ✅ **13. What is the use of `super` keyword?**
- Refers to parent class constructor/method/variable.

---

### ✅ **14. What is the difference between `ArrayList` and `LinkedList`?**
- **ArrayList**: Fast for indexing, slow for insertion/deletion.
- **LinkedList**: Slow for indexing, fast for insertion/deletion.

---

### ✅ **15. Difference between `HashMap` and `Hashtable`?**
- `HashMap`: Not thread-safe, allows null key/value
- `Hashtable`: Thread-safe (synchronized), no null key/value

---

### ✅ **16. What is the difference between `HashMap` and `ConcurrentHashMap`?**
- `ConcurrentHashMap` is thread-safe and uses segment locking.

---

### ✅ **17. Explain `fail-fast` vs `fail-safe` iterators.**
- **Fail-fast**: Throws `ConcurrentModificationException` (`ArrayList`, `HashMap`)
- **Fail-safe**: Works on cloned data (`ConcurrentHashMap`, `CopyOnWriteArrayList`)

---

### ✅ **18. How does Java achieve platform independence?**
- Java code is compiled to **bytecode**, which runs on any **JVM**.

---

### ✅ **19. What is abstraction in Java?**
- Hiding internal details and showing essential features using abstract classes or interfaces.

---

### ✅ **20. Difference between abstract class and interface (Java 8+)?**
- Abstract class can have constructor and state.
- Interface can have default/static methods (since Java 8), but no state.

---

### ✅ **21. What is the use of `volatile` keyword?**
- Ensures visibility of changes across threads.

---

### ✅ **22. What is the difference between `synchronized` and `Lock`?**
- `synchronized` is implicit.
- `Lock` (from `java.util.concurrent.locks`) provides more flexibility like tryLock(), fairness, etc.

---

### ✅ **23. What is a thread in Java?**
- A lightweight sub-process managed by JVM to perform multitasking.

---

### ✅ **24. Difference between process and thread?**
- Process: Independent, has its own memory.
- Thread: Part of process, shares memory.

---

### ✅ **25. How do you create a thread in Java?**
- Extend `Thread` or implement `Runnable`.

---

### ✅ **26. What is the thread lifecycle in Java?**
- New → Runnable → Running → Waiting/Blocked → Terminated

---

### ✅ **27. What is synchronization?**
- Prevents thread interference and ensures memory consistency using `synchronized` keyword.

---

### ✅ **28. Difference between `wait()` and `sleep()`?**
- `wait()`: Releases lock, must be in synchronized block.
- `sleep()`: Holds the lock.

---

### ✅ **29. What is the difference between `Comparable` and `Comparator`?**
- `Comparable`: natural ordering (`compareTo`)
- `Comparator`: custom ordering (`compare`)

---

### ✅ **30. What are functional interfaces?**
- Interfaces with a single abstract method (SAM).  
  E.g., Runnable, Callable, Comparable, etc.

---

### ✅ **31. What is a lambda expression?**
- A concise way to write anonymous functions using `->` (Java 8+)

---

### ✅ **32. What is Stream API in Java 8?**
- Provides functional operations like `map()`, `filter()`, `collect()` for data processing.

---

### ✅ **33. What is Optional in Java 8?**
- A container to avoid `NullPointerException`. It handles nulls gracefully.

---

### ✅ **34. Difference between checked and unchecked exceptions?**
- **Checked**: Must be handled or declared (IOException)
- **Unchecked**: Runtime exceptions (NullPointerException)

---

### ✅ **35. What is the purpose of `try-with-resources`?**
- Automatically closes resources implementing `AutoCloseable`.

---

### ✅ **36. What is garbage collection in Java?**
- JVM automatically removes unreferenced objects to free memory.

---

### ✅ **37. Explain Java class loading mechanism.**
- **ClassLoader** → **Bytecode Verifier** → **Runtime Data Areas** → **Execution**

---

### ✅ **38. What is reflection in Java?**
- Allows runtime inspection and modification of classes, methods, fields.

---

### ✅ **39. What is a Singleton class?**
- A class with only one instance using a private constructor and a static method.

---

### ✅ **40. How to create immutable class in Java?**
- Use `final`, private fields, no setters, defensive copies.

---

### ✅ **41. What are enums in Java?**
- Special class with a fixed set of constants.

---

### ✅ **42. What is a marker interface?**
- An interface with no methods (e.g., Serializable, Cloneable)

---

### ✅ **43. What are annotations in Java?**
- Metadata about code used for compiler instructions or runtime processing.

---

### ✅ **44. What is serialization?**
- Converts object state to a byte stream to save or transmit.

---

### ✅ **45. Difference between `String`, `StringBuffer`, and `StringBuilder`?**
- `String`: Immutable
- `StringBuffer`: Mutable, thread-safe
- `StringBuilder`: Mutable, not thread-safe

---

### ✅ **46. What is method reference in Java 8?**
- A shorthand for lambda calling a specific method.  
  Syntax: `ClassName::methodName`

---

### ✅ **47. What are default and static methods in interface (Java 8)?**
- Interface can have default behavior (default method) and static utility methods.

---

### ✅ **48. What is the diamond problem and how does Java handle it?**
- With multiple inheritance via interfaces, Java uses method resolution order.

---

### ✅ **49. What is the difference between strong, soft, weak, and phantom references?**
- Types used in GC. `WeakReference` objects are GC'ed earlier than `SoftReference`.

---

### ✅ **50. How does `hashCode()` and `equals()` work in collections like HashMap?**
- `hashCode()` locates the bucket, `equals()` checks equality inside the bucket.

---

Would you like a **PDF** version of this? Or want me to move to the **next topic** like **Spring Boot** or **Microservices** next?