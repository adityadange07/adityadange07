# Miscellaneous Interview Questions & Answers

## 1. What is a HashCode Contract?
**Detailed Explanation**: The contract between `equals()` and `hashCode()` ensures that objects stored in hash-based collections (like HashMap) can be retrieved correctly.
*   **Rule**: If `a.equals(b)` is true, then `a.hashCode()` must equal `b.hashCode()`.
*   **Violation**: If violated, you might put an object in a Map but never find it again because the Map looks in the wrong bucket.

---

## 2. Contrast between HASHCODE() and EQUALS() methods?
*   **`equals()`**: Checks if two objects are logically equivalent (e.g., same ID). Slower (compares fields).
*   **`hashCode()`**: Returns an integer to sort objects into buckets. Fast.

---

## 3. Best Approach for Creating REST API
**Detailed Explanation**:
1.  **Design**: Define Resources (Nouns) and Methods (Verbs).
2.  **Controller**: Use `@RestController`.
3.  **Service**: Business logic.
4.  **Repository**: DB interaction.
5.  **DTOs**: Use Data Transfer Objects, don't expose Entities directly.
6.  **Versioning**: `/api/v1/...`
7.  **Error Handling**: Global Exception Handler.

---

## 4. @Qualifier and @Primary
**Detailed Explanation**:
*   **`@Primary`**: The default bean to inject when multiple match.
*   **`@Qualifier`**: Specific bean selection by name. Override `@Primary`.

---

## 5. POST and PUT method diff
**Detailed Explanation**:
*   **POST**: Create new. Not idempotent (2 calls = 2 records).
*   **PUT**: Update/Replace. Idempotent (2 calls = same state).

---

## 6. save() and saveAll() diff
**Detailed Explanation**:
*   **`save(entity)`**: Saves one entity.
*   **`saveAll(list)`**: Saves a list of entities. Optimized for batching.

---

## 7. What is Method References?
**Detailed Explanation**: Shorthand for Lambdas calling a method.
*   `s -> System.out.println(s)` becomes `System.out::println`.

---

## 8. Can we make main method as private?
**Detailed Explanation**: Yes, it compiles. But code does not run. JVM throws "Main method not found" error. Main must be `public`.

---

## 9. JUnit and Mockito related
*   **JUnit**: Testing Framework (`@Test`).
*   **Mockito**: Mocking Framework (`when(repo.find()).thenReturn(data)`). Used to isolate the unit being tested.

---

## 10. How to test private method?
**Detailed Explanation**: Use Reflection (`method.setAccessible(true)`). Generally discouraged; test the public method calling it instead.

---

## 11. Try-catch-finally block
**Detailed Explanation**:
*   **Try**: Code that might throw exception.
*   **Catch**: Code to handle exception.
*   **Finally**: Code that runs *always* (cleanup).

---

## 12. Integration Testing
**Detailed Explanation**: Testing the interaction between modules (e.g., Service + Database). Uses `@SpringBootTest`. Slower than Unit tests.

---

## 13. Difference between final, finally and finalize
*   **final**: Constant/Immutable.
*   **finally**: Block for cleanup.
*   **finalize**: Method called by GC (Deprecated).

---

## 14. Diff between final variable and constant
**Detailed Explanation**:
*   **Final Variable**: Value assigned once. Can be assigned in constructor (instance specific).
*   **Constant**: `static final`. Value is same for ALL instances (Class level).

---

## 15. About Unit Testing
**Detailed Explanation**: Testing individual components (methods) in complete isolation. Dependencies are mocked. Fast execution.

---

## 16. What are the methods of REST API?
**Detailed Explanation**: GET, POST, PUT, DELETE, PATCH, HEAD, OPTIONS.

---

## 17. What is Permanent Generation and Metaspace?
**Detailed Explanation**:
*   **PermGen (Java 7)**: Fixed size memory for class metadata. Prone to `OutOfMemoryError`.
*   **Metaspace (Java 8)**: Replaces PermGen. Uses native OS memory. Auto-resizes.

---

## 18. How to achieve it (Immutability)?
**Detailed Explanation**: 1. `final` class. 2. `private final` fields. 3. No setters. 4. Deep copy mutable fields in getters.

---

## 19. Loose coupling vs Tight coupling
**Detailed Explanation**:
*   **Tight**: Classes depend on concrete implementations (`Car` uses `new Engine()`). Hard to change.
*   **Loose**: Classes depend on Interfaces (`Car` uses `Engine` interface). Easy to swap implementations (Spring DI).

---

## 20. Encryption and Decryption
**Detailed Explanation**:
*   **Encryption**: Convert Plaintext -> Ciphertext (Unreadable) using a Key.
*   **Decryption**: Convert Ciphertext -> Plaintext using Key.
*   **Types**: Symmetric (Same key), Asymmetric (Public/Private key).

---

## 21. OOPS Concepts
**Detailed Explanation**: Encapsulation, Inheritance, Polymorphism, Abstraction.

---

## 22. Hashcode Contract
*(Duplicate of Q1)*.

---

## 23. Approach for Create REST API
*(Duplicate of Q3)*.

---

## 24. Scenario Based Questions
*(Usually refers to "What if DB is slow?" or "How to handle high traffic?" -> Answer: Caching, Indexing, Load Balancing).*

---

## 25. What is the Utility Class?
**Detailed Explanation**: A helper class with only **static methods**. It is stateless.
*   **Example**: `java.lang.Math`, `Collections`, `StringUtils`.

---

## 26. Why do we use it?
**Detailed Explanation**: To avoid code duplication. Common logic (like date formatting) is placed here and reused everywhere.

