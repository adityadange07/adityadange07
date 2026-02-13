## 251. What is ORM?

**Answer:**
**ORM (Object-Relational Mapping)** is a technique that lets you query and manipulate data from a database using an object-oriented paradigm.
*   **Concept:** Maps Java Objects (Entities) to Database Tables.
*   **Benefit:** Developers focus on Java logic instead of writing complex SQL queries.
*   **Tools:** Hibernate, EclipseLink, OpenJPA.

---

## 252. What is JPA?

**Answer:**
**JPA (Java Persistence API)** is a **Specification** (Interface) for accessing, persisting, and managing data between Java objects and a relational database.
*   **Nature:** It is just a set of rules and interfaces (`javax.persistence.*` or `jakarta.persistence.*`). It is **not** an implementation.
*   **Role:** Defines *how* ORM should work in Java.

---

## 253. What is Hibernate?

**Answer:**
**Hibernate** is an **Implementation** of the JPA specification.
*   **Role:** It is the actual framework that performs the mapping and generates SQL.
*   **Features:** It implements JPA but also offers proprietary features (Hibernate Query Language - HQL, Criteria API, Native SQL).

---

## 254. Difference between JPA and Hibernate?

**Answer:**

| Feature | JPA | Hibernate |
| :--- | :--- | :--- |
| **Type** | Specification (Interface). | Implementation (Provider). |
| **Usage** | Cannot be used alone. | Can be used alone or via JPA. |
| **Switching** | Code written against JPA interfaces can easily switch providers. | Code using Hibernate-specific features is locked to Hibernate. |
| **Analogy** | Like JDBC Interface. | Like Oracle JDBC Driver. |

---

## 255. What is Entity?

**Answer:**
An **Entity** is a lightweight, persistent domain object.
*   **Mapping:** It represents a table in a relational database.
*   **Instance:** Each instance of an entity corresponds to a row in that table.
*   **Annotation:** Marked with `@Entity`.
*   **Requirement:** Must have a no-arg constructor and a primary key (`@Id`).

---

## 256. What is @Id and @GeneratedValue?

**Answer:**
*   **@Id:** Specifies the primary key of an entity.
*   **@GeneratedValue:** Provides for the specification of generation strategies for the values of primary keys.
    *   Unlike manually checking max ID and incrementing, this delegates ID generation to the database or provider.

---

## 257. GenerationType strategies?

**Answer:**
1.  **AUTO (Default):** Persistence provider picks the best strategy based on the DB (often SEQUENCE or TABLE).
2.  **IDENTITY:** Relies on an auto-increment column in the DB (MySQL, SQL Server). ID is available only *after* insert.
3.  **SEQUENCE:** Uses a database sequence (Oracle, PostgreSQL). Efficient (can pre-fetch IDs).
4.  **TABLE:** Uses a separate table to keep the next ID. Slow (locking issues), generally avoided.

---

## 258. What is persistence context?

**Answer:**
The **Persistence Context** is a set of entity instances in which for every persistent identity directly referred to, there is a unique entity instance.
*   **Management:** It manages the lifecycle of entities (New, Manage, Detached, Removed).
*   **Scope:** Usually bound to a Transaction.
*   **Visual:** Think of it as the "First-Level Cache" where Hibernate stores objects it is currently tracking.

---

## 259. What is EntityManager?

**Answer:**
**EntityManager** is the primary JPA interface for interacting with the persistence context.
*   **Role:** Used to create, read, and remove operations for entities.
*   **Methods:** `persist()`, `merge()`, `remove()`, `find()`, `createQuery()`.
*   **Spring:** In Spring, you typically inject it via `@PersistenceContext`.

---

## 260. What is first-level cache?

**Answer:**
**First-Level Cache** is the session-level cache associated with the `EntityManager` (or Hibernate `Session`).
*   **Scope:** Transactional. Valid only while the EntityManager is open.
*   **Behavior:** If you request an entity with the same ID twice in the same transaction, Hibernate returns the object from cache (no second SQL query).
*   **Mandatory:** It is enabled by default and cannot be disabled.

---

## 261. Entity lifecycle states?

