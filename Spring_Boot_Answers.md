# Spring Boot Interview Questions & Answers (Deep Dive)

## 1. What is Spring Boot and what are its advantages?
**Core Concept:**
Spring Boot is an opinionated framework that simplifies building production-ready Spring applications. It takes the "Convention over Configuration" approach.

**Key Advantages:**
1.  **Auto Configuration:** It scans the classpath. If `spring-webmvc.jar` is found, it automatically configures a `DispatcherServlet`. If `mysql-connector` is found, it configures a `DataSource`.
2.  **Embedded Servers:** It packages Tomcat, Jetty, or Undertow *inside* the JAR. You run the app as `java -jar app.jar` instead of deploying a WAR to an external Tomcat.
3.  **Starters:** Curated dependencies. `spring-boot-starter-web` imports Spring MVC, Jackson, Tomcat, and logging libraries automatically, resolving version conflicts (Bill of Materials - BOM).
4.  **Actuator:** Provides endpoints like `/health`, `/metrics`, `/loggers` for monitoring without writing code.

## 2. Internal Flow: How does a Spring Boot Application Start?
When you call `SpringApplication.run(App.class, args)`:

1.  **Bootstrapping:** It determines the application type (Servlet Stack or Reactive/WebFlux).
2.  **Environment Preparation:** Loads properties from `application.properties`, System Envs, and Command Line Args.
3.  **ApplicationContext Creation:** Creates the IOC Container (e.g., `AnnotationConfigServletWebServerApplicationContext` for web apps).
4.  **Auto-Configuration:**
    - It reads `META-INF/spring.factories` (or `org.springframework.boot.autoconfigure.AutoConfiguration.imports` in Spring Boot 3.x) from all jar files.
    - It finds all AutoConfiguration classes (e.g., `HibernateJpaAutoConfiguration`).
    - It applies `@Conditional` checks (e.g., Is `Hibernate` class in classpath? Is `datasource` bean missing?).
    - If conditions match, it registers the infrastructure beans.
5.  **Embedded Server Start:** It finds a `ServletWebServerFactory` bean (Tomcat) and starts the web server on port 8080.
6.  **Runners:** Executes any beans implementing `CommandLineRunner` or `ApplicationRunner`.

## 3. Difference between @Component, @Service, @Repository, @Controller
Technically, `@Service`, `@Repository`, and `@Controller` are just aliases (specializations) of `@Component`. They all get scanned and registered as Singleton beans.
**Why use specific ones?**
- **@Controller:** Signals the web layer.
- **@Service:** Signals business logic. (Currently purely semantic, but might get future features).
- **@Repository:** Signals Data Access Layer. **Crucial Feature:** It enables **PersistenceExceptionTranslationPostProcessor**, which catches database-specific exceptions (like SQLException) and re-throws them as Spring's `DataAccessException` (unchecked) hierarchy.

## 4. Bean Scopes in Spring (Examples)
1.  **Singleton (Default):** One instance per ApplicationContext.
    - *Risk:* Not thread-safe if you store state in instance variables.
2.  **Prototype:** New instance every time it is injected or retrieved (`context.getBean()`).
    - *Use Case:* Stateful beans that are not thread-safe.
3.  **Request:** One instance per HTTP Request.
    - *Use Case:* User-specific data for a single call.
4.  **Session:** One instance per HTTP User Session.
    - *Use Case:* Shopping Cart, User Login Info.

**Injecting Prototype into Singleton Problem:**
If Class A (Singleton) has `@Autowired` Class B (Prototype). B is injected **only once** when A is created. So effectively, B acts like a singleton inside A.
- **Solution:** Use `@Lookup` method injection or `ObjectProvider<B>`.

## 5. Dependency Injection Types
1.  **Constructor Injection (Best Practice):**
    ```java
    @Service
    public class UserService {
        private final UserRepository repo;
        
        // @Autowired is optional in newer Spring if 1 constructor
        public UserService(UserRepository repo) {
            this.repo = repo;
        }
    }
    ```
    - *Why Best?* Ensures dependencies are not null. Allows fields to be `final` (Immutable). Easier to test (just pass mock in constructor).

