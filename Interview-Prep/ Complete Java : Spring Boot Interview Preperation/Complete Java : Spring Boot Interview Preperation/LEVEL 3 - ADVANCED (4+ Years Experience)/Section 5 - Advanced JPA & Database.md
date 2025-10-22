# LEVEL 3: ADVANCED (4+ Years Experience)

# Advanced JPA & Databases

## 193. What is the N+1 select problem in JPA? How to fix it?

Absolutely, Aditya! The **N+1 select problem** is a common performance issue in JPA/Hibernate. Let’s go step by step.

---

## **1. What is the N+1 Select Problem?**

* Occurs when you **fetch a collection of entities**, and then for **each entity, a separate query is executed** to fetch related entities.
* This leads to **N+1 queries** instead of **just 1 optimized query**.

### **Example Scenario:**

Suppose you have two entities: `Department` and `Employee` (`OneToMany` relationship).

```java
@Entity
public class Department {
    @Id
    private Long id;
    
    private String name;

    @OneToMany(mappedBy = "department")
    private List<Employee> employees;
}

@Entity
public class Employee {
    @Id
    private Long id;
    private String name;

    @ManyToOne
    private Department department;
}
```

### **Problem Query:**

```java
List<Department> departments = entityManager.createQuery("SELECT d FROM Department d", Department.class)
                                            .getResultList();

for (Department d : departments) {
    System.out.println(d.getEmployees().size()); // triggers extra query per department
}
```

* **SQL Generated:**

  1. `SELECT * FROM Department` → 1 query
  2. For each department, `SELECT * FROM Employee WHERE department_id = ?` → N queries

* If **N = 100 departments**, we end up with **101 queries**, hence N+1.

---

## **2. Why is it a Problem?**

* Causes **huge performance degradation** for large datasets.
* High **database load** due to multiple queries.
* Slows down application significantly.

---

## **3. How to Fix It**

### **Option 1: Use `JOIN FETCH`**

```java
List<Department> departments = entityManager.createQuery(
    "SELECT d FROM Department d JOIN FETCH d.employees", Department.class)
    .getResultList();
```

* Fetches **departments and their employees in a single query**.
* Reduces **N+1 queries → 1 query**.

---

### **Option 2: Use `@EntityGraph`**

```java
@Entity
@NamedEntityGraph(name = "Department.employees", attributeNodes = @NamedAttributeNode("employees"))
public class Department { ... }

// Repository
List<Department> departments = departmentRepository.findAll(
    EntityGraph.EntityGraphType.FETCH, "Department.employees");
```

* Tells JPA to **fetch related collections eagerly** without writing JPQL joins.

---

### **Option 3: Use Batch Fetching (Hibernate Specific)**

```java
@OneToMany(mappedBy = "department")
@BatchSize(size = 10)
private List<Employee> employees;
```

* Hibernate will **load related entities in batches** instead of one by one.

---

### **Option 4: Avoid Lazy Loading in Loops**

* Lazy-loading inside loops is the **root cause** of N+1.
* Always **fetch related entities efficiently** upfront.

---

## **4. Summary Table**

| Approach                    | Pros                                            | Cons                                                       |
| --------------------------- | ----------------------------------------------- | ---------------------------------------------------------- |
| `JOIN FETCH`                | Simple, one query                               | Can return duplicate root entities if multiple collections |
| `@EntityGraph`              | Declarative, reusable                           | Requires defining graphs                                   |
| Batch Fetching              | Reduces number of queries, good for large lists | Requires Hibernate-specific config                         |
| Avoid Lazy Loading in loops | Simple rule to follow                           | Needs careful design                                       |

---

💡 **Interview Tip:**

* Be ready to **identify N+1 problems** in loops with lazy-loaded collections.
* Know **JOIN FETCH**, **EntityGraph**, and **Batch Fetching** as solutions.

---

If you want, I can make a **diagram showing N+1 select problem vs fixed JOIN FETCH approach**, which is **super useful for interviews and whiteboards**.

Do you want me to make that diagram?

---

## 194. What are entity graphs and how do they help?

Absolutely, Aditya! Let’s dive into **Entity Graphs in JPA** and how they help solve problems like the **N+1 select problem**.

---

## **1. What is an Entity Graph?**

