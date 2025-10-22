Great, Aditya! Based on your updated request, here’s the **final breakdown** of the **1000 interview questions**, covering **technical**, **project-based**, and **HR/leadership** aspects aligned with your 3.5+ years of experience as a Full Stack Java Developer and Module Lead:

---

### ✅ **Final Breakdown:**

#### 🔹 Technical Topics – 850 Questions (50 each)

1. Core Java
2. Spring MVC
3. Spring Boot
4. Microservices
5. Hibernate
6. REST APIs
7. JUnit & Mockito
8. JavaScript
9. React.js
10. Angular
11. MySQL
12. PostgreSQL
13. MongoDB
14. Redis
15. RabbitMQ
16. Kafka
17. Docker
18. Kubernetes
19. Jenkins
20. System Design (High-Level & Low-Level combined)

#### 🔹 Non-Technical Topics – 150 Questions

21. **Project-Based Questions** (based on your HRMS, Appointment Booking, Notification Integration projects) – 50
22. **HR Round Questions (Java Developer role)** – 50
23. **Behavioral & Leadership Questions** (Module Lead role) – 50

---

I’ll now begin with the **first set: Core Java – 50 Interview Questions with Answers**.

Would you prefer:

* ✅ 10 questions at a time?
* ✅ Or the full 50 in one go?

Let me know your preference.

Perfect, Aditya! Here's the complete list of **Top 50 Core Java Interview Questions with Answers**, tailored for **3.5+ years of experience** and aligned with your backend expertise.

---

## ✅ **Core Java – Top 50 Interview Questions with Answers**

---

### 🔹 **1. What is the difference between JDK, JRE, and JVM?**

* **JDK (Java Development Kit):** Contains tools for Java development including JRE + compilers.
* **JRE (Java Runtime Environment):** Includes JVM + libraries to run Java programs.
* **JVM (Java Virtual Machine):** Converts bytecode into machine code for execution.

---

### 🔹 **2. Explain the OOPs concepts in Java.**

* **Encapsulation:** Wrapping data and methods (e.g., POJO classes).
* **Abstraction:** Hiding implementation details (e.g., `interface`, `abstract class`).
* **Inheritance:** Acquiring parent class properties.
* **Polymorphism:** Compile-time (method overloading) and runtime (method overriding).

---

### 🔹 **3. What is the difference between `==` and `.equals()`?**

* `==` compares **object references**.
* `.equals()` compares **object content** (if overridden properly in the class).

---

### 🔹 **4. Can we override a static method?**

* No. Static methods are class-level and are **not bound to instance**, hence **not polymorphic**.

---

### 🔹 **5. What is a constructor in Java?**

* A special method used to **initialize** objects.
* Name = class name; no return type.

---

### 🔹 **6. What is the purpose of the `final` keyword?**

* `final class`: Cannot be extended.
* `final method`: Cannot be overridden.
* `final variable`: Acts like a constant.

---

### 🔹 **7. What is the difference between `ArrayList` and `LinkedList`?**

* **ArrayList:** Faster for random access.
* **LinkedList:** Faster for insertions/deletions.

---

### 🔹 **8. What are checked and unchecked exceptions?**

* **Checked:** Compile-time (e.g., `IOException`).
* **Unchecked:** Runtime (e.g., `NullPointerException`).

---

### 🔹 **9. Explain the Java memory model (Heap, Stack, etc.).**

* **Heap:** Objects are stored.
* **Stack:** Method calls and local variables.
* **Method Area, PC Register, Native Stack:** Other memory segments.

---

### 🔹 **10. What is a `StringBuilder` vs `StringBuffer`?**

* `StringBuilder`: Non-thread-safe but fast.
* `StringBuffer`: Thread-safe but slow.

---

### 🔹 **11. What is the use of `transient` keyword?**

* It marks a variable **not to be serialized** during object serialization.

---

### 🔹 **12. What is the difference between `throw` and `throws`?**

* `throw`: To **explicitly throw** an exception.
* `throws`: To **declare exceptions** in method signature.

---

### 🔹 **13. What is method overloading and overriding?**

* **Overloading:** Same method name, different parameters (compile-time).
* **Overriding:** Same method signature in subclass (runtime).

---

### 🔹 **14. What are wrapper classes in Java?**

* Used to convert **primitives into objects** (`int` → `Integer`, `double` → `Double`, etc.).

---

### 🔹 **15. What is autoboxing and unboxing?**

