# LEVEL 1: BEGINNER (0-2 Years Experience)

# Spring Boot Basics

# Core Concepts

## 42. What is Spring Boot?

### **42. What is Spring Boot?**

**Spring Boot** is a **framework built on top of the Spring framework** that simplifies the development of **standalone, production-ready Spring applications**. It provides a set of tools and conventions to make Spring development **faster, easier, and less boilerplate-heavy**.

---

### **🔹 1. Key Features of Spring Boot**

| Feature                      | Description                                                                                                                              |
| ---------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------- |
| **Auto-Configuration**       | Automatically configures Spring applications based on the **dependencies** added in the project (no need for complex XML configuration). |
| **Standalone Applications**  | Can create **executable JARs** or WARs with an **embedded server** (like Tomcat, Jetty).                                                 |
| **Opinionated Defaults**     | Provides **default configurations** to speed up development while still allowing customization.                                          |
| **Starter Dependencies**     | Simplifies dependency management using **Spring Boot Starters** (e.g., `spring-boot-starter-web`, `spring-boot-starter-data-jpa`).       |
| **Embedded Server Support**  | Includes **Tomcat/Jetty/Undertow** embedded, so no external server setup is needed.                                                      |
| **Actuator**                 | Provides **production-ready features** like health checks, metrics, and monitoring.                                                      |
| **Minimal Boilerplate Code** | Reduces the need for XML configuration and repetitive setup code.                                                                        |
| **Spring CLI Support**       | Enables **rapid application prototyping** using command-line interface.                                                                  |

---

### **🔹 2. Advantages of Spring Boot**

1. **Faster Development** – Less boilerplate and auto-configured defaults.
2. **Standalone Applications** – Embedded servers allow running apps with a single JAR.
3. **Easy Testing** – Integration with Spring Test, JUnit, and Mockito.
4. **Production Ready** – Actuator, metrics, and monitoring built-in.
5. **Wide Community Support** – Large ecosystem and active community.

---

### **🔹 3. How Spring Boot Works**

1. You add **Spring Boot Starters** in `pom.xml` or `build.gradle`.
2. Spring Boot **auto-detects dependencies** and configures beans.
3. You write **minimal code**, typically just `@SpringBootApplication` on the main class.
4. Spring Boot runs the application using an **embedded server** or generates a deployable WAR.

---

### **🔹 4. Example: Simple Spring Boot Application**

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@SpringBootApplication
public class MySpringBootApp {
    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApp.class, args);
    }
}

@RestController
class HelloController {
    @GetMapping("/hello")
    public String sayHello() {
        return "Hello, Spring Boot!";
    }
}
```

* Run as **Java Application** → Embedded Tomcat starts → Access `http://localhost:8080/hello`.
* Minimal setup with **no XML configuration**.

---

### **🔹 5. Spring Boot vs Spring Framework**

| Feature               | Spring Framework                         | Spring Boot                                         |
| --------------------- | ---------------------------------------- | --------------------------------------------------- |
| **Configuration**     | Requires manual XML or Java-based config | Auto-configuration & starter dependencies           |
| **Server**            | External server required                 | Embedded server (Tomcat/Jetty/Undertow)             |
| **Development Speed** | Slower due to boilerplate                | Faster, less boilerplate                            |
| **Starter Projects**  | Not available                            | Spring Boot Starters simplify dependency management |

---

💡 **Interview Tip:**

> "Spring Boot simplifies Spring development by **reducing boilerplate code**, providing **auto-configuration**, and supporting **standalone, production-ready applications**."

---

If you want, I can next explain **Spring Boot Starters, Auto-Configuration, and Spring Boot Actuator**, which are commonly asked follow-up questions in interviews.

Do you want me to cover that next?

---

## 43. What are advantages of Spring Boot?

### **43. Advantages of Spring Boot**

Spring Boot is widely used because it simplifies Spring application development and provides production-ready features. Here are the main advantages:

---

### **🔹 1. **Faster Development**

* **Minimal boilerplate code** required.
* No need for lengthy XML configuration files.
* With **Spring Boot Starters**, developers can quickly add dependencies for web, database, security, etc.

**Example:** `spring-boot-starter-web` automatically configures Spring MVC, Tomcat, and Jackson for JSON support.

---

### **🔹 2. **Standalone Applications**

