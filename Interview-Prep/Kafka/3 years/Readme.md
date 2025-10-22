Here are the **Top 50 Apache Kafka Interview Questions and Answers**, specially designed for professionals with **3 years of experience**. These cover **core Kafka concepts**, **architecture**, **real-world usage**, and **Kafka in microservices & distributed systems**.

---

## ✅ Top 50 Kafka Interview Questions (3 Years Experience)

---

### 🔹 **Kafka Basics**

1. **What is Apache Kafka?**  
   Kafka is a distributed streaming platform used for building real-time data pipelines and streaming apps.

---

2. **What are the main components of Kafka?**
    - **Producer**
    - **Consumer**
    - **Broker**
    - **Topic**
    - **Zookeeper (or KRaft)**
    - **Partition**
    - **Cluster**

---

3. **What is a Kafka topic?**  
   A topic is a category/feed name to which records are sent by producers and read by consumers.

---

4. **What is a Kafka partition?**  
   Topics are split into partitions to allow parallel processing and scalability.

---

5. **What is the role of Kafka broker?**  
   Kafka broker receives messages from producers and serves them to consumers.

---

6. **What is a Kafka producer?**  
   An application that sends (publishes) messages to a Kafka topic.

---

7. **What is a Kafka consumer?**  
   An application that reads messages from one or more Kafka topics.

---

8. **What is Kafka cluster?**  
   A group of Kafka brokers working together to handle data ingestion and distribution.

---

9. **What is the role of Zookeeper in Kafka?**  
   Manages broker metadata, leader election, and configuration. (Note: Kafka 2.8+ supports KRaft mode to remove Zookeeper.)

---

10. **What is an offset in Kafka?**  
    A unique ID assigned to each record in a partition, used to track the consumption progress.

---

### 🔹 **Kafka Internals**

11. **What is a Consumer Group?**  
    A group of consumers working together to consume messages from a topic without duplication.

---

12. **What happens if a consumer fails in a group?**  
    Kafka rebalances the partitions among remaining consumers in the group.

---

13. **How does Kafka achieve fault tolerance?**  
    Through replication of partitions across brokers.

---

14. **What is Kafka replication factor?**  
    Number of copies of a partition maintained across brokers for durability.

---

15. **What is ISR (In-Sync Replica)?**  
    List of replicas that are fully synced with the leader and eligible to become leader in case of failure.

---

16. **What is a Kafka controller?**  
    One broker that is responsible for cluster-level decisions (e.g., leader election).

---

17. **How is a leader selected in Kafka?**  
    Kafka elects one replica as the leader of a partition. Others are followers.

---

18. **What is Kafka retention policy?**  
    Specifies how long messages are kept in Kafka. Can be based on time or size.

---

19. **What are Kafka logs?**  
    Kafka stores records in a log file on disk for each partition.

---

20. **What is log compaction?**  
    Kafka can retain only the latest value for each key to save space (used in changelog topics).

---

### 🔹 **Producer & Consumer Mechanics**

21. **How does a Kafka producer send messages?**  
    Producers send messages to a specified topic (and optionally a partition), using Kafka APIs.

---

22. **What is message key in Kafka?**  
    It determines the partition to which a message is sent.

---

23. **What is acks in Kafka producer config?**  
    Defines acknowledgment behavior:
- `0`: Fire-and-forget
- `1`: Wait for leader
- `all`: Wait for all ISR

---

24. **How does Kafka ensure exactly-once delivery?**  
    Using idempotent producers and transactional APIs (since Kafka 0.11+).

---

25. **How does a consumer know where to resume?**  
    Consumers store offsets in Kafka (or Zookeeper). Offsets can be auto-committed or manually controlled.

---

26. **What is auto.offset.reset?**  
    Defines what to do when no offset is found:
- `latest` (default)
- `earliest`
- `none`

---

27. **How can you manually commit offsets?**  
    Use Kafka consumer APIs:  
    `consumer.commitSync()` or `consumer.commitAsync()`

---

28. **What is a rebalance in Kafka?**  
    Redistribution of partitions among consumers when group membership changes.

---

29. **What are idempotent producers in Kafka?**  
    Producers that can safely retry sends without duplicating messages.

---

30. **What is Kafka Streams?**  
    A Java library for building stream processing applications on top of Kafka.

---

### 🔹 **Kafka in Practice**

31. **How do you monitor Kafka?**
- JMX metrics
- Tools like Prometheus, Grafana, Confluent Control Center

---

32. **How do you secure Kafka?**
- SSL for encryption
- SASL for authentication
- ACLs for authorization

---

33. **What is the difference between Kafka and RabbitMQ?**
- Kafka is distributed, high throughput, append-only log
- RabbitMQ is message queue-based with different delivery semantics

---

34. **How is Kafka different from traditional messaging systems?**
- Distributed
- Persistent
- Pull-based
- High throughput

---

35. **How do you handle message ordering in Kafka?**  
    Kafka guarantees order **within a partition**, not across partitions.

---

36. **How can you increase throughput in Kafka?**
- More partitions
- Batch sending
- Compress messages
- Tune producer configs

---

37. **How can you implement dead letter queues in Kafka?**  
    Send failed messages to a separate topic for later inspection or reprocessing.

---

38. **What compression types does Kafka support?**
- `none`
- `gzip`
- `snappy`
- `lz4`
- `zstd`

---

39. **What happens if Kafka broker goes down?**  
    Leader election occurs, and followers replicate messages. No data loss if replication is configured.

---

40. **How to handle backpressure in Kafka consumers?**  
    Tune max.poll.interval.ms and consumer fetch sizes, use flow control mechanisms.

---

### 🔹 **Kafka in Microservices**

41. **Why use Kafka in microservices architecture?**  
    For asynchronous communication, decoupling services, and real-time data streams.

---

42. **How to ensure reliable messaging in microservices with Kafka?**
- Use replication
- Enable retries
- Monitor offsets
- Implement dead letter queues

---

43. **What is the role of schema registry?**  
    Ensures producer and consumer use compatible data formats (e.g., with Avro or Protobuf).

---

44. **What is the difference between Kafka Streams and Kafka Connect?**
- Kafka Streams: For processing and transforming data
- Kafka Connect: For integrating with external systems (DBs, files)

---

45. **What is Kafka Connect?**  
    A tool for scalable and reliable data import/export using connectors.

---

46. **How do you scale Kafka consumers?**  
    Add more consumers to a group (up to the number of partitions in the topic).

---

47. **What is a transactional producer in Kafka?**  
    A producer that supports atomic writes to multiple topics/partitions.

---

48. **What happens if a consumer reads faster than the producer?**  
    It reads the latest available records and waits (no harm).

---

49. **How do you achieve high availability in Kafka?**
- Replication
- Multiple brokers
- Proper partitioning
- Failover handling

---

50. **How do you tune Kafka for performance?**
- Optimize batch size
- Adjust linger.ms
- Tune buffer.memory
- Use compression
- Partition wisely

---

Would you like this in a **PDF format**, or should I proceed with **Spring Kafka**, **Kafka + Microservices**, or **Kafka + Real-time System Design** next?