* An **Entity Graph** is a **JPA feature** that defines a **template for fetching related entities**.
* It tells the **JPA provider which associations to fetch eagerly** in a query, overriding the default fetch type.
* Useful for **avoiding multiple queries (N+1 problem)** while still keeping associations lazy by default.

---

## **2. Types of Entity Graphs**

| Type                     | Description                                                                     |
| ------------------------ | ------------------------------------------------------------------------------- |
| **Named Entity Graph**   | Defined in the entity class using `@NamedEntityGraph`. Reusable across queries. |
| **Dynamic Entity Graph** | Created programmatically in code per query, flexible for runtime requirements.  |

---

## **3. Named Entity Graph Example**

### **Entities**

```java
@Entity
@NamedEntityGraph(
    name = "Department.employees",
    attributeNodes = @NamedAttributeNode("employees")
)
public class Department {
    @Id
    private Long id;
    private String name;

    @OneToMany(mappedBy = "department", fetch = FetchType.LAZY)
    private List<Employee> employees;
}

@Entity
public class Employee {
    @Id
    private Long id;
    private String name;

    @ManyToOne
    private Department department;
}
```

### **Repository Query Using Entity Graph**

```java
List<Department> departments = entityManager.createQuery("SELECT d FROM Department d", Department.class)
    .setHint("javax.persistence.fetchgraph", entityManager.getEntityGraph("Department.employees"))
    .getResultList();
```

* Fetches **departments and their employees in a single query**.
* Overrides **lazy loading** just for this query.

---

## **4. Dynamic Entity Graph Example**

```java
EntityGraph<Department> graph = entityManager.createEntityGraph(Department.class);
graph.addAttributeNodes("employees");

List<Department> departments = entityManager.createQuery("SELECT d FROM Department d", Department.class)
    .setHint("javax.persistence.fetchgraph", graph)
    .getResultList();
```

* Useful when you don’t want to define a named graph in the entity.

---

## **5. How Entity Graphs Help**

1. **Solve N+1 Select Problem**

   * By fetching associations **in one query instead of multiple queries**.

2. **Selective Eager Fetching**

   * Only fetch the associations you need for a particular use case.

3. **Better Performance & Flexibility**

   * Avoids unnecessary data fetches.
   * Works with **Spring Data JPA** using `@EntityGraph` on repository methods:

```java
@Repository
public interface DepartmentRepository extends JpaRepository<Department, Long> {

    @EntityGraph(attributePaths = {"employees"})
    List<Department> findAll();
}
```

---

## **6. Key Points / Interview Tips**

* Entity Graphs **do not change entity mappings** (still lazy/eager by default).
* Ideal for **read-heavy queries** with complex associations.
* Can be **named or dynamic**, reusable across multiple queries.
* Commonly used to **improve performance** in real-world applications.

---

💡 **Analogy:**

* Entities = rooms in a building
* Lazy associations = doors closed by default
* Entity Graph = **map telling JPA which doors to open** when fetching a room

---

If you want, I can make a **diagram showing how an Entity Graph fetches related entities in one query**, which is **excellent for explaining in interviews**.

Do you want me to make that diagram?

---

## 195. When would you use @Query vs derived queries vs Criteria API?

Absolutely, Aditya! Let’s carefully go through **when to use `@Query`, derived queries, and Criteria API in Spring Data JPA**. This is a common interview topic.

---

## **1. Derived Queries (Query Methods)**

### **Definition:**

* Spring Data JPA allows you to **define queries based on method names**.
* Example: `findByUsernameAndStatus(String username, String status)`

### **Example:**

```java
public interface UserRepository extends JpaRepository<User, Long> {
    List<User> findByStatus(String status);
    User findByUsernameAndStatus(String username, String status);
}
```

### **When to Use Derived Queries:**

1. Simple **CRUD queries**.
2. Query can be expressed easily in **method name**.
3. No need for complex joins, aggregations, or dynamic conditions.

**Pros:**

* Very **concise**
* No boilerplate SQL/JPQL

**Cons:**

* Method names can become **very long** for complex queries.
* Not suitable for **dynamic or highly customized queries**.

---

## **2. @Query Annotation**

### **Definition:**

* Allows you to write **custom JPQL or native SQL queries**.
* Useful for **complex queries** that cannot be expressed as method names.

### **Example:**

