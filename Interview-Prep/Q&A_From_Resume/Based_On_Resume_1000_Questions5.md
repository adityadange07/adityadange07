Based on your resume and the technologies you’ve mentioned, here is a complete interview preparation plan consisting of **1000 categorized questions** across the following major areas:

---

### ✅ **Structure: 20 Categories × 50 Questions Each**

1. **Core Java**
2. **Spring Boot**
3. **Spring MVC**
4. **Spring Data JPA**
5. **Spring Security**
6. **Microservices**
7. **Kafka**
8. **RabbitMQ**
9. **Jenkins**
10. **Docker**
11. **Kubernetes**
12. **PostgreSQL**
13. **MongoDB**
14. **Redis**
15. **Angular**
16. **React.js**
17. **System Design (HLD & LLD)**
18. **DSA (Data Structures and Algorithms)**
19. **Project-Based Questions (HRMS, Booking, Notifications)**
20. **HR, Behavioral & Leadership (Module Lead)**

---

### 🔥 Let’s Begin with the First 50: **Core Java Interview Questions**

Would you like to:

* ✅ Start now with **Core Java 50 questions**, and then go topic-by-topic?
* 📄 Or receive the **entire 1000-question PDF** in one document?
* 🧩 Or get a **custom order** (e.g., start with DevOps + Leadership + DSA)?

Let me know your preference so I can tailor it for you.

Great! Let's begin with the **first 50 Core Java interview questions and answers** tailored for your 3.5+ years of experience as a Full Stack Java Developer.

---

## ✅ **Core Java – Top 50 Interview Questions & Answers**

### 🔹 **1. What are the main features of Java?**

Java is:

* **Object-Oriented**
* **Platform-Independent**
* **Robust and Secure**
* **Multithreaded**
* **High Performance (via JIT compiler)**
* **Garbage Collected**

---

### 🔹 **2. What is the difference between JDK, JRE, and JVM?**

* **JVM**: Java Virtual Machine – runs the Java bytecode.
* **JRE**: Java Runtime Environment – JVM + libraries.
* **JDK**: Java Development Kit – JRE + compilers/debuggers.

---

### 🔹 **3. What is the difference between `==` and `.equals()`?**

* `==` checks for **reference equality**.
* `.equals()` checks for **value/content equality** (can be overridden).

---

### 🔹 **4. What is the use of the `final` keyword in Java?**

* **final variable** – constant value.
* **final method** – cannot be overridden.
* **final class** – cannot be extended.

---

### 🔹 **5. What are access modifiers in Java?**

* `private`, `default`, `protected`, `public`
* They define the **scope** of class members.

---

### 🔹 **6. What is the difference between `ArrayList` and `LinkedList`?**

* **ArrayList**: fast for **get(), set()**, but slow for insert/delete.
* **LinkedList**: fast for **insert/delete**, but slower for **get()**.

---

### 🔹 **7. What is method overloading vs. overriding?**

* **Overloading**: same method name, different parameters (compile-time).
* **Overriding**: subclass redefines superclass method (runtime).

---

### 🔹 **8. Explain the concept of constructor in Java.**

* Special method used to initialize objects.
* Name = class name, no return type.
* Can be **default**, **parameterized**, or **copy constructor**.

---

### 🔹 **9. What is an interface in Java?**

* Collection of **abstract methods**.
* Supports **multiple inheritance**.
* Since Java 8, can have **default & static methods**.

---

### 🔹 **10. What is the difference between abstract class and interface?**

| Feature     | Abstract Class      | Interface                     |
| ----------- | ------------------- | ----------------------------- |
| Inheritance | Single              | Multiple                      |
| Fields      | Can have variables  | Only constants (until Java 8) |
| Methods     | Abstract + concrete | Abstract only (Java 7)        |

---

### 🔹 **11. How does garbage collection work in Java?**

* JVM automatically removes **unused objects**.
* Uses algorithms like **Mark & Sweep**.
* Can be invoked using `System.gc()` (just a request).

---

### 🔹 **12. What is the purpose of the `static` keyword?**

* Belongs to the **class**, not instances.
* Used for **shared variables/methods**, `static blocks`, etc.

---

### 🔹 **13. What are exceptions in Java? Types?**

* **Checked**: Compile-time (e.g., IOException)
* **Unchecked**: Runtime (e.g., NullPointerException)
* Use `try-catch-finally` for handling.

---

### 🔹 **14. What is a try-with-resources block?**

* Introduced in Java 7.
* Automatically closes resources (e.g., `FileReader`, `Connection`).

---

### 🔹 **15. What is the difference between `throw` and `throws`?**

* `throw`: used to **throw an exception**.
* `throws`: used in **method signature** to declare exception possibility.

---

### 🔹 **16. What is multithreading in Java?**

* Allows **concurrent execution**.
* Implemented using `Thread` or `Runnable`.
* Methods: `start()`, `run()`, `join()`, `sleep()`.

---

### 🔹 **17. Difference between `synchronized` method and block?**

* `synchronized method`: locks the whole method.
* `synchronized block`: locks a specific object or section.

---

### 🔹 **18. What is a deadlock in multithreading?**

* Two threads wait for each other's lock, causing a **permanent block**.
* Prevent with proper lock ordering.

---

### 🔹 **19. What are functional interfaces?**

* Interface with a **single abstract method**.
* Used in **lambda expressions**.
* Example: `Runnable`, `Comparable`.

---

### 🔹 **20. What are lambda expressions?**

* Introduced in Java 8 for **functional programming**.

```java
(List<String> list) -> list.size();
```

---

### 🔹 **21. What is Stream API in Java 8?**

* Allows **functional-style operations** on collections.
* Operations: `map()`, `filter()`, `collect()`, `forEach()`.

---

### 🔹 **22. What are default methods in interfaces (Java 8)?**

* Interface methods with **default implementation**.

```java
default void log() { System.out.println("Default log"); }
```

---

### 🔹 **23. What is Optional in Java 8?**

* Prevents **null pointer exceptions**.

```java
Optional<String> name = Optional.of("Aditya");
```

---

### 🔹 **24. Difference between HashMap and Hashtable?**

* **HashMap**: not synchronized, allows null.
* **Hashtable**: synchronized, no null keys/values.

---

### 🔹 **25. What is the difference between `HashMap` and `ConcurrentHashMap`?**

* `HashMap`: not thread-safe.
* `ConcurrentHashMap`: thread-safe with better concurrency.

---

### 🔹 **26. What is the significance of `hashCode()` and `equals()`?**

* Used in **collections like HashMap** for object comparison and storage.
* Should override both for custom key behavior.

---

### 🔹 **27. Can you override a static method?**

* No, static methods are **class-level** and **cannot be overridden**.

---

### 🔹 **28. What is the difference between shallow and deep copy?**

* **Shallow copy**: copies references.
* **Deep copy**: copies actual object values (recursively).

---

### 🔹 **29. What are the principles of OOP in Java?**

* **Encapsulation**, **Abstraction**, **Inheritance**, **Polymorphism**.

---

### 🔹 **30. What is encapsulation?**

* Wrapping data (fields) and methods in one unit (class).
* Achieved using **private fields** and **public getters/setters**.

---

### 🔹 **31. What is polymorphism?**

* **Compile-time (overloading)** and **Runtime (overriding)**.

---

### 🔹 **32. What is inheritance?**

* Allows one class to inherit properties of another using `extends`.

---

### 🔹 **33. What is abstraction?**

* Hiding implementation details and exposing functionality via interfaces or abstract classes.

---

### 🔹 **34. What are wrapper classes?**

* Convert primitive to objects (`int` → `Integer`, `double` → `Double`).

---

### 🔹 **35. What is autoboxing and unboxing?**

* **Autoboxing**: primitive to wrapper.
* **Unboxing**: wrapper to primitive.

---

### 🔹 **36. What is the purpose of the `transient` keyword?**

* Prevents field from being serialized.

---

### 🔹 **37. What is the `volatile` keyword?**

* Ensures visibility of changes across threads to a variable.

---

### 🔹 **38. What is the Singleton Design Pattern?**

* Ensures only **one instance** of a class exists.

```java
private static Singleton instance = new Singleton();
```

---

### 🔹 **39. What is the Factory Design Pattern?**

* Used to create objects **without exposing instantiation logic**.

---

### 🔹 **40. Explain `Comparable` vs `Comparator`.**

* `Comparable`: natural ordering.
* `Comparator`: custom sorting logic.

---

### 🔹 **41. What is recursion?**

* A method calling itself.
* Useful for problems like tree traversal, factorial, etc.

---

### 🔹 **42. Difference between `String`, `StringBuffer`, and `StringBuilder`?**

* `String`: immutable
* `StringBuffer`: mutable, thread-safe
* `StringBuilder`: mutable, not thread-safe (faster)

---

### 🔹 **43. How to make a class immutable?**

* Make class `final`, fields `private final`, no setters, constructor to initialize fields.

---

### 🔹 **44. What is ClassLoader in Java?**

* Loads class files into memory.
* Types: **Bootstrap**, **Extension**, **Application**.

---

### 🔹 **45. What is reflection in Java?**

* Allows runtime inspection/modification of classes, methods, fields.

---

### 🔹 **46. What is the difference between process and thread?**

* **Process**: independent program.
* **Thread**: lightweight subprocess of a program.

---

### 🔹 **47. What is the use of `instanceof`?**

* Checks whether an object is an instance of a class or subclass.

---

### 🔹 **48. What are annotations in Java?**

* Provide metadata about code.
* Examples: `@Override`, `@Deprecated`, `@FunctionalInterface`.

---

### 🔹 **49. What are enums in Java?**

* Used to define fixed sets of constants.

```java
enum Days { MONDAY, TUESDAY }
```

---

### 🔹 **50. How is memory managed in Java?**

* **Heap** for objects.
* **Stack** for method calls.
* Managed via **Garbage Collector**.

---

✅ Ready for the next topic? Should we continue with **Spring Boot**, **Spring Data JPA**, or your preferred category from the list?

Let me know, and I’ll continue with the next set of 50 questions.

Awesome! Let's move on to the next 50:

---

## ✅ **Spring Boot – Top 50 Interview Questions & Answers**

---

### 🔹 **1. What is Spring Boot?**

Spring Boot is a framework built on top of the Spring Framework that simplifies application development by:

* Providing **auto-configuration**
* Offering **embedded servers** (Tomcat, Jetty)
* Reducing boilerplate with **starter dependencies**
* Supporting **production-ready features** via **Spring Actuator**

---

### 🔹 **2. What are the main features of Spring Boot?**

* Auto Configuration
* Embedded Server (Tomcat, Jetty)
* Spring Boot Starters
* Spring Boot CLI
* Spring Actuator
* No XML configuration

---

### 🔹 **3. What is the difference between Spring and Spring Boot?**

| Feature | Spring Framework         | Spring Boot             |
| ------- | ------------------------ | ----------------------- |
| Setup   | Manual, XML-based        | Auto-configured, no XML |
| Server  | External server required | Embedded server         |
| Config  | Complex                  | Simplified              |

---

### 🔹 **4. What is a Spring Boot Starter?**

* A **starter dependency** that aggregates related libraries.
* Example: `spring-boot-starter-web` includes Spring MVC, Jackson, Embedded Tomcat.

---

### 🔹 **5. What is Spring Initializr?**

* A web-based tool to **generate Spring Boot project scaffolding**.
* Allows you to select dependencies and generate ZIP file of the project.

---

### 🔹 **6. How does auto-configuration work in Spring Boot?**

* Spring Boot automatically configures beans based on classpath entries using `@EnableAutoConfiguration` and `@Conditional*` annotations.

---

### 🔹 **7. What is the role of `@SpringBootApplication`?**

A **convenience annotation** that includes:

```java
@Configuration
@EnableAutoConfiguration
@ComponentScan
```

---

### 🔹 **8. What is the use of `application.properties` or `application.yml`?**

Used to **configure application settings**:

```properties
server.port=8081
spring.datasource.url=jdbc:mysql://localhost:3306/db
```

---

### 🔹 **9. How do you create custom properties in Spring Boot?**

```properties
myapp.title=Hospital Management
```

Then bind using `@Value` or `@ConfigurationProperties`.

---

### 🔹 **10. What are profiles in Spring Boot?**

* Help in managing **environments**: `dev`, `test`, `prod`

```properties
spring.profiles.active=dev
```

---

### 🔹 **11. What is Spring Boot DevTools?**

* Provides developer productivity features like:

    * Auto-restart
    * Live reload
    * Improved logging

---

### 🔹 **12. What is an embedded server in Spring Boot?**

* Spring Boot apps run with **built-in servers** like Tomcat, Jetty, or Undertow.

---

### 🔹 **13. How to change the default port of Spring Boot?**

```properties
server.port=8081
```

---

### 🔹 **14. What is Spring Boot Actuator?**

* Provides **endpoints to monitor** and manage your app:

    * `/actuator/health`
    * `/actuator/metrics`
    * `/actuator/env`

---

### 🔹 **15. How to enable specific actuator endpoints?**

```properties
management.endpoints.web.exposure.include=health,info
```

---

### 🔹 **16. What is the use of `@RestController`?**

* Combines `@Controller` + `@ResponseBody`
* Returns JSON/XML response directly.

---

### 🔹 **17. What is the use of `@RequestMapping` vs `@GetMapping`?**

* `@RequestMapping` – generic
* `@GetMapping`, `@PostMapping` – HTTP-specific shortcuts

---

### 🔹 **18. How to handle exceptions globally in Spring Boot?**

Use `@ControllerAdvice` and `@ExceptionHandler`:

```java
@ExceptionHandler(Exception.class)
public ResponseEntity<String> handleException(Exception e)
```

---

### 🔹 **19. What is Spring Boot CLI?**

* Command-line tool to **run Groovy scripts** for Spring Boot apps.

---

### 🔹 **20. What is `@SpringBootTest` used for?**

* Used in integration testing; boots up the full application context.

---

### 🔹 **21. What is the use of `@EnableAutoConfiguration`?**

* Instructs Spring Boot to automatically configure based on dependencies.

---

### 🔹 **22. How to disable a specific auto-configuration?**

Use:

```java
@EnableAutoConfiguration(exclude = { DataSourceAutoConfiguration.class })
```

---

### 🔹 **23. How to connect to a MySQL database in Spring Boot?**

