# LEVEL 3: ADVANCED (4+ Years Experience)

# Advanced AOP

## 187. What is AOP and how is it implemented in Spring Boot?

Absolutely, Aditya! Let’s dive into **AOP (Aspect-Oriented Programming)** and how it works in Spring Boot.

---

## 🧠 **1. What is AOP?**

* **Definition:** AOP allows you to **separate cross-cutting concerns** (like logging, security, transactions) from the **business logic**.
* **Goal:** Keep your code **modular and clean**.

**Cross-cutting concerns examples:**

* Logging
* Security checks
* Transaction management
* Performance monitoring

**Analogy:** Think of AOP as **“intercepting the method calls to add extra behavior”**, like a **security guard checking every entry** without changing the actual business logic.

---

## 🧠 **2. Core Concepts of AOP**

| Term           | Description                                                            |
| -------------- | ---------------------------------------------------------------------- |
| **Aspect**     | Module containing cross-cutting concern (like LoggingAspect)           |
| **Join Point** | Point in program execution (like method execution)                     |
| **Advice**     | Action taken at a join point (before, after, around)                   |
| **Pointcut**   | Expression that selects join points                                    |
| **Weaving**    | Linking aspects with target objects (compile-time, load-time, runtime) |

---

## 🧠 **3. Types of Advice**

| Type                | When It Executes                               |
| ------------------- | ---------------------------------------------- |
| **@Before**         | Before method execution                        |
| **@After**          | After method execution (regardless of outcome) |
| **@AfterReturning** | After method returns successfully              |
| **@AfterThrowing**  | If method throws exception                     |
| **@Around**         | Wraps method execution (before + after)        |

---

## ⚙️ **4. How AOP is Implemented in Spring Boot**

### **Step 1: Add dependency**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

### **Step 2: Enable AspectJ support**

* Spring Boot auto-configures AOP if starter is included.
* Or explicitly:

```java
@EnableAspectJAutoProxy
@SpringBootApplication
public class MyApplication { }
```

---

### **Step 3: Create an Aspect**

```java
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.service.*.*(..))")
    public void logBeforeMethod() {
        System.out.println("A method in service package is about to execute...");
    }
}
```

**Explanation:**

* `@Aspect` → marks as an aspect class
* `@Before("execution(* com.example.service.*.*(..))")` → pointcut expression targeting **all methods in service package**

---

### **Step 4: Around Advice Example**

```java
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;

@Around("execution(* com.example.service.*.*(..))")
public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
    long start = System.currentTimeMillis();
    Object result = joinPoint.proceed();
    long end = System.currentTimeMillis();
    System.out.println(joinPoint.getSignature() + " executed in " + (end - start) + "ms");
    return result;
}
```

* `@Around` allows **pre-processing and post-processing** of method execution.
* Can also **modify return values** or **handle exceptions**.

---

## 🔹 **5. Advantages of AOP**

1. **Separation of concerns** → cleaner business logic.
2. **Reusable aspects** → logging, security, transaction management.
3. **Maintainable** → change the aspect in one place for multiple classes.
4. **Declarative programming** → add behavior without modifying code.

---

## 🔹 **6. Common Use Cases in Spring Boot**

* Logging (performance, debug info)
* Security checks (@PreAuthorize, role checks)
* Transaction management (@Transactional uses AOP internally)
* Metrics collection
* Exception handling / auditing

---

💡 **Analogy:**

* Business method = **chef cooking food**
* Aspect = **fire alarm system** → monitors without touching the chef
* Advice = **alarm triggers before or after cooking**

---

If you want, I can make a **diagram showing AOP in Spring Boot**: `Aspect -> Join Point -> Advice -> Target Method`, which is **very useful for interviews and whiteboards**.

Do you want me to make that diagram?

---

## 188. Explain @Before, @After, @Around, @AfterRunning, @AfterThrowing advices.

Absolutely, Aditya! Let’s break down the **types of AOP advices in Spring** with clear explanations, examples, and usage.

---

## **1. @Before Advice**

* **Runs:** **Before the method execution**.
* **Use case:** Logging, security checks, validation.
* **Syntax:**

```java
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.service.*.*(..))")
    public void logBefore() {
        System.out.println("Before method execution...");
    }
}
```

**Key Point:** Does not modify the method execution; only executes before the target method.