```java
public interface UserRepository extends JpaRepository<User, Long> {

    @Query("SELECT u FROM User u WHERE u.status = :status AND u.age > :age")
    List<User> findActiveUsersOlderThan(@Param("status") String status, @Param("age") int age);
    
    @Query(value = "SELECT * FROM users u WHERE u.status = ?1", nativeQuery = true)
    List<User> findUsersByStatusNative(String status);
}
```

### **When to Use @Query:**

1. Complex **JPQL queries** with joins, group by, aggregations.
2. Queries that **cannot be derived from method names**.
3. Native SQL is needed for **database-specific queries**.
4. **Parameterized queries** for dynamic values.

**Pros:**

* Full control over JPQL/SQL
* Can write **complex queries**

**Cons:**

* Harder to maintain for **very long queries**
* Native SQL may reduce **database portability**

---

## **3. Criteria API**

### **Definition:**

* A **type-safe, programmatic way** to build dynamic queries using Java objects.
* No strings; queries are **built using the JPA Metamodel**.

### **Example:**

```java
CriteriaBuilder cb = entityManager.getCriteriaBuilder();
CriteriaQuery<User> cq = cb.createQuery(User.class);
Root<User> user = cq.from(User.class);

Predicate statusPredicate = cb.equal(user.get("status"), "ACTIVE");
Predicate agePredicate = cb.gt(user.get("age"), 25);

cq.where(cb.and(statusPredicate, agePredicate));

List<User> users = entityManager.createQuery(cq).getResultList();
```

### **When to Use Criteria API:**

1. **Dynamic queries** where conditions change at runtime.
2. Complex **filtering or search screens** with optional parameters.
3. Type-safe queries (avoids string-based JPQL errors).

**Pros:**

* Type-safe, avoids JPQL syntax errors
* Dynamic query building

**Cons:**

* Verbose and harder to read than `@Query`
* More boilerplate code

---

## **4. Quick Comparison Table**

| Feature       | Best Use Case                       | Pros                     | Cons                                |
| ------------- | ----------------------------------- | ------------------------ | ----------------------------------- |
| Derived Query | Simple CRUD / static queries        | Concise, no boilerplate  | Complex queries → long method names |
| `@Query`      | Complex JPQL / SQL / joins          | Full control, flexible   | Harder to maintain, less dynamic    |
| Criteria API  | Dynamic queries, runtime conditions | Type-safe, fully dynamic | Verbose, boilerplate-heavy          |

---

### **5. Interview Tip**

* **Use derived queries** when query is simple.
* **Use @Query** when you need a specific query not easily expressed via method name.
* **Use Criteria API** when the query is **dynamic with optional parameters** or very complex.

---

💡 **Analogy:**

* Derived Query = “I know exactly what I want, so I ask directly.”
* `@Query` = “I have a complex request, let me write it myself.”
* Criteria API = “I need a flexible search form where users choose filters dynamically.”

---

If you want, I can make a **diagram showing Derived Query → @Query → Criteria API flow and use cases**, which is very helpful for **interviews**.

Do you want me to make that diagram?

---

## 196. How does optimistic locking work in JPA? @Version annotation?

Absolutely, Aditya! Let’s go step by step on **optimistic locking in JPA** and the `@Version` annotation. This is an important concept for **concurrent data access**.

---

## **1. What is Optimistic Locking?**

* **Optimistic Locking** assumes that **multiple transactions can frequently complete without interfering with each other**.

* Instead of locking the database row, JPA **checks for conflicts at the time of commit**.

* If a conflict occurs (someone else updated the same row), JPA throws an **`OptimisticLockException`**.

* Useful when **conflicts are rare**, e.g., web applications where multiple users rarely edit the same entity simultaneously.

---

## **2. How It Works**

1. **Add a version field** to your entity (e.g., integer or timestamp).
2. JPA automatically **increments the version** on each update.
3. When updating:

   * JPA checks that the version in the database matches the version in the entity.
   * If versions don’t match → **OptimisticLockException**.

---

## **3. Using `@Version` Annotation**

### **Entity Example:**

```java
import jakarta.persistence.*;

@Entity
public class Product {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;
    private double price;

    @Version
    private Integer version; // Optimistic locking field

    // getters and setters
}
```

### **How JPA Uses It:**

* Initial version: `1`
* Transaction A reads product with version `1`.
* Transaction B reads the same product (version `1`).
* Transaction A updates product → version becomes `2`.
* Transaction B tries to update → **OptimisticLockException** because version mismatch (`1 != 2`).