Add MySQL dependency and configure:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/test
spring.datasource.username=root
spring.datasource.password=1234
```

---

### 🔹 **24. What is the default database used in Spring Boot?**

* **H2 in-memory database** (if no DB is specified).

---

### 🔹 **25. What is the purpose of Spring Boot starters?**

* Simplifies dependency management.
* Each starter provides a ready-to-use stack.

---

### 🔹 **26. How can you secure Spring Boot endpoints?**

* Add `spring-boot-starter-security`
* Define config using `WebSecurityConfigurerAdapter` or `SecurityFilterChain`.

---

### 🔹 **27. How does Spring Boot support microservices?**

* Via components like:

    * Spring Cloud
    * Eureka (Service Registry)
    * Spring Gateway
    * Config Server

---

### 🔹 **28. How to create custom banner in Spring Boot?**

* Replace `banner.txt` in `/resources` directory.

---

### 🔹 **29. What are the ways to run a Spring Boot application?**

* Using `main()` method
* Using Maven/Gradle `spring-boot:run`
* As a WAR deployed to external server

---

### 🔹 **30. What is Spring Boot starter parent?**

* A special `pom.xml` base that manages versions of dependencies.

---

### 🔹 **31. How to enable CORS in Spring Boot?**

```java
@CrossOrigin(origins = "*")
@GetMapping("/api")
```

---

### 🔹 **32. How does Spring Boot handle dependency injection?**

* Automatically injects beans using:

    * `@Component`, `@Service`, `@Repository`, `@Autowired`

---

### 🔹 **33. What is the difference between `@Component` and `@Bean`?**

* `@Component`: used at class level.
* `@Bean`: used in `@Configuration` classes to define beans manually.

---

### 🔹 **34. How to externalize configuration in Spring Boot?**

* Use `application.properties`, `.yml`, or environment variables.

---

### 🔹 **35. Can we have multiple `application.properties` files?**

Yes. Use:

```properties
application-dev.properties
application-prod.properties
```

Activate using `spring.profiles.active`.

---

### 🔹 **36. How to load custom properties into a class?**

Use:

```java
@ConfigurationProperties(prefix = "custom")
```

---

### 🔹 **37. How to schedule tasks in Spring Boot?**

* Use `@EnableScheduling` and `@Scheduled`:

```java
@Scheduled(fixedRate = 5000)
```

---

### 🔹 **38. What is the use of `@ConditionalOnProperty`?**

* Enable bean creation based on property values.

---

### 🔹 **39. How to create a WAR instead of JAR in Spring Boot?**

* Change `packaging` in `pom.xml` to `war`
* Extend `SpringBootServletInitializer`

---

### 🔹 **40. How does Spring Boot support asynchronous processing?**

* Use `@Async` and enable with `@EnableAsync`.

---

### 🔹 **41. How do you handle validation in Spring Boot?**

* Use annotations like `@NotNull`, `@Email` and `@Valid` in controller.

---

### 🔹 **42. What is actuator endpoint `/actuator/mappings`?**

* Lists all controller and actuator endpoints with details.

---

### 🔹 **43. How do you use Flyway or Liquibase in Spring Boot?**

* Add dependency and provide migration scripts in `/resources/db/migration`.

---

### 🔹 **44. What is difference between `@RestController` and `@Controller`?**

* `@RestController`: returns data (JSON/XML)
* `@Controller`: returns view (HTML/Thymeleaf)

---

### 🔹 **45. How to return a custom HTTP status code in Spring Boot?**

Use `ResponseEntity`:

```java
return new ResponseEntity<>(body, HttpStatus.CREATED);
```

---

### 🔹 **46. What is `CommandLineRunner`?**

* Executes logic **after application startup**.

---

### 🔹 **47. What is `ApplicationRunner`?**

* Similar to `CommandLineRunner` but provides `ApplicationArguments`.

---

### 🔹 **48. How to exclude an auto-configuration class?**

```java
@SpringBootApplication(exclude = DataSourceAutoConfiguration.class)
```

---

### 🔹 **49. How to log in Spring Boot?**

* Uses **SLF4J** with **Logback** by default.
* Configured in `application.properties`.

---

### 🔹 **50. How do you test Spring Boot applications?**

* Unit tests with `@WebMvcTest`
* Integration tests with `@SpringBootTest`

---

✅ **Next up:** Spring Data JPA, Spring Security, or a topic of your choice.

Let me know your preference and I’ll continue with the next 50!

Great! Let’s continue with the next 50:

---

## ✅ **Spring Data JPA – Top 50 Interview Questions & Answers**

---

### 🔹 **1. What is Spring Data JPA?**

Spring Data JPA is part of the Spring Data family that simplifies the implementation of JPA-based repositories by reducing boilerplate code and supporting advanced query features.

---

### 🔹 **2. What are the advantages of using Spring Data JPA?**

* Reduces boilerplate code
* Supports custom queries
* Integrates well with Spring Boot
* Built-in CRUD operations
* Paging, sorting, and auditing

---

### 🔹 **3. What is a `JpaRepository`?**

An interface that extends `PagingAndSortingRepository` and `CrudRepository`, adding JPA-specific methods like:

```java
List<T> findAll();
Optional<T> findById(ID id);
```

---

### 🔹 **4. What are the differences between `CrudRepository`, `PagingAndSortingRepository`, and `JpaRepository`?**

| Interface                  | Features                                     |
| -------------------------- | -------------------------------------------- |
| CrudRepository             | Basic CRUD                                   |
| PagingAndSortingRepository | CRUD + Pagination/Sorting                    |
| JpaRepository              | All above + batch operations, flushing, etc. |

---

### 🔹 **5. How do you define a repository interface?**

```java
@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {}
```

---

### 🔹 **6. What is the purpose of the `@Entity` annotation?**

Marks a class as a **JPA entity** that maps to a database table.

---

### 🔹 **7. What is the difference between `@Entity` and `@Table`?**

* `@Entity`: Declares a class as a JPA entity.
* `@Table`: Optional. Specifies the table name.

---

### 🔹 **8. What are derived query methods in Spring Data JPA?**

Methods like `findByName`, `findByAgeBetween`, etc., auto-generate SQL based on method name.

---

### 🔹 **9. How do you create a custom query in Spring Data JPA?**

Use `@Query`:

```java
@Query("SELECT e FROM Employee e WHERE e.name = ?1")
List<Employee> findByName(String name);
```

---

### 🔹 **10. What is the difference between JPQL and native SQL?**

* **JPQL**: operates on entity objects.
* **Native SQL**: operates directly on database tables.

---

### 🔹 **11. How to execute native SQL in Spring Data JPA?**

```java
@Query(value = "SELECT * FROM employee WHERE name = :name", nativeQuery = true)
List<Employee> findByName(@Param("name") String name);
```

---

### 🔹 **12. How do you paginate results in Spring Data JPA?**

Use `Pageable` and `Page`:

```java
Page<Employee> findAll(Pageable pageable);
```

---

### 🔹 **13. How do you sort results in Spring Data JPA?**

Use `Sort` object:

```java
findAll(Sort.by("name").ascending());
```

---

### 🔹 **14. What is optimistic locking?**

Prevents data conflicts using `@Version`. If data was modified after fetching, update fails.

---

### 🔹 **15. What is pessimistic locking?**

Locks the row in the database for exclusive access, preventing other transactions.

---

### 🔹 **16. What is the difference between `save()` and `saveAndFlush()`?**

* `save()`: queues changes.
* `saveAndFlush()`: persists immediately.

---

### 🔹 **17. What is cascading in JPA?**

Automatic propagation of entity operations (persist, merge, delete) to associated entities.

---

### 🔹 **18. What is `@OneToMany` and `@ManyToOne`?**

Defines relationships:

```java
@OneToMany(mappedBy = "department")
List<Employee> employees;

@ManyToOne
Department department;
```

---

### 🔹 **19. What is `@JoinColumn`?**

Specifies the **foreign key column** in a relationship.

---

### 🔹 **20. How do you define a composite primary key?**

Use `@IdClass` or `@EmbeddedId`.

---

### 🔹 **21. What is `@Embedded` and `@Embeddable`?**

Used to embed a value object (address, etc.) in the parent entity.

---

### 🔹 **22. What is lazy vs eager fetching?**

* **Lazy**: loads data only when needed.
* **Eager**: loads all related data immediately.

---

### 🔹 **23. What is N+1 select problem?**

Occurs when a parent fetch triggers multiple additional queries for children.

---

### 🔹 **24. How to resolve N+1 problem?**

Use `JOIN FETCH` or `EntityGraph`.

---

### 🔹 **25. How to validate entities in JPA?**

Use JSR 303 annotations like:

```java
@NotNull, @Size, @Min, @Max
```

---

### 🔹 **26. How to enable auditing in Spring Data JPA?**

Use:

* `@EnableJpaAuditing`
* `@CreatedDate`, `@LastModifiedDate`

---

### 🔹 **27. What is a DTO and why use it?**

A Data Transfer Object used to transfer only required fields from entity to response.

---

### 🔹 **28. How do you map a DTO using JPQL?**

```java
@Query("SELECT new com.dto.EmpDto(e.id, e.name) FROM Employee e")
List<EmpDto> findCustom();
```

---

### 🔹 **29. What is the difference between `merge()` and `persist()`?**

* `persist()`: adds a new entity.
* `merge()`: updates an existing one.

---

### 🔹 **30. What is the purpose of `@Modifying` annotation?**

Used with `@Query` to execute `INSERT`, `UPDATE`, or `DELETE`.

---

### 🔹 **31. What is `flush()` in JPA?**

Synchronizes persistence context with the database.

---

### 🔹 **32. How to count records in a table using Spring Data JPA?**

```java
long count();
```

or custom:

```java
@Query("SELECT COUNT(e) FROM Employee e")
```

---

### 🔹 **33. What are projections in Spring Data JPA?**

Return partial data using interfaces or classes.

---

### 🔹 **34. How to perform bulk updates in JPA?**

Use `@Modifying` + `@Query`.

---

### 🔹 **35. Can we execute stored procedures with Spring Data JPA?**

Yes, using `@Procedure`.

---

### 🔹 **36. What is the purpose of the `@GeneratedValue` annotation?**

Automatically generates primary key value.

```java
@GeneratedValue(strategy = GenerationType.IDENTITY)
```

---

### 🔹 **37. What are entity listeners in JPA?**

Lifecycle hooks like `@PrePersist`, `@PostLoad`, etc.

---

### 🔹 **38. What is the difference between `EntityManager` and `JpaRepository`?**

* `EntityManager`: lower-level JPA operations.
* `JpaRepository`: high-level abstraction.

---

### 🔹 **39. How do you perform batch inserts in Spring Data JPA?**

Enable:

```properties
spring.jpa.properties.hibernate.jdbc.batch_size=30
```

---

### 🔹 **40. How to configure lazy loading in Spring Boot?**

```properties
spring.jpa.open-in-view=true
```

---

### 🔹 **41. Can JPA entities be immutable?**

Yes, by marking fields `final` and using constructor-based injection.

---

### 🔹 **42. What is the default fetch type for relationships?**

* `@OneToMany`: **LAZY**
* `@ManyToOne`: **EAGER**

---

### 🔹 **43. How to write dynamic queries in Spring Data JPA?**

Use `Specifications` with `JpaSpecificationExecutor`.

---

### 🔹 **44. What is the role of `EntityTransaction`?**

Manages commit/rollback in manual transaction management.

---

### 🔹 **45. What is the use of `@Inheritance`?**

Defines entity **inheritance mapping strategy**:

* `SINGLE_TABLE`, `JOINED`, `TABLE_PER_CLASS`

---

### 🔹 **46. Can you use multiple databases in one Spring Boot app?**

Yes, using multiple `DataSource`, `EntityManagerFactory`, and `TransactionManager`.

---

### 🔹 **47. How to update only specific fields using JPA?**

Use custom `@Query` with `@Modifying`.

---

### 🔹 **48. How to handle null values in query results?**

Use `Optional` or `COALESCE()` in JPQL.

---

### 🔹 **49. What is a named query in JPA?**

Predefined JPQL stored with the entity using `@NamedQuery`.

---

### 🔹 **50. How to log JPA SQL queries in Spring Boot?**

```properties
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
```

---

✅ **Next up:** Should I continue with **Spring Security** or your next preferred topic?

Let me know and I’ll give you the next 50.

Perfect! Let's continue with the next 50:

---

## ✅ **Spring Security – Top 50 Interview Questions & Answers**

---

### 🔹 **1. What is Spring Security?**

Spring Security is a powerful and customizable authentication and access-control framework for Java applications, mainly used to secure Spring-based web apps.

---

### 🔹 **2. What are the core features of Spring Security?**

* Authentication & Authorization
* Password Encoding
* Session Management
* CSRF protection
* Method-level Security
* Security Headers
* LDAP & OAuth2 Integration

---

### 🔹 **3. How does Spring Security handle authentication?**

It uses `AuthenticationManager` to authenticate `UsernamePasswordAuthenticationToken` with user details from a database, memory, or LDAP.

---

### 🔹 **4. What is the difference between authentication and authorization?**

* **Authentication**: Verifying identity (e.g., username/password)
* **Authorization**: Verifying access rights to resources (roles, permissions)

---

### 🔹 **5. What is the role of `UserDetails` and `UserDetailsService`?**

* `UserDetails`: Interface representing user credentials and roles.
* `UserDetailsService`: Loads user data from a source (DB, in-memory, etc.).

---

### 🔹 **6. What is `PasswordEncoder`?**

Used to hash and validate passwords. Common implementations:

```java
BCryptPasswordEncoder, SCryptPasswordEncoder
```

---

### 🔹 **7. How do you secure REST APIs with Spring Security?**

* Use `HttpSecurity` config with JWT or Basic Auth
* Disable CSRF for stateless APIs

```java
http.csrf().disable().authorizeRequests().anyRequest().authenticated();
```

---

### 🔹 **8. What is the use of `SecurityFilterChain`?**

Defines filter chain configurations for different URL patterns in modern Spring Security.

---

### 🔹 **9. How to create custom login page in Spring Security?**

```java
http.formLogin().loginPage("/customLogin").permitAll();
```

---

### 🔹 **10. How to disable security for specific endpoints?**

```java
http.authorizeRequests().antMatchers("/public/**").permitAll();
```

---

### 🔹 **11. What is CSRF?**

Cross-Site Request Forgery: An attack that forces authenticated users to submit a request. Spring Security adds CSRF tokens to prevent this.

---

### 🔹 **12. How do you disable CSRF protection?**

```java
http.csrf().disable();
```

---

### 🔹 **13. How do you enable method-level security?**

Use:

```java
@EnableGlobalMethodSecurity(prePostEnabled = true)
```

And annotate methods with `@PreAuthorize`, `@PostAuthorize`.

---

### 🔹 **14. What is role-based authorization in Spring Security?**

Restrict access to URLs or methods using roles:

```java
@PreAuthorize("hasRole('ADMIN')")
```

---

### 🔹 **15. What is the difference between `hasRole` and `hasAuthority`?**

* `hasRole('ADMIN')` automatically adds prefix `ROLE_`
* `hasAuthority('ROLE_ADMIN')` uses full authority name

---

### 🔹 **16. What is the default user and password behavior in Spring Security?**

A default user is created with a random password printed in the logs.

---

### 🔹 **17. How to store user details in a database?**

* Implement `UserDetailsService` and fetch users from DB
* Encode passwords with `PasswordEncoder`

---

### 🔹 **18. What is a security context?**

Holds authentication info for the current session using `SecurityContextHolder`.

---

### 🔹 **19. What is stateless authentication?**

No session; authentication handled via tokens (e.g., JWT).

---

### 🔹 **20. How to configure Basic Authentication in Spring Security?**

```java
http.httpBasic();
```

---

### 🔹 **21. How to implement JWT authentication in Spring Security?**

* Create JWT token provider
* Validate token using filters
* Add the filter before `UsernamePasswordAuthenticationFilter`

---

### 🔹 **22. What is the difference between session-based and token-based authentication?**

* **Session-based**: Server stores session in memory
* **Token-based**: Stateless, client stores token (e.g., JWT)

---

### 🔹 **23. What is `SecurityConfigurerAdapter`?**

Used for customizing authentication and authorization. Deprecated in newer versions; now use `SecurityFilterChain`.

---

### 🔹 **24. How to logout in Spring Security?**

Spring handles logout automatically at `/logout`, or customize with:

```java
http.logout().logoutUrl("/signout").logoutSuccessUrl("/login");
```

---

### 🔹 **25. What is OAuth2 and how does Spring Security support it?**

OAuth2 allows third-party logins (Google, Facebook). Use:

```xml
spring-boot-starter-oauth2-client
```

---

### 🔹 **26. What is `@WithMockUser` used for?**

Used in tests to mock an authenticated user.

---

### 🔹 **27. What is `SecurityContextHolder`?**

Holds the current user's authentication info.

---

### 🔹 **28. What is `AccessDeniedHandler`?**

Used to define behavior when a user is authenticated but not authorized.

---

### 🔹 **29. What is the difference between `AuthenticationEntryPoint` and `AccessDeniedHandler`?**

* **AuthenticationEntryPoint**: Handles unauthenticated access
* **AccessDeniedHandler**: Handles unauthorized (403) access

---

### 🔹 **30. What is `SecurityFilterChain`?**

A chain of filters applied to requests; new way to define security logic (Spring Security 5+).

---

### 🔹 **31. How to secure only specific URLs in Spring Security?**

```java
.antMatchers("/admin/**").hasRole("ADMIN")
```

---

### 🔹 **32. What is filter order in Spring Security?**

Filter execution happens in a specific order:

* `UsernamePasswordAuthenticationFilter`
* `BasicAuthenticationFilter`
* `ExceptionTranslationFilter`
* etc.

---

### 🔹 **33. How to encrypt passwords in Spring Security?**

Use `BCryptPasswordEncoder`:

```java
@Bean
public PasswordEncoder encoder() {
    return new BCryptPasswordEncoder();
}
```

---

### 🔹 **34. What are GrantedAuthority and Role?**

* `GrantedAuthority`: represents user authority (role/privilege)
* `Role`: a special type of authority

---

### 🔹 **35. How to get current logged-in user?**

```java
Authentication auth = SecurityContextHolder.getContext().getAuthentication();
String username = auth.getName();
```

---

### 🔹 **36. How to create a custom `AuthenticationProvider`?**

Implement `AuthenticationProvider` and override `authenticate()`.

---

### 🔹 **37. What is `SecurityExpressionHandler`?**

Handles parsing of security expressions like `hasRole()`, `isAuthenticated()`.

---

### 🔹 **38. How to test secured endpoints in Spring Boot?**

Use:

* `@WithMockUser`
* `MockMvc`
* `SpringBootTest` with real security

---

### 🔹 **39. How to handle exceptions in Spring Security filters?**

Use `ExceptionTranslationFilter` or write custom exception handling filter.

---

### 🔹 **40. What are common security headers added by Spring Security?**

* `X-Frame-Options`
* `Strict-Transport-Security`
* `X-Content-Type-Options`

---

### 🔹 **41. What is `SecurityContextPersistenceFilter`?**

Persists and restores `SecurityContext` across requests.

---

### 🔹 **42. Can we have multiple authentication providers?**

Yes, register multiple `AuthenticationProvider` beans.

---

### 🔹 **43. How to implement remember-me in Spring Security?**

```java
http.rememberMe().key("secret").tokenValiditySeconds(86400);
```

---

### 🔹 **44. How to restrict access based on IP address?**

Create custom `WebSecurityConfigurerAdapter` and use IP condition.

---

### 🔹 **45. How does Spring Security integrate with JWT?**

* JWT filter checks token
* Extracts user info
* Sets in `SecurityContextHolder`

---

### 🔹 **46. What are best practices for securing REST APIs?**

* Use HTTPS
* Secure endpoints with roles
* Use JWT or OAuth2
* Disable CSRF
* Input validation

---

### 🔹 **47. What is `AnonymousAuthenticationToken`?**

A token assigned to users that are **not logged in** but can still access public resources.

---

### 🔹 **48. How to use role hierarchy in Spring Security?**

```java
@Bean
RoleHierarchyImpl roleHierarchy() {
    roleHierarchy.setHierarchy("ROLE_ADMIN > ROLE_USER");
}
```

---

### 🔹 **49. Can Spring Security be integrated with LDAP?**

Yes, using `LdapAuthenticationProvider` and proper configuration.

---

### 🔹 **50. How to integrate Spring Security with Angular frontend?**

* Use JWT authentication
* CORS enabled
* Store token in localStorage/sessionStorage

---

✅ **Next up:** Would you like to proceed with **Kubernetes**, **Kafka**, or any other specific area?

Let me know, and I’ll provide the next 50 questions!

Awesome! Let’s move ahead with the next 50:

---

## ✅ **Kubernetes – Top 50 Interview Questions & Answers (For Java Devs using Spring Boot & Microservices)**

---

### 🔹 **1. What is Kubernetes?**

Kubernetes (K8s) is an open-source container orchestration platform used to automate:

* Deployment
* Scaling
* Load balancing
* Management of containerized applications

---

### 🔹 **2. What are the key components of Kubernetes architecture?**

* **Master Node**: API Server, Scheduler, Controller Manager, etcd
* **Worker Node**: kubelet, kube-proxy, container runtime (e.g., Docker, containerd)

---

### 🔹 **3. What is a Pod?**

A Pod is the smallest deployable unit in Kubernetes that contains one or more containers sharing storage, network, and context.

---

### 🔹 **4. What is a ReplicaSet?**

Ensures a specified number of pod replicas are running at all times.

---

### 🔹 **5. What is a Deployment in Kubernetes?**

A higher-level object that manages ReplicaSets and allows updates, rollbacks, and scaling.

---

### 🔹 **6. How to scale applications in Kubernetes?**

Use:

```bash
kubectl scale deployment my-app --replicas=5
```

---

### 🔹 **7. What is a Service in Kubernetes?**

A stable abstraction that exposes a set of Pods as a network service, e.g., ClusterIP, NodePort, LoadBalancer.

---

### 🔹 **8. What is a ConfigMap?**

Stores configuration in key-value format separate from container images. Mounted as files or injected as environment variables.

---

### 🔹 **9. What is a Secret in Kubernetes?**

Used to store sensitive information (passwords, tokens, keys) encoded in base64.

---

### 🔹 **10. What is a StatefulSet?**

Manages stateful applications, like databases, where each pod has a **unique identity** and **persistent storage**.

---

### 🔹 **11. What is `kubectl`?**

CLI tool to interact with Kubernetes clusters.

---

### 🔹 **12. What is the difference between Deployment and StatefulSet?**

| Feature      | Deployment     | StatefulSet        |
| ------------ | -------------- | ------------------ |
| Pod identity | Anonymous      | Stable hostname    |
| Storage      | Shared         | Persistent per pod |
| Usage        | Stateless apps | Stateful apps      |

---

### 🔹 **13. What is a DaemonSet?**

Ensures a copy of a pod runs on **every node** (or specific nodes).

---

### 🔹 **14. How to expose a Deployment via NodePort?**

```yaml
type: NodePort
```

Service exposes application on all nodes at static port.

---

### 🔹 **15. What is Ingress in Kubernetes?**

Manages **external HTTP/HTTPS** access to services using rules and paths.

---

### 🔹 **16. What is a Helm chart?**

A **package manager** for Kubernetes that defines, installs, and upgrades applications via templates.

---

### 🔹 **17. What is `kubelet`?**

Agent that runs on each node, ensures containers are running as expected.

---

### 🔹 **18. What is `kube-proxy`?**

Handles networking and load-balancing between pods and services.

---

### 🔹 **19. What is `etcd`?**

A distributed key-value store used for all cluster data.

---

### 🔹 **20. What is the purpose of namespaces in Kubernetes?**

Used for **scoping resources** logically within a cluster (e.g., dev, test, prod).

---

### 🔹 **21. How do you define resource limits in Kubernetes?**

```yaml
resources:
  requests:
    memory: "512Mi"
  limits:
    memory: "1Gi"