* **Autoboxing:** Primitive → Wrapper.
* **Unboxing:** Wrapper → Primitive.

---

### 🔹 **16. What are the different access modifiers in Java?**

* `private`, `default` (package-private), `protected`, `public`.

---

### 🔹 **17. Difference between `abstract class` and `interface`?**

* **Abstract class:** Can have both abstract and concrete methods.
* **Interface:** Only abstract (Java 8+ allows `default` and `static` methods).

---

### 🔹 **18. What is the use of `instanceof`?**

* Used to check if an object **is an instance of a specific class** or subclass.

---

### 🔹 **19. What is `HashMap`? How does it work internally?**

* Key-value pair storage using **hashing**.
* Uses **hashCode()** to find the bucket and **equals()** to resolve collisions.

---

### 🔹 **20. Can a class be both abstract and final?**

* No. `abstract` requires subclassing; `final` prevents subclassing.

---

### 🔹 **21. What is the difference between `Array` and `ArrayList`?**

* Arrays are **fixed-size**, **non-resizable**.
* `ArrayList` is **dynamic**, part of **Collection framework**.

---

### 🔹 **22. What is `volatile` keyword in Java?**

* Prevents **thread caching**; ensures the variable is **read directly from main memory**.

---

### 🔹 **23. What is synchronization?**

* A mechanism to **control access** to a shared resource by multiple threads.

---

### 🔹 **24. Difference between `sleep()` and `wait()`?**

* `sleep()` is from `Thread` class; doesn’t release lock.
* `wait()` is from `Object` class; releases lock.

---

### 🔹 **25. Explain `hashCode()` and `equals()` contract.**

* If two objects are equal (via `.equals()`), they **must** have same `hashCode()`.
* Crucial for `HashMap`, `HashSet`.

---

### 🔹 **26. What is a thread-safe collection?**

* Collections like `Vector`, `Hashtable`, or concurrent classes (`ConcurrentHashMap`) ensure thread safety.

---

### 🔹 **27. Explain exception hierarchy in Java.**

```
Throwable
├── Error (unchecked)
└── Exception
     ├── Checked
     └── RuntimeException (unchecked)
```

---

### 🔹 **28. What is an anonymous class in Java?**

* A class defined **without a name**, used for **one-time use**, mostly with event handling or threading.

---

### 🔹 **29. What is a lambda expression?**

* Java 8 feature for writing **functional-style** code:

```java
(x, y) -> x + y;
```

---

### 🔹 **30. What is functional interface?**

* An interface with only **one abstract method**.
* Annotated with `@FunctionalInterface`.

---

### 🔹 **31. What are default methods in interfaces?**

* Java 8 allows method definitions in interfaces using `default` keyword.

---

### 🔹 **32. Difference between `Comparator` and `Comparable`?**

* `Comparable`: Natural ordering (in class).
* `Comparator`: Custom ordering (external class).

---

### 🔹 **33. What is the use of `super` keyword?**

* Refers to the **parent class**.
* Used to access parent methods, constructors, and variables.

---

### 🔹 **34. What is immutability?**

* An object is immutable if **its state cannot change** once created. (e.g., `String` class)

---

### 🔹 **35. What is a memory leak in Java?**

* Unused objects remaining in memory due to unintentional references → memory leak.

---

### 🔹 **36. Difference between shallow copy and deep copy?**

* **Shallow copy:** References are copied.
* **Deep copy:** Entire objects are duplicated.

---

### 🔹 **37. What are enums in Java?**

* A type that defines a **fixed set of constants**.

```java
enum Day { MON, TUE, WED }
```

---

### 🔹 **38. What is the use of `this` keyword?**

* Refers to the **current instance** of the class.

---

### 🔹 **39. What is a static block?**

* A block that is executed **only once** when the class is loaded.

---

### 🔹 **40. Explain garbage collection in Java.**

* Java automatically reclaims memory from unreachable objects using **Garbage Collector** (GC).

---

### 🔹 **41. What is the difference between `String`, `StringBuilder`, `StringBuffer`?**

* `String`: Immutable.
* `StringBuilder`: Mutable, non-thread-safe.
* `StringBuffer`: Mutable, thread-safe.

---

### 🔹 **42. Explain try-with-resources.**

* Java 7+ feature for automatic closing of resources.

```java
try (BufferedReader br = new BufferedReader(...)) {
   // ...
}
```

---

### 🔹 **43. How does Java achieve platform independence?**

