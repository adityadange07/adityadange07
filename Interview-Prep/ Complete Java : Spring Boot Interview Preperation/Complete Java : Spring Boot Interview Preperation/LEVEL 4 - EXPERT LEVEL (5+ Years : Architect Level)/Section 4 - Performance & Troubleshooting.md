# EXPERT LEVEL (5+ Years / Architect Level)

# Performance & Troubleshotting

## 283. How do you profile Java applications? 

Absolutely! Let’s go step by step on **profiling Java applications**, including tools, techniques, and best practices.

---

## 1️⃣ What is Java Profiling?

**Java profiling** is the process of **analyzing a Java application's performance** to identify:

* CPU bottlenecks
* Memory leaks and garbage collection issues
* Thread contention and deadlocks
* Slow database queries or I/O

Profiling helps improve **performance, scalability, and resource usage**.

---

## 2️⃣ Key Areas to Profile

| Area                   | Purpose                                           |
| ---------------------- | ------------------------------------------------- |
| **CPU Usage**          | Identify methods consuming excessive CPU          |
| **Memory Usage**       | Detect memory leaks, high heap usage              |
| **Garbage Collection** | Analyze GC pauses and efficiency                  |
| **Thread Activity**    | Detect deadlocks, thread contention               |
| **I/O / DB Calls**     | Identify slow database queries or file operations |

---

## 3️⃣ Profiling Tools

### **1. VisualVM**

* Ships with JDK (or can be downloaded separately)
* Features:

  * CPU & memory profiling
  * Thread monitoring
  * Heap dumps & GC analysis
* Usage: Connect to a running JVM, start profiling, and analyze hot methods.

### **2. JConsole**

* Ships with JDK
* Features:

  * Real-time memory usage
  * Thread activity
  * Basic CPU monitoring
* Useful for **quick checks** of live applications.

### **3. Java Flight Recorder (JFR) + Mission Control (JMC)**

* Built into JDK 11+
* Features:

  * Low-overhead profiling in production
  * Event-based monitoring for CPU, memory, threads, I/O
* Usage:

```bash
java -XX:StartFlightRecording=duration=60s,filename=myapp.jfr -jar myapp.jar
```

### **4. YourKit / JProfiler**

* Commercial profilers with rich GUI
* Features:

  * CPU & memory snapshots
  * Thread analysis
  * Database query monitoring
* Useful for deep **production-like profiling**.

### **5. JVM Flags for GC & Heap Analysis**

* Enable GC logs:

```bash
-XX:+PrintGCDetails -XX:+PrintGCDateStamps -Xloggc:gc.log
```

* Analyze memory behavior and GC pauses.

---

## 4️⃣ Profiling Techniques

### **CPU Profiling**

* Identify methods consuming the most CPU.
* Example tools: VisualVM, JFR, YourKit
* Steps:

  1. Attach profiler to JVM.
  2. Record CPU sampling for a period under load.
  3. Analyze top hot methods.

### **Memory Profiling**

* Detect memory leaks, large object allocations.
* Tools: VisualVM, JFR, YourKit
* Steps:

  1. Take **heap snapshot**.
  2. Analyze objects retained in memory.
  3. Identify memory leaks and optimize.

### **Thread Profiling**

* Detect deadlocks or thread contention.
* Tools: VisualVM, JConsole, JFR
* Steps:

  1. Observe thread states (`RUNNABLE`, `BLOCKED`, `WAITING`).
  2. Identify stuck threads or high contention.
  3. Fix synchronization issues.

### **I/O & Database Profiling**

* Detect slow DB calls or file I/O.
* Tools: JFR, YourKit, Spring Boot Actuator metrics
* Steps:

  1. Enable metrics or profiling.
  2. Identify slow queries or I/O methods.
  3. Optimize queries or caching.

---

## 5️⃣ Best Practices

1. **Profile in staging or production with low overhead** → JFR is ideal.
2. **Use sampling instead of instrumentation** for minimal performance impact.
3. **Focus on hot methods and large objects** → highest ROI.
4. **Combine GC logs, memory snapshots, and CPU profiling** for full picture.
5. **Monitor continuously** → prevent regressions in production.

---

## 6️⃣ Summary

| Aspect   | Tool / Approach               | Notes                                |
| -------- | ----------------------------- | ------------------------------------ |
| CPU      | VisualVM, JFR, YourKit        | Identify hotspots                    |
| Memory   | Heap dump, VisualVM, JFR      | Detect leaks, optimize allocations   |
| Thread   | VisualVM, JConsole, JFR       | Detect deadlocks, contention         |
| GC       | GC logs, JFR                  | Analyze pauses, optimize GC strategy |
| I/O / DB | JFR, YourKit, Spring Actuator | Identify slow queries and I/O        |

> Profiling helps **improve performance, resource efficiency, and reliability** of Java applications.

---

I can also create a **diagram showing Java app profiling: JVM, heap, threads, CPU, GC, and tools like VisualVM/JFR** for visual understanding, which is very useful for interviews.

Do you want me to create that diagram?

---

## 284. How to debug memory leaks?

Absolutely! Let’s go step by step on **debugging memory leaks in Java**, including techniques, tools, and best practices.

---

## 1️⃣ What is a Memory Leak in Java?

A **memory leak** occurs when objects are **no longer needed but are still referenced**, preventing the garbage collector (GC) from freeing memory.

**Symptoms:**

* OutOfMemoryError (OOM)
* Increasing heap usage over time
* Frequent GC cycles with little memory reclaimed
* Application slowdown

---

## 2️⃣ Common Causes

| Cause                        | Description                                                 |
| ---------------------------- | ----------------------------------------------------------- |
| **Static references**        | Objects stored in static collections that never get cleared |
| **Unclosed resources**       | InputStreams, OutputStreams, JDBC connections, sockets      |
| **Listeners / Observers**    | Objects registered but not deregistered                     |
| **Caching without eviction** | Large caches that grow indefinitely                         |
| **ThreadLocal misuse**       | Values not removed after thread execution                   |
| **Third-party libraries**    | Bugs in library retaining objects                           |