---

## **2. @After Advice**

* **Runs:** **After the method execution**, **regardless of its outcome** (success or exception).
* **Use case:** Resource cleanup, logging method completion.

```java
@After("execution(* com.example.service.*.*(..))")
public void logAfter() {
    System.out.println("After method execution...");
}
```

**Key Point:** Always executes, even if an exception occurs.

---

## **3. @AfterReturning Advice**

* **Runs:** **Only after method successfully returns** (no exception).
* **Use case:** Logging return values, post-processing results.

```java
@AfterReturning(
    pointcut = "execution(* com.example.service.*.*(..))",
    returning = "result"
)
public void logAfterReturning(Object result) {
    System.out.println("Method returned value: " + result);
}
```

**Key Point:** You can **capture the return value** and use it in the advice.

---

## **4. @AfterThrowing Advice**

* **Runs:** **Only if method throws an exception**.
* **Use case:** Logging errors, sending alerts, exception monitoring.

```java
@AfterThrowing(
    pointcut = "execution(* com.example.service.*.*(..))",
    throwing = "ex"
)
public void logAfterThrowing(Exception ex) {
    System.out.println("Method threw exception: " + ex.getMessage());
}
```

**Key Point:** You can **capture the thrown exception** and handle it.

---

## **5. @Around Advice**

* **Runs:** **Before and after the method execution**; can **control execution**.
* **Use case:** Performance monitoring, modifying return value, exception handling.

```java
@Around("execution(* com.example.service.*.*(..))")
public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
    long start = System.currentTimeMillis();
    Object result = joinPoint.proceed(); // execute the method
    long end = System.currentTimeMillis();
    System.out.println(joinPoint.getSignature() + " executed in " + (end - start) + "ms");
    return result;
}
```

**Key Points:**

* Can **control whether the target method executes**.
* Can **modify return value or handle exceptions**.

---

## **6. Quick Summary Table**

| Advice Type         | When it Runs               | Can Access Result | Can Access Exception | Can Control Execution |
| ------------------- | -------------------------- | ----------------- | -------------------- | --------------------- |
| **@Before**         | Before method              | ❌                 | ❌                    | ❌                     |
| **@After**          | After method (any outcome) | ❌                 | ❌                    | ❌                     |
| **@AfterReturning** | After successful execution | ✅                 | ❌                    | ❌                     |
| **@AfterThrowing**  | After exception            | ❌                 | ✅                    | ❌                     |
| **@Around**         | Before + after             | ✅                 | ✅                    | ✅                     |

---

💡 **Analogy:**

* `@Before` → knock on the door **before entering**.
* `@After` → say goodbye **after leaving**.
* `@AfterReturning` → comment on **what was achieved inside**.
* `@AfterThrowing` → react to **something going wrong inside**.
* `@Around` → **escort them in and out**, timing the visit, controlling actions.

---

If you want, I can create a **diagram showing all advices with method execution timeline**, which is **super useful for interviews and whiteboards**.

Do you want me to make that diagram?

---

## 189. What is a Pointcut and how do you define it?

Absolutely, Aditya! Let’s dive into **Pointcuts in Spring AOP**.

---

## 🧠 **1. What is a Pointcut?**

* **Definition:** A **Pointcut** is an **expression that matches one or more join points** (places in the code where advice can be applied, e.g., method executions).
* **Purpose:** It **selects the methods** where the advice should be executed.
* Essentially, it defines the **“where”** in the code your aspect logic applies.

---

## 🧠 **2. Components of Pointcut**

| Term           | Description                                                                      |
| -------------- | -------------------------------------------------------------------------------- |
| **Join Point** | A specific point in program execution (e.g., method call, constructor execution) |
| **Advice**     | Action taken at a join point (e.g., logging, security)                           |
| **Pointcut**   | Expression that selects join points for the advice                               |

---

## 🧠 **3. How to Define Pointcuts**

### **Option 1: Inline in Advice**

```java
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.service.*.*(..))")
    public void logBeforeMethod() {
        System.out.println("Before method execution in service package");
    }
}
```

* `execution(* com.example.service.*.*(..))` → Pointcut expression.

  * `*` → any return type
  * `com.example.service.*.*` → any class and any method in the package
  * `(..)` → any arguments

---

