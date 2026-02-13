## 171. What is Inversion of Control?

**Answer:**
**Inversion of Control (IoC)** is a design principle where the control of object creation and management is transferred from the programmer to a container (framework).
*   **Traditional:** App code calls Library. (You control flow).
*   **IoC:** Framework calls App code. (Framework controls flow - "Don't call us, we'll call you").
*   **Implementation:** Dependency Injection (DI) is the most common way to implement IoC.

---

## 172. What is Dependency Injection?

**Answer:**
**Dependency Injection (DI)** is a design pattern used to implement IoC.
*   **Concept:** Instead of an object creating its own dependencies (e.g., `new Service()`), the dependencies are "injected" into the object by an external entity (the Sprng Container).
*   **Benefit:** Loose coupling, easier unit testing (can mock dependencies), and cleaner code.

---

## 173. Constructor vs Setter injection?

**Answer:**

| Feature | Constructor Injection | Setter Injection |
| :--- | :--- | :--- |
| **Use Case** | **Mandatory** dependencies. | **Optional** dependencies. |
| **Immutability** | Fields can be `final`. | Fields cannot be `final`. |
| **Safety** | Object is valid/fully initialized when created. | Object might be in partial state until setters are called. |
| **Preference** | **Recommended** (Spring team preferred). | Use sparingly. |

---

## 174. Field injection drawbacks?

**Answer:**
Field Injection (`@Autowired` directly on field) is generally **discouraged**.
*   **Drawbacks:**
    1.  **Testing:** Hard to unit test because you cannot inject mocks without a Spring Context (or using Reflection).
    2.  **Immutability:** Fields cannot be `final`.
    3.  **Hiding Dependencies:** A class can easily become bloated with too many dependencies without noticing (Constructor arguments makes it obvious).
    4.  **Circular Dependencies:** Easier to accidentally create them.

---

## 175. What is ApplicationContext?

**Answer:**
**ApplicationContext** is the central interface to the Spring IoC Container.
*   **Role:** It instantiates, configures, and assembles beans.
*   **Functionality:** It provides advanced features like:
    *   Internationalization (i18n).
    *   Event publication (ApplicationEvent).
    *   AOP integration.
    *   Transaction management.

---

## 176. BeanFactory vs ApplicationContext?

**Answer:**
| Feature | BeanFactory | ApplicationContext |
| :--- | :--- | :--- |
| **Type** | Basic IoC Container. | Advanced IoC Container (Extends BeanFactory). |
| **Loading** | **Lazy** (Loads beans only when requested `getBean`). | **Eager** (Pre-instantiates all Singletons at startup). |
| **Features** | Basic DI support. | DI + AOP + Messaging + Web support + i18n. |
| **Use Case** | Resource-constrained mobile/embedded apps. | Enterprise Web Applications (Standard). |

---

## 177. What is Bean lifecycle?

**Answer:**
The lifecycle of a Spring Bean:
1.  **Instantiate:** Create object (Constructor).
2.  **Populate Properties:** Inject dependencies (Setters/Fields).
3.  **Aware Interfaces:** setBeanName, setBeanFactory using `BeanNameAware`, etc.
4.  **Pre-Initialization:** `BeanPostProcessor.postProcessBeforeInitialization()`.
5.  **Initialize:** `@PostConstruct`, `InitializingBean.afterPropertiesSet()`, custom `init-method`.
6.  **Post-Initialization:** `BeanPostProcessor.postProcessAfterInitialization()` (AOP Proxies created here).
7.  **Ready:** Bean is ready to use.
8.  **Destroy:** `@PreDestroy`, `DisposableBean.destroy()`, custom `destroy-method` (When context closes).

---

## 178. What are Bean scopes?

**Answer:**
Spring Beans have 6 standard scopes:
1.  **Singleton (Default):** One instance per container.
2.  **Prototype:** New instance every time it is requested.
3.  **Request:** One instance per HTTP Request (Web only).
4.  **Session:** One instance per HTTP Session (Web only).
5.  **Application:** One instance per `ServletContext` (Web only).
6.  **WebSocket:** One instance per WebSocket (Web only).

---

## 179. Singleton vs Prototype?

**Answer:**
*   **Singleton:** Shared instance. **Stateless** beans (Services, DAO, Controllers) should be Singletons. Thread-safety must be handled if state is maintained.
*   **Prototype:** Independent instances. **Stateful** beans (Users, ShoppingCarts) can be Prototypes.
*   **Injection:** If a Singleton bean has a Prototype dependency, the Prototype is injected **once** (at creation time), effectively becoming a Singleton. (Solution: Use `Lookup Method Injection` or `Provider<Prototype>`).

