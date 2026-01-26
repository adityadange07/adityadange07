# Spring Boot Interview Questions & Answers

## 1. What is Spring Boot and what are its advantages?
**Detailed Explanation**: Spring Boot is an extension of the Spring Framework that eliminates boiler-plate configuration used for setting up a Spring application.
*   **Goal**: To make it easy to create stand-alone, production-grade Spring based Applications that you can "just run".
*   **Advantages**:
    1.  **Auto Configuration**: Automatically configures your application based on the dependencies present on the classpath.
    2.  **Starter Dependencies**: Simplified dependency management (e.g., `spring-boot-starter-web` brings in Spring MVC, Jackson, Tomcat).
    3.  **Embedded Server**: Comes with embedded Tomcat, Jetty, or Undertow. No need to deploy WAR files.
    4.  **Production Ready**: Attributes like metrics, health checks, and externalized configuration.

**Example**:
Instead of adding 10 dependencies for a Web App, you add just one:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

---

## 2. Explain the difference between Spring and Spring Boot.
**Detailed Explanation**:
*   **Spring Framework**: The core framework providing Dependency Injection, AOP, Transaction Management, etc. It requires significant manual configuration (XML or Java-based) to set up.
*   **Spring Boot**: A tool/framework built *on top* of Spring. It focuses on convention over configuration. It handles the low-level setup so developers can focus on business logic.
*   **Analogy**:
    *   **Spring**: Buying raw ingredients (flour, sugar, eggs) to bake a cake. Flexible but requires effort.
    *   **Spring Boot**: Buying a pre-mixed cake mix. You just add water and bake. Faster.

---

## 3. How does Spring Boot Auto-Configuration work?
**Detailed Explanation**:
*   **Mechanism**: It scans the classpath for jar files and configuration beans. Based on what it finds, it automatically creates the necessary beans.
*   **Annotation**: `@EnableAutoConfiguration` (usually wrapped inside `@SpringBootApplication`).
*   **Under the hood**: It looks at `META-INF/spring.factories` (or `imports` in newer versions) to load auto-configuration classes.
*   **Conditionals**: It uses annotations like `@ConditionalOnClass` or `@ConditionalOnMissingBean`.
    *   *Example*: If `H2.jar` is on classpath AND no `DataSource` bean is manually defined -> Configure an H2 in-memory database.

**Example**:
```java
// Spring Boot sees 'spring-boot-starter-web'
// It finds 'Tomcat.class' and 'SpringMVC.class'
// So it automatically configures a TomcatWebServer and DispatcherServlet.
```

---

## 4. What is the @SpringBootApplication annotation?
**Detailed Explanation**: It is a convenience annotation that combines three other important annotations:
1.  **`@Configuration`**: Marks the class as a source of bean definitions.
2.  **`@EnableAutoConfiguration`**: Tells Spring Boot to start adding beans based on classpath settings.
3.  **`@ComponentScan`**: Tells Spring to look for other components, configurations, and services in the current package and sub-packages.

**Example**:
```java
@SpringBootApplication 
// Equivalent to:
// @Configuration
// @EnableAutoConfiguration
// @ComponentScan
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args);
    }
}
```

---

## 5. How does a Spring Boot application start? (Internal flow)
**Detailed Explanation**: When you call `SpringApplication.run(MyApp.class, args)`:
1.  **Create Context**: Creates the appropriate `ApplicationContext` (e.g., `AnnotationConfigServletWebServerApplicationContext` for web apps).
2.  **Register Beans**: It scans for components and registers beans.
3.  **Trigger Auto-Config**: Processes `@EnableAutoConfiguration` to load internal starters.
4.  **Start Embedded Server**: If it's a web app, it starts Tomcat/Jetty on port 8080 (default).
5.  **Run Runners**: Executes any `CommandLineRunner` or `ApplicationRunner` beans.

---