**Answer:**
JPA defines 4 states for an entity:
1.  **Transient (New):** Object created (`new User()`) but not associated with any EntityManager. No ID (mostly).
2.  **Managed (Persistent):** Associated with an EntityManager and has an ID. Changes are tracked and synced to DB.
3.  **Detached:** Previously managed, but the EntityManager is closed or `detach()` was called. Changes are **not** tracked.
4.  **Removed:** Scheduled for deletion from the DB.

---

## 262. What is detached entity?

**Answer:**
A **Detached Entity** is an object that has a database identity (ID) but is no longer connected to an active Persistence Context.
*   **Cause:** Transaction ended, Session closed, or explicit `em.detach(entity)`.
*   **Effect:** Modifying this object will **not** update the database unless it is re-attached (merged).

---

## 263. What is merge()?

**Answer:**
**merge()** is used to re-attach a detached entity to the persistence context.
*   **Behavior:**
    1.  It loads the entity with the same ID from the database (or cache).
    2.  It copies the fields from the detached object to the managed object.
    3.  It returns the **managed** instance.
*   **Note:** The original object passed to `merge()` remains detached.

---

## 264. What is persist()?

**Answer:**
**persist()** is used to make a transient instance **managed** and persistent.
*   **Effect:** It executes an `INSERT` statement (immediately or at flush time).
*   **Constraint:** If the entity already has an ID (generated strategy), calling `persist()` might throw an exception (depending on strategy).

---

## 265. What is remove()?

**Answer:**
**remove()** deletes the entity instance.
*   **State:** Transitions a managed entity to the **Removed** state.
*   **Effect:** It executes a `DELETE` statement at flush time.
*   **Constraint:** You can only remove **managed** entities. If you have a detached entity, you must `merge()` it first (or `getReference()`), then `remove()`.

---

## 266. What is flush()?

**Answer:**
**flush()** forces the EntityManager to synchronize the persistence context with the database.
*   **Action:** Executes pending SQL statements (INSERT, UPDATE, DELETE) immediately.
*   **Auto-flush:** Hibernate usually flushes automatically before a query execution (to ensure query sees latest data) and at transaction commit.

---

## 267. What is dirty checking?

**Answer:**
**Dirty Checking** is a feature where Hibernate automatically detects changes made to **managed** entities and updates the database.
*   **Mechanism:** When you load an entity, Hibernate keeps a snapshot. At flush time, it compares the current state with the snapshot. If different, it generates an `UPDATE` statement.
*   **Benefit:** You don't need to explicitly call `save()` or `update()` for managed objects.

---

## 268. What is cascading?

**Answer:**
**Cascading** allows operations performed on a parent entity to be automatically propagated to its child entities.
*   **Usage:** Configured via `cascade` attribute in relationships (`@OneToMany(cascade = CascadeType.ALL)`).
*   **Example:** if `User` has `List<Address>`, deleting `User` should delete all `Address` records.

---

## 269. Cascade types?

**Answer:**
Standard JPA Cascade Types:
1.  **PERSIST:** Propagates `persist()`.
2.  **MERGE:** Propagates `merge()`.
3.  **REMOVE:** Propagates `remove()`.
4.  **REFRESH:** Propagates `refresh()`.
5.  **DETACH:** Propagates `detach()`.
6.  **ALL:** All of the above.

---

## 270. What is orphanRemoval?

**Answer:**
**orphanRemoval** is a special feature (specific to `@OneToMany` and `@OneToOne`) that cleans up "orphaned" entities.
*   **Behavior:** If you remove a child entity from the collection of the parent, Hibernate automatically deletes that child from the database.
*   **Diff from Cascade.REMOVE:** `Cascade.REMOVE` only deletes children if the *Parent* is deleted. `orphanRemoval=true` deletes children if they are *disconnected* from the Parent.

---

## 271. @OneToOne vs @OneToMany?

**Answer:**
*   **@OneToOne:** Each row in Table A links to exactly one row in Table B.
    *   Example: `User` and `UserProfile`.
*   **@OneToMany:** Each row in Table A links to multiple rows in Table B.
    *   Example: `User` and `Orders`.
    *   Usually paired with `@ManyToOne` on the child side for bidirectional navigation.

---

## 272. Owning side vs inverse side?

