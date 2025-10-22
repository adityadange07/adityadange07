# LEVEL 2: INTERMEDIATE (2-4 Years Experience)

# Spring Boot Intermediate

# Advanced Configuration

## 102. How does Spring Boot auto-configuration work?

### **Spring Boot Auto-Configuration**

Spring Boot’s **auto-configuration** is one of its most powerful features. It automatically configures your application based on the **dependencies on the classpath** and the **properties defined in `application.properties` or `application.yml`**, reducing the need for boilerplate configuration.

---

## **1. How Auto-Configuration Works**

1. **Spring Boot Starter Dependencies**

   * When you add a starter dependency, e.g., `spring-boot-starter-web`, it **brings all required libraries** for web development (Spring MVC, Jackson, Tomcat).

2. **`@EnableAutoConfiguration` / `@SpringBootApplication`**

   * `@SpringBootApplication` is a combination of:

     ```java
     @Configuration
     @EnableAutoConfiguration
     @ComponentScan
     ```
   * `@EnableAutoConfiguration` triggers Spring Boot to **scan the classpath** and automatically configure beans for components it finds.

3. **Conditional Configuration**

   * Auto-configuration classes use **`@ConditionalOnClass`, `@ConditionalOnMissingBean`, `@ConditionalOnProperty`** annotations to decide whether to create a bean.
   * Example: Spring Boot configures a **DataSource** only if:

     * `DataSource` class is on the classpath
     * No other `DataSource` bean is defined

4. **Application Context**

   * Spring Boot loads the **auto-configuration classes** and registers beans in the **ApplicationContext**.
   * If user-defined beans exist, Spring Boot **backs off** (does not override them).

---

## **2. Example: Auto-Configured DataSource**

```java
@SpringBootApplication
public class DemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

* Add **`spring-boot-starter-data-jpa`** and **database driver** to `pom.xml`.
* Define **database properties** in `application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/testdb
spring.datasource.username=root
spring.datasource.password=root
spring.jpa.hibernate.ddl-auto=update
```

* Spring Boot automatically configures:

  * `DataSource` bean
  * `EntityManagerFactory`
  * `TransactionManager`

No manual configuration is required.

---

## **3. Key Annotations in Auto-Configuration**

| Annotation                  | Purpose                                                                 |
| --------------------------- | ----------------------------------------------------------------------- |
| `@EnableAutoConfiguration`  | Enables Spring Boot’s auto-configuration mechanism                      |
| `@ConditionalOnClass`       | Apply configuration only if a class is on the classpath                 |
| `@ConditionalOnMissingBean` | Apply configuration only if a bean is not already defined               |
| `@ConditionalOnProperty`    | Apply configuration based on property value                             |
| `@SpringBootApplication`    | Combines `@Configuration`, `@EnableAutoConfiguration`, `@ComponentScan` |

---

## **4. Auto-Configuration Flow**

1. Spring Boot scans **`spring.factories`** in all dependencies.
2. Loads all **`@Configuration` classes** listed under `EnableAutoConfiguration`.
3. Applies **conditional annotations** to decide which beans to create.
4. Registers beans in the **Spring ApplicationContext**.
5. User-defined beans **override auto-configured beans**.

---

## **5. Advantages of Auto-Configuration**

1. Reduces boilerplate configuration.
2. Works out-of-the-box with common libraries.
3. Provides **sensible defaults** that can be customized via `application.properties`.
4. Allows **user-defined beans** to override auto-configured ones.
5. Speeds up development for microservices and REST APIs.

---

💡 **Interview Tip:**

> "Spring Boot auto-configuration works by scanning the classpath, using `@Conditional` annotations, and automatically creating beans if certain classes are present and no user-defined beans exist. You can override defaults by defining your own beans or customizing properties."

---

I can next explain **how Spring Boot decides which auto-configuration class to load and how to debug auto-configuration issues**, which is a common follow-up in interviews.

Do you want me to cover that?

---

## 103. What is the role of @Configuration and @Bean?

### **Spring Annotations: `@Configuration` and `@Bean`**

In Spring, `@Configuration` and `@Bean` are core annotations used to define **Java-based configuration** instead of XML. They are part of Spring’s **IoC container mechanism** for defining and managing beans.

---

## **1. `@Configuration`**

* **Definition:** Indicates that a class is a **source of bean definitions**.
* **Purpose:** Tells Spring that the class contains **methods annotated with `@Bean`** that should be registered as beans in the **ApplicationContext**.
* **Example:**

```java
@Configuration
public class AppConfig {
    @Bean
    public MyService myService() {
        return new MyServiceImpl();
    }
}
```

* **Key Points:**

  1. Classes annotated with `@Configuration` are **processed by Spring container** to generate beans.
  2. Ensures **singleton beans** by default using **CGLIB proxies** so that method calls within the configuration class return the **same bean instance**.

---

## **2. `@Bean`**

* **Definition:** Indicates that a **method produces a bean** to be managed by the Spring container.
* **Purpose:** Explicitly declares a bean **instead of using component scanning** (`@Component`, `@Service`).
* **Example:**

```java
@Configuration
public class AppConfig {

    @Bean
    public MyRepository myRepository() {
        return new MyRepositoryImpl();
    }

    @Bean
    public MyService myService() {
        return new MyServiceImpl(myRepository());
    }
}
```

* **Key Points:**

  1. Can define **dependencies** between beans by calling other `@Bean` methods.
  2. Beans are **singletons by default**, unless `@Scope` is used.
  3. Can customize initialization and destruction using **`initMethod`** and **`destroyMethod`** attributes.

---

## **3. How They Work Together**

1. `@Configuration` marks the class as a **configuration source**.
2. `@Bean` inside the class defines **bean instances** to be registered in the **Spring IoC container**.
3. Spring ensures that **dependencies are injected** automatically between beans.

**Example Flow:**

```java
@Configuration
public class AppConfig {

    @Bean
    public DataSource dataSource() {
        return new HikariDataSource();
    }

    @Bean
    public UserService userService() {
        return new UserServiceImpl(dataSource()); // dependency injection
    }
}
```

* Spring creates `dataSource` bean first, then injects it into `userService` bean.
* Both beans are managed in **ApplicationContext**.

---

## **4. Difference Between `@Component` and `@Bean`**

| Feature               | @Component                           | @Bean                                 |
| --------------------- | ------------------------------------ | ------------------------------------- |
| **Used on**           | Class                                | Method inside @Configuration class    |
| **Bean Registration** | Automatically via classpath scanning | Explicitly defined by developer       |
| **Scope**             | Singleton by default                 | Singleton by default (can use @Scope) |
| **Dependencies**      | Use @Autowired for injection         | Can call other @Bean methods directly |
| **Flexibility**       | Less control                         | Full control over bean creation       |

---

## **5. Advantages**

1. **Java-based configuration** (no XML).
2. **Explicit and clear** bean definitions.
3. Supports **method-level dependency injection**.
4. Easy to customize **init and destroy methods**.
5. Works seamlessly with **Spring Boot auto-configuration**.

---

💡 **Interview Tip:**

> "`@Configuration` marks a class as a source of bean definitions. `@Bean` defines the actual bean instances to be managed by Spring. Together, they replace XML configuration with type-safe Java code."

---

I can next explain **difference between @Configuration, @Component, and @Service**, which is often asked in interviews.

Do you want me to cover that?

---

## 104. How do profiles work in Spring Boot (@Profile use case)?

### **Spring Boot Profiles and `@Profile` Annotation**

Spring Boot **profiles** allow you to define **environment-specific configurations** (like dev, test, prod) and **load beans or properties selectively** based on the active profile. This makes your application **flexible and environment-aware**.

---

## **1. What is a Profile?**

* A **profile** is a named, logical grouping of beans and configurations.
* Spring Boot can **activate a profile** to load specific beans or properties.
* Typical profiles: `dev`, `test`, `prod`.

---

## **2. Using `@Profile` Annotation**

* **Definition:** `@Profile` indicates that a **bean or configuration class should only be loaded** when a specific profile is active.
* **Package:** `org.springframework.context.annotation.Profile`

**Example:**

```java
@Configuration
@Profile("dev")
public class DevDatabaseConfig {
    @Bean
    public DataSource dataSource() {
        return new HikariDataSource(); // dev DB config
    }
}

@Configuration
@Profile("prod")
public class ProdDatabaseConfig {
    @Bean
    public DataSource dataSource() {
        return new HikariDataSource(); // production DB config
    }
}
```

* Here, **only one `DataSource` bean** will be loaded depending on the **active profile**.

---

## **3. Activating a Profile**

### **a) Using `application.properties` or `application.yml`**

```properties
spring.profiles.active=dev
```

```yaml
spring:
  profiles:
    active: prod
```

* Spring Boot loads beans or property files matching the active profile.

---

### **b) Using Command-Line Arguments**

```bash
java -jar app.jar --spring.profiles.active=prod
```

---

### **c) Using Environment Variables**

```bash
export SPRING_PROFILES_ACTIVE=dev
```

---

## **4. Profile-Specific Properties Files**

* Spring Boot supports **profile-specific property files**:

```
application.properties        // common properties
application-dev.properties    // dev-specific
application-prod.properties   // prod-specific
```

* Active profile determines which **properties file overrides default values**.

---

## **5. Combining @Profile and @Bean**

* You can use `@Profile` at **class-level** or **method-level**.

```java
@Configuration
public class AppConfig {

    @Bean
    @Profile("dev")
    public Service devService() {
        return new DevServiceImpl();
    }

