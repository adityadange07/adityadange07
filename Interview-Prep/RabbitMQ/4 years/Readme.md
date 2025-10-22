Here are the **Top 50 RabbitMQ Interview Questions and Answers** tailored for someone with **4 years of experience**. These cover intermediate to advanced concepts including real-world architecture, reliability, performance tuning, message patterns, and Spring Boot integration.

---

## 🧠 Top 50 RabbitMQ Interview Questions (For 4 Years Experience)

---

### 🔸 **1–10: Core Concepts & Architecture**

1. **What is RabbitMQ and what protocol does it use?**  
   RabbitMQ is an open-source message broker that uses the AMQP (Advanced Message Queuing Protocol).

2. **What are the main components of RabbitMQ architecture?**  
   Producer, Exchange, Queue, Binding, Routing Key, Consumer.

3. **What is the purpose of an exchange in RabbitMQ?**  
   Exchanges route messages to queues using bindings and routing keys.

4. **What types of exchanges are supported in RabbitMQ?**  
   Direct, Fanout, Topic, Headers.

5. **How does a direct exchange work?**  
   It routes messages to queues where the routing key matches exactly.

6. **How does a topic exchange work?**  
   It routes messages to queues based on pattern matching in routing keys using wildcards (`*`, `#`).

7. **How does a fanout exchange work?**  
   It broadcasts messages to all queues bound to it, regardless of routing key.

8. **How does a headers exchange work?**  
   It routes messages based on header values instead of routing keys.

9. **What is the difference between a queue and an exchange?**  
   An exchange routes messages, a queue stores and holds them for consumers.

10. **Can one queue be bound to multiple exchanges?**  
    Yes, a queue can be bound to multiple exchanges with different bindings.

---

### 🔸 **11–20: Message Durability & Acknowledgements**

11. **What is a durable queue?**  
    A queue that survives a broker restart.

12. **What is a persistent message?**  
    A message that is stored on disk, not just in memory.

13. **How do you ensure a message is never lost?**  
    Use durable queues + persistent messages + manual acks.

14. **What is message acknowledgment (ack)?**  
    Confirmation from the consumer that a message has been processed.

15. **What happens if a message is not acknowledged?**  
    It can be redelivered or dead-lettered, depending on configuration.

16. **Difference between auto-ack and manual-ack?**
- Auto-ack: Acknowledges upon receipt.
- Manual-ack: Explicit ack after successful processing.

17. **What is a dead-letter exchange (DLX)?**  
    An exchange to which messages go when they are rejected or expire.

18. **What conditions cause a message to be dead-lettered?**  
    TTL expiration, queue overflow, message rejection with `requeue=false`.

19. **How to configure a DLQ (Dead Letter Queue)?**  
    Add `x-dead-letter-exchange` and `x-dead-letter-routing-key` to the original queue.

20. **What is the impact of unacked messages on RabbitMQ memory?**  
    They stay in memory and can lead to memory pressure if not cleared.

---

### 🔸 **21–30: Performance & Optimization**

21. **What is prefetch count and why is it important?**  
    It limits the number of unacknowledged messages per consumer to balance load.

22. **What is a lazy queue?**  
    A queue that stores messages directly to disk to reduce RAM usage.

23. **How to avoid memory overload in RabbitMQ?**  
    Use lazy queues, limit prefetch, monitor queues, and configure flow control.

24. **What is flow control in RabbitMQ?**  
    Mechanism to stop producers when resources (RAM, disk) are low.

25. **What is a priority queue?**  
    Queue that delivers higher-priority messages before lower-priority ones.

26. **How do you scale RabbitMQ consumers?**  
    Add more instances of consumers using the competing consumer pattern.

27. **What is message TTL (Time To Live)?**  
    The time after which a message expires and can be dead-lettered or discarded.

28. **Can you limit the size of a queue?**  
    Yes, using `x-max-length` or `x-max-length-bytes` arguments.

29. **What is the impact of using large messages?**  
    Can cause memory pressure and reduce throughput. Chunking or compression is advised.

30. **What is the maximum size of a message in RabbitMQ?**  
    There’s no strict limit, but very large messages (hundreds of MBs) are discouraged.

---

### 🔸 **31–40: Clustering, High Availability & Real-World Usage**

31. **What is a RabbitMQ cluster?**  
    A group of nodes working together to provide high availability and scalability.

32. **What is the difference between mirrored and quorum queues?**
- **Mirrored**: Master-slave replication.
- **Quorum**: Raft-based consensus model for better reliability.

33. **What is a virtual host (vhost) in RabbitMQ?**  
    A namespace for separating queues, exchanges, and permissions.

34. **What is federation in RabbitMQ?**  
    Enables message flow between brokers in different networks.

35. **What is the shovel plugin used for?**  
    For reliably pushing/pulling messages between RabbitMQ brokers.

36. **What is high availability in RabbitMQ?**  
    Ensuring queue and message availability across node failures via mirrored/quorum queues.

37. **What are alternate exchanges?**  
    A fallback exchange used when messages can't be routed.

38. **How does RabbitMQ handle network partitions?**  
    In quorum queues, using Raft protocol ensures consistency. In mirrored queues, behavior depends on pause-minority settings.

39. **What is consumer cancel notification?**  
    Notification to consumers when the queue they are consuming from is deleted or reconfigured.

40. **What are some RabbitMQ plugins you've used?**
- Management Plugin
- Shovel Plugin
- Federation Plugin
- Prometheus Plugin

---

### 🔸 **41–50: Spring Boot & Integration**

41. **How do you connect Spring Boot with RabbitMQ?**  
    Use `spring-boot-starter-amqp` and configure using `application.properties`.

42. **What is RabbitTemplate in Spring Boot?**  
    Helper class to send messages to queues/exchanges.

43. **How do you consume messages in Spring Boot?**  
    Use `@RabbitListener` on a method.

44. **How to set TTL or DLQ in Spring Boot queues?**  
    Provide custom arguments when defining a `Queue` bean.

45. **How do you configure message serialization (JSON) in Spring Boot?**  
    Use `Jackson2JsonMessageConverter` with `RabbitTemplate`.

46. **How do you configure retries in Spring AMQP?**  
    Use `RetryTemplate`, `@Retryable`, or DLQ-based retry mechanism.

47. **How can you do manual acknowledgment in Spring Boot?**  
    Use `AcknowledgeMode.MANUAL` and `ChannelAwareMessageListener`.

48. **How to configure multiple RabbitMQ listeners in Spring Boot?**  
    Define multiple `@RabbitListener` methods and bind them to different queues.

49. **How do you test RabbitMQ with Spring Boot?**  
    Use embedded RabbitMQ or `Testcontainers` for integration testing.

50. **What are some best practices for using RabbitMQ in Spring Boot?**
- Use `@RabbitListener` wisely
- Always use manual acks for critical processing
- Handle retries and failures
- Monitor queues and consumers

---

Would you like these in **PDF format**, or should I also help you with a **case-study-based project or system design** involving RabbitMQ to practice with?