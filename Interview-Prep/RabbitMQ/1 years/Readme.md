Here are the **Top 50 RabbitMQ Interview Questions and Answers** tailored for someone with **1 year of experience**. These are focused on understanding core concepts, practical usage, and basic troubleshooting that a junior developer or QA might encounter.

---

## ✅ Top 50 RabbitMQ Interview Questions (1 Year Experience)

---

### 🔹 **Basic Concepts**

1. **What is RabbitMQ?**  
   A message broker that allows applications to communicate through asynchronous messaging.

2. **Why use RabbitMQ?**  
   For decoupling systems, enabling asynchronous communication, and improving scalability and reliability.

3. **What protocol does RabbitMQ use?**  
   AMQP (Advanced Message Queuing Protocol).

4. **What is a message broker?**  
   Middleware that enables communication between applications by routing messages.

5. **What is a message in RabbitMQ?**  
   A piece of data sent from a producer to a consumer through the broker.

---

### 🔹 **Core Components**

6. **What is a producer?**  
   An application that sends messages to RabbitMQ.

7. **What is a consumer?**  
   An application that receives messages from RabbitMQ.

8. **What is a queue in RabbitMQ?**  
   A buffer that stores messages until they are consumed.

9. **What is an exchange?**  
   A component that routes messages to queues based on rules.

10. **What is binding?**  
    A relationship between a queue and an exchange with a routing key.

---

### 🔹 **Exchanges**

11. **What are the types of exchanges in RabbitMQ?**
- Direct
- Fanout
- Topic
- Headers

12. **What is a direct exchange?**  
    Routes messages to queues based on exact routing key match.

13. **What is a fanout exchange?**  
    Broadcasts messages to all bound queues regardless of routing key.

14. **What is a topic exchange?**  
    Routes messages to queues using pattern matching (`*`, `#`).

15. **What is a headers exchange?**  
    Routes messages based on message header values instead of routing keys.

---

### 🔹 **Queues and Routing**

16. **Can multiple queues be bound to one exchange?**  
    Yes.

17. **Can one queue be bound to multiple exchanges?**  
    Yes.

18. **What is a routing key?**  
    A string used by exchanges to decide how to route messages.

19. **What is a default exchange?**  
    A pre-defined direct exchange with an empty string as the name.

20. **What happens if no queue is bound to an exchange?**  
    The message is dropped.

---

### 🔹 **Durability and Reliability**

21. **What is a durable queue?**  
    A queue that survives a broker restart.

22. **How to make messages persistent?**  
    Set delivery mode to `2` and publish to a durable queue.

23. **What is an exclusive queue?**  
    A queue used by only one connection and deleted when that connection closes.

24. **What is an auto-delete queue?**  
    A queue that is deleted automatically when the last consumer unsubscribes.

25. **What is message acknowledgment?**  
    A confirmation sent by the consumer to tell RabbitMQ a message was processed.

---

### 🔹 **Acknowledgment and Requeueing**

26. **What is the difference between auto-ack and manual ack?**
- Auto-ack: Message is removed immediately.
- Manual ack: Removed only after successful processing.

27. **What happens if a message is not acknowledged?**  
    It can be requeued or sent to a dead-letter queue.

28. **What is a dead-letter queue?**  
    A queue for messages that were not processed successfully.

29. **How can you reject a message?**  
    Using `basic.reject` or `basic.nack`.

30. **What is prefetch count?**  
    Limits the number of unacknowledged messages a consumer can receive.

---

### 🔹 **Performance and Monitoring**

31. **How can you monitor RabbitMQ?**  
    Using the RabbitMQ Management Plugin.

32. **What is the RabbitMQ Management Plugin?**  
    A web UI for monitoring queues, exchanges, and connections.

33. **How to enable RabbitMQ Management Plugin?**  
    Run: `rabbitmq-plugins enable rabbitmq_management`

34. **What ports does RabbitMQ use?**
- AMQP: 5672
- Management UI: 15672

35. **What is a virtual host in RabbitMQ?**  
    A namespace for queues, exchanges, and bindings.

---

### 🔹 **Common Configurations**

36. **How do you declare a queue in code (example: Java)?**  
    Using a channel:
   ```java
   channel.queueDeclare("myQueue", true, false, false, null);
   ```

37. **What does `queueDeclare` return?**  
    A `DeclareOk` object with queue information.

38. **What is the default user in RabbitMQ?**  
    Username: `guest`, Password: `guest`

39. **Can the `guest` user access RabbitMQ remotely?**  
    No, it is restricted to localhost.

40. **How do you create a new user in RabbitMQ?**
   ```bash
   rabbitmqctl add_user myuser mypassword
   ```

---

### 🔹 **Use Cases and Best Practices**

41. **When should you use RabbitMQ?**
- Background task processing
- Microservice communication
- Load balancing and buffering

42. **When should you avoid RabbitMQ?**  
    For event streaming — use Kafka instead.

43. **Can RabbitMQ ensure message ordering?**  
    Yes, per queue with single consumer.

44. **How can you ensure no message is lost?**
- Durable queues
- Persistent messages
- Manual acks

45. **How can you retry failed messages?**  
    Use dead-letter exchanges or retry queues.

---

### 🔹 **Common Troubleshooting**

46. **What happens when a queue is full?**  
    RabbitMQ can reject messages or block publishers depending on configuration.

47. **What if a consumer crashes before acking?**  
    Message is requeued and redelivered.

48. **Why might a message not be routed?**
- No bound queue
- No matching routing key

49. **How can you list queues via CLI?**
   ```bash
   rabbitmqctl list_queues
   ```

50. **What are common RabbitMQ client libraries?**
- Java: Spring AMQP, RabbitMQ Java Client
- Python: pika
- Node.js: amqplib

---

Would you like a **PDF format** or next want **RabbitMQ + Spring Boot integration questions** or **real-world scenarios with RabbitMQ**?