    @Bean
    @Profile("prod")
    public Service prodService() {
        return new ProdServiceImpl();
    }
}
```

* Only the **bean matching the active profile** will be registered.

---

## **6. Use Cases of Profiles**

1. **Environment-Specific Beans** – Dev DB vs Prod DB.
2. **Feature Toggles** – Enable/disable features per environment.
3. **External Services** – Use mocks in dev, real services in prod.
4. **Testing** – Load test configurations without affecting production.

---

## **7. Summary Table**

| Feature                     | Description                                               |
| --------------------------- | --------------------------------------------------------- |
| `@Profile`                  | Load bean/config only for active profile                  |
| Activation                  | `application.properties`, env variable, command-line args |
| Profile-Specific Properties | `application-{profile}.properties` or YAML                |
| Use Case                    | Dev/prod DB configs, mock services, feature toggles       |

---

💡 **Interview Tip:**

> "Spring Profiles allow environment-specific configurations. Using `@Profile` or profile-specific property files, you can define beans that are loaded only for certain environments, making your application flexible and easy to deploy across dev, test, and prod."

---

I can next explain **how multiple profiles work together and default profiles in Spring Boot**, which is a common follow-up question in interviews.

Do you want me to cover that?

---

## 105. What is @Transactioal, and what's the benifit?

### **`@Transactional` in Spring**

The `@Transactional` annotation in Spring is used to **manage database transactions declaratively**. It ensures that a **set of operations execute as a single unit of work**, with **automatic rollback on failure**.

---

## **1. Definition**

* **Annotation:** `org.springframework.transaction.annotation.Transactional`
* **Purpose:** Marks a **method or class** to participate in a **transaction**.
* Spring **automatically begins, commits, or rolls back** the transaction based on the method execution outcome.

**Basic Syntax:**

```java
@Transactional
public void transferMoney(Account from, Account to, double amount) {
    withdraw(from, amount);
    deposit(to, amount);
}
```

---

## **2. Key Features**

1. **Automatic Transaction Management**

   * Begins a transaction when method starts.
   * Commits if method completes normally.
   * Rolls back if a runtime exception occurs.

2. **Declarative Approach**

   * No need to write **manual commit/rollback code** like JDBC `Connection.commit()` or `rollback()`.

3. **Propagation**

   * Defines how **existing transactions** should behave.
   * Common types:

     * `REQUIRED` (default): join existing or create new transaction
     * `REQUIRES_NEW`: always create a new transaction
     * `MANDATORY`: must join existing transaction

4. **Rollback Rules**

   * By default, rolls back on **unchecked exceptions** (`RuntimeException`, `Error`).
   * Can be customized using `rollbackFor` or `noRollbackFor`.

```java
@Transactional(rollbackFor = SQLException.class)
public void saveData() { ... }
```

5. **Isolation Levels**

   * Controls **concurrency effects** like dirty reads, non-repeatable reads, and phantom reads.
   * Examples: `READ_COMMITTED`, `REPEATABLE_READ`, `SERIALIZABLE`.

---

## **3. Example**

```java
@Service
public class BankService {

    @Autowired
    private AccountRepository repo;

    @Transactional
    public void transfer(long fromId, long toId, double amount) {
        Account from = repo.findById(fromId).get();
        Account to = repo.findById(toId).get();

        from.setBalance(from.getBalance() - amount);
        to.setBalance(to.getBalance() + amount);

        repo.save(from);
        repo.save(to);

        // If any exception occurs, transaction will rollback automatically
    }
}
```

---

## **4. Benefits of `@Transactional`**

| Benefit                      | Description                                                         |
| ---------------------------- | ------------------------------------------------------------------- |
| **Consistency**              | Ensures **ACID properties** for database operations                 |
| **Automatic Rollback**       | Rollback on failure or exception automatically                      |
| **Declarative Transactions** | No need to manually manage transactions                             |
| **Simplifies Code**          | Reduces boilerplate commit/rollback logic                           |
| **Flexible**                 | Supports **propagation, isolation levels, timeout, read-only mode** |
| **Integration**              | Works with Spring Data JPA, JDBC, Hibernate, etc.                   |

---

## **5. Notes / Best Practices**

1. **Only public methods** should be annotated for proxy-based transactions.
2. **Self-invocation problem:** `@Transactional` does **not work** if a method calls another transactional method in the **same class**.
3. Use **rollbackFor** for checked exceptions if needed.
4. Read-only transactions for **queries** can improve performance:

```java
@Transactional(readOnly = true)
public List<Account> getAccounts() { ... }
```

---

💡 **Interview Tip:**

> "`@Transactional` ensures that multiple database operations execute as a single atomic unit. It simplifies transaction management, automatically rolls back on exceptions, and supports propagation and isolation levels to handle concurrency."

---

I can next explain **difference between programmatic and declarative transactions**, which is a common follow-up question in Spring interviews.

Do you want me to cover that?

---

## 106. How do you write a global exception handler in Spring Boot?

### **Global Exception Handling in Spring Boot**

In Spring Boot, you can handle exceptions **centrally** for all controllers using a **global exception handler**. This avoids repetitive `try-catch` blocks in controllers and provides **consistent error responses**.

---

## **1. Using `@ControllerAdvice` and `@ExceptionHandler`**

* **`@ControllerAdvice`**: Marks a class as a **global exception handler**.
* **`@ExceptionHandler`**: Defines methods to handle specific exceptions.

**Example:**

```java
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.ControllerAdvice;
import org.springframework.web.bind.annotation.ExceptionHandler;

@ControllerAdvice
public class GlobalExceptionHandler {

    // Handle custom exception
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity<String> handleResourceNotFound(ResourceNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }

    // Handle generic exceptions
    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleGenericException(Exception ex) {
        return new ResponseEntity<>("Something went wrong: " + ex.getMessage(),
                                    HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

* **Explanation:**

  1. `ResourceNotFoundException` is handled specifically.
  2. Any other exception is caught by the **generic handler**.
  3. Returns **HTTP status codes** and custom messages.

---

## **2. Using `@ResponseStatus` for Simple Exceptions**

* You can annotate **custom exception classes** with `@ResponseStatus` to automatically set HTTP status:

```java
@ResponseStatus(HttpStatus.NOT_FOUND)
public class ResourceNotFoundException extends RuntimeException {
    public ResourceNotFoundException(String message) {
        super(message);
    }
}
```

* Spring automatically returns **404 Not Found** when this exception is thrown.

---

## **3. Returning a Standard Error Response**

* For APIs, it’s better to return **structured JSON responses**:

```java
import java.time.LocalDateTime;

public class ErrorResponse {
    private String message;
    private int status;
    private LocalDateTime timestamp;

    // constructors, getters, setters
}
```

```java
@ExceptionHandler(ResourceNotFoundException.class)
public ResponseEntity<ErrorResponse> handleResourceNotFound(ResourceNotFoundException ex) {
    ErrorResponse error = new ErrorResponse(
        ex.getMessage(),
        HttpStatus.NOT_FOUND.value(),
        LocalDateTime.now()
    );
    return new ResponseEntity<>(error, HttpStatus.NOT_FOUND);
}
```

* Provides a **consistent response structure** for frontend/API clients.

---

## **4. Best Practices**

1. **Handle specific exceptions first**, then generic exceptions.
2. **Log exceptions** for debugging: `logger.error("Error:", ex);`
3. Use **ErrorResponse DTO** for consistent API output.
4. Keep **controller logic clean** by moving exception handling to global layer.
5. Combine with **`@ResponseStatus`** for simplicity when detailed response is not needed.

---

## **5. Summary Table**

| Feature             | Description                             |
| ------------------- | --------------------------------------- |
| `@ControllerAdvice` | Marks class as global exception handler |
| `@ExceptionHandler` | Handles specific exception types        |
| `@ResponseStatus`   | Sets HTTP status for exception class    |
| ErrorResponse DTO   | Provides structured JSON response       |

---

💡 **Interview Tip:**

> "Global exception handling in Spring Boot is implemented using `@ControllerAdvice` with `@ExceptionHandler`. It centralizes error handling, provides consistent responses, and keeps controller code clean."

---

I can next explain **difference between @ControllerAdvice, @RestControllerAdvice, and local exception handling**, which is often asked in Spring Boot interviews.

Do you want me to cover that?

---

## 107. Difference between application.properties and application.yml?

### **Difference Between `application.properties` and `application.yml` in Spring Boot**

Spring Boot allows you to configure your application using either **`application.properties`** or **`application.yml`** (YAML) files. Both serve the same purpose, but differ in **format, readability, and structure**.

---

## **1. Format**

| Feature            | `application.properties`                           | `application.yml`                                       |
| ------------------ | -------------------------------------------------- | ------------------------------------------------------- |
| **Syntax**         | Key-value pairs                                    | Hierarchical indentation (YAML format)                  |
| **Example**        | `server.port=8080`                                 | `server:\n  port: 8080`                                 |
| **Structure**      | Flat                                               | Nested / hierarchical                                   |
| **Comments**       | `# Comment`                                        | `# Comment`                                             |
| **Arrays / Lists** | Comma-separated: `spring.profiles.active=dev,prod` | Dash list: `spring.profiles.active:\n  - dev\n  - prod` |

---

## **2. Example Comparison**

**`application.properties`:**

```properties
server.port=8080
spring.datasource.url=jdbc:mysql://localhost:3306/testdb
spring.datasource.username=root
spring.datasource.password=root
spring.jpa.hibernate.ddl-auto=update
spring.profiles.active=dev
```

**`application.yml`:**

```yaml
server:
  port: 8080

spring:
  datasource:
    url: jdbc:mysql://localhost:3306/testdb
    username: root
    password: root
  jpa:
    hibernate:
      ddl-auto: update
  profiles:
    active: dev
```

* YAML provides a **clean hierarchical structure**, which is easier to read for complex configurations.

---

## **3. Key Differences**

| Feature            | `application.properties`                 | `application.yml`                                |
| ------------------ | ---------------------------------------- | ------------------------------------------------ |
| **Readability**    | Less readable for nested structures      | More readable and organized                      |
| **Data Hierarchy** | Flattened keys (dot notation)            | Supports nested properties naturally             |
| **Lists / Arrays** | Comma-separated                          | Dash `-` syntax or inline `[item1, item2]`       |
| **Complex Config** | Harder to manage                         | Easier to manage complex nested configs          |
| **File Parsing**   | Loaded by Spring Boot `PropertiesLoader` | Loaded by Spring Boot `YamlPropertySourceLoader` |

---

## **4. Pros and Cons**

### **Properties File**

* **Pros:**

  * Simple and easy for small apps
  * Supported in older Spring apps
* **Cons:**

  * Harder to read for nested configurations
  * Not very maintainable for large projects

### **YAML File**

* **Pros:**

  * Better readability
  * Ideal for **nested configs** like multiple data sources, profiles, etc.
  * Supports **lists and maps** easily
* **Cons:**

  * Indentation-sensitive (can lead to errors)
  * Slightly more complex syntax

---

## **5. Usage in Profiles**

* You can create **profile-specific files** for both:

```
application-dev.properties
application-prod.properties
```

```
application-dev.yml
application-prod.yml
```

* Spring Boot automatically picks the correct file based on **`spring.profiles.active`**.

---

💡 **Interview Tip:**

> "`application.properties` is simple key-value configuration, while `application.yml` is hierarchical and more readable for complex configs. YAML is preferred in modern Spring Boot projects for clarity and structure, especially with multiple profiles or nested properties."

---

I can next explain **when to prefer application.yml over properties and how to convert between them**, which is often asked in Spring Boot interviews.

Do you want me to cover that?

---

## 108. What is the use of CommandLineRunner and ApplicationRunner?

### **CommandLineRunner vs ApplicationRunner in Spring Boot**

Both **`CommandLineRunner`** and **`ApplicationRunner`** are **functional interfaces in Spring Boot** used to **execute code after the Spring Boot application starts**. They are typically used for **initialization tasks** like seeding the database, loading default data, or running startup logic.

---

## **1. CommandLineRunner**

* **Definition:** Executes code **after the Spring Boot application context is loaded**.
* **Interface:** `org.springframework.boot.CommandLineRunner`
* **Method:**

```java
void run(String... args) throws Exception;
```

* **Example:**

```java
@Component
public class MyCommandLineRunner implements CommandLineRunner {

    @Override
    public void run(String... args) throws Exception {
        System.out.println("CommandLineRunner executed!");
        for (String arg : args) {
            System.out.println("Arg: " + arg);
        }
    }
}
```

* **Notes:**

  * `args` contains **raw command-line arguments** passed to the application.
  * Useful for **simple startup logic** or scripts.

---

## **2. ApplicationRunner**

* **Definition:** Similar to `CommandLineRunner`, but **provides parsed application arguments**.
* **Interface:** `org.springframework.boot.ApplicationRunner`
* **Method:**

```java
void run(ApplicationArguments args) throws Exception;
```

* **Example:**

```java
@Component
public class MyApplicationRunner implements ApplicationRunner {

    @Override
    public void run(ApplicationArguments args) throws Exception {
        System.out.println("ApplicationRunner executed!");
        
        // Access non-option arguments
        System.out.println("Non-option args: " + args.getNonOptionArgs());
        
        // Access option arguments
        if(args.containsOption("debug")) {
            System.out.println("Debug mode enabled");
        }
    }
}
```

* **Notes:**

  * `ApplicationArguments` provides:

    * `getOptionNames()` → List of option names
    * `getOptionValues("name")` → List of values for option
    * `getNonOptionArgs()` → List of arguments without options

---

## **3. Key Differences**

| Feature              | CommandLineRunner          | ApplicationRunner                                            |
| -------------------- | -------------------------- | ------------------------------------------------------------ |
| **Method Signature** | `void run(String... args)` | `void run(ApplicationArguments args)`                        |
| **Argument Access**  | Raw string array           | Parsed and structured (`ApplicationArguments`)               |
| **Use Case**         | Simple startup tasks       | Tasks needing option/non-option arguments                    |
| **Example Input**    | `--debug=true test`        | Can access `--debug=true` as option and `test` as non-option |

---

## **4. Execution Order**

* Multiple runners can be defined.
* Use **`@Order`** annotation to control execution sequence:

```java
@Component
@Order(1)
public class FirstRunner implements CommandLineRunner { ... }

@Component
@Order(2)
public class SecondRunner implements CommandLineRunner { ... }
```

---

## **5. Use Cases**

1. **Database initialization** – seed default data.
2. **Startup checks** – verify resources or configuration.
3. **Execute scripts or batch jobs** at application startup.
4. **Debug/logging startup parameters**.

---

💡 **Interview Tip:**

> "`CommandLineRunner` executes code after Spring Boot startup with raw string arguments, while `ApplicationRunner` provides parsed and structured application arguments. Use `ApplicationRunner` when you need to handle options and non-option args."

---

I can next explain **the difference between `@PostConstruct`, CommandLineRunner, and ApplicationRunner**, which is a common interview follow-up.

Do you want me to cover that?

---

## 109. How does the embedded server (Tomcat) work in Spring Boot?

### **Embedded Server (Tomcat) in Spring Boot**

Spring Boot comes with **embedded servers** like **Tomcat, Jetty, or Undertow**, allowing your application to run as a **standalone executable JAR** without needing an external server. Tomcat is the **default embedded server** in Spring Boot.

---

## **1. How Embedded Tomcat Works**

1. **Spring Boot Starter Web**

   * When you include `spring-boot-starter-web`, Spring Boot automatically adds **Tomcat libraries** as dependencies.
   * Example in `pom.xml`:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>
```

2. **SpringApplication Bootstrapping**

   * `SpringApplication.run()` starts the Spring context and initializes **auto-configured beans**, including the embedded Tomcat server.

3. **Tomcat Embedded Lifecycle**

   * Tomcat runs **inside the application JVM**, no need to install it separately.
   * Default port: `8080` (configurable via `server.port`).
   * Handles HTTP requests and forwards them to **Spring DispatcherServlet**.

4. **DispatcherServlet Integration**

   * Tomcat receives HTTP requests → **servlet container** → DispatcherServlet → Spring controllers → returns response.

---

## **2. Key Features of Embedded Tomcat**

| Feature                | Description                                                                 |
| ---------------------- | --------------------------------------------------------------------------- |
| **Standalone**         | No external Tomcat installation required                                    |
| **Auto-configuration** | Spring Boot configures server settings automatically                        |
| **Customizable**       | Configure port, context path, SSL, max threads via `application.properties` |
| **Servlet Support**    | Supports servlets, filters, listeners                                       |
| **Executable JAR/WAR** | Package as JAR (`java -jar`) or WAR for external deployment                 |

---

## **3. Customizing Embedded Tomcat**

You can configure it via **`application.properties`**:

```properties
server.port=9090
server.servlet.context-path=/myapp
server.error.whitelabel.enabled=false
```

Or programmatically:

```java
@Bean
public WebServerFactoryCustomizer<TomcatServletWebServerFactory> tomcatCustomizer() {
    return factory -> factory.setPort(9090);
}
```

---

## **4. Advantages of Embedded Tomcat**

1. **Simplified Deployment** – Just run the JAR; no external server setup.
2. **Consistency** – Same server version across environments.
3. **Easy Integration with Spring Boot** – Auto-configured by Spring Boot starters.
4. **Portability** – Works on any environment with JDK.
5. **Rapid Development** – Supports hot reload with Spring DevTools.

---

## **5. How It Differs from Traditional Deployment**

| Aspect            | Traditional Tomcat         | Embedded Tomcat (Spring Boot)  |
| ----------------- | -------------------------- | ------------------------------ |
| **Installation**  | Separate installation      | Comes with the app             |
| **Deployment**    | Deploy WAR to server       | Run JAR directly               |
| **Configuration** | Manual server.xml, web.xml | Auto-configured by Spring Boot |
| **Portability**   | Dependent on server setup  | Fully portable JAR             |

---

💡 **Interview Tip:**

> "Embedded Tomcat allows Spring Boot applications to run standalone without an external server. Spring Boot auto-configures Tomcat, handles HTTP requests, and forwards them to DispatcherServlet, making deployment easier and consistent."

---

I can next explain **differences between embedded Tomcat, Jetty, and Undertow in Spring Boot**, which is often asked in interviews.

Do you want me to cover that?

---

## 110. How do you override default auto-configuration?

### **Overriding Default Auto-Configuration in Spring Boot**

Spring Boot auto-configuration provides **sensible defaults**, but sometimes you need to **customize or override them**. Spring Boot allows overriding auto-configured beans in several ways.

---

## **1. Override by Defining Your Own Bean**

* **Spring Boot Back-Off Mechanism:** Auto-configuration beans are only created **if a bean of the same type is missing**.
* **Solution:** Define a bean with the **same type or name** in your configuration; Spring Boot will **use your bean instead**.

**Example: Custom DataSource**

```java
@Configuration
public class CustomDataSourceConfig {

    @Bean
    public DataSource dataSource() {
        HikariDataSource ds = new HikariDataSource();
        ds.setJdbcUrl("jdbc:mysql://localhost:3306/customdb");
        ds.setUsername("customuser");
        ds.setPassword("custompass");
        return ds;
    }
}
```

* Spring Boot **ignores the default DataSource** and uses this one.

---

## **2. Exclude Auto-Configuration Classes**

* Use `exclude` in `@SpringBootApplication` or `@EnableAutoConfiguration` to **prevent certain auto-configurations** from loading.

```java
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

* Useful when you want **full control** over configuration or when auto-configuration conflicts with custom setup.

---

## **3. Customize Properties in `application.properties` or `application.yml`**

* Many auto-configured beans respect **Spring Boot properties**.
* Example: Override Tomcat server port:

```properties
server.port=9090
spring.datasource.url=jdbc:mysql://localhost:3306/customdb
spring.jpa.show-sql=true
```

* Properties allow **non-intrusive customization** without defining beans.

---

## **4. Using `@Primary` Annotation**

* If multiple beans of the **same type** exist, you can mark **one as primary** using `@Primary`:

```java
@Bean
@Primary
public DataSource primaryDataSource() {
    return new HikariDataSource();
}
```

* Spring uses the `@Primary` bean wherever an **autowired bean of that type** is needed.

---

## **5. Conditional Beans and Custom Configuration**

* You can also use `@ConditionalOnMissingBean` and `@ConditionalOnBean` for **fine-grained control**:

```java
@Bean
@ConditionalOnMissingBean(DataSource.class)
public DataSource defaultDataSource() {
    return new HikariDataSource();
}
```

* This ensures your bean **only loads if no other bean of the type exists**, maintaining auto-configuration flexibility.

---

## **6. Summary Table**

| Method                     | When to Use                                    |
| -------------------------- | ---------------------------------------------- |
| Define custom bean         | Override specific auto-configured bean         |
| Exclude auto-configuration | Disable conflicting or unnecessary auto-config |
| application.properties     | Customize behavior without defining beans      |
| `@Primary`                 | Choose preferred bean when multiple exist      |
| Conditional beans          | Control bean creation with conditions          |

---

💡 **Interview Tip:**

> "Spring Boot auto-configuration can be overridden by defining your own bean of the same type, excluding specific auto-configuration classes, customizing properties, or using `@Primary` for preference. This provides flexibility while still leveraging Spring Boot’s defaults."

---

I can next explain **how to debug Spring Boot auto-configuration using `spring-boot-actuator` and `@Conditional` annotations**, which is often asked in interviews.

Do you want me to cover that?

---

## 111. How do you handle circular dependencies in Spring Boot?

### **Handling Circular Dependencies in Spring Boot**

A **circular dependency** occurs when **two or more Spring beans depend on each other**, either directly or indirectly, which can cause Spring to fail during **bean creation**.

---

## **1. Example of Circular Dependency**

```java
@Component
public class A {
    private final B b;

    public A(B b) {
        this.b = b;
    }
}

@Component
public class B {
    private final A a;

    public B(A a) {
        this.a = a;
    }
}
```

* Spring cannot instantiate `A` because it requires `B`, which in turn requires `A`.
* This will throw: **`BeanCurrentlyInCreationException`**.

---

## **2. How Spring Boot Handles Circular Dependencies**

* **By default**, Spring **supports circular dependencies** for **singleton beans** using **setter/field injection**, but **constructor injection** fails.
* Recommended approaches: avoid constructor-based circular references if possible.

---

## **3. Solutions to Handle Circular Dependencies**

### **a) Use `@Lazy` Annotation**

* Marks a bean to be **lazily initialized**, delaying its creation until it’s needed.

```java
@Component
public class A {
    private final B b;

    public A(@Lazy B b) {
        this.b = b;
    }
}

@Component
public class B {
    private final A a;

    public B(@Lazy A a) {
        this.a = a;
    }
}
```

* Spring can now create proxies to resolve the circular dependency.

---

### **b) Use Setter Injection Instead of Constructor Injection**

* Constructor injection **does not allow circular references**, but setter injection works for singleton beans.

```java
@Component
public class A {
    private B b;

    @Autowired
    public void setB(B b) {
        this.b = b;
    }
}

@Component
public class B {
    private A a;

    @Autowired
    public void setA(A a) {
        this.a = a;
    }
}
```

* Spring can **instantiate one bean first** and then inject the other via setter.

---

### **c) Redesign Bean Dependencies**

* Circular dependencies often indicate **tight coupling**.
* Refactor code to break the cycle:

  1. Introduce a **third service** that both depend on.
  2. Combine classes if logically related.
  3. Use **event publishing** or **callbacks** instead of direct dependencies.

---

### **d) Use `ObjectProvider` / `Provider`**

* Allows **lazy fetching** of beans without `@Lazy`.

```java
@Component
public class A {
    private final B b;

    @Autowired
    public A(ObjectProvider<B> bProvider) {
        this.b = bProvider.getIfAvailable();
    }
}
```

* Helps in situations where **lazy initialization** is preferred.

---

## **4. Key Notes**

1. **Constructor Injection** + Circular Dependency → fails.
2. **Setter/Field Injection** + Circular Dependency → works for singletons.
3. Prefer **refactoring code** over using `@Lazy` for maintainability.
4. Singleton beans can form circular dependencies, but **prototype beans** cannot.

---

## **5. Summary Table**

| Approach         | Pros                                      | Cons                            |
| ---------------- | ----------------------------------------- | ------------------------------- |
| `@Lazy`          | Quick fix, resolves constructor injection | Can hide design issues          |
| Setter Injection | Works for singleton beans                 | Not ideal for immutability      |
| Refactor Design  | Clean and maintainable                    | May require significant changes |
| ObjectProvider   | Lazy resolution without `@Lazy`           | Slightly complex                |

---

💡 **Interview Tip:**

> "Circular dependencies occur when two beans depend on each other. Best practices are to refactor the code to remove the cycle. If necessary, `@Lazy` or setter injection can resolve the issue for singleton beans."

---

I can next explain **how Spring Boot detects circular dependencies and the related properties like `spring.main.allow-circular-references`**, which is commonly asked.

Do you want me to cover that?

---


# Dependency Injection

## 112. What is constructor injection vs field injection vs setter injection?

### **Dependency Injection Types in Spring**

Spring provides multiple ways to inject dependencies into beans: **Constructor Injection**, **Setter Injection**, and **Field Injection**. Each has its use cases, pros, and cons.

---

## **1. Constructor Injection**

* **Definition:** Dependencies are injected **through the class constructor**.
* **Recommended for:** **Mandatory dependencies**, immutable objects.

**Example:**

```java
@Component
public class UserService {

    private final UserRepository userRepository;

    @Autowired // optional in Spring 4.3+ for single constructor
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public void createUser(String name) {
        userRepository.save(name);
    }
}
```

**Pros:**

* Dependencies are **final and immutable**.
* Promotes **clean design and testability**.
* Works well with **unit testing** (can pass mocks via constructor).
* Makes **mandatory dependencies explicit**.

**Cons:**

* Circular dependencies cannot be resolved with constructor injection.

---

## **2. Setter Injection**

* **Definition:** Dependencies are injected through **public setter methods**.
* **Recommended for:** **Optional dependencies** or when circular references need to be resolved.

**Example:**

```java
@Component
public class UserService {

    private UserRepository userRepository;

    @Autowired
    public void setUserRepository(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public void createUser(String name) {
        userRepository.save(name);
    }
}
```

**Pros:**

* Allows **optional dependencies**.
* Can **resolve circular dependencies** for singleton beans.

**Cons:**

* Dependencies are mutable.
* Requires explicit setters for all dependencies.

---

## **3. Field Injection**

* **Definition:** Dependencies are injected **directly into fields** using `@Autowired`.
* **Recommended for:** Quick prototyping, small projects (not ideal for production).

**Example:**

```java
@Component
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public void createUser(String name) {
        userRepository.save(name);
    }
}
```

**Pros:**

* Minimal boilerplate, very concise.

**Cons:**

* Harder to unit test (cannot inject mocks easily).
* Violates **encapsulation** (direct field access).
* Not recommended for large, maintainable applications.

---

## **4. Summary Table**

| Feature                  | Constructor Injection | Setter Injection                | Field Injection           |
| ------------------------ | --------------------- | ------------------------------- | ------------------------- |
| **Injection Point**      | Constructor           | Setter method                   | Field directly            |
| **Mandatory / Optional** | Mandatory             | Optional                        | Optional                  |
| **Circular Dependency**  | ❌ Cannot resolve      | ✅ Can resolve (singleton beans) | ❌ Cannot resolve          |
| **Immutability**         | ✅ Final fields        | ❌ Mutable                       | ❌ Mutable                 |
| **Testability**          | ✅ Easy with mocks     | ✅ Easy                          | ❌ Hard without reflection |
| **Boilerplate**          | Medium                | High                            | Low                       |

---

💡 **Interview Tip:**

> "Constructor injection is preferred for mandatory dependencies because it enforces immutability and testability. Setter injection is good for optional dependencies or circular references, while field injection is convenient but not recommended for maintainable applications."

---

I can next explain **best practices for choosing the right injection type in Spring Boot projects**, which is often asked in interviews.

Do you want me to cover that?

---

## 113. What is @Qualifier and @Primary annotation?

### **`@Qualifier` vs `@Primary` in Spring**

In Spring, when **multiple beans of the same type** exist, the framework may not know which one to inject. **`@Qualifier`** and **`@Primary`** are used to **resolve ambiguity**.

---

## **1. `@Primary` Annotation**

* **Definition:** Marks a bean as the **default choice** when multiple beans of the same type exist.
* Spring will **inject the `@Primary` bean** if no specific bean is specified.

**Example:**

```java
@Component
@Primary
public class MySqlDataSource implements DataSource {
    // MySQL implementation
}

@Component
public class PostgresDataSource implements DataSource {
    // PostgreSQL implementation
}

@Component
public class DatabaseService {
    private final DataSource dataSource;

    @Autowired
    public DatabaseService(DataSource dataSource) {
        this.dataSource = dataSource; // MySqlDataSource injected by default
    }
}
```

* **Use Case:** When you have **one preferred bean** among multiple candidates.

---

## **2. `@Qualifier` Annotation**

* **Definition:** Explicitly specifies **which bean** to inject when multiple candidates exist.
* Works **alongside `@Autowired`**.

**Example:**

```java
@Component
public class DatabaseService {

    private final DataSource dataSource;

    @Autowired
    public DatabaseService(@Qualifier("postgresDataSource") DataSource dataSource) {
        this.dataSource = dataSource; // PostgresDataSource explicitly injected
    }
}
```

* `@Qualifier` **overrides `@Primary`**, giving precise control over bean selection.

---

## **3. Field Injection Example with `@Qualifier`**

```java
@Autowired
@Qualifier("postgresDataSource")
private DataSource dataSource;
```

* Injects the bean named `postgresDataSource` even if a `@Primary` bean exists.

---

## **4. Key Differences**

| Feature             | `@Primary`                        | `@Qualifier`                                  |
| ------------------- | --------------------------------- | --------------------------------------------- |
| **Purpose**         | Sets default bean                 | Specifies exact bean to inject                |
| **Usage**           | On bean definition                | On injection point                            |
| **Overridden By**   | Can be overridden by `@Qualifier` | N/A                                           |
| **Number of Beans** | One primary bean                  | Can be used to select any bean among multiple |

---

## **5. Best Practices**

1. Use `@Primary` when **one bean is the main/default choice**.
2. Use `@Qualifier` when **you need to inject a specific bean**.
3. Avoid using **both excessively**; design beans to minimize ambiguity.
4. Works with **constructor, setter, and field injection**.

---

💡 **Interview Tip:**

> "`@Primary` marks a default bean for injection, while `@Qualifier` explicitly chooses a bean when multiple candidates exist. `@Qualifier` overrides `@Primary` at the injection point."

---

I can next explain **`@Primary` and `@Qualifier` usage with profiles and multiple environments**, which is a common Spring Boot interview scenario.

Do you want me to cover that?

---

## 114. If both @Qualifier and @Primary are used, which one will take precedence?

### **`@Qualifier` vs `@Primary` Precedence in Spring**

When **both `@Primary` and `@Qualifier` are present**, **`@Qualifier` always takes precedence** over `@Primary`.

---

## **1. How It Works**

* **`@Primary`**: Marks a bean as the **default choice** when multiple beans of the same type exist.
* **`@Qualifier`**: Explicitly **selects a specific bean** at the injection point.
* **Rule:** Spring **injects the bean specified by `@Qualifier`**, ignoring the `@Primary` bean.

---

## **2. Example**

```java
@Component
@Primary
public class MySqlDataSource implements DataSource {
    // Primary/default bean
}

@Component
public class PostgresDataSource implements DataSource {
    // Secondary bean
}

@Component
public class DatabaseService {

    private final DataSource dataSource;

    @Autowired
    public DatabaseService(@Qualifier("postgresDataSource") DataSource dataSource) {
        this.dataSource = dataSource; // PostgresDataSource injected
    }
}
```

* Even though `MySqlDataSource` is marked as `@Primary`, the **PostgresDataSource** is injected because of `@Qualifier`.

---

## **3. Field Injection Example**

```java
@Autowired
@Qualifier("postgresDataSource")
private DataSource dataSource; // Overrides the @Primary bean
```

---

## **4. Key Points**

1. `@Qualifier` **always wins** when explicitly specified.
2. `@Primary` only applies **if no `@Qualifier` is used**.
3. Both annotations can coexist: `@Primary` provides a **default**, and `@Qualifier` allows **explicit override**.

---

💡 **Interview Tip:**

> "When both `@Primary` and `@Qualifier` are used, Spring injects the bean specified by `@Qualifier`. `@Primary` acts as a fallback only when no `@Qualifier` is present."

---

I can next explain **how to use `@Qualifier` with multiple profiles and multiple implementations**, which is a common Spring Boot interview scenario.

Do you want me to cover that?

---

## 115. How to avoid bean creation failure in dependency injection?

### **Avoiding Bean Creation Failures in Spring Dependency Injection**

Bean creation failures in Spring usually occur due to **missing beans, multiple beans, circular dependencies, or misconfigurations**. Proper practices can help avoid these issues.

---

## **1. Common Causes of Bean Creation Failure**

| Cause                       | Description                                            |
| --------------------------- | ------------------------------------------------------ |
| **Missing Bean**            | No bean defined for a dependency type                  |
| **Multiple Beans**          | Multiple candidates without `@Primary` or `@Qualifier` |
| **Circular Dependencies**   | Beans depend on each other creating a loop             |
| **Incorrect Configuration** | Bean not annotated or component scan missing           |
| **Type Mismatch**           | Bean type incompatible with injection point            |

---

## **2. Strategies to Avoid Bean Creation Failure**

### **a) Use @Component / @Service / @Repository Correctly**

* Make sure all beans are **annotated** and within **component scan path**:

```java
@Component
public class UserService { ... }
```

* Verify `@SpringBootApplication` scans the package containing the bean.

---

### **b) Handle Multiple Beans with @Primary or @Qualifier**

* When multiple beans of the same type exist, Spring throws `NoUniqueBeanDefinitionException`.
* **Solutions:**

```java
@Component
@Primary
public class MySqlDataSource implements DataSource { ... }

@Component
public class PostgresDataSource implements DataSource { ... }

@Autowired
@Qualifier("postgresDataSource")
private DataSource dataSource; // explicit selection
```

---

### **c) Use @Lazy for Circular Dependencies**

* Circular dependencies with constructor injection can cause failure.
* **Solutions:**

```java
@Component
public class A {
    private final B b;
    public A(@Lazy B b) { this.b = b; }
}

@Component
public class B {
    private final A a;
    public B(@Lazy A a) { this.a = a; }
}
```

* Alternatively, use **setter injection** for singleton beans.

---

### **d) Make Optional Dependencies Explicit**

* For optional dependencies, use `required = false`:

```java
@Autowired(required = false)
private OptionalService optionalService;
```

* Spring won't fail if the bean is missing.

---

### **e) Check Bean Type Compatibility**

* Ensure the **injected bean type matches** the dependency type:

```java
@Autowired
private DataSource dataSource; // must match the type of available beans
```

---

### **f) Conditional Beans and Profiles**

* Beans can be **conditionally created** using `@ConditionalOnMissingBean` or `@Profile` to avoid conflicts:

```java
@Bean
@ConditionalOnMissingBean
public DataSource defaultDataSource() { ... }

@Bean
@Profile("dev")
public DataSource devDataSource() { ... }
```

---

### **g) Enable Component Scanning**

* Ensure Spring scans the correct package:

```java
@SpringBootApplication(scanBasePackages = "com.example")
public class MyApp { ... }
```

* Missing scan paths cause Spring to **not detect beans**.

---

### **3. Summary Table**

| Problem             | Solution                                        |
| ------------------- | ----------------------------------------------- |
| Missing bean        | Annotate with `@Component`, ensure scan path    |
| Multiple beans      | Use `@Primary` or `@Qualifier`                  |
| Circular dependency | Use `@Lazy` or setter injection                 |
| Optional bean       | `@Autowired(required = false)`                  |
| Bean type mismatch  | Ensure correct type or interface implementation |
| Profile mismatch    | Use correct `@Profile` or conditional beans     |

---

💡 **Interview Tip:**

> "Bean creation failures usually occur due to missing beans, multiple candidates, or circular dependencies. They can be avoided using proper annotations (`@Primary`, `@Qualifier`, `@Lazy`), component scanning, optional dependencies, and conditional beans."

---

I can next explain **how Spring Boot logs and reports bean creation errors for debugging**, which is a common follow-up in interviews.

Do you want me to cover that?

---

## 116. @Autowired vs @Qualifier

### **`@Autowired` vs `@Qualifier` in Spring**

Both **`@Autowired`** and **`@Qualifier`** are related to **dependency injection**, but they serve different purposes.

---

## **1. `@Autowired`**

* **Purpose:** Marks a dependency for **automatic injection** by Spring.
* **Behavior:** Spring tries to inject a **matching bean** by **type**.

**Example:**

```java
@Component
public class UserService {

    @Autowired
    private UserRepository userRepository; // Injects a UserRepository bean automatically
}
```

* **Notes:**

  * If **only one bean of that type** exists → injected automatically.
  * If **multiple beans exist** → Spring throws `NoUniqueBeanDefinitionException` unless resolved.

---

## **2. `@Qualifier`**

* **Purpose:** Resolves **ambiguity** when multiple beans of the same type exist.
* Works **with `@Autowired`** to specify **which bean** to inject.

**Example:**

```java
@Component
public class MySqlDataSource implements DataSource { }

@Component
public class PostgresDataSource implements DataSource { }

@Component
public class DatabaseService {

    @Autowired
    @Qualifier("postgresDataSource")
    private DataSource dataSource; // Explicitly injects PostgresDataSource
}
```

* **Notes:**

  * Overrides any `@Primary` bean.
  * Can be used on **constructor, setter, or field injection**.

---

## **3. Key Differences**

| Feature                   | `@Autowired`                   | `@Qualifier`                                       |
| ------------------------- | ------------------------------ | -------------------------------------------------- |
| **Purpose**               | Marks dependency for injection | Specifies which bean to inject when multiple exist |
| **Required**              | Yes (by default)               | Works with `@Autowired`                            |
| **Resolves ambiguity**    | ❌ No                           | ✅ Yes                                              |
| **Default injection**     | By type                        | By name (or bean ID)                               |
| **Can override @Primary** | ❌                              | ✅                                                  |

---

## **4. Usage Together**

* Always use `@Qualifier` **with `@Autowired`** if multiple beans of the same type exist:

```java
@Autowired
@Qualifier("beanName")
private SomeService service;
```

* Without `@Qualifier`, Spring will attempt **type-based injection** and may fail if multiple beans exist.

---

💡 **Interview Tip:**

> "`@Autowired` is used to inject dependencies automatically by type. `@Qualifier` is used alongside `@Autowired` to specify which bean to inject when multiple candidates exist. `@Qualifier` overrides `@Primary`."

---

I can next explain **`@Primary`, `@Qualifier`, and `@Autowired` together with multiple beans and profiles**, which is a common tricky Spring Boot interview question.

Do you want me to cover that?

---

## 117. @Primary vs @Qualifier

### **`@Primary` vs `@Qualifier` in Spring**

Both **`@Primary`** and **`@Qualifier`** are used to **resolve ambiguity** when multiple beans of the same type exist, but they serve **different purposes**.

---

## **1. `@Primary`**

* **Definition:** Marks a bean as the **default candidate** for injection when multiple beans of the same type exist.
* **Use Case:** One bean should be the **preferred/default** without specifying explicitly.

**Example:**

```java
@Component
@Primary
public class MySqlDataSource implements DataSource { }

@Component
public class PostgresDataSource implements DataSource { }

@Component
public class DatabaseService {

    @Autowired
    private DataSource dataSource; // MySqlDataSource injected by default
}
```

* **Notes:**

  * Only **one primary bean** should exist for a type.
  * Acts as a **fallback** when no `@Qualifier` is used.

---

## **2. `@Qualifier`**

* **Definition:** Explicitly **selects which bean** to inject when multiple candidates exist.
* **Use Case:** You need **specific bean injection**, overriding `@Primary`.

**Example:**

```java
@Component
public class DatabaseService {

    @Autowired
    @Qualifier("postgresDataSource")
    private DataSource dataSource; // PostgresDataSource injected explicitly
}
```

* **Notes:**

  * Can override `@Primary`.
  * Works with **constructor, setter, and field injection**.

---

## **3. Key Differences**

| Feature                  | `@Primary`             | `@Qualifier`                            |
| ------------------------ | ---------------------- | --------------------------------------- |
| **Purpose**              | Default bean selection | Explicit bean selection                 |
| **Used On**              | Bean definition        | Injection point                         |
| **Overrides the other?** | ❌                      | ✅ Overrides `@Primary`                  |
| **Best Use**             | One main/default bean  | Specific selection among multiple beans |
| **Required?**            | No, optional           | Required if ambiguity exists            |

---

## **4. Example Together**

```java
@Component
@Primary
public class MySqlDataSource implements DataSource { }

@Component
public class PostgresDataSource implements DataSource { }

@Component
public class DatabaseService {

    @Autowired
    @Qualifier("postgresDataSource")
    private DataSource dataSource; // Explicitly chooses PostgresDataSource, ignoring @Primary
}
```

* Here, **`@Qualifier` wins over `@Primary`**.

---

💡 **Interview Tip:**

> "`@Primary` provides a default bean when multiple candidates exist. `@Qualifier` explicitly selects a bean and overrides `@Primary` at the injection point."

---

I can next explain **`@Primary` and `@Qualifier` usage with multiple Spring profiles**, which is a common interview scenario.

Do you want me to cover that?

---


# REST API Advanced

## 118. @RequestMapping vs @GetMapping

### **`@RequestMapping` vs `@GetMapping` in Spring**

Both **`@RequestMapping`** and **`@GetMapping`** are used to map **HTTP requests** to handler methods in Spring controllers, but they differ in **flexibility and specificity**.

---

## **1. `@RequestMapping`**

* **Definition:** General-purpose annotation for mapping HTTP requests to controller methods.
* **Can handle:** Any HTTP method (GET, POST, PUT, DELETE, etc.) using the `method` attribute.

**Example:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @RequestMapping(value = "/all", method = RequestMethod.GET)
    public List<User> getAllUsers() {
        return List.of(new User("Alice"), new User("Bob"));
    }

    @RequestMapping(value = "/create", method = RequestMethod.POST)
    public String createUser(@RequestBody User user) {
        return "User created: " + user.getName();
    }
}
```

* **Features:**

  * Supports **path variables, query parameters, headers, consumes/produces**.
  * Can map multiple HTTP methods with `method = {RequestMethod.GET, RequestMethod.POST}`.

---

## **2. `@GetMapping`**

* **Definition:** Specialized shortcut for **`@RequestMapping(method = RequestMethod.GET)`**.
* Introduced in **Spring 4.3** to simplify RESTful mappings.

**Example:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/all")
    public List<User> getAllUsers() {
        return List.of(new User("Alice"), new User("Bob"));
    }
}
```

* **Advantages:**

  * More **concise and readable**.
  * Specifically for **GET requests**; similar annotations exist for other HTTP methods:

    * `@PostMapping` → POST
    * `@PutMapping` → PUT
    * `@DeleteMapping` → DELETE
    * `@PatchMapping` → PATCH

---

## **3. Key Differences**

| Feature         | `@RequestMapping`                                         | `@GetMapping`                               |
| --------------- | --------------------------------------------------------- | ------------------------------------------- |
| **HTTP Method** | Can handle all (GET, POST, etc.) using `method` attribute | Only GET (shortcut for `RequestMethod.GET`) |
| **Introduced**  | Spring 2.x                                                | Spring 4.3                                  |
| **Conciseness** | More verbose                                              | More concise                                |
| **Use Case**    | Flexible, multiple methods                                | Simple GET mapping for REST APIs            |

---

## **4. Summary**

* Use **`@RequestMapping`** if you need **flexibility for multiple HTTP methods** or **custom attributes**.
* Use **`@GetMapping`** (and other shortcuts) for **clear, concise REST controllers**.

---

💡 **Interview Tip:**

> "`@GetMapping` is a specialized version of `@RequestMapping` for GET requests. Use `@RequestMapping` when multiple HTTP methods need to be handled or when more configuration is required."

---

I can next explain **`@RequestParam` vs `@PathVariable`**, which is a common follow-up question after request mapping.

Do you want me to cover that?

---

## 119. @PathVariable vs @RequestParam

### **`@PathVariable` vs `@RequestParam` in Spring**

Both annotations are used to **extract values from an HTTP request** in Spring controllers, but they are used in **different contexts**.

---

## **1. `@PathVariable`**

* **Definition:** Binds a **method parameter** to a **URI template variable** in the URL path.
* **Use Case:** When the value is part of the **path** itself.

**Example:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public String getUserById(@PathVariable("id") int userId) {
        return "User ID: " + userId;
    }
}
```

* **Request:** `GET /users/101` → `userId = 101`

**Notes:**

* Can handle **multiple path variables**.
* Path variables are **mandatory** by default but can be made optional with `required = false` and a default value.

---

## **2. `@RequestParam`**

* **Definition:** Binds a **method parameter** to a **query parameter** in the URL.
* **Use Case:** When the value comes from **URL query string or form parameters**.

**Example:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/search")
    public String searchUser(@RequestParam("name") String username) {
        return "Searching user: " + username;
    }
}
```

* **Request:** `GET /users/search?name=Alice` → `username = Alice`

**Notes:**

* Supports **default values**: `@RequestParam(value="name", defaultValue="Guest")`
* Can handle **optional parameters** with `required=false`.

---

## **3. Key Differences**

| Feature                  | `@PathVariable`                 | `@RequestParam`                              |
| ------------------------ | ------------------------------- | -------------------------------------------- |
| **Source**               | URL path                        | Query string or form data                    |
| **Mandatory by default** | Yes (unless `required=false`)   | Yes (unless `required=false`)                |
| **Typical Use**          | Resource identifier (RESTful)   | Filters, optional data, search parameters    |
| **Syntax**               | `/users/{id}`                   | `/users?name=Alice`                          |
| **Multiple Values**      | Yes, via multiple path segments | Yes, via repeated query parameters or arrays |

---

## **4. Combined Example**

```java
@GetMapping("/users/{id}/posts")
public String getUserPosts(
        @PathVariable("id") int userId,
        @RequestParam(value="sort", defaultValue="date") String sortBy) {
    return "User ID: " + userId + ", Sorted by: " + sortBy;
}
```

* **Request:** `GET /users/101/posts?sort=title`
* **Output:** `User ID: 101, Sorted by: title`

---

💡 **Interview Tip:**

> "`@PathVariable` extracts values from the URL path, typically used for resource IDs in REST APIs. `@RequestParam` extracts query or form parameters, often used for optional filters or search criteria."

---

I can next explain **`@RequestBody` vs `@RequestParam` vs `@PathVariable`**, which is a common advanced interview question.

Do you want me to cover that?

---

## 120. @PostMapping vs @PutMapping

### **`@PostMapping` vs `@PutMapping` in Spring**

Both annotations are used to handle **HTTP requests** in Spring controllers, but they map to **different HTTP methods** and have different **semantics** in RESTful design.

---

## **1. `@PostMapping`**

* **Definition:** Shortcut for `@RequestMapping(method = RequestMethod.POST)`
* **Purpose:** Used to **create a new resource**.
* **Idempotent:** ❌ Not idempotent (repeating the request can create multiple resources).

**Example:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @PostMapping("/create")
    public String createUser(@RequestBody User user) {
        // Logic to save user
        return "User created: " + user.getName();
    }
}
```

* **Request:** `POST /users/create` with JSON body `{ "name": "Alice" }`
* Creates a **new user**.

---

## **2. `@PutMapping`**

* **Definition:** Shortcut for `@RequestMapping(method = RequestMethod.PUT)`
* **Purpose:** Used to **update an existing resource** or **create a resource if it does not exist**.
* **Idempotent:** ✅ Idempotent (repeating the request has the same effect).

**Example:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @PutMapping("/update/{id}")
    public String updateUser(@PathVariable int id, @RequestBody User user) {
        // Logic to update user with ID
        return "User updated: " + user.getName();
    }
}
```

