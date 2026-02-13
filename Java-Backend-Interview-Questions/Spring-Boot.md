## 201. What is Spring Boot?

**Answer:**
**Spring Boot** is an opinionated framework built on top of the Spring Framework.
*   **Goal:** To simplify the bootstrapping and development of new Spring applications.
*   **Key Features:**
    1.  **Auto-Configuration:** Automatically configures your application based on jar dependencies.
    2.  **Standalone:** Creates stand-alone Spring applications with embedded servers (Tomcat, Jetty).
    3.  **Opinionated:** Provides "Starter" dependencies to simplify build configuration.
    4.  **Production-ready:** Includes metrics, health checks, and externalized configuration.

---

## 202. What is auto-configuration?

**Answer:**
**Auto-configuration** attempts to automatically configure your Spring application based on the jar dependencies that you have added.
*   **Mechanism:** It uses `@EnableAutoConfiguration` (part of `@SpringBootApplication`).
*   **Example:** If `HSQLDB` is on your classpath, and you haven't manually configured any database connection beans, Spring Boot auto-configures an in-memory database.
*   **Debug:** Use `debug=true` in `application.properties` to see the **Positive matches** (applied configs) and **Negative matches** (skipped configs).

---

## 203. How does @SpringBootApplication work?

**Answer:**
`@SpringBootApplication` is a convenience annotation that combines three valid annotations:
1.  **@Configuration:** Allows Java-based configuration.
2.  **@EnableAutoConfiguration:** Enables Spring Boot's auto-configuration mechanism.
3.  **@ComponentScan:** Scans for components in the current package and its sub-packages.

---

## 204. What is starter dependency?

**Answer:**
**Starters** are a set of convenient dependency descriptors that you can include in your application.
*   **Benefit:** Instead of copying sample dependency code for 10 different libraries, you include one "starter".
*   **Example:** `spring-boot-starter-web` imports:
    *   Spring MVC
    *   Jackson (JSON)
    *   Tomcat (Embedded Server)
    *   Validation API

---

## 205. What is embedded server?

**Answer:**
An **Embedded Server** means the HTTP server (like Tomcat, Jetty, Undertow) is packaged **inside** your application JAR.
*   **Traditional:** You build a WAR file and deploy it into an external Tomcat server.
*   **Spring Boot:** You build an executable JAR. When you run `java -jar app.jar`, it starts the embedded Tomcat, which then hosts your application.
*   **Default:** Tomcat (Port 8080).

---

## 206. How to change server port?

**Answer:**
You can change the embedded server port in `application.properties` (or `application.yml`):
```properties
server.port=8081
```
Or via command line argument:
```bash
java -jar app.jar --server.port=8081
```

---

## 207. What is application.properties vs YAML?

**Answer:**
Both are used for external configuration.
*   **Properties:** Standard Java format (`key=value`), flat structure.
*   **YAML (.yml):** Hierarchical structure (indentation-based), more readable for complex configurations (lists, maps).
*   **Precedence:** If both exist, properties usually override YAML (implementation detail, but good to know).

---

## 208. What is profiles in Spring Boot?

**Answer:**
**Profiles** provide a way to segregate parts of your application configuration and make it be available only in certain environments.
*   **Usage:** `application-dev.properties`, `application-prod.properties`.
*   **Activation:**
    *   `spring.profiles.active=dev` in `application.properties`.
    *   `--spring.profiles.active=prod` command line argument.

---

## 209. What is actuator?

**Answer:**
**Spring Boot Actuator** adds production-ready features to your application to help you **monitor and manage** it.
*   **Endpoints:** Exposes HTTP (or JMX) endpoints to check health, metrics, environment, beans, etc.
*   **Dependency:** `spring-boot-starter-actuator`.

---

## 210. Important actuator endpoints?

**Answer:**
*   `/actuator/health`: Application health status (UP/DOWN).
*   `/actuator/info`: Arbitrary application info.
*   `/actuator/metrics`: JVM, CPU, Memory metrics.
*   `/actuator/loggers`: View and modify logging levels at runtime.
*   `/actuator/env`: Environment variables and properties.
*   `/actuator/beans`: List of all Spring beans.
*   `/actuator/threaddump`: Thread dump.
*   `/actuator/heapdump`: Heap dump.

---

## 211. What is Spring Boot DevTools?

**Answer:**
**Spring Boot DevTools** is a module that improves the development experience.
*   **Automatic Restart:** Automatically restarts the application when classes on the classpath change (faster than full cold start).
*   **LiveReload:** Triggers a browser refresh when resources change, provided the LiveReload browser extension is installed.
*   **Property Defaults:** Disables caching for templates (Thymeleaf/Freemarker) to see changes immediately.

---

## 212. What is CommandLineRunner?

**Answer:**
`CommandLineRunner` is a functional interface used to run code **once** after the Spring Boot application has started.
*   **Method:** `void run(String... args)`.
*   **Usage:** Database initialization, seeding data, or checking system integrity at startup.
*   **Alternative:** `ApplicationRunner` (Same purpose, but receives arguments as an `ApplicationArguments` object instead of raw String array).

---

## 213. What is @ConfigurationProperties?

**Answer:**
`@ConfigurationProperties` is used to bind external configuration properties (from `application.properties`) to a Java Bean.
*   **Type-safe:** Provides strongly typed configuration with validation.
*   **Structure:** Can map hierarchical data (lists, maps, nested objects).
*   **Usage:**
    ```java
    @ConfigurationProperties(prefix = "app.mail")
    @Component
    public class MailConfig {
        private String host;
        private int port;
        // getters/setters
    }
    ```

