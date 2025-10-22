Here are the **Top 50 MySQL Interview Questions and Answers** tailored for professionals with **4+ years of experience**, covering SQL querying, indexing, performance tuning, normalization, transactions, stored procedures, replication, and more.

---

## ✅ Top 50 MySQL Interview Questions (4 Years Experience)

---

### 🔹 Basics & SQL Queries

1. **What is MySQL and how is it different from SQL?**
    - **MySQL** is a relational database management system.
    - **SQL** is the language used to interact with RDBMS.

---

2. **What are the different types of joins in MySQL?**
    - `INNER JOIN`, `LEFT JOIN`, `RIGHT JOIN`, `FULL JOIN` (simulated), `SELF JOIN`, `CROSS JOIN`.

---

3. **What is the difference between `WHERE` and `HAVING` clause?**
    - `WHERE`: Filters rows before aggregation.
    - `HAVING`: Filters after aggregation.

---

4. **What is the use of `GROUP BY` in SQL?**  
   Groups rows with the same values and allows aggregate functions like `SUM()`, `COUNT()`, etc.

---

5. **What is the difference between `UNION` and `UNION ALL`?**
    - `UNION`: Removes duplicates.
    - `UNION ALL`: Keeps all records.

---

6. **How do you fetch the nth highest salary from a table?**  
   Using `LIMIT` and `OFFSET` or subqueries with `DISTINCT`.

---

7. **What are subqueries and correlated subqueries?**
    - **Subquery**: Independent query.
    - **Correlated subquery**: Depends on the outer query.

---

8. **How do you perform pagination in MySQL?**  
   Using `LIMIT` and `OFFSET`:
   ```sql
   SELECT * FROM table LIMIT 10 OFFSET 20;
   ```

---

9. **What is the `EXPLAIN` keyword used for?**  
   Analyzes how MySQL executes a query — useful for optimization.

---

10. **How do you find duplicate records in MySQL?**
   ```sql
   SELECT name, COUNT(*) FROM users GROUP BY name HAVING COUNT(*) > 1;
   ```

---

### 🔹 Data Types & Constraints

11. **What are the different data types in MySQL?**
- Numeric: `INT`, `DECIMAL`, `FLOAT`
- Date/Time: `DATE`, `DATETIME`, `TIMESTAMP`
- String: `VARCHAR`, `TEXT`, `CHAR`

---

12. **What are primary keys and foreign keys?**
- **Primary Key**: Uniquely identifies rows
- **Foreign Key**: Enforces referential integrity

---

13. **What is the difference between `CHAR` and `VARCHAR`?**
- `CHAR`: Fixed-length
- `VARCHAR`: Variable-length

---

14. **What are constraints in MySQL?**
- `NOT NULL`, `UNIQUE`, `DEFAULT`, `CHECK`, `PRIMARY KEY`, `FOREIGN KEY`

---

15. **How do you define an auto-increment column?**
   ```sql
   id INT AUTO_INCREMENT PRIMARY KEY
   ```

---

### 🔹 Indexing & Optimization

16. **What is an index? Why is it used?**  
    Speeds up query execution on large datasets.

---

17. **What are the types of indexes in MySQL?**
- Primary index
- Unique index
- Full-text index
- Composite index
- Spatial index

---

18. **What is a composite index?**  
    An index on multiple columns.

---

19. **When should you avoid indexing?**  
    On frequently updated/deleted columns, or small tables.

---

20. **How do you view indexes on a table?**
   ```sql
   SHOW INDEX FROM table_name;
   ```

---

21. **What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?**
- `DELETE`: Deletes rows, can be rolled back
- `TRUNCATE`: Deletes all rows, faster, cannot rollback
- `DROP`: Deletes the table structure

---

22. **What are some ways to optimize a slow query?**
- Use indexes
- Avoid `SELECT *`
- Normalize data
- Use `EXPLAIN`

---

23. **What is query caching in MySQL?**  
    Caches query results to speed up repeated executions (deprecated in MySQL 8+).

---

24. **What is a covering index?**  
    An index that includes all columns used in a query.

---

25. **How does indexing affect write performance?**  
    Slows down `INSERT`, `UPDATE`, `DELETE` operations due to index maintenance.

---

### 🔹 Transactions & Concurrency

26. **What is a transaction in MySQL?**  
    A sequence of operations performed as a single unit of work.

---

27. **What are ACID properties?**
- **Atomicity**
- **Consistency**
- **Isolation**
- **Durability**

---

28. **How do you start and end a transaction in MySQL?**
   ```sql
   START TRANSACTION;  
   -- SQL statements  
   COMMIT;  
   -- or  
   ROLLBACK;
   ```

---

29. **What is the default isolation level in MySQL?**  
    `REPEATABLE READ`

---

30. **What are the isolation levels in MySQL?**
- `READ UNCOMMITTED`
- `READ COMMITTED`
- `REPEATABLE READ`
- `SERIALIZABLE`

---

31. **What is a deadlock? How do you resolve it?**  
    Two or more transactions wait for each other to release locks.  
    Resolved by timeout or manually killing one transaction.

---

32. **What is a savepoint?**  
    A point within a transaction to which you can rollback partially.

---

### 🔹 Views, Functions & Stored Procedures

33. **What is a view in MySQL?**  
    A virtual table based on a SQL query.

---

34. **Can views be updated?**  
    Yes, if they meet specific conditions (no joins, aggregates, etc.).

---

35. **What is a stored procedure?**  
    A reusable set of SQL statements stored in the database.

---

36. **What is the difference between a stored procedure and function?**
- Procedure: Doesn’t return a value
- Function: Returns a value and can be used in expressions

---

37. **How to call a stored procedure?**
   ```sql
   CALL procedure_name(params);
   ```

---

38. **How do you handle exceptions in stored procedures?**  
    Using `DECLARE ... HANDLER`.

---

### 🔹 Replication & Backup

39. **What is MySQL replication?**  
    Copying data from one server (master) to others (slaves/replicas).

---

40. **What are the types of MySQL replication?**
- Statement-based
- Row-based
- Mixed

---

41. **How do you take a backup in MySQL?**  
    Using `mysqldump` or `mysqlpump`.

---

42. **How do you restore a database backup?**
   ```bash
   mysql -u user -p db_name < backup.sql
   ```

---

43. **How do you check for replication lag?**  
    Query `SHOW SLAVE STATUS;` and check `Seconds_Behind_Master`.

---

44. **How to improve replication performance?**
- Use row-based replication
- Optimize queries
- Tune `sync_binlog`, `innodb_flush_log_at_trx_commit`

---

### 🔹 Advanced Concepts

45. **What is normalization?**  
    Process of organizing data to reduce redundancy and improve integrity.

---

46. **What are the normal forms in DBMS?**
- 1NF: Atomic columns
- 2NF: No partial dependency
- 3NF: No transitive dependency

---

47. **What is denormalization?**  
    Adding redundancy for performance optimization (e.g., joins become faster).

---

48. **What is a foreign key constraint?**  
    Ensures that the value in a column exists in another table’s primary key.

---

49. **What is `ENUM` in MySQL?**  
    A string object with a predefined set of values.

---

50. **How do you secure a MySQL database?**
- Set strong root password
- Use `GRANT` for privileges
- Disable remote root login
- Enable SSL for connections

---

Would you like a **PDF download**, or should I move on to **real-world MySQL scenarios**, **query challenges**, or **MySQL + Java integration questions** next?