### **Option 2: Named Pointcut (Reusable)**

```java
@Aspect
@Component
public class LoggingAspect {

    // Define reusable pointcut
    @Pointcut("execution(* com.example.service.*.*(..))")
    public void serviceMethods() { }

    @Before("serviceMethods()")
    public void logBefore() {
        System.out.println("Before service method execution");
    }

    @After("serviceMethods()")
    public void logAfter() {
        System.out.println("After service method execution");
    }
}
```

* `@Pointcut` allows **reuse across multiple advices**.

---

## 🧠 **4. Common Pointcut Expressions**

| Expression                                                              | Meaning                                           |
| ----------------------------------------------------------------------- | ------------------------------------------------- |
| `execution(* com.example..*.*(..))`                                     | All methods in `com.example` and subpackages      |
| `within(com.example.service.*)`                                         | All methods in classes within the service package |
| `args(String)`                                                          | Methods with a single String argument             |
| `@annotation(org.springframework.transaction.annotation.Transactional)` | Methods annotated with `@Transactional`           |
| `bean(myBean)`                                                          | Methods in a specific Spring bean                 |

---

## 🧠 **5. Key Points / Interview Tips**

1. **Pointcut = Where advice applies**.
2. Use `execution()` for **method signature matching**.
3. Use `within()`, `args()`, `@annotation()` for **more precise targeting**.
4. Named `@Pointcut` → **reuse pointcut expressions**.
5. Combined with advice types → powerful, modular AOP.

---

💡 **Analogy:**

* Advice = what you want to do (e.g., log, monitor)
* Pointcut = **which doors or rooms to apply it to**

---

If you want, I can make a **diagram showing Pointcut → Join Points → Advice execution flow**, which is **super handy for interviews and whiteboards**.

Do you want me to make that diagram?

---

## 190. What is a joinPoint and what data can it provide?

Absolutely, Aditya! Let’s carefully explain **JoinPoint in Spring AOP** and what information it provides.

---

## 🧠 **1. What is a JoinPoint?**

* **Definition:** A **JoinPoint** represents a **specific point in the execution of a program** where an **advice can be applied**.

* Examples of join points:

  * Method execution
  * Constructor execution
  * Field access (in some AOP frameworks)

* **In Spring AOP:** JoinPoints are **always method executions**.

---

## 🧠 **2. JoinPoint vs Pointcut**

| Concept       | What it defines                                                                 |
| ------------- | ------------------------------------------------------------------------------- |
| **JoinPoint** | A **runtime point** where advice can be applied (method call)                   |
| **Pointcut**  | A **predicate/expression** that selects which join points the advice applies to |

* **Example:**

  * Pointcut: `execution(* com.example.service.*.*(..))` → selects all methods in service package
  * JoinPoint: Actual method `getUser()` in `UserService` during runtime

---

## 🧠 **3. Using JoinPoint in Advice**

You can inject `JoinPoint` into your advice methods to get **runtime information**:

```java
import org.aspectj.lang.JoinPoint;
import org.aspectj.lang.annotation.Before;
import org.aspectj.lang.annotation.Aspect;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.service.*.*(..))")
    public void logMethodDetails(JoinPoint joinPoint) {
        System.out.println("Method: " + joinPoint.getSignature());
        System.out.println("Target Class: " + joinPoint.getTarget().getClass().getName());
        System.out.println("Arguments: " + Arrays.toString(joinPoint.getArgs()));
    }
}
```

---

## 🧠 **4. Data Provided by JoinPoint**

| Method                               | What it Provides                                             |
| ------------------------------------ | ------------------------------------------------------------ |
| `getSignature()`                     | Method signature being called (name, return type, modifiers) |
| `getTarget()`                        | The **target object** (actual bean instance)                 |
| `getArgs()`                          | Method **arguments** as an Object array                      |
| `getThis()`                          | Proxy object calling the method                              |
| `toShortString()` / `toLongString()` | Readable method info                                         |
| `getKind()`                          | Kind of join point (`method-execution`)                      |

---

## 🧠 **5. Example Output**

Suppose we call:

```java
userService.createUser("Aditya", "admin");
```

**JoinPoint data:**

* `getSignature()` → `UserService.createUser(String,String)`
* `getTarget()` → `UserService@3f2a5`
* `getArgs()` → `[Aditya, admin]`
* `getThis()` → Spring proxy object