**Answer:**
In a bidirectional relationship:
*   **Owning Side:** The side that **physically contains the foreign key** in the database.
    *   This side is responsible for updating the relationship in the DB.
*   **Inverse Side:** The other side, strictly for object navigation.
    *   Marked with `mappedBy`.
    *   Changes to the inverse side collection are **ignored** by Hibernate unless the owning side is also updated.

---

## 273. What is mappedBy?

**Answer:**
**mappedBy** is an attribute used on the **Inverse Side** of a relationship (usually `@OneToMany` or `@OneToOne`).
*   **Meaning:** "I am not responsible for this relationship. Look at the field named 'X' in the other class to find the configuration."
*   **Rule:** If you don't use `mappedBy` on a `@OneToMany`, Hibernate creates a separate Join Table by default instead of using a standard Foreign Key.

---

## 274. FetchType LAZY vs EAGER?

**Answer:**
*   **EAGER:** The related data is loaded **immediately** with the parent entity (often using a JOIN).
    *   Default for `@ManyToOne`, `@OneToOne`.
*   **LAZY:** The related data is loaded **on demand** (only when you call `getOrders()`).
    *   Default for `@OneToMany`, `@ManyToMany`.
    *   **Best Practice:** Prefer LAZY to avoid performance issues (loading too much data).

---

## 275. What is N+1 problem?

**Answer:**
The **N+1 Select Problem** occurs when you fetch a list of **N** parent entities, and then iterate over them to fetch a related child entity (Lazy Loaded).
*   **Query 1:** Fetch N Parents (`SELECT * FROM User`).
*   **Queries N:** Fetch Child for each Parent (`SELECT * FROM Address WHERE user_id = ?`).
*   **Total:** 1 + N queries. This kills performance for large details.

---

## 276. How to solve N+1?

**Answer:**
1.  **Join Fetch:** Use `JOIN FETCH` in JPQL/HQL.
    *   `SELECT u FROM User u JOIN FETCH u.addresses`.
    *   This forces a single SQL JOIN query.
2.  **EntityGraph:** Use `@EntityGraph` in JPA 2.1 to define fetch plans.
3.  **BatchFetching:** `@BatchSize(size = 10)` loads children in batches (IN clause) rather than one by one.

---

## 277. What is @JoinColumn?

**Answer:**
**@JoinColumn** specifies the Foreign Key column name in the database.
*   **Location:** Placed on the **Owning Side** of the relationship.
*   **Example:**
    ```java
    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;
    ```

---

## 278. What is @JoinTable?

**Answer:**
**@JoinTable** is used to map a relationship using a separate **Link Table** (Association Table).
*   **Default:** Default for `@ManyToMany`.
*   **Optional:** Can be used for `@OneToMany` if you don't want a foreign key in the child table (clean schema).
*   **Attributes:** `joinColumns` (FK to source), `inverseJoinColumns` (FK to target).

---

## 279. What is @Embeddable?

**Answer:**
**@Embeddable** marks a class whose instances are stored as an intrinsic part of an owning entity and share the identity of the entity.
*   **Usage:** Value Objects (e.g., `Address` with street, city, zip).
*   **@Embedded:** Used in the parent entity to include the embeddable.
*   **DB:** Fields define columns in the *same table* as the parent entity.

---

## 280. What is inheritance mapping strategies?

**Answer:**
JPA supports mapping inheritance hierarchies to DB tables:
1.  **SINGLE_TABLE (Default):** One table for the whole hierarchy. Uses a "Discriminator Column" (DTYPE). Fast, but nullable columns.
2.  **JOINED:** Base table + separate table for each subclass (with FK). Normalized, but slow (JOINs).
3.  **TABLE_PER_CLASS:** Separate table for each concrete class. No shared table. Unions are slow.

---

## 281. What is JPQL?

**Answer:**
**JPQL (Java Persistence Query Language)** is an object-oriented query language defined in the JPA specification.
*   **Target:** It queries **Entity Objects** and their attributes, not database tables.
*   **Portability:** It is database-independent. The provider translates JPQL to SQL for the specific DB dialect.
*   **Example:** `SELECT u FROM User u WHERE u.age > 18`.

---

## 282. JPQL vs Native Query?