---

## 3️⃣ Steps to Debug Memory Leaks

### **Step 1: Monitor Heap Usage**

* Tools: **VisualVM, JConsole, JFR, Prometheus metrics**
* Look for increasing heap usage over time.
* Observe GC frequency and memory pressure.

### **Step 2: Enable GC Logging**

```bash
-XX:+PrintGCDetails -XX:+PrintGCDateStamps -Xloggc:gc.log
```

* Analyze GC logs for memory pressure and survivor space issues.

### **Step 3: Take Heap Dumps**

* Heap dumps capture **all objects in memory at a point in time**.
* Tools: **jmap**, VisualVM, Eclipse Memory Analyzer (MAT)

```bash
# Using jmap
jmap -dump:format=b,file=heapdump.hprof <pid>
```

### **Step 4: Analyze Heap Dumps**

* Load heap dump in **Eclipse MAT, VisualVM, or YourKit**.
* Look for:

  * Objects with **largest retained heap**
  * **Duplicate / unexpected instances**
  * Objects still referenced via **GC roots**

**MAT Example:**

* Use **"Dominators Tree"** → shows objects holding the most memory
* Use **"Top Consumers"** → identify which classes consume most heap

### **Step 5: Identify Leaky References**

* Find **paths from GC roots** to leaked objects
* Commonly leaked references:

  * Static fields
  * Long-lived collections
  * Caches
  * ThreadLocals

### **Step 6: Fix the Leak**

* Remove unnecessary references
* Use **weak references** for caches (`WeakHashMap`)
* Close resources properly (try-with-resources)
* Deregister listeners / observers
* Limit cache size with eviction policies

---

## 4️⃣ Tools Summary

| Tool                              | Use Case                                          |
| --------------------------------- | ------------------------------------------------- |
| **VisualVM**                      | Real-time monitoring, heap dumps, memory analysis |
| **Eclipse Memory Analyzer (MAT)** | Advanced heap dump analysis, leak suspects        |
| **Java Flight Recorder (JFR)**    | Low-overhead production profiling                 |
| **YourKit / JProfiler**           | Commercial profiling & memory analysis            |
| **jmap / jhat**                   | Command-line heap dumps and analysis              |

---

## 5️⃣ Best Practices to Prevent Memory Leaks

1. **Close all resources** → use try-with-resources for streams, connections.
2. **Limit cache size** → use LRU or time-based eviction.
3. **Avoid unnecessary static references**.
4. **Clean up listeners and ThreadLocals** after use.
5. **Use monitoring** → GC logs, metrics for early detection.
6. **Code review** → check for object retention patterns.

---

## 6️⃣ Summary Flow

```
Detect Memory Leak → Monitor Heap → Take Heap Dump → Analyze → Identify Leaky References → Fix → Monitor
```

**Key Points:**

* Memory leaks cause OOM or performance degradation.
* Use **heap dumps and GC logs** for diagnosis.
* Tools like **VisualVM, MAT, YourKit** help pinpoint leaks.
* Prevention: proper resource management, weak references, and cache limits.

---

I can also create a **diagram showing memory leak detection workflow: JVM heap → GC logs → Heap Dump → Analysis → Fix**, which is very handy for interviews.

Do you want me to create that diagram?

---

## 285. How to analyze thread dump?

Absolutely! Let’s go step by step on **analyzing Java thread dumps**, including how to capture them, interpret them, and debug issues like deadlocks or thread contention.

---

## 1️⃣ What is a Thread Dump?

A **thread dump** is a snapshot of **all threads in a JVM** at a given time, including:

* Thread name & ID
* Thread state (`RUNNABLE`, `BLOCKED`, `WAITING`, `TIMED_WAITING`)
* Stack trace of each thread
* Locks held or waited for

**Purpose:** Identify **deadlocks, blocked threads, high CPU usage, or thread contention**.

---

## 2️⃣ When to Capture a Thread Dump

* Application **hangs or is slow**
* Unexpected **high CPU usage**
* **Deadlocks or thread contention**
* During **profiling and performance tuning**

---

## 3️⃣ How to Capture Thread Dumps

| Method                         | Command / Tool                               |
| ------------------------------ | -------------------------------------------- |
| **jstack**                     | `jstack <pid> > threaddump.txt`              |
| **kill -3**                    | `kill -3 <pid>` → dumps to stdout / log file |
| **VisualVM**                   | Attach to JVM → Threads → Thread Dump        |
| **JConsole / Mission Control** | Thread monitoring → capture dump             |
| **Spring Boot Actuator**       | `/actuator/threaddump` endpoint              |

> Capture **multiple dumps over time** (3–5) to identify consistent issues.

---

## 4️⃣ Understanding Thread States

| Thread State      | Meaning                                          |
| ----------------- | ------------------------------------------------ |
| **RUNNABLE**      | Thread is executing Java code or waiting for CPU |
| **BLOCKED**       | Waiting for monitor/lock held by another thread  |
| **WAITING**       | Waiting indefinitely for `notify()`/`signal()`   |
| **TIMED_WAITING** | Waiting with timeout (`sleep`, `wait`, `join`)   |
| **NEW**           | Thread created but not started                   |
| **TERMINATED**    | Thread finished execution                        |

---

## 5️⃣ Key Sections in a Thread Dump

1. **Thread header**

```
"worker-1" #12 prio=5 os_prio=0 tid=0x00007f8 java.lang.Thread.State: RUNNABLE
```

* Thread name = `worker-1`
* Thread ID = `#12`
* State = `RUNNABLE`

2. **Stack trace**

```
at java.lang.Thread.sleep(Native Method)
at com.example.MyService.run(MyService.java:45)
```

