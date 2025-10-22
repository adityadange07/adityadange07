Here are the **Top 50 RabbitMQ Interview Questions and Answers** tailored for someone with **3 years of experience**. This set covers **intermediate to advanced** concepts, including **message routing**, **durability**, **dead-lettering**, **acknowledgments**, **Spring Boot integration**, and **real-world scenarios**.

---

## ✅ Top 50 RabbitMQ Interview Questions (3 Years Experience)

---

### 🔹 **1. Core RabbitMQ Concepts**

1. **What is RabbitMQ and what problem does it solve?**  
   RabbitMQ is a message broker that decouples services by facilitating asynchronous communication via messaging queues.

2. **Explain the architecture of RabbitMQ.**  
   Producers → Exchanges → Bindings → Queues → Consumers

3. **What is the AMQP protocol?**  
   Advanced Message Queuing Protocol is a standardized wire-level protocol used by RabbitMQ for messaging.

4. **What are the main components in RabbitMQ?**
    - Producer
    - Consumer
    - Exchange
    - Queue
    - Binding
    - Routing key

5. **How does RabbitMQ ensure decoupling of services?**  
   By enabling asynchronous communication and message buffering between producers and consumers.

---

### 🔹 **2. Exchanges and Routing**

6. **What are the different exchange types in RabbitMQ?**
    - Direct
    - Topic
    - Fanout
    - Headers

7. **How does a direct exchange work?**  
   Routes messages to queues whose binding key exactly matches the routing key.

8. **How does a topic exchange work?**  
   Routes messages to queues based on wildcard pattern matching in routing keys.

9. **How does a fanout exchange work?**  
   Routes messages to **all bound queues**, regardless of routing keys.

10. **What is a headers exchange?**  
    Routes messages based on matching header attributes instead of routing keys.

---

### 🔹 **3. Queue Behavior**

11. **What is a durable queue?**  
    A queue that survives RabbitMQ broker restarts.

12. **What is an exclusive queue?**  
    Used by only one connection and deleted when the connection closes.

13. **What is an auto-delete queue?**  
    Automatically deleted when all consumers disconnect.

14. **Can a queue be bound to multiple exchanges?**  
    Yes, a queue can be bound to multiple exchanges using different binding keys.

15. **What is the difference between durable and transient messages?**  
    Durable messages are written to disk, while transient ones are stored only in memory.

---

### 🔹 **4. Message Delivery and Acknowledgment**

16. **What is message acknowledgment (ack)?**  
    It's a signal sent by the consumer to confirm successful message processing.

17. **What is the difference between auto-ack and manual ack?**
- Auto-ack: Message is deleted immediately after delivery.
- Manual ack: Message is deleted only after explicit acknowledgment.

18. **What happens if a message is not acknowledged?**  
    It is either requeued or dead-lettered depending on configuration.

19. **What is `basic.reject` vs `basic.nack`?**
- `basic.reject`: Rejects a single message.
- `basic.nack`: Rejects one or more messages, with optional requeue.

20. **How do you prevent message loss?**
- Use durable queues
- Send persistent messages
- Use manual acknowledgment
- Implement dead-letter queues

---

### 🔹 **5. Dead Letter Queues (DLQ)**

21. **What is a Dead Letter Exchange (DLX)?**  
    An exchange to which unprocessed or failed messages are routed.

22. **When does a message go to a DLQ?**
- If it's rejected without requeue
- TTL expires
- Queue is full
- Max delivery attempts reached

23. **How to configure DLQ in RabbitMQ?**  
    Set `x-dead-letter-exchange` and optionally `x-dead-letter-routing-key` on the original queue.

24. **What is the benefit of DLQ?**  
    Helps in debugging and safely retrying failed messages.

25. **How do you retry messages from a DLQ?**  
    Consume from DLQ and republish to the original exchange or queue.

---

### 🔹 **6. Message TTL, Expiry and Priority**