**Answer:**
*   **JPQL:** Operates on Entities. Database agnostic. Preferred for standard CRUD and business logic.
*   **Native Query:** Operates on Tables (SQL). Database specific.
    *   **Use Case:** When you need ultra-specific SQL features (Window functions, complex joins, stored procedure calls) not supported by JPQL.
    *   **Risk:** Ties your code to a specific database vendor.

---

## 283. What is Criteria API?

**Answer:**
**Criteria API** is a programmatic, type-safe way to define dynamic queries.
*   **Mechanism:** You build the query object using Java methods (`cb.equal()`, `cb.greaterThan()`) instead of string concatenation.
*   **Advantage:** Errors are caught at compile time. Useful for dynamic search filters (e.g., search screen with 10 optional fields).

---

## 284. What is named query?

**Answer:**
A **Named Query** is a statically defined query with a predefined unchangeable query string.
*   **Definition:** Defined on the Entity class using `@NamedQuery`.
*   **Performance:** Validated and parsed at application startup (fail-fast), creating a slight performance boost over dynamic JPQL.
*   **Usage:** `em.createNamedQuery("User.findAll").getResultList()`.

---

## 285. What is @Query annotation?

**Answer:**
In **Spring Data JPA**, `@Query` allows you to define JPQL or Native SQL directly on the Repository interface method.
*   **JPQL:** `@Query("SELECT u FROM User u WHERE u.email = ?1")`
*   **Native:** `@Query(value = "SELECT * FROM users WHERE email = ?1", nativeQuery = true)`

---

## 286. What is query derivation?

**Answer:**
**Query Derivation** (or Query Creation from Method Names) is a Spring Data JPA feature where the framework automatically generates the SQL based on the method name.
*   **Convention:** `findBy[Property][Condition]`.
*   **Examples:**
    *   `findByEmail(String email)`
    *   `findByAgeGreaterThan(int age)`
    *   `findByLastnameAndFirstname`

---

## 287. What is pagination?

**Answer:**
**Pagination** allows fetching large datasets in chunks (pages) rather than all at once.
*   **Interface:** `Pageable` and `Page<T>`.
*   **Usage:**
    ```java
    Pageable pageable = PageRequest.of(0, 10); // Page 0, Size 10
    Page<User> page = userRepository.findAll(pageable);
    List<User> users = page.getContent();
    ```

---

## 288. What is sorting in JPA?

**Answer:**
Sorting can be achieved via the `Sort` object or directly within `Pageable`.
*   **Usage:**
    ```java
    Sort sort = Sort.by(Sort.Direction.ASC, "lastname");
    List<User> users = userRepository.findAll(sort);
    ```

---

## 289. What is projection?

**Answer:**
**Projection** allows fetching only a **subset of attributes** (selective columns) instead of the entire Entity.
*   **Interface-based:** Define an interface with getter methods for the fields you want.
    ```java
    interface UserSummary {
        String getFirstname();
        String getLastname();
    }
    ```
*   Spring Data JPA automatically implements this interface and populates it.

---

## 290. What is DTO projection?

**Answer:**
**DTO (Data Transfer Object) Projection** maps the query result directly to a DTO class.
*   **Constructor Expression:** Used in JPQL.
    ```java
    @Query("SELECT new com.example.dto.UserDTO(u.firstname, u.lastname) FROM User u")
    List<UserDTO> findAllUserDTOs();
    ```
*   **Benefit:** Optimized read performance (fetches fewer columns) and decouples API response from DB Entity.

---

## 291. What is @Transactional propagation?

**Answer:**
**Propagation** defines how a business method relates to existing transactions.
*   **Definition:** "If a transaction exists, what should I do? If not, what should I do?"
*   **Usage:** `@Transactional(propagation = Propagation.REQUIRED)`.

---

## 292. Propagation types?

**Answer:**
1.  **REQUIRED (Default):** Use existing transaction if available, else create a new one.
2.  **REQUIRES_NEW:** Suspends current transaction and creates a new independent one.
3.  **MANDATORY:** Support current transaction; throw exception if none exists.
4.  **NEVER:** Throw exception if a transaction exists.
5.  **SUPPORTS:** Execute non-transactionally if none exists; else use existing.
6.  **NOT_SUPPORTED:** Suspend current transaction and execute non-transactionally.
7.  **NESTED:** Executes within a nested transaction (savepoint) if a current transaction exists.

