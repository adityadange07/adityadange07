# LEVEL 3: ADVANCED (4+ Years Experience)

# Advanced Spring Boot

## 175. How does Spring manage bean lifecycle? What are the hooks?

Absolutely, Aditya! Let’s break down the **Spring Bean Lifecycle** step by step, including **all the hooks and callbacks** you can use. This is a common topic in Spring Boot interviews.

---

## 🧠 **1. What is a Bean in Spring?**

* A **Bean** is an object **managed by the Spring IoC container**.
* Spring takes care of **instantiation, dependency injection, initialization, and destruction**.

---

## ⚙️ **2. Spring Bean Lifecycle Steps**

1. **Bean Definition**

   * Container reads bean metadata from **XML, Java config (`@Bean`), or component scan (`@Component`)**.

2. **Instantiation**

   * Spring creates **an instance of the bean** using default constructor or factory method.

3. **Populate Properties / Dependency Injection**

   * Dependencies are injected via **setter injection, constructor injection, or field injection (`@Autowired`)**.

4. **BeanNameAware & BeanFactoryAware (Optional)**

   * If the bean implements **`BeanNameAware`**, Spring passes the **bean name**.
   * If the bean implements **`BeanFactoryAware`**, Spring passes the **BeanFactory reference**.

5. **ApplicationContextAware (Optional)**

   * If the bean implements **`ApplicationContextAware`**, Spring passes the **ApplicationContext reference**.

6. **Pre-initialization Bean Post Processors**

   * Spring applies **`BeanPostProcessor.beforeInitialization()`** methods.

7. **Custom Initialization (`@PostConstruct` or `afterPropertiesSet()`)**

   * `@PostConstruct` annotation on a method is called.
   * Or bean implements **`InitializingBean.afterPropertiesSet()`**.

8. **Post-initialization Bean Post Processors**

   * Spring applies **`BeanPostProcessor.afterInitialization()`** methods.

9. **Bean Ready to Use**

   * Bean is fully initialized and ready for use by the application.

10. **Destruction / Shutdown Hooks**

    * When context is closed:

      * `@PreDestroy` method is called.
      * Bean implements **`DisposableBean.destroy()`**.
      * Custom destroy-method defined in config is called.

---

## 🔹 **3. Lifecycle Hooks Summary**

| Hook / Interface / Annotation                     | When Called         | Purpose                 |
| ------------------------------------------------- | ------------------- | ----------------------- |
| `BeanNameAware.setBeanName()`                     | After instantiation | Get bean name           |
| `BeanFactoryAware.setBeanFactory()`               | After instantiation | Get BeanFactory         |
| `ApplicationContextAware.setApplicationContext()` | After instantiation | Get ApplicationContext  |
| `BeanPostProcessor.beforeInitialization()`        | Before init         | Modify bean before init |
| `InitializingBean.afterPropertiesSet()`           | During init         | Custom initialization   |
| `@PostConstruct`                                  | During init         | Custom initialization   |
| `BeanPostProcessor.afterInitialization()`         | After init          | Modify bean after init  |
| `@PreDestroy`                                     | During destruction  | Cleanup before removal  |
| `DisposableBean.destroy()`                        | During destruction  | Cleanup before removal  |
| `destroy-method` in config                        | During destruction  | Cleanup                 |

---

## ⚙️ **4. Example Bean Lifecycle in Spring**

```java
import javax.annotation.PostConstruct;
import javax.annotation.PreDestroy;
import org.springframework.beans.factory.InitializingBean;
import org.springframework.beans.factory.DisposableBean;
import org.springframework.stereotype.Component;

@Component
public class MyBean implements InitializingBean, DisposableBean {

    public MyBean() {
        System.out.println("1. Bean Constructor called");
    }

    @Override
    public void afterPropertiesSet() {
        System.out.println("4. afterPropertiesSet called");
    }

    @PostConstruct
    public void init() {
        System.out.println("3. @PostConstruct init method called");
    }

    @PreDestroy
    public void cleanup() {
        System.out.println("7. @PreDestroy cleanup method called");
    }

    @Override
    public void destroy() {
        System.out.println("8. DisposableBean destroy called");
    }
}
```

**Output when context starts and stops:**

```
1. Bean Constructor called
3. @PostConstruct init method called
4. afterPropertiesSet called
... bean is ready ...
7. @PreDestroy cleanup method called
8. DisposableBean destroy called
```

---

## 🔹 **5. Key Points**

1. **BeanPostProcessor** can intercept **before and after initialization**.
2. **`@PostConstruct`** and **`InitializingBean.afterPropertiesSet()`** → initialization hooks.
3. **`@PreDestroy`** and **`DisposableBean.destroy()`** → destruction hooks.
4. Spring manages **complete lifecycle** → developers rarely need manual initialization or destruction.

---

💡 **Interview Tip:**

* Mention **BeanPostProcessor**, **Aware interfaces**, **@PostConstruct / @PreDestroy**, and **destroy-method**.
* Diagrammatic explanation (constructor → DI → init → ready → destroy) helps **visualize lifecycle**.

---

If you want, I can make a **diagram showing all Spring bean lifecycle phases with hooks**, which is **super useful for interviews and whiteboard explanation**.

