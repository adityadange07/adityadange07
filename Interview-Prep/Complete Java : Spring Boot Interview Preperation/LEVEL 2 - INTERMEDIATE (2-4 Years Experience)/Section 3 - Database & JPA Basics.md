# LEVEL 2: INTERMEDIATE (2-4 Years Experience)

# Database & JPA Bsics

## 127. What is ORM?

### **What is ORM (Object-Relational Mapping)?**

**ORM** stands for **Object-Relational Mapping**. It is a programming technique that **maps objects in an object-oriented language (like Java) to relational database tables**.

---

## **1. Purpose of ORM**

* Bridges the gap between **object-oriented programming (OOP)** and **relational databases** (RDBMS).
* Allows developers to **work with database records as Java objects** instead of writing raw SQL queries.

---

## **2. How ORM Works**

* **Class → Table**: Each Java class maps to a database table.
* **Object → Row**: Each object instance maps to a row in the table.
* **Field → Column**: Each class field maps to a table column.

**Example:**

```java
@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;

    @Column(name = "username")
    private String name;

    @Column(name = "email")
    private String email;

    // Getters and Setters
}
```

* Here, the `User` class maps to the `users` table.
* Each `User` object corresponds to a row in the table.

---

## **3. Advantages of ORM**

1. **Productivity:** Less boilerplate SQL code; developers can work with objects.
2. **Maintainability:** Changes in class structure can be automatically reflected in the database.
3. **Portability:** Database-agnostic; switching databases requires minimal changes.
4. **Caching & Lazy Loading:** Many ORM frameworks provide built-in caching and fetching strategies.

---

## **4. Popular Java ORM Frameworks**

* **Hibernate** – Most widely used ORM for Java.
* **JPA (Java Persistence API)** – Standard Java ORM specification.
* **Spring Data JPA** – Simplifies data access with JPA and repositories.

---

## **5. Example Workflow**

1. Define **entity classes** using `@Entity`.
2. Use **repository or session** to save, retrieve, update, or delete objects.
3. ORM framework **generates SQL queries automatically**.

```java
// Saving an object using JPA repository
User user = new User();
user.setName("Alice");
user.setEmail("alice@example.com");
userRepository.save(user); // No SQL needed
```

---

💡 **Interview Tip:**

> "ORM maps Java objects to database tables, allowing developers to perform CRUD operations using objects instead of writing raw SQL, improving productivity and maintainability."

---

I can next explain **JPA vs Hibernate**, which is a common follow-up interview question after ORM.

Do you want me to cover that?

---

## 128. What is JPA? Difference between JPA and Hibernate?

### **What is JPA?**

**JPA (Java Persistence API)** is a **standard specification** in Java for **object-relational mapping (ORM)** and **data persistence**.
It defines a set of interfaces and annotations to **map Java objects to database tables** and perform **CRUD operations** without writing SQL manually.

* **Key Annotations in JPA:**

  * `@Entity` → Marks a class as a database entity.
  * `@Table` → Maps entity to a specific table.
  * `@Id` → Marks the primary key.
  * `@GeneratedValue` → Auto-generates primary key values.
  * `@Column` → Maps field to table column.
  * `@OneToMany`, `@ManyToOne`, etc. → Defines relationships.

**Example:**

```java
@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;

    @Column(name = "username")
    private String name;

    @Column(name = "email")
    private String email;

    // getters and setters
}
```

---

### **Difference Between JPA and Hibernate**

| Feature                  | JPA                                                       | Hibernate                                                                     |
| ------------------------ | --------------------------------------------------------- | ----------------------------------------------------------------------------- |
| **Definition**           | Specification / API for ORM in Java                       | Implementation of JPA; ORM framework                                          |
| **Standard vs Vendor**   | Standard interface defined by Java                        | Actual framework providing ORM features                                       |
| **SQL Generation**       | Defined by specification, implemented by provider         | Generates SQL automatically                                                   |
| **Provider**             | Needs an implementation (Hibernate, EclipseLink, OpenJPA) | Implements JPA and adds additional features                                   |
| **Caching**              | Basic support via specification                           | Advanced caching (first-level, second-level, query cache)                     |
| **Query Language**       | JPQL (Java Persistence Query Language)                    | Supports HQL (Hibernate Query Language) and JPQL                              |
| **Database Independent** | Yes, via specification                                    | Yes, Hibernate supports many DBs but has vendor-specific optimizations        |
| **Extra Features**       | Only what specification allows                            | Advanced features like lazy loading, batch fetching, native queries, auditing |