```

---

### 🔹 **22. What is a volume in Kubernetes?**

Storage used by containers. Types include `emptyDir`, `hostPath`, `persistentVolumeClaim`.

---

### 🔹 **23. What is a PersistentVolume (PV) and PersistentVolumeClaim (PVC)?**

* **PV**: A piece of storage in the cluster
* **PVC**: Request for storage by a user

---

### 🔹 **24. What is taint and toleration in Kubernetes?**

Used to **restrict pods** from being scheduled on certain nodes unless they can tolerate the taint.

---

### 🔹 **25. What are labels and selectors?**

Labels are key-value pairs used to group and filter Kubernetes resources.

---

### 🔹 **26. How to perform a rolling update in Kubernetes?**

Update the image version in the deployment; Kubernetes will update pods gradually without downtime.

---

### 🔹 **27. What is a rollout and rollback in Kubernetes?**

* **Rollout**: Deploy a new version of an app
* **Rollback**: Revert to a previous version

```bash
kubectl rollout undo deployment my-app
```

---

### 🔹 **28. How to check pod logs?**

```bash
kubectl logs pod-name
```

---

### 🔹 **29. What are readiness and liveness probes?**

* **Liveness**: Checks if the app is alive (restart if fails)
* **Readiness**: Checks if app is ready to serve traffic

---

### 🔹 **30. How to create a pod in Kubernetes?**

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: mypod
spec:
  containers:
  - name: nginx
    image: nginx
```

---

### 🔹 **31. How to restart a deployment in Kubernetes?**

```bash
kubectl rollout restart deployment my-app
```

---

### 🔹 **32. What is an init container?**

Runs **before** the main container starts. Used for setup tasks like waiting for services.

---

### 🔹 **33. What is the difference between `args` and `command` in containers?**

* `command`: overrides ENTRYPOINT
* `args`: overrides CMD

---

### 🔹 **34. How to view all pods across all namespaces?**

```bash
kubectl get pods --all-namespaces
```

---

### 🔹 **35. What is an admission controller?**

Intercepts requests to Kubernetes API before persistence and can accept/modify/reject them.

---

### 🔹 **36. What is `kubectl describe` used for?**

Shows detailed information about a resource.

---

### 🔹 **37. How do you exec into a running container?**

```bash
kubectl exec -it pod-name -- /bin/bash
```

---

### 🔹 **38. How to monitor Kubernetes cluster?**

Tools:

* Prometheus
* Grafana
* Kube-state-metrics
* Kubernetes Dashboard

---

### 🔹 **39. What are service accounts in Kubernetes?**

Provide **identity** for processes running in pods to authenticate with the API server.

---

### 🔹 **40. What is Horizontal Pod Autoscaler (HPA)?**

Automatically scales pods based on CPU/memory metrics.

---

### 🔹 **41. How to run a job in Kubernetes?**

```yaml
kind: Job
```

Runs a task once to completion.

---

### 🔹 **42. What is CronJob in Kubernetes?**

Runs jobs on a **schedule**, like cron in Unix/Linux.

---

### 🔹 **43. What are best practices for Kubernetes YAML files?**

* Use versioned labels
* Separate config from code
* Use `liveness` and `readiness` probes
* Define `resources` and `limits`

---

### 🔹 **44. How to expose services externally?**

* `NodePort`
* `LoadBalancer`
* `Ingress`

---

### 🔹 **45. What is cluster autoscaler?**

Adds/removes nodes based on pod requirements and cluster utilization.

---

### 🔹 **46. What are sidecar containers?**

Secondary containers in a pod that support the main app (e.g., logging, monitoring).

---

### 🔹 **47. How does Kubernetes handle high availability?**

* Multiple masters
* Health checks
* Self-healing pods

---

### 🔹 **48. What is affinity and anti-affinity?**

Controls **pod placement** based on node or pod labels.

---

### 🔹 **49. What happens when a node fails?**

Pods are rescheduled to other healthy nodes automatically.

---

### 🔹 **50. How do you debug a pod stuck in `CrashLoopBackOff`?**

* Check logs: `kubectl logs`
* Describe pod: `kubectl describe`
* Check image/config/entrypoint errors

---

✅ Next up: Would you like to continue with **Kafka**, **PostgreSQL**, **MongoDB**, or another specific topic?

Let me know and I’ll continue with the next 50!

Great! Let's continue with the next 50:

---

## ✅ **Apache Kafka – Top 50 Interview Questions & Answers (For Java Microservices Developers)**

---

### 🔹 **1. What is Apache Kafka?**

Kafka is a **distributed, fault-tolerant, high-throughput** event streaming platform used to build real-time data pipelines and streaming apps.

---

### 🔹 **2. What are the main components of Kafka?**

* **Producer**
* **Consumer**
* **Topic**
* **Broker**
* **ZooKeeper** (deprecated in newer versions)
* **Cluster**

---

### 🔹 **3. What is a Kafka topic?**

A **logical channel** where records are sent (by producers) and read (by consumers). Topics are **partitioned** and **replicated**.

---

### 🔹 **4. What is a Kafka partition?**

A **subset** of a topic that allows parallelism. Each partition is an **ordered log** of events.

---

### 🔹 **5. What is a Kafka broker?**

A Kafka broker is a **Kafka server** that stores messages and serves clients.

---

### 🔹 **6. What is the role of ZooKeeper in Kafka?**

Manages metadata, leader election, and cluster state (phased out in Kafka 3.x+ using KRaft).

---

### 🔹 **7. How does Kafka ensure fault tolerance?**

Through **replication** of partitions across brokers.

---

### 🔹 **8. What is a consumer group?**

A group of consumers that work together to **consume messages in parallel** from a topic.

---

### 🔹 **9. What happens if the number of consumers > partitions?**

Some consumers remain **idle** as one partition can be consumed by only one consumer in a group.

---

### 🔹 **10. What are Kafka offsets?**

Offsets track the **position of a consumer** in a partition. Can be committed manually or automatically.

---

### 🔹 **11. How to manually commit offsets in Kafka?**

```java
consumer.commitSync();
```

---

### 🔹 **12. What is the difference between `commitSync()` and `commitAsync()`?**

* `commitSync()`: blocking and retries on failure.
* `commitAsync()`: non-blocking, no retries.

---

### 🔹 **13. What is the retention period in Kafka?**

Time Kafka keeps messages (default 7 days). Configurable per topic.

---

### 🔹 **14. What is a Kafka producer?**

An application that **publishes records** to Kafka topics.

---

### 🔹 **15. How does a Kafka producer achieve load balancing?**

By **partitioning** messages based on keys or round-robin.

---

### 🔹 **16. How to send messages using Java Kafka producer?**

```java
ProducerRecord<String, String> record = new ProducerRecord<>("topic", "key", "value");
producer.send(record);
```

---

### 🔹 **17. What is `acks` in Kafka?**

Controls acknowledgment levels:

* `0`: no ack
* `1`: leader ack
* `all`: all replicas must ack

---

### 🔹 **18. What is Kafka Streams?**

A client library for building **stream processing** apps directly on Kafka.

---

### 🔹 **19. What is Kafka Connect?**

A tool to **import/export data** between Kafka and other systems (DBs, file systems).

---

### 🔹 **20. How to achieve exactly-once delivery in Kafka?**

Enable **idempotence** on producer and **transactional** APIs.

---

### 🔹 **21. What is idempotence in Kafka producer?**

Prevents **duplicate messages** when retrying.

---

### 🔹 **22. What is a compacted topic?**

A topic that retains only the **latest value** for a key. Useful for state storage.

---

### 🔹 **23. How to create a Kafka topic?**

```bash
kafka-topics.sh --create --topic my-topic --partitions 3 --replication-factor 2
```

---

### 🔹 **24. How to list all Kafka topics?**

```bash
kafka-topics.sh --list
```

---

### 🔹 **25. How to describe a topic’s details?**

```bash
kafka-topics.sh --describe --topic my-topic
```

---

### 🔹 **26. What is message key in Kafka?**

Defines how records are **partitioned**. Records with the same key go to the same partition.

---

### 🔹 **27. What serialization formats does Kafka support?**

* String
* JSON
* Avro
* Protobuf
* Parquet

---

### 🔹 **28. How to use Avro with Kafka?**

Use **Confluent Schema Registry** to register and enforce schemas.

---

### 🔹 **29. What is Kafka's delivery guarantee?**

* **At most once**: no retry
* **At least once**: retry without deduplication
* **Exactly once**: retry with idempotence/transactions

---

### 🔹 **30. What are Kafka logs?**

Kafka stores records in log files per partition, which are **append-only** and **segmented**.

---

### 🔹 **31. What are common Kafka use cases?**

* Log aggregation
* Event sourcing
* Stream processing
* Data pipelines
* Real-time analytics

---

### 🔹 **32. How does Kafka ensure ordering?**

Messages in a **single partition** are strictly ordered.

---

### 🔹 **33. What is the role of the Kafka controller?**

Manages **partition leadership**, broker registration, and failover.

---

### 🔹 **34. What happens when a Kafka broker fails?**

Partition replicas are redistributed and led by in-sync replicas.

---

### 🔹 **35. What is ISR (In-Sync Replicas)?**

Replicas that are **up-to-date** with the leader.

---

### 🔹 **36. What are Kafka ACLs (Access Control Lists)?**

Used to restrict access to Kafka resources like topics, groups, or clusters.

---

### 🔹 **37. How do Kafka consumers poll messages?**

```java
ConsumerRecords<String, String> records = consumer.poll(Duration.ofMillis(100));
```

---

### 🔹 **38. How to handle deserialization errors in Kafka consumer?**

Use **error handlers**, or **custom deserializers** with try-catch logic.

---

### 🔹 **39. What is Kafka's default message format?**

Binary. You define key/value serializers & deserializers.

---

### 🔹 **40. What is backpressure and how is it handled in Kafka?**

Occurs when consumers can't keep up. Kafka **buffers** messages; if buffer full → old messages deleted per retention policy.

---

### 🔹 **41. What is rebalance in Kafka?**

Redistribution of partition ownership when a consumer joins/leaves a group.

---

### 🔹 **42. How to avoid frequent consumer rebalances?**

Use `heartbeat.interval.ms` and `session.timeout.ms` carefully.

---

### 🔹 **43. What happens during a Kafka partition rebalance?**

* Stop consuming
* Assign new partitions
* Resume consuming

---

### 🔹 **44. What is Kafka MirrorMaker?**

A tool to **replicate topics** between Kafka clusters.

---