Do you want me to make that diagram?

---

## 176. What is a proxy in Spring? JDK vs CGLIB proxies?

Absolutely, Aditya! Let’s break down **Spring Proxies** and the difference between **JDK dynamic proxies** and **CGLIB proxies**. This is an important concept for **AOP, transactions, and Spring internals**.

---

## 🧠 **1. What is a Proxy in Spring?**

* **Definition:** A **proxy** is an **object that wraps another object** (the target) and **intercepts method calls** to add additional behavior.
* In Spring, proxies are widely used for:

  * **AOP (Aspect-Oriented Programming)** – logging, transactions, security.
  * **Lazy initialization**
  * **Remote procedure calls**
* Spring creates proxies **automatically** for beans when features like `@Transactional` or `@Async` are used.

---

### **How it works:**

1. Client calls a method on the **proxy object**.
2. Proxy intercepts the call.
3. Executes **pre-processing logic** (like transaction begin).
4. Calls the **actual target method**.
5. Executes **post-processing logic** (like transaction commit).

**Visual:**

```
Client ---> Proxy ---> Target Bean
           (intercepts method calls)
```

---

## ⚙️ **2. Types of Proxies in Spring**

Spring mainly uses **two types of proxies**:

### **A. JDK Dynamic Proxy**

* **Requirement:** Target class must implement **interfaces**.
* **Mechanism:** Uses **`java.lang.reflect.Proxy`** and **`InvocationHandler`**.
* **Creates proxy for interface** only (not the concrete class).
* **Use case:** Preferred if the bean **implements one or more interfaces**.

**Example:**

```java
public interface Service {
    void perform();
}

@Service
public class MyService implements Service {
    public void perform() { System.out.println("Service performing"); }
}

// Spring creates JDK proxy implementing Service interface
```

**Notes:**

* Proxy type = interface.
* Target class itself is **not subclassed**.

---

### **B. CGLIB Proxy**

* **Requirement:** Target class **does not need interfaces**.
* **Mechanism:** Uses **CGLIB (Code Generation Library)** to **subclass the target class** at runtime.
* **Proxy is a subclass** that overrides methods to add behavior.
* **Use case:** Used when **target class has no interfaces**.

**Example:**

```java
@Service
public class MyService {
    public void perform() { System.out.println("Service performing"); }
}

// Spring creates CGLIB proxy by subclassing MyService
```

**Notes:**

* Proxy type = subclass.
* Cannot proxy **final classes or final methods**.

---

### 🔹 **3. Differences between JDK and CGLIB Proxies**

| Feature            | JDK Dynamic Proxy                | CGLIB Proxy                                        |
| ------------------ | -------------------------------- | -------------------------------------------------- |
| Requirement        | Must implement **interface**     | Class doesn’t need interface                       |
| Implementation     | `java.lang.reflect.Proxy`        | Subclass using CGLIB                               |
| Proxy type         | Interface-based                  | Class-based                                        |
| Final class/method | Works only for interface methods | Cannot proxy final classes/methods                 |
| Performance        | Slightly slower for many methods | Faster for multiple methods (but creates subclass) |
| Default in Spring  | If interface present → JDK proxy | If no interface → CGLIB                            |

---

### 🔹 **4. How Spring Decides Which Proxy to Use**

* **`@EnableTransactionManagement(proxyTargetClass = false)` (default):**

  * If interface exists → **JDK proxy**
  * Else → fallback to **CGLIB proxy**
* **`proxyTargetClass = true`** → **force CGLIB proxy** even if interfaces exist.

---

### 🔹 **5. Real-Life Analogy**

* Think of a **proxy as a bodyguard**:

  * You want to **call a VIP** (target).
  * Proxy (bodyguard) **intercepts your call**, checks your credentials (pre-processing), forwards call to VIP, and monitors response (post-processing).

---

### 🔹 **6. Key Takeaways**

1. Spring uses proxies for **AOP, transactions, security**.
2. **JDK proxy → interface-based**, **CGLIB → class-based**.
3. **JDK preferred** if interface exists, **CGLIB used** otherwise.
4. Avoid **final classes/methods** if using CGLIB.

---

💡 **Interview Tip:**

* Always mention: **interface vs class**, **subclassing**, **@Transactional**, and **proxyTargetClass attribute**.
* Can also draw a simple diagram showing **client → proxy → target bean**.

---

If you want, I can make a **diagram comparing JDK proxy vs CGLIB proxy in Spring**, showing method interception flow, which is perfect for **whiteboard explanations in interviews**.

Do you want me to make that diagram?

---

## 177. What is the difference between @Autowired, @Inject, and @Resource?

Absolutely, Aditya! Let’s break down the differences between **`@Autowired`**, **`@Inject`**, and **`@Resource`** in Spring, including their behavior, source, and usage.

---

## 🧠 **1. @Autowired (Spring-specific)**

* **Package:** `org.springframework.beans.factory.annotation.Autowired`
* **Definition:** Spring’s **dependency injection annotation**.
* **Injection type:** By **type** (default), can also use by **name** with `@Qualifier`.
* **Required attribute:** `required=true` (default) → throws exception if no bean found.
* Can be used on:

  * **Fields**
  * **Constructors**
  * **Setter methods**