## 6. Spring Boot Annotations
**Detailed Explanation**:
*   **`@Component`**: Generic stereotype for any Spring-managed component.
*   **`@Service`**: Specialization of Component for the Service Layer (Business Logic).
*   **`@Repository`**: Specialization for generic DAO (Data Access Object). Enables exception translation for DB errors.
*   **`@Controller`**: Standard Spring MVC controller. Returns logical view names (JSP/HTML).
*   **`@RestController`**: Combines `@Controller` + `@ResponseBody`. Returns data (JSON/XML) directly.
*   **`@Configuration`**: Indicates a class declares one or more `@Bean` methods.
*   **`@Bean`**: Marks a method to return an object to be managed by Spring Context.

**Example**:
```java
@Service // Business Logic
public class UserService { ... }

@Configuration
public class AppConfig {
    @Bean // Custom Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}
```

---

## 7. Dependency Injection (DI) and Inversion of Control (IoC)
**Detailed Explanation**:
*   **IoC (Inversion of Control)**: A design principle where the control of object creation and lifecycle is transferred from the developer to a container (Spring). Instead of `new User()`, Spring gives you the User.
*   **DI (Dependency Injection)**: The *pattern* used to implement IoC. The container "injects" the required dependencies into a class (via Constructor or Setter).

**Example**:
```java
// Traditional (Tight Coupling)
class Car {
    Engine e = new V8Engine(); // Car controls Engine creation
}

// IoC/DI (Loose Coupling)
@Component
class Car {
    private Engine engine;
    
    // Spring injects the engine
    public Car(Engine engine) {
        this.engine = engine;
    }
}
```

---

## 8. Types of Dependency Injection (Constructor vs Setter vs Field)
**Detailed Explanation**:
1.  **Constructor Injection** (Recommended): Dependencies are provided through the class constructor.
    *   *Pros*: Ensures immutability, prevents nulls, easy to test.
2.  **Setter Injection**: Dependencies are provided via public setter methods.
    *   *Pros*: Optional dependencies.