---

## **4. Example Repository Usage**

```java
@Transactional
public void updatePrice(Long productId, double newPrice) {
    Product product = productRepository.findById(productId).orElseThrow();
    product.setPrice(newPrice);
    productRepository.save(product); // version automatically checked and incremented
}
```

* If another transaction updated the same product, `save()` will throw **`OptimisticLockException`**.

---

## **5. Key Points**

1. `@Version` can be **Integer, Long, or Timestamp**.
2. **No database locks** are used, so it’s very efficient for read-heavy applications.
3. **Exceptions must be handled** – usually by retrying the operation.
4. Works well with **REST APIs**, **web apps**, and **high-concurrency scenarios**.

---

## **6. Optimistic vs Pessimistic Locking**

| Feature     | Optimistic Locking        | Pessimistic Locking                    |
| ----------- | ------------------------- | -------------------------------------- |
| Assumption  | Conflicts are rare        | Conflicts are frequent                 |
| Locking     | No DB lock                | Locks the row in DB                    |
| Performance | High (no lock overhead)   | Lower (locks block other transactions) |
| Exception   | `OptimisticLockException` | May wait or timeout                    |

---

💡 **Analogy:**

* Optimistic Locking = **“I hope no one else is changing it. If they are, I’ll handle it.”**
* Pessimistic Locking = **“I’ll lock it so no one else can touch it until I’m done.”**

---

If you want, I can make a **diagram showing two transactions updating the same entity with `@Version` and throwing OptimisticLockException**, which is **super useful for interviews**.

Do you want me to make that diagram?

---

## 197. What is pessimistic locking? When to use it?

Absolutely, Aditya! Let’s go through **pessimistic locking in JPA**, its working, and use cases.

---

## **1. What is Pessimistic Locking?**

* **Pessimistic Locking** assumes that **concurrent transactions are likely to conflict**, so it **locks the database row** immediately when a transaction reads it.
* Other transactions trying to access the same row **must wait** until the lock is released.
* Ensures **data consistency** at the cost of **potential performance bottlenecks**.

---

## **2. How It Works in JPA**

JPA provides **lock modes** for pessimistic locking:

| Lock Mode                     | Description                                                                                    |
| ----------------------------- | ---------------------------------------------------------------------------------------------- |
| `PESSIMISTIC_READ`            | Allows reading the row, but other transactions cannot update it.                               |
| `PESSIMISTIC_WRITE`           | Locks the row for writing. Other transactions cannot read or write until the lock is released. |
| `PESSIMISTIC_FORCE_INCREMENT` | Locks and also increments version (optimistic + pessimistic hybrid).                           |

---

### **Example**

```java
@Transactional
public void updateProductStock(Long productId, int quantity) {
    Product product = entityManager.find(
        Product.class, 
        productId, 
        LockModeType.PESSIMISTIC_WRITE
    );

    product.setStock(product.getStock() - quantity);
    entityManager.merge(product);
}
```

* **Row locked** until transaction commits.
* Prevents **other transactions from reading/writing** the same row simultaneously.

---

## **3. When to Use Pessimistic Locking**

1. **High contention scenarios** where multiple transactions frequently update the same entity.

   * Example: Banking transfers, inventory stock decrement.
2. **Critical data updates** where conflicts cannot be tolerated.
3. **Legacy systems** where optimistic locking may fail due to concurrent modifications.

---

## **4. Comparison: Optimistic vs Pessimistic Locking**

| Feature     | Optimistic Locking             | Pessimistic Locking                 |
| ----------- | ------------------------------ | ----------------------------------- |
| Assumption  | Conflicts are rare             | Conflicts are frequent              |
| Locking     | No DB locks, checked at commit | Locks row immediately in DB         |
| Performance | High (less blocking)           | Lower (blocks other transactions)   |
| Exceptions  | `OptimisticLockException`      | May wait or timeout                 |
| Use Case    | Web apps, low conflict         | Banking, inventory, high contention |

---

💡 **Analogy:**

* Optimistic Locking = **“I’ll go ahead and hope no one else edits it. If they do, I’ll retry.”**
* Pessimistic Locking = **“I’ll lock it now so no one else can touch it until I finish.”**

---