* Spring Boot applications can run as **executable JARs/WARs**.
* Comes with **embedded servers** like **Tomcat, Jetty, or Undertow**.
* No need to deploy on an external application server.

---

### **🔹 3. **Auto-Configuration**

* Spring Boot **automatically configures beans** based on the dependencies present in the classpath.
* Reduces manual setup and speeds up development.

**Example:** If `spring-boot-starter-data-jpa` is included, it automatically configures `EntityManagerFactory` and `DataSource`.

---

### **🔹 4. **Opinionated Defaults**

* Provides **sensible default configurations** to make applications work out-of-the-box.
* Developers can override defaults if required.

---

### **🔹 5. **Production-Ready Features**

* **Spring Boot Actuator** provides metrics, health checks, and monitoring endpoints.
* Easily integrate with **logging, metrics, and external monitoring systems**.

---

### **🔹 6. **Easy Testing**

* Built-in support for **JUnit, Mockito, and Spring Test**.
* Embedded server allows **integration testing** without deploying the app externally.

---

### **🔹 7. **Microservices Ready**

* Ideal for **microservice architectures**.
* Works well with **Spring Cloud** for service discovery, configuration management, and load balancing.

---

### **🔹 8. **Wide Community Support**

* Large community and active development.
* Many **starter projects and third-party integrations** are available.

---

### **🔹 9. **Reduced Configuration Overhead**

* Handles **database connection, transaction management, and MVC setup** automatically.
* Developers focus on **business logic instead of boilerplate code**.

---

### **🔹 10. **Seamless Dependency Management**

* **Starters** simplify adding commonly used dependencies.
* Example: `spring-boot-starter-web`, `spring-boot-starter-data-jpa`, `spring-boot-starter-security`.

---

💡 **Interview Tip:**

> "Spring Boot reduces boilerplate code, provides **auto-configuration**, supports **standalone applications**, and includes **production-ready features**, making it ideal for fast and scalable development."

---

If you want, I can next explain **Spring Boot Starters, Auto-Configuration, and Spring Boot Actuator**, which are also common follow-up interview topics.

Do you want me to cover that next?

---

## 44. What is @SpringBootApplication annotation?

### **44. What is `@SpringBootApplication` Annotation in Spring Boot**

The `@SpringBootApplication` annotation is a **convenience annotation** that combines three commonly used annotations in Spring:

---

### **🔹 1. Annotations Included**

1. **`@SpringBootConfiguration`**

   * Indicates that this class provides **Spring Boot application configuration**.
   * It is itself a specialization of `@Configuration`.

2. **`@EnableAutoConfiguration`**

   * Enables **Spring Boot’s auto-configuration feature**.
   * Automatically configures Spring beans based on the **dependencies in the classpath**.

3. **`@ComponentScan`**

   * Enables **component scanning** so that Spring can detect `@Component`, `@Service`, `@Repository`, and `@Controller` annotations in the specified package and its sub-packages.

---

### **🔹 2. Example**

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class MySpringBootApp {

    public static void main(String[] args) {
        SpringApplication.run(MySpringBootApp.class, args);
    }
}
```

* This single annotation replaces the need to explicitly write:

```java
@Configuration
@EnableAutoConfiguration
@ComponentScan
```

* Spring Boot will **scan the package of this class and its sub-packages** for Spring components.

---

### **🔹 3. Key Points**

1. Usually placed on the **main application class**.
2. Should be in the **root package** so that `@ComponentScan` can scan all sub-packages automatically.
3. **Auto-configuration** is triggered by `@EnableAutoConfiguration`.
4. Makes Spring Boot applications **ready to run** with minimal setup.

---

### **🔹 4. Breakdown**

| Included Annotation        | Purpose                                              |
| -------------------------- | ---------------------------------------------------- |
| `@SpringBootConfiguration` | Marks class as configuration                         |
| `@EnableAutoConfiguration` | Enables Spring Boot to configure beans automatically |
| `@ComponentScan`           | Scans packages for Spring components                 |

---

💡 **Interview Tip:**

> "`@SpringBootApplication` is a **convenience annotation** combining configuration, component scanning, and auto-configuration. It is the entry point for a Spring Boot application."

---

If you want, I can next explain **Spring Boot Starters and their importance**, which is often asked right after `@SpringBootApplication`.

Do you want me to cover that next?

---

## 45. What is the difference between @Component, @Service, and @Repository?

### **45. Difference Between `@Component`, `@Service`, and `@Repository` in Spring**

All three annotations are **stereotype annotations** in Spring used to **define beans** that Spring will manage, but they have **different semantic roles**.

---

### **🔹 1. `@Component`**

* **Definition:** Generic stereotype annotation to mark a class as a **Spring-managed component**.
* **Purpose:** For any **general-purpose bean**.
* **Example Use:** Utility classes, helper classes.

```java
import org.springframework.stereotype.Component;