* Java compiles code into **bytecode**, which is executed by **JVM**, making it platform-independent.

---

### 🔹 **44. What is the use of `package` in Java?**

* Organizes classes into **namespaces** to avoid conflicts and support modular code.

---

### 🔹 **45. What is the difference between `private`, `protected`, and `public`?**

* `private`: Only within class.
* `protected`: Class + subclasses + same package.
* `public`: Accessible everywhere.

---

### 🔹 **46. What is the diamond problem in Java?**

* Arises with **multiple inheritance**, solved in Java using **interfaces** and **default methods**.

---

### 🔹 **47. Can we create an object of an abstract class?**

* No. But we can reference it using subclass objects.

---

### 🔹 **48. What is the purpose of `Object` class?**

* It's the **superclass** of all Java classes. Provides methods like `toString()`, `equals()`, `hashCode()`.

---

### 🔹 **49. What is classloader in Java?**

* Loads class files into JVM. Types:

    * Bootstrap
    * Extension
    * Application

---

### 🔹 **50. What is reflection in Java?**

* Allows inspecting and modifying classes, methods, and fields **at runtime** using `java.lang.reflect`.

---

✅ Let me know when you're ready for the next topic: **Spring MVC – 50 Questions**, or if you want the PDF export of this set.

Great! Let's move on to the next topic in your interview preparation list.

---

## ✅ **Spring MVC – Top 50 Interview Questions with Answers**

Tailored for 3.5+ years of real-world backend development experience, especially in enterprise projects like HRMS and booking systems.

---

### 🔹 **1. What is Spring MVC?**

* A web framework under the Spring Framework that follows the **Model-View-Controller** design pattern for building scalable web applications.

---

### 🔹 **2. What is the role of DispatcherServlet in Spring MVC?**

* It acts as the **front controller** that intercepts all incoming requests and routes them to appropriate handlers (controllers).

---

### 🔹 **3. Explain the Spring MVC flow.**

1. Request → DispatcherServlet
2. DispatcherServlet → HandlerMapping
3. Handler → Controller
4. Controller returns ModelAndView
5. ViewResolver resolves view
6. DispatcherServlet renders response

---

### 🔹 **4. What is a Controller in Spring MVC?**

* A Java class annotated with `@Controller` to handle web requests.

```java
@Controller
public class MyController {
    @GetMapping("/hello")
    public String sayHello() {
        return "hello.jsp";
    }
}
```

---

### 🔹 **5. Difference between `@Controller` and `@RestController`?**

* `@Controller`: Returns view name.
* `@RestController`: Returns data (`@Controller` + `@ResponseBody`).

---

### 🔹 **6. How do you map a request to a method in Spring MVC?**

* Using `@RequestMapping`, `@GetMapping`, `@PostMapping`, etc.

---

### 🔹 **7. What is `@RequestParam` used for?**

* To extract query parameters from a request.

```java
@GetMapping("/greet")
public String greet(@RequestParam String name) { ... }
```

---

### 🔹 **8. What is `@PathVariable` used for?**

* Extracts values from URI path.

```java
@GetMapping("/user/{id}")
public String getUser(@PathVariable int id) { ... }
```

---

### 🔹 **9. What is `@ModelAttribute` used for?**

* Binds form data to model object or adds attributes to model.

---

### 🔹 **10. How do you handle exceptions in Spring MVC?**

* Using `@ExceptionHandler`, `@ControllerAdvice`, or custom error pages.

---

### 🔹 **11. What is ViewResolver in Spring MVC?**

* Resolves view names into actual views.

---

### 🔹 **12. What are the common View types in Spring MVC?**

* JSP, Thymeleaf, FreeMarker, PDF, JSON, Excel.

---

### 🔹 **13. What is `HandlerMapping`?**

* It determines which controller method should handle a request.

---

### 🔹 **14. What is `ModelAndView` in Spring MVC?**

* Combines both the model data and view name in a single return object.

---

### 🔹 **15. Difference between `Model`, `ModelMap`, and `ModelAndView`?**

* All are used to pass data from controller to view.

---

### 🔹 **16. What is the default scope of a Spring MVC bean?**

* `singleton`. But in MVC context, `request` and `session` are also common.

---

### 🔹 **17. How do you upload a file in Spring MVC?**

* Use `MultipartFile` with `multipartResolver` bean configuration.

---

### 🔹 **18. How do you handle form validation in Spring MVC?**

* Use `@Valid` or `@Validated` with JSR-303 and `BindingResult`.

