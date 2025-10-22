Here are the **Top 100 Redis interview questions and answers** tailored for a **Java software developer (3–5 years of experience)**. These are grouped into categories to help you cover fundamentals, usage with Java, and real-world practices.

---

## 🔹 1. Redis Basics

1. What is Redis and why is it used?
2. Is Redis an in-memory database?
3. What data structures does Redis support?
4. What is the default port of Redis?
5. What is the difference between Redis and Memcached?
6. What are some common use cases of Redis?
7. How does Redis persist data?
8. What are the two main Redis persistence mechanisms?
9. What is RDB persistence?
10. What is AOF (Append Only File) persistence?

---

## 🔹 2. Core Redis Data Types

11. What is a Redis string? Give an example.
12. What is a Redis list? When would you use it?
13. What is a Redis set? How is it different from a list?
14. What is a Redis sorted set (zset)?
15. What is a Redis hash? When is it useful?
16. How do you increment a counter in Redis?
17. How do you add and retrieve values from a list?
18. How do you implement a queue using Redis?
19. What is the difference between LPUSH and RPUSH?
20. What is the difference between SADD and ZADD?

---

## 🔹 3. Redis with Java

21. What are the popular Redis Java clients?
22. What is Jedis?
23. What is Lettuce in Redis?
24. How do you connect to Redis using Jedis in Java?
25. How do you store a Java object in Redis?
26. How do you retrieve and deserialize a Java object from Redis?
27. How do you configure a RedisTemplate in Spring Boot?
28. What is the role of RedisTemplate?
29. What is `@Cacheable` and `@CachePut` in Spring?
30. How do you implement a TTL for a key in Java using Redis?

---

## 🔹 4. Redis Caching

31. What is caching?
32. How do you implement caching using Redis in Spring Boot?
33. What are common caching strategies in Redis?
34. What is cache eviction? What are different eviction policies?
35. What is the default eviction policy of Redis?
36. What is cache invalidation and why is it important?
37. How do you configure cache TTL in Spring Boot?
38. What is the difference between write-through and write-behind caching?
39. How does Redis handle cache misses?
40. What are some caching annotations in Spring?

---

## 🔹 5. Redis Transactions and Pub/Sub

41. How do you implement transactions in Redis?
42. What is the MULTI command?
43. What does DISCARD do in Redis?
44. What is optimistic locking in Redis?
45. What are the WATCH and UNWATCH commands?
46. What is Redis Pub/Sub?
47. How does Pub/Sub work in Redis?
48. How do you publish and subscribe messages using Redis in Java?
49. What are some limitations of Redis Pub/Sub?
50. Can Redis queues be used for messaging between services?

---

## 🔹 6. Redis Persistence

51. Compare RDB and AOF persistence.
52. Can Redis use both RDB and AOF simultaneously?
53. What are fsync policies in AOF?
54. What happens during Redis restart?
55. What is Redis snapshotting?
56. What are the pros and cons of AOF?
57. How do you trigger a manual Redis backup?
58. How do you configure persistence in redis.conf?
59. How do you reduce Redis startup time with large datasets?
60. How do you check the size of the AOF or RDB file?

---

## 🔹 7. Redis Performance and Optimization

61. How do you monitor Redis performance?
62. What are some common Redis performance bottlenecks?
63. What is pipelining in Redis?
64. How do you implement pipelining in Java using Jedis?
65. What is lazy deletion in Redis?
66. What is memory fragmentation in Redis?
67. How do you tune maxmemory settings in Redis?
68. How do you profile slow commands in Redis?
69. How do you avoid cache stampede in Redis?
70. What is cache penetration and how do you prevent it?

---

## 🔹 8. Redis Security

71. How do you secure a Redis instance?
72. What is Redis AUTH?
73. How do you restrict access to Redis?
74. Can you enable TLS/SSL in Redis?
75. How do you change the default Redis port?
76. What are some Redis best practices for security?
77. How do you prevent unauthorized flush of Redis data?
78. How do you disable dangerous commands in Redis?
79. What are Redis ACLs?
80. Can Redis be used in a multi-tenant environment securely?

---

## 🔹 9. Redis in Distributed Systems

81. What is Redis Sentinel?
82. How does Sentinel provide high availability?
83. What is Redis Cluster?
84. How is data sharded in Redis Cluster?
85. What is hash slot in Redis Cluster?
86. How do you scale Redis horizontally?
87. How do you configure and use Redis Sentinel in Java?
88. What happens during a failover in Redis Sentinel?
89. Can you use Redis with Docker and Kubernetes?
90. How do you deploy Redis in a production environment?

---

## 🔹 10. Real-world Use Cases & Troubleshooting

91. How do you use Redis for session management?
92. How do you implement rate limiting using Redis?
93. How can you use Redis for leaderboard design?
94. How do you use Redis for distributed locks?
95. How does Redisson help in distributed locking?
96. What is Redisson? How is it different from Jedis?
97. What are common Redis issues in Java applications?
98. How do you handle Redis connection failures?
99. What is the impact of using Redis with large keys?
100. When should Redis **not** be used?

---

Would you like the **answers** to these questions or a **PDF version**? I can also provide:

* ✅ **Spring Boot + Redis examples**
* ✅ **Project use cases (e.g., rate limiter, cache layer)**
* ✅ **Hands-on exercises or mini projects**

Let me know what you'd prefer next!