* **Supports Optional injection**: using `required=false` or `Optional<>`.

**Example:**

```java
@Autowired
private MyService myService;

// Constructor injection
@Autowired
public MyController(MyService myService) {
    this.myService = myService;
}
```

---

## 🧠 **2. @Inject (JSR-330 / Standard)**

* **Package:** `javax.inject.Inject`
* **Definition:** Standard Java **dependency injection annotation** (part of **JSR-330**).
* **Injection type:** By **type** (like `@Autowired`).
* **No `required` attribute** → use `@Inject Optional<MyService>` for optional injection.
* Spring **supports `@Inject`** out-of-the-box.

**Example:**

```java
@Inject
private MyService myService;
```

**Key Difference vs @Autowired:**

* Standardized (JSR-330), portable outside Spring.
* No `required` attribute; optional injection requires `Optional<>`.

---

## 🧠 **3. @Resource (JSR-250 / Java EE)**

* **Package:** `javax.annotation.Resource`
* **Definition:** Java EE annotation for **dependency injection by name** (default).
* **Injection type:** By **name**, can also use **type** if no name matches.
* Attributes:

  * `name` → inject bean by name
  * `type` → inject bean by type
* Mostly used in **Java EE environments**, but Spring supports it.

**Example:**

```java
@Resource(name = "myService")
private MyService myService;
```

**Key Difference vs @Autowired:**

* Resolves by **bean name first**, then by type.
* Part of Java EE standard (`JSR-250`).

---

## 🔹 **4. Comparison Table**

| Feature     | @Autowired                                | @Inject                     | @Resource                                    |
| ----------- | ----------------------------------------- | --------------------------- | -------------------------------------------- |
| Package     | Spring                                    | javax.inject                | javax.annotation                             |
| Type        | Spring-specific                           | JSR-330 (standard)          | JSR-250 (standard)                           |
| Injection   | By type (default), by name via @Qualifier | By type                     | By name (default), by type if no name)       |
| Required    | `required=true/false`                     | No attribute (use Optional) | No attribute (throws exception if not found) |
| Portability | Spring only                               | Standard, portable          | Standard, portable                           |

---

## 🔹 **5. Key Points / Interview Tips**

1. **`@Autowired`** → Spring-specific, most common in Spring projects.
2. **`@Inject`** → Standard JSR-330, portable to other DI frameworks.
3. **`@Resource`** → Java EE style, injects **by name** by default.
4. For **optional dependencies**, use:

   * `@Autowired(required=false)`
   * `@Inject Optional<>`
5. When multiple beans exist:

   * Use `@Qualifier` with `@Autowired` or `@Inject`
   * Use `name` attribute with `@Resource`

---

💡 **Quick Rule of Thumb for Interviews:**

* **By type → @Autowired / @Inject**
* **By name → @Resource**
* **Spring-specific features → @Autowired**

---

If you want, I can make a **diagram showing how @Autowired, @Inject, and @Resource resolve dependencies**, which is very helpful for **whiteboard explanations in interviews**.

Do you want me to make that diagram?

---

## 178. Can you inject a prototype bean into a singleton? How?

Absolutely, Aditya! This is a **classic Spring question** and an important concept for **bean scopes**. Let’s break it down clearly.

---

## 🧠 **1. Problem Statement**

* **Singleton bean:** Created **once per Spring container**, same instance shared.
* **Prototype bean:** Created **every time it’s requested** from the container.

**Issue:**
If you inject a **prototype bean directly** into a **singleton**, Spring will inject it **only once at singleton creation time**.

* Singleton will **always use the same prototype instance**, defeating the purpose of “prototype” scope.

---

## ⚙️ **2. Solution: How to inject prototype into singleton**

Spring provides multiple ways:

---

### **A. Using `@Lookup` Annotation (Recommended)**

* `@Lookup` tells Spring: **get a new instance from container every time this method is called**.

```java
@Component
@Scope("singleton")
public class SingletonBean {

    @Lookup
    public PrototypeBean getPrototypeBean() {
        // Spring will override this method to return a new PrototypeBean each time
        return null;
    }

    public void doSomething() {
        PrototypeBean prototype = getPrototypeBean();
        System.out.println(prototype);
    }
}

@Component
@Scope("prototype")
public class PrototypeBean { }
```

**Behavior:**

* Each call to `doSomething()` returns a **new PrototypeBean instance**.

---

### **B. Using `ObjectFactory` or `Provider`**

#### **1. Using `ObjectFactory`**

```java
@Component
@Scope("singleton")
public class SingletonBean {

    @Autowired
    private ObjectFactory<PrototypeBean> prototypeBeanFactory;

    public void doSomething() {
        PrototypeBean prototype = prototypeBeanFactory.getObject();
        System.out.println(prototype);
    }
}
```

#### **2. Using `javax.inject.Provider` (JSR-330)**

```java
@Component
@Scope("singleton")
public class SingletonBean {

    @Inject
    private Provider<PrototypeBean> prototypeProvider;

    public void doSomething() {
        PrototypeBean prototype = prototypeProvider.get();
        System.out.println(prototype);
    }
}
```

