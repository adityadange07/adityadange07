
## 581. What is system design?

**Answer:**
**System Design** is the process of defining the architecture, components, modules, interfaces, and data for a system to satisfy specified requirements.
*   **Goal:** Build systems that are scalable, reliable, and maintainable.

---

## 582. What is scalability?

**Answer:**
**Scalability** is the ability of a system to handle growing amounts of work by adding resources.
*   **Vertical (Scale Up):** Add more power (CPU/RAM) to an existing machine.
*   **Horizontal (Scale Out):** Add more machines to the pool.

---

## 583. What is availability?

**Answer:**
**Availability** is the percentage of time a system remains operational and accessible.
*   **Metric:** "Nines" (e.g., 99.9% uptime = 8.7 hours downtime/year; 99.999% = 5 mins/year).
*   **Strategy:** Redundancy, Failover, Replication.

---

## 584. What is reliability?

**Answer:**
**Reliability** is the probability that a system will perform its intended function without failure for a specified time.
*   **Key:** A system can be available (respond 200 OK) but unreliable (return wrong data).

---

## 585. What is CAP theorem?

**Answer:**
In a distributed system, you can only guarantee **two** of the following three:
1.  **Consistency (C):** All nodes see the same data at the same time.
2.  **Availability (A):** Every request receives a response (succeed/fail).
3.  **Partition Tolerance (P):** System continues to operate despite network failures (partitions).
*   **Reality:** In distributed systems, **P** is mandatory. You chose between **CP** (Consistency/MongoDB) or **AP** (Availability/Cassandra).

---

## 586. What is consistency model?

**Answer:**
Defines the rules for the apparent order and expected visibility of updates.
*   **Strong Consistency:** Updates are visible immediately to all (like a single machine).
*   **Eventual Consistency:** Updates will propagate to all nodes *eventually*.
*   **Causal Consistency:** Causally related operations are seen in order.

---

## 587. What is strong vs eventual consistency?

