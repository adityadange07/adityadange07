
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