3.  **Field Injection** (`@Autowired` on field):
    *   *Cons*: Hard to test (can't inject mock without reflection), hides dependencies. Avoid if possible.

**Example**:
```java
@Service
public class UserService {
    private final UserRepository repo;

    // Constructor Injection (Best Practice)
    @Autowired // Optional in newer Spring versions if only 1 constructor
    public UserService(UserRepository repo) {
        this.repo = repo;
    }
}
```

---

## 9. Difference between @Controller and @RestController
**Detailed Explanation**:
*   **`@Controller`**:
    *   Used for traditional web applications (MVC).
    *   Methods return a `String` which represents a View name (e.g., "index.html").
    *   Need `@ResponseBody` on every method if you want to return JSON.
*   **`@RestController`**:
    *   Convenience annotation for `@Controller` + `@ResponseBody`.
    *   Used for RESTful Web Services.
    *   Methods return **Data** (Objects) which are automatically serialized to JSON/XML.

**Example**:
```java
@Controller
public class WebController {
    @GetMapping("/hello")
    public String page() { return "hello"; } // Returns hello.html
}

@RestController
public class ApiController {
    @GetMapping("/api/hello")
    public String data() { return "Hello World"; } // Returns string "Hello World"
}
```

---

## 10. Difference between @BeanFactory and @ApplicationContext
**Detailed Explanation**:
*   **BeanFactory**: The most basic container.
    *   Lazy loading (instantiates beans only when requested with `getBean()`).
    *   Used in resource-constrained systems.
*   **ApplicationContext**: Extends BeanFactory.
    *   Eager loading (instantiates Singletons on startup).
    *   Adds enterprise features: Event publishing, i18n messages, AOP support.
    *   **This is what we use 99% of the time.**

---

## 11. Bean Scopes in Spring
**Detailed Explanation**: Defines the lifecycle and visibility of that bean.
1.  **Singleton** (Default): Only **one instance** per Spring Container. Cached and reused.
2.  **Prototype**: A **new instance** is created *every time* it is requested.
3.  **Request** (Web): One instance per HTTP Request.
4.  **Session** (Web): One instance per HTTP Session.
5.  **GlobalSession** (Portlet): Global session.

**Example**:
```java
@Component
@Scope("prototype")
public class MyBean { ... }
```

---

## 12. Bean Lifecycle in Spring
**Detailed Explanation**: The journey of a bean managed by Spring container.
1.  **Instantiate**: `new Object()`.
2.  **Populate Properties**: DI (Inject dependencies).
3.  **Set Name/Factory**: `setBeanName`, `setBeanFactory`.
4.  **Pre-Initialization**: `BeanPostProcessor.postProcessBeforeInitialization`.
5.  **Initialize**:
    *   `@PostConstruct` methods.
    *   `InitializingBean.afterPropertiesSet()`.
    *   Custom `init-method`.
6.  **Post-Initialization**: `BeanPostProcessor.postProcessAfterInitialization`.
7.  **Ready to Use**.
8.  **Destroy**:
    *   `@PreDestroy`.
    *   `DisposableBean.destroy()`.

---

## 13. What is the default bean scope? Why is it Singleton?
**Detailed Explanation**:
*   **Default**: Singleton.
*   **Why**: Performance. Creating a new object for every request is expensive (memory + CPU). Most services (Service, DAO, Controller) are stateless, so sharing one instance is safe and efficient.

---

## 14. Difference between @Qualifier and @Primary
**Detailed Explanation**: Both solve the ambiguity problem when multiple beans of the same type exist.
*   **`@Primary`**: Defines a **default** preference. If multiple beans exist, inject *this* one unless specified otherwise.
*   **`@Qualifier`**: Specific selection. Used at the injection point to tell Spring *exactly* which bean name to use.
*   `@Qualifier` overrides `@Primary`.

**Example**:
```java
@Component @Primary
class Dog implements Animal {}

@Component("catBean")
class Cat implements Animal {}

// Injection
public Service(@Qualifier("catBean") Animal a) { ... } // Injects Cat
public Service(Animal a) { ... } // Injects Dog (Primary)
```

---

## 15. How to exclude a specific dependency or auto-configuration?
**Detailed Explanation**:
1.  **Exclude Auto-Configuration**: Use `exclude` attribute in the main annotation.
    *   `@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})`
2.  **Exclude Dependency**: In `pom.xml` (Maven).
    *   Use `<exclusions>` tag inside a dependency to block a transitive dependency.

**Example**:
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

---

## 16. How to handle exceptions in Spring Boot? (@ControllerAdvice)
**Detailed Explanation**:
*   **Global Exception Handling**: Instead of try-catch in every controller, use **`@ControllerAdvice`**.
*   **`@ExceptionHandler`**: Define methods that handle specific exceptions (e.g., `UserNotFoundException`) and return a custom error response (JSON) with proper HTTP status codes.

**Example**:
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFound(UserNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }
}
```

---

## 17. What is Spring Boot Actuator?
**Detailed Explanation**: A production-ready feature that helps you monitor and manage your application.
*   **Usage**: Adds REST endpoints to your app.
*   **Common Endpoints**:
    *   `/actuator/health`: Application status (UP/DOWN).
    *   `/actuator/info`: Version info.
    *   `/actuator/metrics`: CPU, Memory, Request counts.
    *   `/actuator/loggers`: View/Modify log levels at runtime.

**Example**:
Enable in `application.properties`:
`management.endpoints.web.exposure.include=*`

---

## 18. Spring Profiles (Dev, QA, Prod setup)
**Detailed Explanation**: Allows you to segregation parts of your application configuration and make it available only in certain environments.
*   **Mechanism**: Load different properties files based on the active profile.
*   **Files**: `application-dev.properties`, `application-prod.properties`.
*   **Activation**: `spring.profiles.active=dev` (in properties or command line argument `-Dspring.profiles.active=dev`).

**Example**:
*   Dev: `db.url=localhost`
*   Prod: `db.url=192.168.1.50`

---

## 19. How to read values from application.properties?
**Detailed Explanation**:
1.  **`@Value`**: Inject single property values.
    *   `@Value("${app.name}") private String appName;`
2.  **`@ConfigurationProperties`**: Bind a group of properties to a Java POJO. Type-safe.
    *   Prefix `app.mail.host`, `app.mail.port` -> Mapped to `MailConfig` class fields.

**Example**:
```java
@Component
public class MyService {
    @Value("${server.port}")
    private int port;
}
```

---

## 20. Difference between application.properties and application.yml
**Detailed Explanation**:
*   **Properties**: Key-Value structure. Standard Java format.
    *   `server.port=8080`
*   **YAML (YAML Ain't Markup Language)**: Hierarchical structure. More readable for complex configs.
    *   `server: port: 8080` (Indentation matters).
*   **Priority**: If both exist, `properties` file usually takes precedence over `yml` (though using both suggests bad practice).

---

## 21. REST API Best Practices
**Detailed Explanation**:
1.  **Nouns for Resources**: Use `/users`, not `/getUsers`.
2.  **HTTP Methods**: Use GET (read), POST (create), PUT (update full), PATCH (update partial), DELETE (remove).
3.  **Status Codes**: Return standard codes.
    *   200 OK, 201 Created, 204 No Content.
    *   400 Bad Request, 401 Unauthorized, 404 Not Found.
    *   500 Server Error.
4.  **Versioning**: `/api/v1/users`.
5.  **Plural**: `/users/1` instead of `/user/1`.

---

## 22. HTTP Methods (GET, POST, PUT, PATCH, DELETE)
**Detailed Explanation**:
*   **GET**: Retrieve resource. Safe & Idempotent.
*   **POST**: Create new resource. Not Safe, Not Idempotent.
*   **PUT**: Replace resource completely. If field missing, sets to null. Idempotent.
*   **PATCH**: Update resource partially. Only updates sent fields. Not strictly Idempotent (but usually treated as such).
*   **DELETE**: Remove resource. Idempotent.

---

## 23. Idempotency in HTTP methods
**Detailed Explanation**:
*   **Definition**: An operation is idempotent if making the same request multiple times produces the **same result state** on the server as making it once.
*   **Idempotent**: GET, PUT, DELETE, HEAD.
    *   Deleting user ID 5 once -> User gone.
    *   Deleting user ID 5 ten times -> User still gone (State is same).
*   **Non-Idempotent**: POST.
    *   POST `/users` once -> 1 user created.
    *   POST `/users` ten times -> 10 users created.

---

## 24. How to achieve security in REST APIs?
**Detailed Explanation**:
1.  **Authentication**: Who are you? (Basic Auth, JWT, OAuth2).
2.  **Authorization**: What can you do? (Role-based access).
3.  **HTTPS**: Encrypt data in transit (SSL/TLS).
4.  **JWT (JSON Web Token)**: Stateless auth. Server signs a token, client sends it in `Authorization: Bearer <token>` header. Server verifies signature. No session stored on server.

---

## 25. Spring Security Loop (Auth vs Auth)
**Detailed Explanation**:
*   **Authentication (Loop 1)**: User sends creds. `AuthenticationManager` verifies checks DB. If valid, creates `Authentication` object and stores in `SecurityContext`.
*   **Authorization (Loop 2)**: FilterSecurityInterceptor checks `SecurityContext`. Does current user have Role required for this URL?
*   **Filters**: Spring Security is essentially a chain of filters (`DelegatingFilterProxy`) that intercept every request before it reaches the DispatcherServlet.

---

## 26. Usage of @Transactional annotation
**Detailed Explanation**: Ensures that a method executes within a database transaction. If method succeeds, Commit. If exception (Runtime), Rollback.
*   **Propagation**:
    *   `REQUIRED` (Default): Use existing transaction or create new.
    *   `REQUIRES_NEW`: Suspend existing, create fresh transaction.
*   **Isolation**:
    *   `READ_COMMITTED`: Prevent dirty reads.
    *   `SERIALIZABLE`: Strict.

**Example**:
```java
@Service
public class OrderService {
    @Transactional
    public void placeOrder(Order order) {
        inventoryRepo.decreaseStock(order);
        paymentRepo.processPayment(order);
        // If payment fails, stock decrease is ROLLED BACK automatically.
    }
}
```

---

## 27. JPA vs Hibernate
**Detailed Explanation**:
*   **JPA (Java Persistence API)**: A **Specification** (Interface). It defines the standard rules for ORM in Java. You cannot use JPA alone.
*   **Hibernate**: An **Implementation** (Provider). A library that actually implements the JPA interfaces.
*   **Analogy**: JPA is the interface `List`, Hibernate is the implementation `ArrayList`.

---

## 28. Hibernate Entity States
**Detailed Explanation**:
1.  **Transient**: Created with `new`, not associated with any Session, no ID. (Not in DB).
2.  **Persistent**: Associated with a Session, represented in DB. Changes are auto-saved.
3.  **Detached**: Session closed. Object has ID, but changes won't be saved automatically.
4.  **Removed**: Scheduled for deletion.

---

## 29. N+1 Problem in Hibernate and how to solve it?
**Detailed Explanation**:
*   **Problem**: Fetching a list of N Parent entities causes N+1 queries.
    *   Query 1: Select * from Departments. (Returns N departments).
    *   Query 2..N+1: For *each* department, select * from Employees where dept_id = ?.
*   **Solution**:
    1.  **Join Fetch**: Use JPQL `JOIN FETCH` to load data in a single query.
    2.  **Entity Graph**: Define graph to eager load specific fields.
    3.  **Batch Size**: `@BatchSize(size=10)` to load children in batches.

**Example**:
`SELECT d FROM Department d JOIN FETCH d.employees`

---

## 30. Lazy vs Eager Loading
**Detailed Explanation**:
*   **Eager (Default for @ManyToOne)**: Fetches the related data immediately along with the parent. Can cause performance issues (loading too much).
*   **Lazy (Default for @OneToMany)**: Fetches related data *on-demand* (when you call `getEmployees()`).
*   **Best Practice**: Prefer LAZY loading to save memory, use JOIN FETCH when you actually need the data.

---

## 31. Difference between save() and saveAll(), save() vs persist()
**Detailed Explanation**:
*   **`save()` (Spring Data)**: Checks if ID exists. If null/new -> calls `persist` (Insert). If exists -> calls `merge` (Update).
*   **`saveAll()`**: Performs batch save for a list.
*   **`persist()` (JPA)**: insert only. Void return.
*   **`merge()` (JPA)**: update only. Returns copy.

---

## 32. Entity Relationships
**Detailed Explanation**:
*   **`@OneToOne`**: User <-> Profile.
*   **`@OneToMany`**: Department -> Employees. (Foreign key in Employee table).
*   **`@ManyToOne`**: Employee -> Department.
*   **`@ManyToMany`**: Student <-> Course. (Requires a 3rd Join Table).

---

## 33. How to create a Custom Annotation?
**Detailed Explanation**: Use `@interface` keyword. Combine with AOP (Aspect Oriented Programming) to add logic.
*   **Use Case**: Logging time taken by method `@LogExecutionTime`.

**Example**:
```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
public @interface MyCustomAnnotation {
    String value() default "default";
}
```

---

## 34. Interceptors vs Filters in Spring
**Detailed Explanation**:
*   **Filter**:
    *   Part of **Servlet Standard**.
    *   Runs **before** request reaches Spring DispatcherServlet.
    *   Good for: Security, Compression, Logging raw request.
*   **Interceptor**:
    *   Part of **Spring MVC**.
    *   Runs **inside** Spring context (between DispatcherServlet and Controller).
    *   Good for: Auth checks, adding global model attributes, access to Handler object.

---

## 35. How to handle Circular Dependency?
**Detailed Explanation**:
*   **Problem**: Bean A needs Bean B, and Bean B needs Bean A. Spring cannot create either.
*   **Solutions**:
    1.  **Redesign**: Best. Move common logic to Bean C.
    2.  **`@Lazy`**: Inject one bean lazily (`@Autowired @Lazy`). Spring creates a proxy instead of the real bean, breaking the initialization loop.
    3.  **Setter Injection**: Use setters instead of constructors (breaks the cycle at creation time).

**Example**:
```java
class A {
    @Autowired @Lazy
    private B b;
}
class B {
    @Autowired
    private A a;
}
```
