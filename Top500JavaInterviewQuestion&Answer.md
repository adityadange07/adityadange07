# Top 500 Java Backend Interview FAQs

---

# 1.Explain the diﬀerence between == and .equals() in Java.

---

In Java, `==` and `.equals()` are both used for comparison, but they serve **very different purposes**. This is a **very common interview question**, especially for Java developers and leads.

---

## 1️⃣ `==` Operator

### What it does

* Compares **references (memory addresses)** for objects
* Compares **actual values** for primitive data types

### Behavior

* Checks whether **both variables point to the same object in memory**
* Does **not** check logical/content equality for objects

### Example (Primitives)

```java
int a = 10;
int b = 10;

System.out.println(a == b); // true
```

✔ Because it compares actual values.

### Example (Objects)

```java
String s1 = new String("Java");
String s2 = new String("Java");

System.out.println(s1 == s2); // false
```

❌ Because `s1` and `s2` refer to **different objects** in memory.

---

## 2️⃣ `.equals()` Method

### What it does

* Compares **content (logical equality)** of objects
* Defined in `java.lang.Object` class
* Can be **overridden** by classes

### Default behavior

* In `Object` class, `.equals()` behaves like `==`
* Many classes override it to compare values (e.g., `String`, `Integer`)

### Example

```java
String s1 = new String("Java");
String s2 = new String("Java");

System.out.println(s1.equals(s2)); // true
```

✔ Because `String` overrides `.equals()` to compare character content.

---

## 3️⃣ Key Differences (Interview-Friendly Table)

| Feature           | `==`                                     | `.equals()`                       |
| ----------------- | ---------------------------------------- | --------------------------------- |
| Type              | Operator                                 | Method                            |
| Compares          | Reference (objects) / Value (primitives) | Object content (logical equality) |
| Can be overridden | ❌ No                                     | ✅ Yes                             |
| Used with         | Primitives & Objects                     | Objects only                      |
| Memory check      | ✅ Yes                                    | ❌ No (unless not overridden)      |

---

## 4️⃣ Custom Class Example (Very Important for Interviews)

```java
class Employee {
    int id;
    String name;

    Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }
}
```

```java
Employee e1 = new Employee(1, "Aditya");
Employee e2 = new Employee(1, "Aditya");

System.out.println(e1 == e2);        // false
System.out.println(e1.equals(e2));   // false
```

❌ Because `.equals()` is **not overridden**.

### Overriding `.equals()`

```java
@Override
public boolean equals(Object o) {
    if (this == o) return true;
    if (o == null || getClass() != o.getClass()) return false;
    Employee emp = (Employee) o;
    return id == emp.id && name.equals(emp.name);
}
```

✔ Now `.equals()` compares content correctly.

---

## 5️⃣ String Pool Special Case (Tricky Interview Point)

```java
String s1 = "Java";
String s2 = "Java";

System.out.println(s1 == s2);       // true
System.out.println(s1.equals(s2));  // true
```

✔ Because **String literals** are stored in the **String Pool** and reused.

---

## 6️⃣ One-Line Interview Answer (Perfect for Lead Round)

> "`==` compares reference equality for objects and value equality for primitives, whereas `.equals()` compares logical/content equality of objects and can be overridden to define custom comparison logic."

---

If you want, I can also provide:

* 🔥 **Tricky interview scenarios**
* 🧠 **Follow-up questions asked in Lead/Senior rounds**
* 📝 **Real-world use cases**

Just tell me 👍

---

# 2.Why is String immutable in Java?

---

This is a **very important Core Java + Lead-level interview question**. Let’s break it down clearly, with **real-world reasoning and interview-ready points**.

---

## Why is `String` Immutable in Java?

In Java, a `String` object **cannot be changed once it is created**. Any modification creates a **new String object** instead of changing the existing one.

---

## 1️⃣ Security (Most Important Reason)

Strings are heavily used in **security-sensitive areas**:

* Database connection URLs
* Usernames & passwords
* File paths
* Network connections
* Class loading

### Example

```java
String url = "jdbc:mysql://localhost:3306/appdb";
```

If `String` were mutable, a malicious reference could modify it at runtime:

```java
url = "jdbc:mysql://malicious-server";
```

✅ **Immutability prevents this risk**, making applications more secure.

---

## 2️⃣ String Pool & Memory Optimization

Java stores String literals in a **String Constant Pool (SCP)**.

```java
String s1 = "Java";
String s2 = "Java";
```

Both `s1` and `s2` refer to the **same object** in memory.

If Strings were mutable:

* Changing `s1` would affect `s2`
* Shared references would cause data corruption

✅ Immutability allows **safe sharing and memory efficiency**.

---

## 3️⃣ Thread Safety (Without Synchronization)

Since Strings cannot be modified:

* Multiple threads can safely share the same String
* No need for synchronization

```java
String name = "Aditya"; // safe in multi-threaded environment
```

✅ This improves performance in concurrent applications.

---

## 4️⃣ HashCode Caching (Performance Boost)

