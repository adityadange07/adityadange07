Here are the **Top 50 MySQL Interview Questions and Answers** tailored for candidates with **2 years of experience**. These cover basics, querying, optimization, indexing, joins, transactions, and some admin-level understanding.

---

## ✅ Top 50 MySQL Interview Questions (2 Years Experience)

---

### 🔹 **Basic & Fundamentals**

1. **What is MySQL?**  
   A popular open-source relational database management system (RDBMS) based on SQL.

---

2. **What are the different data types in MySQL?**
    - Numeric: INT, BIGINT, FLOAT, DOUBLE
    - String: VARCHAR, TEXT, CHAR
    - Date/Time: DATE, TIME, DATETIME
    - Others: BLOB, ENUM, SET

---

3. **What is the difference between `CHAR` and `VARCHAR`?**
    - `CHAR`: Fixed length
    - `VARCHAR`: Variable length, more space efficient

---

4. **What are primary keys?**  
   Unique identifier for each record in a table. Cannot be NULL or duplicate.

---

5. **What are foreign keys?**  
   Keys used to link two tables together, enforcing referential integrity.

---

6. **What is a unique key?**  
   Ensures all values in a column are distinct but allows a single NULL.

---

7. **Difference between `DELETE`, `TRUNCATE`, and `DROP`?**
    - `DELETE`: Removes rows, can be rolled back
    - `TRUNCATE`: Deletes all rows, can't rollback
    - `DROP`: Deletes the table structure

---

8. **What is the default port for MySQL?**  
   `3306`

---

9. **What are the different storage engines in MySQL?**
    - InnoDB (default): Supports transactions, FK
    - MyISAM: Faster read, no transactions
    - MEMORY, CSV, ARCHIVE, etc.

---

10. **What is the difference between InnoDB and MyISAM?**
- InnoDB: Supports transactions, row-level locking
- MyISAM: Table-level locking, faster for read-heavy ops

---

### 🔹 **SQL Queries & Clauses**

11. **How do you fetch the top 5 rows from a table?**
   ```sql
   SELECT * FROM table_name LIMIT 5;
   ```

---

12. **What is the `WHERE` clause used for?**  
    To filter records that meet a specified condition.

---

13. **What is the `GROUP BY` clause?**  
    Groups rows that have the same values into summary rows.

---

14. **What is the `HAVING` clause?**  
    Filters groups (used with `GROUP BY`), unlike `WHERE` which filters rows.

---

15. **What is a subquery?**  
    A query nested inside another query.

---

16. **What is the difference between `BETWEEN` and `IN`?**
- `BETWEEN`: Range filter
- `IN`: Checks for multiple discrete values

---

17. **How do you write a case-insensitive query?**  
    Use `LOWER()` or `UPPER()`, or ensure collation is case-insensitive.

---

18. **What does `IS NULL` and `IS NOT NULL` do?**  
    Checks whether a column has or doesn't have a NULL value.

---

19. **What is a `LIKE` operator?**  
    Pattern matching in string comparisons using `%` and `_`.

---

20. **How do you find duplicate rows in a table?**
   ```sql
   SELECT column, COUNT(*)  
   FROM table  
   GROUP BY column  
   HAVING COUNT(*) > 1;
   ```

---

### 🔹 **Joins & Relationships**

21. **What is a JOIN?**  
    Combines rows from two or more tables based on a related column.

---

22. **Different types of JOINs?**
- `INNER JOIN`: Matching rows
- `LEFT JOIN`: All from left + matches
- `RIGHT JOIN`: All from right + matches
- `FULL OUTER JOIN`: Not directly supported in MySQL (use UNION)
- `SELF JOIN`: Joins a table to itself

---

23. **Example of INNER JOIN:**
   ```sql
   SELECT a.name, b.salary  
   FROM employees a  
   INNER JOIN salaries b ON a.id = b.emp_id;
   ```

---