---

## 27. Does the Utility class have a constructor?
**Detailed Explanation**: It SHOULD have a **private constructor** to prevent instantiation. You never say `new Math()`.

---

## 28. Example of utility class
```java
public final class StringUtils {
    private StringUtils() {} // Private

    public static boolean isEmpty(String s) {
        return s == null || s.length() == 0;
    }
}
```

---

## 29. PermGen vs Metaspace
*(Duplicate of Q17)*.

---

## 30. Method Idempotency
**Detailed Explanation**: Doing an action multiple times has the same effect as doing it once.
*   **Idempotent**: DELETE, PUT, GET.
*   **Not Idempotent**: POST.

---

## 31. Why delete is idempotent?
**Detailed Explanation**: If you delete Row ID 5. It's gone. If you call delete Row ID 5 again, it's still generic "Gone". Server state doesn't change further.

---

## 32. What does delete return when we again hit delete?
**Detailed Explanation**:
*   **First call**: 200 OK / 204 No Content.
*   **Second call**: 404 Not Found (since it's already gone). (Wait, Idempotency refers to server state, not necessarily the response code being identical, though standards vary).

---

## 33. Which is idempotent and which is not?
*   **Idempotent**: PUT, DELETE, GET.
*   **Not**: POST, PATCH (sometimes).

---

## 34. Criteria API
**Detailed Explanation**: A programmatic, type-safe way to write DB queries in Java (instead of String HQL).
*   **Example**: `cb.createQuery(Employee.class); root.select(...).where(...)`.

---

## 35. Static keyword
**Detailed Explanation**: Belongs to the **Class**, not instance. Shared by all objects. Shared memory.

---

## 36. Encryption and Decryption
*(Duplicate of Q20)*.

---

## 37. Write a code for a REST API.
```java
@RestController
@RequestMapping("/api/users")
public class UserController {
    @GetMapping("/{id}")
    public User getUser(@PathVariable int id) {
        return new User(id, "John");
    }
}
```

---

## 38. Relationship 1 Dept to Multiple Emps
**Detailed Explanation**:
*   **Department**: `@OneToMany(mappedBy="dept") List<Employee> emps;`
*   **Employee**: `@ManyToOne Department dept;`

---

## 39. What is N+1 Problem?
**Detailed Explanation**: Fetching 1 Parent + N Children results in N+1 SQL queries. Major performance killer.

---

## 40. How to resolve it?
**Detailed Explanation**: Use `JOIN FETCH` in JPQL.
`SELECT d FROM Dept d JOIN FETCH d.employees`.

---

## 41. Lazy Fetch
**Detailed Explanation**: Fetch data only when getter is called. Default for OneToMany.

---

## 42. How to mention Lazy Fetch?
**Detailed Explanation**: `fetch = FetchType.LAZY`.
`@OneToMany(fetch = FetchType.LAZY)`

---

## 43. All classes to create REST API
**Detailed Explanation**:
1.  **Entity**: `User.java` (DB Table).
2.  **Repo**: `UserRepository.java` (Interface extending JpaRepository).
3.  **Service**: `UserService.java` (Logic).
4.  **Controller**: `UserController.java` (Endpoints).

---

## 44. Packages
**Detailed Explanation**:
*   `com.app.model`
*   `com.app.repository`
*   `com.app.service`
*   `com.app.controller`
*   `com.app.config`

---

## 45. Repeated characters without changing order
**Detailed Explanation**: LinkedHashMap logic (See Coding Q1).

---

## 46. Tell me about yourself.
*(See HR Q1)*.

---

## 47. What is Inversion of Control?
**Detailed Explanation**: Spring container takes control of creating and injecting objects.

---

## 48. Migration benefits?
**Detailed Explanation**: "Moving to Microservices improved our Scalability. Individual services could be deployed daily. Fault isolation improved system uptime."

---

## 49. How Authentication and Authorization work?
*(See Spring Boot Q25)*.

---

## 50. Default keyword
**Detailed Explanation**:
1.  **Switch Case**: Default case.
2.  **Interface**: Default method implementation (Java 8).

---

## 51. REST API
*(General Topic).*

---

## 52. How to override server configuration?
**Detailed Explanation**: In `application.properties`.
`server.port=9090`
`server.servlet.context-path=/api`

---

## 53. Lazy vs Eager loading
*(Duplicate of Q41)*.

---

## 54. Save vs Persist
*(Duplicate of Spring Boot Q31)*.

---

## 55. Database knowledge & Queries
*(General Topic - See Database section).*

---

## 56. Where from?
*(HR: Where are you from?)*.

---

## 57. IAM Role Policy
**Detailed Explanation**: An AWS JSON document defining permissions.
*   **Example**: "Allow S3 Read Access".
*   Attached to Users or Roles.

---

## 58. Can we overload main method?
**Detailed Explanation**: Yes. But JVM only calls the standard `String[] args` one.

---

## 59. Can you overload 2 main methods?
**Detailed Explanation**: Yes, you can have `main(String[] args)` and `main(int x)`. JVM calls the first one.

---

## 60. Method Overriding Scenario
**Detailed Explanation**: Runtime Polymorphism. Child class provides specific implementation of Parent method.
*   Access modifier cannot be more restrictive.
*   Return type must be same or covariant.

---

## 61. Default Static Method
**Detailed Explanation**: In Interface (Java 8):
*   **Default**: Has body. Can be overridden. Instance method.
*   **Static**: Has body. Utility method. Cannot be overridden. Called via `InterfaceName.method()`.