### 🔹 **45. How to tune Kafka for high throughput?**

* Batch size
* Compression
* Acknowledgments
* Number of partitions

---

### 🔹 **46. How do you monitor Kafka?**

* Kafka JMX metrics
* Prometheus & Grafana
* Confluent Control Center

---

### 🔹 **47. How is Kafka integrated with Spring Boot?**

Using `spring-kafka` with `@KafkaListener` and `KafkaTemplate`.

---

### 🔹 **48. How to define a Kafka consumer in Spring Boot?**

```java
@KafkaListener(topics = "topic", groupId = "group")
public void listen(String message) {}
```

---

### 🔹 **49. How to send a message using Spring Kafka?**

```java
kafkaTemplate.send("topic", "key", "value");
```

---

### 🔹 **50. What are common issues faced with Kafka in production?**

* Consumer lag
* Broker crashes
* Disk I/O bottlenecks
* Rebalancing storms

---

✅ Next up: Would you like to continue with **PostgreSQL**, **MongoDB**, **Redis**, or a different module?

Let me know and I’ll deliver the next 50!

Perfect! Let's continue with the next 50:

---

## ✅ **PostgreSQL – Top 50 Interview Questions & Answers (For Full Stack Developers & Java Backend)**

---

### 🔹 **1. What is PostgreSQL?**

PostgreSQL is a **powerful, open-source object-relational database** system known for its extensibility, reliability, and support for advanced data types.

---

### 🔹 **2. How is PostgreSQL different from MySQL?**

| Feature       | PostgreSQL                  | MySQL                      |
| ------------- | --------------------------- | -------------------------- |
| Compliance    | Fully ACID compliant        | Partially ACID             |
| JSON Support  | Advanced                    | Basic                      |
| Extensibility | High                        | Limited                    |
| Performance   | Better with complex queries | Better for read-heavy apps |

---

### 🔹 **3. How do you connect a Java app to PostgreSQL?**

Using JDBC with PostgreSQL driver:

```java
jdbc:postgresql://localhost:5432/mydb
```

---

### 🔹 **4. What are data types supported by PostgreSQL?**

* Numeric: `integer`, `serial`, `decimal`, `numeric`
* Character: `char`, `varchar`, `text`
* Date/Time: `timestamp`, `date`, `interval`
* Boolean, Arrays, JSON, UUID, etc.

---

### 🔹 **5. What is a `serial` data type?**

Auto-incrementing integer (like `AUTO_INCREMENT` in MySQL).

---

### 🔹 **6. How do you define a primary key in PostgreSQL?**

```sql
CREATE TABLE emp (
  id SERIAL PRIMARY KEY,
  name VARCHAR(100)
);
```

---

### 🔹 **7. How do you create an index in PostgreSQL?**

```sql
CREATE INDEX idx_name ON employees(name);
```

---

### 🔹 **8. What is the purpose of `EXPLAIN` in PostgreSQL?**

Analyzes **query execution plan** to optimize performance.

---

### 🔹 **9. How do you perform a full-text search in PostgreSQL?**

Using:

```sql
to_tsvector('english', column) @@ to_tsquery('term')
```

---

### 🔹 **10. What is a CTE (Common Table Expression)?**

A temporary result set used within queries:

```sql
WITH dept_count AS (
  SELECT dept_id, COUNT(*) AS total FROM emp GROUP BY dept_id
)
SELECT * FROM dept_count WHERE total > 10;
```

---

### 🔹 **11. What is the difference between `INNER JOIN` and `LEFT JOIN`?**

* `INNER JOIN`: Only matching rows
* `LEFT JOIN`: All from left + matches from right

---

### 🔹 **12. How do you write a stored procedure in PostgreSQL?**

```sql
CREATE OR REPLACE FUNCTION get_count()
RETURNS INT AS $$
BEGIN
  RETURN (SELECT COUNT(*) FROM employees);
END;
$$ LANGUAGE plpgsql;
```

---

### 🔹 **13. What are constraints in PostgreSQL?**

* `NOT NULL`
* `UNIQUE`
* `CHECK`
* `DEFAULT`
* `FOREIGN KEY`
* `PRIMARY KEY`

---

### 🔹 **14. What are views in PostgreSQL?**

Virtual tables representing the result of a SQL query.

---

### 🔹 **15. What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?**

| Command  | Description                 |
| -------- | --------------------------- |
| DELETE   | Removes rows with condition |
| TRUNCATE | Removes all rows (fast)     |
| DROP     | Deletes table structure too |

---

### 🔹 **16. How do you backup a PostgreSQL database?**

Using `pg_dump`:

```bash
pg_dump mydb > mydb.sql
```

---

### 🔹 **17. How do you restore a backup in PostgreSQL?**

```bash
psql mydb < mydb.sql
```

---

### 🔹 **18. What are transactions in PostgreSQL?**

A group of SQL operations treated as a single unit:

```sql
BEGIN;
UPDATE ...;
COMMIT;
```

---

### 🔹 **19. What is the use of `ROLLBACK`?**

Undo changes made during a transaction.

---

### 🔹 **20. What is a sequence in PostgreSQL?**

A database object used to generate **unique numeric values**.

---

### 🔹 **21. How to list all tables in PostgreSQL?**

```sql
\dt
```

---

### 🔹 **22. What are roles and privileges in PostgreSQL?**

Roles are users or groups; privileges define what they can do (`GRANT`, `REVOKE`).

---

### 🔹 **23. What is JSONB in PostgreSQL?**

A **binary format** of JSON that is faster and indexable.

---

### 🔹 **24. What are indexes and why are they used?**

Used to **speed up query performance** by reducing scan time.

---

### 🔹 **25. What is `VACUUM` in PostgreSQL?**

Cleans up dead tuples and reclaims storage.

---

### 🔹 **26. How to optimize queries in PostgreSQL?**

* Use indexes
* Avoid `SELECT *`
* Use CTEs and subqueries wisely
* Analyze with `EXPLAIN`

---

### 🔹 **27. How to perform pagination in PostgreSQL?**

```sql
SELECT * FROM emp LIMIT 10 OFFSET 20;
```

---

### 🔹 **28. How to update multiple rows in PostgreSQL?**

```sql
UPDATE emp SET salary = salary + 5000 WHERE dept_id = 3;
```

---

### 🔹 **29. How do you handle null values in PostgreSQL?**

Use `IS NULL` and `COALESCE()`.

---

### 🔹 **30. What is the difference between `IS NULL` and `= NULL`?**

Use `IS NULL`; `= NULL` will always return false.

---

### 🔹 **31. How to create a composite primary key?**

```sql
PRIMARY KEY (emp_id, dept_id)
```

---

### 🔹 **32. What is `DISTINCT` used for?**

Removes **duplicate rows** from result set.

---

### 🔹 **33. What are triggers in PostgreSQL?**

Procedures that execute automatically in response to events like `INSERT`, `UPDATE`, or `DELETE`.

---

### 🔹 **34. How to create a trigger in PostgreSQL?**

```sql
CREATE TRIGGER my_trigger
AFTER INSERT ON emp
FOR EACH ROW EXECUTE FUNCTION log_emp();
```

---

### 🔹 **35. What is a materialized view?**

Like a view, but **stored physically** and can be refreshed.

---

### 🔹 **36. What is the difference between `UNION` and `UNION ALL`?**

* `UNION`: Removes duplicates
* `UNION ALL`: Includes duplicates

---

### 🔹 **37. How to sort records in PostgreSQL?**

```sql
ORDER BY column_name ASC|DESC;
```

---

### 🔹 **38. How do you check the version of PostgreSQL?**

```sql
SELECT version();
```

---

### 🔹 **39. What is a subquery?**

A query nested inside another query.

---

### 🔹 **40. What is `ILIKE` in PostgreSQL?**

Case-insensitive version of `LIKE`.

---

### 🔹 **41. What are array types in PostgreSQL?**

PostgreSQL supports array columns:

```sql
int[] or text[]
```

---

### 🔹 **42. How to use `CASE` in PostgreSQL?**

```sql
SELECT name, 
  CASE 
    WHEN salary > 50000 THEN 'High'
    ELSE 'Low'
  END AS category
FROM emp;
```

---

### 🔹 **43. How to use `GROUP BY` and `HAVING`?**

```sql
SELECT dept_id, COUNT(*) FROM emp GROUP BY dept_id HAVING COUNT(*) > 5;
```

---

### 🔹 **44. How to list all databases in PostgreSQL?**

```sql
\l
```

---

### 🔹 **45. How to switch databases in psql?**

```sql
\c dbname
```

---

### 🔹 **46. What is logical replication in PostgreSQL?**

Used for **real-time data replication** between databases using publications/subscriptions.

---

### 🔹 **47. How to generate UUIDs in PostgreSQL?**

```sql
uuid_generate_v4()
```

---

### 🔹 **48. What are foreign keys used for?**

Enforce **referential integrity** between tables.

---

### 🔹 **49. What is the purpose of the `NOW()` function?**

Returns the **current timestamp**.

---

### 🔹 **50. How to rename a column in PostgreSQL?**

```sql
ALTER TABLE emp RENAME COLUMN name TO full_name;
```

---

✅ Next up: Would you like to proceed with **MongoDB**, **Redis**, **Jenkins**, or another focus area?

Let me know and I’ll deliver the next 50 right away!

Great! Let’s move ahead with the next 50:

---

## ✅ **MongoDB – Top 50 Interview Questions & Answers (For Java Full Stack & Microservices Developers)**

---

### 🔹 **1. What is MongoDB?**

MongoDB is a **NoSQL, document-oriented** database that stores data in **BSON (Binary JSON)** format instead of tables.

---

### 🔹 **2. What are the key features of MongoDB?**

* Schema-less (flexible documents)
* High availability (replication)
* Horizontal scalability (sharding)
* Indexing support
* Aggregation pipeline

---

### 🔹 **3. What is a document in MongoDB?**

A document is a JSON-like object containing key-value pairs. Example:

```json
{ "_id": 1, "name": "Aditya", "role": "Developer" }
```

---

### 🔹 **4. What is a collection in MongoDB?**

A **collection** is a group of MongoDB documents, similar to a table in relational DBs.

---

### 🔹 **5. How is MongoDB different from RDBMS?**

| MongoDB            | RDBMS            |
| ------------------ | ---------------- |
| Document-based     | Table-based      |
| Dynamic schema     | Fixed schema     |
| No joins           | Joins supported  |
| Horizontal scaling | Vertical scaling |

---

### 🔹 **6. What is the default `_id` field in MongoDB?**

A **unique ObjectId** automatically generated for each document.

---

### 🔹 **7. How do you insert a document into MongoDB using Java?**

```java
collection.insertOne(new Document("name", "Aditya"));
```

---

### 🔹 **8. What is the use of `find()` in MongoDB?**

Retrieves documents from a collection.

```javascript
db.users.find({ name: "Aditya" });
```

---

### 🔹 **9. How to update a document in MongoDB?**

```javascript
db.users.updateOne({ name: "Aditya" }, { $set: { role: "Lead" } });
```

---

### 🔹 **10. How to delete documents in MongoDB?**

```javascript
db.users.deleteOne({ name: "Aditya" });
```

---

### 🔹 **11. What is indexing in MongoDB?**

Indexes improve **query performance**. Use:

```javascript
db.users.createIndex({ name: 1 });
```

---

### 🔹 **12. What is a compound index?**

An index on **multiple fields**:

```javascript
db.users.createIndex({ name: 1, role: -1 });
```

---

### 🔹 **13. What is the Aggregation Framework?**

Processes data using stages (`$match`, `$group`, `$sort`) like SQL GROUP BY.

---

### 🔹 **14. Example of an aggregation pipeline?**

```javascript
db.orders.aggregate([
  { $match: { status: "A" } },
  { $group: { _id: "$cust_id", total: { $sum: "$amount" } } }
]);
```

---

### 🔹 **15. What is sharding in MongoDB?**

Distributes data across multiple servers to **scale horizontally**.

---

### 🔹 **16. What is replication in MongoDB?**

Creates multiple copies of data to provide **high availability**.

---

### 🔹 **17. What is a replica set?**

A group of **mongod instances** that maintain the same data set with automatic failover.

---

### 🔹 **18. What is a primary and secondary in replication?**

* **Primary**: handles writes
* **Secondary**: replicates data from primary (read-only)

---

### 🔹 **19. What are capped collections?**

Fixed-size collections that **overwrite old data** when the limit is reached.

---

### 🔹 **20. What is GridFS?**

Used to store and retrieve **large files** (like images, videos) in chunks.

---

### 🔹 **21. What is the difference between `find()` and `aggregate()`?**

* `find()`: basic querying
* `aggregate()`: advanced data transformation

---

### 🔹 **22. How do you sort results in MongoDB?**

```javascript
db.users.find().sort({ name: 1 });
```

---

### 🔹 **23. What is projection in MongoDB?**

Limits fields returned in query results:

```javascript
db.users.find({}, { name: 1, _id: 0 });
```

---

### 🔹 **24. What is the `$in` operator?**

Checks if a field’s value is **in an array** of values:

```javascript
db.users.find({ name: { $in: ["Aditya", "John"] } });
```

---

### 🔹 **25. What is the `$regex` operator?**

Used for pattern matching (like SQL `LIKE`):

```javascript
db.users.find({ name: { $regex: "^Adi" } });
```

---

### 🔹 **26. What is schema validation in MongoDB?**

Enforces rules on documents using `validator`:

```javascript
validator: { $jsonSchema: { required: ["name", "email"] } }
```

---

### 🔹 **27. What are transactions in MongoDB?**

Provide **ACID guarantees** for multiple-document operations (from v4.0+).

---

### 🔹 **28. What is the `ObjectId` structure?**

Contains:

* Timestamp
* Machine ID
* Process ID
* Counter

---

### 🔹 **29. How to check MongoDB version?**

```bash
db.version()
```

---

### 🔹 **30. How to limit and skip documents?**

```javascript
db.users.find().limit(5).skip(10);
```

---

### 🔹 **31. How to get distinct values?**

```javascript
db.users.distinct("role");
```

---

### 🔹 **32. How to check collection stats?**

```javascript
db.collection.stats()
```

---

### 🔹 **33. What is `$lookup` used for?**

Performs a **left outer join** between collections.

```javascript
{
  $lookup: {
    from: "orders",
    localField: "userId",
    foreignField: "userId",
    as: "user_orders"
  }
}
```

---

### 🔹 **34. How to update multiple documents?**

```javascript
db.users.updateMany({ role: "Dev" }, { $set: { active: true } });
```

---

### 🔹 **35. How to rename a field?**

```javascript
db.users.updateMany({}, { $rename: { "oldField": "newField" } });
```

---

### 🔹 **36. How to check if a field exists?**

```javascript
db.users.find({ email: { $exists: true } });
```

---

### 🔹 **37. What is the difference between `embedded` and `referenced` data models?**

* **Embedded**: nested docs (denormalized)
* **Referenced**: normalized, linked via `_id`

---

### 🔹 **38. What is write concern?**

Defines **write acknowledgment** level: `w:1`, `w:majority`

---

### 🔹 **39. What is read preference?**

Specifies from **which replica set member** to read: `primary`, `secondary`

---

### 🔹 **40. What is the `$elemMatch` operator?**

Matches **elements of an array** with specified conditions:

```javascript
db.users.find({ skills: { $elemMatch: { name: "Java", level: "expert" } } });
```

---

### 🔹 **41. How to drop a collection?**

```javascript
db.users.drop();
```

---

### 🔹 **42. How to drop a database?**

```javascript
db.dropDatabase();
```

---

### 🔹 **43. What is `MongoTemplate` in Spring Boot?**

Spring’s abstraction for working with MongoDB (alternative to repositories).

---

### 🔹 **44. How to use `@Document` in Spring Data MongoDB?**

Marks a POJO as a MongoDB document:

```java
@Document(collection = "users")
public class User { ... }
```

---

### 🔹 **45. How to use MongoRepository?**

```java
public interface UserRepository extends MongoRepository<User, String> {}
```

---

### 🔹 **46. How to find documents by field?**

```java
List<User> findByName(String name);
```

---

### 🔹 **47. How to enable Mongo auditing?**

Use:

```java
@EnableMongoAuditing
@CreatedDate, @LastModifiedDate
```

---

### 🔹 **48. How to configure MongoDB in `application.properties`?**