* **Request:** `PUT /users/update/101` with JSON body `{ "name": "Alice Updated" }`
* Updates the **existing user** with ID 101.

---

## **3. Key Differences**

| Feature                   | `@PostMapping`           | `@PutMapping`                                  |
| ------------------------- | ------------------------ | ---------------------------------------------- |
| **HTTP Method**           | POST                     | PUT                                            |
| **Purpose**               | Create new resource      | Update existing resource (or create if absent) |
| **Idempotent**            | ❌ No                     | ✅ Yes                                          |
| **Request Body**          | Usually required         | Usually required                               |
| **Typical Use**           | `/users/create`          | `/users/update/{id}`                           |
| **Multiple Calls Effect** | Creates multiple entries | Same result as one call                        |

---

## **4. RESTful Best Practices**

1. **POST** → Create new resource, server generates ID.
2. **PUT** → Update resource at known URL or ID; can also be used to **replace** the resource.
3. **PATCH** → Partially update a resource (introduced in HTTP/1.1).

---

💡 **Interview Tip:**

> "`@PostMapping` is used for creating resources and is not idempotent. `@PutMapping` is used for updating resources and is idempotent. In REST, POST creates, PUT updates or replaces."

---

I can next explain **`@PatchMapping` vs `@PutMapping`**, which is often asked in advanced REST API interviews.