---

## 🔹 **6. Key Points / Interview Tips**

1. **JoinPoint = runtime info about the executing method**.
2. Can access **method name, arguments, target object, proxy object**.
3. Essential for **dynamic logging, auditing, or security checks**.
4. Often combined with `@Around` advice for **flexible control and monitoring**.

---

💡 **Analogy:**

* JoinPoint = **a snapshot of the action happening right now** (like a camera capturing the chef cooking).
* Pointcut = **deciding which kitchens to monitor**.
* Advice = **what you do with the snapshot** (log, alert, modify).

---

If you want, I can make a **diagram showing Pointcut → JoinPoint → Advice → Target Method** highlighting **all data JoinPoint provides**, which is excellent for interviews.

Do you want me to make that diagram?

---

## 191. How do you create custom annotations and intercept then using AOP?

Absolutely, Aditya! Let’s go step by step on **creating custom annotations in Spring and intercepting them using AOP**. This is a **common pattern for logging, security, or validation** in real-world projects.

---

## **1. Step 1: Create a Custom Annotation**

* Use `@interface` to define a custom annotation.
* Common meta-annotations:

  * `@Retention(RetentionPolicy.RUNTIME)` → available at runtime for AOP to read
  * `@Target(ElementType.METHOD)` → applicable to methods

### Example:

```java
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;
import java.lang.annotation.ElementType;

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface LogExecutionTime {
}
```

* **`@Retention(RUNTIME)`** → needed so Spring AOP can detect it at runtime.
* **`@Target(METHOD)`** → annotation can only be applied to methods.

---

## **2. Step 2: Apply Annotation to Methods**

```java
import org.springframework.stereotype.Service;

@Service
public class UserService {

    @LogExecutionTime
    public void createUser(String name) {
        // business logic
        System.out.println("Creating user: " + name);
    }
}
```

* Now, `createUser()` is marked with **`@LogExecutionTime`**.

---

## **3. Step 3: Create an Aspect to Intercept Annotation**

* Use `@Around` or `@Before`/`@After` advice.
* Pointcut expression: `@annotation(<your annotation class>)`

### Example using `@Around`:

```java
import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.springframework.stereotype.Component;

@Aspect
@Component
public class LoggingAspect {

    @Around("@annotation(com.example.annotations.LogExecutionTime)")
    public Object logExecutionTime(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();

        Object proceed = joinPoint.proceed(); // execute the method

        long executionTime = System.currentTimeMillis() - start;
        System.out.println(joinPoint.getSignature() + " executed in " + executionTime + "ms");

        return proceed;
    }
}
```

**Explanation:**

* `@Around("@annotation(com.example.annotations.LogExecutionTime)")` → intercepts **any method annotated with `@LogExecutionTime`**
* `joinPoint.proceed()` → executes the actual method
* You can log, measure execution time, or even modify return values

---

## **4. Step 4: Output Example**

When `userService.createUser("Aditya")` runs:

```
Creating user: Aditya
UserService.createUser executed in 25ms
```

* Business logic executes normally, but AOP **adds logging automatically**.

---

## **5. Benefits**

1. **Separation of concerns** → your business logic doesn’t include logging code.
2. **Reusable behavior** → annotate any method without repeating code.
3. **Flexible** → can intercept methods dynamically based on annotations.

---

## **6. Key Points / Interview Tips**

* Always use **`RUNTIME` retention** for AOP interception.
* Use `@annotation` pointcut expression for annotation-based aspects.
* Works well for **logging, metrics, validation, and security**.
* Can combine with **Spring’s `@Transactional` or custom annotations** for cleaner code.

---

💡 **Analogy:**

* Annotation = **sticky note on the method** saying “apply logging here.”
* Aspect = **the person reading the sticky note** and taking action (logging, timing, etc.).

---

If you want, I can make a **diagram showing Custom Annotation → Aspect → JoinPoint → Advice flow**, which is very useful for **interviews and whiteboard explanations**.

Do you want me to make that diagram?

---

## 192. Real-world use cases of AOP (logging, auditing, security, caching)

Absolutely, Aditya! Let’s explore **real-world use cases of AOP** in Spring Boot. These are very common in enterprise applications, and understanding them well is excellent for interviews.

---

## **1. Logging**