If you want, I can make a **diagram showing multiple transactions with pessimistic locks blocking each other**, which is **great for interviews**.

Do you want me to make that diagram?

---

## 198. How do you handle pagination and sorting in Spring Data JPA?

Absolutely, Aditya! Handling **pagination and sorting** is a very common task in Spring Data JPA and a frequent interview question. Let’s go step by step.

---

## **1. Using `Pageable` for Pagination**

Spring Data JPA provides the **`Pageable`** interface to fetch data **page by page**.

### **Example Repository**

```java
public interface EmployeeRepository extends JpaRepository<Employee, Long> {

    // Spring Data JPA automatically handles pagination
    Page<Employee> findByDepartment(String department, Pageable pageable);
}
```

---

### **2. Example Service/Controller Usage**

```java
// Pageable: pageNumber starts from 0
Pageable pageable = PageRequest.of(0, 10); // Page 0, 10 items per page
Page<Employee> page = employeeRepository.findByDepartment("HR", pageable);

List<Employee> employees = page.getContent(); // List of employees
int totalPages = page.getTotalPages();
long totalElements = page.getTotalElements();
```

* `Page<Employee>` provides:

  * `getContent()` → list of items in current page
  * `getTotalPages()` → total number of pages
  * `getTotalElements()` → total number of elements

---

## **3. Adding Sorting**

Spring Data JPA allows sorting using the **`Sort`** class or combining it with `Pageable`.

### **Sort Example:**

```java
List<Employee> employees = employeeRepository.findAll(
    Sort.by(Sort.Direction.ASC, "name")  // Sort by name ascending
);
```

### **Pagination + Sorting Example:**

```java
Pageable pageable = PageRequest.of(0, 10, Sort.by(Sort.Direction.DESC, "salary"));
Page<Employee> page = employeeRepository.findByDepartment("IT", pageable);
```

* Fetches **first page** (10 items) of IT employees, sorted by salary in descending order.

---

## **4. Dynamic Sorting Example**

```java
Sort sort = Sort.by(Sort.Order.asc("department"), Sort.Order.desc("salary"));
List<Employee> employees = employeeRepository.findAll(sort);
```

* Sorts first by department ascending, then salary descending.

---

## **5. Using Spring Data REST / Controller Example**

```java
@GetMapping("/employees")
public Page<Employee> getEmployees(
        @RequestParam int page,
        @RequestParam int size,
        @RequestParam String sortBy
) {
    Pageable pageable = PageRequest.of(page, size, Sort.by(sortBy).ascending());
    return employeeRepository.findAll(pageable);
}
```

* Client can request `/employees?page=0&size=10&sortBy=salary`

---

## **6. Key Notes**

1. **Page numbers start from 0**, not 1.
2. Use `Pageable` when dealing with **large datasets** to avoid fetching all rows.
3. `Page` vs `Slice`:

   * `Page` → total elements + total pages info
   * `Slice` → just the current slice, **lighter and faster** if total info not needed

---

## **7. Summary Table**

| Feature              | Class / Method                            | Notes                            |
| -------------------- | ----------------------------------------- | -------------------------------- |
| Pagination           | `Pageable` / `PageRequest.of(page, size)` | Fetch data page by page          |
| Sorting              | `Sort.by()`                               | Can sort ascending or descending |
| Pagination + Sorting | `PageRequest.of(page, size, Sort)`        | Combine pagination and sorting   |
| Return type          | `Page<T>` or `Slice<T>`                   | Contains content, metadata       |

---

💡 **Interview Tip:**

* Always mention `Page` vs `Slice` difference.
* Show ability to **combine filters, pagination, and sorting dynamically**.

---

If you want, I can make a **diagram showing Spring Data JPA pagination + sorting workflow** for interview whiteboards.

Do you want me to make that diagram?

---

## 199. What are databases transactions? ACID properties?

Absolutely, Aditya! Let’s break down **database transactions** and **ACID properties** in detail.

---

## **1. What is a Database Transaction?**

A **transaction** is a **sequence of one or more operations** performed as a single **logical unit of work** in a database.

* Either **all operations succeed** (commit)
* Or **all operations fail** (rollback)
* Ensures **data consistency and integrity**

### **Example: Banking Transfer**

Transferring $100 from Account A to Account B:

1. Subtract $100 from Account A
2. Add $100 to Account B

**Transaction ensures:**