Do you want me to cover that?

---

## 121. PUT vs PATCH

### **`PUT` vs `PATCH` in REST / Spring**

Both **`PUT`** and **`PATCH`** are HTTP methods used to **update resources**, but they differ in **how they apply updates** and **idempotency**.

---

## **1. PUT**

* **Definition:** Replaces the **entire resource** with the new data.
* **Idempotent:** ✅ Yes (repeating the request produces the same result).
* **Use Case:** When you have **all fields of the resource** and want to update/replace it.

**Example in Spring:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @PutMapping("/update/{id}")
    public User updateUser(@PathVariable int id, @RequestBody User user) {
        // Replace the entire user resource with the new object
        return userService.updateUser(id, user);
    }
}
```

* **Request:** `PUT /users/101`
* JSON body must contain **all fields** of the user. Missing fields may be overwritten with null.

---

## **2. PATCH**

* **Definition:** Applies a **partial update** to the resource.
* **Idempotent:** ✅ Ideally idempotent (repeating may produce same result), but depends on implementation.
* **Use Case:** When you want to **update only certain fields** of a resource.

**Example in Spring:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @PatchMapping("/update/{id}")
    public User updateUserName(@PathVariable int id, @RequestBody Map<String, Object> updates) {
        // Update only the specified fields
        return userService.patchUser(id, updates);
    }
}
```