@Component
public class MyComponent {
    public void show() {
        System.out.println("Hello from Component");
    }
}
```

---

### **🔹 2. `@Service`**

* **Definition:** Specialization of `@Component` used for **service layer beans**.
* **Purpose:** To indicate that this class holds **business logic**.
* **Benefit:** Improves **clarity and readability** of your code; helps tools/frameworks detect business services.

```java
import org.springframework.stereotype.Service;

@Service
public class UserService {
    public String getUserName() {
        return "Aditya";
    }
}
```

---

### **🔹 3. `@Repository`**

* **Definition:** Specialization of `@Component` used for **data access layer beans**.
* **Purpose:** Indicates that the class interacts with **databases**.
* **Benefit:**

  1. Automatically translates **database exceptions into Spring’s `DataAccessException`**.
  2. Makes your **DAO layer more meaningful**.

```java
import org.springframework.stereotype.Repository;

@Repository
public class UserRepository {
    public void saveUser(String name) {
        // Database save operation
    }
}
```

---

### **🔹 4. Key Differences**

| Annotation    | Purpose / Layer                | Special Features                                                       |
| ------------- | ------------------------------ | ---------------------------------------------------------------------- |
| `@Component`  | Generic bean                   | Base annotation; no extra semantics                                    |
| `@Service`    | Service layer / Business logic | Semantic clarity for services; no special behavior beyond `@Component` |
| `@Repository` | DAO layer / Database access    | Exception translation (SQL → Spring `DataAccessException`)             |

---

### **🔹 5. Hierarchy**

```
@Component
 ├─ @Repository  (DAO layer)
 ├─ @Service     (Service layer)
 └─ @Controller  (Presentation layer)
```

> All are detected via **component scanning** and registered as **Spring Beans**.

---

💡 **Interview Tip:**

> "`@Component` is generic, `@Service` is for business logic, and `@Repository` is for database operations with exception translation."

---

If you want, I can next explain **Difference between `@Controller`, `@RestController`, and `@RequestMapping` in Spring Boot**, which is often asked in interviews.

Do you want me to cover that next?

---

## 46. What is dependency injection?

### **46. What is Dependency Injection (DI) in Java / Spring**

**Dependency Injection (DI)** is a **design pattern** used to achieve **Inversion of Control (IoC)**, where the **control of object creation and dependency management** is transferred from the class itself to an **external framework or container** (like Spring).

In simple terms:

> Instead of a class creating its dependencies, **they are injected from outside**, usually by the Spring container.

---

### **🔹 1. Benefits of Dependency Injection**

1. **Loose Coupling** – Classes depend on **interfaces** rather than concrete implementations.
2. **Easier Testing** – Dependencies can be **mocked or stubbed** in unit tests.
3. **Maintainability** – Changing a dependency doesn’t require changing the dependent class.
4. **Reusable Components** – Same dependency can be shared across multiple classes.

---

### **🔹 2. Types of Dependency Injection**

| Type                      | Description                                             | Example in Spring                                             |
| ------------------------- | ------------------------------------------------------- | ------------------------------------------------------------- |
| **Constructor Injection** | Dependencies are provided via **constructor arguments** | `@Autowired public UserService(UserRepository repo) { ... }`  |
| **Setter Injection**      | Dependencies are provided via **setter methods**        | `@Autowired public void setRepo(UserRepository repo) { ... }` |
| **Field Injection**       | Dependencies are directly injected into **fields**      | `@Autowired private UserRepository repo;`                     |

> Constructor injection is generally preferred for **mandatory dependencies**.
> Setter/field injection can be used for **optional dependencies**.

---

### **🔹 3. Example in Spring**

#### **Step 1: Dependency Class**

```java
import org.springframework.stereotype.Repository;

@Repository
public class UserRepository {
    public String getUserName() {
        return "Aditya";
    }
}
```

#### **Step 2: Dependent Class (Service)**

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {
    private final UserRepository userRepository;

    // Constructor Injection
    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public void printUserName() {
        System.out.println(userRepository.getUserName());
    }
}
```

