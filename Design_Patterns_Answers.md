# Design Patterns & SOLID Principles Interview Questions & Answers

## 1. Singleton Pattern
**Detailed Explanation**: Ensures that a class has only **one instance** and provides a global point of access to it.
*   **Usage**: Logging, Database Connection, Configuration settings.
*   **Breaking Singleton**: Reflection, Serialization, Cloning.
*   **Best Implementation**: Enums (Safe from Reflection/Serialization).

**Example**:
```java
// Thread-Safe Singleton
public class Database {
    private static Database instance;
    private Database() {} // Private Constructor

    public static synchronized Database getInstance() {
        if (instance == null) {
            instance = new Database();
        }
        return instance;
    }
}

// Enum Singleton (Best)
public enum DatabaseEnum {
    INSTANCE;
    public void connect() { ... }
}
```

---

## 2. Factory Pattern
**Detailed Explanation**: Creates objects without exposing the instantiation logic to the client. Copier refers to newly created object through a common interface.
*   **Concept**: A Factory Class deciding which subclass to instantiate based on input.

**Example**:
```java
interface Shape { void draw(); }
class Circle implements Shape { public void draw() { ... } }
class Square implements Shape { public void draw() { ... } }

class ShapeFactory {
    public Shape getShape(String type) {
        if (type.equals("CIRCLE")) return new Circle();
        if (type.equals("SQUARE")) return new Square();
        return null;
    }
}
```

---

## 3. Builder Pattern
**Detailed Explanation**: Used to construct a complex object step by step. It separates construction from representation.
*   **Usage**: When an object has 10+ parameters, and many are optional. Avoids "Telescoping Constructor Anti-pattern".

**Example**:
```java
User user = new User.UserBuilder("John", "Doe")
    .age(30)
    .phone("1234567")
    // .address("...") // Optional, skipped
    .build();
```

---

## 4. Strategy Pattern
**Detailed Explanation**: Defines a family of algorithms, encapsulates each one, and makes them interchangeable at runtime.
*   **Usage**: Payment strategies (Credit Card, PayPal, Google Pay).

**Example**:
```java
interface PaymentStrategy { void pay(int amount); }

class CreditCardStrategy implements PaymentStrategy { ... }
class PayPalStrategy implements PaymentStrategy { ... }

class ShoppingCart {
    void pay(PaymentStrategy strategy) {
        strategy.pay(totalAmount);
    }
}
```

---

## 5. Observer Pattern
**Detailed Explanation**: Defines a one-to-many dependency so that when one object (Subject) changes state, all its dependents (Observers) are notified automatically.
*   **Usage**: Event Handling, YouTube Channel (Subject) -> Subscribers (Observers).

**Example**:
```java
class Channel {
    List<Subscriber> subs = new ArrayList<>();
    void upload(String video) {
        for(Subscriber s : subs) s.notify(video);
    }
}
```

---

## 6. Adapter vs Decorator Pattern
**Detailed Explanation**:
*   **Adapter**: Makes two incompatible interfaces work together. (Like a Travel Power Adapter).
    *   *Goal*: Convert Interface A to Interface B.
*   **Decorator**: Adds new functionality to an existing object dynamically without altering its structure. (Like adding toppings to Pizza).
    *   *Goal*: Enhance/Extend behavior.

---

## 7. SOLID Principles
**Detailed Explanation**:
1.  **S - Single Responsibility Principle (SRP)**: A class should have only one reason to change (Do one job).
2.  **O - Open/Closed Principle (OCP)**: Open for extension, Closed for modification. (Use Inheritance/Interfaces, don't change existing code).
3.  **L - Liskov Substitution Principle (LSP)**: Child classes must be substitutable for their parent classes without breaking the app.
4.  **I - Interface Segregation Principle (ISP)**: Many specific interfaces are better than one general-purpose interface.
5.  **D - Dependency Inversion Principle (DIP)**: Depend on abstractions (Interfaces), not concretions (Classes).

---

## 8. Proxy Pattern
**Detailed Explanation**: Provides a placeholder for another object to control access to it.
*   **Types**:
    *   **Lazy Loading**: Load image only when requested.
    *   **Security**: Check permissions before calling real object.

**Example**:
```java
class ProxyImage implements Image {
    private RealImage realImage;
    private String filename;

    public void display() {
        if(realImage == null) {
            realImage = new RealImage(filename);
        }
        realImage.display();
    }
}
```

---

## 9. Prototype Pattern
**Detailed Explanation**: Creates new objects by copying an existing object (Cloning).
*   **Usage**: When object creation is expensive (DB calls), we create one, cache it, and clone it when needed.
*   **Mechanism**: Implements `Cloneable` interface.

**Example**:
```java
class Shape implements Cloneable {
    public Object clone() {
        return super.clone();
    }
}
```
