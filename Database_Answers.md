# Database & SQL Interview Questions & Answers

## 1. SQL Query: Find the second highest salary.
**Detailed Explanation**: A common interview question. The goal is to skip the highest and take the next one.
*   **Approach 1 (Subquery)**: Find max salary, then find max salary LESS than that.
*   **Approach 2 (Limit/Offset)**: Sort descending and take the 2nd unique value.
*   **Approach 3 (Dense Rank)**: Use window function to rank salaries. Safest for duplicates.

**Example**:
```sql
-- Method 1: Subquery
SELECT MAX(salary) FROM Employee 
WHERE salary < (SELECT MAX(salary) FROM Employee);

-- Method 2: Limit/Offset (MySQL/PostgreSQL)
SELECT DISTINCT salary FROM Employee 
ORDER BY salary DESC 
LIMIT 1 OFFSET 1;

-- Method 3: Window Function (Best)
SELECT salary FROM (
    SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) as rank
    FROM Employee
) as ranked_table
WHERE rank = 2;
```

---

## 2. SQL Query: Find employees with salary greater than average.
**Detailed Explanation**: Requires calculating the average salary of the entire table first, then filtering rows against that value.
*   **Concept**: Subquery in WHERE clause.

**Example**:
```sql
SELECT name, salary 
FROM Employee 
WHERE salary > (SELECT AVG(salary) FROM Employee);
```

---

## 3. SQL Query: Find duplicate records.
**Detailed Explanation**: To find duplicates, you group by the columns that define uniqueness (e.g., name, email) and check if the count is greater than 1.

**Example**:
```sql
SELECT name, email, COUNT(*)
FROM Employee
GROUP BY name, email
HAVING COUNT(*) > 1;
```

---

## 4. SQL Query: Find max salary per department.
**Detailed Explanation**: Group employees by their `department_id` and apply the `MAX()` aggregate function to the `salary` column.

**Example**:
```sql
SELECT department_id, MAX(salary) 
FROM Employee 
GROUP BY department_id;
```

---

## 5. SQL Query: Find nth highest salary.
**Detailed Explanation**: A generalized version of "Second Highest".
*   **Approach**: Use `DENSE_RANK()`. It handles duplicates gracefully (if two people have rank 2, the next one is 3).

**Example**:
```sql
SELECT salary FROM (
    SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) as rnk
    FROM Employee
) as temp
WHERE rnk = N; -- Replace N with 5, 10, etc.
```

---

## 6. Types of Joins
**Detailed Explanation**:
1.  **INNER JOIN**: Returns records that have matching values in **both** tables.
2.  **LEFT (OUTER) JOIN**: Returns all records from the Left table, and the matched records from the Right table (NULL if no match).
3.  **RIGHT (OUTER) JOIN**: Returns all records from the Right table, and matched from Left.
4.  **FULL (OUTER) JOIN**: Returns all records when there is a match in **either** Left or Right table.
5.  **CROSS JOIN**: Cartesian product. Returns (Rows in A) * (Rows in B).

**Example**:
```sql
-- Employees with their Department Names (Inner Join)
SELECT e.name, d.dept_name
FROM Employee e
INNER JOIN Department d ON e.dept_id = d.id;
```

---

## 7. Difference between DELETE, TRUNCATE, and DROP
**Detailed Explanation**:
*   **DELETE (DML)**: Removes specific rows (using WHERE). Can be rolled back. Slower (logs per row). triggers fire.
*   **TRUNCATE (DDL)**: Removes **ALL** rows. Cannot be rolled back (in some DBs). Faster (deallocates pages). Resets Identity.
*   **DROP (DDL)**: Removes the **entire table** structure and data.

---

## 8. What is a View? Can we insert data into a view?
**Detailed Explanation**:
*   **View**: A virtual table based on the result-set of an SQL statement. It contains no data itself (unless Materialized View). Used to simplify complex queries or restrict access.
*   **Insert?**:
    *   **Yes**, if it's a "Simple View" (maps directly to one table, no grouping/distinct). The DB inserts into the underlying table.
    *   **No**, if it's a "Complex View" (joins, aggregates, distinct).

**Example**:
```sql
CREATE VIEW IT_Employees AS
SELECT * FROM Employee WHERE dept_id = 'IT';
```

---

## 9. What is an Index? How does it improve performance?
**Detailed Explanation**: A data structure (B-Tree) that improves the speed of data retrieval operations.
*   **How**: Instead of scanning the whole table (Full Table Scan), DB traverses the B-Tree to find the pointer to data. O(log N).
*   **Clustered Index**: Sorts and stores the *actual data rows* in the table based on key. Only 1 per table (usually Primary Key).
*   **Non-Clustered Index**: Stores a separate structure with the Key and a *pointer* to the data row. Can have many.

---

## 10. Stored Procedures vs Functions
**Detailed Explanation**:
*   **Stored Procedure**:
    *   Can perform complex business logic, transactions, DML (Insert/Update).
    *   May or may not return values.
    *   Call using `CALL procedure_name()`.