Strings are widely used as keys in:

* `HashMap`
* `HashSet`
* `Hashtable`

Because Strings are immutable:

* Their `hashCode` is computed **once and cached**
* Hash-based collections perform faster

```java
Map<String, Integer> map = new HashMap<>();
map.put("user", 1);
```

❌ If Strings were mutable, changing a key would break the map structure.

---

## 5️⃣ Predictable & Reliable Behavior

Immutability ensures:

* Consistent behavior across the application
* No accidental modification

```java
String s = "Java";
s.concat(" World");

System.out.println(s); // Java
```

✔ Developers must explicitly assign a new reference.

---

## 6️⃣ Class Loading & Reflection Safety

Class names are passed as Strings:

```java
Class.forName("com.app.MyClass");
```

If mutable:

* Class loading could be manipulated at runtime

✅ Immutability ensures safe class resolution.

---

## 7️⃣ Supports Functional Programming Style

Immutability aligns with:

* Functional programming
* Safer and cleaner code

---

## Interview Summary Table

| Reason           | Benefit                          |
| ---------------- | -------------------------------- |
| Security         | Prevents malicious modification  |
| String Pool      | Memory efficiency & safe sharing |
| Thread Safety    | No synchronization needed        |
| HashCode caching | Faster collections               |
| Predictability   | Stable behavior                  |
| Class loading    | Runtime safety                   |

---

## One-Line Lead Interview Answer ⭐

> **"String is immutable in Java to ensure security, thread safety, memory efficiency through the String pool, and reliable behavior when used in hash-based collections."**

---

## Follow-up Interview Question (Very Common)

### ❓ If Strings are immutable, how do we modify them?

👉 Using **`StringBuilder`** (non-thread-safe, fast) or **`StringBuffer`** (thread-safe, synchronized).

---

If you want, I can also provide:

* 🔥 **Tricky interview scenarios**
* 🧠 **Deep JVM internals explanation**
* 📝 **String vs StringBuilder vs StringBuffer comparison**

Just tell me 👍

---

# 3.What is the diﬀerence between HashMap and ConcurrentHashMap?

---

This is a **very common Senior / Lead-level Java interview question**, especially when multithreading and scalability are discussed. I’ll explain it **conceptually + practically + interview-ready**.

---

## Difference between `HashMap` and `ConcurrentHashMap`

Both store **key–value pairs**, but they behave **very differently in multithreaded environments**.

---

## 1️⃣ Thread Safety

### HashMap

* **NOT thread-safe**
* Multiple threads modifying it simultaneously can cause:

  * Data inconsistency
  * Infinite loops (during resize)
  * Lost updates

```java
Map<String, String> map = new HashMap<>();
```

❌ Unsafe in concurrent scenarios.

---

### ConcurrentHashMap

* **Thread-safe**
* Designed for **high concurrency**
* Allows multiple threads to read & write **simultaneously**

```java
Map<String, String> map = new ConcurrentHashMap<>();
```

✅ Safe for multithreaded applications.

---

## 2️⃣ Synchronization Mechanism

### HashMap

* No synchronization
* If needed, must be externally synchronized

```java
Map<String, String> map = Collections.synchronizedMap(new HashMap<>());
```

⚠ Still has **performance bottlenecks**.

---

### ConcurrentHashMap

* Uses **fine-grained locking**
* Java 8+:

  * Uses **CAS (Compare-And-Swap)**
  * Locks only **specific buckets/nodes**, not the whole map

✅ Much better scalability.

---

## 3️⃣ Performance

| Operation     | HashMap | ConcurrentHashMap  |
| ------------- | ------- | ------------------ |
| Single-thread | Faster  | Slight overhead    |
| Multi-thread  | Unsafe  | High performance   |
| Reads         | Fast    | Non-blocking       |
| Writes        | Fast    | Controlled locking |

---

## 4️⃣ Null Key & Null Values

### HashMap

* Allows **1 null key**
* Allows **multiple null values**

```java
map.put(null, "value");
map.put("key", null);
```

---

### ConcurrentHashMap

* ❌ **Does NOT allow null keys or null values**

```java
map.put(null, "value"); // NullPointerException
```

✔ Prevents ambiguity during concurrent operations.

---

## 5️⃣ Iteration Behavior

### HashMap

* Iterators are **fail-fast**
* Throws `ConcurrentModificationException` if modified during iteration

```java
for (String key : map.keySet()) {
    map.put("x", "y"); // Exception
}
```

---

### ConcurrentHashMap

* Iterators are **fail-safe**
* Reflects **weakly consistent** view
* No `ConcurrentModificationException`

```java
for (String key : map.keySet()) {
    map.put("x", "y"); // Works
}
```

---

## 6️⃣ Locking Scope

### HashMap

* Entire map must be locked (if synchronized)

### ConcurrentHashMap

* Locks **only affected segments/buckets**
* Multiple threads can update different keys at the same time

---

## 7️⃣ Use Case Comparison