#### **Step 3: Main Application**

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.context.ApplicationContext;

@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        ApplicationContext context = SpringApplication.run(MyApp.class, args);
        UserService service = context.getBean(UserService.class);
        service.printUserName();
    }
}
```

**Output:**

```
Aditya
```

* Spring automatically **injects `UserRepository` into `UserService`**.
* No need to create `UserRepository` manually (`new` keyword not used).

---

### **🔹 4. How DI Works in Spring**

1. Spring container **manages beans** annotated with `@Component`, `@Service`, `@Repository`, etc.
2. When a bean requires another bean, Spring **injects it automatically** using `@Autowired`.
3. Dependencies can also be injected using **Java configuration (`@Bean`)** or **XML configuration**.

---

### **🔹 5. Advantages Over Manual Instantiation**

| Feature     | Manual Instantiation     | Dependency Injection               |
| ----------- | ------------------------ | ---------------------------------- |
| Coupling    | Tight                    | Loose                              |
| Testing     | Hard (difficult to mock) | Easy (mock dependencies)           |
| Flexibility | Low                      | High (swap implementations easily) |
| Reusability | Limited                  | High                               |

---

💡 **Interview Tip:**

> "Dependency Injection allows Spring to **manage dependencies**, reduces **tight coupling**, and makes applications **testable and maintainable**. Use `@Autowired` for injection."

---

If you want, I can next explain **Difference between Constructor, Setter, and Field Injection in Spring**, which is a commonly asked follow-up to DI.

Do you want me to cover that next?

---

## 47. What is @Autowired?

### **47. What is `@Autowired` in Spring**

**`@Autowired`** is a **Spring annotation** used for **automatic dependency injection**. It allows Spring to **resolve and inject collaborating beans into your class automatically**, without explicitly instantiating them using `new`.

---

### **🔹 1. Purpose**

* Reduces **manual bean creation**.
* Enables **Inversion of Control (IoC)**, letting Spring manage dependencies.
* Can be used with **constructor, setter, or field injection**.

---

### **🔹 2. How It Works**

1. Spring **scans beans** (annotated with `@Component`, `@Service`, `@Repository`, etc.).
2. When it finds a dependency annotated with `@Autowired`, it **injects the appropriate bean** automatically.
3. By default, Spring injects beans **by type**.

---

### **🔹 3. Example Usage**

#### **Field Injection**

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class UserService {

    @Autowired
    private UserRepository userRepository; // Injected automatically

    public void printUserName() {
        System.out.println(userRepository.getUserName());
    }
}
```

---

#### **Setter Injection**

```java
@Service
public class UserService {
    private UserRepository userRepository;

    @Autowired
    public void setUserRepository(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
}
```

---

#### **Constructor Injection**

```java
@Service
public class UserService {
    private final UserRepository userRepository;

    @Autowired
    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }
}
```

> **Constructor injection** is recommended for **mandatory dependencies** because it ensures the dependency is **not null**.

---

### **🔹 4. Key Points**

1. Can be applied to:

   * Fields
   * Setter methods
   * Constructors

2. Spring resolves dependencies **by type**.

3. If multiple beans of the same type exist, use `@Qualifier` to **specify which bean to inject**.

```java
@Autowired
@Qualifier("specialUserRepository")
private UserRepository userRepository;
```

4. Optional injection can be done using `required=false`:

```java
@Autowired(required = false)
private UserRepository userRepository;
```

---

### **🔹 5. Advantages**

* Reduces **boilerplate code**.
* Promotes **loose coupling**.
* Makes the application **more maintainable and testable**.
* Works seamlessly with **Spring Boot auto-configuration**.

---

💡 **Interview Tip:**

> "`@Autowired` tells Spring to automatically **inject dependencies** into a bean. It can be used on constructors, setters, or fields, and helps achieve **IoC and DI**."

---

If you want, I can next explain **Difference Between @Component, @Service, @Repository, and @Controller in Spring**, which is a commonly asked interview question.

Do you want me to cover that next?

---

## 48. What are Spring Boot Starters?

### **48. What are Spring Boot Starters?**

**Spring Boot Starters** are a set of **convenient dependency descriptors** (Maven or Gradle) that **bundle commonly used libraries** together for a specific functionality, so you **don’t have to search and add dependencies manually**.