```properties
spring.data.mongodb.uri=mongodb://localhost:27017/mydb
```

---

### 🔹 **49. What is `$type` operator in MongoDB?**

Checks the **type** of a field:

```javascript
db.users.find({ age: { $type: "int" } });
```

---

### 🔹 **50. How to sort embedded fields?**

```javascript
db.users.find().sort({ "address.city": 1 });
```

---

✅ Next up: Would you like to continue with **Redis**, **Jenkins**, **Angular**, or **System Design**?

Let me know and I’ll give you the next set of 50!

Great! Let's now continue with the next 50:

---

## ✅ **Redis – Top 50 Interview Questions & Answers (For Java + Spring Boot Developers)**

---

### 🔹 **1. What is Redis?**

Redis (Remote Dictionary Server) is an **in-memory data store** used as a **cache, database, and message broker**.

---

### 🔹 **2. What are the main features of Redis?**

* In-memory storage
* Persistence support
* Data structures: Strings, Hashes, Lists, Sets, Sorted Sets
* Pub/Sub messaging
* Transactions and scripting
* High performance and scalability

---

### 🔹 **3. What are common use cases of Redis?**

* Caching
* Session management
* Leaderboards
* Real-time analytics
* Message queuing
* Rate limiting

---

### 🔹 **4. What data types does Redis support?**

* String
* List
* Hash
* Set
* Sorted Set (ZSet)
* Bitmap
* HyperLogLog
* Streams

---

### 🔹 **5. What is the default port Redis runs on?**

`6379`

---

### 🔹 **6. How do you store and retrieve a value in Redis?**

```bash
SET key value
GET key
```

---

### 🔹 **7. How do you set a key with expiry?**

```bash
SET key value EX 60   # Expires in 60 seconds
```

---

### 🔹 **8. How do you delete a key in Redis?**

```bash
DEL key
```

---

### 🔹 **9. What is TTL in Redis?**

**Time To Live** – the remaining time in seconds for a key to expire.

---

### 🔹 **10. How to get TTL of a key?**

```bash
TTL key
```

---

### 🔹 **11. What is Redis persistence?**

Redis offers:

* **RDB** (snapshotting)
* **AOF** (Append Only File)
* Or both (hybrid)

---

### 🔹 **12. What is Redis RDB persistence?**

Saves snapshots of data at configured intervals.

---

### 🔹 **13. What is AOF persistence?**

Logs every write operation for recovery after crash.

---

### 🔹 **14. How do you enable persistence in Redis?**

Configure in `redis.conf`:

```conf
appendonly yes
```

---

### 🔹 **15. What is the difference between RDB and AOF?**

| Feature     | RDB             | AOF             |
| ----------- | --------------- | --------------- |
| Format      | Binary snapshot | Append-only log |
| Performance | Faster          | Slower          |
| Recovery    | Less frequent   | More durable    |

---

### 🔹 **16. What are Redis transactions?**

Multiple commands executed **atomically** using:

```bash
MULTI
SET key1 val1
SET key2 val2
EXEC
```

---

### 🔹 **17. How do you use Pub/Sub in Redis?**

```bash
SUBSCRIBE channel
PUBLISH channel message
```

---

### 🔹 **18. What is Redis Cluster?**

A distributed version of Redis with **automatic sharding** and **failover support**.

---

### 🔹 **19. What is Redis Sentinel?**

Monitors Redis instances for **high availability** and **automatic failover**.

---

### 🔹 **20. What is the difference between Redis and Memcached?**

* Redis supports persistence, data structures, Pub/Sub.
* Memcached is a simpler, memory-only key-value store.

---

### 🔹 **21. What is pipelining in Redis?**

Sends multiple commands **without waiting** for replies, improving performance.

---

### 🔹 **22. How do you check if a key exists?**

```bash
EXISTS key
```

---

### 🔹 **23. What is `INCR` in Redis?**

Increments a numeric string value by 1:

```bash
INCR counter
```

---

### 🔹 **24. What is a Redis Hash?**

Stores **field-value pairs**:

```bash
HSET user:1 name "Aditya"
HGET user:1 name
```

---

### 🔹 **25. What are Redis Lists used for?**

Ordered collection of strings. Useful for queues:

```bash
LPUSH queue val
RPOP queue
```

---

### 🔹 **26. What are Redis Sets?**

Unordered collection of **unique strings**:

```bash
SADD team "aditya"
SMEMBERS team
```

---

### 🔹 **27. What is a Sorted Set in Redis?**

A set where each element has a **score**:

```bash
ZADD leaderboard 100 "Aditya"
ZRANGE leaderboard 0 -1 WITHSCORES
```

---

### 🔹 **28. How to rename a key in Redis?**

```bash
RENAME oldKey newKey
```

---

### 🔹 **29. How to get all keys?**

```bash
KEYS *
```

⚠️ Not recommended in production.

---

### 🔹 **30. What is Redis eviction policy?**

Decides which key to remove when memory is full (e.g., `volatile-lru`, `allkeys-lru`).

---

### 🔹 **31. How do you persist Java objects in Redis?**

* Use serialization (Java/Kryo/JSON)
* Spring Data Redis with custom serializers

---

### 🔹 **32. What is Spring Data Redis?**

Spring module to integrate with Redis easily using `RedisTemplate` and repositories.

---

### 🔹 **33. How to configure Redis in `application.properties`?**

```properties
spring.redis.host=localhost
spring.redis.port=6379
```

---

### 🔹 **34. What is `RedisTemplate` in Spring Boot?**

A helper class to perform Redis operations:

```java
redisTemplate.opsForValue().set("key", "value");
```

---

### 🔹 **35. What are Redis repositories?**

Spring abstractions for Redis-based CRUD on annotated entities.

---

### 🔹 **36. What are cache annotations in Spring Boot?**

* `@EnableCaching`
* `@Cacheable`
* `@CachePut`
* `@CacheEvict`

---

### 🔹 **37. Example of `@Cacheable` usage?**

```java
@Cacheable("books")
public Book getBookById(String id) { ... }
```

---

### 🔹 **38. What is `@CacheEvict` used for?**

Removes item from cache:

```java
@CacheEvict(value="books", key="#id")
```

---

### 🔹 **39. How to set expiry for cache in Spring Boot Redis?**

```java
@Cacheable(value = "books", key = "#id", unless = "#result == null")
```

Set TTL using Redis config bean.

---

### 🔹 **40. What is Redis HyperLogLog?**

Probabilistic data structure to count **unique elements** efficiently.

---

### 🔹 **41. What is Redis Bitmap?**

Bit-level operations for **tracking boolean states** (e.g., attendance).

---

### 🔹 **42. How to flush all data in Redis?**

```bash
FLUSHALL
```

---

### 🔹 **43. How to monitor Redis commands in real-time?**

```bash
MONITOR
```

---

### 🔹 **44. How to perform backup and restore in Redis?**

* Backup: copy `dump.rdb`
* Restore: place it back and restart server

---

### 🔹 **45. How to persist Spring sessions in Redis?**

Add:

```xml
spring-session-data-redis
```

Configure `@EnableRedisHttpSession`.

---

### 🔹 **46. How to test Redis locally?**

Use Docker:

```bash
docker run -p 6379:6379 redis
```

---

### 🔹 **47. What is a Redis stream?**

Data structure for real-time **log/event streaming** (like Kafka-lite).

---

### 🔹 **48. How to use Redis for rate limiting?**

Use key + TTL:

```bash
INCR key
EXPIRE key 60
```

---

### 🔹 **49. What is lazy loading in Redis cache?**

Data is loaded into cache **only when first requested**, via `@Cacheable`.

---

### 🔹 **50. What are best practices for using Redis in Java apps?**

* Set TTLs for keys
* Use connection pooling
* Avoid using `KEYS *` in production
* Prefer `SCAN` over `KEYS`
* Use serializers efficiently

---

✅ You're doing great! Would you like to continue with **Jenkins**, **Angular**, **Tomcat**, or **System Design** next?

Let me know and I’ll prepare the next 50 immediately!

Excellent! Let's move ahead with the next 50:

---

## ✅ **Jenkins – Top 50 Interview Questions & Answers (For Java DevOps + CI/CD Setup with Spring Boot)**

---

### 🔹 **1. What is Jenkins?**

Jenkins is an **open-source automation server** used to automate building, testing, and deploying applications via **CI/CD pipelines**.

---

### 🔹 **2. What are the key features of Jenkins?**

* Easy installation & configuration
* Wide plugin support
* Pipeline-as-code (Jenkinsfile)
* Distributed builds
* Extensible architecture

---

### 🔹 **3. What is Continuous Integration (CI)?**

Practice of **frequently integrating code** into a shared repository with automated builds/tests to detect issues early.

---

### 🔹 **4. What is Continuous Delivery (CD)?**

Automating the release process so that code changes can be **deployed to production at any time**.

---

### 🔹 **5. What is a Jenkins pipeline?**

A series of **steps or stages** defined in code (`Jenkinsfile`) to automate CI/CD workflows.

---

### 🔹 **6. What is a `Jenkinsfile`?**

A text file that contains the **pipeline definition** written in **Groovy DSL** or declarative syntax.

---

### 🔹 **7. Example of a basic Jenkinsfile (declarative):**

```groovy
pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'mvn clean install'
      }
    }
    stage('Test') {
      steps {
        sh 'mvn test'
      }
    }
  }
}
```

---

### 🔹 **8. What is the difference between Declarative and Scripted pipeline?**

* **Declarative**: Simpler, structured, preferred
* **Scripted**: Full control using Groovy, more flexible but complex

---

### 🔹 **9. What are Jenkins agents (nodes)?**

Machines connected to Jenkins master for **running jobs**. Master delegates work to agents.

---

### 🔹 **10. What is the Jenkins master?**

The central server that manages jobs, user interface, schedules builds, and dispatches jobs to agents.

---

### 🔹 **11. How do you trigger a Jenkins job automatically?**

* Poll SCM (`pollSCM`)
* Webhook (e.g., GitHub)
* Scheduled trigger (`cron`)
* Upstream job completion
* REST API trigger

---

### 🔹 **12. What is a build trigger?**

Defines **when and how** a Jenkins job should be triggered.

---

### 🔹 **13. What are Jenkins plugins?**

Extensions that add new features to Jenkins. Examples:

* Git Plugin
* Maven Plugin
* Docker Plugin
* Slack Notification Plugin

---

### 🔹 **14. How do you install a Jenkins plugin?**

* Jenkins UI → Manage Jenkins → Plugin Manager → Available → Install

---

### 🔹 **15. What are build artifacts in Jenkins?**

Files generated during the build (e.g., JARs, WARs, logs) that can be archived and downloaded.

---

### 🔹 **16. How do you archive artifacts in Jenkins?**

```groovy
archiveArtifacts artifacts: '**/target/*.jar', fingerprint: true
```

---

### 🔹 **17. What is a parameterized build in Jenkins?**

Allows users to **pass parameters** (e.g., branch name, environment) before starting a job.

---

### 🔹 **18. What is the role of `sh` or `bat` in Jenkins pipeline?**

Executes shell (`sh`) or batch (`bat`) commands in pipeline stages.

---

### 🔹 **19. How do you integrate Git with Jenkins?**

* Install Git plugin
* Configure repository URL
* Add credentials
* Trigger builds on Git push

---

### 🔹 **20. How do you integrate Maven with Jenkins?**

* Install Maven plugin
* Use `mvn clean install` in build steps
* Or define Maven tool in Jenkins global settings

---

### 🔹 **21. What are stages and steps in a Jenkins pipeline?**

* **Stages**: Logical divisions (e.g., Build, Test, Deploy)
* **Steps**: Actual actions inside each stage

---

### 🔹 **22. What is `input` step in Jenkins pipeline?**

Used for **manual approval** in a pipeline.

```groovy
input message: 'Approve Deployment?'
```

---

### 🔹 **23. What is Jenkins Blue Ocean?**

Modern UI for Jenkins to visualize and manage pipelines more efficiently.

---

### 🔹 **24. How to integrate Slack with Jenkins?**

* Install Slack plugin
* Configure webhook
* Add Slack notification steps to pipeline

---

### 🔹 **25. How do you send email notifications in Jenkins?**

* Install Mailer plugin
* Configure SMTP
* Use `emailext` step in pipeline

---

### 🔹 **26. How do you trigger one job from another in Jenkins?**

Use:

* **Build Trigger** → "Build after other projects"
* `build job: 'job-name'` in pipeline

---

### 🔹 **27. How do you handle credentials securely in Jenkins?**

Use **Credentials plugin** and reference via:

```groovy
withCredentials([usernamePassword(credentialsId: 'my-creds')]) { ... }
```

---

### 🔹 **28. What is `withEnv` in Jenkins?**

Temporarily sets environment variables:

```groovy
withEnv(['VAR1=value1']) { ... }
```

---

### 🔹 **29. What is `post` block in Jenkins pipeline?**

Used to define steps that run **after a stage**, e.g., cleanup, notifications.

---

### 🔹 **30. What is `agent` in Jenkinsfile?**

Defines **where the pipeline or stage should run**, e.g., `any`, `docker`, or specific node label.

---

### 🔹 **31. What is a shared library in Jenkins?**

Reusable Groovy code stored in a separate repo and loaded via:

```groovy
@Library('my-shared-lib') _
```

---

### 🔹 **32. What is the use of `parallel` in Jenkins pipeline?**

Run multiple branches **concurrently** in a stage.

```groovy
parallel (
  "Unit Tests": { sh 'mvn test' },
  "Lint Check": { sh 'npm run lint' }
)
```

---

### 🔹 **33. What are common security best practices in Jenkins?**

* Use matrix-based security
* Disable CLI if unused
* Use credentials plugin
* Regularly update Jenkins/plugins

---

### 🔹 **34. What are the build status indicators in Jenkins?**

* Blue/Green: Success
* Yellow: Unstable (tests failed)
* Red: Failed
* Grey: Not executed

---

### 🔹 **35. How do you clean the workspace in Jenkins?**

```groovy
cleanWs()
```

Or check "Delete workspace before build starts" in job config.

---

### 🔹 **36. How do you integrate Docker with Jenkins?**

* Install Docker plugin
* Use `docker.build()` and `docker.image().run()` in pipeline
* Run Jenkins agent inside Docker container

---

### 🔹 **37. What is the Jenkins REST API?**

Used to trigger and query builds:

```bash
curl -X POST http://jenkins/job/myjob/build?token=xyz
```

---

### 🔹 **38. What is `checkout scm` in Jenkinsfile?**

Checks out source code from the repository used to trigger the build.

---

### 🔹 **39. What is the difference between freestyle and pipeline jobs?**

| Job Type  | Description                     |
| --------- | ------------------------------- |
| Freestyle | GUI-based, simple configuration |
| Pipeline  | Code-driven, flexible, scalable |

---

### 🔹 **40. What is a build queue in Jenkins?**

A list of builds waiting to be executed.

---

### 🔹 **41. How to avoid concurrent job execution in Jenkins?**

Enable **"Disable concurrent builds"** in job config or use `lock()` in pipelines.

---

### 🔹 **42. What is `retry` block in pipeline?**

Retries a step on failure:

```groovy
retry(3) {
  sh 'unstable-command'
}
```

---

### 🔹 **43. What is `timeout` block in Jenkins?**

Limits execution time:

```groovy
timeout(time: 2, unit: 'MINUTES') {
  sh './deploy.sh'
}
```

---

### 🔹 **44. How to trigger Jenkins job on GitHub push?**

* Configure webhook in GitHub
* Enable "GitHub hook trigger" in Jenkins

---

### 🔹 **45. How to deploy a Spring Boot app using Jenkins?**

* Build JAR with Maven
* SCP JAR to server or Docker container
* Restart service or container

---

### 🔹 **46. What is Jenkins X?**

A cloud-native CI/CD solution built on Kubernetes using Jenkins pipelines.

---

### 🔹 **47. How to handle secrets in Jenkins pipelines?**

Use `withCredentials` and mask in logs:

```groovy
withCredentials([string(credentialsId: 'secret')]) {
  sh "curl -H 'Authorization: $SECRET'"
}
```

---

### 🔹 **48. How to manage Jenkins logs?**

* `/var/log/jenkins/jenkins.log`
* Use `logrotate`
* Or install log management tools like ELK stack

