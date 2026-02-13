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
