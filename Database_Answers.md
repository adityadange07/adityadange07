# Database Interview Questions & Answers (Deep Dive & Multiple Approaches)

## 1. SQL Query: Find the second highest salary

**Approach 1: Subquery (ANSI standard)**
Works in almost all databases but performance can be slower on large datasets.
```sql
SELECT MAX(salary) 
FROM Employee 
WHERE salary < (SELECT MAX(salary) FROM Employee);
```

**Approach 2: LIMIT / OFFSET (MySQL, PostgreSQL)**
Simple and fast for finding a specific rank.
```sql
SELECT salary 
FROM Employee 
ORDER BY salary DESC 
LIMIT 1 OFFSET 1;
```

**Approach 3: Window Function (DENSE_RANK) - Best Practice**
Handles duplicates correctly (e.g., if two people have the highest salary, the next distinct salary is ranked 2).
```sql
SELECT DISTINCT salary 
FROM (
    SELECT salary, DENSE_RANK() OVER (ORDER BY salary DESC) as rnk 
    FROM Employee
) as ranked_table
WHERE rnk = 2;
```

## 2. SQL Query: Find duplicate records

**Approach 1: GROUP BY (Standard)**
Identify duplicates by grouping and counting.
```sql
SELECT name, COUNT(*) 
FROM Employee 
GROUP BY name 
HAVING COUNT(*) > 1;
```

**Approach 2: Window Function (ROW_NUMBER)**
More flexible, allows identifying the specific row IDs of duplicates.
```sql
SELECT * FROM (
    SELECT id, name, ROW_NUMBER() OVER (PARTITION BY name ORDER BY id) as row_num 
    FROM Employee
) as temp
WHERE row_num > 1;
```

## 3. SQL Query: Delete duplicate records

**Approach 1: Using Self-Join (MySQL)**
Keeps the row with the lowest ID.
```sql
DELETE e1 
FROM Employee e1 
JOIN Employee e2 
WHERE e1.name = e2.name AND e1.id > e2.id;
```

**Approach 2: Using CTE & Window Function (SQL Server, MaxDB, Postgres)**
Cleanest way for modern databases.
```sql
WITH CTE AS (
    SELECT name, ROW_NUMBER() OVER (PARTITION BY name ORDER BY id) as row_num 
    FROM Employee
)
DELETE FROM CTE WHERE row_num > 1;
```

## 4. SQL Query: Find max salary per department

**Approach 1: Group By (Standard)**
```sql
SELECT dept_id, MAX(salary) 
FROM Employee 
GROUP BY dept_id;
```

**Approach 2: Join with Employee Table (To get Name)**
If you need the *name* of the employee with the max salary (which Approach 1 doesn't give).
```sql
SELECT e.name, e.salary, e.dept_id
FROM Employee e
INNER JOIN (
    SELECT dept_id, MAX(salary) as max_sal
    FROM Employee
    GROUP BY dept_id
) grouped_e ON e.dept_id = grouped_e.dept_id AND e.salary = grouped_e.max_sal;
```

**Approach 3: Window Function (No Join needed)**
Much more efficient than self-join for fetching related columns.
```sql
SELECT name, salary, dept_id
FROM (
    SELECT name, salary, dept_id, RANK() OVER (PARTITION BY dept_id ORDER BY salary DESC) as rnk
    FROM Employee
) as ranked
WHERE rnk = 1;
```

## 5. SQL vs NoSQL Internals
**SQL (B-Tree):**
- Data stored in Pages (8KB or 16KB).
- **Indexing (B-Tree):** Balanced Tree. Root -> Intermediate -> Leaf Nodes. Leaf nodes point to physical data pages.
- **Search Cost:** O(log N). Excellent for Range queries (`> 500`).

**NoSQL (LSM Tree - Log Structured Merge):**
- Used by Cassandra, HBase.
- Writes go to **MemTable** (RAM). Fast writes.
- Flushed to **SSTable** (Disk) as immutable files.
- Reads check MemTable, then Bloom Filter, then SSTables.
- **Compaction:** Merges SSTables in background to remove stale data.

## 6. ACID Properties Deep Dive
1.  **Atomicity (Undo Log):**
    - Database writes "Before Image" to Undo Log before modifying data.
    - If crash/rollback, it reads Undo Log to restore old state.
2.  **Consistency:** Rules (Constraints, Foreign Keys) are enforced.
3.  **Isolation (Locking/MVCC):**
    - **Read Uncommitted:** Dirty Reads possible.
    - **Read Committed:** No Dirty reads. Uses Locks or Snapshots.
    - **Repeatable Read:** No Non-Repeatable reads. (MySQL Default).
    - **Serializable:** Strict Locking (Rows + Gaps). Slowest.
4.  **Durability (Redo Log / WAL):**
    - Write-Ahead Logging. Changes written to disk log *before* data pages are modified.
    - If crash, DB replays Redo Log to recover committed transactions.

## 7. Database Normalization (Advanced)
- **1NF:** Atomicity.
- **2NF:** Remove Partial Dependency (Key is atomic).
- **3NF:** Remove Transitive Dependency (A->B, B->C).
- **BCNF (Boyce-Codd):** Stricter 3NF. For every dependency X->Y, X must be a Super Key.

## 8. Stored Procedures vs Functions
**Approach 1: Stored Procedure**
Used for business logic that modifies state.
```sql
CREATE PROCEDURE UpdateSalary(IN emp_id INT, IN amount DECIMAL)
BEGIN
    UPDATE Employee SET salary = salary + amount WHERE id = emp_id;
END;
-- Call with: CALL UpdateSalary(1, 500);
```

**Approach 2: User Defined Function (UDF)**
Used for calculations inside a SELECT query.
```sql
CREATE FUNCTION CalculateTax(salary DECIMAL) RETURNS DECIMAL
BEGIN
    RETURN salary * 0.1;
END;
-- Call with: SELECT name, CalculateTax(salary) FROM Employee;
```

## 9. Transaction Isolation Levels & Anomalies
- **Dirty Read:** T1 reads uncommitted change of T2.
- **Non-Repeatable Read:** T1 reads X. T2 updates X. T1 reads X again (value changed).
- **Phantom Read:** T1 reads range (count=5). T2 Inserts new row. T1 reads range (count=6).
- *Solution:* Serializable level or MVCC (Multi-Version Concurrency Control).

## 10. Optimistic vs Pessimistic Locking
**Pessimistic:**
```sql
SELECT * FROM table WHERE id=1 FOR UPDATE;
```
Database holds lock. Other transactions block.

**Optimistic:**
Application Logic.
```java
// UPDATE table SET val=new, version=2 WHERE id=1 AND version=1
int rows = repo.update(id, newVal, oldVer);
if (rows == 0) throw new OptimisticLockException("Data changed by someone else");
```