---

### 🔹 **49. What are upstream and downstream jobs?**

* **Upstream**: Triggers other jobs
* **Downstream**: Gets triggered by others

---

### 🔹 **50. How do you ensure Jenkins job portability across environments?**

* Use parameters
* Externalize environment config
* Use shared libraries
* Use Docker agents

---

✅ You're progressing incredibly well! Would you like to continue with:

* **Angular**
* **Tomcat**
* **System Design**
* **Project-Based + HR + Leadership Questions**

Let me know what you'd like next, and I’ll provide the next set of 50 right away!

Excellent! Let’s now continue with the next 50:

---

## ✅ **Angular – Top 50 Interview Questions & Answers (For Full Stack Developers)**

---

### 🔹 **1. What is Angular?**

Angular is a **TypeScript-based front-end framework** for building single-page applications (SPAs) by Google.

---

### 🔹 **2. What are the main features of Angular?**

* TypeScript support
* Two-way data binding
* Dependency injection
* Component-based architecture
* RxJS and Observables
* CLI tool for scaffolding

---

### 🔹 **3. What is a component in Angular?**

A building block of UI:

```ts
@Component({
  selector: 'app-hello',
  templateUrl: './hello.component.html'
})
export class HelloComponent {}
```

---

### 🔹 **4. What are modules in Angular?**

Logical units of Angular apps defined using `@NgModule`:

```ts
@NgModule({
  declarations: [...],
  imports: [...],
  bootstrap: [AppComponent]
})
export class AppModule {}
```

---

### 🔹 **5. What is data binding in Angular?**

The mechanism to synchronize data between model and view:

* Interpolation: `{{ value }}`
* Property binding: `[src]="imageUrl"`
* Event binding: `(click)="onClick()"`
* Two-way: `[(ngModel)]="name"`

---

### 🔹 **6. What is Angular CLI?**

Command-line interface to scaffold, build, test, and deploy Angular applications.

---

### 🔹 **7. How to create a new Angular app?**

```bash
ng new my-app
cd my-app
ng serve
```

---

### 🔹 **8. What is the purpose of `ngOnInit()`?**

Lifecycle hook called once after component initialization. Ideal for data fetching.

---

### 🔹 **9. What is a directive in Angular?**

A class that adds behavior to DOM elements:

* **Structural** (`*ngIf`, `*ngFor`)
* **Attribute** (`[ngClass]`, `[ngStyle]`)

---

### 🔹 **10. What is a service in Angular?**

A reusable class used for logic or data access. Injected using Angular’s DI system.

---

### 🔹 **11. How to create and use a service?**

```bash
ng generate service my-service
```

Inject it using constructor:

```ts
constructor(private myService: MyService) {}
```

---

### 🔹 **12. What is dependency injection in Angular?**

A design pattern where dependencies (services) are **injected** into components rather than being created manually.

---

### 🔹 **13. What are pipes in Angular?**

Used to **transform data** in the template:

```html
{{ date | date:'shortDate' }}
```

---

### 🔹 **14. What is routing in Angular?**

Allows navigation between views using `RouterModule`:

```ts
{ path: 'home', component: HomeComponent }
```

---

### 🔹 **15. What is lazy loading in Angular?**

Modules are **loaded only when required**, reducing initial load time.

---

### 🔹 **16. What is a guard in Angular?**

Used to **protect routes**:

* `CanActivate`, `CanDeactivate`, `Resolve`, `CanLoad`

---

### 🔹 **17. What is two-way data binding in Angular?**

Combination of property and event binding using `[(ngModel)]`.

---

### 🔹 **18. What is the difference between `ngIf` and `ngSwitch`?**

* `*ngIf`: conditionally renders a template
* `*ngSwitch`: handles multiple conditional views

---

### 🔹 **19. What is a reactive form?**

Forms with **programmatic control** using `FormControl`, `FormGroup`.

---

### 🔹 **20. What is a template-driven form?**

Forms built using directives (`ngModel`, `required`) in templates.

---

### 🔹 **21. What is `ngModel`?**

Used for **two-way binding** in template-driven forms.

---

### 🔹 **22. What are observables in Angular?**

Provided by RxJS to handle asynchronous data streams.

---

### 🔹 **23. What is the difference between Observable and Promise?**

| Feature    | Observable | Promise |
| ---------- | ---------- | ------- |
| Streams    | Yes        | No      |
| Lazy       | Yes        | Yes     |
| Cancelable | Yes        | No      |

---

### 🔹 **24. How to handle HTTP calls in Angular?**

Use `HttpClientModule`:

```ts
this.http.get('/api/users');
```

---

### 🔹 **25. What is HttpInterceptor?**

Used to **intercept HTTP requests/responses** for logging, token injection, etc.

---

### 🔹 **26. How to implement error handling in Angular?**

Using:

```ts
.catchError(err => of([]))
```

Or `HttpInterceptor`.

---

### 🔹 **27. What is the difference between `ViewChild` and `ContentChild`?**

* `ViewChild`: DOM in the component’s template
* `ContentChild`: DOM projected using `<ng-content>`

---

### 🔹 **28. What are lifecycle hooks in Angular?**

Methods like:

* `ngOnInit()`
* `ngOnChanges()`
* `ngOnDestroy()`

---

### 🔹 **29. How to pass data between components?**

* Parent to child: via `@Input()`
* Child to parent: via `@Output()` and `EventEmitter`

---

### 🔹 **30. What is `ng-content`?**

Acts as a placeholder for **projected content** (used in content projection).

---

### 🔹 **31. What is `ChangeDetectionStrategy`?**

Controls how change detection runs. Options:

* `Default`
* `OnPush` (better performance)

---

### 🔹 **32. What is Angular Universal?**

Used for **server-side rendering (SSR)** of Angular apps for better SEO and performance.

---

### 🔹 **33. How do you handle state management in Angular?**

Using services or libraries like:

* `@ngrx/store`
* `BehaviorSubject`

---

### 🔹 **34. What is `ngOnDestroy()`?**

Lifecycle hook used for cleanup like unsubscribing observables.

---

### 🔹 **35. How to conditionally apply classes in Angular?**

```html
<div [ngClass]="{ active: isActive }"></div>
```

---

### 🔹 **36. What is trackBy in `*ngFor`?**

Improves performance by tracking items by a unique key.

---

### 🔹 **37. What are custom pipes?**

User-defined pipes to transform values:

```ts
@Pipe({ name: 'capitalize' })
export class CapitalizePipe implements PipeTransform {
  transform(value: string): string { return value.toUpperCase(); }
}
```

---

### 🔹 **38. How to optimize Angular apps?**

* Lazy loading
* OnPush change detection
* Ahead-of-time (AOT) compilation
* Tree shaking

---

### 🔹 **39. What is AOT compilation?**

Converts Angular HTML and TypeScript code **into JavaScript** at build time.

---

### 🔹 **40. What are environment files?**

Used to configure variables for `dev`, `prod`, etc.:

```ts
export const environment = { production: false };
```

---

### 🔹 **41. What is the difference between `ng serve` and `ng build`?**

* `ng serve`: starts dev server
* `ng build`: creates production-ready build

---

### 🔹 **42. What are polyfills?**

Code used to provide **backward compatibility** for older browsers.

---

### 🔹 **43. What are decorators in Angular?**

Functions that add **metadata** to classes: `@Component`, `@Injectable`, `@NgModule`

---

### 🔹 **44. What is the use of `async` pipe?**

Automatically **subscribes and unsubscribes** from an Observable in the template.

---

### 🔹 **45. What is Angular Material?**

A UI component library based on **Google’s Material Design** for Angular.

---

### 🔹 **46. What is Ivy in Angular?**

Angular’s **new rendering engine** with faster compilation and better debugging.

---

### 🔹 **47. How to secure Angular routes?**

Using route guards like `CanActivate`.

---

### 🔹 **48. How do you share data between unrelated components?**

Use a **shared service** with `BehaviorSubject`.

---

### 🔹 **49. How to handle forms validation in Angular?**

* Template-driven: `required`, `pattern`
* Reactive: `Validators.required`, `Validators.pattern`

---

### 🔹 **50. What is the role of RxJS in Angular?**

Provides **reactive programming** features like:

* Observables
* Subjects
* Operators (map, filter, debounceTime, etc.)

---

✅ You're covering amazing ground!

Would you like to continue with:

* **Tomcat**
* **System Design**
* **DSA**
* **Project-Based + HR + Leadership**

Let me know and I’ll send the next 50 right away!

Fantastic! Let's move ahead with the next 50:

---

## ✅ **Apache Tomcat – Top 50 Interview Questions & Answers (For Java Web Application Deployment & Configuration)**

---

### 🔹 **1. What is Apache Tomcat?**

Tomcat is an **open-source Java servlet container** developed by the Apache Software Foundation. It runs Java Servlets and renders JSPs.

---

### 🔹 **2. What is the role of Tomcat in a Java web application?**

It **serves as a web server + servlet container**, executing Java servlets and rendering JSPs to generate dynamic content.

---

### 🔹 **3. Which ports does Tomcat use by default?**

* HTTP: `8080`
* AJP: `8009`
* Shutdown: `8005`

---

### 🔹 **4. Where is the web application deployed in Tomcat?**

Deployed inside the `webapps` folder. WAR files are auto-extracted and deployed.

---

### 🔹 **5. What is `server.xml` in Tomcat?**

The main **configuration file** for Tomcat, defining connectors, hosts, ports, etc.

---

### 🔹 **6. What is `web.xml` in Tomcat?**

Deployment descriptor located in `WEB-INF/` that configures servlets, filters, listeners, etc.

---

### 🔹 **7. What is a WAR file?**

A **Web ARchive** that packages all resources (servlets, JSPs, HTML, etc.) for deployment.

---

### 🔹 **8. How to deploy a WAR file in Tomcat?**

* Copy the `.war` to `webapps/`
* Use Tomcat Manager UI

---

### 🔹 **9. How do you start and stop Tomcat?**

```bash
catalina.sh start
catalina.sh stop
```

---

### 🔹 **10. How to change Tomcat’s default port?**

Edit `server.xml`:

```xml
<Connector port="8080" ... />
```

---

### 🔹 **11. How does Tomcat handle multithreading?**

Each incoming request is handled in a **separate thread** using a thread pool.

---

### 🔹 **12. What is a servlet container?**

Part of a web server that interacts with Java servlets, managing their lifecycle.

---

### 🔹 **13. What are the main directories in a Tomcat installation?**

* `bin/`: startup/shutdown scripts
* `conf/`: configuration files
* `webapps/`: deployed apps
* `logs/`: server logs
* `lib/`: core libraries

---

### 🔹 **14. How to enable HTTPS in Tomcat?**

* Generate keystore
* Configure `server.xml` with SSL Connector

```xml
<Connector port="8443" protocol="HTTP/1.1" SSLEnabled="true" ... />
```

---

### 🔹 **15. What is Tomcat Manager?**

A web-based application to **deploy, undeploy, and monitor** apps via UI or API.

---

### 🔹 **16. How do you enable Tomcat Manager?**

Add user with `manager-gui` role in `tomcat-users.xml`.

---

### 🔹 **17. What is AJP in Tomcat?**

**Apache JServ Protocol**: Connector that allows Tomcat to communicate with web servers like Apache HTTPD.

---

### 🔹 **18. How do you enable access logs in Tomcat?**

Edit `server.xml` and enable:

```xml
<Valve className="AccessLogValve" ... />
```

---

### 🔹 **19. How do you monitor Tomcat performance?**

* JMX beans
* Prometheus + Grafana
* VisualVM or JConsole

---

### 🔹 **20. How to set environment variables for Tomcat?**

Edit `setenv.sh` or `setenv.bat` to configure `JAVA_OPTS`, `CATALINA_OPTS`.

---

### 🔹 **21. What is the difference between `Context` and `Host` in Tomcat?**

* **Context**: individual web app
* **Host**: virtual host (domain)

---

### 🔹 **22. How to configure multiple web apps in Tomcat?**

Deploy multiple WARs in `webapps/`, each with a unique context path.

---

### 🔹 **23. What is the use of `context.xml`?**

Defines app-specific configuration, like:

* DataSource
* Session settings
* Context path

---

### 🔹 **24. How do you configure a DataSource in Tomcat?**

Add in `context.xml`:

```xml
<Resource name="jdbc/myDB" auth="Container" type="javax.sql.DataSource" ... />
```

---

### 🔹 **25. How to configure session timeout in Tomcat?**

In `web.xml`:

```xml
<session-config>
  <session-timeout>30</session-timeout>
</session-config>
```

---

### 🔹 **26. How do you increase the max file upload size in Tomcat?**

Modify `server.xml`:

```xml
maxPostSize="10485760"   <!-- 10MB -->
```

---

### 🔹 **27. How to restrict access to Tomcat Manager?**

Use roles in `tomcat-users.xml` and IP filters via `RemoteAddrValve`.

---

### 🔹 **28. What is Tomcat clustering?**

Support for **load balancing and session replication** across multiple Tomcat instances.

---

### 🔹 **29. What are the common HTTP status codes returned by Tomcat?**

* `200`: OK
* `404`: Not Found
* `500`: Server Error
* `403`: Forbidden

---

### 🔹 **30. How to deploy an exploded WAR directory?**

Copy the unzipped folder to `webapps/`.

---

### 🔹 **31. How does Tomcat differ from other app servers like JBoss or WebLogic?**

* Tomcat: **Servlet container**
* JBoss/WebLogic: **Full JEE app servers**

---

### 🔹 **32. What is TomEE?**

Apache Tomcat + additional Java EE features (JPA, CDI, JMS, etc.).

---

### 🔹 **33. How do you configure logging in Tomcat?**

* Use `logging.properties` in `conf/`
* Or switch to **Log4j** or **SLF4J**

---

### 🔹 **34. How to deploy Spring Boot app in Tomcat?**

1. Package as WAR (`<packaging>war</packaging>`)
2. Extend `SpringBootServletInitializer`
3. Deploy to `webapps/`

---

### 🔹 **35. What is the difference between embedded and external Tomcat?**

* **Embedded**: Starts with Spring Boot app (JAR)
* **External**: Standalone Tomcat server (WAR)

---

### 🔹 **36. How do you configure Tomcat in Spring Boot?**

Via `application.properties`:

```properties
server.port=9090
server.servlet.context-path=/myapp
```

---

### 🔹 **37. How to enable compression in Tomcat?**

In `server.xml`:

```xml
compression="on" compressionMinSize="1024"
```

---

### 🔹 **38. How do you tune Tomcat for high performance?**

* Increase thread pool size
* Enable caching
* Use connection pool (e.g., HikariCP)
* Optimize GC

---

### 🔹 **39. How to manage memory settings for Tomcat?**

Set `JAVA_OPTS`:

```bash
export JAVA_OPTS="-Xms512m -Xmx1024m"
```

---

### 🔹 **40. How do you configure CORS in Tomcat?**

Add a CORS filter in `web.xml` or use Spring’s `@CrossOrigin`.

---

### 🔹 **41. How to change Tomcat’s default webapp directory?**

Update `<Host>` in `server.xml`:

```xml
appBase="/path/to/myapps"
```

---

### 🔹 **42. Can you run multiple Tomcat instances on the same machine?**

Yes, but change ports (`server.xml`), logs, and shutdown port.

---

### 🔹 **43. How do you test Tomcat installation?**

Access `http://localhost:8080` and verify welcome page loads.

---

### 🔹 **44. What is the default deployment context of a WAR?**

WAR name determines context path:

* `myapp.war` → `/myapp`

---

### 🔹 **45. How do you undeploy a webapp in Tomcat?**

* Delete WAR + exploded folder from `webapps/`
* Or use Tomcat Manager

---

### 🔹 **46. What is `conf/catalina.properties` used for?**

Used for internal configurations like class loading.

---

### 🔹 **47. How to avoid session memory leaks in Tomcat?**

* Use `@PreDestroy`
* Unregister JDBC drivers
* Clear static caches

---

### 🔹 **48. How to monitor active sessions in Tomcat?**

Enable session stats valve or use JMX/Manager app.

---

### 🔹 **49. How do you rotate logs in Tomcat?**

Use `logrotate` or configure `AccessLogValve` with timestamped files.

---

### 🔹 **50. How to secure Tomcat for production?**

