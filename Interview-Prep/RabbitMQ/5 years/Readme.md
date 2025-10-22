Here are the **Top 50 RabbitMQ Interview Questions and Answers** tailored for someone with **5 years of experience**. These cover **core concepts, advanced architecture, message reliability, clustering, Spring integration, security, observability**, and **real-world scenarios** relevant to senior/lead developer roles.

---

## ✅ Top 50 RabbitMQ Interview Questions (5 Years Experience)

---

### 🔹 **1. Core Concepts & Architecture**

1. **What is RabbitMQ and how does it implement AMQP?**  
   RabbitMQ is an open-source message broker that uses AMQP (Advanced Message Queuing Protocol) to facilitate asynchronous communication via producers, exchanges, queues, and consumers.

2. **Explain the key components of AMQP.**
    - Producer
    - Consumer
    - Exchange
    - Queue
    - Binding
    - Routing Key
    - Virtual Host

3. **What are the different types of exchanges in RabbitMQ?**
    - Direct
    - Topic
    - Fanout
    - Headers

4. **What is the difference between a direct and topic exchange?**
    - Direct: Exact match of routing key
    - Topic: Pattern matching using wildcards `*` and `#`

5. **What is the use of fanout and headers exchange?**
    - Fanout: Broadcasts to all bound queues
    - Headers: Routes based on message header attributes

6. **Can a queue be bound to multiple exchanges?**  
   Yes, a single queue can bind to multiple exchanges with different routing keys.

7. **What is a binding and what role does it play?**  
   It links an exchange to a queue using a routing key.

8. **How does RabbitMQ handle message delivery guarantees?**  
   Through a combination of durable queues, persistent messages, and acknowledgments.

9. **What is the significance of virtual hosts in RabbitMQ?**  
   Logical partitions for multi-tenancy, access control, and resource separation.

10. **What are consumer acknowledgments and why are they important?**  
    Ensures that messages are processed successfully before removal from the queue.

---

### 🔹 **2. Message Durability & Reliability**

11. **What is the difference between a durable queue and a persistent message?**
- Durable queue survives broker restarts.
- Persistent messages are written to disk to survive crashes.

12. **How do you implement guaranteed message delivery?**  
    Use durable queues, persistent messages, manual acks, and dead-letter queues.

13. **What happens if a consumer crashes before sending an ack?**  
    The message is requeued and delivered to another available consumer.

14. **What is the difference between `basic.ack`, `basic.nack`, and `basic.reject`?**
- `basic.ack`: Acknowledge success
- `basic.nack`: Reject one/many messages, requeue optionally
- `basic.reject`: Reject one message only

15. **What is a dead-letter exchange (DLX)?**  
    An exchange that handles undeliverable messages.

16. **What scenarios trigger a DLX?**
- Message TTL expiry
- Queue limit reached
- Message rejection with `requeue=false`

17. **What is a TTL (Time-To-Live) in RabbitMQ?**  
    Configurable expiry for messages or queues.

18. **How do you configure TTL and DLX in Spring Boot?**  
    Using `x-message-ttl`, `x-dead-letter-exchange`, and `x-dead-letter-routing-key`.

19. **What are alternate exchanges?**  
    A fallback route for messages that cannot be routed to any queue.

20. **What is the role of `mandatory` and `immediate` flags?**
- `mandatory`: Return unroutable message to producer
- `immediate`: (Deprecated) Deliver only if a consumer is available

---

### 🔹 **3. High Availability & Clustering**

21. **What is a RabbitMQ cluster and why is it used?**  
    A group of nodes sharing the same metadata, enabling horizontal scaling and HA.

22. **How is clustering achieved in RabbitMQ?**  
    Use `rabbitmqctl join_cluster` to connect nodes with shared cookies.

23. **What is the difference between mirrored and quorum queues?**
- Mirrored: Replication of a classic queue
- Quorum: Raft-based consensus model, recommended for production

24. **What are quorum queues and when to use them?**  
    For high consistency and availability, especially in distributed systems.