* Shows **exact code location** where the thread is stuck or running.

3. **Locks / Monitors**

```
- waiting to lock <0x000000> (a java.lang.Object)
- locked <0x000001> (a java.lang.Object)
```

* Indicates which locks are **held** and which are **contended**.

---

## 6️⃣ Analyzing Common Issues

### **1. Deadlocks**

* Look for:

```
Found one Java-level deadlock:
"Thread-1":
  waiting to lock <0x1> (held by Thread-2)
"Thread-2":
  waiting to lock <0x2> (held by Thread-1)
```

* **Fix:** Change lock acquisition order, reduce synchronized blocks, use `ReentrantLock.tryLock()`.

### **2. Thread Contention / Blocking**

* Threads in `BLOCKED` state on same monitor → indicates **hot lock / bottleneck**.
* Fix: Reduce synchronized scope, use concurrent collections.

### **3. High CPU**

* Many threads in `RUNNABLE` but stuck in loops → check **stack traces** for hot methods.

### **4. Waiting / TIMED_WAITING**

* Often normal if threads wait for I/O, queues, or scheduled tasks.
* Check if waiting is **expected** or causing backlog.

---

## 7️⃣ Tools for Easier Analysis

| Tool                           | Features                                                    |
| ------------------------------ | ----------------------------------------------------------- |
| **VisualVM**                   | Thread visualization, live thread state chart               |
| **FastThread**                 | Online thread dump analyzer, detects deadlocks and hotspots |
| **Java Mission Control (JMC)** | Live thread monitoring, profiling                           |
| **YourKit / JProfiler**        | Commercial profiling with thread contention and locks       |

---

## 8️⃣ Best Practices

1. **Take multiple dumps** → helps distinguish transient vs consistent issues.
2. **Correlate with CPU usage** → if CPU is 100%, look for RUNNABLE threads.
3. **Focus on blocked / waiting threads** → usually the root cause of bottlenecks.
4. **Identify deadlocks early** → fix locking order or use non-blocking concurrency.
5. **Combine with heap dump** → memory and thread issues often related.

---

## 9️⃣ Summary Workflow

```
Detect Performance Issue → Capture Thread Dump → Identify Thread States → Analyze Stack Traces → Detect Deadlocks / Contention → Apply Fixes → Monitor
```

**Key Points:**

* Thread dumps are **snapshots, not continuous monitoring**
* RUNNABLE ≠ “stuck” – check stack trace
* BLOCKED / WAITING often indicate **synchronization issues**
* Deadlocks can be **directly reported** in thread dump

---

I can also create a **diagram showing JVM threads, their states (RUNNABLE, BLOCKED, WAITING), stack traces, and locks**, which is very useful for interviews.

Do you want me to create that diagram?

---

## 286. Gateway Timeout vs Service Unavailable - troubleshooting?

Absolutely! Let’s break down **HTTP 504 Gateway Timeout** vs **HTTP 503 Service Unavailable**, their causes, and troubleshooting steps, especially in a **microservices or cloud-native context**.

---

## 1️⃣ HTTP Status Codes Overview

| Status Code | Name                | Meaning                                                                                                |
| ----------- | ------------------- | ------------------------------------------------------------------------------------------------------ |
| **503**     | Service Unavailable | The server is currently **unable to handle the request**. Usually temporary.                           |
| **504**     | Gateway Timeout     | The **server acting as a gateway or proxy** did not receive a timely response from an upstream server. |

---

## 2️⃣ Key Differences

| Aspect            | 503 Service Unavailable                                        | 504 Gateway Timeout                                        |
| ----------------- | -------------------------------------------------------------- | ---------------------------------------------------------- |
| **Source**        | Origin server (application/service itself)                     | Gateway / API Gateway / Reverse Proxy                      |
| **Reason**        | Server overloaded, down for maintenance, or resource exhausted | Upstream service took too long to respond                  |
| **Typical Usage** | Temporary overload, maintenance, circuit breaker               | Timeout between proxy/gateway and backend service          |
| **Recovery**      | Retry later, scale server                                      | Check upstream response time, network, or timeout settings |

---

## 3️⃣ Typical Causes

### **503 Service Unavailable**

* Application crash or not started
* Server overloaded → high CPU/memory
* Circuit breaker or rate-limiting triggered
* Maintenance window (manual or automated)

### **504 Gateway Timeout**

* API Gateway / Load Balancer timeout exceeded
* Slow upstream service or database query
* Network latency between gateway and service
* Misconfigured timeout settings in gateway / reverse proxy

---

## 4️⃣ Troubleshooting Steps

### **Step 1: Identify the Source**

* **503:** Comes from the service itself → check service logs
* **504:** Comes from gateway / proxy → check API Gateway or load balancer logs

### **Step 2: Check Service Health**

* Use **health checks** (`/actuator/health`) to ensure service is alive
* Verify pods are **ready** in Kubernetes:

```bash
kubectl get pods
kubectl describe pod <pod-name>
```

### **Step 3: Review Metrics**

* **CPU / Memory usage** → if service is overloaded, 503 is common
* **Latency / Response times** → if upstream service responds slowly, gateway timeout occurs

### **Step 4: Check Timeout Configurations**

* **API Gateway / Nginx / HAProxy / Envoy** → default timeout might be low
* **Spring Boot / Tomcat / Jetty** → server timeout settings (e.g., `server.connection-timeout`)

### **Step 5: Analyze Logs**

* Check **application logs** for slow requests or errors
* Check **gateway logs** for timeout errors
* Identify slow endpoints or database queries

### **Step 6: Apply Fixes**

**For 503:**

* Scale service horizontally (increase replicas)
* Fix resource bottlenecks (CPU, memory, database)
* Reduce load using circuit breakers / rate limiting

**For 504:**

