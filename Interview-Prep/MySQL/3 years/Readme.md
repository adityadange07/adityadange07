Here are the **Top 50 MySQL Interview Questions and Answers** tailored for someone with **3 years of experience**, covering concepts ranging from SQL fundamentals to advanced optimization, indexing, joins, transactions, and real-world scenarios.

---

## ✅ Top 50 MySQL Interview Questions (3 Years Experience)

---

### 🔹 **Basic SQL & MySQL Concepts**

1. **What is MySQL?**  
   MySQL is an open-source relational database management system based on SQL (Structured Query Language).

---

2. **What are the different data types in MySQL?**
    - Numeric: `INT`, `FLOAT`, `DOUBLE`, `DECIMAL`
    - Date/Time: `DATE`, `DATETIME`, `TIMESTAMP`
    - String: `VARCHAR`, `CHAR`, `TEXT`, `BLOB`

---

3. **Difference between `CHAR` and `VARCHAR`?**
    - `CHAR`: Fixed-length, faster
    - `VARCHAR`: Variable-length, more space-efficient

---

4. **What is the difference between `PRIMARY KEY` and `UNIQUE`?**
    - `PRIMARY KEY`: Uniqueness + NOT NULL
    - `UNIQUE`: Only uniqueness, allows NULLs

---

5. **What is the default port for MySQL?**
    - **3306**

---

6. **What are the different types of SQL statements?**
    - DDL (CREATE, ALTER, DROP)
    - DML (INSERT, UPDATE, DELETE)
    - DQL (SELECT)
    - DCL (GRANT, REVOKE)
    - TCL (COMMIT, ROLLBACK)

---

7. **How do you fetch the current date and time in MySQL?**
   ```sql
   SELECT NOW();
   ```

---

8. **What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?**
    - `DELETE`: Deletes rows, can be rolled back
    - `TRUNCATE`: Deletes all rows, cannot be rolled back
    - `DROP`: Deletes table structure

---

9. **What is the use of `AUTO_INCREMENT`?**  
   Automatically generates unique values for a column.

---

10. **How do you retrieve unique records?**
   ```sql
   SELECT DISTINCT column FROM table;
   ```

---

### 🔹 **Joins & Subqueries**

11. **Types of joins in MySQL?**
- INNER JOIN
- LEFT JOIN
- RIGHT JOIN
- FULL OUTER JOIN (emulated via UNION)
- SELF JOIN
- CROSS JOIN

---

12. **What is the difference between `INNER JOIN` and `LEFT JOIN`?**
- INNER JOIN: Only matching rows
- LEFT JOIN: All left + matched right rows

---

13. **What is a subquery?**  
    A query within another SQL query.

---

14. **What is a correlated subquery?**  
    A subquery that depends on the outer query for its values.

---

15. **How to find duplicate records in a table?**
   ```sql
   SELECT column, COUNT(*)  
   FROM table  
   GROUP BY column  
   HAVING COUNT(*) > 1;
   ```

---

16. **What is the difference between `WHERE` and `HAVING`?**
- `WHERE`: Filters rows before aggregation
- `HAVING`: Filters after aggregation

---

17. **How to perform a self join?**  
    Join a table with itself using aliases.

---

18. **What is the purpose of `GROUP BY`?**  
    Used to group rows that have the same values in specified columns.

---

19. **Can we use `GROUP BY` without `HAVING`?**  
    Yes, `HAVING` is optional.

---

20. **How do you retrieve the nth highest salary?**
   ```sql
   SELECT salary  
   FROM employees e1  
   WHERE N-1 = (SELECT COUNT(DISTINCT salary) FROM employees e2 WHERE e2.salary > e1.salary);
   ```

---

### 🔹 **Indexes & Optimization**

21. **What is an index?**  
    A data structure that improves query performance.

---

22. **Types of indexes in MySQL?**
- Primary
- Unique
- Full-text
- Composite
- Spatial

---