---

### 🔹 **19. What is `WebDataBinder`?**

* A mechanism for binding HTTP request parameters to JavaBean objects.

---

### 🔹 **20. How to redirect to another controller in Spring MVC?**

```java
return "redirect:/new-url";
```

---

### 🔹 **21. How to forward to another view internally?**

```java
return "forward:/internal.jsp";
```

---

### 🔹 **22. What is the use of `@InitBinder`?**

* Used to customize request parameter binding.

---

### 🔹 **23. How do you secure a Spring MVC application?**

* Use **Spring Security**, interceptors, or filters.

---

### 🔹 **24. What are interceptors in Spring MVC?**

* `HandlerInterceptor` to intercept requests before and after controller processing.

---

### 🔹 **25. How does Spring MVC support RESTful web services?**

* Using `@RestController`, `@GetMapping`, `@PostMapping`, etc., with JSON/XML support.

---

### 🔹 **26. How do you return JSON from a controller?**

* Use `@ResponseBody` or `@RestController`, and Jackson is used for conversion.

---

### 🔹 **27. What is `@ResponseBody`?**

* Converts return value of a method directly to HTTP response (like JSON or XML).

---

### 🔹 **28. What is `@RequestBody`?**

* Binds the HTTP request body to a Java object.

---

### 🔹 **29. Difference between form backing bean and command object?**

* Both are used to bind form fields to POJOs.

---

### 🔹 **30. What is a custom validator?**

* Implements `Validator` interface or use `@Constraint` for custom annotation.

---

### 🔹 **31. How to internationalize a Spring MVC app?**

* Use `ResourceBundleMessageSource` and locale-specific message properties.

---

### 🔹 **32. What is content negotiation in Spring MVC?**

* Determines response type (JSON, XML, etc.) using headers, params, or file extensions.

---

### 🔹 **33. How do you enable static resource handling in Spring MVC?**

```java
@Override
public void addResourceHandlers(ResourceHandlerRegistry registry) {
    registry.addResourceHandler("/static/**").addResourceLocations("/resources/");
}
```

---

### 🔹 **34. How do you configure Spring MVC without XML?**

* Use **Java Config** (`@Configuration`, `@EnableWebMvc`) and `WebMvcConfigurer`.

---

### 🔹 **35. What is `@SessionAttributes` in Spring MVC?**

* Used to store model attributes in session across multiple requests.

---

### 🔹 **36. How is `@RequestMapping` different from `@GetMapping`?**

* `@RequestMapping` is generic, supports multiple HTTP methods; `@GetMapping` is specific to GET.

---

### 🔹 **37. How to test Spring MVC controllers?**

* Use `MockMvc` in Spring Test framework.

---

### 🔹 **38. What is `ContentNegotiatingViewResolver`?**

* Resolves view based on request’s `Accept` header (e.g., JSON, XML, HTML).

---

### 🔹 **39. What is `HiddenHttpMethodFilter`?**

* Enables support for HTTP methods like PUT and DELETE via hidden form fields.

---

### 🔹 **40. How to manage session in Spring MVC?**

* Use `HttpSession`, or Spring’s `@SessionAttributes`.

---

### 🔹 **41. How do you initialize `DispatcherServlet` in Java config?**

* By extending `AbstractAnnotationConfigDispatcherServletInitializer`.

---

### 🔹 **42. What is `FlashMap` in Spring MVC?**

* Used for passing temporary data during a redirect.

---

### 🔹 **43. How does Spring MVC integrate with JSP?**

* By configuring `InternalResourceViewResolver` and placing JSPs in `/WEB-INF/views`.

---

### 🔹 **44. How does Spring handle form binding for dates and custom types?**

* Using `@DateTimeFormat`, `@InitBinder`, or custom `PropertyEditor`.

---

### 🔹 **45. What are tag libraries in Spring MVC?**

* JSP tag libraries like `spring-form`, `spring-core`, used for form binding and data display.

---

### 🔹 **46. How to return an Excel or PDF from Spring MVC controller?**

* Implement custom view using `AbstractPdfView` or `AbstractXlsView`.

---

### 🔹 **47. How does Spring MVC handle circular dependencies?**

* Spring can detect and throw `BeanCurrentlyInCreationException`.

---

### 🔹 **48. What is `SimpleMappingExceptionResolver`?**

* Maps exceptions to view names using properties.

---

### 🔹 **49. Can we define multiple `DispatcherServlet`s?**