25. **What are the trade-offs between mirrored and quorum queues?**
- Quorum: Slower write, better fault tolerance
- Mirrored: Higher performance, but prone to split-brain issues

26. **What is queue synchronization in RabbitMQ?**  
    Ensures slave queues are updated with master before failover.

27. **How do you handle node failures in a RabbitMQ cluster?**
- Use mirrored/quorum queues
- Ensure clients are configured with multiple broker URLs

28. **How does RabbitMQ handle partition tolerance?**  
    Limited—requires quorum queues to ensure consistency over availability.

29. **What is RabbitMQ federation?**  
    A way to link brokers across regions for message replication or forwarding.

30. **What is RabbitMQ shoveling?**  
    Transfers messages between brokers via plugin (more eager than federation).

---

### 🔹 **4. Spring Integration & Dev Use-Cases**

31. **How do you integrate RabbitMQ with Spring Boot?**  
    Using `spring-boot-starter-amqp`, `@RabbitListener`, `RabbitTemplate`, etc.

32. **How to configure RabbitMQ properties in `application.yml`?**
   ```yaml
   spring.rabbitmq.host: localhost
   spring.rabbitmq.port: 5672
   spring.rabbitmq.username: guest
   ```

33. **How to send and receive messages in Spring Boot?**
- Producer: `RabbitTemplate.convertAndSend()`
- Consumer: `@RabbitListener`

34. **What is `@RabbitListener` and how is it used?**  
    Declares a method as a message listener for a queue.

35. **What is RabbitTemplate and what are its use cases?**  
    Helper class to send/receive messages with conversions and custom settings.

36. **How do you handle retries and error handling in Spring AMQP?**  
    Use `RetryTemplate`, `RecoveryCallback`, DLX, or retry queues.

37. **How to configure message converters (e.g., JSON) in Spring Boot?**  
    Define a `Jackson2JsonMessageConverter` bean.

38. **How to manually acknowledge messages in Spring Boot?**  
    Use `SimpleMessageListenerContainer` with `MANUAL` ack mode.

39. **How do you declare exchanges and queues programmatically in Spring Boot?**  
    Use `@Bean` methods with `Queue`, `Exchange`, `Binding`.

40. **What is the use of correlationId in messaging?**  
    Matches requests with responses, especially for RPC.

---

### 🔹 **5. Monitoring, Security, and Troubleshooting**

41. **How do you monitor RabbitMQ in production?**
- Management UI
- Prometheus/Grafana
- Logs
- `rabbitmq-diagnostics`

42. **What is flow control in RabbitMQ?**  
    Temporary throttling of publishers when memory/disk limits are reached.

43. **What are signs of back pressure or overload?**
- Message buildup
- High memory usage
- Publisher flow control triggered

44. **How do you secure RabbitMQ?**
- Use TLS/SSL
- Enable user-based permissions
- Enable vhost isolation
- Use secure password policies

45. **How does RabbitMQ handle authentication and authorization?**
- Auth: User login
- AuthZ: Permissions per vhost (configure, write, read)

46. **What is the difference between `rabbitmqctl` and `rabbitmq-diagnostics`?**
- `rabbitmqctl`: Admin CLI
- `rabbitmq-diagnostics`: Health checks and stats

47. **How do you debug message delivery issues in RabbitMQ?**
- Enable publisher confirms
- Monitor DLQs
- Use message tracing (firehose plugin)

48. **What is the firehose in RabbitMQ?**  
    A plugin to trace all message activity for debugging.

49. **How to test RabbitMQ locally in CI/CD pipelines?**
- Use Docker containers
- Use TestContainers in JUnit
- Use mocks or embedded broker

50. **What is your approach to RabbitMQ disaster recovery and failover?**
- Backup configuration
- Use HA queues (quorum)
- Load-balanced connections
- Monitor cluster health

---

Would you like this list as a **PDF**, or do you want to dive into **hands-on scenarios or case studies** involving RabbitMQ + Spring Boot + microservices?