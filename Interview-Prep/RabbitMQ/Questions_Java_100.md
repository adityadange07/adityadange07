Here are the **Top 100 RabbitMQ interview questions and answers** specifically tailored for **Java Software Developers** with **3–5 years of experience**. The questions are organized by **topic categories** to ensure clarity and depth.

---

## 🔹 1. **RabbitMQ Basics**

1. What is RabbitMQ?
2. How does RabbitMQ differ from Kafka?
3. What are the key features of RabbitMQ?
4. What messaging protocols does RabbitMQ support?
5. What is the default port of RabbitMQ?
6. What is AMQP and how does RabbitMQ use it?
7. What is a message broker?
8. Explain the architecture of RabbitMQ.
9. What is the role of an exchange in RabbitMQ?
10. What are queues in RabbitMQ?

---

## 🔹 2. **Core Concepts**

11. What are the types of exchanges in RabbitMQ?
12. Explain the difference between direct, topic, fanout, and headers exchanges.
13. What is routing key in RabbitMQ?
14. What is binding in RabbitMQ?
15. What is a virtual host in RabbitMQ?
16. How does message acknowledgment work in RabbitMQ?
17. What is prefetch count in RabbitMQ?
18. What are durable, persistent, and transient messages?
19. What is the difference between auto-delete and exclusive queues?
20. How do dead-letter exchanges work in RabbitMQ?

---

## 🔹 3. **RabbitMQ with Java (Spring Boot)**

21. How do you integrate RabbitMQ with Spring Boot?
22. What is `spring-boot-starter-amqp`?
23. How do you define a queue and exchange in Spring Boot?
24. How do you create a listener in Spring Boot for RabbitMQ?
25. What is the role of `RabbitTemplate` in Spring Boot?
26. How do you send a message using `RabbitTemplate`?
27. What is `@RabbitListener` annotation?
28. How do you implement message converters (JSON/XML) in Spring Boot RabbitMQ?
29. How do you implement manual acknowledgment in Spring Boot?
30. How do you configure connection settings in `application.properties`?

---

## 🔹 4. **Advanced RabbitMQ Messaging**

31. What is message TTL (Time-To-Live)?
32. How do you implement delayed messaging in RabbitMQ?
33. What is the purpose of dead-letter exchanges?
34. How can you handle failed messages or message retries?
35. What is the difference between message redelivery and retries?
36. How do you implement priority queues?
37. How do you implement message ordering?
38. How do you handle poison messages?
39. What is a consumer tag?
40. How does RabbitMQ handle message persistence?

---

## 🔹 5. **Administration and Monitoring**

41. How do you monitor RabbitMQ using the management UI?
42. What is the RabbitMQ Management Plugin?
43. How do you list queues and exchanges using the RabbitMQ CLI?
44. How do you purge a queue in RabbitMQ?
45. How do you enable and disable plugins in RabbitMQ?
46. What is the `rabbitmqctl` command?
47. How do you check the health of a RabbitMQ node?
48. What are RabbitMQ policies?
49. How do you configure mirrored queues?
50. How do you manage user permissions in RabbitMQ?

---

## 🔹 6. **Security**

51. How do you secure communication in RabbitMQ?
52. How do you enable SSL in RabbitMQ?
53. How do you set up authentication and authorization in RabbitMQ?
54. How do you prevent unauthorized queue access?
55. What is the default guest user and its restrictions?

---

## 🔹 7. **Clustering and High Availability**

56. What is RabbitMQ clustering?
57. How do you set up a RabbitMQ cluster?
58. What is the role of mirrored queues?
59. How does RabbitMQ achieve high availability?
60. How do you deal with network partitions in RabbitMQ?

---

## 🔹 8. **Performance and Tuning**

61. How can you improve RabbitMQ throughput?
62. What are some common performance tuning parameters?
63. How does batching help in RabbitMQ?
64. How do you tune consumer concurrency?
65. What is lazy queue and when should it be used?

---

## 🔹 9. **Error Handling and Reliability**

66. How do you handle message retries in Spring Boot?
67. What happens when a message is rejected?
68. What is negative acknowledgment (nack)?
69. How do you ensure message delivery reliability?
70. How do you avoid message duplication?

---

## 🔹 10. **Testing and Debugging**

71. How do you test RabbitMQ listeners?
72. How do you mock RabbitMQ in unit tests?
73. What are some useful RabbitMQ logs to check for debugging?
74. How do you trace a message flow in RabbitMQ?
75. How do you handle backpressure in consumers?

---

## 🔹 11. **Deployment and Configuration**

76. How do you deploy RabbitMQ using Docker?
77. How do you configure RabbitMQ using environment variables?
78. How do you configure RabbitMQ on Kubernetes?
79. How do you persist RabbitMQ data on container restarts?
80. How do you scale RabbitMQ consumers in production?

---

## 🔹 12. **Real-world Use Cases and Best Practices**

81. What are common use cases for RabbitMQ in microservices?
82. What are the best practices for queue naming?
83. How do you ensure idempotent message processing?
84. What is a work queue and how is it implemented?
85. When would you choose RabbitMQ over Kafka?
86. What are the trade-offs of using RabbitMQ?
87. What is backpressure and how do you manage it?
88. How do you ensure at-most-once and at-least-once delivery?
89. How do you implement request-reply messaging with RabbitMQ?
90. How do you manage multiple consumers on a queue?

---

## 🔹 13. **Integration with Other Tools**

91. How does RabbitMQ integrate with ELK Stack for logging?
92. How do you integrate RabbitMQ with monitoring tools like Prometheus & Grafana?
93. How do you send messages from one service to another using RabbitMQ?
94. How can RabbitMQ be used in event-driven architecture?
95. How do you integrate RabbitMQ with external systems (like email or SMS)?

---

## 🔹 14. **Concurrency and Scaling**

96. How do you manage concurrency in RabbitMQ consumers?
97. How do you distribute load across multiple consumers?
98. What happens when multiple consumers listen to the same queue?
99. How do you scale RabbitMQ in a distributed system?
100. How does RabbitMQ ensure fair dispatch?

---

If you'd like a **PDF version**, **topic-wise deep explanations**, or **Spring Boot project examples**, let me know — I can prepare that for you as well.