* Both steps happen together (commit)
* If something fails (e.g., network, insufficient funds), **rollback** occurs

---

## **2. ACID Properties**

ACID ensures **reliable transactions** in databases.

| Property        | Description                                                    | Example                                                        |
| --------------- | -------------------------------------------------------------- | -------------------------------------------------------------- |
| **Atomicity**   | Transaction is **all or nothing**                              | If one step fails in money transfer, all changes are undone    |
| **Consistency** | Transaction moves database from **one valid state to another** | Account balances remain correct after transfer                 |
| **Isolation**   | Transactions **do not interfere** with each other              | Two transfers happening simultaneously do not corrupt balances |
| **Durability**  | Once committed, changes are **permanent**                      | Even if DB crashes, committed transfer persists                |

---

## **3. Transaction Lifecycle in DB**

1. **Begin Transaction** – Start a new transaction
2. **Execute Operations** – Insert/update/delete/select
3. **Commit** – Make all changes permanent
4. **Rollback** – Undo all changes if any step fails

---

## **4. Spring & JPA Transactions**

In **Spring Boot / JPA**, transactions are managed via `@Transactional`:

```java
@Service
public class AccountService {

    @Autowired
    private AccountRepository accountRepository;

    @Transactional
    public void transferMoney(Long fromId, Long toId, double amount) {
        Account from = accountRepository.findById(fromId).orElseThrow();
        Account to = accountRepository.findById(toId).orElseThrow();

        from.setBalance(from.getBalance() - amount);
        to.setBalance(to.getBalance() + amount);

        accountRepository.save(from);
        accountRepository.save(to);
    }
}
```

* **@Transactional** ensures **all operations succeed or fail together**
* Supports **rollback** in case of exceptions

---

## **5. Isolation Levels (Optional Advanced Note)**

* **READ_UNCOMMITTED** – Dirty reads allowed
* **READ_COMMITTED** – Only committed data visible
* **REPEATABLE_READ** – Prevents non-repeatable reads
* **SERIALIZABLE** – Full isolation, transactions executed one after another

---

💡 **Interview Tip:**

* Always explain **ACID properties with real-world examples**.
* Mention that Spring `@Transactional` handles **commit/rollback automatically**.

---

If you want, I can make a **diagram showing ACID properties and transaction flow in DB** which is **very helpful for interviews**.

Do you want me to make that diagram?

---

## 200. What is connection pooling? HikariCP configuration?

Absolutely, Aditya! Let’s go step by step on **connection pooling** and **HikariCP configuration** in Spring Boot.

---

## **1. What is Connection Pooling?**

* A **database connection** is **expensive to create** (handshake, authentication, network setup).
* **Connection pooling** maintains a **pool of reusable connections** instead of creating a new one every time.
* Benefits:

  1. **Faster database access**
  2. **Reduces overhead** of creating/closing connections
  3. **Manages maximum connections** efficiently

### **How It Works:**

1. Application requests a connection → pool provides an available connection.
2. Application uses connection → returns it to the pool instead of closing.
3. Pool manages idle, active, and max connections.

---

## **2. HikariCP (High-Performance JDBC Connection Pool)**

* **HikariCP** is the **default connection pool in Spring Boot 2+**.
* Lightweight, fast, low latency, widely used in production.

---

## **3. HikariCP Configuration in Spring Boot**

Spring Boot automatically configures HikariCP if it finds it on the classpath.
You can configure it via **`application.properties`** or **`application.yml`**.

### **Example: application.properties**

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=pass
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# HikariCP settings
spring.datasource.hikari.maximum-pool-size=10
spring.datasource.hikari.minimum-idle=5
spring.datasource.hikari.idle-timeout=30000
spring.datasource.hikari.connection-timeout=20000
spring.datasource.hikari.max-lifetime=1800000
spring.datasource.hikari.pool-name=MyHikariCP
```

### **Explanation of Key Properties:**

| Property             | Description                                        |
| -------------------- | -------------------------------------------------- |
| `maximum-pool-size`  | Max number of connections in the pool              |
| `minimum-idle`       | Minimum idle connections to maintain               |
| `idle-timeout`       | Max idle time before connection is removed         |
| `connection-timeout` | Max time to wait for a connection from the pool    |
| `max-lifetime`       | Max lifetime of a connection before it is recycled |
| `pool-name`          | Name of the pool (for logging/monitoring)          |

---

### **Optional: application.yml Example**

```yaml
spring:
  datasource:
    url: jdbc:mysql://localhost:3306/mydb
    username: root
    password: pass
    driver-class-name: com.mysql.cj.jdbc.Driver
    hikari:
      maximum-pool-size: 10
      minimum-idle: 5
      idle-timeout: 30000
      connection-timeout: 20000
      max-lifetime: 1800000
      pool-name: MyHikariCP