| Scenario                    | Use               |
| --------------------------- | ----------------- |
| Single-threaded app         | HashMap           |
| Multi-threaded app          | ConcurrentHashMap |
| High read/write concurrency | ConcurrentHashMap |
| Need null keys              | HashMap           |
| Real-time systems           | ConcurrentHashMap |

---

## 8️⃣ Real-World Example (Interview Gold)

### HashMap issue

* Used in web apps with multiple users
* Leads to **data corruption**

### ConcurrentHashMap use

* Session storage
* Caches
* Rate limiting
* Token management
* Configuration maps

---

## One-Line Interview Answer ⭐

> **"HashMap is not thread-safe and allows nulls, whereas ConcurrentHashMap is thread-safe, does not allow nulls, uses fine-grained locking, and provides high performance in concurrent environments."**

---

## Common Follow-Up Questions (Lead Round)

1. Why doesn’t ConcurrentHashMap allow null?
2. How does ConcurrentHashMap work internally in Java 8?
3. Difference between `Collections.synchronizedMap()` and `ConcurrentHashMap`?
4. Is ConcurrentHashMap fully lock-free?
5. What happens during resizing?

If you want, I can cover **internal working with diagrams**, or provide **real interview scenarios** next.

---

# 4.Explain the concept of fail-fast vs fail-safe iterators.

---

This is a **very common Core Java + Senior/Lead interview question**, especially around **collections and concurrency**. I’ll explain it **clearly, with examples and interview-ready points**.

---

## Fail-Fast vs Fail-Safe Iterators in Java

Iterators in Java define **how collections behave when they are modified during iteration**.

---

## 1️⃣ Fail-Fast Iterators

### 🔹 Concept

* **Fail-fast iterators throw an exception immediately** if the collection is structurally modified while iterating.
* They detect **concurrent modification** and stop execution.

### 🔹 Exception Thrown

* `ConcurrentModificationException`

### 🔹 How it Works

* Collection maintains a **modCount**
* Iterator checks modCount during iteration
* If mismatch is detected → exception is thrown

### 🔹 Example

```java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);

Iterator<Integer> it = list.iterator();
while (it.hasNext()) {
    Integer val = it.next();
    if (val == 2) {
        list.remove(val); // ❌ Structural modification
    }
}
```

### Output

```text
ConcurrentModificationException
```

---

### 🔹 Collections Using Fail-Fast Iterators

* `ArrayList`
* `LinkedList`
* `HashMap`
* `HashSet`
* `Vector` (iterator is still fail-fast)

---

## 2️⃣ Fail-Safe Iterators

### 🔹 Concept

* **Fail-safe iterators do NOT throw exceptions**
* They iterate over a **snapshot or a copy** of the collection

### 🔹 Behavior

* Structural modification is allowed during iteration
* Iterator may **not reflect latest changes**

### 🔹 Example

```java
Map<Integer, String> map = new ConcurrentHashMap<>();
map.put(1, "A");
map.put(2, "B");

Iterator<Integer> it = map.keySet().iterator();
while (it.hasNext()) {
    Integer key = it.next();
    map.put(3, "C"); // ✅ Allowed
}
```

### ✔ No exception thrown

---

### 🔹 Collections Using Fail-Safe Iterators

* `ConcurrentHashMap`
* `CopyOnWriteArrayList`
* `CopyOnWriteArraySet`

---

## 3️⃣ Key Differences (Interview Table)

| Feature              | Fail-Fast                                | Fail-Safe                    |
| -------------------- | ---------------------------------------- | ---------------------------- |
| Exception            | Throws `ConcurrentModificationException` | No exception                 |
| Modification allowed | ❌ No                                     | ✅ Yes                        |
| Data view            | Real-time collection                     | Snapshot / weakly consistent |
| Memory overhead      | Low                                      | Higher (copy/snapshot)       |
| Thread safety        | ❌ No                                     | ✅ Yes                        |
| Used in              | Non-concurrent collections               | Concurrent collections       |

---

## 4️⃣ Important Interview Clarifications ⭐

### ❓ Is fail-fast guaranteed?

➡️ **No**. It is **best-effort**, not guaranteed in multi-threaded scenarios.

### ❓ Is fail-safe truly safe?

➡️ Safer, but **changes may not be visible** during iteration.

### ❓ Can we modify collection safely in fail-fast?

➡️ Yes, using:

```java
it.remove(); // Legal way
```

---

## 5️⃣ Real-World Analogy (Easy to Remember)

* **Fail-Fast**:
  🚨 "Stop everything! Something changed unexpectedly!"

* **Fail-Safe**:
  📸 "I’ll continue with the snapshot I already have."

---

## One-Line Interview Answer ⭐

> **"Fail-fast iterators immediately throw ConcurrentModificationException on structural modification, whereas fail-safe iterators work on a snapshot or weakly consistent view and allow concurrent modification without exceptions."**

---

## Common Follow-Up Questions (Lead Level)