* Increase timeout in gateway / proxy
* Optimize upstream service response time (database indexes, caching)
* Ensure network stability between services

---

## 5️⃣ Example: Microservices Scenario

```
Client → API Gateway → Service A → Service B → Database
```

* **503**: Service B crashed → Service A returns 503
* **504**: Service B is slow → API Gateway returns 504 to client

---

## 6️⃣ Best Practices

1. **Implement health checks** → avoid sending traffic to unhealthy services
2. **Use circuit breakers & bulkheads** → prevent cascading failures
3. **Set proper timeouts** → avoid long waits at gateways
4. **Use retries with exponential backoff** → for transient failures
5. **Monitor metrics** → CPU, memory, latency, request failures
6. **Scale services dynamically** → Kubernetes HPA / cluster autoscaler

---

✅ **Summary Table**

| Status                  | Source              | Cause                        | Fix                                                |
| ----------------------- | ------------------- | ---------------------------- | -------------------------------------------------- |
| 503 Service Unavailable | Application server  | Overload, crash, maintenance | Scale service, fix bug, reduce load                |
| 504 Gateway Timeout     | API Gateway / Proxy | Upstream slow / timeout      | Optimize upstream, increase timeout, check network |

---

I can also create a **diagram showing client → API Gateway → service flow with 503 vs 504 scenarios**, highlighting where each error originates.

Do you want me to create that diagram?

---

## 287. How do you optimize database queries?

Absolutely! Let’s go step by step on **optimizing database queries**, including strategies, techniques, and best practices for relational (e.g., MySQL, PostgreSQL) or NoSQL databases.

---

## 1️⃣ Why Query Optimization is Important

* **Performance:** Reduce query execution time and improve application responsiveness
* **Scalability:** Handle more concurrent users without overloading the database
* **Resource efficiency:** Lower CPU, memory, and I/O usage

---

## 2️⃣ Common Performance Issues

| Issue                         | Description                                         |
| ----------------------------- | --------------------------------------------------- |
| **Full table scans**          | Query reads the entire table due to missing indexes |
| **N+1 queries**               | Application issues repeated queries in loops        |
| **Joins on large tables**     | Slow join operations without proper indexing        |
| **Inefficient WHERE clauses** | Functions or calculations prevent index usage       |
| **Lack of pagination**        | Retrieving all rows instead of limited sets         |
| **Blocking / locking**        | Long transactions holding locks, causing contention |

---

## 3️⃣ Query Optimization Strategies

### **A. Indexing**

* Use **B-tree / hash / composite indexes** to speed up lookups
* Index columns used in **WHERE, JOIN, ORDER BY, GROUP BY**
* Avoid excessive indexing → overhead on writes
* Example:

```sql
CREATE INDEX idx_user_email ON users(email);
```

---

### **B. Limit Selected Columns**

* Avoid `SELECT *` → retrieve only needed columns

```sql
SELECT id, name, email FROM users WHERE status='ACTIVE';
```

---

### **C. Use Proper Joins**

* Prefer **INNER JOIN** over **CROSS JOIN** if possible
* Ensure **join columns are indexed**
* Example:

```sql
SELECT o.id, c.name
FROM orders o
JOIN customers c ON o.customer_id = c.id
WHERE o.status='PENDING';
```

---

### **D. Query Rewriting**

* Replace subqueries with **JOINs** if more efficient
* Use **EXISTS** instead of `IN` for large datasets
* Avoid functions on indexed columns in WHERE clause

---

### **E. Pagination / Limit**

* Fetch only required rows

```sql
SELECT * FROM orders ORDER BY created_at DESC LIMIT 50 OFFSET 0;
```

* For large tables, **keyset pagination** is faster than offset-based

---

### **F. Caching / Materialized Views**

* Use **Redis / Memcached** for frequently read queries
* Use **materialized views** in DB for expensive aggregations

---

### **G. Analyze Execution Plans**

* Use `EXPLAIN` in SQL to see how queries execute

```sql
EXPLAIN SELECT * FROM orders WHERE customer_id = 123;
```

* Look for **full table scans, missing indexes, inefficient joins**

---

### **H. Optimize Transactions**

* Keep transactions **short** → avoid holding locks
* Use **appropriate isolation levels** to reduce contention
* Batch updates/inserts to reduce overhead

---

### **I. Partitioning / Sharding**

* **Partition large tables** → split by date, region, or type
* **Sharding** → horizontal split across multiple DB nodes for high-scale systems

---

### **J. Use Connection Pooling**

* Use HikariCP, c3p0, or database-provided pools to **reuse connections** efficiently

---

## 4️⃣ Monitoring & Tools

| Tool / Command                         | Use                                                                  |
| -------------------------------------- | -------------------------------------------------------------------- |
| **EXPLAIN / EXPLAIN ANALYZE**          | See query execution plan                                             |
| **SHOW STATUS / pg_stat_statements**   | Monitor slow queries and counts                                      |
| **Database profiler / slow query log** | Identify long-running queries                                        |
| **ORM logging**                        | Hibernate, JPA: enable SQL logs to detect N+1 issues                 |
| **APM tools**                          | NewRelic, Datadog, AppDynamics → monitor query latency in production |

---

## 5️⃣ Best Practices Summary

1. **Use indexes smartly** → WHERE, JOIN, ORDER BY, GROUP BY
2. **Limit result sets** → use pagination or filters
3. **Avoid unnecessary columns** → don’t select everything
4. **Rewrite inefficient queries** → avoid subqueries or functions on indexed columns
5. **Use caching** → Redis, Memcached, or materialized views
6. **Monitor execution plans** → EXPLAIN or profiler tools
7. **Batch operations & short transactions**
8. **Consider partitioning/sharding** for large datasets
9. **Avoid N+1 queries** → fetch joins or batching
10. **Regularly analyze slow query logs**

---

✅ **Summary Table**