---

### **Key Points**

1. **JPA = Specification** → You define entities and repositories using JPA interfaces.
2. **Hibernate = Implementation** → Implements JPA interfaces and provides extra ORM features.
3. You **can use JPA with Hibernate** as the provider:

```properties
spring.jpa.hibernate.ddl-auto=update
spring.datasource.url=jdbc:mysql://localhost:3306/mydb
spring.datasource.username=root
spring.datasource.password=pass
```

* JPA handles abstraction, Hibernate does the actual work.

---

💡 **Interview Tip:**

> "JPA is a standard ORM specification in Java, while Hibernate is a popular ORM framework that implements JPA and provides additional advanced features like caching, HQL, and better performance optimization."

---

I can next explain **JPA Entity Lifecycle with examples**, which is a very common interview question.

Do you want me to cover that?

---

## 129. What is an Entity in JPA?

### **What is an Entity in JPA?**

In **JPA (Java Persistence API)**, an **Entity** is a **plain Java class (POJO) that is mapped to a database table**. Each **instance of the entity class represents a row in the table**.

Entities are the **core concept in JPA** and are used to **persist data to the database**.

---

## **1. Key Points About Entities**

* Annotated with `@Entity`.
* Must have a **primary key** annotated with `@Id`.
* Can optionally use `@Table` to specify the table name (default: class name).
* Fields map to **columns** (default: field name).
* Can define **relationships** with other entities using `@OneToOne`, `@OneToMany`, `@ManyToOne`, `@ManyToMany`.

---

## **2. Example of a JPA Entity**

```java
import jakarta.persistence.*;

@Entity
@Table(name = "users") // optional, defaults to class name
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id; // primary key

    @Column(name = "username")
    private String name;

    @Column(name = "email")
    private String email;

    // Constructors, getters, setters
    public User() { }
    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }

    // getters and setters
}
```

* `User` class → mapped to `users` table.
* Each `User` object → represents a **row** in the `users` table.
* `id` → primary key.

---

## **3. Rules for JPA Entities**

1. Must be annotated with `@Entity`.
2. Must have a **no-argument constructor** (can be `protected`).
3. Must have a **primary key** annotated with `@Id`.
4. Cannot be a **final class**, and fields should not be `final` if you want them persisted.
5. Should follow **JavaBean conventions** (getter/setter methods).

---

## **4. Summary**

* **Entity = Table representation in Java**.
* **POJO + `@Entity` + `@Id`** → JPA can persist, update, delete, and query it automatically.
* Essential for **object-relational mapping**.

---

💡 **Interview Tip:**

> "An Entity in JPA is a Java class mapped to a database table, where each instance represents a row. It must have `@Entity` and a primary key `@Id`. Entities allow CRUD operations without writing SQL manually."

---

I can next explain **JPA Entity Lifecycle (Transient, Persistent, Detached, Removed)** with examples, which is a very commonly asked interview question.

Do you want me to cover that?

---

## 130. What are JPA annotations (@Entity,@Id,@GeneratedValue)?

### **Common JPA Annotations**

In **JPA (Java Persistence API)**, annotations are used to **map Java classes and fields to database tables and columns**. Here are the most commonly used ones:

---

## **1. `@Entity`**

* **Purpose:** Marks a Java class as a **JPA entity** (a table in the database).
* **Requirements:**

  * Must have a **primary key** (`@Id`).
  * Must have a **no-argument constructor**.

**Example:**

```java
import jakarta.persistence.Entity;

@Entity
public class User {
    @Id
    private int id;
    private String name;
}
```