1. Why is `Iterator.remove()` allowed in fail-fast?
2. Why are ConcurrentHashMap iterators weakly consistent?
3. Difference between `CopyOnWriteArrayList` and `Collections.synchronizedList`?
4. Is ConcurrentHashMap iterator fail-safe or weakly consistent?

If you want, I can explain **internal working with diagrams**, or provide **tricky interview scenarios** next 👍

---

# 5.What is the signiﬁcance of hashCode() and equals() method?

---

# 6.How does ArrayList work internally?

---

# 7.What is the diﬀerence between ArrayList and LinkedList?

---

# 8.How does Java handle memory management?

---

# 9.What is the role of the ﬁnal keyword?

---

# 10.How does Garbage Collection work in Java?

---

# 11.What is a WeakHashMap?

---

# 12.How is synchronization achieved in Java?

---

# 13.What are the diﬀerent thread states?

---

# 14.What is the diﬀerence between Runnable and Callable?

---

# 15.What is thread starvation?

---

# 16.What is the diﬀerence between wait(), sleep(), and yield()?

---

# 17.How does the volatile keyword work?

---

# 18.What is a race condition? How to prevent it?

---

# 19.Explain ReentrantLock vs synchronized block.

---

# 20.What is thread pooling and how is it implemented?

---

# 21.What is the Fork/Join framework?

---

# 22.Explain Stream API with examples.

---

# 23.Diﬀerence between map() and ﬂatMap() in Streams?

---

# 24.What are functional interfaces?

---

# 25.What is the diﬀerence between Optional.of() and Optional.ofNullable()?

---

# 26.What is method reference? Give examples.

---

# 27.How does Collectors.groupingBy() work?

---

# 28.What is the default method in interfaces?

---

# 29.What are sealed classes in Java?

---

# 30.What is a record class in Java?

---

# 31.Diﬀerence between checked and unchecked exceptions.

---

# 32.Custom exception handling in real-world applications.

---

# 33.What is the diamond problem in Java?

---

# 34.How does autoboxing/unboxing work?

---

# 35.Explain Enum in Java.

---

# 36.When to use TreeMap vs HashMap?

---

# 37.Why should hashCode() be consistent with equals()?

---

# 38.How to make an object immutable?

---

# 39.What is the use of transient keyword?

---

# 40.What is reﬂection in Java?

---

# 41.What is the diﬀerence between static and instance initialization block?

---

# 42.Diﬀerence between shallow copy and deep copy.

---

# 43.What is the use of System.identityHashCode()?

---

# 44.Explain CompletableFuture with example.

---

# 45.How do you implement a singleton pattern?

---

# 46.What are some ways to break a singleton?

---

# 47.What is double-checked locking?

---

# 48.What are phantom references?

---

# 49.Why is clone() considered bad practice?

---

# 50.How would you design your own custom collection?

---

# 51.Explain method overloading vs overriding

---

# 52.Explain covariant return types.

---

# 53.How does Java handle pass-by-value or reference?

---

# 54.Can we override private/static/ﬁnal methods?

---

# 55.When would you use an abstract class over interface?

---

# 56.What is java.lang.instrument used for?

---

# 57.What is Metaspace in Java?

---

# 58.How to detect memory leaks in Java?

---

# 59.What is ClassLoader? Types of class loaders?

---

# 60.What is JIT compiler?

---

# 61.How do annotations work internally?

---

# 62.How to create custom annotations?

---

# 63.What is annotation processing in Java?

---

# 64.What are lambdas and how do they work internally?

---

# 65.Explain Type Erasure in Generics.

---

# 66.How are Generics implemented internally?

---

# 67.Explain bounded vs unbounded wildcards.

---

# 68.What is raw type in Java?

---

# 69.How would you make a list thread-safe?

---

# 70.How to avoid deadlock in concurrent programming?

---

# 71.Diﬀerence between Spring and Spring Boot.

---

# 72.What is dependency injection and how is it implemented in Spring?

---

# 73.Diﬀerence between @Component, @Service, @Repository, and @Controller.

---

# 74.What is the role of @Autowired and how does it work?

---

# 75.How does Spring Boot auto-conﬁguration work?

---

# 76.What are the starter dependencies in Spring Boot?

---

# 77.What is @SpringBootApplication composed of?

---

# 78.How does component scanning work in Spring Boot?

---

# 79.How do proﬁles work in Spring Boot?

---

# 80.What are beans in Spring? Lifecycle?

---

# 81.Diﬀerence between ApplicationContext and BeanFactory.

---

# 82.How to deﬁne a custom scope?

---

# 83.What is AOP? Explain with use-case.

---

# 84.Diﬀerence between cross-cutting concern and business logic?

---

# 85.How to implement custom annotations with AOP?

---

# 86.What is the use of @Transactional?

---

# 87.What is the diﬀerence between programmatic and declarative transaction management?

---

# 88.Explain propagation types in transaction management.

---

# 89.How does Spring handle circular dependency?

---

# 90.What is the diﬀerence between @Value, @ConﬁgurationProperties, and Environment?