* **Request:** `PATCH /users/101`
* JSON body: `{ "name": "Alice Updated" }` → only the **name** field is updated.

---

## **3. Key Differences**

| Feature          | PUT                                        | PATCH                                 |
| ---------------- | ------------------------------------------ | ------------------------------------- |
| **Update Type**  | Full replacement                           | Partial update                        |
| **Request Body** | Must contain all fields                    | Only fields to update                 |
| **Idempotent**   | ✅ Yes                                      | ✅ Ideally (depends on implementation) |
| **Use Case**     | Replace resource                           | Modify selected fields                |
| **Risk**         | Missing fields may overwrite existing data | Safer for partial updates             |

---

## **4. Summary**

* **PUT** → Replace entire resource; requires full object.
* **PATCH** → Modify resource partially; safer for updates of a few fields.

---

💡 **Interview Tip:**

> "Use `PUT` for complete replacement of a resource, and `PATCH` for partial updates. PATCH is more efficient when updating only some fields."

---

I can next explain **when to use POST vs PUT vs PATCH vs DELETE in REST**, which is a common REST API interview question.

Do you want me to cover that?

---

## 122. @ExceptionHandler vs @ControllerAdvice

### **`@ExceptionHandler` vs `@ControllerAdvice` in Spring**

Both annotations are used for **handling exceptions** in Spring MVC / Spring Boot, but they work at **different scopes**.