```

---

## **4. Advanced Notes / Interview Tips**

1. HikariCP **validates connections** automatically.
2. **Preferred over other pools** (Tomcat, DBCP) for **performance and reliability**.
3. Spring Boot + HikariCP automatically integrates with **Spring Data JPA / JDBC templates**.
4. Can monitor pool stats using **`HikariDataSource.getHikariPoolMXBean()`**.

---

💡 **Analogy:**

* Without pool: Every request → build new car → drive → destroy car
* With pool: Fleet of cars ready → just pick one → return it after use → reuse

---

If you want, I can make a **diagram showing HikariCP connection lifecycle and pool management**, which is **excellent for interview illustrations**.

Do you want me to make that diagram?

---

## 201. How do you implement database migrations with Flyway / Liquibase?

Absolutely, Aditya! Let’s go step by step on **database migrations** using **Flyway** and **Liquibase**, which are widely used in Spring Boot projects.

---

## **1. What is Database Migration?**

* **Database migration** means managing **schema changes** (tables, columns, constraints, indexes) in a **version-controlled and repeatable way**.
* Helps in:

  1. Keeping **development, testing, and production databases consistent**
  2. Automating schema changes during **CI/CD deployments**
  3. Tracking changes with **version history**

---

## **2. Flyway in Spring Boot**

### **How Flyway Works:**

1. Maintains a **version table** (`flyway_schema_history`) in the database.
2. Executes **versioned SQL scripts** in order (V1__, V2__, …).
3. Prevents re-running scripts already applied.

### **Step 1: Add Dependency**

```xml
<dependency>
    <groupId>org.flywaydb</groupId>
    <artifactId>flyway-core</artifactId>
</dependency>
```

### **Step 2: Create Migration Scripts**

* Place scripts under `src/main/resources/db/migration`
* Example:

**V1__create_employee_table.sql**

```sql
CREATE TABLE employee (
    id BIGINT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(100) NOT NULL,
    department VARCHAR(50),
    salary DOUBLE
);
```

**V2__add_email_column.sql**

```sql
ALTER TABLE employee ADD COLUMN email VARCHAR(100);
```

### **Step 3: Configure Flyway (optional)**

```properties
spring.flyway.enabled=true
spring.flyway.baseline-on-migrate=true
spring.flyway.locations=classpath:db/migration
```

* On application startup, Flyway automatically applies migrations.

---

## **3. Liquibase in Spring Boot**

### **How Liquibase Works:**

* Uses **changelogs** in **XML, YAML, JSON, or SQL** format.
* Tracks applied changes in **DATABASECHANGELOG** table.
* Supports **rollback**, making it safer for production.

### **Step 1: Add Dependency**

```xml
<dependency>
    <groupId>org.liquibase</groupId>
    <artifactId>liquibase-core</artifactId>
</dependency>
```

### **Step 2: Create Changelog File**

* `src/main/resources/db/changelog/db.changelog-master.yaml`

```yaml
databaseChangeLog:
  - changeSet:
      id: 1
      author: aditya
      changes:
        - createTable:
            tableName: employee
            columns:
              - column:
                  name: id
                  type: BIGINT
                  autoIncrement: true
                  constraints:
                    primaryKey: true
              - column:
                  name: name
                  type: VARCHAR(100)
                  constraints:
                    nullable: false
              - column:
                  name: department
                  type: VARCHAR(50)