| Optimization Technique | Example / Note                                           |
| ---------------------- | -------------------------------------------------------- |
| Indexing               | B-tree / composite indexes on frequently queried columns |
| Column Limiting        | `SELECT id, name` instead of `SELECT *`                  |
| Query Rewriting        | Replace subquery with JOIN or EXISTS                     |
| Pagination             | `LIMIT 50 OFFSET 0` or keyset pagination                 |
| Caching                | Redis for frequently read results                        |
| Analyze Execution Plan | `EXPLAIN SELECT ...`                                     |
| Batch & Transactions   | Reduce lock contention and DB roundtrips                 |

---

I can also create a **diagram showing optimized query flow: client → cache → DB with indexes → paginated results**, which is great for interviews.

Do you want me to create that diagram?

---

## 288. How to handle high CPU usage in production?

Absolutely! Let’s break down **handling high CPU usage in production** step by step, including **diagnosis, root causes, mitigation, and prevention**.

---

## 1️⃣ Symptoms of High CPU Usage

* Application slowdown or unresponsiveness
* High response times / timeouts
* Thread starvation or queuing
* System alerts or scaling triggers

---

## 2️⃣ Common Causes

| Cause                             | Description                                         |
| --------------------------------- | --------------------------------------------------- |
| **Inefficient code / algorithms** | CPU-heavy loops, recursion, or complex computations |
| **High request volume**           | Sudden traffic spikes overwhelm the server          |
| **Excessive garbage collection**  | Frequent GC due to memory pressure                  |
| **Thread contention**             | Many threads competing for locks                    |
| **Database / I/O bottlenecks**    | CPU waiting on slow queries or disk I/O             |
| **Infinite loops / busy waits**   | Logic errors in code                                |
| **Misconfigured thread pools**    | Too many threads causing context switching overhead |

---

## 3️⃣ Diagnosis Steps

### **Step 1: Monitor CPU**

* Tools: **top, htop, vmstat (Linux)**, **Cloud monitoring dashboards**
* Check **per-process CPU usage**

### **Step 2: Thread Dumps**

* Capture multiple dumps to see **threads consuming CPU**

```bash
jstack <pid> > threaddump.txt
```

* Look for threads in **RUNNABLE** state stuck in loops or hot methods

### **Step 3: Profiling**

* Use **Java profilers**: VisualVM, JFR (Java Flight Recorder), YourKit, JProfiler
* Identify **hot methods or inefficient algorithms**

### **Step 4: Analyze Garbage Collection**

* Enable GC logs:

```bash
-XX:+PrintGCDetails -XX:+PrintGCDateStamps -Xloggc:gc.log
```

* Look for **frequent or long GC pauses** indicating memory pressure

### **Step 5: Check Database / I/O**

* Slow queries can cause CPU waiting
* Enable slow query logging, use connection pool metrics

---

## 4️⃣ Mitigation Strategies

### **Code Optimization**

* Optimize loops, recursion, and data structures
* Reduce object creation → less GC overhead
* Use **efficient algorithms**

### **Thread & Pool Management**

* Configure **optimal thread pool sizes**
* Avoid thread oversubscription → context switching overhead

### **Caching**

* Use **Redis / Memcached** for frequently accessed data
* Reduce repeated expensive calculations or DB queries

### **Database Optimization**

* Add indexes, rewrite slow queries, batch operations
* Reduce unnecessary joins / data retrieval

### **Load Management**

* Enable **rate limiting** at API Gateway
* Queue requests using **message brokers** for asynchronous processing

### **GC Tuning**

* Switch to **G1 / ZGC / Shenandoah** for large heaps
* Adjust **heap size** to reduce frequent collections

### **Scaling**

* Horizontal scaling → add more instances
* Use auto-scaling in Kubernetes or cloud platforms

---

## 5️⃣ Prevention & Best Practices

1. **Monitoring & Alerts**

   * CPU, memory, threads, GC metrics → Prometheus, Grafana, CloudWatch
2. **Profiling in staging**

   * Detect hot paths before production deployment
3. **Use Circuit Breakers & Bulkheads**

   * Prevent cascading failures under high load
4. **Asynchronous processing**

   * Move CPU-heavy tasks to background jobs / queues
5. **Limit concurrent requests**

   * Thread pool limits and API throttling
6. **Optimize JVM settings**

   * Heap size, GC tuning, JIT compiler optimizations

---

## 6️⃣ Quick Summary Table

| Step                | Tool / Action                       | Purpose                        |
| ------------------- | ----------------------------------- | ------------------------------ |
| Monitor CPU         | top, htop, Cloud Metrics            | Detect high usage processes    |
| Thread Analysis     | jstack, VisualVM                    | Identify hot threads / loops   |
| Profiling           | JFR, YourKit                        | Pinpoint CPU-intensive methods |
| GC Analysis         | GC logs, JFR                        | Reduce GC overhead             |
| Database            | Indexing, query optimization        | Reduce CPU wait on DB          |
| Scaling             | Horizontal / vertical               | Handle load spikes             |
| Code / Architecture | Optimize code, caching, async tasks | Prevent future high CPU        |

---

✅ **Key Takeaways**

* High CPU can be caused by **code, DB, I/O, GC, or thread issues**
* Use **thread dumps, profilers, and metrics** to pinpoint the root cause
* Mitigate via **code optimization, caching, async processing, and scaling**
* Always **monitor and tune** proactively to prevent spikes

---

I can also create a **diagram showing high CPU troubleshooting flow: metrics → thread dump → profiler → fix → scale**, which is great for interviews.

Do you want me to create that diagram?

---

## 289. What tools do you use for application monitoring?

Absolutely! Let’s go through the **tools commonly used for application monitoring**, categorized by their purpose and usage in modern Java/cloud-native applications.

---

## 1️⃣ Types of Application Monitoring