---

### **🔹 1. Purpose**

* Simplifies **dependency management**.
* Provides a **ready-to-use setup** for common Spring features.
* Reduces **manual configuration and boilerplate**.

> Example: Instead of manually adding Spring MVC, Jackson, and Tomcat dependencies for a web application, you just add `spring-boot-starter-web`.

---

### **🔹 2. Common Spring Boot Starters**

| Starter                            | Description                                                                                         |
| ---------------------------------- | --------------------------------------------------------------------------------------------------- |
| **spring-boot-starter-web**        | For building **RESTful web services** with Spring MVC, embedded Tomcat, and JSON support (Jackson). |
| **spring-boot-starter-data-jpa**   | For **Spring Data JPA** and database integration (Hibernate, JPA).                                  |
| **spring-boot-starter-security**   | Adds **Spring Security** dependencies for authentication and authorization.                         |
| **spring-boot-starter-test**       | For **unit and integration testing** (JUnit, Mockito, Hamcrest).                                    |
| **spring-boot-starter-actuator**   | Adds **production-ready features** like health checks, metrics, and monitoring.                     |
| **spring-boot-starter-thymeleaf**  | Adds **Thymeleaf template engine** support for web applications.                                    |
| **spring-boot-starter-validation** | Adds **Bean Validation (Hibernate Validator)** support.                                             |

---

### **🔹 3. Example in Maven**

```xml
<dependencies>
    <!-- Starter for web applications -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <!-- Starter for JPA and database -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
</dependencies>
```

* Spring Boot automatically includes all **transitive dependencies** required for these starters.

---

### **🔹 4. Advantages of Using Starters**

1. **Simplifies Dependency Management** – No need to manually include multiple libraries.
2. **Reduces Configuration** – Auto-configures the framework based on the starter.
3. **Faster Development** – Quickly set up new features like web, security, or JPA.
4. **Consistent Versions** – Avoids version conflicts since starters manage compatible library versions.

---

### **🔹 5. How It Works**

1. You add a starter dependency in **Maven or Gradle**.
2. Spring Boot **auto-detects the included libraries**.
3. Auto-configuration (`@EnableAutoConfiguration`) sets up the beans and configurations automatically.

---

💡 **Interview Tip:**

> "Spring Boot Starters are **predefined dependency bundles** that make it easier to add functionality like web, JPA, or security without manually managing each library. They speed up development and reduce boilerplate code."

---

If you want, I can next explain **Spring Boot Auto-Configuration and how it works**, which is often asked right after Starters.

Do you want me to cover that next?

---

## 49. What is application.properties file?

### **49. What is `application.properties` in Spring Boot**

In Spring Boot, **`application.properties`** (or `application.yml`) is a **configuration file** used to define **application-level settings** such as database connection, server port, logging levels, and other properties.

It allows you to **externalize configuration** so your code remains **environment-independent** and easy to maintain.

---

### **🔹 1. Location**

* Usually placed under:

```
src/main/resources/application.properties
```

* Spring Boot automatically loads this file at startup.

---

### **🔹 2. Purpose**

* Externalize configuration from the code.
* Easily **switch environments** (development, testing, production) by using different property files.
* Simplify **application settings management**.

---

### **🔹 3. Common Use Cases**

| Property                                                 | Description                                                                       |
| -------------------------------------------------------- | --------------------------------------------------------------------------------- |
| `server.port=8081`                                       | Changes the **embedded server port**. Default is 8080.                            |
| `spring.datasource.url=jdbc:mysql://localhost:3306/mydb` | Database connection URL.                                                          |
| `spring.datasource.username=root`                        | Database username.                                                                |
| `spring.datasource.password=root`                        | Database password.                                                                |
| `spring.jpa.hibernate.ddl-auto=update`                   | Hibernate schema generation strategy (`none`, `update`, `create`, `create-drop`). |
| `logging.level.org.springframework=DEBUG`                | Sets logging level for specific packages.                                         |
| `spring.profiles.active=dev`                             | Activates specific **Spring profile**.                                            |

---

### **🔹 4. Example `application.properties`**

```properties
# Server configuration
server.port=8081

# Datasource configuration
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=root
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA / Hibernate
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

# Logging
logging.level.org.springframework=INFO

# Custom property
app.name=MySpringBootApp
```

---

