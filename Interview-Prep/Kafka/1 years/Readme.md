Here are the **Top 50 Apache Kafka Interview Questions and Answers** tailored for **1 year of experience**. This set includes basic and foundational topics related to Kafka architecture, components, producer-consumer behavior, and configuration, ideal for junior/mid-level roles.

---

## ✅ Top 50 Kafka Interview Questions (1 Year Experience)

---

### 🔹 **Basic Kafka Concepts**

1. **What is Apache Kafka?**  
   A distributed, fault-tolerant, high-throughput messaging system for building real-time data pipelines and streaming apps.

---

2. **What are the main components of Kafka?**
    - Producer
    - Consumer
    - Broker
    - Topic
    - Partition
    - Zookeeper (in older versions)

---

3. **What is a Kafka topic?**  
   A category or feed name to which records are sent by producers and from which consumers receive records.

---

4. **What is a Kafka partition?**  
   A topic is split into partitions to allow parallel processing and scalability.

---

5. **What is a Kafka broker?**  
   A Kafka server that stores data and serves clients (producers/consumers).

---

6. **What is the role of Zookeeper in Kafka?**  
   Manages Kafka cluster metadata, leader election, and configuration synchronization. (Being replaced by KRaft mode)

---

7. **What is a Kafka producer?**  
   A client that publishes data to Kafka topics.

---

8. **What is a Kafka consumer?**  
   A client that reads data from Kafka topics.

---

9. **What is a consumer group in Kafka?**  
   A group of consumers working together to consume a topic. Each partition is assigned to one consumer in the group.

---

10. **How does Kafka ensure fault tolerance?**
- Data replication across brokers
- Automatic leader election
- Retention policies

---

### 🔹 **Message Handling and Internals**

11. **What is message offset in Kafka?**  
    A unique identifier for each message within a partition.

---

12. **Are Kafka messages deleted after being consumed?**  
    No. Messages are retained based on time or size policies, not consumption status.

---

13. **How does Kafka achieve high throughput?**
- Batching of messages
- Zero-copy architecture
- Asynchronous writes

---

14. **What is Kafka retention policy?**  
    Controls how long data is stored (based on time or size). Configurable per topic.

---

15. **What is replication factor in Kafka?**  
    Number of copies of each partition across brokers for fault tolerance.

---

16. **What is the role of the leader and follower in Kafka?**
- **Leader**: Handles all read/write for the partition
- **Follower**: Replicates data and takes over if leader fails

---

17. **What happens if a consumer fails?**  
    Kafka reassigns the partitions to other consumers in the same group.

---

18. **What happens if a broker fails?**  
    Partition leadership is reassigned to a follower replica.

---

19. **Can a topic have more partitions than brokers?**  
    Yes. Partitions are evenly distributed among brokers.

---

20. **Can a consumer consume data from multiple topics?**  
    Yes, a consumer can subscribe to one or more topics.

---

### 🔹 **Configuration and Commands**

21. **How do you create a topic in Kafka?**  
    Using the CLI:
   ```bash
   kafka-topics.sh --create --topic my-topic --bootstrap-server localhost:9092 --partitions 3 --replication-factor 2
   ```

---

22. **How do you produce data to Kafka?**
   ```bash
   kafka-console-producer.sh --topic my-topic --bootstrap-server localhost:9092
   ```

---

23. **How do you consume data from Kafka?**
   ```bash
   kafka-console-consumer.sh --topic my-topic --from-beginning --bootstrap-server localhost:9092
   ```

---

24. **What is the `acks` setting in Kafka producer?**
- `0`: Fire and forget
- `1`: Leader acknowledgment
- `all`: Wait for all replicas to acknowledge (strongest guarantee)

---

25. **What does `auto.offset.reset` do?**  
    Defines behavior when there's no committed offset:
- `earliest`: Read from beginning
- `latest`: Read from new messages only

---

26. **What is the default retention period in Kafka?**  
    7 days (`log.retention.hours = 168`)

---

27. **How can you list all topics?**
   ```bash
   kafka-topics.sh --list --bootstrap-server localhost:9092
   ```

---

28. **How do you increase partitions for a topic?**
   ```bash
   kafka-topics.sh --alter --topic my-topic --partitions 5 --bootstrap-server localhost:9092
   ```

---

29. **Can you decrease the number of partitions for a topic?**  
    No. Kafka does not support decreasing partitions after creation.

---

30. **What happens when the same consumer group has multiple consumers?**  
    Kafka distributes partitions among consumers. Each partition goes to one consumer.

---

### 🔹 **Real-time Use & Troubleshooting**

31. **What is lag in Kafka?**  
    The difference between the latest offset and the committed offset of a consumer.

---

32. **How can you monitor Kafka consumer lag?**  
    Use tools like Kafka Manager, Burrow, or JMX metrics.

---

33. **What are dead-letter topics?**  
    Topics where messages are sent if they fail processing after retries.

---

34. **What is the difference between Kafka and traditional message brokers like RabbitMQ?**
- Kafka is distributed, log-based, and supports large-scale throughput.
- RabbitMQ uses queues with message acknowledgement and routing.

---

35. **Can Kafka guarantee message ordering?**  
    Yes, per partition. Messages in the same partition maintain order.

---

36. **What is the Kafka commit mechanism?**  
    It’s the process of storing the last successfully processed offset.

---

37. **Difference between manual and auto commit?**
- **Auto commit**: Kafka commits offsets automatically
- **Manual commit**: Gives more control and is safer for critical applications

---

38. **What is idempotence in Kafka producer?**  
    Ensures that retrying message sends won’t result in duplicates.

---

39. **What is log compaction in Kafka?**  
    Keeps the latest value for each key in a topic, removing older records with the same key.

---

40. **What is Kafka Streams?**  
    A Java library for processing and transforming data in Kafka.

---

### 🔹 **Basic Development Questions**

41. **How do you implement a Kafka producer in Java?**  
    Using `KafkaProducer` class and `ProducerRecord`.

---

42. **How do you implement a Kafka consumer in Java?**  
    Using `KafkaConsumer` class and subscribing to a topic.

---

43. **Can a Kafka producer be a consumer too?**  
    Yes, an application can produce and consume messages simultaneously.

---

44. **What is serialization in Kafka?**  
    Converts data into byte format before sending it to Kafka. Common types: StringSerializer, JsonSerializer, Avro.

---

45. **How can you secure a Kafka cluster?**
- TLS for encryption
- SASL for authentication
- ACLs for authorization

---

46. **What is Kafka Connect?**  
    A framework to connect Kafka with external systems (DBs, files, etc.) using pre-built connectors.

---

47. **What is schema registry in Kafka?**  
    Stores and validates message schemas (often used with Avro/Protobuf).

---

48. **How does Kafka handle backpressure?**  
    Kafka itself doesn’t apply backpressure. Producers can block or buffer depending on `buffer.memory` and `max.block.ms`.

---

49. **How do you test Kafka locally?**  
    Using tools like Testcontainers, Embedded Kafka, or Confluent Platform.

---

50. **What are Kafka use cases?**
- Real-time analytics
- Log aggregation
- Event sourcing
- Data pipeline streaming

---

Would you like these in **PDF format**, or should I continue with **Spring Boot + Kafka**, or move on to **Kafka advanced questions for senior roles**?