* **Effect:** Tells JPA/Hibernate to **persist this class to the database**.

---

## **2. `@Id`**

* **Purpose:** Marks a field as the **primary key** of the entity.
* **Requirements:**

  * Every entity must have **exactly one `@Id` field**.
* **Example:**

```java
@Entity
public class User {
    @Id
    private int id; // primary key
    private String name;
}
```

---

## **3. `@GeneratedValue`**

* **Purpose:** Specifies how the **primary key is generated** automatically.
* **Common strategies:**

  | Strategy                  | Description                                                  |
  | ------------------------- | ------------------------------------------------------------ |
  | `GenerationType.AUTO`     | Default; lets the persistence provider choose the strategy.  |
  | `GenerationType.IDENTITY` | Auto-increment column in the database.                       |
  | `GenerationType.SEQUENCE` | Uses a database sequence object (common in Oracle/Postgres). |
  | `GenerationType.TABLE`    | Uses a separate table to generate unique IDs.                |

**Example:**

```java
@Entity
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id; // auto-generated

    private String name;
}
```

* **Effect:** When you save a new `User`, the ID is automatically generated by the database.

---

## **4. Optional: `@Table` and `@Column`**

* `@Table(name="table_name")` → Specify the table name (default: class name).
* `@Column(name="column_name")` → Specify column name, length, nullable, etc.

**Example:**

```java
@Entity
@Table(name = "users")
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int id;

    @Column(name = "username", nullable = false, length = 50)
    private String name;
}
```

---

## **Summary**

| Annotation        | Purpose                                                  |
| ----------------- | -------------------------------------------------------- |
| `@Entity`         | Marks a class as a JPA entity (mapped to a table)        |
| `@Id`             | Marks a field as the primary key                         |
| `@GeneratedValue` | Specifies how the primary key is automatically generated |
| `@Table`          | Specifies table name (optional)                          |
| `@Column`         | Specifies column details (optional)                      |

---

💡 **Interview Tip:**

> "`@Entity` maps a class to a table, `@Id` marks the primary key, and `@GeneratedValue` auto-generates the ID. `@Table` and `@Column` are optional for customizing table/column names."

---

I can next explain **JPA relationships annotations (`@OneToOne`, `@OneToMany`, `@ManyToOne`, `@ManyToMany`)** with examples, which is a very common interview topic.

Do you want me to cover that?

---

## 131. What is difference between persist() and merge()?

### **Difference Between `persist()` and `merge()` in JPA**

Both `persist()` and `merge()` are methods provided by the **`EntityManager`** in JPA to manage entity state, but they behave differently regarding **entity states** and **database operations**.

---

## **1. `persist()`**

* **Purpose:** Makes a **transient entity persistent** by **saving it to the database**.
* **Behavior:**

  * Changes the entity state from **transient → persistent**.
  * The **entity must not already exist in the database**.
  * **No return value**; operates on the original entity.
  * Throws `EntityExistsException` if the entity already exists.

**Example:**

```java
User user = new User();
user.setName("Alice");

entityManager.persist(user); // user is now persistent and will be inserted
```

* The **same `user` object** is managed by the persistence context.

---

## **2. `merge()`**

* **Purpose:** Updates an existing entity or saves a **detached entity** into the persistence context.
* **Behavior:**

  * Can be used for **both new and existing entities**.
  * Returns a **managed instance** of the entity.
  * Does **not change the state of the original entity**; the returned object is managed.
  * If the entity does not exist, it **inserts** it; if it exists, it **updates** it.

**Example:**

```java
User detachedUser = new User();
detachedUser.setId(1);
detachedUser.setName("Bob");

User managedUser = entityManager.merge(detachedUser);
// managedUser is now attached to persistence context
```

* `detachedUser` is **still detached**; `managedUser` is managed by JPA.

---

## **3. Key Differences**