---

# 91.Explain RestTemplate vs WebClient.

---

# 92.What is reactive programming in Spring?

---

# 93.Diﬀerence between Mono and Flux?

---

# 94.What is Spring WebFlux?

---

# 95.How to secure a REST API using Spring Security?

---

# 96.Diﬀerence between permitAll() and authenticated()?

---

# 97.What is CSRF and how to handle it in Spring?

---

# 98.What is AuthenticationManager?

---

# 99.How to implement custom authentication in Spring Security?

---

# 100. What are ﬁlters and interceptors?

---

# 101. What is the diﬀerence between Filter and HandlerInterceptor?

---

# 102. How does Spring handle exceptions?

---

# 103. What is the diﬀerence between @ControllerAdvice and @ExceptionHandler?

---

# 104. How to return consistent error responses in Spring REST?

---

# 105. How to create custom validators in Spring Boot?

---

# 106. Diﬀerence between validation groups and constraints?

---

# 107. What is the use of @Valid and @Validated?

---

# 108. How to use Swagger/OpenAPI in Spring Boot?

---

# 109. Diﬀerence between @PathVariable and @RequestParam.

---

# 110. What is HATEOAS?

---

# 111. How does @Async work in Spring Boot?

---

# 112. What is Spring Scheduler? Cron jobs?

---

# 113. How to publish and listen to events in Spring?

---

# 114. Diﬀerence between synchronous and asynchronous event publishing.

---

# 115. How does caching work in Spring Boot?

---

# 116. How to use Redis for caching?

---

# 117. How to monitor Spring Boot applications?

---

# 118. What are Spring Boot Actuators?

---

# 119. How to expose custom metrics?

---

# 120. How to conﬁgure a datasource manually?

---

# 121. What is Spring Data JPA?

---

# 122. What are derived query methods?

---

# 123. Diﬀerence between CrudRepository, JpaRepository, PagingAndSortingRepository.

---

# 124. How to handle pagination in Spring Data?

---

# 125. What is query-by-example (QBE)?

---

# 126. How to write native queries in JPA?

---

# 127. Diﬀerence between EntityManager and JdbcTemplate.

---

# 128. What is @EntityGraph?

---

# 129. What is lazy vs eager loading?

---

# 130. How does dirty checking work in JPA?

---

# 131. What is the N+1 select problem? Solution?

---

# 132. Diﬀerence between optimistic and pessimistic locking.

---

# 133. What is @DynamicUpdate in Hibernate?

---

# 134. How does @Inheritance work in JPA?

---

# 135. What is a DTO? Why is it used?

---

# 136. How to map DTO to Entity and vice versa?

---

# 137. What is ModelMapper?

---

# 138. What are common performance pitfalls in Spring Boot applications?

---

# 139. How to use Spring Boot with Docker?

---

# 140. How to externalize conﬁgurations in Spring Boot?

---

# 141. What is Spring Conﬁg Server?

---

# 142. Diﬀerence between Spring Cloud Conﬁg and application.yml?

---

# 143. How to use Spring Cloud with Eureka?

---

# 144. What is a circuit breaker in Spring Cloud?

---

# 145. What is Spring Cloud Gateway? Diﬀerence with Zuul?

---

# 146. How to write ﬁlters in Spring Gateway?

---

# 147. What is Resilience4j and how is it integrated?

---

# 148. What is Sleuth and Zipkin? How do they work?

---

# 149. What is Spring Retry?

---

# 150. What are distributed transactions and how to manage them in Spring?

---

# 151. What is Saga Pattern?

---

# 152. How to implement service discovery?

---

# 153. Diﬀerence between Ribbon and Spring Cloud LoadBalancer?

---

# 154. What is Hystrix? Why is it deprecated?

---

# 155. What is FeignClient and how does it work?

---

# 156. Diﬀerence between OpenFeign and RestTemplate?

---

# 157. How does OAuth2 work with Spring Security?

---

# 158. What is JWT? How is it integrated with Spring Boot?

---

# 159. How to secure microservices with API Gateway?

---

# 160. What is Spring Session?

---

# 161. How to implement rate limiting in Spring Boot?

---

# 162. What is service registry and how does it help?

---

# 163. How to trace a request across multiple services?

---

# 164. How to implement custom starter in Spring Boot?

---

# 165. How to test Spring Boot applications?

---

# 166. What is MockMvc and when to use it?

---

# 167. How to mock external services in integration tests?

---

# 168. What is @DataJpaTest?

---

# 169. What is TestContainers and how to use with Spring Boot?

---

# 170. What is the diﬀerence between Unit Test and Integration Test in Spring?

---

# 171. How is a microservice diﬀerent from a monolith?

---

# 172. What are the advantages and disadvantages of microservices?

---

# 173. How do microservices communicate?

---

# 174. What is service discovery?

---

# 175. What is Eureka and how does it work?

---

# 176. What is API Gateway in microservices?

---

# 177. How does Spring Cloud Gateway work?