| Type                                         | Purpose                                           |
| -------------------------------------------- | ------------------------------------------------- |
| **Infrastructure Monitoring**                | CPU, memory, disk, network usage of servers/VMs   |
| **Application Performance Monitoring (APM)** | Metrics, latency, error rates, transaction traces |
| **Log Monitoring**                           | Centralized logging, log analysis, alerting       |
| **Distributed Tracing / Observability**      | Track requests across microservices               |
| **Alerting & Dashboards**                    | Notify on thresholds, visualize metrics           |

---

## 2️⃣ Common Tools

### **A. Infrastructure & Metrics Monitoring**

| Tool                 | Purpose                                       | Notes                                         |
| -------------------- | --------------------------------------------- | --------------------------------------------- |
| **Prometheus**       | Metrics collection from apps & infrastructure | Often paired with Grafana for visualization   |
| **Grafana**          | Dashboard & visualization                     | Can integrate Prometheus, Loki, Elasticsearch |
| **CloudWatch (AWS)** | Cloud-native monitoring                       | Metrics, logs, alarms for AWS resources       |
| **Datadog**          | Metrics + monitoring + APM                    | SaaS-based, cloud-native support              |
| **Zabbix / Nagios**  | Traditional server monitoring                 | CPU, memory, disk, network, alerts            |

---

### **B. Application Performance Monitoring (APM)**

| Tool            | Purpose                                       | Notes                                       |
| --------------- | --------------------------------------------- | ------------------------------------------- |
| **New Relic**   | Full-stack APM                                | Java, Spring Boot, microservices monitoring |
| **AppDynamics** | Performance & business transaction monitoring | Supports Java, DB, and infrastructure       |
| **Dynatrace**   | Auto-discovery & monitoring                   | AI-powered anomaly detection                |
| **Elastic APM** | Open-source APM                               | Part of ELK stack                           |

---

### **C. Log Management & Monitoring**

| Tool                                            | Purpose                     | Notes                                  |
| ----------------------------------------------- | --------------------------- | -------------------------------------- |
| **ELK Stack (Elasticsearch, Logstash, Kibana)** | Collect, index, search logs | Centralized logging for microservices  |
| **Loki + Grafana**                              | Lightweight log aggregation | Works well with Prometheus metrics     |
| **Splunk**                                      | Enterprise log analytics    | Powerful search & correlation features |
| **Graylog**                                     | Centralized log management  | Open-source alternative                |

---

### **D. Distributed Tracing / Observability**

| Tool                    | Purpose                | Notes                                      |
| ----------------------- | ---------------------- | ------------------------------------------ |
| **Jaeger**              | Open-source tracing    | Traces requests across microservices       |
| **Zipkin**              | Distributed tracing    | Works with Spring Cloud Sleuth             |
| **OpenTelemetry**       | Metrics, traces, logs  | Vendor-neutral, standardizes observability |
| **Spring Cloud Sleuth** | Tracing in Spring Boot | Adds trace IDs to logs for microservices   |

---

### **E. Alerting & Incident Management**

| Tool                        | Purpose                   | Notes                                   |
| --------------------------- | ------------------------- | --------------------------------------- |
| **Prometheus Alertmanager** | Alerting based on metrics | Integrates with email, Slack, PagerDuty |
| **Grafana Alerting**        | Custom dashboard alerts   | Threshold-based or anomaly detection    |
| **PagerDuty / OpsGenie**    | Incident response         | Escalation & on-call management         |
| **Slack / MS Teams**        | Notification channel      | Used with APM or monitoring tools       |

---

## 3️⃣ Typical Monitoring Stack for Java Microservices

```
Application (Spring Boot) 
    ↓ Micrometer / Sleuth
Metrics → Prometheus → Grafana Dashboards
Logs → ELK / Loki → Kibana / Grafana
Tracing → Sleuth → Jaeger / Zipkin
Alerts → Prometheus Alertmanager / Grafana → PagerDuty / Slack
```

**Notes:**

* **Micrometer** → standardized metrics for Java apps, integrates with Prometheus
* **Spring Boot Actuator** → exposes metrics, health checks, thread pools
* **Sleuth** → distributed tracing across microservices

---

## 4️⃣ Best Practices

1. **Centralize logs & metrics** → don’t rely on local server logs
2. **Use distributed tracing** → track requests across microservices
3. **Set meaningful alerts** → CPU, memory, response time, error rate thresholds
4. **Visualize dashboards** → Grafana or Kibana for quick insights
5. **Correlate logs, metrics, and traces** → faster root cause analysis

---

✅ **Summary Table**

| Monitoring Aspect        | Tool Examples                                      |
| ------------------------ | -------------------------------------------------- |
| Infrastructure / Metrics | Prometheus, Grafana, CloudWatch, Datadog           |
| Application Performance  | New Relic, AppDynamics, Dynatrace, Elastic APM     |
| Logs                     | ELK Stack, Loki, Splunk, Graylog                   |
| Distributed Tracing      | Jaeger, Zipkin, OpenTelemetry, Spring Cloud Sleuth |
| Alerts / Incident        | Prometheus Alertmanager, Grafana, PagerDuty, Slack |

---

I can also create a **diagram showing full monitoring flow for a Java microservices app: metrics → logs → tracing → dashboards → alerts**, which is very useful for interviews.

Do you want me to create that diagram?

---

## 290. How do you implement distributed tracing?

Absolutely! Let’s go step by step on **implementing distributed tracing** for Java microservices, including concepts, tools, and practical implementation.

---

## 1️⃣ What is Distributed Tracing?

**Distributed tracing** tracks a **request as it flows across multiple microservices** in a system.

It helps:

* Identify **performance bottlenecks**
* Detect **latency issues** in a service chain
* Troubleshoot **errors and failures** in distributed systems

**Core concepts:**