| Feature                        | `persist()`                          | `merge()`                                                    |
| ------------------------------ | ------------------------------------ | ------------------------------------------------------------ |
| **State Transition**           | Transient → Persistent               | Detached → Persistent                                        |
| **Return Value**               | void                                 | Managed instance of entity                                   |
| **Use Case**                   | Insert new entity                    | Update existing entity or save detached entity               |
| **Entity Already Exists?**     | Throws exception                     | Updates existing entity                                      |
| **Changes to Original Object** | Original object becomes managed      | Original object remains detached; returned object is managed |
| **Lifecycle**                  | Works only on new/transient entities | Works on detached or new entities                            |

---

## **4. Example of Lifecycle States**

| Entity State   | `persist()`                | `merge()`                    |
| -------------- | -------------------------- | ---------------------------- |
| **Transient**  | Becomes persistent         | Returns a persistent copy    |
| **Persistent** | Already managed, no effect | Updates state in database    |
| **Detached**   | Throws exception           | Becomes persistent (managed) |
| **Removed**    | Throws exception           | Can reattach and update      |

---

💡 **Interview Tip:**

> "`persist()` is used to save a new entity and works on transient objects. `merge()` is used to reattach a detached entity or update an existing entity; it returns a managed instance."

---

I can next explain **`remove()` vs `delete()` in JPA/Hibernate**, which is a related topic often asked in interviews.

Do you want me to cover that?

---

## 132. What are JPA relationship (@OneToMany,@ManyToOne,etc.)?

### **JPA Relationships (`@OneToOne`, `@OneToMany`, `@ManyToOne`, `@ManyToMany`)**

In **JPA**, entities often have **relationships with other entities**, just like tables in a relational database. These are defined using **relationship annotations**.

---

## **1. `@OneToOne`**

* **Definition:** One entity is associated with **exactly one** instance of another entity.
* **Example:** A **User** has **one Profile**.

```java
@Entity
public class User {
    @Id
    private int id;
    private String name;

    @OneToOne(cascade = CascadeType.ALL)
    @JoinColumn(name = "profile_id")
    private Profile profile;
}
```

* **`@JoinColumn`** → specifies the foreign key column.
* `cascade = CascadeType.ALL` → automatically persists/updates related entity.

---

## **2. `@OneToMany`**

* **Definition:** One entity is associated with **multiple instances** of another entity.
* **Example:** A **Department** has **many Employees**.

```java
@Entity
public class Department {
    @Id
    private int id;
    private String name;

    @OneToMany(mappedBy = "department", cascade = CascadeType.ALL)
    private List<Employee> employees;
}
```

* `mappedBy` → indicates the field in the **child entity** that owns the relationship.

```java
@Entity
public class Employee {
    @Id
    private int id;
    private String name;

    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;
}
```

* **Owning side:** `Employee.department`
* **Inverse side:** `Department.employees`

---

## **3. `@ManyToOne`**

* **Definition:** Many instances of one entity relate to **one instance** of another entity.

* Essentially the **inverse of `@OneToMany`**.

* Already shown above in the Employee example.

---

## **4. `@ManyToMany`**

* **Definition:** Many instances of one entity relate to **many instances** of another entity.
* **Example:** A **Student** can enroll in **many Courses**, and a **Course** can have **many Students**.

```java
@Entity
public class Student {
    @Id
    private int id;
    private String name;

    @ManyToMany(cascade = CascadeType.ALL)
    @JoinTable(
        name = "student_course",
        joinColumns = @JoinColumn(name = "student_id"),
        inverseJoinColumns = @JoinColumn(name = "course_id")
    )
    private List<Course> courses;
}

@Entity
public class Course {
    @Id
    private int id;
    private String name;

    @ManyToMany(mappedBy = "courses")
    private List<Student> students;
}
```

* **`@JoinTable`** → defines the join table for the many-to-many relationship.

---

## **5. Summary Table of Relationships**