---

# 178. What are edge services?

---

# 179. Explain the importance of bounded contexts in microservices.

---

# 180. What is domain-driven design (DDD)?

---

# 181. What is the diﬀerence between orchestration and choreography in microservices?

---

# 182. What is a distributed transaction?

---

# 183. How do you achieve eventual consistency?

---

# 184. Explain the Saga pattern with example.

---

# 185. How would you handle inter-service communication failures?

---

# 186. What is circuit breaker pattern?

---

# 187. How does Resilience4j work?

---

# 188. What is rate limiting? How do you implement it?

---

# 189. How to design idempotent APIs?

---

# 190. What is a fallback method in circuit breaker?

---

# 191. What is load balancing? Types?

---

# 192. Diﬀerence between client-side and server-side load balancing.

---

# 193. What is Ribbon? Is it still used?

---

# 194. What is Spring Cloud LoadBalancer?

---

# 195. What is API versioning and how to implement it?

---

# 196. How to secure microservices using OAuth2?

---

# 197. What is JWT? How to use it in microservices?

---

# 198. What is token propagation?

---

# 199. How do you handle secrets in microservices?

---

# 200. What is conﬁg server?

---

# 201. How to refresh conﬁg without restarting services?

---

# 202. What is bootstrap.yml vs application.yml?

---

# 203. What is centralized logging?

---

# 204. How does distributed tracing work?

---

# 205. What is Sleuth? What is Zipkin?

---

# 206. What are span and trace IDs?

---

# 207. What is an anti-corruption layer?

---

# 208. What is the database-per-service pattern?

---

# 209. What are shared-nothing architectures?

---

# 210. What is CQRS? When to use it?

---

# 211. What is Event Sourcing?

---

# 212. What is a sidecar pattern?

---

# 213. What is service mesh? What tools are used?

---

# 214. What is Istio and Linkerd?

---

# 215. How do you monitor microservices?

---

# 216. What is Prometheus and Grafana?

---

# 217. What are metrics and observability?

---

# 218. What is health check API?

---

# 219. How to perform health checks in Spring Boot?

---

# 220. How do you debug issues in a distributed environment?

---

# 221. What are dead-letter queues?

---

# 222. How do you manage service versioning?

---

# 223. How to maintain backward compatibility?

---

# 224. How do you deploy multiple microservices together?

---

# 225. What is blue-green deployment?

---

# 226. What is canary deployment?

---

# 227. How to rollback a faulty microservice?

---

# 228. What are the common microservices pitfalls?

---

# 229. How would you refactor a monolith into microservices?

---

# 230. What is a shared library in microservices?

---

# 231. What is API composition?

---

# 232. What is service granularity?

---

# 233. How do you manage dependencies between microservices?

---

# 234. How to test microservices independently?

---

# 235. What is consumer-driven contract testing?

---

# 236. What is Pact and how does it work?

---

# 237. How do you handle timeouts in microservices?

---

# 238. What is asynchronous communication?

---

# 239. When to use synchronous vs asynchronous communication?

---

# 240. What is eventual consistency vs strong consistency?

---

# 241. How to handle large payloads in microservices?

---

# 242. How to implement ﬁle upload in a microservice?

---

# 243. What is throttling?

---

# 244. How do you scale a microservice?

---

# 245. What is horizontal vs vertical scaling?

---

# 246. What is container orchestration?

---

# 247. How does Kubernetes support microservices?

---

# 248. What is the diﬀerence between microservices and SOA?

---

# 249. What is a backend-for-frontend (BFF) pattern?

---

# 250. What is the role of a message broker in microservices?

---

# 251. What are the best practices for microservice architecture?

---

# 252. What is a service mesh used for?

---

# 253. Explain the Ambassador pattern in microservices.

---

# 254. What are the 12 factors of microservices?

---

# 255. What is polyglot persistence?

---

# 256. What is observability and why is it critical?

---

# 257. How do you ensure microservices are resilient?

---

# 258. What’s the diﬀerence between telemetry, tracing, and logging?

---

# 259. What is shadow traﬃc?

---

# 260. How do you handle API deprecation in microservices?

---

# 261. How do you build a microservice SDK?

---

# 262. What is the diﬀerence between REST and gRPC?

---

# 263. How do you integrate GraphQL in microservices?

---

# 264. What is a lightweight vs heavyweight service?

---

# 265. What is head-of-line blocking?

---

# 266. What is a correlation ID and how is it useful?

---

# 267. How to design authentication in a microservice ecosystem?

---

# 268. What is the strangler pattern in microservices migration?

---

# 269. Explain real-world microservice monitoring setup using Spring Boot + Sleuth + Zipkin + Prometheus + Grafana.

---

# 270. What is the diﬀerence between WHERE and HAVING?

---

# 271. What is indexing? How does it improve performance?

---

# 272. What is a composite index?

---

# 273. What are clustered and non-clustered indexes?

---

# 274. What is normalization? Types?

---

# 275. What is denormalization?