*   **Function (UDF)**:
    *   Designed to return a single value (or table).
    *   Used inside SQL statements (`SELECT my_func(col) FROM...`).
    *   Usually cannot perform DML (Insert/Update) inside.

---

## 11. What are ACID properties?
**Detailed Explanation**: Properties that guarantee reliable processing of database transactions.
1.  **Atomicity**: All or Nothing. (If one step fails, rollback everything).
2.  **Consistency**: Database moves from one valid state to another. Constraints are respected.
3.  **Isolation**: Modifications by one transaction are hidden from others until commit.
4.  **Durability**: Once committed, data is saved permanently (even if power fails).

---

## 12. Difference between Primary Key and Unique Key
**Detailed Explanation**:
*   **Primary Key**:
    *   Uniquely identifies a record.
    *   **NO NULLs** allowed.
    *   Only **1** per table.
    *   Creates Clustered Index by default.
*   **Unique Key**:
    *   Ensures unique values in a column.
    *   **Allows ONE Null** (in SQL Server) or Multiple Nulls (Oracle, Postgres).
    *   Multiple allowed per table.

---

## 13. Difference between WHERE and HAVING clause
**Detailed Explanation**:
*   **WHERE**: Filters rows **before** grouping. Applies to individual records. Cannot use aggregates (`SUM`, `COUNT`).
*   **HAVING**: Filters groups **after** grouping. Applies to the result of an aggregate.
*   **Order**: `FROM` -> `WHERE` -> `GROUP BY` -> `HAVING` -> `SELECT`.

**Example**:
```sql
SELECT dept_id, SUM(salary)
FROM Employee
WHERE salary > 1000  -- Filter individual rows first
GROUP BY dept_id
HAVING SUM(salary) > 50000; -- Filter the sums
```

---

## 14. Database Normalization
**Detailed Explanation**: The process of organizing data to reduce redundancy and improve integrity.
*   **1NF**: Atomic values (No lists/arrays in a cell). Each row unique.
*   **2NF**: 1NF + No Partial Dependency (Non-key attributes depend on Whole Primary Key).
*   **3NF**: 2NF + No Transitive Dependency (Non-key columns shouldn't depend on other non-key columns).

---

## 15. SQL vs NoSQL
**Detailed Explanation**:
*   **SQL (Relational)**:
    *   Structured (Tables, Rows). Schema-strict.
    *   Good for complex joins, transactions (ACID).
    *   Scale Up (Vertical).
    *   Ex: MySQL, PostgreSQL, Oracle.
*   **NoSQL (Non-Relational)**:
    *   Unstructured (Documents, Key-Value, Graphs). Schema-less.
    *   Good for Big Data, Rapid changes, High Throughput.
    *   Scale Out (Horizontal).
    *   Ex: MongoDB, Redis, Cassandra.

---

## 16. MongoDB features
**Detailed Explanation**: A Document-Oriented NoSQL Database.
1.  **JSON Data**: Stores data in BSON (Binary JSON) documents. Flexible schema.
2.  **Scalability**: Built-in Sharding (Horizontal scaling).
3.  **Replication**: Replica Sets for high availability.
4.  **Ad-hoc Queries**: Supports indexing, range queries, aggregations.

**Example**:
```json
// SQL: Table User with columns
// Mongo: Document
{
  "_id": 1,
  "name": "Alice",
  "skills": ["Java", "SQL"] // Can store arrays directly
}
```

---

## 17. Transaction Management (Commit, Rollback)
**Detailed Explanation**: To protect data integrity, multiple operations are grouped.
*   **Commit**: Save changes permanently.
*   **Rollback**: Undo changes up to the start of transaction or a Savepoint.
*   **Savepoint**: A marker within a transaction to rollback partially.

**Example**:
```sql
BEGIN TRANSACTION;
UPDATE Account SET balance = balance - 100 WHERE id = 1;
UPDATE Account SET balance = balance + 100 WHERE id = 2;
-- If error occurs here:
ROLLBACK; 
-- Else:
COMMIT;
```

---

## 18. Optimistic vs Pessimistic Locking
**Detailed Explanation**: Strategies to handle concurrent updates.
*   **Pessimistic Locking**:
    *   "I suspect a conflict."
    *   **Lock the record** when reading it. No one else can read/write until I finish.
    *   High integrity, lower concurrency. Deadlock prone.
    *   SQL: `SELECT * FROM Table FOR UPDATE`.
*   **Optimistic Locking**:
    *   "I hope there's no conflict."
    *   **No locks**. Just versioning.
    *   Read record (version v1). Update. When saving, check if version is still v1. If yes, save (v2). If no (someone else made it v2), fail.
    *   High concurrency.

**Example**:
```sql
-- Optimistic approach (JPA uses @Version)
UPDATE Product 
SET price = 20, version = 2 
WHERE id = 1 AND version = 1; 
-- If 0 rows updated, it means data was stale.
```