| Relationship | Direction   | Example                | Key Annotation               |
| ------------ | ----------- | ---------------------- | ---------------------------- |
| One-to-One   | 1 → 1       | User → Profile         | `@OneToOne`                  |
| One-to-Many  | 1 → Many    | Department → Employees | `@OneToMany` + `mappedBy`    |
| Many-to-One  | Many → 1    | Employee → Department  | `@ManyToOne`                 |
| Many-to-Many | Many ↔ Many | Student ↔ Course       | `@ManyToMany` + `@JoinTable` |

---

💡 **Interview Tip:**

> "JPA relationships map the associations between entities similar to foreign keys in DB. `@OneToOne`, `@OneToMany`, `@ManyToOne`, and `@ManyToMany` define cardinality. `mappedBy` is used on the inverse side, `@JoinColumn` or `@JoinTable` defines foreign keys or join tables."

---

I can next explain **lazy vs eager fetching (`FetchType.LAZY` vs `FetchType.EAGER`) in JPA relationships**, which is a common interview question.

Do you want me to cover that?

---

## 133. WHat is JPQL? 

### **What is JPQL (Java Persistence Query Language)?**

**JPQL** is a **query language defined by JPA** for querying **entities in the database**. It is **similar to SQL**, but instead of working with tables and columns, it works with **Java entity objects and their fields**.

---

## **1. Key Points About JPQL**

* **Object-Oriented Query Language:** Operates on **entities and their attributes**, not directly on database tables.
* **Database Independent:** Abstracts the underlying database, so queries work across different DBs.
* **Supports CRUD and Complex Queries:** Can retrieve, update, delete entities, and perform joins, aggregation, grouping, ordering, etc.

---

## **2. JPQL vs SQL**

| Feature                 | JPQL                                        | SQL                                      |
| ----------------------- | ------------------------------------------- | ---------------------------------------- |
| **Query Target**        | Entities (classes)                          | Tables (DB tables)                       |
| **Fields**              | Entity attributes                           | Columns                                  |
| **Join**                | Object relationships                        | Foreign key columns                      |
| **Database Dependency** | Database independent                        | Database specific                        |
| **Example**             | `SELECT u FROM User u WHERE u.name = :name` | `SELECT * FROM users WHERE username = ?` |

---

## **3. Basic JPQL Syntax**

```java
// JPQL query to get users by name
String jpql = "SELECT u FROM User u WHERE u.name = :name";
TypedQuery<User> query = entityManager.createQuery(jpql, User.class);
query.setParameter("name", "Alice");
List<User> users = query.getResultList();
```

* `User` → Entity class, not table.
* `u` → Alias for entity.
* `:name` → Named parameter.

---

## **4. Common JPQL Operations**

1. **Select All Entities**

```java
SELECT u FROM User u
```

2. **Where Clause**

```java
SELECT u FROM User u WHERE u.email LIKE '%@example.com'
```

3. **Join (Entity Relationships)**

```java
SELECT e FROM Employee e JOIN e.department d WHERE d.name = 'IT'
```

4. **Update/Delete**

```java
UPDATE User u SET u.name = 'Bob' WHERE u.id = 1
DELETE FROM User u WHERE u.id = 2
```

---

## **5. Advantages of JPQL**

* Database independent.
* Object-oriented; works with entities directly.
* Supports relationships (`@OneToMany`, `@ManyToOne`, etc.).
* Can be **typed queries** (`TypedQuery`) for compile-time safety.

---

💡 **Interview Tip:**

> "JPQL is an object-oriented query language for JPA entities. Unlike SQL, it queries entities and their attributes, not tables and columns, and works independently of the underlying database."

---

I can next explain **Named Queries vs Dynamic JPQL Queries** in JPA, which is a frequently asked topic in interviews.

Do you want me to cover that?

---

## 134. What is lazy loading vs eager loading?

### **Lazy Loading vs Eager Loading in JPA**

In JPA, **entity relationships** can be fetched from the database in **two main ways**: **lazily** or **eagerly**. This determines **when related data is loaded**.

---

## **1. Eager Loading (`FetchType.EAGER`)**

* **Definition:** Related entities are **fetched immediately** along with the parent entity.
* **Behavior:** When you load a parent entity, all associated entities marked as `EAGER` are loaded **at the same time** (join or separate query).
* **Use Case:** When you **always need the related entities**.