---

## 214. How to externalize configuration?

**Answer:**
Spring Boot lets you externalize configuration so you can work with the same code in different environments.
**Priority Order (High to Low):**
1.  Command line arguments (`--server.port=9000`).
2.  Java System properties (`-Dserver.port=9000`).
3.  OS Environment variables.
4.  `application-profile.properties` (outside jar).
5.  `application-profile.properties` (inside jar).
6.  `application.properties` (outside/inside jar).

---

## 215. What is logging configuration?

**Answer:**
Spring Boot uses **Commons Logging** for all internal logging but leaves the underlying log implementation open.
*   **Default:** **Logback**.
*   **Console Output:** Enabled by default.
*   **File Output:** Set `logging.file.name` or `logging.file.path`.
*   **Levels:** `logging.level.com.example=DEBUG`.
*   **Custom:** Add `logback-spring.xml` or `log4j2.xml` to the classpath for advanced control.

---

## 216. How to secure actuator endpoints?

**Answer:**
Since Actuator endpoints expose sensitive data, they should be secured using **Spring Security**.
1.  **Exclude Sensitivity:** By default, only `/health` and `/info` are exposed over HTTP.
2.  **Enable All:** `management.endpoints.web.exposure.include=*`.
3.  **Security Config:**
    ```java
    http.requestMatchers(EndpointRequest.toAnyEndpoint())
        .hasRole("ADMIN")
    ```

---

## 217. What is Spring Boot caching support?

**Answer:**
Spring Boot provides an abstraction for transparent caching.
*   **Enable:** `@EnableCaching`.
*   **Annotate:** `@Cacheable("users")` on methods.
*   **Providers:** Auto-configures providers like **Redis**, **Caffeine**, **EhCache**, or **Hazelcast** if they are on the classpath.
*   **Fallback:** Uses a `ConcurrentHashMap` if no provider is found.

---

## 218. What is Spring Boot CLI?

**Answer:**
**Spring Boot CLI** (Command Line Interface) is a command-line tool for prototyping with Spring.
*   **Groovy:** It allows running **Groovy** scripts that look like Java without boilerplate (no imports, no `public class`, no `main` method).
*   **Usage:** Swiftly testing code snippets or writing simple scripts.

---

## 219. What is custom auto-configuration?

**Answer:**
You can create your own starter libraries that auto-configure beans for other applications.
*   **Steps:**
    1.  Create a standard `@Configuration` class.
    2.  Use `@Conditional` annotations (`@ConditionalOnClass`, `@ConditionalOnMissingBean`) to define when configuration should apply.
    3.  Register the config class in `META-INF/spring.factories` (or `META-INF/spring/org.springframework.boot.autoconfigure.AutoConfiguration.imports` in newer versions).

---

## 220. How to create fat jar?

**Answer:**
A **Fat Jar** (or Uber Jar) contains the compiled application classes AND all dependency JARs.
*   **Plugin:** The **Spring Boot Maven Plugin** (or Gradle plugin) Repackages the standard jar.
*   **Command:** `mvn clean package`.
*   **Result:** A runnable jar file that can be executed via `java -jar application.jar` without needing an external classpath setup.

---

## 221. How to run Spring Boot app in production?

**Answer:**
1.  **Executable JAR:** `java -jar app.jar` (simplest).
2.  **Docker:** Create a Docker image and run it in a container orchestrator (Kubernetes).
3.  **Systemd Service:** Run as a Linux service (background process) managed by `systemd`.
4.  **WAR Deployment:** Deploy to an external Tomcat/Wildfly/WebLogic server (Legacy).

---

## 222. How to enable HTTPS?

**Answer:**
You need an SSL certificate (PKCS12 or JKS). Configure it in `application.properties`:
```properties
server.ssl.key-store=classpath:keystore.p12
server.ssl.key-store-password=changeit
server.ssl.key-store-type=PKCS12
server.ssl.key-alias=tomcat
server.port=8443
```

---

## 223. How to configure multiple datasources?

**Answer:**
1.  **Properties:** Define two sets of properties (e.g., `app.datasource.primary`, `app.datasource.secondary`).
2.  **Beans:** Create two `DataSource` beans. Mark one as `@Primary`.
3.  ** EntityManager:** If using JPA, you also need to configure two `EntityManagerFactory` and `TransactionManager` beans, pointing to respective datasources and package scans.

---

## 224. How to enable async in Spring Boot?

**Answer:**
1.  **Enable:** Add `@EnableAsync` to a configuration class.
2.  **Usage:** Annotate a method with `@Async`.
3.  **Behavior:** The method executes in a separate thread (from a helper TaskExecutor).
4.  **Return Type:** `void` or `Future<T>` / `CompletableFuture<T>`.

---

## 225. How to implement global exception handling?

**Answer:**
Use **@ControllerAdvice** (or `@RestControllerAdvice`) and **@ExceptionHandler**.
*   **Mechanism:** It acts as an interceptor for exceptions thrown by any controller.
*   **Example:**
    ```java
    @RestControllerAdvice
    public class GlobalExceptionHandler {
        @ExceptionHandler(UserNotFoundException.class)
        public ResponseEntity<String> handleUserNotFound(Exception ex) {
            return new ResponseEntity<>(ex.getMessage(), HttpStatus.NOT_FOUND);
        }
    }
    ```