24. **Difference between JOIN and UNION?**
- `JOIN`: Combines columns from multiple tables
- `UNION`: Combines result sets (rows) from multiple SELECTs

---

25. **What is a cross join?**  
    Cartesian product: returns all possible combinations of two tables.

---

### 🔹 **Indexes & Performance**

26. **What is an index in MySQL?**  
    A data structure that improves query performance on a column.

---

27. **Types of indexes?**
- Primary
- Unique
- Full-text
- Composite (multi-column)

---

28. **How do indexes improve performance?**  
    Speeds up searches by reducing row scans using B-Trees.

---

29. **What are the disadvantages of indexing?**
- Slower `INSERT`, `UPDATE`, `DELETE`
- Takes additional storage

---

30. **How to view indexes on a table?**
   ```sql
   SHOW INDEXES FROM table_name;
   ```

---

### 🔹 **Transactions & Constraints**

31. **What is a transaction?**  
    A sequence of SQL statements treated as a single unit of work.

---

32. **ACID properties of transactions?**
- Atomicity
- Consistency
- Isolation
- Durability

---

33. **How do you start a transaction in MySQL?**
   ```sql
   START TRANSACTION;  
   -- statements  
   COMMIT;  
   ROLLBACK;
   ```

---

34. **What is the `AUTOCOMMIT` feature?**  
    When ON, each SQL statement is treated as a separate transaction.

---

35. **What are constraints in MySQL?**  
    Rules enforced on columns:
- `NOT NULL`, `UNIQUE`, `CHECK`, `DEFAULT`, `PRIMARY KEY`, `FOREIGN KEY`

---

### 🔹 **Functions & Operators**

36. **Common string functions in MySQL?**  
    `CONCAT()`, `SUBSTRING()`, `LENGTH()`, `LOWER()`, `UPPER()`

---

37. **Common numeric functions?**  
    `ROUND()`, `FLOOR()`, `CEIL()`, `MOD()`, `ABS()`

---

38. **Date functions in MySQL?**  
    `NOW()`, `CURDATE()`, `DATEDIFF()`, `DATE_ADD()`, `YEAR()`

---

39. **What is `COALESCE()` in MySQL?**  
    Returns the first non-null value from a list.

---

40. **What is `IFNULL()`?**  
    Replaces NULL with a default value:  
    `IFNULL(col, 'default')`

---

### 🔹 **Administration & Tools**

41. **How to check MySQL version?**
   ```sql
   SELECT VERSION();  
   ```

---

42. **How to create a new user in MySQL?**
   ```sql
   CREATE USER 'user'@'localhost' IDENTIFIED BY 'password';
   ```

---

43. **How to grant privileges to a user?**
   ```sql
   GRANT ALL PRIVILEGES ON db.* TO 'user'@'localhost';  
   FLUSH PRIVILEGES;
   ```

---

44. **How to backup a MySQL database?**  
    Use `mysqldump`:
   ```bash
   mysqldump -u root -p database_name > backup.sql
   ```

---

45. **How to restore a MySQL backup?**
   ```bash
   mysql -u root -p database_name < backup.sql
   ```

---

46. **What is the `INFORMATION_SCHEMA`?**  
    A metadata database that stores info about tables, columns, indexes, etc.

---

47. **How to change a column's datatype?**
   ```sql
   ALTER TABLE table_name MODIFY column_name NEW_DATATYPE;
   ```

---

48. **How to rename a table?**
   ```sql
   RENAME TABLE old_name TO new_name;
   ```

---

49. **How do you prevent SQL injection?**
- Use prepared statements
- ORM frameworks
- Validate and sanitize inputs

---

50. **How do you optimize slow queries?**
- Use `EXPLAIN`
- Add indexes
- Avoid `SELECT *`
- Use joins instead of subqueries

---

Would you like these questions in **PDF format**, or want to dive deeper into **MySQL performance tuning**, **indexing strategies**, or **interview coding exercises involving SQL joins and queries**?