| Concept                       | Meaning                                                       |
| ----------------------------- | ------------------------------------------------------------- |
| **Trace**                     | Entire journey of a request across multiple services          |
| **Span**                      | Single operation within a trace (e.g., method call, DB query) |
| **Trace ID**                  | Unique ID for the request across all services                 |
| **Span ID**                   | Unique ID for each span within a trace                        |
| **Parent-Child Relationship** | Spans can have parent-child links to show call hierarchy      |

---

## 2️⃣ When to Use Distributed Tracing

* Microservices architecture
* High latency or error troubleshooting
* Performance optimization and bottleneck detection
* Correlating logs with request paths

---

## 3️⃣ Tools for Distributed Tracing

| Tool                    | Notes                                                  |
| ----------------------- | ------------------------------------------------------ |
| **Jaeger**              | Open-source, integrates with OpenTelemetry, Prometheus |
| **Zipkin**              | Popular tracing tool, works with Spring Cloud Sleuth   |
| **OpenTelemetry**       | Vendor-neutral, collects metrics, logs, traces         |
| **Spring Cloud Sleuth** | Adds trace IDs to logs in Spring Boot apps             |

---

## 4️⃣ Implementing Distributed Tracing in Java (Spring Boot Example)

### **Step 1: Add Dependencies**

```xml
<!-- Spring Cloud Sleuth + Zipkin -->
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-sleuth</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-zipkin</artifactId>
</dependency>
```

---

### **Step 2: Configure Tracing**

```yaml
# application.yml
spring:
  zipkin:
    base-url: http://localhost:9411
    sender: web
  sleuth:
    sampler:
      probability: 1.0  # 100% of requests traced in dev
```

* `probability` → fraction of requests to trace (0.0–1.0)

---

### **Step 3: Automatic Tracing**

* Sleuth automatically:

  * Generates **trace IDs** for incoming requests
  * Propagates trace context to **outgoing HTTP / Feign / RestTemplate / Kafka** calls
  * Adds **trace IDs to logs** for correlation

Example log:

```
2025-10-08 12:00:00.123 TRACE [order-service,traceId=abcd1234,spanId=efgh5678] Order created
```

---

### **Step 4: Instrument Custom Spans (Optional)**

```java
@Autowired
Tracer tracer;

public void processOrder() {
    Span newSpan = tracer.nextSpan().name("processOrder").start();
    try (Tracer.SpanInScope ws = tracer.withSpan(newSpan.start())) {
        // custom code to trace
    } finally {
        newSpan.end();
    }
}
```

---

### **Step 5: Run Zipkin / Jaeger**

* Start Zipkin server:

```bash
docker run -d -p 9411:9411 openzipkin/zipkin
```

* Access tracing UI at `http://localhost:9411/`
* View **trace paths, span durations, and service interactions**

---

## 5️⃣ Best Practices

1. **Use sampling** → avoid tracing every request in high-volume production
2. **Propagate trace IDs** → ensure all downstream services receive the same trace ID
3. **Integrate logs with trace IDs** → makes debugging easier
4. **Instrument critical paths** → DB calls, external APIs, messaging queues
5. **Use centralized tracing UI** → Jaeger / Zipkin for visualization

---

## 6️⃣ Summary Workflow

```
Client Request → API Gateway → Service A → Service B → Database
        │               │          │
   Trace ID propagated   │          │
        ↓               ↓          ↓
   Sleuth / OpenTelemetry captures spans
        ↓
     Trace exported to Zipkin / Jaeger
        ↓
  Visualize trace, spans, latency, errors
```

---

✅ **Key Points**

* Distributed tracing tracks **requests across multiple services**
* **Trace → Spans → IDs** are the core building blocks
* Tools: **Spring Cloud Sleuth + Zipkin / Jaeger / OpenTelemetry**
* Integration includes **automatic trace propagation and log correlation**

---

I can also create a **diagram showing a client request flowing across microservices with traces and spans visualized in Zipkin/Jaeger**, which is excellent for interviews.

Do you want me to create that diagram?

---

## 291. Service Not Found - how to troubleshoot?

Absolutely! Let’s break down **“Service Not Found” errors**, their causes, and how to troubleshoot them in a microservices or distributed system.

---

## 1️⃣ What “Service Not Found” Means

* Typically corresponds to **HTTP 404** or **API Gateway routing failures**
* The client or service tried to call another service, but the **service endpoint could not be located**
* Common in **microservices, service discovery, or API gateway setups**

---

## 2️⃣ Common Causes

| Cause                                     | Description                                              |
| ----------------------------------------- | -------------------------------------------------------- |
| **Incorrect service URL or endpoint**     | Typo or wrong path in client or API Gateway              |
| **Service is down / not deployed**        | The target service is not running or crashed             |
| **Service not registered with discovery** | In dynamic environments (Eureka, Consul, Kubernetes DNS) |
| **DNS / Network issues**                  | Service host not resolvable or network partitioned       |
| **API Gateway misconfiguration**          | Route not defined, wrong path mapping                    |
| **Versioning mismatch**                   | Client calling wrong version (`/v2/endpoint`)            |
| **Firewall / security rules**             | Blocks requests to target service                        |

---

## 3️⃣ Troubleshooting Steps

### **Step 1: Check Client Request**

* Verify **URL, endpoint, port**
* Confirm **HTTP method** matches (`GET`, `POST`, etc.)

### **Step 2: Verify Service Health**

* Check if the service is **running / healthy**
* For Spring Boot, use Actuator endpoint:

```http
GET http://service-host:port/actuator/health
```

* In Kubernetes:

```bash
kubectl get pods
kubectl describe pod <pod-name>
kubectl logs <pod-name>
```

### **Step 3: Check Service Discovery / Registry**

* Ensure service is **registered** (Eureka, Consul, etc.)
* Use registry dashboard or API to confirm the service instance exists

### **Step 4: Check API Gateway / Load Balancer**

