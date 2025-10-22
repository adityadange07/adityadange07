Here are the **Top 50 Apache Kafka Interview Questions and Answers** tailored for professionals with **5 years of experience**, focusing on core architecture, real-world usage, scalability, tuning, security, and advanced Kafka ecosystem components.

---

## ✅ Top 50 Kafka Interview Questions (5 Years Experience)

---

### 🔹 **Basics & Architecture**

1. **What is Apache Kafka?**  
   A distributed, fault-tolerant event streaming platform used for high-throughput real-time data pipelines and applications.

---

2. **What are the main components of Kafka architecture?**
    - **Producer**
    - **Consumer**
    - **Broker**
    - **Topic**
    - **Partition**
    - **Zookeeper** (in older versions) or **KRaft** (newer versions)

---

3. **What is a Kafka topic?**  
   A category to which records are sent by producers and consumed by consumers.

---

4. **What is a Kafka partition?**  
   Topics are split into partitions to allow parallelism and scalability.

---

5. **What is a Kafka broker?**  
   A Kafka server that stores and serves data (messages) to consumers.

---

6. **What is a Kafka cluster?**  
   A group of Kafka brokers working together.

---

7. **How does Kafka achieve fault tolerance?**  
   Through replication of partitions across multiple brokers.

---

8. **What is the role of ZooKeeper in Kafka?**
    - Manages metadata
    - Tracks broker status
    - Handles leader election (Kafka 2.x and below)

---

9. **What is Kafka KRaft mode?**  
   Kafka Raft (KRaft) replaces ZooKeeper in newer Kafka versions for metadata management and controller logic.

---

10. **How is data stored in Kafka?**  
    As logs on disk in a sequential, append-only format.

---

### 🔹 **Producers & Consumers**

11. **What is a Kafka Producer?**  
    A client that writes data (messages) to Kafka topics.

---

12. **What is a Kafka Consumer?**  
    A client that reads messages from Kafka topics.

---

13. **What is a Consumer Group?**  
    A group of consumers working together to consume data from a topic in parallel, each partition assigned to one consumer.

---

14. **How does Kafka ensure message ordering?**  
    Messages are ordered **within a partition**, not across partitions.

---

15. **How can producers ensure messages go to a specific partition?**  
    By specifying a key. Kafka uses key hashing to map to a partition.

---

16. **What are producer acks?**  
    Controls durability guarantees:
- `acks=0`: No ack
- `acks=1`: Leader ack
- `acks=all`: All replicas ack

---

17. **What are delivery semantics in Kafka?**
- **At most once**
- **At least once**
- **Exactly once (EOS)**

---

18. **How does Kafka achieve exactly-once semantics?**  
    Using **idempotent producers** and **transactional APIs**.

---

19. **How does offset management work in Kafka?**  
    Offsets track the position of consumers. They can be stored in Kafka (`__consumer_offsets`) or manually managed.

---

20. **How do you reset offsets?**  
    Using `kafka-consumer-groups` CLI tool with the `--reset-offsets` flag.

---

### 🔹 **Performance & Scaling**

21. **How to increase throughput in Kafka?**
- Increase partitions
- Use compression (`gzip`, `snappy`, etc.)
- Batch messages
- Optimize replication factor

---

22. **How does Kafka handle backpressure?**  
    Kafka itself does not apply backpressure but can be handled at the producer/consumer level using flow control and retries.

---

23. **What is log compaction in Kafka?**  
    A cleanup policy that retains only the **latest message per key** in a topic.

---

24. **Difference between delete and compact cleanup policies?**
- **delete**: Old messages deleted after retention time
- **compact**: Latest key-value pairs retained indefinitely

---

25. **What is Kafka retention policy?**  
    Controls how long Kafka retains messages:
- Time-based (`retention.ms`)
- Size-based (`retention.bytes`)

---

26. **How to handle message reprocessing?**
- Reset offsets
- Use a separate reprocessing topic
- Replay using retained logs

---

27. **What happens when a consumer fails?**  
    Kafka reassigns partitions to remaining consumers in the group.

---

28. **How to ensure high availability in Kafka?**
- Use replication
- Multiple brokers
- ISR (In-Sync Replica) mechanism

---

29. **What are ISR and OSR in Kafka?**
- **ISR (In-Sync Replicas)**: Up-to-date replicas
- **OSR (Out-of-Sync Replicas)**: Lagging behind

---

30. **How does Kafka handle message duplication?**  
    By enabling **idempotence** in producers or using **deduplication logic** on the consumer side.

---

### 🔹 **Kafka Ecosystem Tools**

31. **What is Kafka Connect?**  
    A framework for connecting Kafka with external systems like DBs, Elasticsearch using prebuilt connectors.

---

32. **What is Kafka Streams?**  
    A client library for building stream processing applications using Kafka topics.

---

33. **Difference between Kafka Streams and Kafka Consumer API?**
- Streams: High-level abstraction with state, joins, windows
- Consumer API: Low-level message consumption

---

34. **What is KSQL (ksqldb)?**  
    A SQL-like interface to query and process Kafka topics.

---

35. **What are internal Kafka topics?**
- `__consumer_offsets`: Stores consumer offsets
- `__transaction_state`: Transactional state data

---

36. **What is schema registry in Kafka?**  
    Stores and validates schemas (usually Avro/JSON/Protobuf) used by producers and consumers.

---

37. **How does Kafka ensure schema compatibility?**  
    Via schema evolution rules: `BACKWARD`, `FORWARD`, `FULL`, `NONE`.

---

38. **What is watermarking in Kafka Streams?**  
    Technique used in windowed operations to manage out-of-order events.

---

39. **What is repartitioning in Kafka Streams?**  
    Process of redistributing records based on key to ensure correct stateful operations.

---

40. **What are changelogs and state stores in Kafka Streams?**
- **State store**: Local storage
- **Changelog topic**: Backups state for fault tolerance

---

### 🔹 **Security & Administration**

41. **What security features does Kafka provide?**
- TLS encryption
- SASL/SSL authentication
- ACL-based authorization

---

42. **How to create a Kafka topic manually?**
   ```bash
   kafka-topics.sh --create --topic my-topic --bootstrap-server localhost:9092 --partitions 3 --replication-factor 2
   ```

---

43. **How to monitor Kafka?**  
    Tools like Prometheus + Grafana, Confluent Control Center, LinkedIn Burrow.

---

44. **What are common Kafka metrics to monitor?**
- Under-replicated partitions
- Consumer lag
- Request latency
- Throughput

---

45. **How does Kafka guarantee durability?**
- Messages written to disk
- Replication to multiple brokers
- `acks=all` for producers

---

46. **How do you tune Kafka for low latency?**
- Reduce `linger.ms`
- Smaller batch size
- Increase partitions

---

47. **Can Kafka be used for request-response communication?**  
    Yes, using separate response topics or correlation IDs for RPC-like behavior.

---

48. **How is Kafka different from traditional message brokers (like RabbitMQ)?**  
    Kafka is distributed, log-based, optimized for high throughput and long-term storage.

---

49. **What is Kafka’s role in a microservices architecture?**
- Event sourcing
- Decoupling producers/consumers
- Asynchronous communication

---

50. **What are common Kafka deployment models?**
- Self-hosted Kafka cluster
- Kafka on Kubernetes
- Confluent Cloud
- AWS MSK (Managed Kafka)

---

Would you like this as a **PDF**, or shall I help you with **Kafka + Spring Boot integration questions**, or **real-time scenario-based Kafka case studies** next?