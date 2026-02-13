
## 386. What is Redis?

**Answer:**
**Redis (Remote Dictionary Server)** is an open-source, in-memory data structure store.
*   **Role:** Used as a database, cache, and message broker.
*   **Key Features:**
    *   **In-Memory:** Extremely fast (Sub-millisecond latency).
    *   **Persistence:** Can save data to disk (RDB/AOF).
    *   **Data Structures:** Supports more than just strings (Lists, Sets, Sorted Sets).

---

## 387. What data structures Redis supports?

**Answer:**
Redis is not just a Key-Value store; it supports complex data structures:
1.  **String:** Basic text or binary data (up to 512MB).
2.  **List:** Linked lists of strings (e.g., Queue/Stack).
3.  **Set:** Unordered collection of unique strings.
4.  **Sorted Set (ZSet):** Set ordered by a score (e.g., Leaderboard).
5.  **Hash:** Map of fields and values (like a Java Map).
6.  **Bitmap/HyperLogLog:** For advanced analytics.

---

## 388. What is TTL?

**Answer:**
**TTL (Time To Live)** is a setting that defines how long a key should exist in the cache before it is automatically deleted (expired).
*   **Command:** `EXPIRE key seconds` (e.g., `EXPIRE session:123 60`).
*   **Purpose:** Prevents stale data and frees up memory.

---

## 389. What is cache eviction policy?

**Answer:**
When Redis memory is full, the **Eviction Policy** determines which keys to remove to make space for new data.
*   **Policies:**
    *   `noeviction`: Returns error (Default).
    *   `allkeys-lru`: Evict Least Recently Used keys.
    *   `volatile-lru`: Evict Least Recently Used keys *that have an expiration set*.
    *   `allkeys-lfu`: Evict Least Frequently Used keys.
    *   `allkeys-random`: Random removal.

---

## 390. What is cache aside pattern?

**Answer:**
**Cache Aside (Lazy Loading)** is the most common caching strategy.
1.  **Read:** Application checks Cache.
    *   If **Hit**: Return data.
    *   If **Miss**: Load from DB, write to Cache, return data.
2.  **Write:** Application updates DB, then **invalidates** (deletes) the key in Cache. Next read will re-load fresh data.

---


## 391. What is write-through caching?

**Answer:**
**Write-Through** ensures data consistency by writing data to the cache and the database **simultaneously**.
*   **Pro:** Data in cache is always up-to-date (Strong Consistency).
*   **Con:** Higher write latency (2 writes). Good for read-heavy systems.

---

## 392. What is write-behind caching?

**Answer:**
**Write-Behind (Write-Back)** writes data *only* to the cache initially. The cache asynchronously syncs data to the DB later.
*   **Pro:** extremely fast writes.
*   **Con:** Risk of data loss if cache crashes before syncing. Eventual Consistency.

---

## 393. What is cache penetration?

**Answer:**
**Cache Penetration** occurs when a client requests data that **does not exist** in Cache OR Database.
*   **Impact:** Requests bypass cache and hit DB, potentially crashing it.
*   **Solution:**
    1.  Cache empty results (`null`) with short TTL.
    2.  Use **Bloom Filters**.

---

## 394. What is cache breakdown?

**Answer:**
**Cache Breakdown** (Hotspot Invalid) happens when a **hot key** expires, and massive concurrent requests hit the DB simultaneously.
*   **Solution:**
    1.  Mutex Locks (Only 1 thread queries DB).
    2.  Logical Expiry (Soft TTL).

---

## 395. What is cache avalanche?

**Answer:**
**Cache Avalanche** occurs when **many keys expire at the same time**.
*   **Impact:** DB spike/outage.
*   **Solution:**
    1.  Add random jitter to TTL.
    2.  Redis Cluster (High Availability).

---

## 396. How to handle distributed cache?

**Answer:**
**Distributed Cache** spreads data across multiple nodes (Sharding).
*   **Challenge:** How to know which node holds key "user:123"?
*   **Solution:** Consistent Hashing (partitions keys to nodes with minimal movement when nodes add/remove).

---

## 397. What is Redis clustering?

**Answer:**
**Redis Cluster** is a distributed implementation of Redis.
*   **Sharding:** Data partitioned into 16,384 hash slots.
*   **Nodes:** Automatic failover (Master-Slave).
*   **Client:** Connects to any node; redirected to correct node.

---

## 398. What is pub/sub in Redis?

**Answer:**
**Pub/Sub** allows messages to be broadcast to multiple consumers.
*   **Channels:** Publisher sends to `channel_name`. Subscribers listen to `channel_name`.
*   **Decoupled:** Publisher doesn't know subscribers.
*   **Fire-and-Forget:** No persistence (unlike Kafka).

---

## 399. How to implement distributed locking in Redis?

**Answer:**
To ensure mutual exclusion across distributed services:
*   **Simple:** `SET lock_key unique_id NX PX 10000` (Set if Not Exists, Expiry 10s).
*   **Redlock:** Algorithm for running dist-lock on Redis Cluster (more robust).

---

## 400. When not to use cache?

**Answer:**
1.  **Strong Consistency Required:** e.g., Bank balance during transfer.
2.  **Rapidly Changing Data:** If data changes faster than it is read.
3.  **One-off Reads:** Data read only once.
4.  **Complex Queries:** Redis isn't a SQL engine.