* Verify **route configuration**
* Ensure **gateway is pointing to correct service name and port**
* In Spring Cloud Gateway / Zuul: check `application.yml` route definitions

### **Step 5: Check DNS / Network**

* For containerized environments, ensure **service DNS resolves**
* Kubernetes example:

```bash
nslookup my-service.default.svc.cluster.local
ping my-service.default.svc.cluster.local
```

### **Step 6: Check Logs**

* **Client logs** → may show wrong endpoint or URL
* **Server logs** → check if requests are reaching the service

### **Step 7: Versioning / API Contract**

* Ensure the endpoint **exists in the current service version**
* Check **OpenAPI / Swagger definitions** for mismatched paths

---

## 4️⃣ Preventive Measures

1. **Health checks & readiness probes** → avoid routing to unhealthy services
2. **Service discovery with retries** → clients retry if service temporarily missing
3. **API Gateway validation** → reject unknown paths early
4. **Use DNS aliases / stable service names** → avoid hard-coded IPs
5. **Centralized logging / monitoring** → detect missing services quickly
6. **API versioning management** → avoid calling deprecated or non-existent endpoints

---

## 5️⃣ Summary Table

| Step | Action                                                                 |
| ---- | ---------------------------------------------------------------------- |
| 1    | Verify client request URL, endpoint, and method                        |
| 2    | Check target service health (`/actuator/health`)                       |
| 3    | Confirm service is registered with discovery (Eureka, Consul, K8s DNS) |
| 4    | Check API Gateway / Load Balancer route configuration                  |
| 5    | Test network connectivity & DNS resolution                             |
| 6    | Review client and server logs for routing errors                       |
| 7    | Validate API version & contract                                        |

---

✅ **Key Takeaways**

* **Service Not Found** is usually a **routing, registration, or configuration issue**
* Troubleshoot by checking **client request → service health → service registry → gateway → network → logs**
* Prevent with **health checks, retries, monitoring, and proper API versioning**

---

I can also create a **diagram showing service discovery flow with API Gateway and possible “Service Not Found” points**, which is very helpful for interviews.

Do you want me to create that diagram?

---

## 292. How to dubug locally & remotely?

Absolutely! Let’s go step by step on **debugging Java applications locally and remotely**, including setups, tools, and best practices.

---

## 1️⃣ Debugging Locally

### **Step 1: Use an IDE**

* Popular IDEs: **IntelliJ IDEA, Eclipse, VS Code (Java extension)**
* Open your project and set breakpoints in the code.

### **Step 2: Run in Debug Mode**

* **IntelliJ IDEA / Eclipse:**

  * Right-click → `Debug` instead of `Run`
  * Application starts with **debugger attached**
* Breakpoints hit when code executes → inspect variables, stack traces, threads.

### **Step 3: Inspect Variables & Evaluate Expressions**

* Watch variables, modify values at runtime
* Step through code:

  * **Step Over (F8)** → next line
  * **Step Into (F7)** → go inside method
  * **Step Out (Shift+F8)** → exit method

### **Step 4: Debug Spring Boot Applications**

* Use **Spring Boot DevTools** for live reload
* Use **Actuator endpoints** to inspect beans, metrics, health
* Example:

```bash
mvn spring-boot:run
# or
java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 -jar myapp.jar
```

---

## 2️⃣ Debugging Remotely

Remote debugging is **connecting your IDE to a JVM running on a remote server or container**.

### **Step 1: Enable Remote Debugging on JVM**

* Start JVM with debug agent:

```bash
java -agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005 -jar myapp.jar
```

**Options:**

* `transport=dt_socket` → use socket connection

* `server=y` → JVM listens for debugger

* `suspend=n` → don’t wait, start immediately

* `address=5005` → port for debugger connection

* For Spring Boot via Maven:

```bash
mvn spring-boot:run -Dspring-boot.run.jvmArguments="-agentlib:jdwp=transport=dt_socket,server=y,suspend=n,address=5005"
```

### **Step 2: Connect IDE**

* **IntelliJ IDEA / Eclipse:**

  * Run → `Edit Configurations` → `Remote`
  * Set **host** (server IP) and **port** (e.g., 5005)
  * Click `Debug` → IDE attaches to remote JVM

### **Step 3: Debug Inside Container / Kubernetes**

* Expose debug port in container:

```yaml
ports:
  - containerPort: 5005
    hostPort: 5005
```

* Start container JVM with debug agent (as above)
* Attach IDE to `host:5005`

---

## 3️⃣ Tips for Effective Debugging

1. **Use conditional breakpoints** → stop only when condition is true
2. **Log while debugging** → combine logs with breakpoints
3. **Remote debugging over SSH** → secure connection if server is not public

```bash
ssh -L 5005:localhost:5005 user@remote-server
```

4. **Use lightweight JVM flags** in production → avoid high overhead
5. **Thread / heap inspection** → attach profiler if needed

---

## 4️⃣ Common Pitfalls

| Issue                   | Solution                                    |
| ----------------------- | ------------------------------------------- |
| Port blocked / firewall | Open debug port, use SSH tunnel             |
| High load in prod       | Prefer profiling instead of full debug mode |
| IDE not connecting      | Check host, port, network access            |
| JVM version mismatch    | Ensure IDE JDK matches remote JVM           |

---

## 5️⃣ Summary Workflow

```
Local Debug:
IDE → Set breakpoints → Run in debug mode → Inspect variables / stack → Fix / test

Remote Debug:
Enable JVM debug agent → Open port → Attach IDE → Debug like local → Monitor logs
```

**Key Points:**

* **Local debugging** → fast, direct, low-risk
* **Remote debugging** → useful for staging/production, requires network setup
* Use **conditional breakpoints and logging** for efficient inspection

---

I can also create a **diagram showing local vs remote debugging flow, including IDE, JVM, debug ports, and network**, which is great for interviews.

Do you want me to create that diagram?

---