---

# 276. What is ACID property?

---

# 277. What is the diﬀerence between TRUNCATE, DELETE and DROP?

---

# 278. What are window functions? Examples?

---

# 279. What is CTE?

---

# 280. How does GROUP BY work internally?

---

# 281. What is query optimization?

---

# 282. How to analyze slow queries?

---

# 283. What is a transaction isolation level?

---

# 284. Explain deadlocks in SQL and how to resolve.

---

# 285. What are stored procedures? Pros/Cons?

---

# 286. How do you handle migrations in production DB?

---

# 287. How do ORMs like Hibernate work?

---

# 288. What is Hibernate’s ﬁrst-level cache?

---

# 289. What is the diﬀerence between save(), persist(), merge() and update()?

---

# 290. What is the diﬀerence between get() and load()?

---

# 291. What is lazy initialization exception?

---

# 292. What is the purpose of @JoinColumn and @OneToMany?

---

# 293. How to handle orphan removal?

---

# 294. How does Hibernate manage object states?

---

# 295. What are common Hibernate performance issues?

---

# 296. How does the second-level cache work in Hibernate?

---

# 297. Diﬀerence between Criteria API and JPQL?

---

# 298. What is ﬂush() and clear()?

---

# 299. What is a natively generated ID vs sequence?

---

# 300. What is optimistic locking in JPA?

---

# 301. How to implement soft delete in Hibernate?

---

# 302. How does MongoDB store data?

---

# 303. Diﬀerence between MongoDB and MySQL?

---

# 304. What are documents and collections?

---

# 305. How to model one-to-many relationship in MongoDB?

---

# 306. What is aggregation framework in MongoDB?

---

# 307. What is sharding?

---

# 308. What are indexes in MongoDB?

---

# 309. How does Redis work?

---

# 310. What is TTL in Redis?

---

# 311. Diﬀerence between Redis and Memcached?

---

# 312. What are common use cases of Redis?

---

# 313. How to store sessions in Redis?

---

# 314. What is persistence in Redis?

---

# 315. How does Redis pub/sub work?

---

# 316. What are Redis data types?

---

# 317. How to avoid cache stampede?

---

# 318. How does cache eviction work in Redis?

---

# 319. What is write-through vs write-behind cache?

---

# 320. When would you use NoSQL over SQL?

---

# 353. What is CI/CD? Explain the ﬂow.

---

# 354. What tools are used in CI/CD?

---

# 355. Diﬀerence between Jenkins, GitHub Actions, and GitLab CI?

---

# 356. How to automate Spring Boot builds with Maven and Jenkins?

---

# 357. What is a Jenkins pipeline?

---

# 358. What is the diﬀerence between scripted and declarative pipeline?

---

# 359. How do you trigger builds automatically on git push?

---

# 360. What is the use of .gitlab-ci.yml or .github/workﬂows?

---

# 361. What is artifact management? Use of Nexus/Artifactory?

---

# 362. How do you perform zero-downtime deployments?

---

# 363. What is a rollback deployment strategy?

---

# 364. How do you manage secrets in CI/CD?

---

# 365. How do you deploy a Spring Boot app using Jenkins?

---

# 366. What is blue-green deployment? How to implement it?

---

# 367. What are stages in a pipeline?

---

# 368. How to run integration tests during a pipeline?

---

# 369. How to deploy microservices to Kubernetes using CI/CD?

---

# 370. What is infrastructure as code?

---

# 371. How do you use Terraform in CI/CD?

---

# 372. What is Ansible and how does it compare with Chef/Puppet?

---

# 373. What is Helm and how is it used?

---

# 374. What is GitOps?

---

# 375. How do you manage environment-speciﬁc conﬁguration in CI/CD?

---

# 376. What is a canary release?

---

# 377. What are Docker images and how are they pushed in CI/CD?

---

# 378. How do you tag Docker images automatically?

---

# 379. What is build caching?

---

# 380. What is a webhook?

---

# 381. How do you monitor CI/CD pipelines?

---

# 382. What is the use of a staging environment?

---

# 383. How to use SonarQube in your CI pipeline?

---

# 384. How to ensure code quality and security before deployment?

---

# 385. What are test, build, deploy, and post-deploy hooks?

---

# 386. What is Docker? Why is it used?

---

# 387. What is the diﬀerence between a container and an image?

---

# 388. What is a Dockerﬁle? Common instructions?

---

# 389. How to build and run a Docker image?

---

# 390. How to connect containers using Docker network?

---

# 391. What is a Docker volume?

---

# 392. How do you pass environment variables to a container?

---

# 393. What is Docker Compose?

---

# 394. How do you containerize a Spring Boot application?

---

# 395. How to optimize Docker image size?

---

# 396. What is the diﬀerence between ENTRYPOINT and CMD?

---

# 397. What is a multi-stage build in Docker?

---

# 398. How to persist logs in a Docker container?

---

# 399. What are Docker health checks?

---

# 400. What is the role of .dockerignore?