### **🔹 5. Accessing Properties in Code**

You can access properties using `@Value` or `@ConfigurationProperties`.

#### **Example using `@Value`**

```java
import org.springframework.beans.factory.annotation.Value;
import org.springframework.stereotype.Component;

@Component
public class AppConfig {

    @Value("${app.name}")
    private String appName;

    public void printAppName() {
        System.out.println("Application Name: " + appName);
    }
}
```

#### **Example using `@ConfigurationProperties`**

```java
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.stereotype.Component;

@Component
@ConfigurationProperties(prefix = "app")
public class AppProperties {
    private String name;

    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
}
```

---

### **🔹 6. Advantages**

1. **Externalized Configuration** – Easily modify without changing code.
2. **Environment-Specific** – Supports multiple profiles (`application-dev.properties`, `application-prod.properties`).
3. **Centralized Settings** – Keeps all important configurations in one place.
4. **Supports Strong Typing** – When using `@ConfigurationProperties`.

---

💡 **Interview Tip:**

> "`application.properties` is used to define externalized configuration for Spring Boot apps, such as server settings, database configs, and custom properties, making apps environment-independent and easy to maintain."

---

If you want, I can next explain **Difference between `application.properties` and `application.yml` in Spring Boot**, which is also commonly asked.

Do you want me to cover that next?

---

## 50. Difference between Spring and Spring Boot?

### **50. Difference Between Spring and Spring Boot**

Spring and Spring Boot are related but serve **different purposes**. Spring is a **comprehensive framework**, while Spring Boot is a **toolset built on top of Spring** for easier and faster application development.

---

### **🔹 1. Overview**

| Feature                  | **Spring Framework**                                                          | **Spring Boot**                                                                                                |
| ------------------------ | ----------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------- |
| **Definition**           | A comprehensive **Java application framework** for building enterprise apps.  | A **convention-over-configuration framework** on top of Spring that simplifies Spring application development. |
| **Configuration**        | Requires **manual XML or Java-based configuration**.                          | Provides **auto-configuration** to reduce boilerplate code.                                                    |
| **Setup Complexity**     | Complex setup; developer must configure dependencies, server, and frameworks. | Simple setup; uses **starters** and embedded servers.                                                          |
| **Embedded Server**      | Requires **external server** like Tomcat or Jetty.                            | Supports **embedded servers** (Tomcat, Jetty, Undertow).                                                       |
| **Development Speed**    | Slower; more boilerplate.                                                     | Faster; minimal code and setup.                                                                                |
| **Opinionated Defaults** | Not opinionated; fully configurable.                                          | Opinionated defaults; works out-of-the-box.                                                                    |
| **Dependencies**         | Developers must manage **all dependencies manually**.                         | Uses **Spring Boot Starters** to manage dependencies automatically.                                            |
| **Use Case**             | Full-scale enterprise applications with customized configuration.             | Quick development of **microservices, REST APIs, or standalone apps**.                                         |

---

### **🔹 2. Key Features Comparison**

| Feature                        | Spring          | Spring Boot                                                     |
| ------------------------------ | --------------- | --------------------------------------------------------------- |
| **Auto-Configuration**         | ❌ Not available | ✅ Available                                                     |
| **Embedded Server**            | ❌ No            | ✅ Yes                                                           |
| **Starter Projects**           | ❌ No            | ✅ Yes                                                           |
| **Externalized Configuration** | ❌ Partial       | ✅ Full support via `application.properties` / `application.yml` |
| **Default Settings**           | ❌ None          | ✅ Sensible defaults                                             |
| **Command-Line Support**       | ❌ No            | ✅ Yes (Spring Boot CLI)                                         |
| **Actuator for Monitoring**    | ❌ No            | ✅ Yes (health, metrics, logging)                                |

---

### **🔹 3. When to Use Which**

* **Spring Framework:**

  * Full enterprise applications requiring **custom configuration**.
  * Legacy applications already built on Spring.
  * Applications needing **fine-grained control** over all configurations.

* **Spring Boot:**

  * **Rapid development** of REST APIs, microservices, or standalone apps.
  * When **minimal configuration and faster setup** are desired.
  * Projects that benefit from **embedded server and auto-configuration**.

---

### **🔹 4. Example**

**Spring Framework:**

```java
// Need to configure DispatcherServlet in web.xml or Java config
```

**Spring Boot:**

