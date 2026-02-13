## 371. What is messaging system?

**Answer:**
A **Messaging System** allows different software systems to communicate and exchange data (messages) asynchronously.
*   **Role:** Decouples the sender (Producer) from the receiver (Consumer).
*   **Models:**
    1.  **Point-to-Point (Queue):** Message is consumed by exactly one consumer (e.g., RabbitMQ Queue).
    2.  **Publish-Subscribe (Topic):** Message is broadcast to all active subscribers (e.g., Kafka Topic).

---

## 372. Kafka vs RabbitMQ?

**Answer:**

| Feature | Kafka | RabbitMQ |
| :--- | :--- | :--- |
| **Model** | Distributed Streaming Platform (Log-based). | Message Broker (Queue-based). |
| **Throughput** | Extremely High (Millions/sec). | High (Thousands/sec). |
| **Persistence** | Durable (Stores messages for days/weeks). | Transient (Deletes after consumption). |
| **Consumption** | Pull-based (Consumer polls). | Push-based (Broker pushes). |
| **Use Case** | Event sourcing, Stream processing, Logs. | Complex routing, Real-time messaging. |

---

## 373. What is topic in Kafka?

**Answer:**
A **Topic** is a category or feed name to which records are stored and published.
*   **Analogy:** A folder in a filesystem or a table in a database.
*   **Structure:** Topics are partitioned and replicated.
*   **Retention:** Messages are stored for a configurable period (e.g., 7 days) regardless of whether they have been consumed.

---

## 374. What is partition?

**Answer:**
A **Partition** is an ordered, immutable sequence of records that is continually appended to—a structured commit log.
*   **Purpose:** Scalability. A topic can be split into multiple partitions hosted on different brokers.
*   **Ordering:** Guaranteed *within* a partition, but not across the entire topic.

---

## 375. What is offset?

**Answer:**
An **Offset** is a unique sequential integer ID assigned to each record within a partition.
*   **Purpose:** It uniquely identifies a message in a partition.
*   **Consumer Tracking:** Consumers track their progress by storing the offset of the last consumed message.

---

## 376. What is consumer group?

**Answer:**
A **Consumer Group** is a set of consumers that cooperate to consume data from a topic.
*   **Mechanism:** Kafka ensures that each partition is consumed by **exactly one** consumer within the group.
*   **Scaling:** To scale reading, add more consumers to the group (up to the number of partitions).

---

## 377. What is producer acknowledgement?

**Answer:**
**ACKS** (Acknowledgements) determine when the producer considers a request complete.
*   `acks=0`: Producer sends and forgets (Low latency, data loss risk).
*   `acks=1`: Leader receives and writes to local log (Default).
*   `acks=all`: Leader and all ISR (In-Sync Replicas) acknowledge (Highest durability).

---

## 378. What is ISR?

**Answer:**
**ISR (In-Sync Replica)** is a set of replica brokers that are caught up with the leader partition.
*   **Role:** Only members of the ISR are eligible to be elected as a new leader if the current leader fails.
*   **Lag:** If a replica lags too far behind, it is removed from the ISR.

---

## 379. What is replication factor?

**Answer:**
**Replication Factor** determines how many copies of a partition are stored across the cluster.
*   **Default:** Typically 3 (1 Leader + 2 Followers).
*   **Benefit:** Fault tolerance. If N-1 brokers fail, the data is still available.

---

## 380. What is exactly-once semantics?

**Answer:**
**Exactly-Once Semantics (EOS)** guarantees that each message is delivered and processed exactly once, even in the event of failures.
*   **Kafka:** Achieved using **Idempotent Producer** (`enable.idempotence=true`) and **Transactional API** (atomic write across multi-partitions).
*   **Difficulty:** Standard messaging is usually "At-least-once".

---

## 381. What is message ordering?

**Answer:**
**Message Ordering** ensures that messages are consumed in the exact order they were produced.
*   **Kafka:** Order is guaranteed **only within a Partition**, not across the entire topic. To guarantee total order, use a single partition (sacrifices scalability).
*   **RabbitMQ:** Order is guaranteed for a single queue consumer.

---

## 382. What is Kafka retention policy?

**Answer:**
**Retention Policy** determines how long Kafka keeps messages before deleting them.
*   **Time-based:** `log.retention.hours` (e.g., 168 hours = 7 days).
*   **Size-based:** `log.retention.bytes` (e.g., 1GB).
*   **Compaction:** Instead of deleting, keep only the **latest value** for each key (useful for restoring state).

---

## 383. What is dead letter queue?

**Answer:**
A **Dead Letter Queue (DLQ)** is a service-level queue where messages are sent if they cannot be processed successfully after a maximum number of retries.
*   **Purpose:** Allows developers to investigate "poison pill" messages (malformed data) without blocking the main processing queue.
*   **Process:** Alerts are usually set up on the DLQ to notify the team.

---

## 384. What is RabbitMQ exchange types?

**Answer:**
**Exchanges** route messages to queues based on rules.
1.  **Direct:** Routes to queues with an exact matching **binding key**.
2.  **Fanout:** Broadcasts to **all** bound queues (ignores keys).
3.  **Topic:** Routes based on pattern matching (wildcards `*` like `logs.*.error`).
4.  **Headers:** Routes based on message headers instead of routing keys.

---

## 385. What is at-least-once vs at-most-once delivery?

**Answer:**
*   **At-most-once:** Fire and forget. Message might be lost, but never duplicated. (Fastest).
*   **At-least-once:** Message is guaranteed to be delivered, but might be duplicated.
    *   *Requirement:* Consumer must be **Idempotent** (handling duplicates safely).
*   **Exactly-once:** Guarantees no loss and no duplicates. Hardest to achieve (requires transactional support like Kafka Streams).