* Both approaches **fetch a new prototype instance each time**.

---

### **C. Manual ApplicationContext Lookup (Not recommended)**

```java
@Autowired
private ApplicationContext context;

public void doSomething() {
    PrototypeBean prototype = context.getBean(PrototypeBean.class);
}
```

* Works, but **tight-couples your bean to Spring**. Less clean.

---

## 🔹 **3. Key Points / Interview Tips**

1. Direct injection into singleton → **prototype behaves like singleton**.
2. Use **`@Lookup`**, **`ObjectFactory`**, or **`Provider`** for proper prototype injection.
3. Avoid **manual ApplicationContext lookup** unless necessary.
4. Explain **why prototype inside singleton is tricky** – singleton created only once, prototype injected once at that time.

---

💡 **Quick Analogy:**

* Singleton = **your coffee machine**
* Prototype = **coffee cup**
* If you pre-fill the singleton with one cup → you always get **the same cup**.
* Use `@Lookup` / factory → **new cup each time** you press the button.

---

If you want, I can make a **diagram showing singleton calling prototype via @Lookup / ObjectFactory**, which is **super helpful for visual explanation in interviews**.

Do you want me to make that diagram?

---

## 179. What is the default scope of a bean in Spring?

The **default scope of a Spring bean** is:

---

## **1. Singleton Scope (Default)**

* **Definition:** Spring creates **only one instance** of the bean per **Spring IoC container**.
* **Behavior:**

  * Every request for the bean returns the **same instance**.
  * The bean is **created at container startup** (eager initialization) unless lazy-initialized.
* **Annotation / XML:**

  ```java
  @Component
  public class MyBean { }
  ```

  * By default, this bean is a **singleton**.

---

### **2. Other Bean Scopes (for reference)**

| Scope         | Description                                                        |
| ------------- | ------------------------------------------------------------------ |
| `prototype`   | New instance created **every time it’s requested** from container. |
| `request`     | One instance per **HTTP request** (Web applications).              |
| `session`     | One instance per **HTTP session** (Web applications).              |
| `application` | One instance per **ServletContext** (Web applications).            |
| `websocket`   | One instance per **WebSocket session**.                            |

---

### **3. Key Points / Interview Tips**

* Default = **singleton** → most commonly used.
* Singleton beans are **thread-safe** only if they are stateless.
* Prototype beans are **created on demand**.
* Use **`@Scope("prototype")`** or XML `<bean scope="prototype">` to change the default.

---

💡 **Analogy:**

* **Singleton bean:** Like a **shared office printer** → everyone uses the same instance.
* **Prototype bean:** Like a **personal notebook** → each person gets a new one.

---

Do you want me to also explain **how Spring handles singleton beans in multi-threaded environments**? It’s often asked in interviews.

---

## 180. How do you create custom auto-configuration?

Absolutely, Aditya! Creating **custom auto-configuration** in Spring Boot is a key topic, especially for **Spring Boot starters**. Let’s break it down step by step.

---

## 🧠 **1. What is Auto-Configuration?**

* Spring Boot **auto-configuration** automatically configures your Spring application based on **classpath, beans, properties**.
* Example: Adding `spring-boot-starter-data-jpa` → Spring Boot automatically configures `DataSource`, `EntityManagerFactory`, etc.

**Custom auto-configuration** allows you to **provide similar automatic configuration** for your own modules or libraries.

---

## ⚙️ **2. Steps to Create Custom Auto-Configuration**

### **Step 1: Create Configuration Class**

* Annotate with `@Configuration`.
* Use `@ConditionalOn...` annotations to make it conditional.

```java
package com.example.autoconfig;

import org.springframework.boot.autoconfigure.condition.ConditionalOnClass;
import org.springframework.boot.autoconfigure.condition.ConditionalOnMissingBean;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

@Configuration
@ConditionalOnClass(MyService.class)  // Only configure if MyService is on classpath
public class MyAutoConfiguration {

    @Bean
    @ConditionalOnMissingBean  // Only create if no other MyService bean exists
    public MyService myService() {
        return new MyService();
    }
}
```

---

### **Step 2: Create `spring.factories` file**

* Location: `src/main/resources/META-INF/spring.factories`
* Register your auto-configuration class:

```
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.example.autoconfig.MyAutoConfiguration
```

* Spring Boot **scans `spring.factories`** at startup and loads your auto-configuration.

---

### **Step 3: Add Properties (Optional)**

* You can create **custom properties** for your auto-config:

```java
@ConfigurationProperties(prefix = "my.service")
public class MyServiceProperties {
    private String name = "DefaultName";
    // getters & setters
}
```

* Bind properties in your auto-configuration:

```java
@Bean
@ConditionalOnMissingBean
public MyService myService(MyServiceProperties properties) {
    return new MyService(properties.getName());
}
```

---

### **Step 4: Test Your Auto-Configuration**

* Include your library/jar in a Spring Boot app.
* Configure via `application.properties`:

```
my.service.name=CustomService
```

* Verify that the **bean is automatically created**.

---

## 🔹 **3. Common Conditional Annotations**