* **Problem:** Adding logging code in every method clutters business logic.
* **Solution:** Use AOP to log method execution **automatically**.

### Example:

```java
@Aspect
@Component
public class LoggingAspect {

    @Before("execution(* com.example.service.*.*(..))")
    public void logMethodCall(JoinPoint joinPoint) {
        System.out.println("Executing: " + joinPoint.getSignature());
    }
}
```

* Logs **every method call** in the service layer.
* Can log **method arguments, return values, and execution time**.

**Benefits:** Centralized logging without polluting code.

---

## **2. Auditing**

* **Problem:** Track **who did what and when** for compliance or reporting.
* **Solution:** Intercept methods and record **user actions**.

### Example:

```java
@Aspect
@Component
public class AuditAspect {

    @AfterReturning("execution(* com.example.service.UserService.*(..))")
    public void audit(JoinPoint joinPoint) {
        String username = SecurityContextHolder.getContext().getAuthentication().getName();
        System.out.println("User: " + username + " called method: " + joinPoint.getSignature());
    }
}
```

* Useful for **financial apps, HR systems, or sensitive operations**.

---

## **3. Security / Authorization Checks**

* **Problem:** Need to check **permissions** on sensitive methods.
* **Solution:** Apply **security logic centrally** using AOP instead of scattering checks.

### Example:

```java
@Aspect
@Component
public class SecurityAspect {

    @Before("@annotation(com.example.annotations.Secured)")
    public void checkSecurity(JoinPoint joinPoint) {
        // Custom logic to check user roles
        if (!currentUserHasPermission()) {
            throw new AccessDeniedException("User not authorized");
        }
    }
}
```

* Combine with **custom annotation `@Secured`** to mark protected methods.
* Spring Security also uses AOP internally for `@PreAuthorize` and `@PostAuthorize`.

---

## **4. Caching**

* **Problem:** Expensive operations like database queries or remote API calls need **caching**.
* **Solution:** Use AOP to **intercept method calls and cache results**.

### Example:

```java
@Aspect
@Component
public class CacheAspect {

    private Map<String, Object> cache = new HashMap<>();

    @Around("@annotation(com.example.annotations.Cacheable)")
    public Object cacheResult(ProceedingJoinPoint joinPoint) throws Throwable {
        String key = joinPoint.getSignature().toShortString() + Arrays.toString(joinPoint.getArgs());
        if (cache.containsKey(key)) {
            return cache.get(key);
        }
        Object result = joinPoint.proceed();
        cache.put(key, result);
        return result;
    }
}
```

* Avoids repetitive expensive computations.
* Spring’s `@Cacheable` uses a similar AOP mechanism internally.

---

## **5. Transaction Management**

* Spring’s `@Transactional` is implemented using AOP.
* Intercepts method calls and **manages transactions automatically**.

### Benefits of AOP in Transaction Management:

* Centralized management of transactions.
* Reduces boilerplate code for commit/rollback logic.

---

## **6. Performance Monitoring / Metrics**

* Measure **method execution times** to detect slow services.

```java
@Aspect
@Component
public class PerformanceAspect {

    @Around("execution(* com.example.service.*.*(..))")
    public Object measureTime(ProceedingJoinPoint joinPoint) throws Throwable {
        long start = System.currentTimeMillis();
        Object result = joinPoint.proceed();
        long end = System.currentTimeMillis();
        System.out.println(joinPoint.getSignature() + " executed in " + (end - start) + "ms");
        return result;
    }
}
```

* Helpful for **profiling and alerting in production systems**.

---

## **7. Key Advantages of Using AOP for Cross-Cutting Concerns**

1. **Separation of Concerns:** Keep business logic clean.
2. **Reusable Logic:** One aspect can be applied to multiple methods/classes.
3. **Maintainable Code:** Centralized updates for logging, security, caching, etc.
4. **Declarative Approach:** Use annotations like `@Cacheable`, `@Transactional`.

---

💡 **Analogy:**

* **Business logic** = chef cooking.
* **AOP aspects** = waiter, security guard, and auditor monitoring everything **without touching the chef**.

---

If you want, I can make a **diagram showing Logging, Security, Caching, Auditing aspects being applied to multiple service methods**, which is excellent for interviews and whiteboards.

Do you want me to make that diagram?

---