---

## 293. Isolation levels?

**Answer:**
Isolation defines how one transaction sees the changes made by other concurrent transactions.
1.  **READ_UNCOMMITTED:** Dirty reads allowed (lowest isolation).
2.  **READ_COMMITTED:** Dirty reads prevented. Non-repeatable reads possible (Default for Postgres, SQL Server, Oracle).
3.  **REPEATABLE_READ:** Non-repeatable reads prevented. Phantom reads possible (Default for MySQL).
4.  **SERIALIZABLE:** Strongest. Transactions run sequentially (no concurrency side effects).

---

## 294. What is optimistic locking?

**Answer:**
**Optimistic Locking** assumes conflicts are rare. It prevents lost updates without database locks.
*   **Mechanism:** Adds a `@Version` field (number/timestamp) to the entity.
*   **Update:**
    *   Read entity (version = 1).
    *   Update entity.
    *   Save: `UPDATE table SET ..., version = 2 WHERE id = 1 AND version = 1`.
    *   If 0 rows updated (version changed by someone else), throw `OptimisticLockException`.

---

## 295. What is pessimistic locking?

**Answer:**
**Pessimistic Locking** assumes conflicts are likely. It locks the database row when reading data.
*   **Mechanism:** `SELECT ... FOR UPDATE`.
*   **Types:**
    *   `PESSIMISTIC_READ`: Shared lock.
    *   `PESSIMISTIC_WRITE`: Exclusive lock.
*   **Usage:** `entityManager.find(User.class, 1L, LockModeType.PESSIMISTIC_WRITE)`.

---

## 296. What is @Version?

**Answer:**
**@Version** is used to enable **Optimistic Locking** for an entity.
*   **Field types:** `int`, `Integer`, `short`, `Short`, `long`, `Long`, `Timestamp`.
*   **Automatic:** JPA provider automatically manages this field. You should **not** set it manually.

---

## 297. What is transaction rollback rules?

**Answer:**
By default, Spring rolls back a transaction only for **Unchecked Exceptions** (`RuntimeException` and `Error`).
*   **Checked Exceptions:** It commits even if a checked rules exception is thrown (`SQLException`, `IOException`).
*   **Customization:**
    *   `@Transactional(rollbackFor = Exception.class)` (Rollback for all).
    *   `@Transactional(noRollbackFor = SpecificException.class)`.

---

## 298. What is readOnly transaction?

**Answer:**
`@Transactional(readOnly = true)` is a hint to the transaction manager that the transaction will only read data.
*   **Optimizations:**
    *   **Hibernate:** Disables dirty checking (performance boost).
    *   **Database:** May omit locking or use a read replica.
*   **Safety:** Writing data typically fails (depending on implementation).

---

## 299. What is Open Session in View?

**Answer:**
**Open Session In View (OSIV)** is a pattern (enabled by default in Spring Boot) that keeps the Hibernate `Session` open until the view is rendered.
*   **Pro:** Prevents `LazyInitializationException` in the Controller/View layer.
*   **Con:** Keeps database connection held for longer (during view rendering). Can cause performance issues under load.
*   **Best Practice:** Disable it (`spring.jpa.open-in-view=false`) and use DTOs/Join Fetch in the Service layer.

---

## 300. How to improve JPA performance?

**Answer:**
1.  **Solve N+1:** Use `JOIN FETCH` or `@EntityGraph`.
2.  **Lazy Loading:** Prefer `Lazy` fetch type over `Eager`.
3.  **Projections:** Fetch only needed columns (DTOs).
4.  **Read-Only:** Use `@Transactional(readOnly = true)`.
5.  **Batching:** Enable JDBC batching (`spring.jpa.properties.hibernate.jdbc.batch_size=30`).
6.  **Caching:** Use 2nd Level Cache (EhCache, Redis) for read-heavy data.
7.  **Connection Pooling:** Use HikariCP (default in Boot).

---

## 301. Second-level cache?