---

## **1. `@ExceptionHandler`**

* **Definition:** Handles exceptions **within a single controller**.
* **Scope:** Local to the **controller class** where it is defined.

**Example:**

```java
@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public User getUser(@PathVariable int id) {
        return userService.findById(id)
                          .orElseThrow(() -> new UserNotFoundException("User not found"));
    }

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFound(UserNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }
}
```

* Only handles `UserNotFoundException` **for this controller**.

---

## **2. `@ControllerAdvice`**

* **Definition:** Provides **global exception handling** for **all controllers** (or selected ones).
* **Scope:** Application-wide, can handle exceptions from multiple controllers.
* Often combined with `@ExceptionHandler` inside the advice class.

**Example:**

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFound(UserNotFoundException ex) {
        return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
    }

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleAllExceptions(Exception ex) {
        return new ResponseEntity<>("Something went wrong: " + ex.getMessage(),
                                    HttpStatus.INTERNAL_SERVER_ERROR);
    }
}
```

* Handles exceptions **globally**, across all controllers.

---

## **3. Key Differences**

| Feature                | `@ExceptionHandler`                    | `@ControllerAdvice`                                           |
| ---------------------- | -------------------------------------- | ------------------------------------------------------------- |
| **Scope**              | Single controller                      | Global / multiple controllers                                 |
| **Definition**         | Defined inside a controller            | Separate class annotated with `@ControllerAdvice`             |
| **Use Case**           | Controller-specific exception handling | Centralized/global exception handling                         |
| **Combines with**      | `@ResponseStatus` or `ResponseEntity`  | `@ExceptionHandler` methods inside advice                     |
| **Optional Targeting** | N/A                                    | Can filter controllers with `basePackages`, `assignableTypes` |

---

## **4. Summary**

* **`@ExceptionHandler`** → Local, used for exceptions in a **single controller**.
* **`@ControllerAdvice`** → Global, used for exceptions **across multiple controllers**.

---

💡 **Interview Tip:**

> "`@ExceptionHandler` handles exceptions at the controller level. `@ControllerAdvice` allows centralized/global exception handling for multiple controllers. Use `@ControllerAdvice` for consistent error responses in REST APIs."

---

I can next explain **`@RestControllerAdvice` vs `@ControllerAdvice`**, which is often asked in REST API interviews.

Do you want me to cover that?

---


# Spring Boot Annotations

## 123. @ComponentScan vs @EnableAutoConfiguration

### **`@ComponentScan` vs `@EnableAutoConfiguration` in Spring Boot**

Both annotations are commonly used in **Spring Boot**, but they serve **different purposes** in the application context.

---

## **1. `@ComponentScan`**

* **Definition:** Tells Spring **where to look for components** (beans, controllers, services, repositories).
* **Purpose:** Automatically detects classes annotated with `@Component`, `@Service`, `@Repository`, `@Controller`, etc., and **registers them as beans**.
* **Scope:** Package-level scanning.

**Example:**

```java
@SpringBootApplication
@ComponentScan(basePackages = "com.example.services")
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

* Scans only the specified package `com.example.services`.
* Avoids **manual bean registration** via `@Bean`.

---

## **2. `@EnableAutoConfiguration`**

* **Definition:** Tells Spring Boot to **automatically configure beans** based on **classpath dependencies** and **application properties**.
* **Purpose:** Reduces boilerplate configuration. Spring Boot analyzes the **classpath and beans** and creates default configurations.
* **Scope:** Global, automatic setup.

**Example:**