```

### **Step 3: Configure Liquibase**

```properties
spring.liquibase.change-log=classpath:db/changelog/db.changelog-master.yaml
spring.liquibase.enabled=true
```

* On startup, Liquibase applies all **pending changesets**.
* Can **rollback** if necessary.

---

## **4. Flyway vs Liquibase**

| Feature          | Flyway                      | Liquibase                    |
| ---------------- | --------------------------- | ---------------------------- |
| Migration Type   | SQL scripts                 | XML/YAML/JSON/SQL changelogs |
| Rollback Support | Limited                     | Built-in rollback support    |
| Complexity       | Simple, lightweight         | Powerful, feature-rich       |
| Versioning       | Filename-based (V1__, V2__) | Changeset ID-based           |

---

## **5. Key Best Practices**

1. Keep migrations **version-controlled** along with code.
2. **Never edit applied migrations** in production.
3. Use **Flyway** for simple versioned SQL scripts.
4. Use **Liquibase** if you need **rollbacks, dynamic changes, or multi-database support**.

---

💡 **Analogy:**

* Flyway = **“follow a strict ordered list of scripts”**
* Liquibase = **“follow a recipe book with rollback instructions”**

---

If you want, I can make a **diagram showing Flyway vs Liquibase migration flow** which is **excellent for interviews and understanding CI/CD integration**.

Do you want me to make that diagram?

---

## 202. What is database indexing? Query optimization stategies?

Absolutely, Aditya! Let’s go step by step on **database indexing** and **query optimization strategies**, which are very common topics in interviews.

---

## **1. What is Database Indexing?**

* **Indexing** is a **data structure technique** to **quickly locate and access data** in a database table without scanning the entire table.
* Think of it as an **index in a book**: instead of reading every page, you can jump directly to the page you want.

### **How it Works:**

* Database maintains a separate **index structure** (often a **B-Tree** or **Hash**).
* When a query searches on an **indexed column**, the database uses the index to **quickly locate rows** instead of scanning all rows.

---

### **Example:**

```sql
CREATE INDEX idx_employee_name ON employee(name);
```

* Queries like below will **benefit from the index**:

```sql
SELECT * FROM employee WHERE name = 'Aditya';
```

---

## **2. Types of Indexes**

| Type                               | Description                          | Example Use Case               |
| ---------------------------------- | ------------------------------------ | ------------------------------ |
| **Single-column index**            | Index on one column                  | Search by employee name        |
| **Composite / Multi-column index** | Index on multiple columns            | Search by (department, salary) |
| **Unique index**                   | Enforces uniqueness + speeds queries | Email column in employee table |
| **Full-text index**                | Text search optimization             | Search in product descriptions |
| **Clustered index**                | Table rows stored in index order     | Primary key in MySQL InnoDB    |
| **Non-clustered index**            | Separate structure from table rows   | Secondary indexes              |

---

## **3. Query Optimization Strategies**

To make queries faster and reduce database load:

### **A. Proper Indexing**

* Index columns used in `WHERE`, `JOIN`, `ORDER BY`, `GROUP BY` clauses.
* Avoid excessive indexes – **they slow down writes**.

### **B. Use Efficient Queries**

* Prefer **SELECT only required columns** (`SELECT *` is costly).
* Avoid functions on indexed columns in WHERE clause (e.g., `WHERE YEAR(date) = 2025`) – may prevent index use.

### **C. Use Joins Smartly**

* Avoid unnecessary `JOIN`s.
* Use **inner join** if applicable; avoid `CROSS JOIN` unless needed.

### **D. Pagination**

* Use `LIMIT` and `OFFSET` to fetch small chunks instead of loading all rows.

```sql
SELECT * FROM employee ORDER BY salary DESC LIMIT 10 OFFSET 0;
```

### **E. Query Analysis**

* Use **EXPLAIN** to check execution plans:

```sql
EXPLAIN SELECT * FROM employee WHERE name = 'Aditya';
```

* Check whether indexes are being used.

### **F. Denormalization (if needed)**

* For read-heavy systems, sometimes duplicating data can **reduce JOINs**.

### **G. Caching**

* Cache frequently accessed data (Redis, in-memory cache) to reduce DB load.

---

## **4. Key Notes / Interview Tips**

1. Indexes **speed up reads** but **slow down writes** (INSERT, UPDATE, DELETE).
2. Composite indexes are **only used if query filters start with first indexed column**.
3. Always check **execution plans** for large queries.
4. Explain **trade-offs** when using indexing or denormalization.

---

💡 **Analogy:**

* Without index: **scan entire book page by page**
* With index: **look up topic in the index → go directly to the page**

---

If you want, I can make a **diagram showing table scan vs indexed query access + query optimization flow**, which is **super helpful for interviews**.

Do you want me to make that diagram?

---