| Annotation                  | Purpose                                      |
| --------------------------- | -------------------------------------------- |
| `@ConditionalOnClass`       | Configure if a class is present on classpath |
| `@ConditionalOnMissingBean` | Configure only if no other bean exists       |
| `@ConditionalOnProperty`    | Configure if a property is set (or missing)  |
| `@ConditionalOnExpression`  | Configure based on SpEL expression           |

---

### **4. Summary / Interview Tips**

* **Custom auto-configuration** = reusable Spring Boot feature that configures beans automatically.
* Key parts:

  1. `@Configuration` class
  2. Conditional annotations (`@ConditionalOnClass`, `@ConditionalOnMissingBean`)
  3. `spring.factories` registration
  4. Optional properties with `@ConfigurationProperties`
* Always explain **why conditional checks are needed** – avoid overriding user-defined beans.

---

💡 **Analogy:**

* Spring Boot auto-config = **smart assistant**.
* Custom auto-config = **teach your assistant** how to automatically set up your custom module when needed.

---

If you want, I can make a **diagram showing the flow of Spring Boot custom auto-configuration** from classpath scanning → conditional checks → bean creation → application usage. This is **very useful for interviews and whiteboard explanations**.

Do you want me to make that diagram?

---

## 181. What is @Spring Boot Actuator? Important endpoints?

Absolutely, Aditya! Let’s dive into **Spring Boot Actuator**—one of the most important features for **monitoring and managing Spring Boot applications**.

---

## 🧠 **1. What is Spring Boot Actuator?**

* **Definition:** Actuator provides **production-ready features** to monitor and manage your Spring Boot application.

* **Purpose:**

  * Expose metrics, health, and environment info
  * Enable application monitoring
  * Support management via HTTP, JMX, or custom endpoints

* **Dependency:**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

---

## ⚙️ **2. Key Features of Actuator**

1. **Health checks** – check if application is up.
2. **Metrics** – CPU, memory, GC, HTTP requests, datasource, etc.
3. **Environment** – access properties, environment variables, and configs.
4. **Application info** – version, build info.
5. **Auditing** – track events.
6. **Thread dumps** – for debugging.
7. **Custom endpoints** – define your own actuator endpoints.

---

## 🔹 **3. Important Endpoints**

By default, only `/actuator/health` and `/actuator/info` are enabled. You can enable others in **`application.properties`**:

```properties
management.endpoints.web.exposure.include=health,info,metrics,httptrace,beans,env
```

| Endpoint               | Description                                                                |
| ---------------------- | -------------------------------------------------------------------------- |
| `/actuator/health`     | Shows application health status (`UP`, `DOWN`)                             |
| `/actuator/info`       | Application info (version, description)                                    |
| `/actuator/metrics`    | Application metrics like memory, CPU, threads, HTTP requests               |
| `/actuator/httptrace`  | Shows last 100 HTTP requests (needs dependency: `spring-boot-starter-web`) |
| `/actuator/beans`      | Lists all Spring beans in context                                          |
| `/actuator/env`        | Shows environment properties, system variables                             |
| `/actuator/mappings`   | Shows all request mappings                                                 |
| `/actuator/loggers`    | View and modify logging levels at runtime                                  |
| `/actuator/threaddump` | Thread dump for debugging deadlocks                                        |

---

## ⚙️ **4. Custom Endpoints**

You can **create your own actuator endpoint**:

```java
import org.springframework.boot.actuate.endpoint.annotation.Endpoint;
import org.springframework.boot.actuate.endpoint.annotation.ReadOperation;
import org.springframework.stereotype.Component;

@Component
@Endpoint(id = "custom")
public class CustomEndpoint {

    @ReadOperation
    public String customEndpoint() {
        return "Hello, this is a custom actuator endpoint!";
    }
}
```

* Accessible at: `/actuator/custom`

---

## 🔹 **5. Security Considerations**

* Sensitive endpoints like `/actuator/env`, `/actuator/loggers`, `/actuator/shutdown` should be **secured**.
* Example: `application.properties`

```properties
management.endpoints.web.exposure.include=health,info,metrics
management.endpoints.web.exposure.exclude=env,shutdown
management.endpoint.health.show-details=always
```

---

## 🔹 **6. Key Points / Interview Tips**

1. **Actuator = production-ready monitoring & management**.
2. Important endpoints: **health, info, metrics, beans, env, threaddump, loggers**.
3. Can **create custom endpoints** for specific needs.
4. **Secure sensitive endpoints** before exposing to the network.
5. Useful in combination with **Spring Boot Admin, Prometheus, Grafana** for monitoring dashboards.

---

💡 **Analogy:**

* Actuator = **dashboard for your car**
* Shows **health, fuel, speed, engine stats**
* Lets you **diagnose problems** without opening the hood

---

If you want, I can make a **diagram showing Spring Boot app + actuator endpoints + monitoring flow**, which is excellent for **interview whiteboards**.

Do you want me to make that diagram?

---

## 182. How do you implement custom health checks?

Absolutely, Aditya! Implementing **custom health checks** in Spring Boot Actuator is a common interview topic, especially for **production-ready applications**. Let’s go step by step.

---

## 🧠 **1. What is a Health Indicator?**