```java
@SpringBootApplication
@EnableAutoConfiguration
public class MyApplication {
    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

* If `spring-boot-starter-web` is in the classpath, Spring Boot **automatically configures Tomcat, Spring MVC, Jackson**, etc.

---

## **3. Relationship with @SpringBootApplication**

```java
@SpringBootApplication
```

* Combines three annotations:

  1. `@Configuration` → Marks the class as a source of bean definitions.
  2. `@ComponentScan` → Scans for components in the package and sub-packages.
  3. `@EnableAutoConfiguration` → Enables Spring Boot’s auto-configuration.

So you **rarely need to use `@ComponentScan` or `@EnableAutoConfiguration` separately** unless you want custom behavior.

---

## **4. Key Differences**

| Feature                 | @ComponentScan                      | @EnableAutoConfiguration                             |
| ----------------------- | ----------------------------------- | ---------------------------------------------------- |
| **Purpose**             | Scan packages for Spring components | Auto-configure beans based on classpath & properties |
| **Scope**               | Local/package scanning              | Global, framework-level auto-configuration           |
| **Manual vs Automatic** | Manual package selection            | Automatic configuration                              |
| **Typical Use**         | Custom package scanning             | Enable Spring Boot starters and auto beans           |
| **Part of**             | `@SpringBootApplication`            | `@SpringBootApplication`                             |

---

💡 **Interview Tip:**

> "`@ComponentScan` tells Spring where to look for beans, while `@EnableAutoConfiguration` automatically configures beans based on dependencies and classpath. `@SpringBootApplication` combines both plus `@Configuration`."

---

I can next explain **how `@EnableAutoConfiguration` chooses which beans to configure and how to override them**, which is a common Spring Boot interview question.

Do you want me to cover that?

---

## 124. @Configuration vs @Bean

### **`@Configuration` vs `@Bean` in Spring**

Both annotations are part of **Spring’s Java-based configuration**, but they serve **different purposes** in defining and managing beans.

---

## **1. `@Configuration`**

* **Definition:** Marks a class as a **configuration class**, similar to an XML configuration file.
* **Purpose:** Tells Spring that this class contains **bean definitions**.
* **Behavior:**

  * Beans defined inside a `@Configuration` class are **singletons by default**.
  * Spring ensures **CGLIB proxying** so that multiple `@Bean` method calls return the **same instance**.

**Example:**

```java
@Configuration
public class AppConfig {

    @Bean
    public UserService userService() {
        return new UserService(userRepository());
    }

    @Bean
    public UserRepository userRepository() {
        return new UserRepository();
    }
}
```

* `AppConfig` acts like a **Spring XML config file**, but in Java.
* All beans are **managed by Spring container**.

---

## **2. `@Bean`**

* **Definition:** Marks a **method inside a configuration class** as a **bean producer**.
* **Purpose:** Defines a single bean that Spring will manage.
* Can also be used in `@Component`-scanned classes, but typically used inside `@Configuration`.

**Example:**

```java
@Bean
public DataSource dataSource() {
    return new HikariDataSource();
}
```

* Spring calls this method once and **registers the returned object as a bean**.

---

## **3. Key Differences**

| Feature                 | @Configuration                                             | @Bean                                                                                         |
| ----------------------- | ---------------------------------------------------------- | --------------------------------------------------------------------------------------------- |
| **Applied On**          | Class                                                      | Method                                                                                        |
| **Purpose**             | Marks class as a configuration source                      | Defines a single bean                                                                         |
| **Singleton Guarantee** | Yes, Spring ensures singleton through CGLIB proxy          | Only if method is in `@Configuration` class; otherwise, new instance may be created each call |
| **Similar to XML?**     | Yes, class replaces XML config                             | Yes, method replaces `<bean>` element                                                         |
| **Example Use**         | `@Configuration` class containing multiple `@Bean` methods | Each `@Bean` defines a specific bean                                                          |

---

## **4. Important Notes**

1. Without `@Configuration` (just a plain class with `@Bean` methods):

   * Spring **does not proxy the class**, so calling one `@Bean` method from another **creates a new instance** each time.

```java
public class AppConfigWithoutConfig {
    @Bean
    public A a() {
        return new A(b());
    }

    @Bean
    public B b() {
        return new B();
    }
}
```

* Calling `a()` creates a **new B** instead of reusing the singleton.

2. With `@Configuration`, Spring ensures **singleton beans** even if one `@Bean` method calls another.

---

💡 **Interview Tip:**

> "`@Configuration` marks a class as a configuration source and ensures singleton beans through proxying. `@Bean` defines a single bean inside a configuration class. Without `@Configuration`, calling `@Bean` methods may create multiple instances."

---

I can next explain **`@Component` vs `@Configuration` vs `@Bean`**, which is a common Spring Boot interview scenario.

Do you want me to cover that?

---

## 125. @Async vs @Scheduled

### **`@Async` vs `@Scheduled` in Spring**

Both annotations are used for **asynchronous or background processing**, but they serve **different purposes** and work differently.

---

## **1. `@Async`**

* **Definition:** Indicates that a **method should run asynchronously** in a **separate thread**.
* **Purpose:** Execute tasks **without blocking** the caller thread.
* **Requires:** `@EnableAsync` on a configuration class.

**Example:**

```java
@Configuration
@EnableAsync
public class AsyncConfig { }

@Service
public class EmailService {

    @Async
    public void sendEmail(String recipient) {
        // Simulate long-running email task
        System.out.println("Sending email to " + recipient);
    }
}
```

**Usage:**

```java
emailService.sendEmail("user@example.com"); // Returns immediately, task runs asynchronously
```

* **Return Type:** Can return `void`, `Future`, `CompletableFuture`, or `ListenableFuture`.
* **Use Case:** Background tasks triggered by events, non-blocking operations, parallel processing.

---

## **2. `@Scheduled`**

* **Definition:** Schedules a method to run **at fixed intervals** or according to a **cron expression**.
* **Purpose:** Execute **periodic tasks** automatically.
* **Requires:** `@EnableScheduling` on a configuration class.

**Example:**

```java
@Configuration
@EnableScheduling
public class ScheduleConfig { }

@Service
public class ReportService {

    @Scheduled(fixedRate = 5000)
    public void generateReport() {
        System.out.println("Generating report every 5 seconds");
    }

    @Scheduled(cron = "0 0 12 * * ?")
    public void generateDailyReport() {
        System.out.println("Generating daily report at noon");
    }
}
```

* **Use Case:** Scheduled maintenance, automated reports, polling, cron jobs.

---

## **3. Key Differences**

| Feature                  | @Async                                         | @Scheduled                                     |
| ------------------------ | ---------------------------------------------- | ---------------------------------------------- |
| **Purpose**              | Run method asynchronously in a separate thread | Run method at fixed intervals or cron schedule |
| **Execution**            | Triggered by method call                       | Triggered automatically by scheduler           |
| **Configuration Needed** | `@EnableAsync`                                 | `@EnableScheduling`                            |
| **Return Type**          | `void`, `Future`, `CompletableFuture`          | `void`                                         |
| **Use Case**             | Non-blocking tasks, background processing      | Periodic or scheduled tasks                    |

---

## **4. Summary**

* **`@Async`** → Runs **asynchronously on demand**.
* **`@Scheduled`** → Runs **automatically on a schedule**.
* They can also be **combined**, e.g., a scheduled method that executes asynchronously.

---

💡 **Interview Tip:**

> "`@Async` is for executing tasks asynchronously without blocking the caller. `@Scheduled` is for running tasks periodically or at specific times. `@Scheduled` can optionally use `@Async` if you want the scheduled task to run in a separate thread."

---

I can next explain **ThreadPool configuration for @Async and @Scheduled**, which is often asked in Spring Boot interviews.

Do you want me to cover that?

---

## 126. @Cachable vs @CacheEvict

### **`@Cacheable` vs `@CacheEvict` in Spring**

Both annotations are part of **Spring’s caching abstraction** (`spring-boot-starter-cache`) and are used to **improve performance** by storing/retrieving data from a cache.

---

## **1. `@Cacheable`**

* **Definition:** Marks a method **whose result should be cached**.
* **Purpose:** Avoids repeated execution of **expensive or frequent methods**.
* **Behavior:**

  * When the method is called, Spring checks the cache first.
  * If a cached value exists, it is returned **without executing the method**.
  * If no value exists, the method executes, and the result is stored in the cache.

**Example:**

```java
@Service
public class UserService {

    @Cacheable(value = "users", key = "#userId")
    public User getUserById(int userId) {
        System.out.println("Fetching user from DB for ID: " + userId);
        return userRepository.findById(userId).orElse(null);
    }
}
```

* **First call:** Executes method and caches result.
* **Subsequent calls:** Returns cached result directly.

---

## **2. `@CacheEvict`**

* **Definition:** Marks a method to **remove one or more entries from the cache**.
* **Purpose:** Ensures cache **stays consistent** after updates, deletes, or changes.
* **Behavior:**

  * Can evict a single entry using a key.
  * Can evict all entries using `allEntries = true`.
  * Can be executed **before** or **after** method execution using `beforeInvocation`.

**Example:**

```java
@Service
public class UserService {

    @CacheEvict(value = "users", key = "#user.id")
    public void updateUser(User user) {
        userRepository.save(user);
        System.out.println("Updated user and evicted cache");
    }

    @CacheEvict(value = "users", allEntries = true)
    public void deleteAllUsers() {
        userRepository.deleteAll();
        System.out.println("Deleted all users and cleared cache");
    }
}
```

* Keeps cache **synchronized with database changes**.

---

## **3. Key Differences**

| Feature           | @Cacheable                              | @CacheEvict                                           |
| ----------------- | --------------------------------------- | ----------------------------------------------------- |
| **Purpose**       | Store method result in cache            | Remove method result from cache                       |
| **When Executed** | Before method call (checks cache first) | After or before method call (removes entry)           |
| **Use Case**      | Read-heavy operations                   | Write/delete operations to maintain cache consistency |
| **Key Attribute** | `key`                                   | `key`, `allEntries`, `beforeInvocation`               |
| **Behavior**      | Avoids method execution if cached       | Always executes method but updates cache              |

---

## **4. Summary**

* **`@Cacheable`** → Speeds up **read operations** by caching results.
* **`@CacheEvict`** → Keeps cache **consistent after write/update/delete operations**.

---

💡 **Interview Tip:**

> "`@Cacheable` caches the method result to improve performance. `@CacheEvict` removes entries from the cache to maintain consistency. Use them together in read-write scenarios."

---

I can next explain **`@CachePut` vs `@Cacheable`**, which is often asked in caching-related interviews.

Do you want me to cover that?

---