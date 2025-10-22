Here are the **Top 50 MySQL Interview Questions and Answers**, crafted specifically for professionals with **5 years of experience**, covering advanced SQL, indexing, performance tuning, stored procedures, replication, transactions, and real-world use cases.

---

## ✅ Top 50 MySQL Interview Questions (5 Years Experience)

---

### 🔹 **SQL Queries & Joins**

1. **What are different types of joins in MySQL?**
    - `INNER JOIN`
    - `LEFT JOIN`
    - `RIGHT JOIN`
    - `FULL OUTER JOIN` (emulated using `UNION`)
    - `CROSS JOIN`

---

2. **What is the difference between `WHERE` and `HAVING`?**
    - `WHERE`: Filters rows **before** aggregation
    - `HAVING`: Filters rows **after** aggregation

---

3. **How do you find duplicate records in MySQL?**
   ```sql
   SELECT col, COUNT(*) 
   FROM table 
   GROUP BY col 
   HAVING COUNT(*) > 1;
   ```

---

4. **Write a query to fetch the second highest salary.**
   ```sql
   SELECT MAX(salary) 
   FROM employees 
   WHERE salary < (SELECT MAX(salary) FROM employees);
   ```

---

5. **What is the difference between `UNION` and `UNION ALL`?**
    - `UNION`: Removes duplicates
    - `UNION ALL`: Keeps duplicates

---

6. **How do you perform pagination in MySQL?**
   ```sql
   SELECT * FROM table LIMIT 10 OFFSET 20;
   ```

---

7. **What is a correlated subquery?**  
   A subquery that refers to a column from the outer query.

---

8. **What is the difference between `IN` and `EXISTS`?**
    - `IN`: Checks for values
    - `EXISTS`: Checks for the existence of rows (better performance for large datasets)

---

9. **What are window functions in MySQL?**  
   Functions like `ROW_NUMBER()`, `RANK()`, `LEAD()`, `LAG()` that operate over a set of rows.

---

10. **How do you use `CASE` in MySQL?**
   ```sql
   SELECT name,
     CASE WHEN salary > 50000 THEN 'High' ELSE 'Low' END AS salary_grade
   FROM employees;
   ```

---

### 🔹 **Indexes & Optimization**

11. **What is an index?**  
    A data structure that improves the speed of data retrieval operations on a database table.

---

12. **What are different types of indexes in MySQL?**
- Primary Key
- Unique Index
- Full-text Index
- Composite Index
- Spatial Index

---

13. **How do indexes improve performance?**  
    They reduce the amount of data the database needs to scan.

---

14. **What is a composite index?**  
    An index on multiple columns. Useful when queries involve all or leading columns.

---

15. **When should you avoid using indexes?**
- For small tables
- On columns with high update frequency
- On columns with low selectivity (many duplicates)

---

16. **How can you check if an index is used in a query?**  
    Use `EXPLAIN` or `EXPLAIN ANALYZE` before the query.

---

17. **What is index cardinality?**  
    The uniqueness of values in an index column; higher cardinality = better performance.

---

18. **What is a covering index?**  
    An index that contains all the columns required by the query.

---

19. **How to force an index in a query?**
   ```sql
   SELECT * FROM table FORCE INDEX (idx_name) WHERE col = 'value';
   ```

---

20. **What is index selectivity?**  
    Ratio of distinct values to total rows. High selectivity = better index efficiency.

---

### 🔹 **Transactions & Locking**

21. **What are ACID properties?**
- Atomicity
- Consistency
- Isolation
- Durability

---

22. **What is a transaction?**  
    A set of operations executed as a single unit that either all succeed or fail.

---

23. **How do you start and commit a transaction in MySQL?**
   ```sql
   START TRANSACTION;  
   -- queries  
   COMMIT;
   ```

---

24. **What is a savepoint?**  
    A point within a transaction to which you can rollback without affecting the entire transaction.

---

25. **What is the difference between `COMMIT` and `ROLLBACK`?**
- `COMMIT`: Saves the changes
- `ROLLBACK`: Reverts changes since last savepoint or transaction start

---

26. **What is a deadlock?**  
    When two or more transactions wait for each other to release locks.

---

27. **How can you detect and resolve deadlocks?**  
    MySQL detects and automatically rolls back one transaction. Use `SHOW ENGINE INNODB STATUS`.

---

28. **What are isolation levels in MySQL?**
- READ UNCOMMITTED
- READ COMMITTED
- REPEATABLE READ (default)
- SERIALIZABLE

---

29. **How does MySQL handle concurrency?**  
    Through locks and MVCC (Multi-Version Concurrency Control).

---

30. **What is the difference between pessimistic and optimistic locking?**
- Pessimistic: Locks record to prevent conflicts
- Optimistic: Uses versioning or timestamps

---

### 🔹 **Stored Procedures, Triggers & Views**

31. **What is a stored procedure?**  
    A precompiled SQL code block stored in the database.

---

32. **What is a trigger?**  
    A block of code that runs automatically before/after insert, update, delete.

---

33. **Difference between procedure and function?**
- Function returns a value
- Procedure may not return, used for operations

---

34. **What is a view in MySQL?**  
    A virtual table created using a SELECT query.

---

35. **What are the pros and cons of views?**  
    ✅ Simplifies complex queries  
    ❌ Not always up-to-date (especially with performance)

---

36. **Can views be indexed in MySQL?**  
    No, but indexed materialized views can be emulated via triggers + tables.

---

37. **How do you debug stored procedures?**  
    Use `SELECT`, `SET`, and `SHOW WARNINGS` inside procedures for debugging.

---

38. **Can triggers call stored procedures?**  
    Yes, but avoid complexity and recursion issues.

---

39. **How to prevent recursive trigger execution?**  
    Use flags or control logic to detect and stop recursion.

---

40. **What is the `INSTEAD OF` trigger?**  
    MySQL does **not** support it (unlike some other RDBMS like SQL Server).

---

### 🔹 **Administration & Tuning**

41. **How do you take a backup in MySQL?**  
    Using `mysqldump`, `mysqlpump`, or tools like Percona XtraBackup.

---

42. **What are common ways to optimize a slow query?**
- Indexing
- Avoiding `SELECT *`
- Use `EXPLAIN`
- Avoiding subqueries when joins are better

---

43. **How can you monitor slow queries?**  
    Enable and analyze the `slow_query_log`.

---

44. **What is MySQL replication?**  
    Copying data from one MySQL server to another (Master-Slave, Master-Master)

---

45. **How does MySQL replication work?**
- Master writes to binary log
- Slave reads and replays the log via `IO_THREAD` and `SQL_THREAD`

---

46. **What is GTID in replication?**  
    Global Transaction ID: simplifies failover and conflict resolution in replication.

---

47. **Difference between statement-based and row-based replication?**
- Statement-based: Replicates SQL queries
- Row-based: Replicates actual row changes

---

48. **How do you secure a MySQL server?**
- Strong passwords
- Limited privileges
- TLS
- Remove anonymous users and test DB
- Firewall protection

---

49. **What are MySQL storage engines?**
- **InnoDB** (default, supports transactions)
- **MyISAM** (faster reads, no transactions)
- **Memory**, **CSV**, **ARCHIVE**, etc.

---

50. **How do you choose between InnoDB and MyISAM?**
- Use **InnoDB** for most use cases (supports ACID, foreign keys, transactions)
- Use **MyISAM** only for specific use cases with heavy read-only workloads

---

Would you like this in **PDF format** or want **real-time scenario-based MySQL questions**, or **MySQL + Java/Spring Boot integration questions** next?