* Spring Boot Actuator provides **`HealthIndicator`** interface to expose health information.
* Default examples: `/actuator/health` already shows **disk space, DB connection, etc.**
* **Custom health indicators** allow you to check the health of your own services or dependencies.

---

## ⚙️ **2. Implementing a Custom Health Check**

### **Step 1: Implement `HealthIndicator` Interface**

```java
import org.springframework.boot.actuate.health.Health;
import org.springframework.boot.actuate.health.HealthIndicator;
import org.springframework.stereotype.Component;

@Component
public class MyServiceHealthIndicator implements HealthIndicator {

    @Override
    public Health health() {
        // Custom logic to check service health
        boolean serviceUp = checkMyService(); // replace with actual check

        if (serviceUp) {
            return Health.up().withDetail("MyService", "Available").build();
        } else {
            return Health.down().withDetail("MyService", "Not Available").build();
        }
    }

    private boolean checkMyService() {
        // Example: check database, external API, or other dependency
        return true; 
    }
}
```

* This automatically adds a new entry under `/actuator/health`.
* Output example:

```json
{
  "status": "UP",
  "components": {
    "myServiceHealthIndicator": {
      "status": "UP",
      "details": {
        "MyService": "Available"
      }
    }
  }
}
```

---

### **Step 2: Optional – Use `CompositeHealthIndicator`**

* If you have **multiple custom health indicators**, Spring Boot automatically aggregates them.
* The main `/actuator/health` endpoint will show a **combined status** (`UP` if all are up, `DOWN` if any are down).

---

### **Step 3: Enable Health Details (Optional)**

In `application.properties`:

```properties
management.endpoint.health.show-details=always
```

* By default, **detailed info is hidden** in production for security reasons.

---

## 🔹 **3. Conditional Health Checks**

* You can add **conditional checks** using `@ConditionalOnProperty`:

```java
@Component
@ConditionalOnProperty(name="my.service.health.enabled", havingValue="true", matchIfMissing=true)
public class MyServiceHealthIndicator implements HealthIndicator { ... }
```

* Useful for **feature toggles or optional services**.

---

## 🔹 **4. Key Points / Interview Tips**

1. Custom health checks = implement **`HealthIndicator`**.
2. Return **`Health.up()`** or **`Health.down()`**, optionally with `.withDetail()`.
3. Spring Boot aggregates multiple indicators automatically.
4. Use **`@ConditionalOnProperty`** for optional health checks.
5. Secure actuator endpoints in production (`/actuator/health`, `/actuator/info`).

---

💡 **Analogy:**

* Default health indicators = **car engine, battery, fuel level**
* Custom health indicator = **check your custom GPS module or air conditioning system**

---

If you want, I can make a **diagram showing how a custom HealthIndicator integrates into /actuator/health** for a visual explanation, perfect for interviews.

Do you want me to make that diagram?

---

## 183. What is @ConditionalOnProperty, @ConditionalOnClass?

Absolutely, Aditya! These are **key Spring Boot conditional annotations** used in **auto-configuration**. Let’s break them down clearly.

---

## 🧠 **1. @ConditionalOnProperty**

* **Package:** `org.springframework.boot.autoconfigure.condition.ConditionalOnProperty`
* **Purpose:** Enables or disables a **bean or configuration** based on the presence and value of a **property** in `application.properties` or `application.yml`.
* **Common use case:** Feature toggles, enabling/disabling optional beans in auto-configuration.

### **Attributes:**

| Attribute        | Description                                            |
| ---------------- | ------------------------------------------------------ |
| `name`           | Name of the property to check                          |
| `havingValue`    | Only match if property value equals this               |
| `matchIfMissing` | If `true`, bean is created even if property is missing |

### **Example:**

```java
@Configuration
@ConditionalOnProperty(name = "feature.email.enabled", havingValue = "true", matchIfMissing = false)
public class EmailServiceAutoConfiguration {

    @Bean
    public EmailService emailService() {
        return new EmailService();
    }
}
```

* If `feature.email.enabled=true` → `EmailService` bean is created.
* If property missing or false → bean not created.

---

## 🧠 **2. @ConditionalOnClass**

* **Package:** `org.springframework.boot.autoconfigure.condition.ConditionalOnClass`
* **Purpose:** Enables a **bean or configuration** only if a **specific class exists on the classpath**.
* **Common use case:** Auto-configuration of optional dependencies like Redis, Kafka, or JPA.

### **Example:**

```java
@Configuration
@ConditionalOnClass(name = "org.springframework.data.redis.core.RedisTemplate")
public class RedisAutoConfiguration {

    @Bean
    public RedisService redisService() {
        return new RedisService();
    }
}
```

* If `RedisTemplate` class exists → `RedisService` bean is created.
* If Redis dependency is missing → bean is **not created**, no errors thrown.

---

## 🔹 **3. Key Differences**

| Feature  | @ConditionalOnProperty          | @ConditionalOnClass                         |
| -------- | ------------------------------- | ------------------------------------------- |
| Checks   | Property value in configuration | Class presence in classpath                 |
| Use case | Feature toggle, optional config | Auto-configure beans for optional libraries |
| Trigger  | Configurable by name/value      | Library dependency check                    |

