# Design Patterns Interview Questions & Answers (Deep Dive)

## 1. Singleton (Thread-Safe & Reflection-Safe)
**The Problem:** Normal Singleton can be broken by Reflection (`setAccessible(true)`), Serialization (new object on deserialize), or Cloning.
**The Solution (Enum Singleton):**
```java
public enum Singleton {
    INSTANCE;
    public void doSomething() { ... }
}
```
**Why?** Java guarantees Enum instances are created only once (handled by JVM). Reflection cannot instantiate Enums. Serialization is handled automatically.

## 2. Factory vs Abstract Factory
- **Factory Method:** Defines an interface for creating *one* object. (e.g., `CarFactory` -> `Sedan`, `SUV`).
- **Abstract Factory:** Creates *families* of related objects. (e.g., `GUIToolkit` -> `CreateButton`, `CreateScrollbar`).
    - WindowsToolkit -> WindowsButton, WindowsScrollbar.
    - MacToolkit -> MacButton, MacScrollbar.

## 3. Proxy Pattern (Spring AOP Internals)
**Scenario:** You annotate a method with `@Transactional`. How does Spring intercept the call?
**Proxy:** Spring wraps your bean in a Proxy.
1.  **JDK Dynamic Proxy:** Used if class implements Interface. Uses Reflection.
2.  **CGLIB (Code Generation Library):** Used if class is concrete (no interface). Creates a subclass at runtime and overrides methods.
**Self-Invocation Issue:**
If method A calls method B (both in same class), and B is `@Transactional`, the transaction **won't work**.
*Reason:* Use `this.B()` calls the actual object method, bypassing the Proxy.

## 4. Observer Pattern vs Pub-Sub
- **Observer:** Subject knows its observers. Synchronous (usually). Tight coupling (Memory references).
- **Pub-Sub:** Publisher doesn't know Subscriber. Asynchronous. Loose coupling (via Message Broker like Kafka).

## 5. SOLID Principles (Deep Dive)
- **Liskov Substitution Principle (LSP):**
    - *Definition:* If S is a subtype of T, objects of T may be replaced with S without breaking the program.
    - *Violation:* `Rectangle` class with `setWidth`. `Square` extends `Rectangle`. Setting width of Square changes height too. `area()` calculation breaks for code expecting Rectangle behavior.
    - *Fix:* Use separate shapes or immutable objects.
- **Dependency Inversion Principle (DIP):**
    - High-level modules (Business Logic) should not depend on low-level modules (Database Driver). Both should depend on Abstractions (Interfaces).
    - *Example:* `Service` -> depends on `Repository Interface` (not `MySQLRepository` class).

## 6. Adapter vs Decorator vs Facade
- **Adapter:** Changes the interface (Square peg -> Round hole).
- **Decorator:** Adds features (Coffee -> Coffee + Milk + Sugar). Same interface.
- **Facade:** Simplifies interface (Complex Library -> Simple `Library.init()` method).

## 7. Strategy Pattern (Real World)
**Spring:** `Resource` interface. `UrlResource`, `ClassPathResource`, `FileSystemResource`.
**Java:** `Collections.sort(list, Comparator)`. The Comparator is the Strategy.
- Removes `if-else` blocks (e.g., `if type==CreditCard`). Replaces with polymorphic dispatch map: `strategies.get(type).pay()`.