---

# 401. What is Apache Kafka?

---

# 402. How does Kafka work internally?

---

# 403. What is a Kafka topic and partition?

---

# 404. Diﬀerence between Kafka consumer groups and individual consumers?

---

# 405. How do you ensure message ordering in Kafka?

---

# 406. What is the role of Kafka brokers and zookeepers?

---

# 407. How to consume messages from Kafka using Spring Boot?

---

# 408. What is Kafka oﬀset? How is it managed?

---

# 409. What is the diﬀerence between at-most-once, at-least-once, and exactly-once delivery?

---

# 410. How do you handle backpressure in Kafka consumers?

---

# 411. Design an Aadhaar Registration System (like UIDAI).

---

# 412. Design a UPI transaction system.

---

# 413. Design a URL shortener like Bitly.

---

# 414. Design a rate limiter service.

---

# 415. Design an email notiﬁcation system.

---

# 416. Design a payment gateway like Razorpay.

---

# 417. Design an order management system.

---

# 418. Design a social media platform like Twitter.

---

# 419. Design a ride-sharing app backend like Uber.

---

# 420. Design a cab allocation algorithm.

---

# 421. Design a stock trading system.

---

# 422. Design a distributed caching system.

---

# 423. Design a scalable ﬁle storage service like Dropbox.

---

# 424. Design a newsfeed algorithm like Facebook.

---

# 425. Design a job scheduler system.

---

# 426. Design an e-commerce checkout system.

---

# 427. Design a multi-tenant SaaS app.

---

# 428. Design a chat messaging system.

---

# 429. Design a calendar booking system.

---

# 430. Design a scalable search engine.

---

# 431. Design a log aggregation system.

---

# 432. Design a fraud detection system for bank transactions.

---

# 433. Design a real-time bidding system.

---

# 434. Design a student registration portal for an academy.

---

# 435. Design a document approval workﬂow.

---

# 436. Design a notiﬁcation aggregator.

---

# 437. Design an online exam portal.

---

# 438. Design a microservice for user identity management.

---

# 439. Design a task scheduling system.

---

# 440. Design a content moderation system.

---

# 441. Design an IoT telemetry processing service.

---

# 442. Design a language translation service.

---

# 443. Design a product catalog service.

---

# 444. Design a document versioning service.

---

# 445. Design a survey application.

---

# 446. Design a hotel booking system.

---

# 447. Design a cloud storage system.

---

# 448. Design a recommendation engine.

---

# 449. Design an OTP veriﬁcation system.

---

# 450. Design a distributed rate limiter using Redis.

---

# 451. What is scalability? Vertical vs Horizontal?

---

# 452. What is latency vs throughput?

---

# 453. What is availability? What is reliability?

---

# 454. What is eventual consistency?

---

# 455. What is a CAP theorem?

---

# 456. What is partition tolerance?

---

# 457. What is sharding?

---

# 458. What is replication? Master-slave vs multi-master?

---

# 459. What is quorum in distributed systems?

---

# 460. What is a leader election?

---

# 461. What are consistent hashing and its use?

---

# 462. What is cache invalidation?

---

# 463. How to handle cache synchronization across nodes?

---

# 464. What is a load balancer? How does it work?

---

# 465. What is sticky session?

---

# 466. What is a CDN? How does it improve performance?

---

# 467. What are API rate limits and why needed?

---

# 468. What is message deduplication?

---

# 469. What is idempotency?

---

# 470. What is a distributed lock?

---

# 471. What is a bloom ﬁlter?

---

# 472. What is a write-ahead log (WAL)?

---

# 473. What are eventual vs strong consistency tradeoﬀs?

---

# 474. What is data partitioning?

---

# 475. What is circuit breaker pattern in system design?

---

# 476. What is the backpressure mechanism?

---

# 477. What is dead letter queue (DLQ)?

---

# 478. What is rolling update vs blue-green deployment?

---

# 479. What is a health check and readiness probe?

---

# 480. What is service mesh and when to use it?

---

# 481. What is gRPC and when is it better than REST?

---

# 482. What is API Gateway and what are its roles?

---

# 483. How do you ensure observability in distributed systems?

---

# 484. What are retries and exponential backoﬀ?

---

# 485. How to achieve fault tolerance in microservices?

---

# 486. How to horizontally scale a database?

---

# 487. What is an outbox pattern?

---

# 488. What is eventual consistency using Kafka?

---

# 489. How to maintain ACID in distributed systems?

---

# 490. What is data deduplication?

---

# 491. What are shadow writes and reads?

---

# 492. What is a quorum write/read?

---

# 493. What are the tradeoﬀs of NoSQL vs SQL?

---

# 494. How do you scale a notiﬁcation service?

---

# 495. What is system resiliency?

---

# 496. What are retries vs compensation?

---

# 497. What is a read replica? When to use it?

---

# 498. How do you implement distributed tracing?

---

# 499. What is service orchestration vs choreography?

---

# 500. How do you handle schema evolution in microservices?
