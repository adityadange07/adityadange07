
## 401. What is normalization?

**Answer:**
**Normalization** is the process of organizing data in a database to avoid data redundancy and modification anomalies (Update, Insertion, Deletion).
*   **Goal:** Divide larger tables into smaller tables and link them using relationships.
*   **Benefit:** Reduces data duplication, ensures data consistency.

---

## 402. Explain 1NF, 2NF, 3NF, BCNF.

**Answer:**
*   **1NF (First Normal Form):** Atomic values. Each cell contains a single value (no comma-separated lists), and each record is unique.
*   **2NF:** 1NF + No Partial Dependency. All non-key attributes must depend on the *entire* Primary Key (not just part of a composite key).
*   **3NF:** 2NF + No Transitive Dependency. Non-key attributes must depend *only* on the Candidate Key (Primary Key), not on other non-key attributes.
*   **BCNF (Boyce-Codd keys Normal Form):** A stricter 3NF. For every functional dependency X -> Y, X must be a superkey.

---

## 403. What is denormalization?

**Answer:**
**Denormalization** is the process of adding redundant data to an already normalized database to improve read performance.
*   **Trade-off:** Faster reads (fewer JOINS) vs Slower writes (update data in multiple places) and higher storage.
*   **Use Case:** Data Warehousing, Reporting.

---

## 404. What is primary key?

**Answer:**
A **Primary Key** is a column (or set of columns) that uniquely identifies each row in a table.
*   **Constraints:** Must be UNIQUE and NOT NULL.
*   **Limit:** Only one Primary Key per table.

---

## 405. What is composite key?

**Answer:**
A **Composite Key** is a Primary Key that consists of two or more columns.
*   **Example:** In a `Student_Course` table, neither `student_id` nor `course_id` is unique alone, but the combination (`student_id`, `course_id`) is unique.

---

## 406. What is foreign key?