23. **How do indexes affect performance?**
- Speed up read operations
- Slow down write operations slightly due to maintenance

---

24. **What is a composite index?**  
    Index created on multiple columns.

---

25. **How to check if an index is being used?**  
    Use `EXPLAIN` before your query.

---

26. **When should you avoid using indexes?**
- On columns with many duplicate values
- On frequently updated columns

---

27. **How to force MySQL to use a specific index?**
   ```sql
   SELECT * FROM table USE INDEX (index_name);
   ```

---

28. **What is the query execution plan in MySQL?**  
    An internal plan MySQL uses to execute queries. Check using `EXPLAIN`.

---

29. **How to optimize a slow-running query?**
- Use indexing
- Avoid `SELECT *`
- Limit rows
- Optimize joins
- Analyze with `EXPLAIN`

---

30. **What is the difference between clustered and non-clustered index?**
- MySQL InnoDB has one clustered index (primary key)
- Secondary indexes point to primary key

---

### 🔹 **Transactions & Locks**

31. **What is a transaction in MySQL?**  
    A group of operations executed as a single unit.

---

32. **What are ACID properties?**
- Atomicity
- Consistency
- Isolation
- Durability

---

33. **How do you start and end a transaction in MySQL?**
   ```sql
   START TRANSACTION;  
   -- operations  
   COMMIT;  -- or ROLLBACK;
   ```

---

34. **What is the difference between `COMMIT` and `ROLLBACK`?**
- `COMMIT`: Saves changes
- `ROLLBACK`: Discards changes

---

35. **What is a lock in MySQL?**  
    Mechanism to manage concurrent access to data.

---

36. **Types of locks in MySQL?**
- Shared lock (read)
- Exclusive lock (write)
- Table-level and row-level locks

---

37. **What are isolation levels in MySQL?**
- READ UNCOMMITTED
- READ COMMITTED
- REPEATABLE READ (default in InnoDB)
- SERIALIZABLE

---

38. **What are dirty, non-repeatable, and phantom reads?**
- **Dirty Read**: Read uncommitted data
- **Non-repeatable**: Data changes between reads
- **Phantom Read**: New rows added between reads

---

### 🔹 **Stored Procedures, Triggers & Views**

39. **What is a stored procedure?**  
    A saved SQL block that can be reused.

---

40. **What is the difference between a stored procedure and a function?**
- Function returns a value
- Procedure may or may not return a value

---

41. **What is a trigger?**  
    A block of SQL executed automatically on certain events like `INSERT`, `UPDATE`, or `DELETE`.

---

42. **What are views in MySQL?**  
    A virtual table based on the result of a query.

---

43. **Can you insert/update through views?**  
    Yes, if the view is updatable and meets certain conditions.

---

44. **How do you call a stored procedure?**
   ```sql
   CALL procedure_name();
   ```

---

### 🔹 **Advanced & Real-World Usage**

45. **What is normalization?**  
    Process of organizing data to reduce redundancy.

---

46. **What are the normal forms?**
- 1NF: Atomic values
- 2NF: Full functional dependency
- 3NF: No transitive dependency
- BCNF: Stronger version of 3NF

---

47. **What is denormalization?**  
    Combining tables to improve read performance.

---

48. **What is a foreign key?**  
    A field that links to a primary key in another table, maintaining referential integrity.

---

49. **How do you back up and restore a MySQL database?**
- Backup: `mysqldump -u root -p dbname > backup.sql`
- Restore: `mysql -u root -p dbname < backup.sql`

---

50. **How do you import/export data from CSV in MySQL?**
   ```sql
   LOAD DATA INFILE '/path/file.csv'  
   INTO TABLE table_name  
   FIELDS TERMINATED BY ','  
   ENCLOSED BY '"'  
   LINES TERMINATED BY '\n';
   ```

---

Would you like these in **PDF format**, or want to go deeper into **MySQL performance tuning**, **real-world SQL case studies**, or **MySQL + Java integration questions** next?