**Example:**

```java
@Entity
public class Department {

    @Id
    private int id;
    private String name;

    @OneToMany(mappedBy = "department", fetch = FetchType.EAGER)
    private List<Employee> employees;
}
```

* When a `Department` is retrieved, its `employees` list is **automatically loaded**.

**Pros:**

* Simple; no need to explicitly fetch related entities.
* Avoids `LazyInitializationException` outside transaction.

**Cons:**

* Can **impact performance** if there are many related entities.
* May fetch unnecessary data.

---

## **2. Lazy Loading (`FetchType.LAZY`)**

* **Definition:** Related entities are **fetched on demand**, i.e., **only when accessed**.
* **Behavior:** A proxy object is created. When you access the related collection/field, JPA executes a **separate query** to fetch data.
* **Use Case:** When you **don’t always need the related entities**.

**Example:**

```java
@Entity
public class Department {

    @Id
    private int id;
    private String name;

    @OneToMany(mappedBy = "department", fetch = FetchType.LAZY)
    private List<Employee> employees;
}
```

* When a `Department` is retrieved, `employees` are **not loaded immediately**.
* Accessing `department.getEmployees()` triggers a **database query**.

**Pros:**

* Better performance for large collections or optional relationships.
* Reduces unnecessary data retrieval.

**Cons:**

* Can cause `LazyInitializationException` if accessed **outside the transaction**.

---

## **3. Key Differences**

| Feature                  | Eager Loading                        | Lazy Loading                                                |
| ------------------------ | ------------------------------------ | ----------------------------------------------------------- |
| **When data is fetched** | Immediately with parent entity       | On demand when accessed                                     |
| **Performance**          | Can be heavy if collection is large  | More efficient if related data is not always needed         |
| **Default Fetch Type**   | `@OneToOne` and `@ManyToOne`         | `@OneToMany` and `@ManyToMany`                              |
| **Risk**                 | Fetches unnecessary data             | Can throw `LazyInitializationException` outside transaction |
| **Use Case**             | Small or always-needed relationships | Large or optional relationships                             |

---

## **4. Summary**

* **EAGER** → Fetch **all related entities immediately**.
* **LAZY** → Fetch **related entities only when needed**.
* **Best Practice:** Use **lazy loading by default** for collections and **eager only for essential relationships**.

---

💡 **Interview Tip:**

> "Lazy loading fetches related entities only when accessed, improving performance but requiring an active transaction. Eager loading fetches everything immediately, which may reduce performance but avoids lazy-loading issues."

---

I can next explain **`LazyInitializationException` and how to handle it**, which is a very common JPA interview topic.

Do you want me to cover that?

---

## 135. What is the difference between save() and saveAndFlush()?

### **Difference Between `save()` and `saveAndFlush()` in Spring Data JPA**

Both methods are part of **`JpaRepository`** and are used to **persist entities**, but they behave differently with respect to **transaction flushing and database synchronization**.

---

## **1. `save()`**

* **Purpose:** Saves or updates an entity but **does not immediately flush changes to the database**.
* **Behavior:**

  * Entity is saved to the **persistence context** (first-level cache).
  * Actual **SQL INSERT/UPDATE** happens **when the transaction is committed** or the persistence context is flushed.
* **Use Case:** Use when you want **batch saving or transactional operations** without immediate database write.

**Example:**

```java
User user = new User();
user.setName("Alice");
userRepository.save(user); // Not immediately written to DB
```

* The database will be updated **only when the transaction commits**.

---

## **2. `saveAndFlush()`**

* **Purpose:** Saves or updates an entity and **immediately flushes changes to the database**.
* **Behavior:**

  * Entity is saved to the persistence context.
  * **Flush is triggered immediately**, so SQL statements are executed in the database.
* **Use Case:** Use when you **need the entity persisted immediately**, e.g., to generate an ID or ensure DB consistency before next operation.

**Example:**

```java
User user = new User();
user.setName("Bob");
userRepository.saveAndFlush(user); // Immediately written to DB
```