* Yes, for modular web applications.

---

### 🔹 **50. What is `HandlerAdapter` in Spring MVC?**

* Executes the handler (controller) method based on request mapping.

---

✅ Let me know if you'd like the **PDF export** so far or continue with the next topic: **Spring Boot – 50 Questions**?

Awesome, Aditya! Here's your next complete set:

---

## ✅ **Spring Boot – Top 50 Interview Questions with Answers**

Tailored to your **3.5+ years** of backend experience using Spring Boot for building HRMS and Appointment systems.

---

### 🔹 **1. What is Spring Boot?**

* Spring Boot is a framework to build production-ready Spring applications **with minimal configuration**. It simplifies dependency management, embedded server setup, and auto-configuration.

---

### 🔹 **2. What are the advantages of using Spring Boot?**

* Auto Configuration
* Embedded Servers
* No XML Configuration
* Actuator Support
* Rapid Development

---

### 🔹 **3. What is the Spring Boot Starter?**

* A **starter** is a curated set of dependencies bundled in a single library (e.g., `spring-boot-starter-web` for web apps).

---

### 🔹 **4. What is `@SpringBootApplication`?**

* A combination of:

    * `@Configuration`
    * `@EnableAutoConfiguration`
    * `@ComponentScan`

---

### 🔹 **5. What is auto-configuration in Spring Boot?**

* Auto-configures beans based on classpath, property settings, and defined beans using `@EnableAutoConfiguration`.

---

### 🔹 **6. How do you disable specific auto-configuration?**

```java
@SpringBootApplication(exclude = {DataSourceAutoConfiguration.class})
```

---

### 🔹 **7. What is application.properties / application.yml?**

* Configuration file where you define application-level properties like port, DB configs, etc.

```properties
server.port=8081
spring.datasource.url=...
```

---

### 🔹 **8. How do you create REST APIs using Spring Boot?**

* Use `@RestController`, `@RequestMapping`, `@GetMapping`, `@PostMapping`, etc.

---

### 🔹 **9. What embedded servers does Spring Boot support?**

* Tomcat (default), Jetty, Undertow.

---

### 🔹 **10. How do you change the default server port?**

```properties
server.port=9090
```

---

### 🔹 **11. What is Spring Boot Actuator?**

* Provides endpoints to monitor and manage the application (e.g., health, metrics, info).

---

### 🔹 **12. How do you enable and access actuator endpoints?**

```properties
management.endpoints.web.exposure.include=*
```

* Access at: `http://localhost:8080/actuator/health`

---

### 🔹 **13. How do you use profiles in Spring Boot?**

* Create files like `application-dev.properties`, `application-prod.properties`
* Activate using:

```properties
spring.profiles.active=dev
```

---

### 🔹 **14. What is the use of `CommandLineRunner`?**

* Runs code at startup.

```java
@Component
public class AppStartup implements CommandLineRunner {
    public void run(String... args) {
        // logic
    }
}
```

---

### 🔹 **15. What is `@ConfigurationProperties`?**

* Binds hierarchical configuration from properties/yaml files to a Java object.

---

### 🔹 **16. Difference between `@Value` and `@ConfigurationProperties`?**

* `@Value`: Inject single property
* `@ConfigurationProperties`: Maps whole set of related properties

---

### 🔹 **17. What is DevTools in Spring Boot?**

* Provides live reload, automatic restart, and better debugging for development.

---

### 🔹 **18. How to configure a DataSource in Spring Boot?**

```properties
spring.datasource.url=jdbc:mysql://...
spring.datasource.username=root
spring.datasource.password=pass
```

---

### 🔹 **19. What is `@RestControllerAdvice`?**

* A combination of `@ControllerAdvice + @ResponseBody`, used for global exception handling.

---

### 🔹 **20. What is `@EntityScan` and `@EnableJpaRepositories`?**

* Used to specify custom packages for JPA entities and repository interfaces.

---

### 🔹 **21. How to return a custom HTTP status in Spring Boot?**

```java
return new ResponseEntity<>(body, HttpStatus.CREATED);
```

---

### 🔹 **22. How do you configure custom error pages?**

* Create an `error.html` under `src/main/resources/templates`.

---

### 🔹 **23. How to enable Swagger in Spring Boot?**

* Add `springfox-swagger2` and `springfox-swagger-ui` dependencies.
* Use `@EnableSwagger2` + API documentation annotations.

---

### 🔹 **24. What is actuator’s `/shutdown` endpoint?**