---

## 🔹 **4. Common Interview Tips**

1. Both are widely used in **Spring Boot Auto-Configuration**.
2. `@ConditionalOnProperty` → **feature flags or config-based conditions**.
3. `@ConditionalOnClass` → **library existence check**.
4. Often combined:

```java
@Configuration
@ConditionalOnClass(RedisTemplate.class)
@ConditionalOnProperty(name="redis.enabled", havingValue="true", matchIfMissing=true)
public class RedisAutoConfiguration { ... }
```

* Redis beans created **only if Redis library exists and property enabled**.

---

💡 **Analogy:**

* `@ConditionalOnClass` = “Does the toolbox have this tool?” → only then configure.
* `@ConditionalOnProperty` = “Is this feature turned on in settings?” → only then configure.

---

If you want, I can make a **diagram showing how @ConditionalOnClass and @ConditionalOnProperty control bean creation**—very handy for **interview whiteboards**.

Do you want me to make that diagram?

---

## 184. How do you implement custom metrics and monitoring?

Absolutely, Aditya! Implementing **custom metrics and monitoring** in Spring Boot is an important topic, especially for **production-ready applications**. Let’s break it down step by step.

---

## 🧠 **1. What is Metrics in Spring Boot?**

* Spring Boot Actuator exposes **application metrics** via **Micrometer** (default metrics library).

* Metrics include:

  * JVM (memory, threads, GC)
  * HTTP requests
  * Data source (DB connection pool)
  * Custom business metrics

* Exposed via:

  * `/actuator/metrics` endpoint
  * Monitoring tools like **Prometheus, Grafana, New Relic**

---

## ⚙️ **2. Adding Custom Metrics**

Spring Boot provides **`MeterRegistry`** for creating custom metrics.

### **Step 1: Add dependencies**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

<!-- Optional for Prometheus -->
<dependency>
    <groupId>io.micrometer</groupId>
    <artifactId>micrometer-registry-prometheus</artifactId>
</dependency>
```

---

### **Step 2: Inject `MeterRegistry`**

```java
import io.micrometer.core.instrument.Counter;
import io.micrometer.core.instrument.MeterRegistry;
import org.springframework.stereotype.Component;

@Component
public class CustomMetrics {

    private final Counter orderCounter;

    public CustomMetrics(MeterRegistry registry) {
        this.orderCounter = Counter.builder("orders.processed")
                                   .description("Number of orders processed")
                                   .register(registry);
    }

    public void incrementOrderCount() {
        orderCounter.increment();
    }
}
```

* `orders.processed` metric now appears in `/actuator/metrics/orders.processed`.

---

### **Step 3: Use Metrics in Code**

```java
@Service
public class OrderService {

    private final CustomMetrics customMetrics;

    public OrderService(CustomMetrics customMetrics) {
        this.customMetrics = customMetrics;
    }

    public void processOrder(Order order) {
        // Business logic
        customMetrics.incrementOrderCount(); // increment custom metric
    }
}
```

---

## 🔹 **3. Creating Gauges and Timers**

* **Gauge:** Measures **current value** (e.g., queue size, cache size)

```java
Gauge.builder("queue.size", myQueue, q -> q.size())
     .description("Size of the order queue")
     .register(registry);
```

* **Timer:** Measures **duration of operations**

```java
Timer timer = Timer.builder("order.processing.time")
                   .description("Time taken to process an order")
                   .register(registry);

timer.record(() -> orderService.processOrder(order));
```

* **DistributionSummary:** Measures **distribution of values**

```java
DistributionSummary summary = DistributionSummary.builder("order.amount")
                                                 .description("Order amount distribution")
                                                 .register(registry);