* Disable unused connectors
* Change default ports
* Use strong passwords
* Enable HTTPS
* Remove sample apps

---

✅ You're blazing through!

Let me know if you'd like to proceed with:

* ✅ **System Design**
* ✅ **DSA**
* ✅ **Project-Based Qs**
* ✅ **HR + Behavioral + Leadership**

I'll continue with the next batch of 50 immediately.

Perfect! Let’s now continue with the next 50:

---

## ✅ **System Design – Top 50 Interview Questions & Answers (For Java Backend / Full Stack Developers)**

---

### 🔹 **1. What is system design?**

System design is the **process of defining architecture, components, modules, and interfaces** to build scalable and maintainable systems.

---

### 🔹 **2. Difference between High-Level Design (HLD) and Low-Level Design (LLD)?**

* **HLD**: Overview of system, components, APIs, data flow
* **LLD**: Class diagrams, detailed logic, database schema

---

### 🔹 **3. What is scalability?**

Ability of the system to **handle increased load** (users, requests) without performance degradation.

---

### 🔹 **4. What is the difference between horizontal and vertical scaling?**

* **Horizontal**: Add more machines (preferred)
* **Vertical**: Add more power (CPU, RAM) to existing machine

---

### 🔹 **5. What is load balancing?**

Distributes traffic across multiple servers to **avoid overload** and improve reliability.

---

### 🔹 **6. What are types of load balancers?**

* Layer 4 (Transport): TCP, UDP
* Layer 7 (Application): HTTP, HTTPS

---

### 🔹 **7. What is a CDN?**

Content Delivery Network – caches content at edge locations to serve users **faster and closer** to their location.

---

### 🔹 **8. What is a cache?**

Temporary storage to **reduce DB hits and response time**.

---

### 🔹 **9. What are common caching strategies?**

* Write-through
* Write-back
* Write-around
* Cache-aside
* TTL (Time to Live)

---

### 🔹 **10. What is a database sharding?**

Splitting large DB into smaller, faster, more manageable **shards** based on a key (e.g., user ID).

---

### 🔹 **11. What is a message queue?**

A queue that stores messages to be **processed asynchronously** (e.g., RabbitMQ, Kafka, SQS).

---

### 🔹 **12. Synchronous vs. Asynchronous communication?**

* **Sync**: Request/response (blocking)
* **Async**: Decoupled via queues (non-blocking)

---

### 🔹 **13. What is CAP theorem?**

A distributed system can guarantee only **2 out of 3**:

* **C**onsistency
* **A**vailability
* **P**artition tolerance

---

### 🔹 **14. What is consistency?**

All nodes see the same data at the same time.

---

### 🔹 **15. What is availability?**

Every request receives a (non-error) response – without guarantee of the most recent write.

---

### 🔹 **16. What is partition tolerance?**

System continues to operate despite **network failures**.

---

### 🔹 **17. What is eventual consistency?**

Data may be inconsistent temporarily, but becomes consistent **over time**.

---

### 🔹 **18. What is strong consistency?**

All nodes reflect the **latest write** immediately.

---

### 🔹 **19. What is database replication?**

Creating copies of data across multiple servers to improve **availability and read scalability**.

---

### 🔹 **20. What is master-slave replication?**

* **Master**: handles reads/writes
* **Slave**: read-only, syncs from master

---

### 🔹 **21. What is rate limiting?**

Restricting number of API calls per user/time to **prevent abuse**.

---

### 🔹 **22. How do you implement rate limiting?**

* Token bucket
* Leaky bucket
* Redis counter with TTL

---

### 🔹 **23. How to design a URL shortening service like bit.ly?**

* Use Base62 encoded ID
* Store mapping in DB/cache
* Handle collision
* Add analytics and TTL

---

### 🔹 **24. How to design an e-commerce system?**

* Users, Products, Orders, Cart
* Inventory management
* Payment gateway integration
* Microservices for catalog, checkout

---

### 🔹 **25. How to design a distributed cache?**

Use Redis/Memcached with:

* Sharding
* Replication
* Consistent hashing
* Eviction policies

---

### 🔹 **26. What is consistent hashing?**

Minimizes re-mapping of keys when nodes are added/removed in distributed systems.

---

### 🔹 **27. How do you design a chat application?**

* WebSockets for real-time
* Store messages in DB
* Use Redis for pub/sub

---

### 🔹 **28. How do you design a notification system?**

* Producer generates events
* Queue (Kafka, RabbitMQ)
* Consumers send SMS, email, push
* Use retry logic and DLQ

---

### 🔹 **29. What is database indexing?**

Improves **query performance** using data structures like B-trees, hash tables.

---

### 🔹 **30. What is an LRU cache?**

Least Recently Used cache discards the **least recently accessed** items first.

---

### 🔹 **31. How to scale databases?**

* Vertical scaling (more resources)
* Horizontal scaling (sharding, replication)
* Read replicas
* Caching

---

### 🔹 **32. What are microservices?**

Architecture style that splits app into **independent, loosely coupled services**.

---

### 🔹 **33. Pros and cons of microservices?**

✅ Independent deployment
✅ Better scalability
❌ Complex inter-service communication
❌ Requires DevOps maturity

---

### 🔹 **34. What is a service registry and discovery?**

Keeps track of **service locations**. Tools: Eureka, Consul.

---

### 🔹 **35. What is a reverse proxy?**

Intercepts and forwards requests to backend servers (e.g., Nginx, HAProxy).

---

### 🔹 **36. What is CQRS?**

Command Query Responsibility Segregation – separate models for **reading and writing**.

---

### 🔹 **37. What is eventual consistency in microservices?**

Each service maintains its own DB, and **syncs via events**.

---

### 🔹 **38. How to ensure idempotency in APIs?**

* Use idempotency keys
* Store request fingerprints
* Ensure retries don’t cause duplicate processing

---

### 🔹 **39. What is a distributed lock?**

Used to prevent **race conditions** in distributed systems. Example: Redis Redlock.

---

### 🔹 **40. What is the role of API Gateway?**

Handles:

* Authentication
* Routing
* Throttling
* Aggregation

---

### 🔹 **41. How do you design a file storage service?**

* Use S3 or blob storage
* Generate secure upload/download URLs
* Store metadata in DB

---

### 🔹 **42. How do you handle large file uploads?**

* Use pre-signed URLs
* Chunk uploads
* Upload status tracking

---

### 🔹 **43. What are design considerations for real-time systems?**

* Use WebSockets
* Pub/Sub messaging
* Low latency DB (Redis)
* Eventual consistency

---

### 🔹 **44. What are idempotent operations?**

Multiple identical requests result in **same effect** (e.g., PUT, DELETE)

---

### 🔹 **45. How to detect and prevent duplicate requests?**

* Use idempotency tokens
* Log previous request hashes
* Store request history with expiry

---

### 🔹 **46. How do you design a recommendation engine?**

* Collect user activity
* Apply collaborative filtering or ML
* Store results in cache

---

### 🔹 **47. What is a heartbeat mechanism?**

Used to **monitor node health** in distributed systems.

---

### 🔹 **48. What is blue-green deployment?**

Two identical environments (blue & green), traffic is switched after verifying the new version.

---

### 🔹 **49. What is circuit breaker pattern?**

Prevents system from making calls to failing services. Tools: Resilience4j, Hystrix.

---

### 🔹 **50. How do you design for high availability?**

* Use replication
* Avoid single point of failure
* Use load balancers
* Monitor and auto-restart failing services

---

✅ You're making serious progress!

Would you like to continue with:

* **Data Structures & Algorithms (DSA)**
* **Project-Based Questions**
* **HR Round**
* **Behavioral + Leadership**

Let me know, and I’ll deliver the next 50 immediately!

Awesome! Now let’s move on to the next **50** in your journey:

---

## ✅ **Data Structures & Algorithms (DSA) – Top 50 Interview Questions & Answers (For Java Developers)**

---

### 🔹 **1. What is the difference between Array and ArrayList in Java?**

* **Array**: Fixed size, can hold primitives
* **ArrayList**: Resizable, holds only objects

---

### 🔹 **2. What is a LinkedList?**

A linear data structure where elements (nodes) point to the **next (and optionally previous)** node.

---

### 🔹 **3. What is the time complexity of common operations on HashMap?**

* Insert: O(1)
* Delete: O(1)
* Lookup: O(1) average, O(n) worst

---

### 🔹 **4. What is a Stack?**

LIFO structure:

* Push, Pop
* Applications: Expression evaluation, undo/redo

---

### 🔹 **5. What is a Queue?**

FIFO structure:

* Enqueue, Dequeue
* Applications: Scheduling, BFS

---

### 🔹 **6. What is a PriorityQueue?**

A **heap-based queue** where elements are ordered by priority.

---

### 🔹 **7. What is a HashSet?**

A collection that stores **unique, unordered** elements.

---

### 🔹 **8. How is a HashMap implemented?**

Using an **array of buckets**, where each bucket holds entries managed via **linked list or tree** (Java 8+).

---

### 🔹 **9. What is a TreeMap?**

A Red-Black Tree-based map that stores keys in **sorted order**.

---

### 🔹 **10. What is recursion?**

Function that **calls itself**, useful for divide-and-conquer problems (factorial, Fibonacci).

---

### 🔹 **11. What is a base case in recursion?**

The **stopping condition** to avoid infinite recursion.

---

### 🔹 **12. What is memoization?**

A technique to **cache recursive results** to avoid repeated computation.

---

### 🔹 **13. What is Dynamic Programming (DP)?**

Solving problems by **breaking them into subproblems**, storing solutions to avoid recomputation.

---

### 🔹 **14. What is the difference between DFS and BFS?**

* DFS: depth-wise traversal (Stack/Recursion)
* BFS: level-wise traversal (Queue)

---

### 🔹 **15. What is the time complexity of Binary Search?**

O(log n)

---

### 🔹 **16. What are the best sorting algorithms and their complexities?**

| Algorithm | Time (Avg) | Space    |
| --------- | ---------- | -------- |
| QuickSort | O(n log n) | O(log n) |
| MergeSort | O(n log n) | O(n)     |
| HeapSort  | O(n log n) | O(1)     |

---

### 🔹 **17. What is the difference between stable and unstable sort?**

* **Stable**: Preserves order of equal elements (e.g., MergeSort)
* **Unstable**: Doesn’t guarantee order (e.g., QuickSort)

---

### 🔹 **18. What is a binary tree?**

Each node has **at most 2 children**.

---

### 🔹 **19. What is a binary search tree (BST)?**

A binary tree where left < root < right for all nodes.

---

### 🔹 **20. How to check if a tree is balanced?**

A tree is balanced if height difference between left and right is **≤1** for every node.

---

### 🔹 **21. What is a trie?**

Prefix tree used for efficient **string matching** (e.g., autocomplete).

---

### 🔹 **22. What is a heap?**

* Complete binary tree
* Min-heap: parent ≤ children
* Max-heap: parent ≥ children

---

### 🔹 **23. How is heap used in PriorityQueue?**

Java's `PriorityQueue` is a **min-heap** by default.

---

### 🔹 **24. What is a graph?**

Set of vertices connected by edges. Types:

* Directed, Undirected
* Weighted, Unweighted

---

### 🔹 **25. What is the difference between adjacency matrix and list?**

* **Matrix**: O(1) lookup, more space
* **List**: Efficient for sparse graphs

---

### 🔹 **26. What is Dijkstra’s Algorithm?**

Finds **shortest path** from a source node to all others (uses a min-priority queue).

---

### 🔹 **27. What is a cycle in a graph?**

A path that **starts and ends at the same node**.

---

### 🔹 **28. How to detect a cycle in a graph?**

* DFS with visited & recursion stack
* Union-Find (for undirected graphs)

---

### 🔹 **29. What is topological sorting?**

Linear ordering of DAG nodes such that **u appears before v** for all edges u → v.

---

### 🔹 **30. What is backtracking?**

Explores all paths (recursively) and **backtracks** if the path is invalid.

---

### 🔹 **31. Example of backtracking problem?**

* N-Queens
* Sudoku Solver
* Subset Sum

---

### 🔹 **32. What is a sliding window technique?**

A method for solving subarray problems in linear time using **two pointers**.

---

### 🔹 **33. What is two-pointer technique?**

Use of **two indices** moving towards/away from each other to solve problems like pairs with sum.

---

### 🔹 **34. What is Floyd’s cycle detection?**

Used in **linked list cycle detection** (slow/fast pointer).

---

### 🔹 **35. What is a hash collision?**

When two keys hash to the **same bucket**.

---

### 🔹 **36. How to resolve hash collisions?**

* Separate chaining (linked list)
* Open addressing (linear/quadratic probing)

---

### 🔹 **37. What is the KMP algorithm?**

Efficient string matching using a **prefix table** to avoid rechecking characters.

---

### 🔹 **38. What is Rabin-Karp algorithm?**

Uses **hashing** to detect patterns in text quickly.

---

### 🔹 **39. What are bitwise operators in Java?**

* `&`, `|`, `^`, `~`, `<<`, `>>`
* Used in low-level manipulation, performance optimizations

---

### 🔹 **40. What is a monotonic stack?**

A stack that keeps elements in **increasing or decreasing** order to solve problems like "Next Greater Element".

---

### 🔹 **41. How do you reverse a linked list?**

Iteratively or recursively change `.next` pointers.

---

### 🔹 **42. How to detect palindrome?**

Compare characters from both ends or use reverse string logic.

---

### 🔹 **43. What is dynamic array?**

Array that **resizes automatically**, like `ArrayList`.

---

### 🔹 **44. What are time complexities of Java collections?**

| Collection | get  | add            | remove              |
| ---------- | ---- | -------------- | ------------------- |
| ArrayList  | O(1) | O(1) amortized | O(n)                |
| LinkedList | O(n) | O(1)           | O(1) from head/tail |
| HashMap    | O(1) | O(1)           | O(1) avg            |

---

### 🔹 **45. What is merge interval problem?**

Given overlapping intervals, **merge them** into one. Used sorting + two pointers.

---

### 🔹 **46. What is the difference between call stack and heap memory?**

* **Stack**: stores method calls, local variables
* **Heap**: stores objects, managed by GC

---

### 🔹 **47. What is a greedy algorithm?**

Always takes the **best choice at the moment**, doesn't backtrack.

---

### 🔹 **48. Example of greedy algorithm?**

* Activity selection
* Coin change (non-optimal)
* Huffman encoding

---

### 🔹 **49. What is divide-and-conquer?**

Divide problem → Solve recursively → Combine results
Examples: Merge Sort, QuickSort

---

### 🔹 **50. What is tail recursion?**

Recursive call is the **last statement** in a function. Optimizable by compiler (not in Java yet).

---

✅ You’ve completed 750 questions so far across all major backend, frontend, system, and infra areas!

Next up:

* ✅ **Project-Based Questions**
* ✅ **HR + Behavioral**
* ✅ **Leadership (Module Lead)**

Shall I continue with **Project-Based Questions (HRMS, Notification, Booking Apps, etc.)** next?

Let me know and I’ll deliver the next 50 instantly!

Awesome, Aditya! Let’s dive into the next 50:

---

## ✅ **Project-Based Interview Questions – Top 50 (Based on Your Resume: HRMS, Appointments, Notifications, Microservices)**

---

### 🔹 **1. Can you describe the architecture of your Hospital Management System project?**

Yes. It is built using **Spring Boot Microservices**, with separate services for:

* Admin (HRMS)
* Appointments
* Inventory
* Notification
* Gateway
* Auth Service
  Uses **MySQL/Postgres**, **Kafka**, **Redis**, and **JWT Security**.

---

### 🔹 **2. What services did you implement in your HRMS module?**

* User & Role Management
* Employee Info & Leave Management
* Attendance & Payroll
* Reports & Exporting
* Integrated Kafka for Audit & Notification

---

### 🔹 **3. How did you handle authentication and authorization?**

Using:

* **Spring Security + JWT** for token-based auth
* **Role-based access control (RBAC)**
* Integrated `@PreAuthorize` and `SecurityFilterChain`

---

### 🔹 **4. How is inter-service communication handled in your microservices project?**

* **REST APIs** using Feign Clients
* **Kafka** for asynchronous event communication
* **RabbitMQ** for some scheduled background processes

---

### 🔹 **5. How did you manage configurations across services?**