```java
@SpringBootApplication
public class MyApp {
    public static void main(String[] args) {
        SpringApplication.run(MyApp.class, args); // Runs with embedded Tomcat
    }
}
```

* Spring Boot reduces **configuration overhead** and lets you run a Spring application **with a single main class**.

---

💡 **Interview Tip:**

> "Spring is a full-featured framework requiring manual configuration, while Spring Boot is built on Spring to enable **auto-configuration, embedded servers, and rapid development** for modern applications."

---

If you want, I can next explain **Spring Boot Auto-Configuration and how it works**, which is often asked after Spring Boot basics.

Do you want me to cover that next?

---

## 51. What is IOC comtainer in Spring?

### **51. What is IoC Container in Spring**

**IoC (Inversion of Control) Container** is the **core of the Spring Framework**. It is responsible for **creating, managing, and wiring Spring beans** and **injecting dependencies** automatically.

> In simple terms: The IoC container **controls the instantiation and lifecycle of objects** instead of the application code doing it manually.

---

### **🔹 1. Key Concepts**

1. **Inversion of Control (IoC):**

   * Objects **do not create or manage their dependencies** themselves.
   * The control of **object creation and dependency management** is transferred to the Spring container.

2. **Dependency Injection (DI):**

   * DI is a **technique used by IoC** to inject dependencies into beans.
   * Can be **constructor-based**, **setter-based**, or **field-based**.

3. **Bean:**

   * An object **managed by the Spring container** is called a **bean**.
   * Beans are usually annotated with `@Component`, `@Service`, `@Repository`, or defined in XML/Java config.

---

### **🔹 2. Types of IoC Containers in Spring**

| Container              | Description                                                                                                                    | When to Use                                                  |
| ---------------------- | ------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------ |
| **BeanFactory**        | Basic IoC container that provides **lazy initialization**.                                                                     | Lightweight applications where minimal resources are needed. |
| **ApplicationContext** | Advanced container built on BeanFactory. Provides **eager initialization, internationalization, event propagation, and more**. | Most Spring applications; recommended over BeanFactory.      |

**Common ApplicationContext Implementations:**

* `ClassPathXmlApplicationContext` – loads context from XML in classpath.
* `FileSystemXmlApplicationContext` – loads context from XML in filesystem.
* `AnnotationConfigApplicationContext` – loads context from Java-based configuration.
* `WebApplicationContext` – specialized for **web applications**.

---

### **🔹 3. How It Works**

1. Define beans in **XML, Java config, or annotations**.
2. Spring **reads the bean definitions** and **creates bean instances**.
3. Spring **injects dependencies** into the beans (DI).
4. The application **uses these beans** from the container instead of creating them manually.

---

### **🔹 4. Example using Annotation-based Configuration**

```java
import org.springframework.stereotype.Component;
import org.springframework.context.annotation.AnnotationConfigApplicationContext;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;

@Component
class Engine {
    public void start() {
        System.out.println("Engine started");
    }
}

@Component
class Car {
    private final Engine engine;

    public Car(Engine engine) {
        this.engine = engine; // Constructor injection
    }

    public void drive() {
        engine.start();
        System.out.println("Car is driving");
    }
}

@Configuration
@ComponentScan(basePackages = "com.example")
class AppConfig {}

public class MainApp {
    public static void main(String[] args) {
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
        Car car = context.getBean(Car.class);
        car.drive();
        context.close();
    }
}
```

**Output:**

```
Engine started
Car is driving
```

* Spring IoC container **creates `Engine` and `Car` beans** and injects `Engine` into `Car`.
* Application **does not use `new`**, demonstrating **Inversion of Control**.

---

### **🔹 5. Advantages of IoC Container**

1. **Loose Coupling** – Classes don’t create dependencies themselves.
2. **Reusability** – Beans can be reused across multiple classes.
3. **Ease of Testing** – Dependencies can be easily **mocked**.
4. **Centralized Configuration** – Spring container manages all beans.
5. **Flexibility** – Change implementations without modifying dependent classes.

---

💡 **Interview Tip:**

> "IoC Container manages **beans and their dependencies**, allowing **loose coupling, easier testing, and centralized configuration**. It’s the backbone of the Spring Framework."

---

If you want, I can next explain **Difference between BeanFactory and ApplicationContext in Spring**, which is a common interview question following IoC.

Do you want me to cover that next?

---