* Allows remote shutdown (must be enabled explicitly).

---

### 🔹 **25. How do you create custom starters in Spring Boot?**

* Create a module with dependencies + `spring.factories` file.

---

### 🔹 **26. How is Spring Boot different from Spring?**

* Spring Boot is opinionated and convention-driven, with **auto-configuration**, unlike the manual config in traditional Spring.

---

### 🔹 **27. How does Spring Boot handle JSON conversion?**

* Uses Jackson by default to convert Java objects to JSON and vice versa.

---

### 🔹 **28. What is the `@EnableAutoConfiguration` annotation for?**

* Enables Spring Boot to auto-configure the application context based on classpath.

---

### 🔹 **29. What is `@SpringBootTest`?**

* Annotation to run integration tests in Spring Boot.

---

### 🔹 **30. How do you configure logging in Spring Boot?**

* Uses Logback by default. Can be configured using `application.properties`.

```properties
logging.level.org.springframework=DEBUG
```

---

### 🔹 **31. What is the difference between `spring-boot-starter-web` and `spring-boot-starter-data-jpa`?**

* `web`: For web development (Tomcat, REST).
* `data-jpa`: For database access via Spring Data JPA.

---

### 🔹 **32. What are some important production-ready features Spring Boot offers?**

* Health Checks
* Metrics
* Custom Banners
* Graceful shutdown
* External Config Support

---

### 🔹 **33. How to externalize properties in Spring Boot?**

* Use environment variables, command-line arguments, or external `config` directory.

---

### 🔹 **34. What is the use of `@EnableScheduling`?**

* Enables scheduled tasks using `@Scheduled`.

---

### 🔹 **35. What is the use of `@Async` in Spring Boot?**

* Used to run methods asynchronously on a different thread.

---

### 🔹 **36. How to secure a Spring Boot application?**

* Add Spring Security dependency and configure roles and filters.

---

### 🔹 **37. How to limit HTTP request size in Spring Boot?**

```properties
spring.servlet.multipart.max-file-size=10MB
spring.servlet.multipart.max-request-size=10MB
```

---

### 🔹 **38. How to customize the banner in Spring Boot?**

* Place a `banner.txt` file under `src/main/resources`.

---

### 🔹 **39. How to implement file download in Spring Boot?**

```java
@GetMapping("/download")
public ResponseEntity<Resource> downloadFile() {
    ...
}
```

---

### 🔹 **40. How do you test REST APIs in Spring Boot?**

* Use `MockMvc`, `TestRestTemplate`, and JUnit with `@WebMvcTest`.

---

### 🔹 **41. What is Spring Boot Admin?**

* A web UI tool to manage and monitor Spring Boot applications via Actuator.

---

### 🔹 **42. How do you handle exceptions globally in Spring Boot?**

* Using `@ControllerAdvice` with `@ExceptionHandler`.

---

### 🔹 **43. Can we create WAR files using Spring Boot?**

* Yes. Change packaging to WAR in `pom.xml` and configure `SpringBootServletInitializer`.

---

### 🔹 **44. How does Spring Boot connect to databases other than MySQL?**

* Change driver and URL in `application.properties`. Spring Boot auto-configures it accordingly.

---

### 🔹 **45. What is Spring Cloud Config?**

* External config management service for Spring Boot apps in a distributed system.

---

### 🔹 **46. What is an embedded server?**

* A server like Tomcat or Jetty that comes bundled with the Spring Boot app.

---

### 🔹 **47. What’s the difference between `@Component`, `@Service`, `@Repository`, and `@Controller`?**

* All are stereotype annotations.

    * `@Component`: Generic bean
    * `@Service`: Business logic
    * `@Repository`: DAO logic
    * `@Controller`: Web layer

---

### 🔹 **48. What is graceful shutdown in Spring Boot?**

* Allows the application to finish current requests before terminating.

---

### 🔹 **49. How do you schedule tasks in Spring Boot?**

```java
@Scheduled(cron = "0 0 * * * *")
public void task() {
    ...
}
```

---

### 🔹 **50. What is actuator health indicator and how do you implement custom one?**

* Used to provide health status.

```java
@Component
public class CustomHealthIndicator implements HealthIndicator {
    public Health health() {
        return Health.up().withDetail("status", "Available").build();
    }
}
```

---

✅ Ready for the next topic: **Microservices – 50 Questions**? Let me know if you’d also like these in a compiled PDF later.