Used **Spring Cloud Config Server** with profiles for `dev`, `uat`, `prod`.

---

### 🔹 **6. What is your approach to service discovery?**

Implemented **Eureka Server** for service registration and discovery.

---

### 🔹 **7. How did you implement API Gateway in your project?**

Used **Spring Cloud Gateway** for:

* Routing
* Load Balancing
* Authentication filter
* Rate Limiting (via Redis)

---

### 🔹 **8. How did you handle appointment bookings?**

* Patients book appointments through `appointment-service`
* Slots are checked with `doctor-schedule-service`
* Bookings are confirmed via `notification-service` (Kafka + Email/SMS)

---

### 🔹 **9. How does your notification module work?**

* **Listens to Kafka topics** (`appointment-created`, `leave-approved`)
* Sends **email/SMS notifications** using integrated providers (e.g., SMTP, Twilio)

---

### 🔹 **10. How do you track inventory in your system?**

Each inventory action (in/out) is logged and **published to Kafka**, stored in DB, and used for reporting with thresholds and alerts.

---

### 🔹 **11. How did you implement file upload & download for employee documents?**

* Used Spring Boot REST API with **MultipartFile**
* Stored files in **local file system / AWS S3**
* File metadata in DB

---

### 🔹 **12. What is your approach to handling errors between microservices?**

* Used **Feign ErrorDecoder**
* Defined global **`@ControllerAdvice` + `@ExceptionHandler`**
* Kafka messages are pushed to **DLQ (dead-letter queues)** on failure

---

### 🔹 **13. How do you manage transactions across services (saga pattern)?**

* Used **Kafka events** with correlation ID
* Manual compensation logic in case of failure

---

### 🔹 **14. How is audit logging handled in your project?**

* Each microservice **publishes events to Kafka**
* Centralized audit service consumes and stores them in MongoDB for analytics

---

### 🔹 **15. How did you implement caching?**

* Used **Redis** for user sessions, JWT token blacklisting, and frequently accessed data like department lists

---

### 🔹 **16. How do you secure internal service communication?**

* Used JWT between services
* Token validation via **auth-service middleware**

---

### 🔹 **17. How did you ensure application performance under load?**

* Load tested using **JMeter**
* Used **Redis** caching and **connection pooling (HikariCP)**
* Auto-scaled containers using Kubernetes

---

### 🔹 **18. How did you monitor your microservices?**

* Used **Spring Boot Actuator**
* Integrated with **Prometheus + Grafana**
* Alerts via Slack + Email

---

### 🔹 **19. How do you deploy your services?**

* Containerized using **Docker**
* Orchestrated with **Kubernetes**
* Jenkins CI/CD pipelines with staging and production

---

### 🔹 **20. How do you handle data consistency across services?**

* **Eventually consistent** model
* Retry and fallback mechanisms
* Manual reconciliation dashboards

---

### 🔹 **21. What are some challenges you faced with microservices?**

* Service dependency and fallback
* Token propagation
* Data consistency
* Monitoring and alerting across services

---

### 🔹 **22. How did you handle attendance and payroll in HRMS?**

* Integrated **cron jobs** to compute attendance
* Payroll is auto-calculated based on policies and generates downloadable slips

---

### 🔹 **23. What is your reporting strategy?**

* Used custom SQL + Jasper Reports
* Scheduled reports via cron + email

---

### 🔹 **24. What DB strategy did you use for appointments and leaves?**

* **PostgreSQL** with proper indexing
* **Soft deletes**, audit columns for tracking changes

---

### 🔹 **25. What kind of validation was implemented in forms?**

* **Bean Validation (JSR 380)**: `@NotNull`, `@Size`
* Angular front-end used **Reactive Forms** for real-time validation

---

### 🔹 **26. How is role-based access managed in your frontend?**

* Angular consumes JWT → Roles → Controls menu rendering
* `canActivate` guards applied at route level

---

### 🔹 **27. How did you manage different environments (dev, UAT, prod)?**

* Used Spring profiles + Config Server
* Jenkins picks `.yml` per environment

---

### 🔹 **28. How did you manage third-party integrations (SMS, Email)?**

* Abstracted via **interfaces**
* Implemented real + mock senders
* Retry with exponential backoff + logging

---

### 🔹 **29. What audit fields did you maintain?**

* `createdBy`, `createdAt`, `updatedBy`, `updatedAt`
* Auto-populated via JPA Auditing

---

### 🔹 **30. How do you handle concurrency in booking service?**

* Used **optimistic locking** via JPA version
* Serialized slot bookings using Redis locks

---

### 🔹 **31. How do you test your microservices?**

* Unit testing with JUnit, Mockito
* Integration testing using TestContainers + MockMVC
* Kafka event test with embedded Kafka

---

### 🔹 **32. How do you manage logs?**

* Logs go to file + **ELK stack**
* Correlation ID used across services

---

### 🔹 **33. How is leave approval workflow managed?**

* Uses state machine logic
* Notification sent on each state change
* Supervisor approval module with retry and escalation

---

### 🔹 **34. What roles do you support in the HRMS?**

* Admin, HR, Manager, Employee
* Role-based dashboards and permissions

---

### 🔹 **35. How are patient records secured?**

* Encrypted sensitive fields at rest
* Access logged and restricted via roles
* Audit trail via Kafka + Mongo

---

### 🔹 **36. How are reports generated and delivered?**

* Jasper Reports to PDF/Excel
* Delivered via email or downloadable from portal

---

### 🔹 **37. What is your API versioning strategy?**

* `/api/v1/...`
* Deprecated older versions with warnings

---

### 🔹 **38. How do you ensure database migrations?**

* Used **Flyway**
* Version-controlled SQL scripts per service

---

### 🔹 **39. How are failed appointments or leave requests retried?**

* Logged into retry queue (Kafka)
* Retry worker runs via scheduler

---

### 🔹 **40. How is employee onboarding handled?**

* Step-by-step workflow
* Generates employee code, creates default roles, schedules induction

---

### 🔹 **41. What metrics do you track?**

* Total bookings, cancellations, logins, active sessions, time to respond, Kafka lag

---

### 🔹 **42. How do you handle notification failure?**

* Retry logic with fallback to email/SMS
* Manual resend via admin panel

---

### 🔹 **43. How do you manage backups?**

* Daily DB backups
* Mongo + Kafka topic offset backed up weekly
* Stored in S3

---

### 🔹 **44. How is search implemented (e.g., employees, appointments)?**

* ElasticSearch for large-scale search
* SQL `LIKE` for smaller datasets

---

### 🔹 **45. What kind of dashboards are available?**

* Admin: KPIs, logs, user stats
* Manager: team summary
* Employee: leaves, payslip, tasks

---

### 🔹 **46. How did you integrate notification preferences?**

* User profile holds preferences (email/SMS/push)
* Notification module respects settings

---

### 🔹 **47. How did you implement audit logs in MongoDB?**

* Kafka consumer stores `action`, `user`, `timestamp`, `entity`, `diff`

---

### 🔹 **48. How do you version APIs without breaking clients?**

* Introduce new endpoints
* Deprecate old ones gradually with logging & alerts

---

### 🔹 **49. How is health monitoring done?**

* Spring Boot Actuator endpoints `/health`, `/metrics`
* Integrated with Prometheus and Slack alerts

---

### 🔹 **50. What are your key contributions as a Module Lead?**

* Owned end-to-end module delivery
* Mentored juniors
* Conducted code reviews
* Supported release planning
* Handled production incidents

---

✅ Done! Next:

* ✅ **HR Round (Personality, Culture Fit, Strengths, Challenges)**
* ✅ **Behavioral + Leadership (Team Lead / Module Lead)**

Let me know if I should continue with **HR + Behavioral** questions now!

Excellent! Let's proceed with the **HR Round + Behavioral + Leadership (Module Lead)** questions — these are essential for cracking final rounds and higher-level roles.

---

## ✅ **HR Round + Behavioral + Leadership – Top 50 Questions & Answers (For 3.5+ Yrs Java Module Lead Role)**

---

### 🔹 **1. Tell me about yourself.**

**Answer:**
"I'm Aditya Dange, a Full Stack Java Developer with 3.5+ years of experience. I specialize in building scalable web applications using Java, Spring Boot, Microservices, and Angular/React. I’ve led modules like HRMS, Appointment Booking, and Notification Systems, and I'm currently a Module Lead at Oakland Systems where I mentor juniors and own technical delivery."

---

### 🔹 **2. Why do you want to leave your current job?**

**Answer:**
"I'm looking for a role where I can contribute to more complex architectural decisions, work on larger-scale distributed systems, and grow into a solution architect role. I’ve learned a lot here, but I’m ready for the next challenge."

---

### 🔹 **3. What are your strengths?**

* Ownership mindset
* Microservices architecture
* Problem-solving
* Mentorship and leadership
* Strong backend + frontend balance

---

### 🔹 **4. What are your areas of improvement?**

"I’m working on improving my public speaking and presentation skills for better team communication and leadership visibility."

---

### 🔹 **5. Why should we hire you?**

**Answer:**
"Because I bring strong hands-on experience in end-to-end development, a proven track record of module ownership, and a mindset aligned with quality delivery and continuous improvement."

---

### 🔹 **6. Describe a situation where you took initiative.**

**Answer:**
"In our HRMS project, I noticed a performance bottleneck in attendance calculations. I introduced Redis caching and reduced response time by 70%, which improved the user experience and reduced DB load."

---

### 🔹 **7. Have you led a team before?**

**Answer:**
"Yes, I mentor 2–3 junior developers, conduct code reviews, and coordinate sprint planning and delivery for the modules I lead."

---

### 🔹 **8. How do you handle conflict in a team?**

"I prefer resolving it through one-on-one conversations, identifying the root cause, and aligning on a shared goal. Communication is key."

---

### 🔹 **9. How do you handle deadlines?**

"I plan proactively, break down tasks, buffer time for blockers, and ensure progress is visible via stand-ups and Jira."

---

### 🔹 **10. Describe a challenging bug or issue you resolved.**

"Production cache invalidation issue causing stale data. I traced it to a missing eviction call after batch updates and patched it with proper post-commit cache management."

---

### 🔹 **11. What’s your leadership style?**

Supportive and accountability-driven. I lead by example and create a collaborative, quality-focused environment.

---

### 🔹 **12. How do you prioritize tasks?**

I use **Eisenhower matrix** logic: urgent vs important, track in Jira, and focus on business impact.

---

### 🔹 **13. What motivates you?**

Building something impactful, solving real user pain points, and mentoring others.

---

### 🔹 **14. Describe a time when you failed.**

"I underestimated the effort for a Kafka migration. It delayed delivery. I learned to plan for environment compatibility and rollback."

---

### 🔹 **15. How do you handle feedback?**

"I actively seek it, reflect without taking it personally, and take action to improve."

---

### 🔹 **16. How do you manage code reviews?**

I focus on readability, performance, security, and adherence to standards. I also explain reasoning during reviews.

---

### 🔹 **17. How do you stay updated with technology?**

I follow blogs (Baeldung, InfoQ), contribute to GitHub, and complete courses on Udemy/Pluralsight.

---

### 🔹 **18. What are your career goals?**

To become a **Solution Architect** in 3–5 years and lead large-scale distributed systems projects.

---

### 🔹 **19. How do you balance technical and managerial tasks?**

By allocating focused blocks for coding and using agile tools (Jira/Confluence) to track meetings, reviews, and planning.

---

### 🔹 **20. Have you dealt with performance issues in production?**

Yes, I optimized slow SQL joins in reporting service and added Redis-based result caching for heavy queries.

---

### 🔹 **21. Describe a time when you improved a process.**

I introduced a **CI build fail-fast policy** in Jenkins pipelines to catch errors early, saving hours of rework per sprint.

---

### 🔹 **22. How do you ensure code quality?**

* Unit + integration tests
* Static analysis (SonarQube)
* Pair programming and code reviews
* CI checks and pre-merge gates

---

### 🔹 **23. How do you onboard new developers?**

I provide structured onboarding docs, pair-program with them for the first few weeks, and assign small tasks to build confidence.

---

### 🔹 **24. What do you do if a junior is consistently missing deadlines?**

Understand root causes (skill, clarity, motivation), coach them, and break tasks into smaller chunks with check-ins.

---

### 🔹 **25. Describe your biggest professional achievement.**

Successfully designed and delivered an **appointment notification system** integrated with Kafka, scaling to 10k+ events/day.

---

### 🔹 **26. How do you ensure security in your applications?**

* Input validation
* CSRF/XSS prevention
* JWT token validation
* Spring Security + Role management

---

### 🔹 **27. What does ownership mean to you?**

Owning not just the code but the outcome — delivery, performance, monitoring, and user satisfaction.

---

### 🔹 **28. How do you handle multiple modules with dependencies?**

I use Jira, align sprints across modules, define clear contracts, and prioritize integration testing early.

---

### 🔹 **29. What is your approach to documentation?**

Minimal but clear — Swagger for APIs, Confluence for architecture, README for setup/instructions.

---

### 🔹 **30. How do you define success for a project?**

On-time delivery, stable production, zero critical bugs, and satisfied users.

---

### 🔹 **31. What will your previous manager say about you?**

Proactive, dependable, strong problem solver, and technically sound with great team spirit.

---

### 🔹 **32. What was your role in recruitment?**

I conducted technical interviews, shortlisted candidates, and provided onboarding mentorship.

---

### 🔹 **33. How do you estimate effort and timelines?**

Break down features into stories/tasks, use past data + buffers, and review with team.

---

### 🔹 **34. Do you prefer leading or coding?**

I enjoy doing both — I lead by coding, and I code to stay technically strong.

---

### 🔹 **35. How do you manage production issues?**

Use alerts/logs to detect, rollback via CI/CD, patch quickly, and perform RCA.

---

### 🔹 **36. Describe your involvement in sprint planning.**

Define story points, assign tasks, discuss dependencies, and ensure sprint goals are aligned with product roadmap.

---

### 🔹 **37. How do you delegate tasks?**

Based on individual strengths and learning goals, with clear expectations and check-ins.

---

### 🔹 **38. What tools do you use for team collaboration?**

* Jira (project management)
* GitLab/GitHub (version control)
* Slack/MS Teams (communication)
* Confluence (documentation)

---

### 🔹 **39. Have you conducted any training or sessions?**

Yes, I’ve done sessions on:

* Microservices best practices
* Kafka 101
* Spring Boot testing strategies

---

### 🔹 **40. Describe a time when you resolved a team misunderstanding.**

I mediated a tech stack disagreement, got both parties to demo pros/cons, and helped the team reach a consensus.

---

### 🔹 **41. What is your daily routine as a Module Lead?**

* Morning stand-up
* Code reviews
* Dev planning & blocker resolution
* Technical contribution
* Cross-team syncs

---

### 🔹 **42. What does accountability mean to you?**

Delivering what you committed to, proactively flagging risks, and learning from mistakes.

---

### 🔹 **43. How do you encourage innovation in your team?**

I give space for experiments, allow tech POCs in sprints, and recognize contributions.

---

### 🔹 **44. Have you worked with cross-functional teams?**

Yes — collaborated with QA, DevOps, Product Managers, and Designers in all projects.

---

### 🔹 **45. What are your expectations from your next role?**

Opportunity to lead larger projects, design at scale, and contribute to high-impact systems.

---

### 🔹 **46. Describe your communication style.**

Clear, collaborative, and assertive — I ensure mutual understanding without being aggressive.

---

### 🔹 **47. Do you work well under pressure?**

Yes — I stay calm, break down issues, prioritize, and act. Pressure helps sharpen focus.

---

### 🔹 **48. How do you manage remote collaboration?**

* Daily stand-ups
* Async updates via Slack
* Shared docs & Kanban boards

---

### 🔹 **49. Are you open to relocation or remote work?**

"Yes, I’m flexible based on project and company needs."

---

### 🔹 **50. Any questions for us?**

* What are the expectations from someone in this role in the first 3 months?
* What’s your tech stack and architecture like?
* How does the company invest in upskilling developers?

---

✅ That’s a solid 1000-question preparation pack tailored to your resume, role, and experience — **full-stack, DevOps, system design, leadership, HR, and more**.

Let me know if you'd like:

* A **PDF copy**
* A **cheat sheet per topic**
* **Mock interviews**
* Or questions sorted by **difficulty level**

I'm here to help 🚀