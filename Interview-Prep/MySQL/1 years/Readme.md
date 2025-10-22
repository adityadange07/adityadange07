Here are the **Top 50 MySQL Interview Questions and Answers**, specifically tailored for someone with **1 year of experience**. These questions cover **SQL basics**, **database concepts**, **MySQL-specific features**, and **practical queries** that you are likely to encounter in beginner to intermediate interviews.

---

## ✅ Top 50 MySQL Interview Questions (1 Year Experience)

---

### 🔹 **Basics of SQL & MySQL**

1. **What is MySQL?**  
   MySQL is an open-source relational database management system (RDBMS) that uses SQL (Structured Query Language).

---

2. **What are the different types of SQL statements?**
    - DDL: `CREATE`, `ALTER`, `DROP`
    - DML: `SELECT`, `INSERT`, `UPDATE`, `DELETE`
    - DCL: `GRANT`, `REVOKE`
    - TCL: `COMMIT`, `ROLLBACK`, `SAVEPOINT`

---

3. **What is the difference between SQL and MySQL?**
    - SQL is a language for querying databases.
    - MySQL is a database software that uses SQL.

---

4. **What is a primary key?**  
   A unique identifier for a row in a table. Cannot be `NULL`.

---

5. **What is a foreign key?**  
   A field that links two tables, referencing the primary key of another table.

---

6. **What is the difference between `WHERE` and `HAVING`?**
    - `WHERE`: Filters rows before grouping
    - `HAVING`: Filters after grouping (`GROUP BY`)

---

7. **What are indexes in MySQL?**  
   Indexes improve query performance by allowing faster searches.

---

8. **What is the difference between `INNER JOIN`, `LEFT JOIN`, and `RIGHT JOIN`?**
    - `INNER JOIN`: Only matching records
    - `LEFT JOIN`: All from left, matching from right
    - `RIGHT JOIN`: All from right, matching from left

---

9. **What is normalization?**  
   Organizing data to reduce redundancy and improve integrity.

---

10. **What are the different normal forms?**
- 1NF: Atomic columns
- 2NF: No partial dependencies
- 3NF: No transitive dependencies

---

### 🔹 **Data Types & Table Management**

11. **What are common data types in MySQL?**
- Numeric: `INT`, `DECIMAL`, `FLOAT`
- String: `VARCHAR`, `TEXT`, `CHAR`
- Date/Time: `DATE`, `DATETIME`, `TIMESTAMP`

---

12. **How to create a table in MySQL?**
   ```sql
   CREATE TABLE users (
     id INT PRIMARY KEY,
     name VARCHAR(50),
     email VARCHAR(100)
   );
   ```

---

13. **How do you add a column to an existing table?**
   ```sql
   ALTER TABLE users ADD age INT;
   ```

---

14. **How to delete a table in MySQL?**
   ```sql
   DROP TABLE table_name;
   ```

---

15. **What is the difference between `CHAR` and `VARCHAR`?**
- `CHAR`: Fixed length
- `VARCHAR`: Variable length

---

16. **How do you rename a table?**
   ```sql
   RENAME TABLE old_name TO new_name;
   ```

---

17. **What is the difference between `DELETE`, `TRUNCATE`, and `DROP`?**
- `DELETE`: Deletes specific rows
- `TRUNCATE`: Deletes all rows, keeps structure
- `DROP`: Removes table entirely

---

18. **How do you update data in a table?**
   ```sql
   UPDATE users SET name = 'John' WHERE id = 1;
   ```

---

19. **How do you insert data into a table?**
   ```sql
   INSERT INTO users (id, name) VALUES (1, 'Alice');
   ```

---

20. **How do you retrieve data from a table?**
   ```sql
   SELECT * FROM users;
   ```

---

### 🔹 **Constraints & Keys**

21. **What are constraints in MySQL?**  
    Rules enforced on data: `PRIMARY KEY`, `FOREIGN KEY`, `UNIQUE`, `NOT NULL`, `CHECK`

---

22. **What is a unique constraint?**  
    Ensures all values in a column are different.

---

23. **What is auto-increment in MySQL?**  
    Automatically increases the value of a column (usually primary key).

---

24. **How to set default values in a column?**
   ```sql
   age INT DEFAULT 18;
   ```

---

25. **What is a composite key?**  
    A primary key made from two or more columns.

---

### 🔹 **Querying & Filtering**

26. **How to sort query results?**
   ```sql
   SELECT * FROM users ORDER BY name ASC;
   ```

---

27. **How to filter with `LIKE`?**
   ```sql
   SELECT * FROM users WHERE name LIKE 'A%';
   ```

---

28. **How to limit the number of rows returned?**
   ```sql
   SELECT * FROM users LIMIT 5;
   ```

---

29. **What is a subquery?**  
    A query inside another query.

---

30. **How to find duplicate values?**
   ```sql
   SELECT email, COUNT(*) FROM users GROUP BY email HAVING COUNT(*) > 1;
   ```

---

31. **What does `GROUP BY` do?**  
    Groups rows with the same values into summary rows.

---

32. **What is the `DISTINCT` keyword used for?**  
    Removes duplicate rows from results.

---

33. **How do you get the current date in MySQL?**
   ```sql
   SELECT NOW();
   ```

---

34. **How do you use aggregate functions?**
- `SUM()`, `AVG()`, `COUNT()`, `MAX()`, `MIN()`

---

35. **What is a NULL value?**  
    Represents a missing or unknown value.

---

### 🔹 **Functions & Procedures**

36. **What are MySQL functions?**  
    Built-in utilities to perform calculations or formatting, like `LENGTH()`, `UPPER()`, `DATE_FORMAT()`

---

37. **How to concatenate strings in MySQL?**
   ```sql
   SELECT CONCAT(first_name, ' ', last_name) FROM users;
   ```

---

38. **What is a stored procedure?**  
    A saved SQL code block that can be executed repeatedly.

---

39. **How to call a stored procedure?**
   ```sql
   CALL procedure_name();
   ```

---

40. **What is the difference between function and procedure?**
- **Function** returns a value
- **Procedure** may return zero or more values but is mainly for operations

---

### 🔹 **Joins & Relationships**

41. **What is a JOIN in SQL?**  
    Combines rows from two or more tables based on a related column.

---

42. **What are types of joins in MySQL?**
- `INNER JOIN`
- `LEFT JOIN`
- `RIGHT JOIN`
- `FULL OUTER JOIN` (not supported natively, but can be simulated)

---

43. **How to join three tables?**  
    Chain multiple joins:
   ```sql
   SELECT * FROM A  
   JOIN B ON A.id = B.a_id  
   JOIN C ON B.id = C.b_id;
   ```

---

44. **What is self-join?**  
    Joining a table with itself.

---

45. **How to use aliases in SQL?**
   ```sql
   SELECT u.name AS username FROM users u;
   ```

---

### 🔹 **Transactions & Locks**

46. **What is a transaction in MySQL?**  
    A set of SQL operations executed as a single unit with `COMMIT` or `ROLLBACK`.

---

47. **What are ACID properties?**
- **Atomicity**
- **Consistency**
- **Isolation**
- **Durability**

---

48. **How to start and commit a transaction?**
   ```sql
   START TRANSACTION;  
   -- queries  
   COMMIT;
   ```

---

49. **What is a deadlock?**  
    A situation where two or more transactions wait for each other to release locks.

---

50. **How to improve query performance in MySQL?**
- Use indexes
- Optimize joins
- Avoid `SELECT *`
- Use `EXPLAIN` to analyze queries

---

Would you like these in **PDF format**, or want **real-time query scenarios**, or **MySQL + Java integration questions** next?