**Answer:**
A **Foreign Key** is a column that establishes a link between data in two tables.
*   **Role:** It refers to the Primary Key of another table.
*   **Constraint:** Enforces **Referential Integrity** (cannot have a foreign key value that doesn't exist in the parent table).

---

## 407. What is unique constraint?

**Answer:**
A **Unique Constraint** ensures that all values in a column are distinctive.
*   **Difference from Primary Key:**
    1.  A table can have **multiple** Unique Constraints.
    2.  Unique Constraint columns **can** contain NULL values (usually one NULL allowed per column, depending on DB).

---

## 408. What is indexing?

**Answer:**
**Indexing** is a data structure technique used to quickly locate and access the data in a database table.
*   **Structure:** Usually B-Trees or Hash tables.
*   **Trade-off:** Speeds up `SELECT` queries (WHERE clause) but slows down `INSERT`/`UPDATE` (as index must be updated too).

---

## 409. Types of indexes in MySQL?

**Answer:**
1.  **B-Tree Index:** Default. Good for range queries (`>`, `<`) and equality.
2.  **Hash Index:** Extremely fast for exact lookups (`=`), but no range support.
3.  **Full-text Index:** For text searching.
4.  **Spatial Index (R-Tree):** For geographic data.

---

## 410. What is clustered index?

**Answer:**
*   **Clustered Index:** Defines the physical order of data in the table.
    *   The "Leaf Nodes" contain the **actual data rows**.
    *   **Limit:** Only 1 per table (usually the Primary Key).
*   **Non-Clustered Index:** Stored separately from data.
    *   Leaf nodes contain a pointer to the data row (or Primary Key).
    *   Can have multiple per table.

---

## 411. What is EXPLAIN plan?

**Answer:**
**EXPLAIN** is a keyword in SQL (e.g., MySQL, PostgreSQL) used to analyze how the database executes a query.
*   **Output:** It shows the execution plan: which indexes are used, how tables are joined, and estimated row counts.
*   **Usage:** Crucial for optimizing slow queries.

---

## 412. What is query optimization?

**Answer:**
**Query Optimization** is the process of improving the execution speed of SQL queries.
*   **Techniques:**
    1.  **Indexing:** Ensure `WHERE`, `JOIN`, and `ORDER BY` columns are indexed.
    2.  **Avoid SELECT *:** Retrieve only necessary columns.
    3.  **Analyze EXPLAIN plan:** Identify bottlenecks (e.g., Full Table Scans).
    4.  **Denormalization:** For read-heavy systems.

---

## 413. What is full table scan?

**Answer:**
A **Full Table Scan** occurs when the database reads **every row** in the table to find the desired results.
*   **Cause:** Missing indexes or using functions on indexed columns (e.g., `WHERE YEAR(date_col) = 2023`).
*   **Performance:** Very slow for large tables. Always aim to convert these to **Index Scans**.

---

## 414. What is covering index?

**Answer:**
A **Covering Index** is an index that contains (covers) **all** the columns required by the query (both in `WHERE` and `SELECT` clauses).
*   **Benefit:** The DB can retrieve the data directly from the index structure without looking up the actual table rows (Clustered Index). This is extremely fast.

---

## 415. What is composite index?

**Answer:**
A **Composite Index** is an index on multiple columns (e.g., `INDEX(last_name, first_name)`).
*   **Rule:** **Leftmost Prefix Rule**. The index is effective only if the query uses the leftmost columns.
    *   Query on `last_name` -> Uses Index.
    *   Query on `last_name` AND `first_name` -> Uses Index.
    *   Query on `first_name` -> **Does NOT** use Index.

---

## 416. What is cardinality?

**Answer:**
**Cardinality** refers to the uniqueness of data values in a column.
*   **High Cardinality:** Many unique values (e.g., Email, UUID). **Good for indexing**.
*   **Low Cardinality:** Few unique values (e.g., Gender, Boolean). **Bad for indexing** (DB prefers Full Table Scan).

---

## 417. What is slow query log?

**Answer:**
**Slow Query Log** is a database feature (available in MySQL, Postgres) that records queries taking longer than a specified threshold (e.g., 2 seconds).
*   **Purpose:** Helps identify which queries need optimization.

---

## 418. What is query cache?

**Answer:**
**Query Cache** stores the text of a `SELECT` statement together with the corresponding result used.
*   **Mechanism:** If an identical query is received, the DB serves the result from the cache.
*   **Note:** Deprecated/Removed in MySQL 8.0 because it creates contention locks and is invalidated too frequently.

---

## 419. What is partitioning?

**Answer:**
**Partitioning** splits a large table into smaller, more manageable pieces (partitions), while still treating it as a single logical table.
*   **Types:**
    1.  **Range:** By date (e.g., `orders_2022`, `orders_2023`).
    2.  **List:** By discrete values (e.g., Region: `US`, `EU`).
    3.  **Hash:** Random distribution.

---

## 420. What is sharding?

**Answer:**
**Sharding** is a horizontal scaling strategy where data is distributed across **multiple database servers** (shards).
*   **Difference from Partitioning:** Partitioning is on the *same* server; Sharding is on *different* servers.
*   **Complexity:** Application needs to know which shard to query (e.g., `User ID % 4`). Handling joins across shards is very difficult.

---

## 421. What is ACID?

**Answer:**
**ACID** is a set of properties that guarantee valid database transactions.
1.  **Atomicity:** All or nothing. The transaction either completes entirely or fails entirely (Rollback).
2.  **Consistency:** The DB goes from one valid state to another (constraints respected).
3.  **Isolation:** Concurrent transactions don't interfere with each other.
4.  **Durability:** Once committed, data is permanent (persisted to disk), even if power fails.

---

## 422. What are isolation levels?

**Answer:**
**Isolation Levels** define the degree to which a transaction is isolated from others.
1.  **Read Uncommitted:** Lowest. Allows Dirty Reads.
2.  **Read Committed:** Default in many DBs (Oracle, Postgres). Prevents Dirty Reads.
3.  **Repeatable Read:** Default in MySQL. Prevents Dirty and Non-repeatable Reads.
4.  **Serializable:** Highest. Strict serial execution. Prevents all anomalies but slow.

---

## 423. What is dirty read?

**Answer:**
**Dirty Read** occurs when a transaction reads data that has been modified by another transaction but **not yet committed**.
*   **Risk:** If the other transaction rolls back, the first transaction has read invalid data.

---

## 424. What is non-repeatable read?

**Answer:**
**Non-Repeatable Read** occurs when a transaction reads the **same row twice** and gets different values.
*   **Cause:** Another transaction modified or deleted that row and committed in between the two reads.

---

## 425. What is phantom read?

**Answer:**
**Phantom Read** occurs when a transaction reads a set of rows satisfying a condition (e.g., `WHERE age > 10`) twice and gets a **different number of rows**.
*   **Cause:** Another transaction **inserted** or **deleted** rows that match the condition in between the reads.

---

## 426. What is MVCC?

**Answer:**
**MVCC (Multi-Version Concurrency Control)** is a method used by databases (Postgres, MySQL/InnoDB) to handle concurrency without locking the entire database.
*   **Mechanism:** It keeps multiple versions of the data. Readers read an older version ("snapshot") while writers create a new version.
*   **Benefit:** **Readers don't block Writers**, and Writers don't block Readers.

---

## 427. What is row-level locking?

**Answer:**
**Row-Level Locking** locks only the specific rows being accessed or modified by a transaction.
*   **Pro:** High concurrency (many users can edit different rows in the same table).
*   **Con:** High memory overhead (managing millions of locks).

---

## 428. What is table-level locking?

**Answer:**
**Table-Level Locking** locks the entire table.
*   **Pro:** Low overhead (just 1 lock). Fast for bulk updates.
*   **Con:** Poor concurrency (only 1 user can write to the table at a time).

---

## 429. What is deadlock in DB?

**Answer:**
A **Deadlock** happens when two or more transactions are waiting for each other to give up locks.
*   **Scenario:**
    *   Tx1 holds Lock A, waits for Lock B.
    *   Tx2 holds Lock B, waits for Lock A.
*   **Result:** Neither can proceed. The DB eventually kills one transaction to break the cycle.

---

## 430. How to prevent DB deadlocks?

**Answer:**
1.  **Consistent Order:** Always access resources (tables/rows) in the same order in all transactions.
2.  **Keep Tx Short:** Reduce the time locks are held.
3.  **Lock Escalation:** Lock the parent (e.g., Table) if modifying many children rows to avoid row-lock limit.
4.  **Timeouts:** Configure lock wait timeouts.

---

## 431. Vertical vs horizontal scaling?

**Answer:**
*   **Vertical Scaling (Breadth-First):** Adding more power (CPU, RAM, SSD) to an existing server.
    *   *Limit:* Hardware constraints. Single Point of Failure.
*   **Horizontal Scaling (Scale-Out):** Adding more machines (servers) to the resource pool.
    *   *Limit:* Complexity (needs load balancing, distributed consensus). Unlimited theoretical scale.

---

## 432. What is replication?

**Answer:**
**Replication** is the process of copying data from one database server to one or more other servers.
*   **Goal:**
    1.  **Redundancy:** If one node fails, data is safe.
    2.  **Performance:** Distribute read queries to multiple nodes.

---

## 433. Master-slave replication?

**Answer:**
**Master-Slave Replication** is a common architecture.
*   **Master:** Handles all **writes** (INSERT, UPDATE, DELETE) and replicates updates to slaves.
*   **Slave:** Handles **read only** queries.
*   **Lag:** Slaves might be slightly behind the Master (Eventual Consistency).

---

## 434. What is read replica?

**Answer:**
A **Read Replica** is a copy of the primary database used exclusively for read operations.
*   **Use Case:** Offload reporting queries or high-volume reads from the Master database to improve overall performance.

---

## 435. What is failover?

**Answer:**
**Failover** is the automatic process of switching to a redundant or standby database server upon the failure of the primary server.
*   **Mechanism:** If Master is unreachable, a monitoring system/tool (like Orchestrator or AWS RDS) promotes a Slave to be the new Master.

---

## 436. What is connection pooling?

**Answer:**
**Connection Pooling** is a cache of database connections maintained so that the connections can be reused when future requests to the database are required.
*   **Why?** Creating a new DB connection is expensive (TCP Handshake, Auth).
*   **Tool:** **HikariCP** (Default in Spring Boot).

---

## 437. What is database migration?

**Answer:**
**Database Migration** is the process of managing incremental, reversible changes to relational database schemas.
*   **Concept:** Treat DB schema changes like code (Version Control).
*   **Benefit:** Consistency across environments (Dev, Test, Prod).

---

## 438. What is Flyway/Liquibase?

**Answer:**
They are **Database Migration Tools** used in Java.
*   **Flyway:** Uses SQL files (e.g., `V1__init.sql`). Simple and favors SQL.
*   **Liquibase:** Uses abstract formats (XML, YAML, JSON) or SQL. Better for database independence.
*   **Mechanism:** They create a table (e.g., `flyway_schema_history`) to track which scripts have already run.

---

## 439. How to design high-traffic DB?

**Answer:**
1.  **Caching:** Use Redis to reduce DB load.
2.  **Read Replicas:** Scale reads horizontally.
3.  **Indexing:** Optimize queries.
4.  **Partitioning/Sharding:** Split large tables.
5.  **Denormalization:** Avoid complex joins for critical paths.
6.  **Connection Pooling:** Efficient resource usage.

---

## 440. When to use NoSQL?

**Answer:**
Use **NoSQL** (MongoDB, Cassandra) when:
1.  **Schema is flexible/dynamic:** Adding fields without migrations.
2.  **Massive Scale:** Needs effortless horizontal scaling (Sharding built-in).
3.  **Unstructured Data:** JSON documents, Graphs.
4.  **High Write Throughput:** Log ingestion, IoT data.

---

## 441. What is stored procedure?

**Answer:**
A **Stored Procedure** is a prepared SQL code that you can save so the code can be reused over and over again.
*   **Pros:** Reduces network traffic (logic runs on DB server), centralized logic, maintainability.
*   **Cons:** Hard to debug/version control, vendor lock-in (PL/SQL vs T-SQL), increases load on DB server.

---

## 442. What is trigger?

**Answer:**
A **Trigger** is a set of SQL statements that automatically executes (fires) in response to certain events on a particular table.
*   **Events:** `INSERT`, `UPDATE`, `DELETE`.
*   **Timing:** `BEFORE`, `AFTER` (e.g., `BEFORE INSERT`).
*   **Use Case:** Audit trails, enforcing complex constraints, automating actions (updating a `last_modified` timestamp).

---

## 443. What is view?

**Answer:**
A **View** is a virtual table based on the result-set of an SQL statement.
*   **Storage:** It does **not store data** itself; it only stores the query definition.
*   **Use Case:** Simplify complex queries (hide joins), restrict access to specific columns (security).

---

## 444. What is materialized view?

**Answer:**
A **Materialized View** is a view that **physically stores** the result set on disk.
*   **Difference from View:** It is not virtual. It calculates the data beforehand.
*   **Pros:** Extremely fast reads for expensive aggregations.
*   **Cons:** Data is not real-time (must be refreshed). Good for reporting/warehousing.

---

## 445. What is indexing strategy for large tables?

**Answer:**
1.  **Cardinality Analysis:** Only index high-cardinality columns.
2.  **Composite Indexes:** Use multi-column indexes for common `WHERE` clauses (remember Leftmost Prefix).
3.  **Covering Indexes:** Include selected columns in the index to avoid table lookups.
4.  **Partial Indexes:** Index only a subset of rows (e.g., `WHERE active = true`).
5.  **Write Overhead:** Don't over-index; writes become slow.

---

## 446. What is composite vs multiple index?

**Answer:**
*   **Composite Index:** One index on multiple columns `(A, B)`.
    *   Good for `WHERE A=1 AND B=1`.
    *   Good for `WHERE A=1`.
    *   **Bad** for `WHERE B=1` (cannot use index).
*   **Multiple Indexes:** Separate indexes on `A` and `B`.
    *   DB might use "Index Merge" (use both and intersect), but usually less efficient than a proper Composite Index for combined queries.

---

## 447. What is pagination performance issue?

**Answer:**
Using `OFFSET` and `LIMIT` becomes very slow for large offsets (e.g., `LIMIT 10 OFFSET 1000000`).
*   **Why?** The DB must read and discard the first 1,000,000 rows to find the next 10.
*   **Time Complexity:** O(N) where N is the offset.

---

## 448. What is cursor-based pagination?

**Answer:**
**Cursor-based (Keyset) Pagination** solves the `OFFSET` problem by using a unique column (like ID or Timestamp) to find the "next" page.
*   **Query:** `SELECT * FROM users WHERE id > :last_seen_id ORDER BY id ASC LIMIT 10`.
*   **Benefit:** Is instantaneous (O(1) or O(log N) with index) regardless of how deep the page is.
*   **Drawback:** Cannot jump to specific page (e.g., "Go to Page 50").

---

## 449. What is data archiving?

**Answer:**
**Data Archiving** is the process of moving data that is no longer actively used to a separate storage device for long-term retention.
*   **Goal:** Keep the "Hot" database small and fast.
*   **Strategy:** Move "Cold" data (e.g., orders older than 1 year) to an Archive DB or Data Warehouse (S3/Snowflake) via ETL jobs.

---

## 450. How to handle millions of records?

**Answer:**
1.  **Indexing:** Essential for retrieval.
2.  **Partitioning:** Break table by date/ID range.
3.  **Sharding:** Distribute across servers.
4.  **Batch Processing:** Process updates in chunks (Batch size 1000), not one-by-one.
5.  **Asynchronous Processing:** Use queues (Kafka) to decouple ingestion from processing.
6.  **Caching:** Cache frequent reads.

---

## 451. Design schema for e-commerce system.

**Answer:**
**Core Tables:**
1.  `Users`: `id`, `email`, `password_hash`, `role`.
2.  `Products`: `id`, `name`, `description`, `price`, `stock_quantity`, `category_id`.
3.  `Categories`: `id`, `name`, `parent_id` (for hierarchy).
4.  `Orders`: `id`, `user_id`, `total_amount`, `status`, `created_at`.
5.  `OrderItems`: `id`, `order_id`, `product_id`, `quantity`, `price_at_purchase`.
6.  `Cart`: `id`, `user_id`. `CartItems` link to Products.

---

## 452. Design schema for order management.

**Answer:**
Focus on **state transitions** and **history**:
1.  `Orders`: The header information.
2.  `OrderHistory`: `id`, `order_id`, `status_from`, `status_to`, `changed_by`, `timestamp`. Essential for tracking lifecycle (Created -> Paid -> Shipped).
3.  `Payments`: `id`, `order_id`, `transaction_id`, `amount`, `status`, `provider` (Stripe/PayPal).
4.  `Shipments`: `id`, `order_id`, `tracking_number`, `courier`.

---

## 453. How to handle soft delete?

**Answer:**
**Soft Delete** marks a record as deleted without physically removing it from the database.
*   **Column:** Add `is_deleted` (BOOLEAN) or `deleted_at` (TIMESTAMP) to the table.
*   **Query:** All queries must filter `WHERE is_deleted = false`.
*   **Pros:** Data recovery, audit history.
*   **Cons:** Complexity in unique indexes (unique constraint on `email` + `deleted_at` needed), increased storage.

---

## 454. How to handle audit fields?

**Answer:**
Every table should ideally have:
1.  `created_at`: Timestamp.
2.  `created_by`: User ID.
3.  `updated_at`: Timestamp.
4.  `updated_by`: User ID.
*   **Implementation:** Use JPA `@PrePersist` and `@PreUpdate` or Hibernate Envers for full revision history (separate audit tables).

---

## 455. How to design multi-tenant DB?

**Answer:**
1.  **Database per Tenant:** Secure, isolated, expensive to maintain.
2.  **Schema per Tenant:** Shared DB, separate schemas. Good balance.
3.  **Shared Schema (Discriminator Column):** Add `tenant_id` to **every** table.
    *   *Pro:* Cheap, easy to scale.
    *   *Con:* Developer error (forgetting `WHERE tenant_id = ?`) causes data leaks. Use Hibernate Filters to enforce automatically.

---

## 456. How to prevent duplicate data?

**Answer:**
1.  **Database Constraints:** Use `UNIQUE` constraints (e.g., on `email` or composite key). This is the last line of defense.
2.  **Application Logic:** Check before insert (Race conditions possible).
3.  **Idempotency Keys:** For API requests.
4.  **Locks:** Pessimistic locking during check-then-insert.

---

## 457. How to handle transactional consistency?

**Answer:**
*   **Within one DB:** Use `@Transactional`.
*   **Across Microservices (Distributed):**
    1.  **Two-Phase Commit (2PC):** Strict but slow.
    2.  **Saga Pattern:** Choreography or Orchestration using compensating transactions (Undo actions) and Eventual Consistency.

---

## 458. How to design for high write throughput?

**Answer:**
1.  **Remove Secondary Indexes:** Indexes slow down writes.
2.  **Batch Inserts:** Insert 1000 rows in 1 query.
3.  **Partitioning:** Distribute writes across partitions.
4.  **NoSQL:** Cassandra/DynamoDB are optimized for writes (LSM Trees).
5.  **Asynchronous:** Write to a Queue (Kafka) first, then consume and interact with DB at a controlled pace.

---

## 459. How to reduce DB load?

**Answer:**
1.  **Caching:** Redis for frequent reads.
2.  **Read Replicas:** Move read operations to slaves.
3.  **Optimize Queries:** Indexing, avoiding wildcard scans.
4.  **CDN:** Serve static assets (images) away from your servers.
5.  **Archive:** Move old data out.

---

## 460. How to handle schema evolution?

**Answer:**
**Schema Evolution** handling changes without downtime:
1.  **Backward Compatibility:** New columns must be nullable or have defaults.
2.  **Deprecation:** Never delete a column immediately.
    *   Step 1: Renamed/Ignore in code.
    *   Step 2: Deploy code that doesn't use it.
    *   Step 3: Drop column in next release.
3.  **Tools:** Liquibase/Flyway for versioned DDL.

---

## 461. DB CPU is high – how to debug?

**Answer:**
1.  **Check Active Queries:** Use `SHOW PROCESSLIST` (MySQL) or `pg_stat_activity` (Postgres) to find running queries.
2.  **Slow Query Log:** Check if a specific query is appearing frequently.
3.  **Explain Plan:** Analyze the top resource-consuming queries for Full Table Scans.
4.  **Connection Count:** High concurrency might cause context switching overhead.

---

## 462. DB connections exhausted – solution?

**Answer:**
**Symptoms:** Application throws `ConnectionPoolExhaustedException`.
*   **Immediate Fix:** Increase pool size (temporarily).
*   **Root Cause Analysis:**
    1.  **Connection Leak:** App not closing connections (check `finally` block).
    2.  **Long Transactions:** Connections held too long.
    3.  **Scale:** Need `HikariCP` tuning or add Read Replicas.

---

## 463. Slow insert issue – possible causes?

**Answer:**
1.  **Too many indexes:** Every insert requires updating all indexes.
2.  **Lock Contention:** High concurrency on the same table/page.
3.  **Hardware Limits:** Disk I/O (IOPS) saturation.
4.  **Triggers:** Heavy logic executing on every insert.
5.  **Foreign Key Checks:** DB checks referential integrity.

---

## 464. Index not being used – why?

**Answer:**
Even if an index exists, the optimizer might ignore it:
1.  **Low Cardinality:** If the value matches 30%+ of rows, a Full Table Scan is faster.
2.  **Functions on Columns:** `WHERE YEAR(date)` invalidates the index.
3.  **Data Type Mismatch:** Comparing String to Int.
4.  **OR Condition:** Using `OR` on non-indexed columns.
5.  **Leftmost Prefix Violation:** In `(A, B)`, querying on `B` only.

---

## 465. Long-running transaction impact?

**Answer:**
1.  **Locks:** Holds locks on rows/tables, blocking other writers (and potentially readers).
2.  **Undo Log Growth:** In MVCC, old versions must be kept until the transaction finishes, bloating storage.
3.  **Replication Lag:** Slaves cannot replay the transaction until it commits on Master.

---

## 466. Lock wait timeout – causes?

**Answer:**
The application fails with `LockWaitTimeoutException`.
*   **Causes:**
    1.  **Deadlocks:** Two tx waiting for each other.
    2.  **Long Transactions:** Tx A holds lock for 50s; Tx B waits and times out (default 50s in MySQL).
    3.  **Uncommitted Tx:** Developer ran a query manually and forgot to `COMMIT`.

---

## 467. Data inconsistency in distributed system?

**Answer:**
**Scenario:** Order service says "Paid", but Delivery service says "Payment Pending".
*   **Causes:**
    1.  **Network Partition:** Event failed to publish to Kafka.
    2.  **Distributed Tx Failure:** Commit failed in one service but succeeded in another.
    3.  **Replication Lag:** Reading from a stale slave.
*   **Fix:** Reconciliation jobs (Cron) or Saga Pattern (Compensating transactions).

---

## 468. Large join performance issue?

**Answer:**
Queries joining huge tables (Millions of rows) are slow.
*   **Fixes:**
    1.  **Indexing:** Ensure Join Keys (`ON t1.id = t2.id`) are indexed.
    2.  **Reduce Set:** Filter (`WHERE`) *before* joining.
    3.  **Denormalization:** Store required fields in one table to avoid the join.
    4.  **Application Join:** Fetch IDs and join in Java (sometimes faster).

---

## 469. Missing index issue?

**Answer:**
**Symptom:** API is slow (2s+), CPU high.
*   **Diagnosis:** Run `EXPLAIN` on the query. Look for `type: ALL` (Full Table Scan) or `rows: 1000000`.
*   **Fix:** Create the appropriate index. Note that creating an index on a large live table can accept locks (use Online DDL).

---

## 470. Real production DB issue you handled?

**Answer:**
*   **Situation:** Black Friday access spike caused DB CPU to hit 100%.
*   **Analysis:** `SHOW PROCESSLIST` revealed thousands of identical `SELECT * FROM products` queries.
*   **Root Cause:** A new feature introduced an N+1 query problem, fetching product details in a loop.
*   **Resolution:** Hotfix to cache the data in Redis and refactor code to use `IN` clause (Batch fetching).