---

## 180. What is @ComponentScan?

**Answer:**
`@ComponentScan` tells Spring where to look for annotated components (beans).
*   **Usage:** `@ComponentScan(basePackages = "com.example")`.
*   **Mechanism:** It scans the specified packages for classes annotated with `@Component` (and its stereotypes `@Service`, `@Repository`, `@Controller`, `@Configuration`) and registers them as beans in the ApplicationContext.
*   **Spring Boot:** `@SpringBootApplication` includes `@ComponentScan` implicitly for the current package and sub-packages.

---

## 181. What is @Component, @Service, @Repository?

**Answer:**
These are Stereotype Annotations used to register beans in the Spring Container.
*   **@Component:** Generic stereotype for any Spring-managed component.
*   **@Service:** Semantically indicates the class holds **Business Logic**. It doesn't add extra behavior over @Component (except for AOP pointcuts).
*   **@Repository:** Indicates a **Data Access Object (DAO)**. It adds automatic **Exception Translation** (converts SQL exceptions to Spring's `DataAccessException` hierarchy).
*   **@Controller:** Indicates a Spring MVC Controller.

---

## 182. What is @Configuration?

**Answer:**
`@Configuration` indicates that a class allows definition of bean methods (annotated with `@Bean`).
*   **Full Mode (Default):** The class is proxied by CGLIB. Calls to `@Bean` methods within the class are intercepted to ensure **dependency injection** and **singleton scope** are respected (calling a bean method twice returns the *same* instance).
*   **Lite Mode:** (`proxyBeanMethods = false`). No CGLIB proxy. Faster startup, but inter-bean method calls create *new instances*.

---

## 183. What is @Bean annotation?

**Answer:**
`@Bean` is a method-level annotation used in a `@Configuration` class to manually define a bean.
*   **Mechanism:** The return value of the method is registered as a bean in the BeanFactory.
*   **ID:** The bean ID is the method name (unless customized `@Bean("myBean")`).
*   **Lifecycle:** Supports `initMethod` and `destroyMethod` attributes.

---

## 184. What is @Primary?

**Answer:**
`@Primary` indicates that a bean should be given **preference** when multiple candidates are qualified to autowire a single-valued dependency.
*   **Use Case:** You have two implementations of `PaymentService` (`CreditCard`, `PayPal`). Mark `CreditCard` as `@Primary` to inject it by default when `@Autowired PaymentService` is used without a qualifier.

---

## 185. What is @Qualifier?

**Answer:**
`@Qualifier` is used for **fine-grained control** over dependency injection when multiple beans of the same type exist.
*   **Usage:** Combined with `@Autowired`.
*   **Example:**
    ```java
    @Autowired
    @Qualifier("payPalService")
    private PaymentService paymentService;
    ```
*   **Difference:** `@Primary` is a default valid for all injection points. `@Qualifier` overrides the default for a *specific* injection point.

---

## 186. What is circular dependency?

**Answer:**
A **Circular Dependency** occurs when Bean A depends on Bean B, and Bean B depends on Bean A.
*   **Result:** The container cannot instantiate either bean because it needs the other one first.
*   **Spring Handling:** Spring can resolve this *only* for **Singleton** beans interacting via **Setter/Field Injection**. It fails for **Constructor Injection** or Prototype beans.

---

## 187. How does Spring resolve circular dependency?

**Answer:**
Spring resolves circular dependencies for singletons using **Three-Level Caching**:
1.  **Singleton Objects (Level 1):** Fully initialized beans.
2.  **Early Singleton Objects (Level 2):** Raw bean instances (instantiated but not populated/initialized).
3.  **Singleton Factories (Level 3):** Object factories to create the bean (or proxy).
*   **Process:** Bean A is created (raw) and exposed in Level 3. Bean B is created, asks for A. It gets the "Early" A reference. B finishes. A finishes.

---

## 188. What is lazy initialization?

**Answer:**
**Lazy Initialization** means the bean is created **only when it is first requested**, not at application startup.
*   **Annotation:** `@Lazy`.
*   **Scope:** Can be applied to a `@Configuration` class (all beans lazy), a specific `@Bean`, or an `@Autowired` injection point (injects a proxy).
*   **Pros:** Faster startup time.
*   **Cons:** Errors (misconfiguration) are discovered at runtime instead of startup.

---

## 189. What is BeanPostProcessor?

**Answer:**
`BeanPostProcessor` (BPP) is a powerful interface that allows custom modification of new bean instances.
*   **Methods:**
    1.  `postProcessBeforeInitialization()`: Runs *after* dependency injection but *before* init methods (`@PostConstruct`).
    2.  `postProcessAfterInitialization()`: Runs *after* init methods.
*   **Use Cases:** Checking marker interfaces, wrapping beans with Proxies (AOP), modifying bean properties.

---

## 190. What is InitializingBean?

**Answer:**
`InitializingBean` is a callback interface with a single method: `afterPropertiesSet()`.
*   **Execution:** Called by the container after all properties are set (DI is complete).
*   **Usage:** Performing custom initialization logic (validating configuration, opening connections).
*   **Alternative:** `@PostConstruct` annotation (JSR-250) is generally preferred over implementing this Spring-specific interface.

---


---

## 191. What is AOP?

**Answer:**
**AOP (Aspect-Oriented Programming)** is a programming paradigm that aims to increase modularity by allowing the separation of **cross-cutting concerns**.
*   **Cross-cutting concerns:** Functions that span multiple points of an application (e.g., Logging, Security, Transaction Management).
*   **Goal:** To keep business logic clean and separate from system services.

---

## 192. What is aspect?

**Answer:**
An **Aspect** is a modularization of a cross-cutting concern.
*   **Analogy:** In OOP, a key unit of modularity is the `Class`. In AOP, it is the `Aspect`.
*   **Implementation:** In Spring AOP, aspects are implemented using regular classes annotated with `@Aspect` (or XML configuration).
*   **Example:** A `LoggingAspect` class.

---

## 193. What is advice?

**Answer:**
**Advice** is the action taken by an aspect at a particular **Join Point**.
*   **Concept:** It is the actual code (method) that executes when a specific point in the application is reached.
*   **Example:** "Log this message" or "Begin transaction".

---

## 194. Types of advice?

**Answer:**
Spring AOP supports 5 types of advice:
1.  **@Before:** Executes *before* a join point.
2.  **@AfterReturning:** Executes *after* a join point completes normally.
3.  **@AfterThrowing:** Executes if a method exits by throwing an exception.
4.  **@After (Finally):** Executes *after* a join point regardless of the outcome (normal or exception).
5.  **@Around:** The most powerful advice. It surrounds the join point (can perform custom behavior before and after invocation, or even skip invocation).

---

## 195. What is pointcut?

**Answer:**
A **Pointcut** is a predicate (expression) that matches **Join Points**.
*   **Role:** Advice is associated with a pointcut expression and runs at any join point matched by the pointcut.
*   **Expression Language:** Spring uses the AspectJ pointcut expression language.
*   **Example:** `execution(* com.example.service.*.*(..))` (Matches all methods in service package).

---

## 196. What is join point?

**Answer:**
A **Join Point** is a point during the execution of a program, such as the **execution of a method** or the handling of an exception.
*   **Scope:** In Spring AOP, a join point *always* represents a **method execution**.
*   **Info:** You can access join point details (method name, arguments) via the `JoinPoint` parameter in the advice method.

---

## 197. What is weaving?

**Answer:**
**Weaving** is the process of linking aspects with other application types or objects to create an advised object.
*   **Time:** Can occur at:
    *   **Compile Time:** (using AspectJ compiler).
    *   **Load Time:** (using AspectJ loader).
    *   **Runtime:** (Spring AOP default). Spring creates proxies at runtime.

---

## 198. Proxy-based AOP vs AspectJ?

**Answer:**
| Feature | Spring AOP | AspectJ |
| :--- | :--- | :--- |
| **Weaving** | **Runtime** (Proxy). | **Compile-time** / Load-time / Post-compile. |
| **Scope** | Only **Method Execution** on Spring Beans. | Constructor, Field access, Static methods, Final classes. |
| **Performance** | Good (Sufficient for most enterprise needs). | Much Faster (No runtime overhead of proxy creation). |
| **Complexity** | Simple (Pure Java). | Complex (Requires separate compiler/agent). |

---

## 199. What is @Transactional internally?

**Answer:**
`@Transactional` works using **Spring AOP**.
1.  Spring creates a **Proxy** around the bean.
2.  When a method is called, the Proxy's **Around Advice** intercepts it.
3.  It opens a DB Transaction (from TransactionManager).
4.  It executes the actual method.
5.  If success -> **Commit**. If RuntimeException -> **Rollback**.

---

## 200. What are common AOP use cases?

**Answer:**
1.  **Declarative Transaction Management:** (`@Transactional`).
2.  **Logging/Tracing:** Log every method entry/exit or execution time.
3.  **Security:** checking roles before method execution (`@PreAuthorize`).
4.  **Caching:** (`@Cacheable`).
5.  **Error Handling:** Global exception handling.