26. **What is message TTL (Time-To-Live)?**  
    Time a message can stay in the queue before being discarded or dead-lettered.

27. **How to set TTL in RabbitMQ?**
- Per-message via header
- Per-queue via arguments (`x-message-ttl`)

28. **What is queue TTL?**  
    Automatically deletes the queue after a period of inactivity.

29. **What is a priority queue?**  
    Allows consumers to process messages based on their priority.

30. **How to configure a priority queue in RabbitMQ?**  
    Set `x-max-priority` argument during queue declaration.

---

### 🔹 **7. Performance and Reliability**

31. **What is prefetch count and why is it important?**  
    Controls the number of unacknowledged messages a consumer can hold. Prevents overload.

32. **What is lazy queue in RabbitMQ?**  
    A queue that stores messages on disk rather than in memory, optimized for high-volume storage.

33. **How to monitor RabbitMQ performance?**
- Management UI
- `rabbitmqctl`
- Prometheus + Grafana
- Logs and alarms

34. **What is flow control in RabbitMQ?**  
    Mechanism to block publishers when broker is under memory or disk pressure.

35. **How to avoid memory issues in RabbitMQ?**
- Use lazy queues
- Configure prefetch
- Monitor memory alarms
- Scale consumers

---

### 🔹 **8. Spring Boot Integration (Java)**

36. **How do you integrate RabbitMQ with Spring Boot?**  
    Use `spring-boot-starter-amqp`.

37. **How to declare queues, exchanges, and bindings in Spring Boot?**  
    Using `@Bean` methods in a configuration class with `Queue`, `Exchange`, and `Binding`.

38. **What does `@RabbitListener` do in Spring Boot?**  
    Annotates a method to consume messages from a specified queue.

39. **What is `RabbitTemplate` in Spring?**  
    A helper class for publishing messages to exchanges or queues.

40. **How to handle message retries in Spring Boot + RabbitMQ?**
- RetryTemplate
- Dead-lettering with retry queues
- Spring Retry mechanism

---

### 🔹 **9. Security and Administration**

41. **How to secure RabbitMQ?**
- Use TLS/SSL
- Strong passwords
- Role-based access control
- Firewalls and IP whitelisting

42. **What are virtual hosts in RabbitMQ?**  
    Logical containers to isolate environments, users, and resources.

43. **How to create a new user in RabbitMQ?**  
    Use CLI:
   ```bash
   rabbitmqctl add_user username password  
   rabbitmqctl set_permissions -p / username ".*" ".*" ".*"
   ```

44. **How do you define user permissions in RabbitMQ?**  
    Via regex on configure, write, and read permissions per virtual host.

45. **How to enable RabbitMQ Management UI?**  
    Enable plugin:
   ```bash
   rabbitmq-plugins enable rabbitmq_management
   ```

---

### 🔹 **10. Real-world Scenarios & Troubleshooting**

46. **What happens when a queue is full?**  
    New messages are either dropped or dead-lettered depending on policy.

47. **What happens when a consumer crashes after receiving a message?**  
    If not acknowledged, RabbitMQ requeues the message for redelivery.

48. **How to ensure message ordering in RabbitMQ?**
- Use single queue
- Single consumer
- Manual acks processed sequentially

49. **How do you ensure exactly-once delivery?**  
    RabbitMQ does not guarantee it by default. Must implement **deduplication** and **idempotency** at the consumer level.

50. **What are some RabbitMQ alternatives and when would you choose them?**
- **Kafka**: For event streaming and high-throughput
- **ActiveMQ**: JMS-based systems
- **Amazon SQS**: Cloud-native messaging  
  Use RabbitMQ for complex routing, low-latency, and flexible delivery guarantees.

---

Would you like this content as a **PDF or Word file**? Or should I prepare a **Spring Boot + RabbitMQ project-based Q&A** next for hands-on preparation?