**Answer:**
**Second-Level Cache (L2 Cache)** is a session factory-level cache shared across all sessions/transactions.
*   **Scope:** Application-wide.
*   **Providers:** EhCache, Hazelcast, Infinispan, Redis.
*   **Usage:** Used for data that is read frequently but modified rarely (e.g., Reference Data, Product Catalog).
*   **Config:** Enabled via `spring.jpa.properties.hibernate.cache.use_second_level_cache=true` along with `@Cacheable` entities.

---

## 302. Query cache?

**Answer:**
**Query Cache** stores the **results of a query** (List of IDs) based on the query string and parameters.
*   **Dependency:** Requires L2 Cache to be enabled.
*   **Mechanism:**
    1.  Query executes -> returns IDs.
    2.  Hibernate looks up entities by ID in L2 Cache.
*   **Warning:** Can be harmful if the underlying tables are updated frequently (invalidates the cache often).

---

## 303. What is Hibernate interceptor?

**Answer:**
**Interceptor** allows the application to inspect and/or manipulate properties of a persistent object before it is saved, updated, deleted, or loaded.
*   **Interface:** `org.hibernate.Interceptor`.
*   **Methods:** `onSave`, `onFlushDirty`, `onDelete`.
*   **Use Case:** Auditing (setting `created_by`, `updated_at`), Logging, Multi-tenancy filters.

---

## 304. What is event listener?

**Answer:**
The Hibernate **Event System** is a more granular alternative to Interceptors.
*   **Mechanism:** You can register listeners for specific events (e.g., `PostInsertEvent`, `PreUpdateEvent`).
*   **Benefit:** Access to the `Event` object containing detailed context.
*   **Spring:** Spring Data simplifies this with `@EntityListeners` (e.g., `AuditingEntityListener`).

---

## 305. What is batch fetching?

**Answer:**
**Batch Fetching** is an optimization strategy to solve the N+1 problem by fetching multiple initialized proxies in a single query.
*   **Annotation:** `@BatchSize(size = 10)`.
*   **Scenario:** If you iterate over a list of 10 users and access their lazy-loaded `orders`, Hibernate will execute 1 query to fetch orders for *all 10 users* (using `WHERE user_id IN (?, ?, ...)`), instead of 10 separate queries.

---

## 306. What is stateless session?

**Answer:**
**StatelessSession** is a command-oriented API that does **not** keep a persistence context (first-level cache).
*   **Behavior:** No write-behind, no dirty checking, no cascading. Changes are immediate.
*   **Use Case:** Bulk data operations (Import/Export) where you want to avoid OutOfMemoryErrors caused by a massive First-Level Cache.

---

## 307. What is fetch join?

**Answer:**
`JOIN FETCH` is a JPQL/HQL syntax to eagerly load associated entities in a single query.
*   **Syntax:**
    ```sql
    SELECT u FROM User u JOIN FETCH u.department
    ```
*   **Effect:** Overrides the `FetchType.LAZY` setting for that specific query, ensuring the associated `department` is initialized.

---

## 308. What is entity graph?

**Answer:**
**Entity Graph** is a JPA standard for defining a graph of entities to be fetched.
*   **Role:** Acts as a dynamic "Fetch Plan".
*   **Usage:**
    ```java
    @EntityGraph(attributePaths = {"orders", "orders.items"})
    User findWithOrdersByEmail(String email);
    ```
*   **Result:** Generates a single SQL query with necessary JOINs.

---

## 309. What is multi-tenancy?

**Answer:**
**Multi-tenancy** is an architecture where a single instance of software runs on a server and serves multiple organizations (tenants).
*   **Strategies in Hibernate:**
    1.  **Separate Database:** One DB per tenant (safest).
    2.  **Separate Schema:** One Schema per tenant (shared DB).
    3.  **Discriminator Column:** Shared table with a `tenant_id` column (cheapest, strictly logic-based separation).

---

## 310. How to handle large datasets efficiently?

**Answer:**
1.  **Use Pagination:** Never fetch `findAll()`.
2.  **StatelessSession:** Bypass the first-level cache overhead.
3.  **DTOs:** Read-only DTOs are faster than managed Entities.
4.  **ScrollableResults:** Stream results from the DB cursor instead of loading all into memory.
5.  **Bulk Operations:** Use JPQL `UPDATE`/`DELETE` (`em.createQuery("UPDATE...").executeUpdate()`) instead of modifying entities one by one.