2.  **Setter Injection:**
    ```java
    @Autowired
    public void setRepo(UserRepository repo) { this.repo = repo; }
    ```
    - *Use Case:* Optional dependencies or circular dependency resolution.

3.  **Field Injection:** ` @Autowired private UserRepository repo;`
    - *Drawback:* Uses Reflection. Hard to write unit tests without Spring Context or ReflectionUtil.

## 6. How to handle exceptions in Spring Boot?
**1. Global Exception Handling (@ControllerAdvice):**
Create a central class to handle exceptions for ALL controllers.
```java
@RestControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFound(UserNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }
}
```

**2. Local Handling:**
Define `@ExceptionHandler` inside the specific Controller class.

**3. ResponseStatusException:**
Throw directly from service: `throw new ResponseStatusException(HttpStatus.BAD_REQUEST, "Invalid ID");`.

## 7. JPA vs Hibernate vs Spring Data JPA
- **JPA (Java Persistence API):** A Standard Specification (Interface). It defines *how* valid ORM should work (EntityManager, Annotations like @Entity).
- **Hibernate:** The Implementation. The actual library that does the mapping and SQL generation.
- **Spring Data JPA:** A layer *on top* of JPA. It reduces boilerplate.
    - Instead of writing `entityManager.persist(user)`, you write `interface UserRepo extends JpaRepository<User, Long>`.
    - It generates the implementation dynamically at runtime using Proxy.

## 8. N+1 Problem in Hibernate
**Scenario:**
You have `User` -> `@OneToMany` -> `Orders`.
You do `List<User> users = userRepo.findAll();` (1 Query).
Then you loop: `for(User u : users) { u.getOrders().size(); }`
Hibernate fires **1 query per user** to fetch orders lazily.
Total Queries: 1 (Users) + N (Orders for each user). If 1000 users, 1001 queries.

**Solution: Join Fetch**
Write a custom JPQL query:
`@Query("SELECT u FROM User u JOIN FETCH u.orders")`
This forces a single SQL JOIN query to fetch Users AND Orders together.

## 9. @Transactional Deep Dive
**ACID Guarantees:**
When you mark a method `@Transactional`, Spring creates a Proxy around the bean.
- **Begin:** Before method starts, it asks TransactionManager to start a DB transaction.
- **Commit:** If method finishes successfully, it commits.
- **Rollback:** If an **Unchecked Exception** (RuntimeException) occurs, it rolls back.
    - *Note:* Checked Exceptions (e.g., IOException) DO NOT trigger rollback by default.
    - *Fix:* `@Transactional(rollbackFor = Exception.class)`.

**Propagation Types:**
- **REQUIRED (Default):** Join existing transaction or create new.
- **REQUIRES_NEW:** Pause current transaction, create a brand new independent transaction. (If inner fails, outer can still succeed).
- **MANDATORY:** Caller must have a transaction, else throw error.

## 10. Spring Security Architecture
**Authentication (Who are you?):**
User sends credentials -> `AuthenticationFilter` -> `AuthenticationManager` -> `DaoAuthenticationProvider` -> `UserDetailsService` (Loads user from DB) -> PasswordEncoder (Matches hash).

**Authorization (What can you do?):**
Once authenticated, the `SecurityContext` holds the `Principal` (User) and `Authorities` (Roles).
Access decisions happen via FilterSecurityInterceptor or Method Security (`@PreAuthorize("hasRole('ADMIN')")`).

**JWT Flow:**
1.  Login POST /login -> Server verifies creds -> Generates Signed JWT (Base64) -> Returns to Client.
2.  Client stores JWT.
3.  Future Requests: Client sends `Authorization: Bearer <token>`.
4.  Server Filter (`OncePerRequestFilter`) intercepts -> Validates Signature -> Extracts User -> Sets Context. Stateless!