summary.record(order.getAmount());
```

---

## 🔹 **4. Expose Metrics**

* Default actuator metrics: `/actuator/metrics`
* Specific metric: `/actuator/metrics/orders.processed`
* Can integrate with **Prometheus/Grafana** for dashboards.

---

## 🔹 **5. Key Points / Interview Tips**

1. Use **Micrometer** via `MeterRegistry` for custom metrics.
2. Common metric types:

   * **Counter** → increment-only counts
   * **Gauge** → current value snapshot
   * **Timer** → duration of events
   * **DistributionSummary** → statistical distribution
3. Always **name metrics properly** (use dot notation, e.g., `orders.processed`).
4. Integrate with **Prometheus/Grafana** for monitoring dashboards.
5. Custom metrics **help in production monitoring and alerting**.

---

💡 **Analogy:**

* Counter = counting **number of cars passing a toll gate**
* Gauge = current **temperature of engine**
* Timer = **time taken for a car to cross the toll gate**
* DistributionSummary = **distribution of car weights**

---

If you want, I can make a **diagram showing custom metrics flow in Spring Boot using Micrometer → Actuator → Prometheus/Grafana**, which is **perfect for interviews**.

Do you want me to make that diagram?

---

## 185. What are the Scopes in Spring?

Absolutely, Aditya! **Bean scopes in Spring** define the **lifecycle and visibility of beans** within the Spring container. Let’s go through them in detail.

---

## 🧠 **1. Overview**

* A **bean scope** determines **how many instances of a bean are created** and **how long they live**.
* Spring supports **both standard and web-specific scopes**.

---

## ⚙️ **2. Standard Bean Scopes**

| Scope                   | Description                                                                                                    | Annotation / XML        |
| ----------------------- | -------------------------------------------------------------------------------------------------------------- | ----------------------- |
| **singleton** (default) | **One shared instance per Spring container**. Created at container startup (eager initialization unless lazy). | `@Scope("singleton")`   |
| **prototype**           | **New instance every time** it is requested from the container. Spring does **not manage the full lifecycle**. | `@Scope("prototype")`   |
| **request**             | One instance per **HTTP request**. Only valid in **WebApplicationContext**.                                    | `@Scope("request")`     |
| **session**             | One instance per **HTTP session**. Only valid in **WebApplicationContext**.                                    | `@Scope("session")`     |
| **application**         | One instance per **ServletContext**. Useful for web apps.                                                      | `@Scope("application")` |
| **websocket**           | One instance per **WebSocket session**.                                                                        | `@Scope("websocket")`   |

---

## ⚙️ **3. Examples**

### **Singleton Bean (default)**

```java
@Component
public class SingletonBean { }
```

* **Same instance** every time you `@Autowired` it.

### **Prototype Bean**

```java
@Component
@Scope("prototype")
public class PrototypeBean { }
```

* New instance **each time** you `getBean()` from the container.

### **Request Bean (Web context)**

```java
@Component
@Scope("request")
public class RequestBean { }
```

* New bean **per HTTP request**.

---

## ⚙️ **4. Important Points**

1. **Singleton beans** injected with **prototype beans** → prototype behaves like singleton unless **@Lookup / ObjectFactory / Provider** is used.
2. **Request/session/application/websocket** scopes are **only available in web contexts**.
3. Use `@Lazy` to **delay singleton bean creation** until first request.
4. Prototype beans → Spring **does not manage destruction callbacks**.

---

## 🔹 **5. Summary / Interview Tips**

* Default = **singleton**.
* **Prototype** = new instance each time.
* Web-specific scopes: **request, session, application, websocket**.
* Singleton + prototype = **careful with injection**.
* Good to know for **multi-threading and web applications**.

---

💡 **Analogy:**

* **Singleton** = office printer → everyone uses the same one.
* **Prototype** = personal notebook → each person gets a new one.
* **Request** = takeout coffee cup → new cup for each customer.
* **Session** = shopping cart → persists during your session.
* **Application** = shared water cooler → one per office building.

---

If you want, I can make a **diagram showing all Spring bean scopes with lifecycle and usage examples**, which is **super useful for interviews and whiteboards**.

Do you want me to make that diagram?

---

## 186. Prototype vs Request Scope?

Absolutely, Aditya! Let’s carefully compare **Prototype** and **Request** scopes in Spring. They are often confused because both create **new instances**, but the contexts are different.

---

## **1. Prototype Scope**

* **Definition:** Spring creates a **new instance every time** the bean is requested from the container.
* **Context:** Works in **any Spring context** (web or non-web).
* **Lifecycle:** Spring **does not manage full lifecycle** (no destruction callbacks).
* **Usage:** For beans where **state should not be shared** between requests or usages.

### **Example:**

```java
@Component
@Scope("prototype")
public class PrototypeBean { }
```

```java
@Autowired
private PrototypeBean prototypeBean1;

@Autowired
private PrototypeBean prototypeBean2;

// prototypeBean1 != prototypeBean2
```

* Each injection or call to `getBean()` returns a **new instance**.

---

## **2. Request Scope**

* **Definition:** Spring creates a **new instance per HTTP request**.
* **Context:** Only valid in **WebApplicationContext** (web applications).
* **Lifecycle:** Managed by Spring for the duration of the **HTTP request**.
* **Usage:** For beans that should **store request-specific state**, e.g., user session data, request parameters.

### **Example:**

```java
@Component
@Scope("request")
public class RequestBean { }
```

* Each HTTP request gets a **new instance**, but within the same request, the same bean is **reused**.

---

## **3. Key Differences**

| Feature            | Prototype                     | Request                                 |
| ------------------ | ----------------------------- | --------------------------------------- |
| Bean creation      | Every time requested          | Once per HTTP request                   |
| Scope              | Any Spring context            | Only WebApplicationContext              |
| Lifecycle          | Not fully managed             | Fully managed (destroyed after request) |
| Typical use        | Stateless beans, utilities    | Request-specific state, user info       |
| Injection behavior | Each injection = new instance | Same request → same instance            |

---

### **4. Example Scenario**

* **Prototype:** `NotificationService` → each service instance has temporary state and is independent.
* **Request:** `UserRequestContext` → stores current user info during a web request; all components in the same request see the **same instance**.

---

💡 **Analogy:**

* **Prototype:** Like a **fresh notebook** every time you need one.
* **Request:** Like a **coffee cup for a customer** → new cup per customer, but same cup used throughout their visit.

---

If you want, I can make a **diagram showing Prototype vs Request scope with bean lifecycle and web request mapping**, which is **super handy for interviews and whiteboards**.

Do you want me to make that diagram?

---