**Answer:**
*   **Strong:** Higher latency (wait for replication), limits availability (if replica down, write fails). Good for Banking.
*   **Eventual:** Low latency (return immediately), high availability. Good for Social Media feeds (it's okay if a post appears 1s later).

---

## 588. What is horizontal scaling?

**Answer:**
**Horizontal Scaling (Scaling Out):**
*   **Action:** Adding more servers (nodes) to the cluster.
*   **Pros:** Theoretically infinite scaling, cheaper commodity hardware, better fault tolerance.
*   **Cons:** Complex (requires Load Balancer, distributed data handling).

---

## 589. What is vertical scaling?

**Answer:**
**Vertical Scaling (Scaling Up):**
*   **Action:** Upgrade the server (t2.micro -> t2.large).
*   **Pros:** Simple (no code change).
*   **Cons:** Hard limit (finite hardware capacity), Single Point of Failure, Expensive.

---

## 590. What is load balancing?

**Answer:**
**Load Balancing** distributes incoming network traffic across multiple servers (backend).
*   **Algorithms:** Round Robin, Least Connections, IP Hash.
*   **Layer 4 (L4):** Transport Layer (TCP/UDP) - Fast.
*   **Layer 7 (L7):** Application Layer (HTTP/HTTPS) - Smart (can route based on URL path).

---

## 591. Design URL shortener.

**Answer:**
*   **Core:** Map a long URL to a short alphanumeric key.
*   **Algorithm:** Base62 encoding of a unique Database ID (or Snowflake ID).
*   **Database:** NoSQL (DynamoDB/Cassandra) for high write throughput.
*   **Redirect:** HTTP 301 (Permanent) (if analytics not needed) or 302 (Found) (if analytics needed).
*   **Scale:** Cache hot URLs (Redis).

---

## 592. Design rate limiter.

**Answer:**
*   **Goal:** Prevent abuse.
*   **Algorithms:** Token Bucket, Leaky Bucket, Fixed Window, Sliding Window Log.
*   **Storage:** Redis (fast increment/read).
*   **Implementation:** Middleware or API Gateway (Kong/AWS API Gateway).
*   **Response:** HTTP 429 Too Many Requests.

---

## 593. Design notification system.

**Answer:**
*   **Core:** Decouple trigger from delivery.
*   **Flow:** Service A -> Kafka -> Notification Service -> 3rd Party (SendGrid/Twilio/FCM).
*   **Features:** User Preferences (Opt-out), Rate Limiting (Don't spam), Retry mechanism (Dead Letter Queue).

---

## 594. Design chat system.

**Answer:**
*   **Protocol:** WebSocket (Bi-directional, low latency).
*   **Storage:** Cassandra/HBase (Write-heavy, time-series data).
*   **Real-time:** Redis Pub/Sub to broadcast messages across WebSocket servers.
*   **Status:** User Presence (Online/Offline) via Heartbeats in Redis.

---

## 595. Design file storage system.

**Answer:**
*   **Core:** Like Google Drive/Dropbox.
*   **Storage:** Object Storage (S3) for files.
*   **Metadata:** SQL/NoSQL for file hierarchy (Parent ID), Owner, Permissions.
*   **Upload:** Generate Presigned URL so client uploads directly to S3 (offload traffic from server).
*   **Sync:** Block-level deduplication to save bandwidth.

---

## 596. Design payment system.

**Answer:**
*   **Key:** **Consistency** is paramount (ACID).
*   **Database:** SQL (PostgreSQL/Oracle) with Strong Consistency.
*   **Idempotency:** Ensure retries don't charge twice (Use unique `idempotency_key`).
*   **Distributed Transactions:** Two-Phase Commit (2PC) or Saga Pattern (Compensating transactions).
*   **Reconciliation:** Background job to verify internal DB vs Payment Gateway records.

---

## 597. Design logging system.

**Answer:**
*   **Collection:** Filebeat/Fluentd sidecars on pods.
*   **Aggregation:** Kafka (buffer logs during spikes).
*   **Indexing:** Elasticsearch (Searchable).
*   **Visualization:** Kibana.
*   **Retention:** Move old logs to S3 (Cold storage) to save costs.

---

## 598. Design API gateway.

**Answer:**
*   **Role:** Entry point for all client traffic.
*   **Features:** Authentication (JWT validation), Rate Limiting, Routing (Path-based), Protocol Translation (REST -> gRPC), Caching, Logging.
*   **Tools:** Netflix Zuul, Spring Cloud Gateway, Nginx, Kong.

---

## 599. Design distributed cache.

**Answer:**
*   **Algo:** Consistent Hashing to distribute keys across nodes.
*   **Eviction:** LRU (Least Recently Used), LFU.
*   **Consistency:** Cache-Aside (Lazy Loading) vs Write-Through vs Write-Back.
*   **Thundering Herd:** Use locking or random expiration times to prevent all keys expiring at once.

---

## 600. Design search service.

**Answer:**
*   **Core:** Inverted Index (Map words to document IDs).
*   **Tool:** Elasticsearch / Solr / Apache Lucene.
*   **Ingestion:** CDC (Change Data Capture) from main DB -> Kafka -> Elasticsearch.
*   **Query:** Support fuzzy search, synonyms, ranking algorithms (TF-IDF).

---

## 601. How to design high QPS system?

**Answer:**
1.  **Stateless:** Apps should be stateless to scale horizontally.
2.  **Caching:** Use Redis/Memcached to offload DB (Read-heavy).
3.  **Async:** Use Kafka/RabbitMQ to buffer writes (Write-heavy).
4.  **Database:** Sharding (Partition data) and Read Replicas.
5.  **CDN:** Serve static content from edge locations.

---

## 602. How to design id generation?

**Answer:**
Requirements: Unique, Numerical, Sortable by time.
1.  **UUID:** Simple, but not numerical/sortable, large (128-bit).
2.  **Database Auto-Increment:** Simple, but SPOF in distributed system.
3.  **Snowflake ID:** Distributed, unique, time-sortable, 64-bit long.

---

## 603. What is snowflake ID?

**Answer:**
Twitter's **Snowflake ID** is a 64-bit integer composed of:
*   **Sign bit:** 1 bit (unused).
*   **Timestamp:** 41 bits (milliseconds since epoch).
*   **Machine ID:** 10 bits (supports 1024 nodes).
*   **Sequence:** 12 bits (supports 4096 IDs per millisecond per node).

---

## 604. What is CDN?

**Answer:**
**CDN (Content Delivery Network)** is a network of geographically distributed servers that serve static content (Images, CSS, JS) to users from the nearest edge location.
*   **Benefits:** Lower latency, reduced load on origin server.
*   **Providers:** CloudFront, Akamai, Cloudflare.

---

## 605. What is reverse proxy?

**Answer:**
A **Reverse Proxy** sits between the client and the backend servers.
*   **Functions:** Load Balancing, SSL Termination, Caching, Compression (Gzip), Security (WAF).
*   **Examples:** Nginx, HAProxy.

---

## 606. What is caching strategy?

**Answer:**
1.  **Cache-Aside (Lazy Loading):** App checks cache -> Miss -> Read DB -> Update Cache. most common.
2.  **Read-Through:** App asks Cache -> Cache fetches from DB if miss.
3.  **Write-Through:** App writes to Cache -> Cache writes to DB (Safe but slow).
4.  **Write-Back:** App writes to Cache -> Cache writes to DB asynchronously (Fast but risk of data loss).

---

## 607. What is database scaling?

**Answer:**
1.  **Replication:** Master-Slave architecture. Master handles writes, Slaves handle reads.
2.  **Sharding:** Partitioning data across multiple databases (e.g., Users A-M on DB1, N-Z on DB2).
3.  **Federation:** Splitting tables by function (e.g., User DB, Order DB).

---

## 608. What is read-write separation?

**Answer:**
**Read-Write Separation** splits database traffic.
*   **Writes (INSERT/UPDATE/DELETE):** Go to **Master** node.
*   **Reads (SELECT):** Go to **Slave/Replica** nodes.
*   **Challenge:** Replication Lag (Slave might have stale data for a few ms).

---

## 609. What is queue-based architecture?

**Answer:**
Decoupling components using a Message Queue (Kafka/RabbitMQ).
*   **Scenario:** User uploads video -> **Frontend** pushes job to **Queue** -> **Worker** picks job and transcodes video.
*   **Benefit:** Frontend responds immediately ("Processing..."). Worker scales independently.

---

## 610. What is eventual consistency handling?

**Answer:**
How to deal with data that isn't consistent yet (in distributed systems).
1.  **Read-Your-Writes:** Ensure a user sees their own updates immediately (e.g., pin user to Master for 1 min after write).
2.  **Compensation:** If a background step fails (Saga), run a compensating transaction to undo previous steps.
3.  **Retry:** Idempotent retries for failed messages.

---

## 611. What is data partitioning?

**Answer:**
**Data Partitioning (Sharding)** splits a large dataset into smaller, manageable parts.
*   **Horizontal:** Split by rows (e.g., User ID 1-1000 in DB A, 1001-2000 in DB B).
*   **Vertical:** Split by columns (e.g., User Profile in DB A, User Photos in DB B).
*   **Methods:** Key-Based (Hash), Range-Based, Directory-Based.

---

## 612. What is consistent hashing?

**Answer:**
A technique to distribute keys across a dynamic set of nodes with minimal remapping.
*   **Circle:** Nodes are placed on a ring (0-360 degrees). Keys are hashed to the ring and assigned to the next clockwise node.
*   **Virtual Nodes:** Each physical node has multiple positions on the ring to ensure even distribution.
*   **Benefit:** Adding/Removing a node only affects its immediate neighbors.

---

## 613. What is distributed lock?

**Answer:**
Ensures that only one process across the entire distributed system can access a shared resource at a time.
*   **Tools:** specific tools like **Redis (Redlock)** or **Zookeeper**.
*   **Mechanism:** Acquire lock with TTL (Time To Live). If crash, lock expires automatically.

---

## 614. What is leader election?

**Answer:**
Process of designating a single node as the coordinator/master among a cluster of nodes.
*   **Why?** To avoid data conflicts (Split Brain) and coordinate tasks.
*   **Algorithms:** Paxos, Raft, Bully Algorithm.
*   **Tools:** Zookeeper (Ephemeral Nodes), Etcd.

---

## 615. What is quorum?

**Answer:**
**Quorum** is the minimum number of votes required to perform an operation (Read/Write) in a distributed system.
*   **Formula:** `N/2 + 1` (where N is total nodes).
*   **Example:** In a 5-node cluster, you need 3 successful writes to confirm a "Safe Write".

---

## 616. What is gossip protocol?

**Answer:**
A peer-to-peer communication protocol where nodes periodically share state information with random neighbors.
*   **Analogy:** Viral transmission of information.
*   **Use Case:** Cluster membership (Cassandra), Failure detection.

---

## 617. What is service discovery?

**Answer:**
Mechanism for services to find each other without hardcoding IPs.
1.  **Client-Side:** Client asks Registry (Eureka) for IP, then calls Service.
2.  **Server-Side:** Client calls Load Balancer (Nginx), LB asks Registry and forwards traffic.
*   **Tools:** Netflix Eureka, Consul, Zookeeper, K8s DNS.

---

## 618. What is circuit breaker pattern?

**Answer:**
Prevents an application from repeatedly trying to execute an operation that's likely to fail.
*   **States:**
    *   **Closed:** Requests pass through (Normal).
    *   **Open:** Requests fail immediately (Fast Fail) after threshold errors.
    *   **Half-Open:** Allow limited requests to test if backend is back up.
*   **Tools:** Resilience4j, Hystrix.

---

## 619. What is backpressure?

**Answer:**
A mechanism where a consumer signals the producer to slow down because it cannot keep up with the data rate.
*   **Reactive Streams:** `request(n)` method used to pull only `n` items.
*   **Without Backpressure:** Consumer buffer overflows -> OOM Crash.

---

## 620. What is retry strategy?

**Answer:**
Retrying failed operations to handle transient failures.
*   **Exponential Backoff:** Wait 1s, then 2s, then 4s...
*   **Jitter:** Add random noise to wait time to prevent "Thundering Herd" (all clients retrying at exact same time).
*   **Idempotency:** Ensure retries don't duplicate side effects.

---

## 621. Monitoring & observability in system design?

**Answer:**
**Observability** is how well you can understand the internal state of a system from its external outputs.
*   **Three Pillars:**
    1.  **Logs:** Application events ("User X logged in").
    2.  **Metrics:** Aggregated numbers (CPU usage, Request Count).
    3.  **Traces:** Request lifecycle across services (Zipkin/Jaeger).

---

## 622. How to handle failures?

**Answer:**
Assume everything will fail.
1.  **Fail Fast:** Don't wait for timeout if you know it will fail.
2.  **Fail Safe:** Return a default/fallback response instead of crashing.
3.  **Fail Over:** Switch to a backup server/DB.

---

## 623. How to design fault-tolerant system?

**Answer:**
A system that continues to operate (possibly at reduced level) when components fail.
*   **Redundancy:** Eliminate Single Points of Failure (SPOF) by adding backup nodes.
*   **Isolation:** Use Bulkhead pattern so one failing service doesn't crash others.
*   **Recovery:** Automated restarts (K8s) and data restoration from write-ahead logs.

---

## 624. What is SLA design?

**Answer:**
**Service Level Agreement (SLA):** Contract with users (e.g., 99.9% uptime).
*   **SLO (Objective):** Internal goal (e.g., 99.95%).
*   **SLI (Indicator):** Real metric measured (e.g., Actual Uptime = 99.92%).
*   **Design:** To meet high SLA, you need high redundancy and automatic failover.

---

## 625. What is high availability architecture?

**Answer:**
Architecture that ensures system is operational for a long period.
*   **Active-Active:** Traffic goes to both data centers. Instant failover. Complex data sync.
*   **Active-Passive:** Traffic goes to Primary. Secondary is standby. Slower failover (warm-up time).

---

## 626. What is replication strategy?

**Answer:**
Copying data to multiple machines for availability and durability.
1.  **Sync Replication:** Write to Master -> Write to Slave -> Ack Client. Safe but slow.
2.  **Async Replication:** Write to Master -> Ack Client -> Write to Slave. Fast but risk of data loss on crash.
3.  **Semi-Sync:** Write to Master -> Write to **one** Slave -> Ack.

---

## 627. How to reduce latency?

**Answer:**
1.  **CDN:** Move static content closer to user.
2.  **Caching:** Redis/Memcached.
3.  **Database Indexing:** Optimize queries.
4.  **Compression:** Gzip/Brotli payloads.
5.  **Protocol:** Use HTTP/2 or gRPC instead of HTTP/1.1.
6.  **Connection Pooling:** Reuse DB connections.

---

## 628. What is batching?

**Answer:**
Grouping multiple operations into a single unit of work.
*   **Use Case:** ETL jobs, Payroll processing, Report generation.
*   **Pros:** High throughput, efficient resource usage.
*   **Cons:** High latency (real-time is impossible).

---

## 629. What is streaming system?

**Answer:**
Processing data in real-time as it arrives.
*   **Tools:** Apache Kafka, Flink, Spark Streaming.
*   **Use Case:** Fraud detection, Live Dashboard, Log analysis.
*   **Pros:** Low latency.
*   **Cons:** Complex state management (handling late events).

---

## 630. What is event-driven architecture?

**Answer:**
Architecture where components communicate by producing and consuming events (decoupled).
*   **Producer:** Emits "OrderPlaced".
*   **Consumer:** Reacts (updates Inventory, sends Email).
*   **Broker:** Kafka/RabbitMQ mediates.
*   **Benefit:** Scalability, Decoupling, Async processing.

---

## 631. What are trade-offs in system design?

**Answer:**
There is no perfect design, only trade-offs.
*   **Consistency vs Availability:** (CAP Theorem).
*   **Latency vs Throughput:** Processing one by one (Low Latency) vs Batching (High Throughput).
*   **SQL vs NoSQL:** Structured/Joints vs Flexible/Scalable.
*   **Cost vs Performance:** SSD vs HDD, RAM vs Disk.

---

## 632. How to choose database?

**Answer:**
1.  **Structured Data + ACID?** -> RDBMS (PostgreSQL/MySQL).
2.  **Unstructured/JSON?** -> Document DB (MongoDB).
3.  **Key-Value / Caching?** -> Redis/DynamoDB.
4.  **High Write Throughput (Logs/IoT)?** -> Wide Column (Cassandra).
5.  **Graph Relationships?** -> Neo4j.

---

## 633. How to estimate capacity?

**Answer:**
Back-of-the-envelope calculations to size the system.
1.  **Traffic:** DAU (Daily Active Users), Reads/sec, Writes/sec.
2.  **Storage:** Data generated per user per day * Retention Period.
3.  **Bandwidth:** Inbound/Outbound network traffic.
4.  **Memory:** Cache size (e.g., 20% of hot data).

---

## 634. What is traffic estimation?

**Answer:**
Example: 10M DAU.
*   Each user does 5 requests/day.
*   Total Requests = 50M/day.
*   Seconds in day ≈ 86,400 (round to 100,000 for math).
*   **QPS (Queries Per Second)** = 50,000,000 / 100,000 = **500 QPS**.
*   **Peak QPS:** Usually 2x-5x average => 2,500 QPS.

---

## 635. What is storage estimation?

**Answer:**
Example: Instagram-like app.
*   New Photos: 10 QPS (Writes).
*   Size: 1 MB per photo.
*   Total per second: 10 MB/s.
*   Total per day: 10 MB * 86,400 ≈ **860 GB/day**.
*   Total for 10 years: 860 GB * 365 * 10 ≈ **3 PB (Petabytes)**.

---

## 636. How to design analytics system?

**Answer:**
*   **Ingestion:** Kafka (high throughput).
*   **Processing:** Spark Streaming / Flink (Real-time aggregation).
*   **Storage:** Data Lake (S3 - Raw), Data Warehouse (Snowflake/Redshift - Structured).
*   **Query:** Presto / Athena / ClickHouse (OLAP).

---

## 637. What is OLTP vs OLAP?

**Answer:**
*   **OLTP (Online Transaction Processing):**
    *   Row-oriented (MySQL/Postgres).
    *   Fast reads/writes for user-facing apps.
    *   Unit: Single Transaction.
*   **OLAP (Online Analytical Processing):**
    *   Column-oriented (Redshift/BigQuery).
    *   Complex queries/aggregations for BI/Reporting.
    *   Unit: Batch Analysis.

---

## 638. What is data pipeline?

**Answer:**
A set of automated processes that move data from source to destination.
*   **EtL (Extract, Transform, Load):** Transform before loading (Legacy/Warehouse).
*   **ELT (Extract, Load, Transform):** Load raw data first, then transform (Modern/Data Lake).
*   **Tools:** Apache Airflow (Orchestration).

---

## 639. What is data warehouse?

**Answer:**
A central repository of integrated data from one or more disparate sources, structured for query and analysis.
*   **Schema-on-Write:** Structure defined before data entry.
*   **Examples:** Snowflake, AWS Redshift, Google BigQuery.

---

## 640. What is data lake?

**Answer:**
A centralized repository that allows you to store all your structured and unstructured data at any scale.
*   **Schema-on-Read:** Structure defined when querying.
*   **Examples:** AWS S3, Azure Data Lake, Hadoop HDFS.

---

## 641. Security in system design?

**Answer:**
**Security** must be designed from the start ("Security by Design"), not added later.
*   **Authentication (AuthN):** Verify identity (Who are you?).
*   **Authorization (AuthZ):** Verify permissions (What can you do?).
*   **Data Protection:** Encryption at Rest (AES-256) and in Transit (TLS 1.3).
*   **Audit Logic:** Log who did what and when.

---

## 642. Rate limiting strategies?

**Answer:**
Techniques to control the rate of traffic sent or received.
1.  **User-Based:** Limit by User ID / API Key.
2.  **IP-Based:** Limit by IP address (can block NAT users).
3.  **Endpoint-Based:** Limit specific expensive APIs (`/report/generate`).
4.  **Geographic:** Limit traffic from specific regions.

---

## 643. Token bucket vs leaky bucket?

**Answer:**
*   **Token Bucket:**
    *   Tokens added at constant rate. Request consumes a token.
    *   **Pro:** Allows bursts of traffic (if bucket is full).
*   **Leaky Bucket:**
    *   Requests enter bucket. Leak (process) at constant rate.
    *   **Pro:** Smooths out traffic (constant outflow). No bursts.

---

## 644. What is zero trust architecture?

**Answer:**
A security model that assumes **no one** inside or outside the network is trusted by default.
*   **Principle:** "Never trust, always verify."
*   **Implementation:** mTLS between microservices, strict Identity verification for every request, no implicit trust based on network location (VPN).

---

## 645. What is OAuth2?

**Answer:**
**OAuth 2.0** is an authorization framework that enables apps to obtain limited access to user accounts on an HTTP service.
*   **Roles:** Resource Owner (User), Client (App), Authorization Server (Google/Okta), Resource Server (API).
*   **Flows:** Authorization Code (Server-side apps), Client Credentials (Service-to-Service), Implicit (Legacy).

---

## 646. What is JWT?

**Answer:**
**JSON Web Token (JWT)** is a compact, URL-safe means of representing claims to be transferred between two parties.
*   **Structure:** `Header.Payload.Signature`.
*   **Stateless:** Server doesn't store session; validates signature using secret/public key.
*   **Cons:** Can't revoke easily (needs blacklist/short expiry).

---

## 647. What is RBAC?

**Answer:**
**Role-Based Access Control (RBAC):** Permissions are assigned to **Roles** (Admin, Editor, Viewer), and Roles are assigned to **Users**.
*   **Simple:** Easy to manage for standard org structures.
*   **Example:** "Admins can delete users".

---

## 648. What is ABAC?

**Answer:**
**Attribute-Based Access Control (ABAC):** Permissions are granted based on **Attributes** (User, Resource, Environment).
*   **Dynamic:** "User can view document IF user.dept == doc.dept AND time is between 9am-5pm."
*   **Complex:** More granular than RBAC but harder to implement.

---

## 649. What is API throttling?

**Answer:**
**Throttling** is the intentional slowing down of a service to prevent overuse.
*   **Difference from Rate Limiting:**
    *   **Rate Limiting:** Rejects request (429) if limit exceeded.
    *   **Throttling:** Queues user requests or slows down response to smooth usage.

---

## 650. What is graceful degradation?

**Answer:**
The ability of a system to maintain limited functionality even when a large portion of it is destroyed or inoperative.
*   **Example:** If Recommendation Service fails, e-commerce site shows "Best Sellers" (static list) instead of "Recommended for You" (dynamic), rather than crashing the whole homepage.