---

## **3. Key Differences**

| Feature          | `save()`                                                | `saveAndFlush()`                                           |
| ---------------- | ------------------------------------------------------- | ---------------------------------------------------------- |
| **Flush to DB**  | No, flush happens at transaction commit                 | Yes, flush happens immediately                             |
| **Return Value** | Saved entity                                            | Saved entity                                               |
| **Use Case**     | Batch inserts/updates, within transactions              | Immediate persistence needed, e.g., for subsequent queries |
| **Performance**  | Slightly better for multiple operations (delayed flush) | Slightly slower due to immediate DB write                  |

---

## **4. Example Scenario**

```java
// Using save()
User user1 = new User();
user1.setName("Alice");
userRepository.save(user1);
// No SQL executed yet

// Using saveAndFlush()
User user2 = new User();
user2.setName("Bob");
userRepository.saveAndFlush(user2);
// SQL executed immediately, user2 inserted in DB
```

* `save()` is **lazy** within the transaction.
* `saveAndFlush()` is **eager**, ensuring DB synchronization.

---

💡 **Interview Tip:**

> "`save()` saves the entity in the persistence context and flushes at transaction commit. `saveAndFlush()` saves and immediately flushes to the database, useful when subsequent operations depend on the persisted data."

---

I can next explain **difference between `getOne()` (or `getReferenceById()`) vs `findById()` in Spring Data JPA**, which is a common follow-up question.

Do you want me to cover that?

---

## 136. In Hibernate, what is the difference between get() and load() methods?

### **Difference Between `get()` and `load()` in Hibernate**

Both `get()` and `load()` are methods of **`Session`** used to **retrieve entities by primary key**, but they behave differently regarding **fetching strategy, exceptions, and performance**.

---

## **1. `get()` Method**

* **Purpose:** Retrieves an entity **immediately from the database** (eager fetch).
* **Behavior:**

  * Returns the **actual entity object**.
  * Returns **`null`** if no entity is found.
  * **Queries the database immediately**.
  * Typically used when you **want to check if the entity exists**.

**Example:**

```java
User user = session.get(User.class, 1); // Immediately queries DB
if(user != null) {
    System.out.println(user.getName());
} else {
    System.out.println("User not found");
}
```

---

## **2. `load()` Method**

* **Purpose:** Returns a **proxy of the entity** and loads it **lazily** (on demand).
* **Behavior:**

  * Returns a **proxy object**, not the actual entity immediately.
  * Database is queried **only when a property is accessed**.
  * Throws **`ObjectNotFoundException`** if entity does not exist when accessed.
  * Can improve **performance** when you do not always need the entity data.

**Example:**

```java
User user = session.load(User.class, 1); // Returns proxy, no DB query yet
System.out.println(user.getName()); // DB query happens here
```

---

## **3. Key Differences**

| Feature           | `get()`                            | `load()`                                              |
| ----------------- | ---------------------------------- | ----------------------------------------------------- |
| **Return Type**   | Actual entity                      | Proxy object                                          |
| **Database Hit**  | Immediately queries DB             | Queries DB when property is accessed (lazy)           |
| **Null Handling** | Returns `null` if not found        | Throws `ObjectNotFoundException` if not found         |
| **Use Case**      | When you want to check existence   | When you are sure entity exists or want lazy loading  |
| **Performance**   | Slightly slower if entity not used | Faster for large entities if not accessed immediately |

---

## **4. Summary**

* **`get()`** → Eager fetch, safe, returns `null` if entity missing.
* **`load()`** → Lazy fetch, uses proxy, throws exception if entity missing.

---

💡 **Interview Tip:**

> "`get()` hits the database immediately and returns null if the entity doesn’t exist. `load()` returns a proxy and fetches the entity lazily, throwing an exception if it doesn’t exist when accessed."

---

I can next explain **difference between `save()`, `persist()`, and `saveOrUpdate()` in Hibernate**, which is commonly asked in interviews.

Do you want me to cover that?

---