## ✅ Top 100 System Design Interview Questions
**[HLD + LLD Combined – Architecture, Scalability, Design Patterns, Real Systems]**

---

### 🔹 **1–25: High-Level Design Fundamentals**

## 1. What is system design and why is it important?

### ✅ **What is System Design?**

**System Design** is the process of defining the architecture, components, modules, interfaces, and data for a system to satisfy specified requirements. It is a **high-level plan** that helps you design **scalable, efficient, reliable, and maintainable software systems**.

Think of it as **blueprint creation** for software systems, similar to how architects design blueprints for buildings before construction.

---

### ✅ **Types of System Design**

System Design is broadly divided into two categories:

| Type                        | Description                                                                                                                 |
| --------------------------- | --------------------------------------------------------------------------------------------------------------------------- |
| **High-Level Design (HLD)** | Defines the system architecture, components, services, databases, external interfaces. Focuses on “what” the system does.   |
| **Low-Level Design (LLD)**  | Deals with internal logic of each component, data structures, class diagrams, algorithms. Focuses on “how” each part works. |

---

### ✅ **Why is System Design Important?**

| Reason                    | Explanation                                                                                                 |
| ------------------------- | ----------------------------------------------------------------------------------------------------------- |
| **1. Scalability**        | System design helps ensure that the system can handle increasing loads (users, data, requests) efficiently. |
| **2. Reliability**        | A well-designed system continues to function correctly even when some components fail.                      |
| **3. Maintainability**    | Good system design makes the system easier to update and modify in the future.                              |
| **4. Performance**        | Proper design minimizes bottlenecks and optimizes response time and throughput.                             |
| **5. Cost-effectiveness** | Avoids over-engineering or under-designing, helping teams use resources wisely.                             |
| **6. Collaboration**      | Provides a common plan for developers, testers, and stakeholders to understand and build the system.        |

---

### ✅ **Real-World Example: Design a URL Shortener (like bit.ly)**

Let’s walk through a **high-level system design** example.

#### Problem:

Design a URL shortener that converts long URLs to short ones and redirects users from the short URL to the original URL.

#### Functional Requirements:

* Create a short URL from a long URL.
* Redirect from the short URL to the original URL.
* Track usage statistics.

#### Non-Functional Requirements:

* High availability
* Scalability
* Low latency

---

### ✅ **High-Level Design (HLD)**

**Components:**

1. **API Gateway / Load Balancer**

    * Distributes traffic across multiple servers

2. **Web Server**

    * Handles user requests (REST API to create and fetch short URLs)

3. **Application Layer**

    * Contains business logic: generate short URL, store it, handle redirects

4. **Database**

    * Stores long URL ↔ short URL mapping (e.g., NoSQL like Redis or SQL like MySQL)

5. **Cache**

    * To reduce DB calls for frequently accessed short URLs

6. **Analytics Service (optional)**

    * Tracks number of hits, IP addresses, geolocation, etc.

---

### ✅ **Low-Level Design (LLD)** (Simplified View)

#### URL Mapping Table (Database Schema):

| Field Name  | Type      | Description                      |
| ----------- | --------- | -------------------------------- |
| short\_url  | String    | Unique short code (e.g., abc123) |
| long\_url   | String    | Original long URL                |
| created\_at | Timestamp | When the short URL was created   |

#### URL Generation Logic:

* Base62 encoding (using `a-z`, `A-Z`, `0-9`) of a unique ID or hash.

```java
String base62 = "abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789";

String encode(int id) {
    StringBuilder sb = new StringBuilder();
    while (id > 0) {
        sb.append(base62.charAt(id % 62));
        id /= 62;
    }
    return sb.reverse().toString();
}
```

---

### ✅ **Key Design Decisions**

| Question                           | Answer                                            |
| ---------------------------------- | ------------------------------------------------- |
| How to avoid duplicate short URLs? | Use a unique ID or hash of the long URL.          |
| How to handle collisions?          | Use retries or append random suffix.              |
| How to scale?                      | Use sharded DB, load balancers, and cache layers. |
| How to ensure availability?        | Deploy replicas and use distributed services.     |

---

### ✅ **Conclusion**

**System Design** is **crucial for building robust and scalable software**. It involves careful planning of architecture and components to ensure the system meets all functional and non-functional requirements.

---

### ✅ **Pro Tip for Interviews:**

In a system design interview, always follow this structure:

1. Clarify requirements
2. Define scope (functional + non-functional)
3. Draw high-level architecture
4. Explain data flow and components
5. Consider trade-offs (CAP theorem, consistency vs availability)
6. Talk about scalability, reliability, caching, and security
7. Optionally go into LLD if asked

---

## 2. What are the key components of a scalable system?

In system design interviews, understanding **key components of a scalable system** is essential. A **scalable system** can handle increasing load (users, data, traffic) without compromising performance.

---

## ✅ **Key Components of a Scalable System**

Here are the most important components with detailed explanations and examples:

---

### 1. **Load Balancer**

* **Purpose**: Distributes incoming traffic across multiple servers to avoid overloading any one server.
* **Example**: NGINX, HAProxy, AWS Elastic Load Balancer.

🔹 **Why it's important**:

* Helps horizontal scaling.
* Improves availability and fault tolerance.

📘 **Example Use Case**:

* In a web app with 5 application servers, the load balancer ensures even traffic distribution.

---

### 2. **Application Servers (Stateless)**

* **Purpose**: Host the core business logic of the system.
* **Best Practice**: Keep servers **stateless** so any request can be handled by any server.

🔹 **Why it's important**:

* Stateless servers can be scaled horizontally (e.g., adding more servers).

📘 **Example Use Case**:

* A REST API server that can be duplicated easily behind a load balancer.

---

### 3. **Database (Scalable Data Storage)**

* **Types**:

    * SQL (e.g., PostgreSQL, MySQL)
    * NoSQL (e.g., MongoDB, Cassandra, DynamoDB)

🔹 **Techniques for scalability**:

* **Read Replicas**: For scaling reads.
* **Sharding**: Distribute data across multiple machines.

📘 **Example**:

* For a social media app, user profiles can be sharded by user ID hash.

---

### 4. **Caching Layer**

* **Purpose**: Stores frequently accessed data in-memory to reduce database load.
* **Tools**: Redis, Memcached.

🔹 **Why it's important**:

* Greatly improves read performance and response time.

📘 **Example Use Case**:

* Cache top 100 trending posts instead of querying DB every time.

---

### 5. **Message Queue / Event Queue**

* **Purpose**: Decouple services and enable asynchronous communication.
* **Tools**: RabbitMQ, Apache Kafka, AWS SQS.

🔹 **Why it's important**:

* Helps handle high-throughput tasks like sending emails, processing payments, etc.
* Improves fault tolerance.

📘 **Example Use Case**:

* Order placement service pushes events to a queue, and the inventory service listens and updates stock.

---

### 6. **CDN (Content Delivery Network)**

* **Purpose**: Caches and delivers static content like images, CSS, JS from edge locations close to users.
* **Tools**: Cloudflare, Akamai, AWS CloudFront.

🔹 **Why it's important**:

* Reduces latency and load on origin servers.

📘 **Example Use Case**:

* Serving profile images or video thumbnails in a video platform.

---

### 7. **Data Partitioning (Sharding)**

* **Purpose**: Split large datasets into smaller pieces for better performance.
* **Types**:

    * **Horizontal Partitioning (Sharding)**: By user ID, geo, etc.
    * **Vertical Partitioning**: By table columns (e.g., archive older data separately).

🔹 **Why it's important**:

* Helps scale databases and avoids single-point bottlenecks.

📘 **Example Use Case**:

* In a multi-tenant SaaS app, each tenant's data can be stored in separate shards.

---

### 8. **Failover & Redundancy**

* **Purpose**: Ensure backup systems take over in case of a failure.
* **Techniques**:

    * Primary-replica DB setup
    * Multi-region deployments

🔹 **Why it's important**:

* Increases reliability and system uptime (High Availability).

---

### 9. **Monitoring & Alerting**

* **Tools**: Prometheus, Grafana, ELK stack, Datadog.

🔹 **Why it's important**:

* Helps detect issues, analyze performance, and ensure system health.

📘 **Example**:

* Monitoring 95th percentile latency to detect slow services.

---

### 10. **Auto-scaling**

* **Purpose**: Automatically adjusts the number of running instances based on traffic/load.
* **Tools**: AWS Auto Scaling, Kubernetes HPA.

🔹 **Why it's important**:

* Saves cost and ensures performance during traffic spikes.

---

## ✅ Summary Table

| Component             | Purpose                  | Example Tool                 |
| --------------------- | ------------------------ | ---------------------------- |
| Load Balancer         | Traffic distribution     | NGINX, HAProxy               |
| Stateless App Servers | Process business logic   | Spring Boot, Node.js         |
| Scalable DB           | Persistent storage       | PostgreSQL, Cassandra        |
| Caching               | Fast data access         | Redis, Memcached             |
| Message Queue         | Async task handling      | Kafka, RabbitMQ              |
| CDN                   | Static content delivery  | Cloudflare, AWS CloudFront   |
| Sharding              | Data partitioning        | Custom or built-in (MongoDB) |
| Redundancy            | High availability        | Multi-zone DB setup          |
| Monitoring            | Health and alerting      | Prometheus, Grafana          |
| Auto-scaling          | Dynamic resource scaling | AWS ASG, Kubernetes          |

---

### ✅ Final Thoughts

A scalable system is more than just powerful servers—it's a combination of smart architecture, distributed components, and resilience mechanisms.

**Pro tip for interviews**: When asked to design a scalable system, **mention these components and explain how each helps scale the system**.

---

## 3. How do you approach a system design problem?

Interviewers are often more interested in **how you think** than in a perfect design. So having a **structured and methodical approach** is key.

---

## ✅ **Step-by-Step Approach to a System Design Problem**

Here’s a solid and interview-tested framework to follow:

---

### 🔹 **1. Clarify the Requirements**

**Ask Questions**:

* What exactly should the system do?
* What are the **core features**?
* Are there any **non-functional requirements** (e.g., scale, latency)?
* Who are the users? What is the expected load?

📘 **Example**:
If asked to design a **URL Shortener**, ask:

* Should shortened URLs expire?
* Is tracking analytics part of the system?
* What is the expected number of requests per second?

---

### 🔹 **2. Define the Scope**

You can’t design everything in 45 minutes.

**Pick a focused scope**:

* Start with the **core flow** (e.g., shortening + redirecting a URL).
* Mention optional features (analytics, auth) and say you'll handle them if there's time.

---

### 🔹 **3. Estimate Scale & Constraints**

Ask or estimate:

* **QPS** (queries per second)
* **Storage requirements**
* **Read/write ratio**
* **Latency expectations**

📘 **Example**:

* 100 million users
* 10K URL creations/day
* 1M redirects/day
* 100ms response time

---

### 🔹 **4. Design the High-Level Architecture (HLD)**

Draw a diagram with:

* Clients → Load Balancer → Web/App Servers
* Database(s)
* Cache
* Optional: Message Queues, CDN, etc.

📘 Example blocks:

```
Client → Load Balancer → Application Server → Cache + DB
```

Explain how requests flow through the system.

---

### 🔹 **5. Define Each Component in Detail**

Go deeper into:

* **Application Layer**: Stateless? Microservices?
* **Database**: SQL or NoSQL? Sharding?
* **Caching**: What to cache? TTL?
* **Queueing**: What’s async?
* **CDN**: For static files?

---

### 🔹 **6. Address Non-Functional Requirements**

Discuss:

| Aspect           | Solution                                       |
| ---------------- | ---------------------------------------------- |
| **Scalability**  | Horizontal scaling, sharding, load balancing   |
| **Reliability**  | Replication, failover, retries                 |
| **Availability** | Multi-region deployment, redundancy            |
| **Performance**  | Caching, async processing, CDN                 |
| **Consistency**  | CAP tradeoffs, eventual consistency            |
| **Security**     | Rate limiting, authentication, data encryption |

---

### 🔹 **7. Identify Bottlenecks & Trade-Offs**

Think critically:

* What could fail?
* Where are your performance or scaling limits?
* What would you improve with more time or budget?

📘 Examples:

* Trade-off between speed (cache) and freshness (real-time DB)
* Eventual consistency vs. strong consistency in a chat app

---

### 🔹 **8. (Optional) Dive into Low-Level Design (LLD)**

If time permits or interviewer asks:

* Show schema design
* Data model and API endpoints
* Algorithms (e.g., Base62 encoding for URL shortening)

---

### ✅ Final Checklist

| Step                   | Description                  |
| ---------------------- | ---------------------------- |
| ✅ Clarify Requirements | Don’t assume—ask!            |
| ✅ Define Scope         | Focus on core use case       |
| ✅ Estimate Scale       | Users, traffic, storage      |
| ✅ High-Level Design    | Components & flow            |
| ✅ Detail Components    | Each block with reasoning    |
| ✅ Address NFRs         | Scale, availability, latency |
| ✅ Consider Tradeoffs   | Bottlenecks, limitations     |
| ✅ LLD (Optional)       | Schema, APIs, algorithms     |

---

### ✅ Example in Action: Designing a Scalable Chat App

**Clarify**: 1-on-1 chat or group? Message delivery guarantee?
**Scope**: Start with 1-on-1 messaging
**Scale**: 10M users, 50K active at peak
**HLD**: Client → Load Balancer → Chat Service → DB + Queue
**DB**: NoSQL for fast writes, time-ordered chat messages
**Queue**: Kafka to process async message delivery
**Cache**: Redis for most recent chats
**Trade-offs**: Eventual consistency in group message delivery

---

### ✅ Interview Tip

Speak your thoughts **clearly and confidently**. Even if your final design isn’t perfect, showing a logical, step-by-step approach will impress interviewers.

---

## 4. What is the difference between HLD and LLD?

Understanding the difference between **HLD (High-Level Design)** and **LLD (Low-Level Design)** is essential for system design interviews, software architecture discussions, and team collaboration.

---

## ✅ **Difference Between HLD and LLD**

| Feature          | **High-Level Design (HLD)**                          | **Low-Level Design (LLD)**                          |
| ---------------- | ---------------------------------------------------- | --------------------------------------------------- |
| **Definition**   | Overview of the system’s architecture and components | Detailed design of components, logic, and data flow |
| **Focus**        | *What* the system does                               | *How* each part works                               |
| **Audience**     | Architects, senior developers, stakeholders          | Developers and implementation teams                 |
| **Detail Level** | Abstract, broad                                      | Detailed, specific                                  |
| **Scope**        | System-level design                                  | Component/class/module-level design                 |
| **Diagrams**     | System architecture, component diagrams, data flow   | Class diagrams, sequence diagrams, state diagrams   |
| **Output**       | Blueprint of the entire system                       | Design docs for actual implementation               |

---

## ✅ **Example: Designing a URL Shortener**

Let’s say the task is to design something like `bit.ly`.

---

### 🔷 High-Level Design (HLD)

* **Goal**: Show how the whole system fits together.
* **Components**:

    * API Gateway / Load Balancer
    * Web Servers / Application Layer
    * Database (SQL or NoSQL)
    * Cache Layer (e.g., Redis)
    * Analytics Module (optional)
    * CDN (for static content)

📘 **Architecture Diagram**:

```
Client → Load Balancer → Web Server → Cache → DB
```

**Questions addressed in HLD**:

* What are the services involved?
* How does traffic flow through the system?
* How is scalability achieved?
* Which technology stack is used?

---

### 🔷 Low-Level Design (LLD)

* **Goal**: Go deeper into internal logic and class-level design.
* **Details**:

    * How is the short URL generated?
    * Data structures and algorithms used
    * Class design for services (URLService, DatabaseHandler)
    * API contracts (input/output formats)
    * DB schema

📘 **Sample URLService class**:

```java
class URLService {
    Map<String, String> urlMap;

    String shortenURL(String longUrl) {
        String shortKey = generateKey(longUrl);
        urlMap.put(shortKey, longUrl);
        return "http://short.ly/" + shortKey;
    }

    String expandURL(String shortKey) {
        return urlMap.get(shortKey);
    }

    String generateKey(String longUrl) {
        // base62 hash of URL + random salt
    }
}
```

📘 **Sample Table Schema**:

| Field       | Type     | Description           |
| ----------- | -------- | --------------------- |
| short\_key  | VARCHAR  | The unique short code |
| long\_url   | TEXT     | Original long URL     |
| created\_at | DATETIME | Time of creation      |

---

## ✅ Summary Table

| Aspect  | HLD                         | LLD                               |
| ------- | --------------------------- | --------------------------------- |
| View    | Bird’s eye view             | Microscope view                   |
| Purpose | Architecture and components | Logic and internal implementation |
| Level   | System-wide                 | Module/class/function-level       |
| Used by | Architects, designers       | Developers                        |
| Output  | Diagrams and tech stack     | Code design, DB schemas, APIs     |

---

## ✅ Final Thought

Think of **HLD as the map of a city**, and **LLD as the blueprint of each building** in that city. Both are crucial, but they serve different stages and audiences.

---

## 5. What are scalability, availability, and reliability?

These three terms—**scalability**, **availability**, and **reliability**—are **core system design concepts**. They’re often discussed together because they impact how your system performs under stress and over time.

---

## ✅ **1. Scalability**

### 🔹 Definition:

**Scalability** is the system's ability to **handle increased load** (users, traffic, data) **without degrading performance**.

### 🔹 Types:

* **Vertical Scaling**: Increase capacity of a single machine (e.g., more RAM, CPU).
* **Horizontal Scaling**: Add more machines (e.g., add 10 more servers to handle users).

### 🔹 Example:

If your app handles 1,000 users now, and you want it to handle 1 million users with the same speed—your system must be scalable.

### 🔹 Real-world Analogy:

Adding more cashiers at a store during a holiday sale.

---

## ✅ **2. Availability**

### 🔹 Definition:

**Availability** is the percentage of time a system is **operational and accessible** to users.

### 🔹 Common Targets:

* 99.9% (“three nines”) = \~8.7 hours downtime/year
* 99.99% (“four nines”) = \~52 minutes downtime/year

### 🔹 How to achieve:

* Use **load balancers** and **failover** mechanisms
* Deploy across **multiple regions/zones**
* Have **redundant systems** (if one fails, others take over)

### 🔹 Example:

If your service is down for 30 minutes during the day, it's not highly available.

### 🔹 Real-world Analogy:

A 24/7 hospital that always has backup doctors on call.

---

## ✅ **3. Reliability**

### 🔹 Definition:

**Reliability** is the system's ability to **perform correctly and consistently** over time, **even in the face of failures**.

### 🔹 Key traits:

* No data loss
* No corrupted results
* Can recover gracefully after crashes

### 🔹 How to improve:

* Implement **retry mechanisms**
* Use **replication**, **checksums**, **data validation**
* Add **monitoring and alerting**

### 🔹 Example:

A payment gateway that always processes the correct amount, even if a network glitch happens mid-transaction.

### 🔹 Real-world Analogy:

A train that always arrives on time and never skips a stop.

---

## ✅ Summary Table

| Term             | Definition                                 | Goal                          | Techniques Used                         |
| ---------------- | ------------------------------------------ | ----------------------------- | --------------------------------------- |
| **Scalability**  | Ability to handle growing load             | Performance under growth      | Load balancer, sharding, autoscaling    |
| **Availability** | System is up and running when needed       | Minimize downtime             | Redundancy, failover, multi-zone deploy |
| **Reliability**  | System performs consistently and correctly | Correct and consistent output | Retry logic, replication, validation    |

---

## ✅ How They Work Together

Let’s say you’re building a **banking app**:

* It should **scale** during Black Friday when user traffic spikes (scalability).
* It should **stay up 24/7** so people can access funds anytime (availability).
* It should **never lose or misplace money**, even during a crash (reliability).

---

## ✅ In Interviews

When designing a system, always discuss:

* How it **scales** (e.g., via horizontal scaling, stateless services)
* How it remains **available** (e.g., using redundant services, health checks)
* How it stays **reliable** (e.g., through idempotency, error handling)

---

## 6. What is load balancing and how does it work?

**Load balancing** is a foundational concept in system design and is critical for building **scalable**, **highly available**, and **reliable** systems.

---

## ✅ What is Load Balancing?

**Load balancing** is the process of distributing **incoming network traffic** across multiple **servers or resources** to ensure:

* No single server is overwhelmed
* Requests are handled efficiently
* High availability and fault tolerance

---

## ✅ Why is Load Balancing Important?

Without load balancing:

* One server might get all traffic → becomes a bottleneck
* Leads to slow response times or crashes
* Hard to scale or ensure uptime

---

## ✅ How Does Load Balancing Work?

A **Load Balancer** sits between the client and the backend servers.

```
Clients
   ↓
[ Load Balancer ]
   ↓      ↓      ↓
App1   App2   App3
```

### 🔹 Basic Workflow:

1. Client makes a request.
2. Load balancer receives it.
3. It selects a backend server using a **load balancing algorithm**.
4. Forwards the request to that server.
5. Sends the server’s response back to the client.

---

## ✅ Load Balancing Algorithms

Here are common strategies used by load balancers:

| Algorithm                | Description                                             |
| ------------------------ | ------------------------------------------------------- |
| **Round Robin**          | Rotates requests evenly across servers                  |
| **Least Connections**    | Chooses the server with the fewest active connections   |
| **IP Hash**              | Assigns client to a server based on hash of IP          |
| **Weighted Round Robin** | Assigns more traffic to powerful servers                |
| **Random**               | Chooses a server randomly (often used with other logic) |

📘 **Example**:
If there are 3 servers, and you're using round robin:

```
Request 1 → Server A  
Request 2 → Server B  
Request 3 → Server C  
Request 4 → Server A (and so on)
```

---

## ✅ Types of Load Balancers

| Type               | Example           | Use Case                  |
| ------------------ | ----------------- | ------------------------- |
| **Hardware-based** | F5, Cisco         | Large enterprise networks |
| **Software-based** | NGINX, HAProxy    | Web apps, microservices   |
| **Cloud-based**    | AWS ELB, Azure LB | Scalable cloud apps       |

---

## ✅ Load Balancer Types by Layer

| Type                      | Works at                           | Example        |
| ------------------------- | ---------------------------------- | -------------- |
| **Layer 4 (Transport)**   | TCP/UDP level                      | AWS NLB        |
| **Layer 7 (Application)** | HTTP/HTTPS (inspect URLs, headers) | AWS ALB, NGINX |

---

## ✅ Features Load Balancers Often Include

* **Health Checks**: Sends pings to backend servers to check if they're alive. Dead ones are skipped.
* **Sticky Sessions**: Ensures a client is always routed to the same server (used in stateful apps).
* **SSL Termination**: Handles HTTPS decryption to offload backend servers.
* **Failover**: If a server fails, traffic is rerouted to healthy servers.

---

## ✅ Real-World Analogy

Imagine a ticket counter at a movie theater:

* Instead of everyone going to one counter (causing delay),
* A manager (load balancer) tells each person to go to the shortest queue,
* So the lines move faster and no single counter is overwhelmed.

---

## ✅ Summary

| Aspect                | Description                                     |
| --------------------- | ----------------------------------------------- |
| **Purpose**           | Distribute traffic across multiple servers      |
| **Benefits**          | Scalability, fault tolerance, high availability |
| **Common Algorithms** | Round Robin, Least Connections, IP Hash         |
| **Used in**           | Web apps, APIs, microservices, databases        |
| **Tools**             | NGINX, HAProxy, AWS ELB, Azure Load Balancer    |

---

## ✅ Interview Tip

Always mention **load balancing** when designing systems that:

* Serve many users
* Require high availability
* Need horizontal scaling

---

## 7. What is horizontal vs vertical scaling?

Understanding **horizontal** vs **vertical scaling** is crucial when designing scalable systems. These are the two main strategies for increasing a system’s capacity to handle more load (users, requests, data, etc.).

---

## ✅ **1. Vertical Scaling (Scale Up)**

### 🔹 Definition:

Adding **more power** (CPU, RAM, storage) to an **existing machine**.

### 🔹 Characteristics:

* Easier to implement initially
* Limited by the maximum capacity of a single machine
* Often leads to **downtime** when upgrading
* Simpler software architecture

### 🔹 Example:

Upgrading a server from:

* 8 CPU cores → 32 cores
* 32 GB RAM → 128 GB RAM

📘 If your database is slow, you might upgrade the instance from `db.m5.large` to `db.m5.4xlarge`.

---

## ✅ **2. Horizontal Scaling (Scale Out)**

### 🔹 Definition:

Adding **more machines/instances** to your system to distribute the load.

### 🔹 Characteristics:

* Supports **unlimited growth** (in theory)
* Requires **distributed system design**
* Usually more **complex** (load balancers, data partitioning)
* Better for high availability and fault tolerance

### 🔹 Example:

Going from:

* 1 server → 5 servers behind a load balancer
* 1 database shard → 10 shards with partitioned data

📘 In a web application, you add more application servers and use a **load balancer** to distribute traffic among them.

---

## ✅ Summary Table

| Feature               | **Vertical Scaling**         | **Horizontal Scaling**               |
| --------------------- | ---------------------------- | ------------------------------------ |
| **Definition**        | Add more power to one server | Add more servers to handle load      |
| **Cost Efficiency**   | More expensive at scale      | More efficient in the long run       |
| **Complexity**        | Simpler                      | More complex (distributed system)    |
| **Downtime**          | Often requires restart       | No downtime needed                   |
| **Scalability Limit** | Limited by machine capacity  | Theoretically unlimited              |
| **Example**           | Upgrade server to 64 GB RAM  | Add more web servers + load balancer |
| **Best for**          | Small to medium loads        | Large-scale, cloud-native systems    |

---

## ✅ Real-World Analogy

### 📶 Vertical Scaling:

Like upgrading a single restaurant to have more kitchen equipment and more seating.

### 🏢 Horizontal Scaling:

Like opening more restaurant branches to serve more customers in parallel.

---

## ✅ When to Use Which?

| Scenario                                         | Strategy                       |
| ------------------------------------------------ | ------------------------------ |
| Quick fix or small load                          | ✅ Vertical scaling             |
| System already distributed (e.g., microservices) | ✅ Horizontal scaling           |
| Need fault tolerance & high availability         | ✅ Horizontal scaling           |
| Budget-constrained project or prototype          | ✅ Vertical scaling (initially) |

---

## ✅ In Interviews

You should always:

* **Mention both** strategies when discussing system scalability.
* Explain that **horizontal scaling is preferred** for modern, large-scale, fault-tolerant systems.
* Discuss how you'll use **load balancers, stateless services, sharded databases** for horizontal scaling.

---

## 8. Explain stateless vs stateful services.

This is a fundamental concept in **system design** and **distributed computing**, and often comes up in interviews!

---

## ✅ **Stateless vs Stateful Services**

| Aspect                    | **Stateless Service**                                     | **Stateful Service**                                              |
| ------------------------- | --------------------------------------------------------- | ----------------------------------------------------------------- |
| **Definition**            | Doesn’t store data about client sessions between requests | Stores session or context between requests                        |
| **Client Responsibility** | Client sends all necessary info with each request         | Client relies on server to remember context                       |
| **Scalability**           | Highly scalable and easy to distribute                    | Harder to scale, requires sticky sessions or session replication  |
| **Fault Tolerance**       | Easier to recover (can hit any server)                    | Harder to recover (needs to maintain session state)               |
| **Load Balancing**        | Easy (any server can handle any request)                  | Needs sticky sessions or external session storage                 |
| **Examples**              | REST APIs, microservices, stateless authentication        | Databases, chat servers, shopping carts (without session storage) |

---

## ✅ 1. What is a **Stateless Service**?

A **stateless service** does **not retain any information** about the client between requests.

* Each request is **independent**.
* Server treats every request as if it’s coming for the **first time**.
* All context must be provided by the **client or request** itself.

### 🔹 Example:

A RESTful API:

```http
GET /user/123
Authorization: Bearer <token>
```

Each request must include **authentication data**, because the server does **not remember** the user from earlier.

📘 Common in:

* REST APIs
* Microservices
* Cloud-native applications

---

## ✅ 2. What is a **Stateful Service**?

A **stateful service** maintains **client session state** across multiple requests.

* Server remembers things like user login, shopping cart, etc.
* Good for interactive systems but more complex to scale.

### 🔹 Example:

A multiplayer game server that keeps track of each player’s position, score, etc., between requests.

Or:
A traditional web app where user login session is stored on the server:

```http
GET /dashboard
Cookie: sessionId=abc123
```

The server **remembers** `sessionId=abc123` is Alice’s logged-in session.

📘 Common in:

* Web sessions with server-side storage
* Databases
* Chat applications
* Game servers

---

## ✅ Summary Table

| Feature              | Stateless                      | Stateful                         |
| -------------------- | ------------------------------ | -------------------------------- |
| Session tracking     | Not retained                   | Retained                         |
| Request independence | Each is independent            | Depends on previous requests     |
| Failure recovery     | Easy (just reroute request)    | Hard (may lose session)          |
| Scalability          | Easy (no session sync needed)  | Complex (needs sticky sessions)  |
| Typical use cases    | REST APIs, microservices, CDNs | Databases, games, real-time apps |

---

## ✅ Real-World Analogy

### 📭 Stateless:

A vending machine. Every user interaction is independent. Insert money → get item. It doesn’t remember who you are.

### 🧑‍💻 Stateful:

A restaurant waiter. Remembers your order, your table, and whether you asked for the check.

---

## ✅ Best Practice

In **modern distributed systems**, services are typically designed to be **stateless** for:

* **Scalability**
* **Fault tolerance**
* **Ease of deployment**

When **state is required**, it’s **externalized** to:

* A database
* A distributed cache (like Redis)
* A session store

---

## ✅ In Interviews

* Always **prefer stateless** architecture where possible
* Explain how you'll **externalize state** (e.g., store user session in Redis)
* For stateful systems, explain how you'll handle **scaling**, **session replication**, and **failover**

---

## 9. What is a CDN and how does it improve performance?

A **CDN** (Content Delivery Network) is a **core component** of modern web and system design. It significantly improves **performance**, **availability**, and **scalability**, especially for **static content**.

---

## ✅ What is a CDN?

A **Content Delivery Network (CDN)** is a **geographically distributed network of servers** that deliver web content (like images, CSS, JavaScript, videos) to users **based on their location**.

---

## ✅ Why Use a CDN?

Without a CDN:

* All users (whether from India, USA, or Europe) fetch content from a **single origin server**
* Results in **slower load times**, especially for faraway users
* Increased load on the origin server

With a CDN:

* Content is **cached** on edge servers near users
* Requests are served from the **closest location**, not your main server
* Reduces **latency**, **bandwidth usage**, and **server load**

---

## ✅ How a CDN Works (Step-by-Step)

1. A user requests a file (e.g., an image).
2. The browser asks the **nearest CDN edge server** for that file.
3. If the file is cached (✅ **cache hit**), the CDN serves it directly — **very fast**.
4. If not cached (❌ **cache miss**), the CDN fetches it from your **origin server**, stores it locally, and delivers it.
5. Future users near that edge server now get the cached version.

---

## ✅ Benefits of Using a CDN

| Feature                          | Benefit                                               |
| -------------------------------- | ----------------------------------------------------- |
| 🌍 **Geographical distribution** | Serves content closer to the user                     |
| ⚡ **Faster loading times**       | Reduces latency and improves user experience          |
| 📉 **Offloads origin server**    | Handles static content so your backend is less loaded |
| 🔄 **Improved scalability**      | Can absorb massive traffic (e.g., viral video)        |
| 🔐 **Security features**         | Protects against DDoS attacks, adds TLS/SSL           |
| 🔁 **Caching**                   | Stores content to avoid repeated data fetches         |
| 🚨 **Fault tolerance**           | If one node fails, others take over automatically     |

---

## ✅ Common Use Cases

* **Images, videos, JS, CSS**
* **Software downloads**
* **Static HTML pages**
* **APIs (read-heavy public APIs)**
* **Live streaming or VOD**

---

## ✅ Real-World Analogy

Imagine you're delivering pizza.
Without a CDN: All orders are cooked and delivered from your central kitchen in New York — slow for someone in Tokyo.
With a CDN: You have kitchens (edge servers) all around the world. Tokyo users get it from a local branch — fast!

---

## ✅ Example: Cloudflare CDN

If you use **Cloudflare**, it can:

* Cache your entire website globally
* Act as a **reverse proxy**
* Protect against attacks
* Optimize images, minify scripts, and even serve stale content if your origin is down

---

## ✅ In Interviews

When designing a web system or app (e.g., YouTube, Instagram, news site), always mention:

* Use of CDN to cache:

    * Images
    * Videos
    * JS/CSS
    * Static HTML pages
* Benefits for **performance**, **latency**, and **cost savings**

---

## ✅ Bonus: Popular CDNs

| CDN Provider          | Notes                             |
| --------------------- | --------------------------------- |
| **Cloudflare**        | CDN + security, DNS, firewall     |
| **Akamai**            | Enterprise-grade, very reliable   |
| **Amazon CloudFront** | Integrated with AWS               |
| **Fastly**            | Real-time caching, used by GitHub |
| **Google Cloud CDN**  | Integrated with Google Cloud      |

---

## ✅ Diagram

```
User (India)
   ↓
Nearest Edge Server (Mumbai - CDN)
   ↓
[Cached?] → Yes → Fast delivery
         → No  → Fetch from Origin Server (e.g., US)
```

---

## 10. What are the different types of databases and when to use each?

Choosing the right **database type** is crucial to building efficient, scalable systems. Different types of databases are designed to solve different problems, and each has trade-offs.

---

## ✅ Major Types of Databases

| Type                             | Description                                                           | When to Use                                                                                               | Examples                                                                      |
| -------------------------------- | --------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| **Relational Databases (RDBMS)** | Structured data stored in tables with fixed schemas and relationships | Use when data is structured, transactional, and requires strong consistency                               | MySQL, PostgreSQL, Oracle, SQL Server                                         |
| **NoSQL Databases**              | Schema-less or flexible schema, non-relational                        | Use when dealing with large volumes of unstructured or semi-structured data or needing horizontal scaling | MongoDB (Document), Cassandra (Wide-column), Redis (Key-value), Neo4j (Graph) |
| **In-Memory Databases**          | Store data primarily in RAM for ultra-fast access                     | Use for caching, session management, real-time analytics                                                  | Redis, Memcached                                                              |
| **Graph Databases**              | Store data as nodes and edges, focusing on relationships              | Use for social networks, recommendation engines, fraud detection                                          | Neo4j, Amazon Neptune                                                         |
| **Time-Series Databases**        | Optimized for timestamped data (time series)                          | Use for monitoring, IoT, financial data                                                                   | InfluxDB, TimescaleDB                                                         |
| **Object-Oriented Databases**    | Store data as objects (like in programming)                           | Use in complex applications where data is naturally represented as objects                                | db4o, ObjectDB                                                                |
| **NewSQL Databases**             | Combine SQL relational model with horizontal scaling                  | Use for scalable transactional systems requiring strong consistency                                       | Google Spanner, CockroachDB                                                   |

---

## ✅ Detailed Breakdown

### 1. **Relational Databases (RDBMS)**

* Store data in **tables** with rows and columns.
* Use **SQL** for queries.
* Support **ACID** transactions (Atomicity, Consistency, Isolation, Durability).
* Strong schema enforcement.

**Use cases:**

* Banking systems
* E-commerce order management
* Inventory systems

---

### 2. **NoSQL Databases**

* Flexible schemas, can store JSON-like documents, key-value pairs, graphs, or wide-column.
* Easier to **scale horizontally**.
* Often provide **eventual consistency** instead of strict ACID.

**Subtypes:**

* **Document stores:** MongoDB, Couchbase (store JSON documents)
* **Key-value stores:** Redis, DynamoDB (fast lookups)
* **Wide-column stores:** Cassandra, HBase (large distributed datasets)
* **Graph databases:** Neo4j, JanusGraph (complex relationships)

**Use cases:**

* Content management systems
* Big data and analytics
* Real-time messaging apps

---

### 3. **In-Memory Databases**

* Keep data in RAM for **very low latency**.
* Used for **caching** and **session stores**.

**Use cases:**

* Caching layer (to speed up DB queries)
* Real-time bidding systems
* Leaderboards, counters

---

### 4. **Graph Databases**

* Represent data as nodes (entities) and edges (relationships).
* Query with graph traversal languages (Cypher, Gremlin).

**Use cases:**

* Social networks
* Fraud detection
* Recommendation engines

---

### 5. **Time-Series Databases**

* Optimized for **high write throughput** and **time-based queries**.
* Efficient for storing and querying **timestamped data**.

**Use cases:**

* Monitoring and logging systems (Prometheus)
* IoT sensor data
* Stock market data

---

## ✅ When to Use What? (Examples)

| Scenario                                | Recommended Database Type      |
| --------------------------------------- | ------------------------------ |
| Transactional system with complex joins | Relational (PostgreSQL, MySQL) |
| Large-scale user profile storage        | Document store (MongoDB)       |
| Real-time chat app caching              | Key-value store (Redis)        |
| Social graph & recommendations          | Graph DB (Neo4j)               |
| IoT sensor data collection              | Time-series DB (InfluxDB)      |
| Highly scalable, distributed writes     | Wide-column store (Cassandra)  |

---

## ✅ Interview Tip

* Always clarify the **data model**, **consistency requirements**, and **scale** when choosing a database.
* Mention trade-offs between **consistency, availability, and partition tolerance** (CAP theorem).
* Show awareness of **polyglot persistence** — using multiple database types in the same system for different needs.

---

## 11. What is eventual consistency vs strong consistency?

Understanding **eventual consistency** vs **strong consistency** is key to designing distributed systems and databases, especially in large-scale or cloud architectures.

---

## ✅ What is **Strong Consistency**?

* **Definition:** After a write completes, **all subsequent reads** will return the **most recent write**.
* In other words, **everyone sees the same data at the same time**.
* Guarantees **linearizability** or **serializability** — strict ordering of operations.

### 🔹 Example:

* You update your profile picture on a social network.
* Immediately after, when you or anyone else views your profile, the **new picture** is shown everywhere.

### 🔹 Use cases:

* Banking systems (account balance must be accurate)
* Inventory management (no overselling)
* Payment processing

---

## ✅ What is **Eventual Consistency**?

* **Definition:** The system guarantees that, **if no new updates are made**, eventually **all reads will return the last updated value**.
* However, at any point in time, some reads may return **stale or outdated data**.
* Allows **temporary inconsistencies** to achieve **high availability and partition tolerance**.

### 🔹 Example:

* You update your profile picture on a social network.
* For a short time, some users may still see the old picture.
* After some delay (seconds, minutes), all users see the updated picture.

### 🔹 Use cases:

* DNS systems
* Large-scale social media feeds
* Distributed caches
* Systems prioritizing availability over immediate consistency (e.g., Amazon DynamoDB, Cassandra)

---

## ✅ Why Use Eventual Consistency?

* To improve **availability** and **partition tolerance** (CAP theorem).
* To support **highly distributed systems** across regions.
* Reduces write latency by not waiting for all replicas to update before acknowledging.

---

## ✅ Comparison Table

| Aspect              | Strong Consistency              | Eventual Consistency                  |
| ------------------- | ------------------------------- | ------------------------------------- |
| Data freshness      | Always up-to-date               | May be stale temporarily              |
| Read after write    | Immediate                       | May be delayed                        |
| System availability | Lower during network partitions | Higher, can operate during partitions |
| Latency             | Higher (waits for all replicas) | Lower (returns immediately)           |
| Complexity          | Higher                          | Lower                                 |
| Use cases           | Financial, booking systems      | Social feeds, caching, DNS            |

---

## ✅ Real-World Analogy

* **Strong consistency:** You and your friends all see the exact same movie scene at the same time.
* **Eventual consistency:** You’re watching a live stream with some delay; eventually, everyone catches up to the same scene.

---

## ✅ Interview Tip

* Understand and explain the **CAP theorem** trade-offs (Consistency, Availability, Partition tolerance).
* Mention how systems like **Cassandra** and **DynamoDB** choose eventual consistency to favor availability.
* Discuss how **strong consistency** often comes with higher latency and less availability during failures.

---

## 12. What is a message queue and when would you use one?

**Message queues** are fundamental building blocks in modern distributed and scalable systems, so understanding them well will help you shine in system design interviews.

---

## ✅ What is a **Message Queue**?

A **message queue** is a **middleware** component that enables **asynchronous communication** between different parts (services or components) of a system.

* It works like a **buffer** or **pipeline** where messages (data packets) are stored temporarily.
* Producers (senders) put messages into the queue.
* Consumers (receivers) take messages from the queue and process them.
* This decouples the sender and receiver in time and space.

---

## ✅ Key Characteristics

* **Asynchronous:** Sender does not wait for the receiver to process the message.
* **Decoupling:** Sender and receiver can operate independently.
* **Durability:** Messages are stored reliably until consumed.
* **Ordering:** Some queues preserve message order.
* **Scalability:** Multiple consumers can process messages in parallel.
* **Reliability:** Supports retries and dead-letter queues for failed messages.

---

## ✅ Why Use a Message Queue?

| Reason                            | Explanation                                                                           |
| --------------------------------- | ------------------------------------------------------------------------------------- |
| **Decoupling**                    | Allows services to operate independently without needing to be online simultaneously. |
| **Load leveling**                 | Smooths out spikes in traffic by buffering requests and processing at steady pace.    |
| **Asynchronous processing**       | Long-running tasks can be done in background without blocking users.                  |
| **Scalability**                   | Multiple consumers can be added to process messages concurrently.                     |
| **Reliability & fault tolerance** | Ensures messages aren’t lost and can be retried on failure.                           |

---

## ✅ Common Use Cases

* **Order processing:** When a user places an order, the order service places a message in the queue, and other services like inventory, payment, and shipping consume and process asynchronously.
* **Email notifications:** Email sending can be queued and processed without slowing down the main user flow.
* **Log aggregation:** Multiple services send logs to a queue which a centralized processor consumes and stores.
* **Microservices communication:** Services communicate asynchronously through queues instead of direct synchronous calls.
* **Data pipelines:** Events from one system flow through queues to analytics or monitoring systems.

---

## ✅ Example Architecture

```
User → Web Server → (Push message) → Message Queue → Worker Service (Consumer) → Process task
```

* User submits a request.
* Web server quickly acknowledges and pushes a message to the queue.
* Worker services consume messages from the queue and handle processing (e.g., sending email, resizing images).

---

## ✅ Popular Message Queue Systems

| System           | Characteristics                                              |
| ---------------- | ------------------------------------------------------------ |
| **RabbitMQ**     | AMQP protocol, supports complex routing, reliable delivery   |
| **Apache Kafka** | Distributed streaming platform, high throughput, durable log |
| **Amazon SQS**   | Fully managed, simple to use, scalable                       |
| **ActiveMQ**     | Supports JMS, widely used in Java ecosystems                 |

---

## ✅ Interview Tip

* Explain how message queues help **scale systems** and improve **reliability**.
* Discuss trade-offs between **synchronous** vs **asynchronous** communication.
* Mention **idempotency** concerns (handling duplicate messages).
* Explain retry and dead-letter queue handling for failed message processing.

---

## 13. How does caching work and where would you implement it?

Caching is a fundamental technique to boost system performance and scalability, so it’s a very common topic in interviews.

---

## ✅ What is **Caching**?

Caching is the process of **storing copies of data** in a **fast-access layer** (cache) so future requests for that data can be served **faster** without hitting the slower original data source (like a database or API).

---

## ✅ How Does Caching Work?

1. **Request comes in** → Check if data is in the cache (called a **cache hit**).
2. If **yes**, return data immediately (fast!).
3. If **no** (called a **cache miss**), fetch data from the original source (database, API).
4. Store the fetched data in the cache for future requests.
5. Return the data to the client.

---

## ✅ Types of Caches

| Cache Type            | Description                          | Examples               |
| --------------------- | ------------------------------------ | ---------------------- |
| **In-memory cache**   | Stored in RAM for super-fast access  | Redis, Memcached       |
| **Browser cache**     | Stored on client-side                | HTTP cache headers     |
| **CDN cache**         | Caches static assets at edge servers | Cloudflare, Akamai     |
| **Application cache** | Cache inside the app or server       | Local caches in memory |

---

## ✅ Where Would You Implement Caching?

### 1. **Database Query Cache**

* Cache results of expensive database queries.
* Avoid repetitive DB hits for same queries.

### 2. **API Response Cache**

* Cache responses from slow APIs.
* Useful for public APIs or microservices.

### 3. **Page Cache / Template Cache**

* Cache rendered HTML pages or parts of pages in web apps.
* Improves user-perceived performance.

### 4. **CDN Cache**

* Cache static assets like images, CSS, JavaScript near users globally.
* Reduces latency and bandwidth usage.

### 5. **Session Cache**

* Store user session data in a fast in-memory store.
* Avoids DB lookups on every request.

---

## ✅ Cache Invalidation

One of the toughest problems: **How and when to update or remove stale data?**

* **Time-based expiration (TTL):** Cache entries expire after a fixed time.
* **Manual invalidation:** App explicitly removes or updates cache on data change.
* **Write-through cache:** Updates cache and DB simultaneously.
* **Write-back cache:** Updates cache first, then asynchronously writes to DB.

---

## ✅ Benefits of Caching

* **Faster response times** → improved user experience
* **Reduced load** on databases and backend services
* **Lower latency** especially for read-heavy workloads
* **Better scalability** handling more traffic efficiently

---

## ✅ Example Flow with Cache

```
Client Request → Check Cache → Cache Hit? → Return Data (fast)
                    ↓ No
              Query Database → Store Result in Cache → Return Data
```

---

## ✅ Interview Tip

* Mention **trade-offs**: caching improves speed but adds complexity (cache invalidation).
* Talk about **cache coherence** in distributed systems.
* Explain how to **handle cache misses** and **thundering herd problem** (many clients querying simultaneously when cache expires).
* Discuss tools like **Redis** or **Memcached** for distributed caching.

---

## 14. Explain CAP theorem and real-world trade-offs.

The **CAP theorem** is fundamental in distributed system design and is often a key discussion point in interviews.

---

## ✅ What is the CAP Theorem?

CAP theorem, formulated by Eric Brewer, states that in a **distributed data system**, you can only guarantee **two out of the following three** properties simultaneously:

| Property                    | Meaning                                                                                                  |
| --------------------------- | -------------------------------------------------------------------------------------------------------- |
| **Consistency (C)**         | Every read receives the most recent write or an error (strong consistency).                              |
| **Availability (A)**        | Every request receives a (non-error) response, without guarantee that it contains the most recent write. |
| **Partition Tolerance (P)** | The system continues to operate despite network partitions (communication failures between nodes).       |

---

## ✅ Why is this important?

* Distributed systems inevitably face **network partitions** due to network failures or latency.
* When a partition happens, the system must choose to either:

    * **Remain consistent but risk unavailability** (reject some requests),
    * **Remain available but risk inconsistency** (serve stale data).

---

## ✅ Breakdown of the Three Properties

| Property                | Explanation                                                                        |
| ----------------------- | ---------------------------------------------------------------------------------- |
| **Consistency**         | All nodes see the same data at the same time (strong consistency).                 |
| **Availability**        | Every request gets a response (success or failure), no request hangs or times out. |
| **Partition Tolerance** | The system keeps functioning despite network splits or message loss between nodes. |

---

## ✅ The Trade-offs

* You **cannot** have all three at once in a distributed system.
* You must pick two:

| System Choice                               | Result                                                                     | Example Systems                                         |
| ------------------------------------------- | -------------------------------------------------------------------------- | ------------------------------------------------------- |
| **CA (Consistency + Availability)**         | System works well if no network partitions. Not partition-tolerant.        | Traditional RDBMS (single node or tightly coupled)      |
| **CP (Consistency + Partition tolerance)**  | System sacrifices availability during partitions (some requests rejected). | HBase, MongoDB (when configured for strong consistency) |
| **AP (Availability + Partition tolerance)** | System sacrifices consistency (may serve stale data).                      | Cassandra, DynamoDB, Couchbase                          |

---

## ✅ Real-World Examples

### 1. **Banking System (CP)**

* Must never show wrong balances (Consistency).
* Can afford to reject or delay some requests during network issues (Availability).
* Partition tolerance is necessary in distributed setups.

### 2. **Social Media Feed (AP)**

* Users can tolerate slightly stale feeds (Eventual Consistency).
* System remains available during network partitions.
* Partition tolerance is a must.

### 3. **Traditional SQL Database (CA)**

* Single server or tightly coupled cluster ensures consistency and availability.
* But doesn’t handle network partitions well (if network breaks, service might go down).

---

## ✅ Why Partition Tolerance is a Must in Distributed Systems?

* Networks inevitably fail.
* Without partition tolerance, your system can't operate reliably in real-world networks.
* Hence, most modern distributed systems **choose between CP or AP**.

---

## ✅ Visual Summary

```
       Consistency
         /   \
       /       \
     CA         CP
      \         /
        \     /
      Partition Tolerance --- Availability
               \
                \
                 AP
```

---

## ✅ Interview Tip

* Always mention the **CAP theorem trade-offs** when designing distributed databases.
* Explain what your system prioritizes based on use case.
* Talk about **eventual consistency** in AP systems.
* Mention how modern databases provide **configurable consistency levels** (strong, eventual, causal).

---

## 15. What are microservices and how are they different from monoliths?

Understanding **microservices vs monoliths** is fundamental in modern software architecture.

---

## ✅ What are **Microservices**?

* Microservices are an architectural style where an application is broken down into **small, independent services**.
* Each microservice focuses on a **single business capability** and can be developed, deployed, and scaled independently.
* Microservices communicate with each other over **lightweight protocols** (usually HTTP/REST, gRPC, messaging).

---

## ✅ What is a **Monolithic Architecture**?

* A monolith is a **single unified application** where all components (UI, business logic, data access) are tightly integrated and run as one process.
* All features and services are packaged and deployed together.

---

## ✅ Key Differences

| Aspect               | Monolith                                 | Microservices                                       |
| -------------------- | ---------------------------------------- | --------------------------------------------------- |
| **Size**             | Large, single codebase                   | Small, focused services                             |
| **Deployment**       | Single deployable unit                   | Independently deployable services                   |
| **Development**      | Teams work on the same codebase          | Teams own separate services                         |
| **Scalability**      | Scale entire app as one                  | Scale individual services separately                |
| **Technology Stack** | Usually one tech stack                   | Different services can use different tech           |
| **Fault Isolation**  | Failure in one part may affect whole app | Failures isolated to single service                 |
| **Communication**    | Internal function calls                  | Network calls (REST, messaging)                     |
| **Complexity**       | Simple to develop initially              | More complex operationally (networking, monitoring) |
| **Data Management**  | Usually one shared database              | Each service owns its own database                  |

---

## ✅ Why Use Microservices?

* **Flexibility:** Use different technologies per service.
* **Independent Deployment:** Faster releases without impacting whole system.
* **Scalability:** Scale hot services independently.
* **Resilience:** Failure in one service doesn’t bring down entire system.
* **Team Autonomy:** Different teams can develop and own different services.

---

## ✅ When to Use Monolith?

* Simple applications or startups with small teams.
* When rapid initial development is needed.
* When operational complexity of microservices isn’t justified.

---

## ✅ Example Scenario

* **Monolith:** E-commerce site where product catalog, payment, user auth, and order processing are all part of one app.
* **Microservices:** Same e-commerce site but split into independent services like Product Service, Payment Service, Auth Service, Order Service.

---

## ✅ Interview Tip

* Talk about **trade-offs**: microservices improve scalability and agility but add complexity.
* Discuss challenges: service discovery, inter-service communication, data consistency, distributed tracing.
* Mention tools like **Docker**, **Kubernetes**, **API Gateway** that help manage microservices.

---

## 16. What is a reverse proxy and how is it used?

A **reverse proxy** is a key component in many web architectures and system designs.

---

## ✅ What is a **Reverse Proxy**?

A **reverse proxy** is a server that sits **between client requests and backend servers**. It **receives requests from clients** and **forwards them to one or more backend servers**. When backend servers respond, the reverse proxy sends the response back to the client.

---

## ✅ How is it Different from a Forward Proxy?

| Proxy Type        | Role                                                                     | Typical Use Case                              |
| ----------------- | ------------------------------------------------------------------------ | --------------------------------------------- |
| **Forward Proxy** | Acts on behalf of clients, forwarding their requests to the internet     | Used for client anonymity, filtering, caching |
| **Reverse Proxy** | Acts on behalf of servers, forwarding client requests to backend servers | Load balancing, security, caching             |

---

## ✅ Key Functions of a Reverse Proxy

1. **Load Balancing:** Distributes incoming client requests evenly across multiple backend servers to improve scalability and reliability.

2. **SSL Termination:** Handles HTTPS connections by decrypting SSL/TLS traffic, offloading this work from backend servers.

3. **Caching:** Stores responses to serve future requests faster, reducing load on backend servers.

4. **Security:** Acts as a shield by hiding backend server details and filtering malicious requests (e.g., rate limiting, web application firewall).

5. **Compression:** Compresses responses to reduce bandwidth usage.

6. **Static Content Serving:** Serves static files (images, CSS, JavaScript) directly, reducing backend load.

---

## ✅ Common Reverse Proxy Servers

* **Nginx**
* **HAProxy**
* **Apache HTTP Server (with mod\_proxy)**
* **Traefik**
* **AWS Elastic Load Balancer (ELB)**

---

## ✅ Example Flow

```
Client → Reverse Proxy → Backend Servers
        (Load Balancer, Caching, SSL termination)
```

* Client sends a request to the reverse proxy.
* Reverse proxy selects a backend server (based on load balancing policy).
* Sends the request to that backend server.
* Backend processes and responds.
* Reverse proxy forwards the response back to the client.

---

## ✅ Why Use a Reverse Proxy?

* **Improves scalability** by distributing load.
* **Enhances security** by hiding backend details and filtering requests.
* **Simplifies SSL management** by centralizing encryption/decryption.
* **Increases performance** via caching and compression.
* **Enables seamless upgrades** by routing traffic between different backend versions.

---

## ✅ Interview Tip

* Explain how reverse proxies help **decouple clients and servers**.
* Mention their role in **microservices architecture** for service discovery and routing.
* Discuss performance benefits (e.g., caching static assets).
* Give examples of tools and their typical use cases.

---

## 17. What are the key components of a fault-tolerant system?

Designing fault-tolerant systems is critical to building reliable and highly available services. Here’s a detailed explanation of the **key components** and concepts involved:

---

## ✅ What is a Fault-Tolerant System?

A **fault-tolerant system** continues to operate correctly even when some components fail. It minimizes downtime and ensures service reliability by detecting, isolating, and recovering from failures.

---

## ✅ Key Components of a Fault-Tolerant System

### 1. **Redundancy**

* **Definition:** Duplicate critical components or services so if one fails, others take over.
* **Examples:** Multiple servers (replicas), RAID storage arrays, backup power supplies.
* **Purpose:** Avoid single points of failure (SPOF).

### 2. **Failover Mechanism**

* **Definition:** Automatic switching to a standby component or system when failure is detected.
* **Examples:** Primary database failing over to a replica; active-passive clusters.
* **Purpose:** Minimize downtime by quick recovery.

### 3. **Health Monitoring and Failure Detection**

* **Definition:** Continuously check system components’ health.
* **Examples:** Heartbeat signals, health check APIs, monitoring tools (Prometheus, Nagios).
* **Purpose:** Detect faults early for timely intervention.

### 4. **Graceful Degradation**

* **Definition:** System continues operating with reduced functionality rather than complete failure.
* **Examples:** Serving cached content if DB is down, disabling non-critical features.
* **Purpose:** Maintain partial service availability.

### 5. **Data Replication and Backup**

* **Definition:** Keep copies of data in multiple locations.
* **Examples:** Database replication (master-slave, multi-master), backups.
* **Purpose:** Prevent data loss and support recovery.

### 6. **Timeouts and Retries**

* **Definition:** Set time limits for operations and retry failed attempts intelligently.
* **Examples:** Retry policies with exponential backoff.
* **Purpose:** Avoid system hangs and recover from transient failures.

### 7. **Circuit Breakers**

* **Definition:** Pattern that stops requests to a failing service to prevent cascading failures.
* **Examples:** Netflix Hystrix.
* **Purpose:** Protect overall system stability.

### 8. **Load Balancing**

* **Definition:** Distribute incoming traffic across multiple healthy instances.
* **Examples:** Reverse proxies like Nginx, hardware load balancers.
* **Purpose:** Avoid overload and spread risk.

---

## ✅ Real-World Example

* **Database cluster with master-slave replication:** If the master fails, failover automatically promotes a slave to master.
* **Microservices using circuit breakers:** If one service is down, others don’t get overwhelmed retrying calls endlessly.

---

## ✅ Summary Table

| Component               | Purpose                                    | Example Tools/Techniques     |
| ----------------------- | ------------------------------------------ | ---------------------------- |
| Redundancy              | Avoid single points of failure             | Multiple servers, RAID       |
| Failover                | Automatic recovery                         | Active-passive clusters      |
| Health Monitoring       | Early fault detection                      | Heartbeats, monitoring tools |
| Graceful Degradation    | Partial availability                       | Cache fallback               |
| Data Replication/Backup | Data safety and recovery                   | DB replication, backups      |
| Timeouts & Retries      | Prevent hangs and recover transient faults | Exponential backoff          |
| Circuit Breakers        | Prevent cascading failures                 | Hystrix, resilience4j        |
| Load Balancing          | Distribute load, avoid overload            | Nginx, HAProxy               |

---

## ✅ Interview Tip

* Explain **why each component matters** and how they work together.
* Discuss **trade-offs**, like cost vs complexity.
* Mention **monitoring and alerting** as vital to proactive fault management.
* Give examples from systems you know or have designed.

---

## 18. What is the difference between synchronous and asynchronous communication?

Understanding **synchronous vs asynchronous communication** is crucial in system design, especially for building scalable and responsive applications.

---

## ✅ What is **Synchronous Communication**?

* In synchronous communication, the **caller waits** for the called operation to complete and return a response before continuing.
* It’s a **blocking** interaction where both parties are active at the same time.
* Commonly used in traditional function calls, HTTP requests, and RPC (Remote Procedure Calls).

### Example:

* Client sends a request to a server.
* Client waits (blocks) until the server processes the request and sends back a response.
* Then the client continues.

---

## ✅ What is **Asynchronous Communication**?

* In asynchronous communication, the caller **does not wait** for an immediate response.
* The caller sends a request/message and continues its own work.
* The response or result is processed later, usually via callbacks, events, or message queues.
* It’s **non-blocking** and enables decoupling between sender and receiver.

### Example:

* Client sends a request to a server (e.g., places a message in a queue).
* Client immediately continues other tasks.
* Server processes the request independently and sends a response later.

---

## ✅ Key Differences

| Aspect                  | Synchronous                           | Asynchronous                                        |
| ----------------------- | ------------------------------------- | --------------------------------------------------- |
| **Blocking?**           | Yes                                   | No                                                  |
| **Waits for response?** | Yes                                   | No                                                  |
| **Coupling**            | Tight (caller & callee active)        | Loose (decoupled timing)                            |
| **Complexity**          | Simpler to implement and debug        | More complex (requires callbacks, message handling) |
| **Use cases**           | Real-time operations, simple APIs     | Long-running tasks, event-driven systems            |
| **Scalability**         | Can limit scalability due to blocking | Better scalability with concurrency                 |

---

## ✅ When to Use Which?

| Scenario                               | Recommendation                                |
| -------------------------------------- | --------------------------------------------- |
| Real-time user interactions            | Synchronous (e.g., login, form submit)        |
| Background tasks (e.g., email sending) | Asynchronous (via message queues)             |
| Service-to-service RPC calls           | Usually synchronous, unless latency sensitive |
| Event-driven architectures             | Asynchronous                                  |

---

## ✅ Interview Tip

* Explain with simple analogies (e.g., synchronous = phone call where you wait; asynchronous = leaving a voicemail and continuing your day).
* Discuss impact on **system design**, such as latency, resource utilization, and fault tolerance.
* Talk about technologies: REST (sync), Message Queues like Kafka, RabbitMQ (async).
* Mention challenges of async like handling retries, ordering, and eventual consistency.

---

## 19. How would you design a distributed logging system?

Designing a **distributed logging system** is a classic system design question that tests your understanding of scalability, reliability, and data processing in distributed environments. Here’s a detailed explanation with key components, challenges, and example architecture.

---

## 🎯 Goal of a Distributed Logging System

* Collect logs from multiple servers/services distributed across locations.
* Aggregate, store, and index logs centrally.
* Provide real-time and historical log search and analytics.
* Handle high write throughput and large data volumes.
* Be fault-tolerant and scalable.

---

## 🔑 Key Requirements

* **High ingestion rate:** Millions of log events per second.
* **Durability:** Logs must not be lost.
* **Scalability:** Handle growing log volume and number of sources.
* **Low latency:** Fast log ingestion and near real-time querying.
* **Searchability:** Support complex queries on logs.
* **Fault tolerance:** Survive node failures without data loss.
* **Retention & archiving:** Manage data lifecycle.

---

## 🏗️ Core Components of the Design

### 1. **Log Producers**

* Applications, servers, microservices that generate logs.
* Logs are usually JSON or structured text.
* Use libraries/agents (e.g., Filebeat, Fluentd) to collect and forward logs reliably.

### 2. **Log Shippers / Collectors**

* Agents running on servers to **collect logs** and send them to the system.
* Can do buffering, batching, and retry on failures.
* Examples: Fluentd, Logstash, Filebeat.

### 3. **Message Queue / Log Broker**

* Decouples log producers from consumers.
* Handles high throughput and buffering.
* Ensures durability and ordering.
* Examples: **Apache Kafka**, AWS Kinesis.

### 4. **Log Storage & Indexing**

* Stores raw logs and indexes them for fast querying.
* Scalable and distributed storage.
* Examples:

    * **Elasticsearch**: distributed search engine for log indexing.
    * **HDFS** or cloud storage for raw log archiving.

### 5. **Log Processing & Aggregation**

* Processes logs for enrichment, filtering, parsing.
* Aggregates logs for metrics or alerting.
* Tools: Logstash, Apache Flink, Apache Spark Streaming.

### 6. **Query & Visualization Layer**

* User-facing dashboard and APIs for querying logs.
* Real-time dashboards and alerting.
* Examples: Kibana, Grafana.

---

## 🔄 Data Flow Example

```
Log Producers → Log Shippers → Kafka (Message Queue) → Log Processing → Elasticsearch (Storage & Indexing) → Query/Dashboard (Kibana)
```

---

## ⚙️ Additional Design Considerations

### 1. **Scalability**

* Partition logs by source, time, or topic in Kafka.
* Scale Elasticsearch cluster horizontally.
* Use sharding and replication.

### 2. **Fault Tolerance**

* Kafka replicates partitions.
* Use persistent storage with replication for durability.
* Retry and dead-letter queues for failed messages.

### 3. **Consistency & Ordering**

* Ensure ordering within partitions in Kafka.
* Time synchronization (e.g., via NTP) for consistent timestamps.

### 4. **Security**

* Encrypt logs in transit (TLS).
* Authenticate producers and consumers.
* Access control on log queries.

### 5. **Retention Policies**

* Define TTL for logs.
* Archive old logs to cold storage (e.g., AWS S3).
* Automatic deletion after expiry.

---

## 📝 Summary Table

| Component          | Purpose                         | Example Tools               |
| ------------------ | ------------------------------- | --------------------------- |
| Log Producers      | Generate logs                   | Applications, microservices |
| Log Shippers       | Collect & forward logs          | Fluentd, Filebeat, Logstash |
| Message Queue      | Buffer & distribute logs        | Kafka, Kinesis              |
| Storage & Indexing | Store and index logs for search | Elasticsearch, HDFS         |
| Processing         | Enrich, filter, aggregate logs  | Logstash, Spark Streaming   |
| Visualization      | Query and visualize logs        | Kibana, Grafana             |

---

## 🚀 Interview Tips

* Start by clarifying requirements and scale.
* Draw the data flow architecture.
* Talk about **why you use message queues** for decoupling.
* Discuss **scaling strategies** for each component.
* Highlight **fault tolerance** and **data durability**.
* Mention **trade-offs** (e.g., indexing cost vs query latency).

---

## 20. How would you handle data replication and partitioning?

**Data replication** and **partitioning** (also called sharding) are foundational strategies for building scalable, fault-tolerant distributed systems. Let me explain both concepts in detail and how to handle them effectively.

---

## 1️⃣ What is Data Replication?

**Replication** means keeping copies of the same data on multiple machines or nodes.

### Why replicate data?

* **Fault tolerance:** If one node fails, data is still available on others.
* **High availability:** Data can be served from multiple locations, improving uptime.
* **Improved read performance:** Read requests can be distributed across replicas.

---

### Common Replication Strategies:

| Strategy          | Description                                                | Pros                                       | Cons                                        |
| ----------------- | ---------------------------------------------------------- | ------------------------------------------ | ------------------------------------------- |
| **Master-Slave**  | One primary node handles writes; replicas sync data        | Simple to implement, reads scaled          | Write bottleneck at master, replication lag |
| **Master-Master** | Multiple nodes accept writes, replicate changes among them | Higher write availability, no single point | Conflict resolution complexity              |
| **Quorum-based**  | Write/read succeeds only if a quorum of nodes acknowledge  | Stronger consistency guarantees            | Increased write/read latency                |

---

### Handling Replication:

* **Synchronous replication:** Writes are confirmed only after all replicas acknowledge → strong consistency but higher latency.
* **Asynchronous replication:** Write confirmed immediately; replicas updated later → better performance but eventual consistency.

---

## 2️⃣ What is Data Partitioning?

**Partitioning** or **sharding** means splitting a large dataset into smaller, manageable pieces called shards, each stored on a different node.

### Why partition data?

* **Scalability:** Enables distributing data and load across multiple machines.
* **Performance:** Each node handles only a subset of data, improving response times.
* **Manageability:** Easier to maintain smaller datasets.

---

### Common Partitioning Techniques:

| Technique              | Description                                                  | Use Cases                            |
| ---------------------- | ------------------------------------------------------------ | ------------------------------------ |
| **Range Partitioning** | Split data by ranges (e.g., user IDs 1-1000, 1001-2000)      | Ordered data, range queries          |
| **Hash Partitioning**  | Use a hash function on a key to assign shard                 | Uniform distribution, load balancing |
| **List Partitioning**  | Assign data based on a predefined list (e.g., country codes) | Categorical data partitioning        |

---

## 3️⃣ Combining Replication and Partitioning

* **Each shard is replicated** across multiple nodes.
* Data is partitioned to distribute load, replicated to ensure reliability.
* Example: In a Cassandra cluster, data is partitioned by hashing the partition key, and each partition is replicated on multiple nodes.

---

## 4️⃣ Key Considerations & Challenges

| Aspect                       | What to Handle                                                        |
| ---------------------------- | --------------------------------------------------------------------- |
| **Consistency**              | Ensure replicas have up-to-date data (choose sync/async replication). |
| **Replication lag**          | Manage delays between master and replicas.                            |
| **Data rebalancing**         | When adding/removing nodes, redistribute shards without downtime.     |
| **Fault tolerance**          | Handle node failures without data loss.                               |
| **Partitioning key choice**  | Choose keys that evenly distribute data and avoid hotspots.           |
| **Cross-shard transactions** | Avoid or carefully manage transactions that span shards.              |

---

## 5️⃣ Example Scenario

* In a user database:

    * Partition by user ID hash (hash partitioning).
    * Replicate each shard to 3 nodes (replication factor = 3).
    * Reads can be served from any replica; writes go to the leader node.

---

## 6️⃣ Interview Tip

* Clearly explain the **difference and purpose** of replication and partitioning.
* Discuss **trade-offs**: consistency vs latency, complexity of master-master vs master-slave.
* Explain how **partitioning keys affect system performance**.
* Talk about **handling failure and rebalancing** in real systems.
* Reference real-world databases: Cassandra (hash partition + replication), MongoDB (sharding + replica sets), MySQL (master-slave replication).

---

## 21. What is sharding and how do you implement it?

**Sharding** is a fundamental technique used to scale databases and large data stores by distributing data across multiple machines. Here's a detailed explanation with examples.

---

## ✅ What is Sharding?

* **Sharding** is the process of **splitting a large dataset into smaller, more manageable pieces called shards**.
* Each shard is stored on a separate database server or node.
* This allows the system to **scale horizontally** by spreading data and load across many machines.

---

## ✅ Why Shard?

* To **handle large volumes of data** that exceed the capacity of a single machine.
* To **improve performance** by reducing the amount of data each node handles.
* To **increase availability** and fault tolerance by isolating failures to individual shards.

---

## ✅ How is Sharding Different from Replication?

| Aspect        | Sharding                                    | Replication                                 |
| ------------- | ------------------------------------------- | ------------------------------------------- |
| Purpose       | Split data horizontally across servers      | Copy data to multiple servers               |
| Data Location | Each piece stored in exactly one shard      | Each replica has full or partial data       |
| Use Case      | Scale write/read capacity by spreading load | Improve fault tolerance and read throughput |

---

## ✅ How to Implement Sharding?

### 1. Choose a **Shard Key**

* The shard key determines how data is split across shards.
* Good shard key should:

    * **Evenly distribute data** to avoid hotspots.
    * Be **frequently used in queries** for efficient routing.
* Examples: User ID, geographic region, timestamp.

### 2. Sharding Strategies

| Strategy                     | Description                                                                        | Pros                           | Cons                          |
| ---------------------------- | ---------------------------------------------------------------------------------- | ------------------------------ | ----------------------------- |
| **Range-Based Sharding**     | Data is partitioned into ranges based on shard key (e.g., users 1–1000 on shard 1) | Simple, good for range queries | Uneven data distribution risk |
| **Hash-Based Sharding**      | Hash of the shard key decides shard placement                                      | Even data distribution         | Harder to do range queries    |
| **Directory-Based Sharding** | A lookup table maps keys to shards                                                 | Flexible                       | Single point of failure       |

### 3. Routing Queries

* The system needs a **routing mechanism** to send requests to the correct shard.
* Can be:

    * Client-side: Client knows shard locations.
    * Middleware/proxy: Middleware routes requests.
    * Database built-in routing: e.g., MongoDB’s mongos.

### 4. Handling Rebalancing

* When adding/removing shards, data must be **moved/rebalanced** to maintain even distribution.
* Techniques like consistent hashing minimize data movement.

---

## ✅ Example: User Database Sharding

* **Shard Key:** User ID.
* **Strategy:** Hash-based sharding.
* **How it works:** Hash(user\_id) % number\_of\_shards → directs to specific shard.
* User data is distributed evenly across shards.
* Query requests are routed to the shard owning that user’s data.

---

## ✅ Challenges in Sharding

* **Choosing a good shard key** to avoid uneven data distribution.
* **Cross-shard transactions** are complex and costly.
* **Rebalancing shards** without downtime.
* **Maintaining consistency** across shards.
* **Complexity in query routing and system maintenance.**

---

## ✅ Interview Tip

* Define sharding clearly and why it’s necessary.
* Explain different sharding strategies and trade-offs.
* Discuss how queries are routed to shards.
* Mention real-world examples: MongoDB sharding, Cassandra partitioning.
* Highlight challenges and how to mitigate them.

---

## 22. How would you handle system failure and recovery?

Handling **system failure and recovery** is essential to build resilient, reliable systems that minimize downtime and data loss.

---

## 🎯 Goal

* Detect failures quickly.
* Recover from failures with minimal impact.
* Prevent data loss and maintain service availability.
* Learn from failures to improve system robustness.

---

## 1️⃣ Types of Failures to Consider

* **Hardware failures:** disk crashes, network outages, power loss.
* **Software failures:** bugs, memory leaks, crashes.
* **Network failures:** partitions, latency, dropped messages.
* **Human errors:** misconfigurations, accidental data deletion.

---

## 2️⃣ Key Strategies for Handling Failures

### a) **Failure Detection & Monitoring**

* Use **health checks** and **heartbeat signals** to detect failures early.
* Monitor system metrics (CPU, memory, response time) with tools like Prometheus, Nagios.
* Alert on anomalies for rapid response.

### b) **Redundancy & Replication**

* Use redundant hardware and multiple instances.
* Replicate critical data across nodes.
* Avoid single points of failure (SPOF).

### c) **Automatic Failover**

* Design systems to automatically switch to a standby or backup system on failure.
* Example: database primary-slave failover, load balancers redirecting traffic.

### d) **Graceful Degradation**

* Allow the system to continue operating with reduced functionality during partial failures.
* Example: serve cached data if database is temporarily unreachable.

### e) **Backup & Recovery**

* Regular backups of data (full/incremental).
* Test restore procedures periodically.
* Use snapshot and point-in-time recovery techniques.

### f) **Statelessness**

* Design services to be stateless where possible, so they can be restarted or replaced easily.

### g) **Retry and Timeout Policies**

* Implement retries with exponential backoff.
* Set timeouts to avoid hanging processes.

### h) **Circuit Breakers**

* Prevent cascading failures by cutting off calls to failing components.

---

## 3️⃣ Recovery Approaches

### a) **Cold Start**

* System restarts from backup data after a failure (long downtime).

### b) **Warm Start**

* Some system state is preserved; restart faster than cold start.

### c) **Hot Failover**

* Backup system continuously synchronized and ready to take over instantly.

---

## 4️⃣ Example Scenario: Database Failure Recovery

* Detect primary DB failure via health checks.
* Failover to replica promoted as new primary.
* Redirect all writes to new primary.
* Once original primary recovers, re-sync it as replica.

---

## 5️⃣ Summary Table

| Strategy                 | Purpose                   | Example Tools/Techniques       |
| ------------------------ | ------------------------- | ------------------------------ |
| Monitoring & Alerts      | Early detection           | Prometheus, Grafana, Nagios    |
| Redundancy & Replication | Avoid SPOF & data loss    | Database replicas, RAID        |
| Automatic Failover       | Minimize downtime         | Pacemaker, Kubernetes          |
| Graceful Degradation     | Partial availability      | Cache fallback                 |
| Backup & Restore         | Data recovery             | Snapshots, incremental backups |
| Stateless Design         | Easy recovery & scaling   | REST APIs, microservices       |
| Retry & Timeout          | Handle transient failures | Exponential backoff            |
| Circuit Breaker          | Prevent cascading failure | Netflix Hystrix, resilience4j  |

---

## 6️⃣ Interview Tip

* Explain **types of failures** and impact.
* Describe **prevention, detection, and recovery** clearly.
* Use real-world examples.
* Discuss **trade-offs** (cost vs downtime).
* Mention importance of testing recovery procedures (disaster recovery drills).

---

## 23. What is a circuit breaker in system design?

A **circuit breaker** is a key pattern in system design to improve resilience and prevent cascading failures in distributed systems.

---

## ✅ What is a Circuit Breaker?

* Inspired by electrical circuit breakers that stop electricity flow when there's a fault.
* In software, a circuit breaker **monitors calls to a remote service or resource** and **automatically stops calls when failures exceed a threshold**.
* It helps prevent the system from wasting resources on repeated calls to a failing service and gives the failing component time to recover.

---

## ✅ How Does it Work?

The circuit breaker typically has **three states**:

| State         | Description                                                                                                                            |
| ------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| **Closed**    | Calls pass through normally. Failures are counted.                                                                                     |
| **Open**      | Circuit "trips" after too many failures. Calls fail fast without calling the service.                                                  |
| **Half-Open** | After a timeout, a few test calls are allowed to check if the service recovered. If successful, circuit closes; otherwise, it reopens. |

---

## ✅ Why Use a Circuit Breaker?

* **Prevent cascading failures:** Stop flooding a failing service with requests.
* **Fail fast:** Return errors quickly to clients rather than waiting for timeouts.
* **Improve system stability and responsiveness.**
* **Allow graceful recovery** by giving the failing service time to fix itself.

---

## ✅ Real-world Example

Imagine a web app calling an external payment service:

* If the payment service starts failing or is slow, repeated retries can overload it.
* Circuit breaker detects failures and "opens" the circuit.
* Instead of waiting for timeouts, the app immediately returns an error or fallback.
* After a cooldown period, test calls check if the payment service is back.
* If yes, circuit closes and normal traffic resumes.

---

## ✅ Technologies & Libraries

* Netflix **Hystrix** (now in maintenance mode)
* **Resilience4j** (popular for Java)
* Polly (for .NET)
* Built-in support in service meshes like Istio

---

## ✅ Interview Tip

* Explain **why circuit breakers are important** in distributed systems.
* Describe the **three states** clearly.
* Discuss **fail fast behavior** and **avoiding cascading failures**.
* Mention **integration with retries and fallbacks**.
* Give a **concrete example**.

---

## 24. How would you design a rate limiter?

Designing a **rate limiter** is a classic system design problem to control how many requests a user or system can make in a given time window, preventing abuse and ensuring fair resource usage.

---

## 🎯 What is a Rate Limiter?

* A component that **limits the number of requests** a client/user can make to a service in a specified time period.
* Helps **protect APIs**, prevent DoS attacks, and manage traffic bursts.

---

## ✅ Key Requirements

* Define **limits** like “100 requests per minute” per user/IP/API key.
* Should be **accurate and performant** under high load.
* Handle **distributed systems** with multiple servers.
* Provide **fairness** and avoid race conditions.
* Optionally support **bursting** (short bursts allowed above rate limit).

---

## ✅ Common Rate Limiting Algorithms

| Algorithm                  | Description                                              | Use Cases & Pros                 | Cons                                  |
| -------------------------- | -------------------------------------------------------- | -------------------------------- | ------------------------------------- |
| **Fixed Window**           | Count requests in fixed time windows (e.g., per minute). | Simple, easy to implement.       | Can cause bursts at window edges.     |
| **Sliding Window Log**     | Keep timestamps of requests; slide window over time.     | Accurate rate limiting.          | Uses more memory, expensive at scale. |
| **Sliding Window Counter** | Approximate sliding window with counters.                | Balance accuracy and efficiency. | More complex than fixed window.       |
| **Token Bucket**           | Tokens added at fixed rate; each request consumes token. | Supports bursting.               | Requires token management.            |
| **Leaky Bucket**           | Requests added to a queue that leaks at fixed rate.      | Smooths bursts, simple concept.  | Can add latency.                      |

---

## ✅ How to Implement Rate Limiting?

### 1. Fixed Window Counter (Simple Example)

* Store a counter per user/IP per fixed interval (e.g., minute).
* Increment counter for each request.
* Reject requests if counter exceeds limit.
* Reset counter every window.

### 2. Token Bucket (More Flexible)

* Each user has a bucket with tokens.
* Tokens are added at a steady rate.
* Each request consumes a token.
* If no tokens left, request is rejected.
* Allows bursting up to bucket size.

---

## ✅ Distributed Rate Limiting

* Use **centralized storage** like Redis to keep counters/tokens across servers.
* Use **atomic operations** (e.g., Redis `INCR`, `EVAL` for Lua scripts) to avoid race conditions.
* Alternatively, use **API gateways** or **service meshes** with built-in rate limiting.

---

## ✅ Example: Redis Token Bucket (Simplified)

```pseudo
function allowRequest(userId):
    bucket = getBucket(userId)
    refillTokens(bucket)  // based on elapsed time
    if bucket.tokens > 0:
        bucket.tokens -= 1
        saveBucket(userId, bucket)
        return true
    else:
        return false
```

---

## ✅ Additional Considerations

* **Key granularity:** per user, IP, API key, or globally.
* **Distributed clocks:** synchronize time for fairness.
* **Burst handling:** support sudden bursts within limits.
* **Backoff:** clients should slow down on rate limit hits.
* **Monitoring:** track rate limit usage and violations.

---

## ✅ Interview Tip

* Explain **why rate limiting matters**.
* Describe **one or two algorithms** with pros/cons.
* Discuss **how to implement in a distributed environment**.
* Mention **trade-offs** between accuracy, memory, and complexity.
* Optional: describe **integration with API gateway or service mesh**.

---

## 25. How do you ensure security in large-scale systems?

Ensuring **security in large-scale systems** is crucial because these systems often handle sensitive data, support many users, and face diverse threats. Here's a detailed overview of key principles and practices.

---

## 1️⃣ Core Security Goals

* **Confidentiality:** Data is accessed only by authorized users.
* **Integrity:** Data is accurate and unaltered.
* **Availability:** System remains accessible and operational.
* **Authentication:** Verifying user identities.
* **Authorization:** Controlling access to resources.
* **Auditing:** Tracking and logging actions for accountability.

---

## 2️⃣ Key Security Practices in Large-Scale Systems

### a) **Authentication & Authorization**

* Use strong authentication (e.g., OAuth 2.0, OpenID Connect, multi-factor authentication).
* Implement **role-based access control (RBAC)** or **attribute-based access control (ABAC)**.
* Principle of **least privilege** — users/services get minimum access needed.

### b) **Data Encryption**

* Encrypt data **in transit** using TLS/SSL.
* Encrypt data **at rest** using disk or database encryption.
* Use secure key management systems (KMS).

### c) **Network Security**

* Use firewalls, VPNs, and network segmentation.
* Implement **zero trust** principles: never trust by default, always verify.
* Use API gateways to authenticate and throttle requests.

### d) **Input Validation & Sanitization**

* Prevent injection attacks (SQL, XSS) by validating and sanitizing inputs.
* Use parameterized queries and secure libraries.

### e) **Monitoring & Logging**

* Log security events and access attempts.
* Use SIEM (Security Information and Event Management) tools to analyze logs.
* Set up alerts for suspicious activities.

### f) **Security Testing**

* Conduct regular penetration testing and vulnerability scans.
* Use automated static/dynamic code analysis.
* Apply security patches promptly.

### g) **Disaster Recovery & Incident Response**

* Prepare plans for security breaches.
* Have backups and recovery strategies.
* Conduct drills and update response plans regularly.

### h) **Secure Development Lifecycle**

* Integrate security checks in CI/CD pipelines.
* Educate developers on secure coding best practices.

---

## 3️⃣ Scalability & Security Trade-offs

* Balance between strong security measures and system performance.
* Use caching and tokens to reduce load on authentication servers.
* Design for **fail-safe defaults** (deny access unless explicitly allowed).

---

## 4️⃣ Example: Securing a Large Web Application

* Use OAuth 2.0 for user authentication.
* Encrypt all API calls with TLS.
* Rate limit and validate API inputs.
* Log access and error events centrally.
* Use Web Application Firewall (WAF) to block malicious traffic.
* Regularly update dependencies to patch vulnerabilities.

---

## 5️⃣ Interview Tip

* Highlight **layered security** (defense in depth).
* Explain **principles like least privilege, zero trust, and encryption**.
* Mention practical tools and protocols.
* Discuss **security automation and monitoring**.
* Provide concrete examples from real systems.

---

Want me to explain security design for a specific system type (e.g., payment system, social media platform)?

---

### 🔹 **26–50: Real-World System Design Questions (HLD)**

## 26. Design a URL shortener like Bitly.

Awesome! Designing a URL shortener like **Bitly** is a classic system design question that tests your ability to handle key challenges such as unique ID generation, scalability, low latency, and analytics. Let’s break it down step-by-step.

---

# Design a URL Shortener (like Bitly)

---

## 1️⃣ Requirements

### Functional:

* Given a long URL, generate a **shortened URL**.
* Redirect from the short URL to the original long URL.
* Handle **high read & write traffic** efficiently.
* Optional: provide analytics (click counts, user info).

### Non-Functional:

* **High availability** and **low latency**.
* **Scalable** to billions of URLs.
* Handle **collision-free** unique ID generation.
* Durable and consistent storage.

---

## 2️⃣ API Design

* `POST /shorten` — Input: long URL; Output: short URL.
* `GET /{shortCode}` — Redirect to long URL.
* `GET /analytics/{shortCode}` — Return usage stats (optional).

---

## 3️⃣ High-Level Components

| Component            | Responsibility                            |
| -------------------- | ----------------------------------------- |
| API Servers          | Handle client requests                    |
| URL Shortening Logic | Generate unique short codes               |
| Database             | Store mappings (shortCode → longURL)      |
| Cache                | Speed up lookups (e.g., Redis, Memcached) |
| Analytics Service    | Collect and analyze click data (optional) |
| Load Balancer        | Distribute requests across servers        |

---

## 4️⃣ Core Challenges & Solutions

### a) Unique ID Generation (Short Code)

* Use a **Base62 encoding** (0-9, a-z, A-Z) for short codes (e.g., length 6-8 characters).
* Methods:

    * **Auto-increment ID + encode**: Generate a unique numeric ID, encode it to Base62.
    * **Hashing**: Hash the long URL and use part of the hash (handle collisions).
    * **Random generation with collision check**: Generate random string and verify uniqueness.
* Auto-increment + Base62 is simple, fast, and collision-free.

### b) Storage

* Store mapping in a **key-value database** (NoSQL or RDBMS).
* Key: shortCode
* Value: longURL, metadata (creation time, user ID).
* Use **replication and sharding** for scalability.

### c) Redirecting

* When a user accesses the short URL, the system looks up the long URL in cache or DB.
* Redirect HTTP 301 or 302 to the original URL.

### d) Caching

* Use Redis or Memcached to cache popular mappings for fast lookup.
* Cache expiry policy based on usage patterns.

### e) Analytics (Optional)

* Track clicks, geo-location, referrer, timestamp.
* Use asynchronous logging to avoid slowing redirects.

---

## 5️⃣ Data Model (Example)

| Field      | Type      | Description         |
| ---------- | --------- | ------------------- |
| shortCode  | String    | Unique short code   |
| longURL    | String    | Original long URL   |
| createdAt  | Timestamp | Creation time       |
| clickCount | Integer   | Number of redirects |
| userId     | String    | (Optional) Owner ID |

---

## 6️⃣ Scalability Considerations

* **Partitioning:** Shard DB by shortCode prefix or hash.
* **Replication:** Use master-slave or multi-master for availability.
* **Load Balancing:** Across API and DB servers.
* **CDN:** Use CDN for serving redirect responses quickly.
* **Rate Limiting:** Prevent abuse or spam usage.

---

## 7️⃣ Example Flow

1. Client calls `POST /shorten` with long URL.
2. API server generates next ID, encodes to Base62 → shortCode.
3. Store (shortCode, longURL) in DB.
4. Return short URL: `https://short.ly/{shortCode}`.
5. User visits short URL.
6. System checks cache → DB for longURL.
7. Redirects user to original URL.

---

## 8️⃣ Possible Enhancements

* **Custom aliases:** Let users pick short codes.
* **Expiration:** URLs expire after a time.
* **Security:** Prevent malicious URLs.
* **Analytics Dashboard:** Detailed click stats.
* **URL validation:** Ensure valid and safe URLs.

---

## Interview Tip

* Clarify requirements & scope.
* Discuss trade-offs of different ID generation methods.
* Address scalability and fault tolerance.
* Mention caching and database choices.
* Sketch architecture and data flow clearly.

---

## 27. Design a social media feed (e.g., Facebook/Instagram).

Designing a **social media feed** like Facebook or Instagram is a classic system design interview question that tests your understanding of large-scale data handling, real-time updates, ranking algorithms, and scalability.

---

# Design a Social Media Feed

---

## 1️⃣ Requirements

### Functional:

* Show a feed of posts from friends/followed users.
* Support posts with text, images, videos.
* Show feed sorted by relevance or recency.
* Support likes, comments, shares.
* Real-time or near-real-time updates.
* Pagination or infinite scrolling.

### Non-Functional:

* Handle millions of users and posts.
* Low latency for feed loading.
* Scalable and fault tolerant.
* Consistent user experience.

---

## 2️⃣ High-Level Components

| Component            | Responsibility                     |
| -------------------- | ---------------------------------- |
| Client App           | UI, fetch feed, show posts         |
| API Gateway          | Handle client requests             |
| Feed Service         | Generate and serve user feeds      |
| User Service         | User profiles and relationships    |
| Post Service         | Store and serve posts              |
| Timeline Storage     | Store precomputed feeds (optional) |
| Cache                | Cache popular feeds/posts          |
| Notification Service | Push updates or alerts             |
| Analytics Service    | Collect user interactions          |

---

## 3️⃣ Feed Generation Approaches

### a) **Pull Model (On-the-fly Aggregation)**

* When user requests feed, system queries recent posts from all followed users.
* Merge and sort posts by timestamp or relevance.
* Pros: No data duplication, always fresh.
* Cons: Expensive and slow for users following many accounts.

### b) **Push Model (Precomputed Timeline)**

* When user posts, system pushes the post ID to the timelines of all followers.
* Each user has a **timeline** (a list of post IDs) stored in a database.
* Feed retrieval is fast: fetch timeline and then get post details.
* Pros: Fast feed reads.
* Cons: Expensive writes, complexity in fan-out for users with millions of followers.

**Hybrid** approaches balance these based on user type.

---

## 4️⃣ Data Model (Simplified)

* **User:** userId, username, followers\[], following\[].
* **Post:** postId, userId, content, timestamp, mediaUrl.
* **Timeline:** userId, \[postId1, postId2, ...] (ordered by timestamp).
* **Likes/Comments:** postId, userId, commentText, timestamp.

---

## 5️⃣ Storage Solutions

* Use **NoSQL databases** like Cassandra, DynamoDB for posts and timelines due to write/read scalability.
* Use **Redis or Memcached** for caching hot feeds.
* Store media in **object storage** like S3 or CDN.

---

## 6️⃣ Ranking & Personalization

* Sort posts by recency, engagement (likes, comments), user preferences.
* Use **machine learning models** to personalize feed order.
* Incorporate freshness and diversity.

---

## 7️⃣ Handling Scale

* **Fan-out optimization:**

    * For normal users, push posts to followers’ timelines.
    * For celebrities with millions of followers, generate feed on-the-fly or use dedicated pipelines.

* **Caching:** Cache popular feeds and posts.

* **Pagination:** Load feed in chunks using infinite scroll.

* **Load Balancing:** Distribute API requests across servers.

* **CDN:** Deliver media content efficiently.

---

## 8️⃣ Real-Time Updates

* Use WebSockets, long polling, or push notifications to notify users of new posts or interactions.
* Incremental feed updates instead of full reloads.

---

## 9️⃣ Example User Flow

1. User opens app → sends request to Feed Service.
2. Feed Service fetches user timeline from Timeline Storage.
3. Fetches corresponding post details.
4. Applies ranking and personalization.
5. Sends ordered feed to client.
6. Client displays feed with pagination and real-time update support.

---

## 🔟 Interview Tips

* Clarify requirements (e.g., consistency vs latency trade-offs).
* Discuss pros/cons of pull vs push model.
* Highlight challenges in fan-out and scalability.
* Mention caching strategies.
* Talk about personalization briefly.
* Sketch high-level architecture diagram.

---

## 28. Design Twitter (posting, timeline, follow system).

Designing **Twitter** involves key features like posting tweets, building timelines, and managing the follow system at massive scale. Let’s walk through the design step-by-step.

---

# Design Twitter: Posting, Timeline, Follow System

---

## 1️⃣ Requirements

### Functional

* Users can post tweets (up to 280 characters).
* Users can follow/unfollow others.
* Users see a timeline of tweets from people they follow.
* Support real-time or near-real-time timeline updates.
* Support millions of users and tweets.

### Non-Functional

* Highly available and scalable.
* Low latency feed generation.
* Durable storage of tweets.
* Consistent follower-following relationships.

---

## 2️⃣ Core Components

| Component            | Responsibility                                    |
| -------------------- | ------------------------------------------------- |
| User Service         | Manage user profiles, followers/following         |
| Tweet Service        | Accept and store tweets                           |
| Timeline Service     | Generate user timelines                           |
| Feed Generator       | Fan-out tweets to followers (push)                |
| Notification Service | Notify users of new tweets/mentions               |
| Storage              | Databases and caches for tweets, users, timelines |
| API Gateway          | Handle client requests                            |

---

## 3️⃣ User, Tweet & Follow Data Model

* **User:**
  `{ userId, username, followers[], following[] }`

* **Tweet:**
  `{ tweetId, userId, content, timestamp, mediaUrl }`

* **Follow:**
  Store follower → followee relationships. Could be in a graph DB or NoSQL table.

* **Timeline:**
  `{ userId, [tweetId1, tweetId2, ...] }` (precomputed or computed on the fly)

---

## 4️⃣ Posting a Tweet

* User sends a tweet to Tweet Service.
* Tweet stored in database.
* Feed Generator fans out tweet to followers’ timelines (push model).
* If follower count is large (celebrity), delay or switch to pull model for timeline generation.

---

## 5️⃣ Timeline Generation Approaches

### a) **Push Model**

* On tweet creation, push tweet ID into followers’ timeline lists.
* Timeline is precomputed; quick to fetch.
* Challenges: high write fan-out, storage overhead.

### b) **Pull Model**

* When user requests timeline, fetch latest tweets from people they follow.
* Merge and sort by timestamp.
* Challenges: high read latency, expensive if following many users.

### c) **Hybrid**

* Push for normal users.
* Pull for celebrities.

---

## 6️⃣ Storage Choices

* Use **NoSQL DB** (like Cassandra, DynamoDB) for tweets and timelines.
* Use **in-memory cache** (Redis) for hot timelines and tweets.
* Media stored in object storage (e.g., AWS S3).

---

## 7️⃣ Handling Follows & Unfollows

* Update follower-following tables atomically.
* On unfollow, remove tweets from user timeline (optional) or filter at read time.
* Maintain consistency using eventual consistency models.

---

## 8️⃣ Scalability & Performance

* Shard data by userId or tweetId.
* Use consistent hashing to distribute load.
* Use asynchronous processing for fan-out to reduce latency.
* Rate limit API usage to prevent abuse.
* Use CDN for media delivery.

---

## 9️⃣ Real-Time Updates

* Use WebSockets or push notifications for new tweet alerts.
* Incremental timeline updates without full reload.

---

## 🔟 Example User Flow: Posting & Timeline Fetch

1. User posts tweet → API Gateway → Tweet Service.
2. Tweet stored in DB.
3. Feed Generator fans out tweet to followers’ timelines asynchronously.
4. User requests timeline → Timeline Service fetches precomputed timeline from cache/DB.
5. Timeline sent to user’s client app.

---

## Interview Tips

* Clarify push vs pull model pros/cons.
* Talk about fan-out challenge for celebrities.
* Discuss data partitioning and replication.
* Mention caching and rate limiting.
* Describe eventual consistency and user experience trade-offs.

---

## 29. Design WhatsApp (messaging, delivery, storage).

Designing **WhatsApp** involves key challenges in real-time messaging, message delivery guarantees, storage, and scalability. Let’s break down the system design for WhatsApp focusing on messaging, delivery, and storage.

---

# Design WhatsApp: Messaging, Delivery & Storage

---

## 1️⃣ Requirements

### Functional

* One-to-one messaging (text, images, videos).
* Real-time message delivery with low latency.
* Message status: sent, delivered, read.
* Message storage (device + server).
* Support offline messaging (store and forward).
* Group chats (optional, mention for scalability).
* End-to-end encryption (optional mention).

### Non-Functional

* Highly available and scalable.
* Reliable message delivery.
* Support millions to billions of users.
* Minimal latency.

---

## 2️⃣ High-Level Components

| Component                 | Responsibility                                |
| ------------------------- | --------------------------------------------- |
| Client App                | Send/receive messages, show status            |
| API Gateway               | Entry point for message sending and retrieval |
| Messaging Service         | Handle sending, delivery, and acknowledgment  |
| Message Queue             | Buffer messages for offline users             |
| Storage Service           | Persist message history and media             |
| Push Notification Service | Notify users of new messages                  |
| Presence Service          | Track user online/offline status              |
| Encryption Service        | Handle encryption/decryption (end-to-end)     |

---

## 3️⃣ Messaging Flow

### a) Sending a Message

1. User types message → client sends to Messaging Service via API Gateway.
2. Messaging Service:

    * Stores message temporarily.
    * Checks recipient status (online/offline).
    * If online, push message immediately.
    * If offline, enqueue message in Message Queue.

### b) Receiving a Message

* Recipient client listens to push notifications or maintains a persistent connection (WebSocket, MQTT).
* On receiving, client sends **delivery acknowledgment**.
* Sender receives delivery status update.

### c) Message Status Lifecycle

* **Sent:** Message accepted by server.
* **Delivered:** Message received by recipient’s device.
* **Read:** Recipient opened the message.

---

## 4️⃣ Storage

* Store messages **temporarily on servers** to allow delivery.
* Messages can be deleted after delivery or retained for a time window.
* Use **NoSQL DB** (e.g., Cassandra, DynamoDB) for scalability.
* Store media files in **object storage** (e.g., AWS S3).
* End-to-end encryption means server stores only encrypted data.

---

## 5️⃣ Handling Offline Users

* Use message queues (Kafka, RabbitMQ) or push notification queues.
* When user comes online, deliver queued messages.
* Expire undelivered messages after a timeout.

---

## 6️⃣ Real-Time Messaging Protocols

* Use **persistent connections**:

    * WebSocket or MQTT for low-latency messaging.
    * Allows server to push messages instantly.

---

## 7️⃣ Scalability Considerations

* Partition users/messages by user ID for distributed processing.
* Use load balancers for API and Messaging Services.
* Use sharding in databases to distribute storage.
* Use CDN or edge servers for media delivery.

---

## 8️⃣ End-to-End Encryption (Optional Mention)

* Messages are encrypted on sender device.
* Decrypted only on recipient device.
* Server stores encrypted blobs.
* Keys never leave devices.

---

## 9️⃣ Example Data Model (Simplified)

| MessageID | SenderID | ReceiverID | Timestamp | Content (Encrypted) | Status |
| --------- | -------- | ---------- | --------- | ------------------- | ------ |

---

## 🔟 Summary Flow Diagram (Simplified)

1. Sender sends message → API Gateway → Messaging Service.
2. Messaging Service stores message and tries delivering.
3. If recipient online → push message immediately.
4. If offline → enqueue message.
5. Recipient receives message → sends acknowledgment.
6. Messaging Service updates status and informs sender.

---

## Interview Tips

* Emphasize real-time delivery & offline handling.
* Discuss persistent connections (WebSocket/MQTT).
* Talk about data partitioning for scalability.
* Mention storage design and expiration policies.
* Optionally, mention encryption and privacy.

---

## 30. Design an Uber-like ride-sharing system.

Designing an **Uber-like ride-sharing system** is a classic system design problem that involves real-time matching, geospatial queries, scalability, and reliability. Let’s go through it step-by-step.

---

# Design Uber-like Ride-Sharing System

---

## 1️⃣ Requirements

### Functional

* Users can request rides specifying pickup and dropoff locations.
* Drivers can accept ride requests.
* Real-time matching between riders and nearby drivers.
* Track driver and ride status (available, en route, completed).
* Fare calculation and payment processing.
* Support ride history and ratings.

### Non-Functional

* Handle high volume of concurrent users.
* Low latency for matching and updates.
* Scalable and fault-tolerant.
* Accurate and efficient location tracking.

---

## 2️⃣ High-Level Components

| Component             | Responsibility                                   |
| --------------------- | ------------------------------------------------ |
| Client Apps           | Rider and driver apps                            |
| API Gateway           | Handles all client requests                      |
| Ride Matching Service | Match riders with nearby drivers                 |
| Location Service      | Track and update geolocations                    |
| Trip Management       | Manage ride lifecycle (start, in-progress, end)  |
| Payment Service       | Handle fare calculation and transactions         |
| Notification Service  | Notify drivers and riders                        |
| Data Storage          | Store users, rides, driver status, and locations |
| Analytics Service     | For usage stats, surge pricing, etc.             |

---

## 3️⃣ Core Features & Design

### a) Real-Time Location Tracking

* Drivers periodically send GPS updates.
* Location Service stores driver locations in a **geospatial database** or **in-memory data store** (e.g., Redis with Geo commands).
* Enables fast queries for "nearest drivers" to a rider.

### b) Ride Matching

* When rider requests a ride, the system queries nearby available drivers.
* Use a radius search in geospatial DB for candidates.
* Apply filters (driver ratings, car type).
* Assign the ride to the closest driver who accepts.

### c) Ride Lifecycle Management

* Track ride states: requested, accepted, picked-up, completed, canceled.
* Notify driver and rider of updates.
* Handle cancellations and reassignments.

### d) Pricing & Payment

* Calculate fare based on distance, time, surge pricing.
* Integrate with payment gateway for transaction processing.

---

## 4️⃣ Data Model (Simplified)

| Entity   | Fields                                                   |
| -------- | -------------------------------------------------------- |
| User     | userId, name, phone, rating, paymentInfo                 |
| Driver   | driverId, location, status, carDetails, rating           |
| Ride     | rideId, riderId, driverId, pickup, dropoff, status, fare |
| Location | userId/driverId, latitude, longitude, timestamp          |

---

## 5️⃣ Storage Choices

* Use **NoSQL DB** (like Cassandra, MongoDB) for user, ride, and driver data.
* Use **in-memory store** (Redis) for real-time driver locations.
* Use **relational DB** for transactional data if needed.

---

## 6️⃣ Scalability Considerations

* Partition drivers by geographic regions.
* Use load balancers to distribute incoming requests.
* Employ **event-driven architecture** for ride updates.
* Use queues for asynchronous processing (e.g., payments, notifications).
* Use CDN for serving app assets.

---

## 7️⃣ Handling Failures & Edge Cases

* Retry logic for failed ride assignments.
* Graceful handling of driver/rider disconnects.
* Handle surge pricing with real-time analytics.
* Detect and prevent fraud.

---

## 8️⃣ User Flow Example

1. Rider opens app → sends ride request with pickup/dropoff.
2. API Gateway → Ride Matching Service queries nearby drivers.
3. Matching service selects driver and sends request.
4. Driver accepts → Trip Management updates status.
5. Driver picks up rider → status updated.
6. Trip completes → fare calculated and payment processed.
7. Ratings collected.

---

## Interview Tips

* Clarify scope and assumptions (e.g., do you support pooled rides?).
* Discuss data partitioning & geospatial indexing.
* Highlight real-time communication protocols.
* Talk about fault tolerance and retries.
* Sketch architecture diagram and flow.

---

## 31. Design Google Docs (real-time collaboration).

Designing **Google Docs** with real-time collaboration is an excellent system design question involving low-latency syncing, conflict resolution, and scalability. Let’s break it down carefully.

---

# Design Google Docs: Real-Time Collaborative Editor

---

## 1️⃣ Requirements

### Functional

* Multiple users can edit a document simultaneously.
* Changes are reflected in near real-time to all collaborators.
* Support text editing, cursor position, selections.
* Handle conflict resolution so edits don’t overwrite each other.
* Versioning and undo support.
* Support offline edits and sync on reconnect.

### Non-Functional

* Low latency for updates.
* Scalable to millions of users/documents.
* Highly available and fault tolerant.
* Data consistency with conflict resolution.

---

## 2️⃣ Key Challenges

* **Real-time synchronization:** Deliver changes quickly to all clients.
* **Conflict resolution:** Merge concurrent edits from multiple users.
* **Operational Transformation (OT) or CRDT:** Algorithms to handle concurrent changes.
* **Offline support:** Sync changes after reconnect.
* **Scalability:** Handle many documents and users.

---

## 3️⃣ High-Level Components

| Component            | Responsibility                                            |
| -------------------- | --------------------------------------------------------- |
| Client App           | Edit UI, capture user changes, display remote edits       |
| Sync Service         | Receive edits, broadcast updates                          |
| Document Storage     | Persist document versions and changes                     |
| Conflict Resolution  | OT or CRDT engine to merge concurrent edits               |
| Presence Service     | Track active collaborators and cursors                    |
| Offline Sync Manager | Handle offline edits and conflict resolution on reconnect |

---

## 4️⃣ Data Model

* Document consists of an ordered list of characters or elements.
* Changes represented as **operations** (insert, delete, update).
* Each operation has a unique id, timestamp, and userId.
* Store document versions and operation logs.

---

## 5️⃣ Real-Time Sync Workflow

1. Client captures local operation (e.g., insert character).
2. Sends operation to Sync Service.
3. Sync Service applies conflict resolution (OT/CRDT).
4. Broadcasts transformed operations to all collaborators.
5. Clients apply remote operations in order, updating the document view.

---

## 6️⃣ Conflict Resolution: OT vs CRDT

| Approach                                   | Description                                                                | Pros                                         | Cons                            |
| ------------------------------------------ | -------------------------------------------------------------------------- | -------------------------------------------- | ------------------------------- |
| Operational Transformation (OT)            | Transform incoming operations against concurrent ops to preserve intention | Proven, widely used (Google Docs)            | Complex to implement            |
| Conflict-free Replicated Data Types (CRDT) | Data structures that merge without conflicts inherently                    | Simple conflict resolution, offline-friendly | Can have higher memory overhead |

---

## 7️⃣ Offline Support

* Client buffers changes locally while offline.
* On reconnect, sends buffered operations to Sync Service.
* Service merges changes using conflict resolution.
* Updates broadcast to other clients.

---

## 8️⃣ Storage and Versioning

* Use **append-only log** for operations to reconstruct any version.
* Snapshot documents periodically to speed up loading.
* Store in scalable DB like Cassandra or distributed file systems.

---

## 9️⃣ Scalability Considerations

* Partition documents by document ID.
* Use message queues or event streams (Kafka) for operation distribution.
* Horizontal scaling of Sync Service.
* Cache frequently accessed docs and operations.

---

## 🔟 Example User Flow

1. User edits document → client generates operation.
2. Operation sent to Sync Service.
3. Sync Service applies OT to resolve conflicts.
4. Broadcast transformed ops to other clients.
5. Other clients apply ops, updating views.
6. Changes persisted in storage.

---

## Interview Tips

* Explain conflict resolution clearly (OT/CRDT).
* Emphasize real-time sync and offline handling.
* Talk about data structures for storing operations.
* Discuss partitioning and scaling of services.
* Sketch component interaction diagram.

---

## 32. Design a scalable notification system (SMS/Email/Push).

Designing a **scalable notification system** that supports SMS, Email, and Push notifications involves handling high throughput, reliability, user preferences, and delivery guarantees. Let’s go through the design in detail.

---

# Design Scalable Notification System (SMS, Email, Push)

---

## 1️⃣ Requirements

### Functional

* Send notifications via multiple channels: SMS, Email, Push.
* Support personalized messages.
* Support user preferences (which channel to use).
* Handle retries on failure.
* Support scheduling and batching notifications.
* Provide delivery status and logging.

### Non-Functional

* High throughput (millions of notifications/day).
* Low latency for time-sensitive notifications.
* Highly available and fault tolerant.
* Scalable to growing user base.

---

## 2️⃣ High-Level Components

| Component            | Responsibility                                       |
| -------------------- | ---------------------------------------------------- |
| API Gateway          | Accept notification requests                         |
| Notification Service | Core logic to process, queue, and send notifications |
| Message Queue        | Buffer notifications for asynchronous processing     |
| Channel Adapters     | Integrate with external SMS, Email, Push providers   |
| User Preferences DB  | Store user notification preferences                  |
| Scheduler Service    | Handle scheduled or delayed notifications            |
| Delivery Tracker     | Track delivery status, retries, and failures         |
| Logging & Analytics  | Monitor notification success and failures            |

---

## 3️⃣ Notification Flow

1. Client or system sends notification request to API Gateway.
2. Notification Service validates request, checks user preferences.
3. Notifications pushed into Message Queue (Kafka, RabbitMQ).
4. Worker services pull messages from queue per channel.
5. Worker calls appropriate Channel Adapter (SMS gateway, Email SMTP, Push service).
6. Delivery Tracker monitors response and updates status.
7. Retry logic handles failures with exponential backoff.
8. Logs stored for analytics and auditing.

---

## 4️⃣ User Preferences Handling

* Users can set preferred channels (e.g., push over SMS).
* Store preferences in a fast-access DB (NoSQL or cache).
* Notification Service uses preferences to route messages.

---

## 5️⃣ Scalability Considerations

* Decouple components with message queues for async processing.
* Horizontally scale workers based on load.
* Use partitioned queues keyed by user or notification type.
* Use CDN or push notification services (e.g., Firebase Cloud Messaging) for efficient push delivery.
* Throttle per-user or per-channel to avoid spamming.

---

## 6️⃣ Failure Handling & Retry

* Implement retry mechanism with limited retries.
* Dead-letter queue for failed notifications after retries.
* Alerting for persistent failures.
* Fallback channels if primary channel fails (optional).

---

## 7️⃣ Data Storage

* User Preferences DB: NoSQL DB (e.g., DynamoDB, Cassandra).
* Notification Metadata & Logs: SQL/NoSQL DB.
* Delivery status cached for quick querying.

---

## 8️⃣ Example Data Model (Simplified)

| NotificationID | UserID | Channel | Content | Status | Timestamp | RetryCount |
| -------------- | ------ | ------- | ------- | ------ | --------- | ---------- |

---

## 9️⃣ Security & Compliance

* Ensure data privacy (PII handling).
* Rate limiting to avoid abuse.
* Comply with regulations (e.g., GDPR, CAN-SPAM).

---

## 🔟 Summary Diagram

```
Client/System → API Gateway → Notification Service → Message Queue → Workers → Channel Providers
                                ↓                     ↑
                      User Preferences DB       Delivery Tracker & Logger
```

---

## Interview Tips

* Emphasize asynchronous processing for scalability.
* Discuss channel abstraction and modularity.
* Talk about monitoring and alerting.
* Mention throttling and rate limiting.
* Discuss trade-offs between latency and reliability.

---

## 33. Design a file storage system like Dropbox.

Designing a **file storage system like Dropbox** involves building a scalable, reliable, and performant distributed file storage with features like file upload/download, synchronization, versioning, and sharing. Let’s break it down step-by-step.

---

# Design Dropbox-like File Storage System

---

## 1️⃣ Requirements

### Functional

* Users can upload, download, and delete files.
* Files sync across multiple devices in near real-time.
* Support file versioning and restore previous versions.
* Handle large files efficiently.
* Support sharing files with other users.
* Offline access with sync when online.
* Conflict resolution for concurrent edits.

### Non-Functional

* Highly scalable and available.
* Data durability and reliability.
* Low latency access.
* Secure data storage and transfer.

---

## 2️⃣ High-Level Components

| Component                      | Responsibility                                            |
| ------------------------------ | --------------------------------------------------------- |
| Client Apps                    | Upload/download files, sync local changes                 |
| API Gateway                    | Accept requests, authentication                           |
| Metadata Service               | Store file metadata (filename, size, versions, ownership) |
| Storage Service                | Store actual file data (object storage, block storage)    |
| Sync Service                   | Track changes, sync files across devices                  |
| Conflict Resolution            | Handle concurrent edits and sync conflicts                |
| Notification Service           | Notify clients of updates and sync triggers               |
| Version Control                | Manage file versions and rollback                         |
| Authentication & Authorization | Secure access control                                     |

---

## 3️⃣ Data Model

| Entity       | Fields                                                 |
| ------------ | ------------------------------------------------------ |
| FileMetadata | fileId, ownerId, filename, size, timestamps, versions  |
| FileVersion  | versionId, fileId, storagePointer, checksum, timestamp |
| User         | userId, credentials, permissions                       |
| ShareInfo    | fileId, sharedWithUserId, permissions                  |

---

## 4️⃣ Storage Design

* **File data** stored in distributed object storage (e.g., AWS S3, HDFS).
* Store files in **chunks/blocks** (like 4MB blocks).
* Maintain file version history as delta or full copies.
* Use checksums for data integrity verification.

---

## 5️⃣ Sync and Conflict Resolution

* Client detects local changes and sends diffs or full files to Sync Service.
* Sync Service updates metadata and storage.
* Notify other clients of changes for near real-time sync.
* Handle conflicts by:

    * Last-write-wins (simple).
    * Create conflict copies.
    * Use operational transforms for complex edits.

---

## 6️⃣ Scalability Considerations

* Partition metadata DB by user or fileId.
* Use CDN or edge caching for faster downloads.
* Use load balancers for API and storage services.
* Use distributed queues for sync events.
* Employ eventual consistency for metadata updates.

---

## 7️⃣ Security & Privacy

* Encrypt data in transit (TLS) and at rest.
* Use OAuth or similar for authentication.
* Fine-grained permission control for sharing.
* Audit logging for access and changes.

---

## 8️⃣ Example User Flow

1. User uploads a file → Client sends file chunks to Storage Service via API Gateway.
2. Storage Service stores chunks, returns pointers.
3. Metadata Service updates file metadata and version info.
4. Sync Service notifies other devices.
5. Other devices download updates and sync locally.
6. On conflict, system resolves or creates conflict copies.

---

## Interview Tips

* Clarify assumptions: max file size, concurrent users.
* Emphasize chunking and deduplication (if applicable).
* Discuss sync strategies and conflict resolution.
* Highlight security and data integrity.
* Consider backup and disaster recovery.

---

## 34. Design a video streaming platform like YouTube.

Designing a **video streaming platform like YouTube** is a complex but classic system design challenge. It involves video upload, processing, storage, streaming, recommendation, and scalability. Here’s a detailed breakdown.

---

# Design YouTube-like Video Streaming Platform

---

## 1️⃣ Requirements

### Functional

* Users can upload videos.
* Process videos into multiple formats/resolutions (transcoding).
* Store and serve videos efficiently.
* Support video streaming with minimal buffering.
* Search and recommend videos.
* Support likes, comments, subscriptions.
* Handle live streaming (optional).

### Non-Functional

* Highly scalable to billions of users/videos.
* Low latency video streaming globally.
* High availability and fault tolerance.
* Efficient storage and bandwidth usage.

---

## 2️⃣ High-Level Components

| Component                      | Responsibility                                    |
| ------------------------------ | ------------------------------------------------- |
| Client Apps                    | Upload, watch, interact with videos               |
| API Gateway                    | Handles client requests                           |
| Video Upload Service           | Accepts uploads, validates content                |
| Transcoding Service            | Converts videos into multiple formats/resolutions |
| Storage Service                | Stores raw and transcoded videos                  |
| Content Delivery Network (CDN) | Distributes video content globally                |
| Metadata Service               | Stores video metadata, user info, comments, etc.  |
| Recommendation Service         | Suggests videos based on user preferences         |
| Search Service                 | Indexes and searches video metadata               |
| Analytics Service              | Tracks views, watch time, user behavior           |

---

## 3️⃣ Video Upload & Processing Flow

1. User uploads video → Video Upload Service.
2. Upload service stores raw video in storage.
3. Transcoding Service processes video into different formats/resolutions.
4. Transcoded videos stored in storage.
5. Metadata Service updates video info.
6. Video available for streaming via CDN.

---

## 4️⃣ Storage & Streaming

* Store videos in distributed object storage (e.g., S3, GCS).
* Use chunked storage (e.g., HLS/DASH protocols) for adaptive streaming.
* Use CDN edge servers to cache and deliver video segments close to users.
* Support adaptive bitrate streaming for quality adjustments.

---

## 5️⃣ Scalability Considerations

* Partition metadata by video ID or user ID.
* Horizontally scale transcoding and upload services.
* Use queues (Kafka) to decouple upload & transcoding.
* Use global CDN to reduce latency and bandwidth costs.
* Use caching for popular videos.

---

## 6️⃣ Search & Recommendation

* Index video metadata with a search engine (Elasticsearch).
* Recommendation engine uses ML models to suggest relevant videos.
* Track user interactions for personalized recommendations.

---

## 7️⃣ Analytics & Monitoring

* Collect user behavior data (views, likes, watch time).
* Monitor streaming quality (buffering events, errors).
* Use data for improving recommendations and system performance.

---

## 8️⃣ Data Model (Simplified)

| Entity  | Fields                                                          |
| ------- | --------------------------------------------------------------- |
| Video   | videoId, uploaderId, title, description, tags, metadata, status |
| User    | userId, subscriptions, watch history                            |
| Comment | commentId, videoId, userId, text, timestamp                     |

---

## 9️⃣ Example User Flow

1. User uploads video → transcoding jobs triggered.
2. Video ready → metadata updated, CDN caches segments.
3. User watches video → client requests video chunks from CDN.
4. User interacts → likes, comments, subscribes.
5. System updates analytics and recommendation data.

---

## Interview Tips

* Clarify scope (live streaming? comments?).
* Emphasize video chunking and adaptive streaming.
* Talk about storage and CDN usage.
* Discuss decoupling components with queues.
* Highlight scaling transcoding and storage.
* Mention security (DRM, copyright).

---

## 35. Design an online code compiler.

Designing an **online code compiler** (like an online IDE or coding platform) involves building a system that can receive source code from users, compile/run it securely and efficiently, and return the output or errors. Here’s a detailed breakdown of how to design such a system.

---

# Design Online Code Compiler

---

## 1️⃣ Requirements

### Functional

* Users submit code in multiple programming languages.
* Compile and/or run code and return output/errors.
* Support multiple simultaneous users.
* Support code editing, saving, and history (optional).
* Provide sandboxed environment for secure execution.
* Limit resource usage (CPU, memory, execution time).
* Support input/output during execution (stdin/stdout).

### Non-Functional

* Secure execution environment to prevent exploits.
* Low latency for compilation and execution.
* Scalable to many concurrent users.
* Reliable and fault-tolerant.

---

## 2️⃣ High-Level Components

| Component            | Responsibility                                   |
| -------------------- | ------------------------------------------------ |
| Client Interface     | Web or mobile UI for code editing and submission |
| API Gateway          | Receive compile/run requests                     |
| Job Queue            | Manage incoming compilation/execution jobs       |
| Worker Nodes         | Execute code in isolated sandboxes               |
| Sandboxing/Container | Securely run code with resource limits           |
| Result Service       | Store and return output/errors                   |
| Language Support     | Compiler/interpreter binaries and environments   |
| Logging & Monitoring | Track usage, errors, performance                 |

---

## 3️⃣ Execution Flow

1. User submits code + input + language via Client.
2. API Gateway validates request, pushes job to Job Queue.
3. Worker Node picks job, spins up sandbox/container.
4. Worker compiles (if needed) and executes code inside sandbox.
5. Captures stdout, stderr, execution time, memory usage.
6. Stores result and sends response to client.
7. Sandbox destroyed to clean up.

---

## 4️⃣ Key Considerations

### a) Security

* Run code in isolated environments (Docker containers, VMs).
* Limit CPU, memory, and execution time.
* Prevent network access from inside sandbox.
* Sanitize inputs and outputs.

### b) Scalability

* Use Job Queue (e.g., RabbitMQ, Kafka) to buffer jobs.
* Horizontally scale worker nodes.
* Auto-scale workers based on load.

### c) Language Support

* Preinstall compilers/interpreters for supported languages.
* Maintain versioning and environment configs.

### d) Input/Output Handling

* Support stdin input for running programs.
* Return stdout and stderr back to users.

---

## 5️⃣ Architecture Diagram (Simplified)

```
User → Client → API Gateway → Job Queue → Worker Nodes (Sandboxed Execution) → Result Store → Client
```

---

## 6️⃣ Example Data Model (Job)

\| JobID | UserID | Language | SourceCode | Input | Status | Output | Error | ExecutionTime | MemoryUsed |

---

## 7️⃣ Enhancements & Features

* Code auto-save and version history.
* Real-time collaborative editing.
* Support debugging with step-through.
* Persistent storage of user projects.
* Usage limits and quotas.

---

## Interview Tips

* Emphasize sandboxing & security.
* Discuss resource limits and job scheduling.
* Talk about fault tolerance if worker crashes.
* Explain multi-language support approach.
* Highlight asynchronous job processing for scalability.

---

## 36. Design an e-commerce platform like Amazon.

Designing an **e-commerce platform like Amazon** involves building a large-scale system to handle product listings, user management, shopping carts, orders, payments, and more. Here's a detailed approach covering core components, scalability, and key challenges.

---

# Design Amazon-like E-commerce Platform

---

## 1️⃣ Requirements

### Functional

* User registration, login, and profile management.
* Product catalog browsing with search and filters.
* Shopping cart to add/remove products.
* Order placement and tracking.
* Payment processing.
* User reviews and ratings.
* Inventory management.
* Recommendations and personalized offers.

### Non-Functional

* Highly available and scalable.
* Low latency responses.
* Secure transactions.
* Fault tolerant and consistent.

---

## 2️⃣ Core Components

| Component             | Responsibility                                    |
| --------------------- | ------------------------------------------------- |
| User Service          | Manage user accounts, authentication              |
| Product Catalog       | Store product info, categories, prices, inventory |
| Search Service        | Provide search and filtering capabilities         |
| Shopping Cart         | Manage user cart sessions and items               |
| Order Service         | Handle order creation, status updates             |
| Payment Gateway       | Process payments securely                         |
| Inventory Service     | Track product stock levels                        |
| Review Service        | Store and display user reviews and ratings        |
| Recommendation Engine | Suggest products based on user behavior           |
| Notification Service  | Send emails, SMS notifications                    |

---

## 3️⃣ Data Model (Simplified)

| Entity  | Fields                                                   |
| ------- | -------------------------------------------------------- |
| User    | userId, name, email, passwordHash, address, payment info |
| Product | productId, name, description, price, category, stock     |
| Cart    | cartId, userId, list of productIds and quantities        |
| Order   | orderId, userId, products, status, paymentId, timestamps |
| Payment | paymentId, orderId, amount, status                       |
| Review  | reviewId, userId, productId, rating, comment, timestamp  |

---

## 4️⃣ Workflow Examples

### User Browsing & Searching

* User sends query → Search Service queries product catalog and returns results.
* Caching popular searches for faster response.

### Adding to Cart

* Cart Service adds products to user’s cart in session or DB.

### Order Placement

* Validate cart → check inventory.
* Reserve inventory.
* Process payment via Payment Gateway.
* Confirm order → update inventory.
* Notify user of order status.

---

## 5️⃣ Scalability & Architecture

* Use **microservices architecture** for modularity.
* API Gateway routes user requests to services.
* Use **NoSQL DB** (e.g., DynamoDB) for product catalog & user sessions for scalability.
* Use **relational DB** (e.g., MySQL) for transactional data like orders/payments.
* Cache frequently accessed data (Redis, Memcached).
* Use **message queues** (Kafka, RabbitMQ) for asynchronous processing (e.g., order fulfillment).
* CDN for static content (images, CSS, JS).

---

## 6️⃣ Reliability & Fault Tolerance

* Replicate databases for high availability.
* Use circuit breakers and retries for external payment services.
* Implement fallback mechanisms for non-critical features.
* Perform backups and disaster recovery plans.

---

## 7️⃣ Security Considerations

* Encrypt sensitive data (passwords, payment info).
* Use OAuth/JWT for authentication.
* Validate all user inputs to prevent injection attacks.
* PCI compliance for payment processing.
* Monitor and audit all transactions.

---

## 8️⃣ Additional Features

* Personalized recommendations based on ML.
* Real-time inventory updates.
* Multi-region deployment for global users.
* Analytics dashboard for sellers.

---

## 9️⃣ Example System Diagram

```
User → API Gateway → Microservices (User, Product, Cart, Order, Payment, Search, Review)
             ↓                             ↑
         Cache Layer                   Message Queue
             ↓                             ↑
         Databases                    Async Workers
```

---

## Interview Tips

* Clarify requirements and assumptions upfront.
* Explain data partitioning strategies.
* Discuss consistency models for orders and inventory.
* Talk about scaling components independently.
* Cover security and compliance briefly.

---

## 37. Design an online payment system like Stripe.

Designing an **online payment system like Stripe** requires careful consideration of security, reliability, scalability, and compliance. Stripe processes payments between customers and merchants securely and efficiently. Below is a detailed design outline.

---

# Design Online Payment System (like Stripe)

---

## 1️⃣ Requirements

### Functional

* Accept payments via credit/debit cards, wallets, bank transfers.
* Support multiple payment methods and currencies.
* Securely store and manage customer payment info (tokens).
* Handle payment authorization, capture, refunds, and disputes.
* Provide APIs for merchants to integrate.
* Webhooks for payment events.
* Dashboard for transaction history and analytics.

### Non-Functional

* High availability and fault tolerance.
* PCI-DSS compliance (security standards for card data).
* Low latency for payment processing.
* Scalable to millions of transactions daily.
* Strong fraud detection/prevention.

---

## 2️⃣ Core Components

| Component            | Responsibility                                    |
| -------------------- | ------------------------------------------------- |
| API Gateway          | Expose RESTful APIs to merchants and clients      |
| Payment Processor    | Handle payment authorization, capture, refunds    |
| Tokenization Service | Convert card details into tokens (PCI compliance) |
| Customer Vault       | Store payment tokens securely                     |
| Fraud Detection      | Analyze transactions for fraud patterns           |
| Transaction Ledger   | Record all transaction data                       |
| Webhook Service      | Notify merchants about payment status/events      |
| Settlement Service   | Transfer funds to merchant bank accounts          |
| Dashboard Service    | Provide UI for merchants to view reports          |

---

## 3️⃣ Payment Flow

1. **Tokenization:** Client sends card info → Tokenization Service returns a token.
2. **Payment Request:** Merchant sends payment request with token to API Gateway.
3. **Authorization:** Payment Processor authorizes payment with payment networks/banks.
4. **Capture:** Payment captured and reserved.
5. **Settlement:** Funds transferred to merchant’s account after clearing.
6. **Notification:** Webhook Service notifies merchant about payment status.
7. **Refund/Dispute:** Handle refunds or disputes if raised.

---

## 4️⃣ Security & Compliance

* Card data never stored directly; use tokens.
* PCI DSS compliance for all card handling.
* Use HTTPS and encryption in transit and at rest.
* Strong authentication for API access (OAuth, API keys).
* Monitor for suspicious activities.

---

## 5️⃣ Scalability & Reliability

* Use asynchronous processing for non-critical tasks.
* Partition data by merchant ID for scale.
* Replicate transaction data for durability.
* Circuit breakers when calling external payment networks.
* Auto-scale components based on load.

---

## 6️⃣ Data Model (Simplified)

| Entity         | Fields                                                      |
| -------------- | ----------------------------------------------------------- |
| Customer       | customerId, paymentTokens, billingInfo                      |
| Payment        | paymentId, customerId, amount, currency, status, timestamps |
| Merchant       | merchantId, accountInfo, API keys                           |
| TransactionLog | transactionId, paymentId, status, responseCode, timestamps  |

---

## 7️⃣ Additional Features

* Support subscriptions and recurring billing.
* Multi-currency support with FX conversion.
* Multi-step 3D Secure authentication support.
* Fraud analytics and risk scoring.
* Real-time analytics and reporting.

---

## 8️⃣ Architecture Diagram (Simplified)

```
Merchant/Client → API Gateway → Tokenization → Payment Processor → Banks/Networks
                                   ↓
                        Customer Vault & Transaction Ledger
                                   ↓
                         Fraud Detection & Webhook Service
                                   ↓
                          Merchant Dashboard & Analytics
```

---

## Interview Tips

* Emphasize security and PCI compliance.
* Discuss tokenization and why it’s critical.
* Explain payment authorization vs capture.
* Talk about asynchronous processing and reliability.
* Mention fraud detection strategies.

---

## 38. Design a stock trading platform.

Designing a **stock trading platform** involves building a highly performant, secure, and reliable system to handle real-time order placement, matching, execution, and settlement of trades. Below is a detailed approach:

---

# Design Stock Trading Platform

---

## 1️⃣ Requirements

### Functional

* User registration, authentication, and portfolio management.
* Real-time stock price updates and market data.
* Support placing different order types (market, limit, stop-loss).
* Order matching engine to match buy/sell orders.
* Trade execution and confirmation.
* Order book management per stock.
* Historical trade data and reporting.
* Notifications for order status, executions.
* Compliance with financial regulations.

### Non-Functional

* Ultra low latency and high throughput.
* High availability and fault tolerance.
* Strong data consistency.
* Secure and auditable.

---

## 2️⃣ Core Components

| Component            | Responsibility                                         |
| -------------------- | ------------------------------------------------------ |
| User Service         | Authentication, portfolio, account management          |
| Market Data Service  | Real-time stock prices, order book info                |
| Order Management     | Accept, validate, and queue orders                     |
| Matching Engine      | Match buy and sell orders based on price/time priority |
| Trade Execution      | Confirm and record executed trades                     |
| Notification Service | Inform users of order/trade events                     |
| Compliance & Audit   | Monitor trades, regulatory reporting                   |
| Historical Data      | Store past trades, market data for analysis            |

---

## 3️⃣ Data Model (Simplified)

| Entity | Fields                                                       |
| ------ | ------------------------------------------------------------ |
| User   | userId, credentials, portfolio, account balances             |
| Order  | orderId, userId, stockSymbol, quantity, price, type, status  |
| Trade  | tradeId, buyOrderId, sellOrderId, price, quantity, timestamp |
| Stock  | symbol, companyName, currentPrice                            |

---

## 4️⃣ Key Processes

### Order Placement

* User submits order → Order Management validates and queues.
* Send to Matching Engine.

### Order Matching

* Matching Engine keeps order book per stock.
* Matches buy & sell orders by price and time priority.
* Partial fills supported.

### Trade Execution

* Execute matched trades → update portfolios and balances.
* Persist trade info.
* Notify users.

---

## 5️⃣ Scalability & Performance

* Use in-memory data structures (e.g., Redis) for order books for speed.
* Partition order books by stock symbols.
* Use message queues to decouple components.
* Deploy Matching Engine in low-latency environment.
* Horizontal scaling of user and market data services.

---

## 6️⃣ Reliability & Fault Tolerance

* Replicate trade data for durability.
* Use consensus algorithms for critical state consistency.
* Graceful degradation under heavy load.
* Disaster recovery with backups.

---

## 7️⃣ Security & Compliance

* Use strong authentication (MFA).
* Encrypt sensitive data.
* Audit trails of orders and trades.
* Regulatory compliance (e.g., SEC, MiFID).
* Real-time fraud detection.

---

## 8️⃣ Example System Diagram

```
User → API Gateway → User Service → Order Management → Matching Engine → Trade Execution
                         ↓                                      ↓
                Market Data Service                      Notification Service
```

---

## Interview Tips

* Highlight latency-sensitive design.
* Explain order matching algorithms.
* Discuss consistency and durability.
* Address security and compliance.
* Talk about handling edge cases like partial fills, cancellations.

---

## 39. Design a parking lot system.

Designing a **parking lot system** is a classic system design question focusing on managing parking spots, vehicle entries/exits, and billing. Here’s a detailed breakdown:

---

# Design Parking Lot System

---

## 1️⃣ Requirements

### Functional

* Vehicle entry and exit management.
* Allocate parking spots based on availability and vehicle type.
* Track parking duration for billing.
* Support multiple vehicle types (car, motorcycle, truck).
* Support different parking spot types (compact, large, handicapped).
* Real-time spot availability display.
* Billing and payment processing.

### Non-Functional

* Efficient spot allocation.
* Scalability for large parking lots.
* Fault tolerance for hardware failures (gates, sensors).
* Real-time updates.

---

## 2️⃣ Core Components

| Component            | Responsibility                                    |
| -------------------- | ------------------------------------------------- |
| Entry Gate           | Detect vehicle entry, issue tickets               |
| Exit Gate            | Accept ticket, calculate charges, process payment |
| Parking Spot Manager | Track spot availability and assign spots          |
| Billing System       | Calculate parking fees based on duration          |
| Vehicle Detector     | Sensors to detect spot occupancy                  |
| Display System       | Show available spots in real-time                 |
| User Interface       | Mobile/web app for users to check availability    |

---

## 3️⃣ Data Model (Simplified)

| Entity      | Fields                                                   |
| ----------- | -------------------------------------------------------- |
| ParkingSpot | spotId, type, isOccupied                                 |
| Ticket      | ticketId, vehicleId, spotId, entryTime, exitTime, amount |
| Vehicle     | vehicleId, type, licensePlate                            |

---

## 4️⃣ Workflow

### Vehicle Entry

1. Vehicle arrives → Entry Gate issues ticket with timestamp.
2. Parking Spot Manager assigns appropriate free spot.
3. Vehicle parks; sensors mark spot as occupied.

### Vehicle Exit

1. Vehicle presents ticket → Exit Gate scans.
2. Billing System calculates fee based on duration.
3. User pays (cash/card/app).
4. Spot marked free.

---

## 5️⃣ Spot Allocation Strategy

* First come, first serve for free spots matching vehicle type.
* Optionally reserve spots for handicapped, VIP, or electric vehicles.
* Balance load to avoid clustering.

---

## 6️⃣ Scalability & Fault Tolerance

* Use distributed system for large parking lots with multiple gates.
* Fail-safe sensors with manual override.
* Real-time updates through event-driven architecture.
* Use caching for availability info.

---

## 7️⃣ Additional Features

* Mobile app for pre-booking spots.
* Integration with navigation apps.
* Dynamic pricing based on demand.
* Support for monthly subscriptions.

---

## 8️⃣ Example System Diagram

```
Vehicle → Entry Gate → Parking Spot Manager → Sensors → Billing System → Exit Gate
                                       ↓
                                  Display System
```

---

## Interview Tips

* Clarify scope and parking lot size.
* Discuss real-time spot tracking challenges.
* Explain design of ticketing and billing.
* Talk about sensor failures and manual overrides.
* Cover scalability for multi-level parking garages.

---

## 40. Design an elevator control system.

Designing an **Elevator Control System** is a classic system design problem that focuses on efficiently managing multiple elevators servicing requests in a building to minimize wait and travel times.

---

# Design Elevator Control System

---

## 1️⃣ Requirements

### Functional

* Control multiple elevators in a building.
* Handle pickup requests from floors (up/down).
* Handle drop-off requests inside elevators.
* Optimize elevator assignment to reduce wait times.
* Support different modes (normal, express, maintenance).
* Display elevator status and position.

### Non-Functional

* Efficient scheduling and dispatch.
* Real-time response.
* Fault tolerance (e.g., elevator breakdown).
* Safety compliance.

---

## 2️⃣ Core Components

| Component           | Responsibility                                         |
| ------------------- | ------------------------------------------------------ |
| Elevator Controller | Central system that manages all elevators              |
| Elevator Unit       | Individual elevator with position, state, and requests |
| Request Handler     | Receives pickup/drop-off requests and queues them      |
| Scheduler           | Assigns elevators to requests optimally                |
| Sensors & Actuators | Detect current floor, open/close doors, move elevator  |
| Display Module      | Shows elevator info on floors and inside cabins        |

---

## 3️⃣ Key Data Structures

* **Request Queue:** Pending requests (floor, direction).
* **Elevator State:** Current floor, direction, door status, load.
* **Pickup Requests:** Floors waiting for an elevator going up/down.
* **Destination Requests:** Floors selected inside elevator.

---

## 4️⃣ Workflow

### When a Pickup Request Arrives:

* Request Handler receives (floor, direction).
* Scheduler evaluates all elevators.
* Assign request to best-suited elevator based on:

    * Elevator proximity.
    * Direction of travel.
    * Current load.
* Elevator updates its destination queue.

### Elevator Movement:

* Moves floor by floor, stopping at requested floors.
* Updates state and signals arrival.
* Opens/closes doors, waits for boarding/alighting.

---

## 5️⃣ Scheduling Strategies

* **Nearest Car Algorithm:** Assigns request to nearest elevator going in same direction.
* **Collective Control:** Elevator stops at all floors requested in direction of travel.
* **Zoning:** Divide building floors among elevators.
* **Dynamic Scheduling:** Real-time optimization using algorithms or ML.

---

## 6️⃣ Handling Edge Cases

* Elevator breakdown → Reassign requests.
* Overload → Deny new requests.
* Emergency mode → Elevator goes to predefined floor.
* Idle elevators → Return to default floors or standby.

---

## 7️⃣ Example System Diagram

```
User Requests → Request Handler → Scheduler → Elevator Controller → Elevator Units
                          ↑                             ↓
                    Display System              Sensors & Actuators
```

---

## 8️⃣ Interview Tips

* Clarify number of elevators and floors.
* Discuss scheduling algorithms and trade-offs.
* Talk about fault tolerance and safety.
* Explain how to minimize wait and travel time.
* Mention scalability for very tall buildings.

---

## 41. Design a hotel booking system.

Designing a **hotel booking system** involves managing hotel rooms, availability, reservations, user profiles, and payments with scalability and reliability. Here's a detailed system design:

---

# Design Hotel Booking System

---

## 1️⃣ Requirements

### Functional

* Search hotels by location, date, price, ratings.
* Check room availability.
* Book and cancel reservations.
* User account management.
* Support multiple room types and hotels.
* Payment processing.
* Manage hotel details and reviews.
* Send booking confirmations and notifications.

### Non-Functional

* Handle high traffic during peak seasons.
* Consistent and reliable availability checks.
* Secure user data and payments.
* Scalable to support many hotels and users.

---

## 2️⃣ Core Components

| Component            | Responsibility                            |
| -------------------- | ----------------------------------------- |
| User Service         | Manage user registration, login, profiles |
| Hotel Service        | Store hotel info, rooms, amenities        |
| Search Service       | Search hotels by criteria                 |
| Availability Service | Check and update room availability        |
| Booking Service      | Create, cancel, modify reservations       |
| Payment Service      | Process payments and refunds              |
| Notification Service | Send booking confirmations, reminders     |
| Review Service       | Manage hotel reviews and ratings          |

---

## 3️⃣ Data Model (Simplified)

| Entity  | Fields                                                       |
| ------- | ------------------------------------------------------------ |
| User    | userId, name, email, passwordHash, phone                     |
| Hotel   | hotelId, name, location, description, rating                 |
| Room    | roomId, hotelId, type, price, amenities                      |
| Booking | bookingId, userId, roomId, checkInDate, checkOutDate, status |
| Payment | paymentId, bookingId, amount, status                         |
| Review  | reviewId, userId, hotelId, rating, comment                   |

---

## 4️⃣ Workflow

### Searching & Booking

* User searches → Search Service queries Hotel + Availability Service.
* Show available rooms.
* User selects room and dates → Booking Service checks availability again.
* Booking created → Payment Service processes payment.
* Confirmation sent via Notification Service.

### Cancelation

* User requests cancelation → Booking status updated, refund processed if applicable.

---

## 5️⃣ Scalability & Architecture

* Use caching (Redis) for popular hotel searches.
* Use relational DB for transactional booking data.
* Use NoSQL for hotel info and reviews for flexibility.
* Asynchronous processing for notifications.
* Microservices architecture for modularity.

---

## 6️⃣ Handling Concurrency

* Use distributed locks or optimistic concurrency when booking rooms.
* Prevent double booking with atomic updates or transactions.

---

## 7️⃣ Additional Features

* Support for discounts, coupons, loyalty programs.
* Multi-currency and language support.
* Integration with third-party hotel APIs.
* Analytics dashboard for hotels.

---

## 8️⃣ Example System Diagram

```
User → API Gateway → Search Service → Hotel Service + Availability Service
               ↓                                  ↓
          Booking Service ← Payment Service ← Notification Service
```

---

## Interview Tips

* Clarify availability consistency and concurrency control.
* Discuss database schema and indexing.
* Explain payment integration and failure handling.
* Talk about scaling for peak loads.
* Address security and privacy.

---

## 42. Design a food delivery app (e.g., Swiggy/Zomato).

Designing a **food delivery app** like Swiggy or Zomato involves building a system to connect customers, restaurants, and delivery agents efficiently. Here’s a detailed breakdown:

---

# Design Food Delivery App

---

## 1️⃣ Requirements

### Functional

* User registration and profile management.
* Restaurant listing with menus.
* Search and filter restaurants and dishes.
* Order placement and tracking.
* Real-time order status updates.
* Delivery agent assignment and tracking.
* Payment processing.
* Ratings and reviews for restaurants and delivery agents.
* Push notifications for order updates.

### Non-Functional

* Handle high traffic especially during peak hours.
* Real-time updates with low latency.
* Scalable to support millions of users.
* Secure payment processing.
* Fault tolerance and high availability.

---

## 2️⃣ Core Components

| Component            | Responsibility                                 |
| -------------------- | ---------------------------------------------- |
| User Service         | Manage users, authentication, profiles         |
| Restaurant Service   | Manage restaurant data, menus, availability    |
| Search Service       | Search and filter restaurants and dishes       |
| Order Service        | Manage order lifecycle (create, update, track) |
| Delivery Service     | Assign and track delivery agents               |
| Payment Service      | Process payments securely                      |
| Notification Service | Push order updates and alerts                  |
| Review Service       | Handle ratings and feedback                    |
| Geo-Location Service | Track delivery agent and map routes            |

---

## 3️⃣ Data Model (Simplified)

| Entity        | Fields                                                      |
| ------------- | ----------------------------------------------------------- |
| User          | userId, name, email, phone, address                         |
| Restaurant    | restaurantId, name, location, menu, ratings                 |
| MenuItem      | itemId, restaurantId, name, description, price              |
| Order         | orderId, userId, restaurantId, items\[], status, timestamps |
| DeliveryAgent | agentId, name, location, availability                       |
| Payment       | paymentId, orderId, amount, status                          |
| Review        | reviewId, userId, restaurantId/agentId, rating, comment     |

---

## 4️⃣ Workflow

### Order Placement

* User searches restaurants → selects items → places order.
* Order Service creates order, assigns to restaurant.
* Restaurant confirms order and prepares food.
* Delivery Service assigns nearest available delivery agent.
* Delivery agent picks up and delivers food.
* User tracks order in real-time.
* Payment processed on order or delivery.

---

## 5️⃣ Scalability & Performance

* Use caching for popular restaurants and menus.
* Use message queues (Kafka) for asynchronous order processing.
* Partition data by geographic regions.
* Use CDN for static content (images, menus).
* Real-time updates via WebSockets or push notifications.

---

## 6️⃣ Fault Tolerance & Reliability

* Retry mechanisms for failed order or payment processing.
* Circuit breaker patterns for external service calls.
* Backup agents if delivery fails.
* Redundant services for high availability.

---

## 7️⃣ Additional Features

* Promotions, discounts, and loyalty programs.
* Estimated delivery time calculation.
* Multi-language and multi-currency support.
* Customer support chat integration.
* Analytics for restaurants and delivery performance.

---

## 8️⃣ Example System Diagram

```
User → API Gateway → User Service + Search Service + Order Service
                                  ↓                 ↓
                          Restaurant Service    Delivery Service
                                  ↓                 ↓
                         Payment Service ← Notification Service
```

---

## Interview Tips

* Clarify user flow and priority features.
* Discuss real-time tracking and notification mechanisms.
* Explain delivery agent assignment algorithms.
* Talk about data partitioning by region.
* Address payment and security concerns.

---

## 43. Design a search engine.

Designing a **search engine** is a complex, large-scale system problem that involves crawling, indexing, querying, ranking, and serving search results efficiently. Here's a detailed breakdown for interview preparation:

---

# Design a Search Engine

---

## 1️⃣ Requirements

### Functional

* Crawl and index billions of web pages.
* Support keyword and phrase search.
* Return ranked, relevant results quickly.
* Support basic features like autocomplete and spell correction.
* Handle multiple languages.
* Provide snippet/summary for results.

### Non-Functional

* Handle massive scale and throughput.
* Low latency for search queries.
* Highly available and fault-tolerant.
* Fresh and up-to-date indexes.

---

## 2️⃣ Core Components

| Component        | Responsibility                                                    |
| ---------------- | ----------------------------------------------------------------- |
| Crawler (Spider) | Automatically browse the web and fetch pages                      |
| Parser           | Extract useful content and metadata from pages                    |
| Indexer          | Create and update inverted indexes for fast lookup                |
| Query Processor  | Parse and interpret user queries                                  |
| Ranking Engine   | Rank pages based on relevance algorithms (e.g., PageRank, TF-IDF) |
| Storage          | Store raw pages, indexes, and metadata                            |
| Frontend/UI      | User interface for search input and results display               |

---

## 3️⃣ Detailed Workflow

### Crawling

* Start from a list of seed URLs.
* Fetch pages respecting robots.txt and politeness policies.
* Extract links and add to crawl queue.
* Store raw HTML and metadata.

### Parsing & Indexing

* Parse HTML to extract text, title, keywords.
* Create inverted index mapping words → list of documents with positions.
* Update index incrementally.

### Query Processing

* Parse query into tokens.
* Retrieve matching documents from index.
* Apply ranking algorithms considering keyword frequency, page importance, freshness.
* Generate snippets showing query context.

### Serving Results

* Return top-k ranked documents with snippets.
* Support pagination.

---

## 4️⃣ Data Structures

* **Inverted Index:** Maps terms to document IDs and positions.
* **Forward Index:** Maps documents to terms.
* **Document Store:** Raw content, metadata.
* **Link Graph:** For PageRank calculations.

---

## 5️⃣ Scalability & Architecture

* Use distributed crawling and indexing across many servers.
* Partition index by terms or document IDs (sharding).
* Use MapReduce for batch processing of index updates.
* Cache popular queries and results.
* Use CDNs to serve static content quickly.

---

## 6️⃣ Ranking Algorithms

* TF-IDF (Term Frequency-Inverse Document Frequency)
* PageRank or other link-based ranking.
* Machine learning models for personalization and relevance.
* Freshness and user context signals.

---

## 7️⃣ Handling Real-World Challenges

* Duplicate content detection.
* Spam and malicious site filtering.
* Handling multi-language and synonyms.
* Autocomplete and typo correction using tries and edit-distance algorithms.
* Updating indexes efficiently.

---

## 8️⃣ Example System Diagram

```
Crawler → Parser → Indexer → Distributed Storage
                                    ↓
                             Query Processor → Ranking Engine → Frontend/UI
```

---

## Interview Tips

* Clarify scale and scope of search engine.
* Explain crawling policies and challenges.
* Describe index data structures and update strategies.
* Discuss ranking metrics and ML integration.
* Talk about caching and query latency optimization.

---

## 44. Design a blogging platform like Medium.

Designing a **blogging platform like Medium** involves managing user-generated content, social features, content discovery, and scalability. Here’s a detailed system design breakdown:

---

# Design a Blogging Platform (like Medium)

---

## 1️⃣ Requirements

### Functional

* User registration, profiles, and authentication.
* Write, edit, publish, and delete blog posts.
* Rich text editor with media (images, videos).
* Follow users and tags.
* Like, comment, and share posts.
* Search and browse by tags, authors, popularity.
* Personalized feed based on follows and interests.
* Notifications (new posts, comments, likes).
* Bookmark/favorite posts.
* Version control for drafts and published posts.

### Non-Functional

* Handle large numbers of users and posts.
* Low latency for feed loading and searching.
* Scalable storage for text and media.
* Secure and prevent spam or abuse.

---

## 2️⃣ Core Components

| Component             | Responsibility                                   |
| --------------------- | ------------------------------------------------ |
| User Service          | User profiles, authentication, and authorization |
| Post Service          | Create, update, delete, and retrieve blog posts  |
| Feed Service          | Generate personalized feeds                      |
| Follow Service        | Manage following relationships between users     |
| Comment Service       | Add, edit, delete comments on posts              |
| Like/Bookmark Service | Manage likes and bookmarks                       |
| Search Service        | Search posts by tags, content, authors           |
| Notification Service  | Send real-time notifications                     |
| Media Service         | Store and serve images/videos                    |

---

## 3️⃣ Data Model (Simplified)

| Entity   | Fields                                                                                    |
| -------- | ----------------------------------------------------------------------------------------- |
| User     | userId, username, email, passwordHash, bio, profilePic                                    |
| Post     | postId, authorId, title, content, tags\[], createdAt, updatedAt, status (draft/published) |
| Comment  | commentId, postId, userId, content, createdAt                                             |
| Follow   | followerId, followeeId                                                                    |
| Like     | likeId, userId, postId                                                                    |
| Bookmark | bookmarkId, userId, postId                                                                |

---

## 4️⃣ Workflow

### Publishing a Post

* User creates/edits post → Post Service saves draft.
* User publishes → status updated → Post indexed by Search Service.
* Followers’ feeds updated.

### Feed Generation

* Feed Service fetches posts from followed users and tags.
* Applies ranking (recency, popularity).
* Caches feeds for performance.

### Interactions

* Comments and likes saved and updated in respective services.
* Notifications sent on interactions.

---

## 5️⃣ Scalability & Architecture

* Microservices architecture for modularity.
* Use CDN for serving media.
* Cache hot posts and feeds (Redis).
* Use a relational database for transactional data.
* Use NoSQL (e.g., Elasticsearch) for search.
* Asynchronous processing for notifications and feed updates.

---

## 6️⃣ Additional Features

* Draft autosave and version history.
* Multi-device sync.
* Content moderation and spam detection.
* Analytics dashboard for authors.
* Recommendations using ML.

---

## 7️⃣ Example System Diagram

```
User → API Gateway → User Service / Post Service / Feed Service
                ↓           ↓                 ↓
        Follow Service  Comment Service   Search Service
                 ↓                    ↓               ↓
            Notification Service   Media Service    Cache/CDN
```

---

## Interview Tips

* Clarify scope: focus on core features first.
* Discuss feed generation strategies.
* Explain handling of drafts vs published posts.
* Talk about search indexing and querying.
* Address moderation and security concerns.

---

## 45. Design a collaborative whiteboard app.

Designing a **collaborative whiteboard app** is a rich problem involving real-time synchronization, multi-user interaction, conflict resolution, and efficient rendering. Here's a detailed system design for interview prep:

---

# Design Collaborative Whiteboard App

---

## 1️⃣ Requirements

### Functional

* Multiple users can draw, erase, and add shapes/text on a shared whiteboard in real-time.
* Real-time cursor and pointer tracking for all participants.
* Support undo/redo actions.
* Ability to create, save, and load multiple whiteboards.
* Support different drawing tools (pen, shapes, colors).
* Chat or voice integration (optional).
* Access control (private/public boards, permissions).

### Non-Functional

* Low latency for real-time collaboration.
* Scalability to support many concurrent users.
* Conflict-free data synchronization.
* Offline support and sync on reconnect (optional).
* Persistence and version history.

---

## 2️⃣ Core Components

| Component              | Responsibility                                        |
| ---------------------- | ----------------------------------------------------- |
| Client Application     | Capture user actions, render whiteboard, sync updates |
| Real-time Sync Service | Manage real-time message broadcasting and updates     |
| Conflict Resolution    | Resolve concurrent edits (CRDTs or OT algorithms)     |
| Storage Service        | Persist whiteboard state and version history          |
| Authentication Service | Manage users and access control                       |
| Notification Service   | Inform users of updates, user joins/leaves            |

---

## 3️⃣ Data Structures & Algorithms

* **Operational Transformation (OT)** or **Conflict-free Replicated Data Types (CRDTs)** for consistency across concurrent edits.
* Data model includes elements like strokes, shapes, text boxes with properties (position, color, size).
* History stack for undo/redo.

---

## 4️⃣ Workflow

### Real-Time Collaboration

* Client captures drawing actions (e.g., draw line from x1,y1 to x2,y2).
* Sends operations to Sync Service.
* Sync Service broadcasts updates to other clients.
* Clients apply operations locally with conflict resolution.
* Update persisted asynchronously.

### Joining & Loading

* User joins a board → client fetches latest state from Storage Service.
* Real-time connection established (WebSocket).
* User sees live updates.

### Undo/Redo

* Clients send undo/redo operations.
* Sync Service propagates to others, maintaining consistency.

---

## 5️⃣ Scalability & Architecture

* Use WebSockets or WebRTC for low-latency bi-directional communication.
* Partition users by whiteboard sessions.
* Use pub/sub message brokers (e.g., Kafka, Redis Pub/Sub) for update distribution.
* Persist snapshots periodically for faster loading.
* CDN for static assets (images, icons).

---

## 6️⃣ Challenges & Solutions

| Challenge               | Solution                                     |
| ----------------------- | -------------------------------------------- |
| Concurrent edits        | Use OT or CRDT algorithms                    |
| Network latency & drops | Client-side buffering, optimistic UI updates |
| Data persistence        | Periodic snapshots + operation logs          |
| Security & privacy      | Authentication, authorization per board      |

---

## 7️⃣ Example System Diagram

```
User Clients ←→ Real-time Sync Service ←→ Storage Service
                    ↑
            Message Broker (Pub/Sub)
                    ↑
          Authentication & Notification Services
```

---

## Interview Tips

* Explain real-time protocols (WebSocket vs HTTP).
* Discuss OT vs CRDT trade-offs.
* Highlight client-server sync models.
* Address offline and reconnection strategies.
* Talk about UI/UX considerations for collaboration.

---

## 46. Design an online voting system.

Designing an **online voting system** requires careful attention to security, integrity, scalability, and reliability to ensure votes are cast, counted, and audited properly. Here’s a detailed system design breakdown:

---

# Design an Online Voting System

---

## 1️⃣ Requirements

### Functional

* Voters can securely register and authenticate.
* Voters can cast their vote once per election.
* Support multiple types of elections (single choice, multiple choice).
* Real-time vote tallying and final result publishing.
* Audit logs for all voting activity.
* Election officials can manage elections (create, start, end).
* Voter anonymity ensured.
* Allow vote verification without compromising anonymity.

### Non-Functional

* High security to prevent fraud and tampering.
* High availability during election periods.
* Scalability to handle large number of voters.
* Data integrity and tamper-proof audit logs.
* Compliance with legal and privacy regulations.

---

## 2️⃣ Core Components

| Component            | Responsibility                                  |
| -------------------- | ----------------------------------------------- |
| Voter Registration   | Register voters, verify eligibility             |
| Authentication       | Secure login (multi-factor authentication)      |
| Voting Service       | Cast, validate, and store votes                 |
| Election Management  | Create/manage elections, configure options      |
| Vote Tally Service   | Count votes in real-time or after election ends |
| Audit & Logging      | Maintain immutable logs for all actions         |
| Notification Service | Notify voters of status, results                |
| Admin Dashboard      | Election officials monitor and manage           |

---

## 3️⃣ Security Measures

* **End-to-end encryption** of votes.
* Use of **blockchain or append-only logs** for audit trails.
* **Anonymous credentials** or blind signatures to ensure vote privacy.
* **Rate limiting** and anomaly detection to prevent fraud.
* Secure **key management** for cryptographic operations.
* **TLS** for all communications.

---

## 4️⃣ Data Model (Simplified)

| Entity    | Fields                                                           |
| --------- | ---------------------------------------------------------------- |
| Voter     | voterId, name, eligibilityStatus, registrationInfo               |
| Election  | electionId, name, description, startTime, endTime                |
| Candidate | candidateId, electionId, name                                    |
| Vote      | voteId, electionId, voterId (anonymized), candidateId, timestamp |
| AuditLog  | logId, actionType, timestamp, metadata                           |

---

## 5️⃣ Workflow

### Registration & Authentication

* Voter registers and verifies identity.
* System issues credentials for voting.

### Voting

* Voter logs in securely.
* System verifies eligibility and voting status.
* Voter casts vote (encrypted).
* Vote stored in tamper-proof storage.
* Confirmation sent to voter.

### Tallying

* Votes decrypted or tallied securely.
* Results published at election close.

### Auditing

* Immutable logs available for verification.
* Optionally third-party observers can verify correctness.

---

## 6️⃣ Scalability & Architecture

* Distributed architecture for handling large voter base.
* Use sharding by election or region.
* Caching to speed up eligibility checks.
* Asynchronous processing for vote tallying.
* Use of cloud HSM (Hardware Security Module) for key management.

---

## 7️⃣ Example System Diagram

```
Voter → Auth Service → Voting Service → Secure Vote Storage
                                      ↓
                               Vote Tally Service
                                      ↓
                              Audit & Logging Service
                                      ↓
                              Admin Dashboard / Notifications
```

---

## 8️⃣ Challenges & Solutions

| Challenge        | Solution                                          |
| ---------------- | ------------------------------------------------- |
| Vote tampering   | Encryption, blockchain/append-only logs           |
| Voter anonymity  | Blind signatures, anonymized IDs                  |
| Double voting    | Strict eligibility and vote status checks         |
| Scalability      | Distributed systems, load balancing               |
| Legal compliance | Follow election regulations and data privacy laws |

---

## Interview Tips

* Emphasize security and privacy mechanisms.
* Discuss trade-offs between transparency and anonymity.
* Explain how you’d prevent fraud and ensure auditability.
* Talk about scaling for national-level elections.
* Consider disaster recovery and failover strategies.

---

## 47. Design a load balancer.

Designing a **load balancer** is a fundamental system design problem involving distributing incoming network traffic efficiently across multiple servers to ensure high availability and reliability. Here’s a detailed breakdown:

---

# Design a Load Balancer

---

## 1️⃣ Requirements

### Functional

* Distribute client requests across multiple backend servers.
* Support multiple load balancing algorithms (Round Robin, Least Connections, IP Hash, etc.).
* Health checks to detect server availability.
* Support SSL termination (optional).
* Session persistence (sticky sessions).
* Handle millions of requests per second.
* Provide metrics and monitoring.

### Non-Functional

* High availability and fault tolerance.
* Low latency and high throughput.
* Scalability to handle traffic spikes.
* Secure communication.

---

## 2️⃣ Core Components

| Component            | Responsibility                                     |
| -------------------- | -------------------------------------------------- |
| Frontend Listener    | Accept incoming client requests                    |
| Load Balancing Logic | Decide which backend server to forward the request |
| Health Checker       | Periodically check backend server health           |
| Session Manager      | Manage sticky sessions if required                 |
| Monitoring & Logging | Collect metrics, logs, and alerts                  |

---

## 3️⃣ Load Balancing Algorithms

| Algorithm            | Description                                        | Use Case                            |
| -------------------- | -------------------------------------------------- | ----------------------------------- |
| Round Robin          | Distribute requests evenly in order                | Simple, stateless load balancing    |
| Least Connections    | Forward to server with fewest active connections   | Balancing uneven workloads          |
| IP Hash              | Use client IP to consistently route to same server | Session persistence without cookies |
| Weighted Round Robin | Assign weights to servers based on capacity        | Servers with different specs        |

---

## 4️⃣ Workflow

1. Client sends request to load balancer.
2. Load balancer performs health check on backend servers.
3. Based on selected algorithm, load balancer picks a healthy server.
4. Request is forwarded to backend server.
5. Response from backend server returned to client.

---

## 5️⃣ Health Checks

* Periodic HTTP/HTTPS/TCP checks.
* Mark servers healthy/unhealthy based on response.
* Automatically remove unhealthy servers from rotation.
* Optionally trigger alerts.

---

## 6️⃣ Architecture & Scalability

* **Single Load Balancer:** Simple setup but single point of failure.
* **Distributed Load Balancers:** Multiple LB instances with DNS or anycast IP.
* Use **Consistent Hashing** for distributed load balancers to route requests efficiently.
* Layer 4 (Transport Layer) or Layer 7 (Application Layer) load balancing.
* Use **Auto-scaling** to dynamically add/remove backend servers.

---

## 7️⃣ Sticky Sessions

* Maintain session affinity by routing requests from same client to same backend.
* Implemented via cookies or IP hashing.

---

## 8️⃣ Example System Diagram

```
Clients → Load Balancer(s) → Backend Servers
                      ↑
             Health Checker & Monitoring
```

---

## 9️⃣ Additional Features

* SSL termination to offload SSL processing from backend.
* Rate limiting and throttling.
* IP filtering and security rules.
* Logging and analytics.

---

## Interview Tips

* Clarify L4 vs L7 load balancing.
* Explain different algorithms and when to use them.
* Discuss handling failures and health checks.
* Talk about scaling the load balancer itself.
* Mention sticky sessions and challenges with them.

---

## 48. Design a distributed cron job scheduler.

Designing a **distributed cron job scheduler** involves orchestrating the execution of scheduled tasks reliably across multiple nodes while ensuring fault tolerance, scalability, and no duplicate executions. Here’s a detailed breakdown:

---

# Design a Distributed Cron Job Scheduler

---

## 1️⃣ Requirements

### Functional

* Schedule and execute jobs/tasks at specified times or intervals (e.g., cron syntax).
* Support distributed execution across multiple nodes.
* Ensure exactly-once execution (no duplicates).
* Support retries and failure handling.
* Allow job status monitoring and logging.
* Support dynamic job registration, update, and deletion.
* Support different job types (e.g., HTTP call, script execution).

### Non-Functional

* Highly available and fault tolerant.
* Scalable to many jobs and nodes.
* Low latency and high accuracy in job scheduling.
* Consistent across nodes in face of failures.

---

## 2️⃣ Core Components

| Component             | Responsibility                                   |
| --------------------- | ------------------------------------------------ |
| Job Scheduler         | Maintains schedule, triggers jobs on time        |
| Job Dispatcher        | Dispatches jobs to worker nodes                  |
| Worker Nodes          | Execute jobs and report status                   |
| Coordination Service  | Ensures leader election, job assignment, locking |
| Job Store             | Persistent storage of job definitions and logs   |
| Monitoring & Alerting | Track job health, execution logs, and failures   |

---

## 3️⃣ Key Design Challenges

| Challenge                 | Solution Approach                                       |
| ------------------------- | ------------------------------------------------------- |
| Distributed coordination  | Use leader election (e.g., via ZooKeeper, etcd, Consul) |
| Preventing duplicate runs | Use distributed locks or lease mechanisms               |
| Fault tolerance           | Heartbeats and failover mechanisms                      |
| Clock synchronization     | Rely on synchronized clocks (NTP) and tolerate drift    |
| Scalability               | Partition jobs or use sharding                          |

---

## 4️⃣ Workflow

### Leader Election & Scheduling

* Nodes participate in leader election; leader schedules jobs.
* Leader scans job schedule, triggers jobs when due.
* Leader acquires distributed lock for each job before dispatch.

### Job Dispatching

* Leader sends job execution requests to worker nodes.
* Workers execute jobs and report completion or failure.

### Failure Handling

* If a worker fails, leader can retry or assign job to another node.
* Jobs can have retry policies (max attempts, backoff).

### Dynamic Job Management

* Jobs can be added/updated/deleted via API.
* Changes propagated to all nodes via job store or coordination service.

---

## 5️⃣ Technologies & Tools

* **Coordination:** Apache ZooKeeper, etcd, Consul for leader election and locking.
* **Messaging:** Kafka, RabbitMQ, or direct RPC for dispatching jobs.
* **Storage:** Relational DB or distributed KV store for job definitions.
* **Execution:** Containers or isolated processes on worker nodes.

---

## 6️⃣ Data Model (Simplified)

| Entity       | Fields                                                       |
| ------------ | ------------------------------------------------------------ |
| Job          | jobId, cronExpression, command, status, retries, nextRunTime |
| ExecutionLog | executionId, jobId, startTime, endTime, status, output       |

---

## 7️⃣ System Diagram

```
+------------+          +---------------------+         +-------------+
|  Worker 1  | ←------- |     Job Dispatcher   | ----->  |  Worker 2   |
+------------+          +---------------------+         +-------------+
        ↑                       ↑                              ↑
        |                       |                              |
        |                       |                              |
    Job Execution           Leader Election                Job Execution
        |                       |                              |
        +-----------------------+------------------------------+
                                |
                        Coordination Service (ZooKeeper)
                                |
                        Job Store (DB / KV store)
```

---

## 8️⃣ Additional Considerations

* Use **heartbeat mechanism** to detect failed workers.
* Support **backoff retries** for failed jobs.
* Allow **job prioritization**.
* Provide **API and UI** for job monitoring and manual triggers.
* Ensure **time zone handling** for schedules.

---

## Interview Tips

* Discuss leader election and distributed locks in detail.
* Explain trade-offs between availability and consistency.
* Talk about job failure recovery and exactly-once execution.
* Discuss scaling the scheduler and workers.
* Consider clock drift and latency effects.

---

## 49. Design an authentication system with OAuth2.

Designing an **authentication system using OAuth2** involves understanding OAuth2 concepts, flow, security, and integration with clients and resource servers. Here's a detailed explanation suitable for interview preparation:

---

# Design an Authentication System with OAuth2

---

## 1️⃣ What is OAuth2?

* OAuth2 is an **authorization framework** that enables a third-party application to obtain limited access to a web service on behalf of a user.
* Commonly used for delegated access (e.g., “Login with Google”).
* Provides **authorization**, not authentication directly, but often combined with OpenID Connect for authentication.
* Defines roles:

    * **Resource Owner:** User who authorizes access.
    * **Client:** Application requesting access.
    * **Authorization Server:** Issues tokens after authenticating the user and obtaining consent.
    * **Resource Server:** Hosts protected resources (APIs).

---

## 2️⃣ OAuth2 Grant Types

* **Authorization Code Grant** (most common for server-side apps)
* **Implicit Grant** (for browser-based apps, less secure, less recommended)
* **Resource Owner Password Credentials Grant** (only trusted apps)
* **Client Credentials Grant** (machine-to-machine)
* **Device Code Grant** (IoT devices)

---

## 3️⃣ Core Components

| Component            | Responsibility                                     |
| -------------------- | -------------------------------------------------- |
| Authorization Server | Authenticate users, issue access & refresh tokens  |
| Client Application   | Requests authorization, uses tokens to access APIs |
| Resource Server      | Validates tokens and serves protected resources    |
| User                 | Grants consent to clients                          |

---

## 4️⃣ Typical OAuth2 Flow (Authorization Code Grant)

1. **User Authentication & Consent:**

    * User tries to login via client app.
    * Client redirects user to Authorization Server’s login page.

2. **Authorization Code:**

    * After successful login and consent, Authorization Server redirects back with an **authorization code**.

3. **Access Token Request:**

    * Client exchanges authorization code for an **access token** (and optionally refresh token) by authenticating itself to the Authorization Server.

4. **Access Protected Resource:**

    * Client uses access token to call Resource Server APIs.

5. **Token Refresh:**

    * When access token expires, client uses refresh token to get a new access token without user involvement.

---

## 5️⃣ Token Types

* **Access Token:** Short-lived token to access resources.
* **Refresh Token:** Longer-lived token to obtain new access tokens.
* **ID Token:** (OpenID Connect) Contains user authentication info.

---

## 6️⃣ Security Considerations

* Use **HTTPS** everywhere.
* Secure storage of tokens on client.
* Validate tokens on Resource Server (e.g., JWT signature, introspection).
* Implement **scope** to limit token permissions.
* Use **state parameter** to prevent CSRF attacks.
* Use **PKCE** (Proof Key for Code Exchange) for public clients.
* Limit token lifetimes.

---

## 7️⃣ Example Architecture

```
User → Client App ↔ Authorization Server ↔ Resource Server (API)
           ↑                   |
           └------ Authorization Code, Tokens -----
```

---

## 8️⃣ Data Model (Simplified)

| Entity       | Fields                                       |
| ------------ | -------------------------------------------- |
| User         | userId, username, passwordHash, profileData  |
| Client       | clientId, clientSecret, redirectUris, scopes |
| AccessToken  | token, userId, clientId, expiry, scopes      |
| RefreshToken | token, userId, clientId, expiry              |

---

## 9️⃣ Workflow Summary

* User authenticates via Authorization Server.
* Client obtains access token securely.
* Access token used to access Resource Server APIs.
* Refresh token used to renew access tokens without re-authentication.

---

## 10️⃣ Interview Tips

* Clarify OAuth2 roles and flows.
* Explain how tokens are issued, validated, and revoked.
* Discuss differences between OAuth2 and OpenID Connect.
* Talk about PKCE and why it’s important.
* Mention common attacks (CSRF, token leakage) and mitigations.

---

## 50. Design a chat application (group and private messaging).

Designing a **chat application** supporting both **private** and **group messaging** is a classic system design problem that involves real-time communication, message storage, user presence, and scalability. Here's a detailed design breakdown:

---

# Design a Chat Application (Private & Group Messaging)

---

## 1️⃣ Requirements

### Functional

* One-to-one private messaging.
* Group chats with multiple users.
* Real-time message delivery with low latency.
* Message history and persistence.
* User presence (online/offline status).
* Typing indicators and read receipts.
* Support for text, emojis, and media (optional).
* Notifications for new messages.

### Non-Functional

* Highly available and scalable to millions of users.
* Ensure message ordering and delivery guarantees.
* Secure communication and data privacy.
* Support multi-device synchronization.

---

## 2️⃣ Core Components

| Component            | Responsibility                             |
| -------------------- | ------------------------------------------ |
| Client App           | UI, sending/receiving messages             |
| API Gateway          | Entry point for client requests            |
| Messaging Service    | Handle message routing and delivery        |
| User Service         | Manage user profiles and presence          |
| Chat Service         | Manage chat rooms, groups, and memberships |
| Storage Service      | Persist messages and metadata              |
| Notification Service | Push notifications for offline users       |

---

## 3️⃣ Data Model (Simplified)

| Entity  | Fields                                                                          | Notes                            |
| ------- | ------------------------------------------------------------------------------- | -------------------------------- |
| User    | userId, username, status (online/offline)                                       |                                  |
| Chat    | chatId, type (private/group), participantIds                                    | For private chat: 2 participants |
| Message | messageId, chatId, senderId, content, timestamp, status (sent, delivered, read) |                                  |
| Group   | groupId, groupName, adminIds, memberIds                                         | For group management             |

---

## 4️⃣ Message Flow

### Private Message

1. User sends message from client to Messaging Service.
2. Messaging Service validates and stores the message.
3. Delivers message to recipient if online (via persistent connection).
4. If offline, store message for later delivery.
5. Update read/delivery receipts.

### Group Message

1. User sends message to group chat.
2. Messaging Service stores the message.
3. Broadcasts message to all group members currently online.
4. Store messages for offline members to receive later.

---

## 5️⃣ Real-Time Communication

* Use **WebSocket** or **TCP-based persistent connections** for bidirectional communication.
* Maintain active connections in Messaging Service or a connection manager.
* Use **publish-subscribe (pub/sub)** pattern to distribute messages efficiently.

---

## 6️⃣ Presence & Notifications

* Presence Service tracks online/offline status, updated via heartbeat pings.
* Notification Service sends push notifications for offline users using APNs, FCM, etc.

---

## 7️⃣ Scalability & Architecture

* Use **sharding/partitioning** by user ID or chat ID to distribute load.
* Deploy multiple Messaging Service instances with consistent hashing or a routing layer.
* Use **message queues** (Kafka, RabbitMQ) for asynchronous processing and delivery.
* Use **CDN or edge caching** for media files.
* Employ **database replication and partitioning** for message storage.

---

## 8️⃣ Example System Diagram

```
Users (Clients)
     ↓ WebSocket / HTTP
API Gateway
     ↓
Messaging Service ←→ User Service
     ↓
Storage (DB / Cache)
     ↓
Notification Service
```

---

## 9️⃣ Additional Features

* End-to-end encryption for message privacy.
* Message search.
* Message edits/deletions.
* Media upload and streaming.
* Multi-device sync and offline message queueing.

---

## 1️⃣0️⃣ Interview Tips

* Clarify consistency and delivery guarantees (at-least-once, exactly-once).
* Discuss message ordering in groups and private chats.
* Explain failure scenarios and recovery (e.g., reconnect, duplicate messages).
* Talk about scaling user presence and connection management.
* Consider security aspects like encryption and authentication.

---

### 🔹 **51–75: Low-Level System Design (LLD) & OOP**

---

## 51. What are SOLID principles? Give examples.

Here's a detailed explanation of **SOLID principles** with examples — great for interviews:

---

# SOLID Principles

SOLID is an acronym for five important object-oriented design principles that help create more maintainable, understandable, and flexible software.

---

## 1️⃣ Single Responsibility Principle (SRP)

**Definition:**
A class should have only one reason to change, meaning it should have only one job or responsibility.

**Example:**
Suppose you have a class that handles both user data processing and file saving. According to SRP, these responsibilities should be split:

```java
// Bad: Multiple responsibilities
class UserManager {
    void processUser() { /* logic */ }
    void saveToFile() { /* file saving logic */ }
}

// Good: Separate responsibilities
class UserProcessor {
    void processUser() { /* logic */ }
}

class FileManager {
    void saveToFile() { /* file saving logic */ }
}
```

---

## 2️⃣ Open/Closed Principle (OCP)

**Definition:**
Software entities (classes, modules, functions) should be open for extension but closed for modification.

**Example:**
Instead of modifying existing code to add new behavior, extend it through inheritance or interfaces:

```java
interface Notification {
    void send(String message);
}

class EmailNotification implements Notification {
    public void send(String message) { /* send email */ }
}

class SMSNotification implements Notification {
    public void send(String message) { /* send SMS */ }
}

// To add PushNotification, just create a new class implementing Notification
```

---

## 3️⃣ Liskov Substitution Principle (LSP)

**Definition:**
Subtypes must be substitutable for their base types without altering the correctness of the program.

**Example:**
If a function uses a base class, it should work correctly if a derived class is passed instead:

```java
class Bird {
    void fly() { }
}

class Sparrow extends Bird { }
class Ostrich extends Bird {
    void fly() {
        throw new UnsupportedOperationException("Ostrich can't fly");
    }
}

// Problem: Ostrich violates LSP because it cannot fly like a Bird
```

Solution: Redesign hierarchy so that only flying birds inherit fly method.

---

## 4️⃣ Interface Segregation Principle (ISP)

**Definition:**
Clients should not be forced to depend on interfaces they don’t use. Prefer many specific interfaces over a single general-purpose interface.

**Example:**

```java
interface Worker {
    void work();
    void eat();
}

class Robot implements Worker {
    public void work() { /* robot works */ }
    public void eat() { throw new UnsupportedOperationException(); }
}

// Problem: Robot forced to implement eat()

// Better:
interface Workable {
    void work();
}

interface Eatable {
    void eat();
}

class Robot implements Workable {
    public void work() { /* robot works */ }
}

class Human implements Workable, Eatable {
    public void work() { /* human works */ }
    public void eat() { /* human eats */ }
}
```

---

## 5️⃣ Dependency Inversion Principle (DIP)

**Definition:**
High-level modules should not depend on low-level modules; both should depend on abstractions. Abstractions should not depend on details; details should depend on abstractions.

**Example:**

```java
// Bad: High-level module depends on low-level module
class MySQLDatabase {
    void connect() { }
}

class UserService {
    MySQLDatabase db = new MySQLDatabase();
    void addUser() {
        db.connect();
        // logic
    }
}

// Good: Both depend on abstraction
interface Database {
    void connect();
}

class MySQLDatabase implements Database {
    public void connect() { }
}

class UserService {
    Database db;
    UserService(Database db) {
        this.db = db;
    }
    void addUser() {
        db.connect();
        // logic
    }
}
```

This allows easy swapping of database implementations.

---

# Summary Table

| Principle | Summary                                    |
| --------- | ------------------------------------------ |
| SRP       | One class, one responsibility              |
| OCP       | Open to extension, closed to modification  |
| LSP       | Subtypes replace base types without errors |
| ISP       | Many specific interfaces over one general  |
| DIP       | Depend on abstractions, not concretes      |

---

## 52. What is the difference between composition and inheritance?

Here’s a clear, detailed explanation of **composition vs inheritance**, which often comes up in interviews:

---

# Difference Between Composition and Inheritance

---

## 1️⃣ Inheritance

### Definition:

* Inheritance is an **"is-a"** relationship.
* It allows a class (child/subclass) to inherit properties and behaviors (methods) from another class (parent/superclass).
* It supports code reuse and polymorphism.

### Example:

```java
class Animal {
    void eat() { System.out.println("Eating"); }
}

class Dog extends Animal {
    void bark() { System.out.println("Barking"); }
}

// Dog is an Animal (is-a)
Dog dog = new Dog();
dog.eat(); // inherited
dog.bark();
```

### Pros:

* Easy to reuse code.
* Enables polymorphism and method overriding.

### Cons:

* Tightly couples child to parent.
* Inheritance hierarchies can become complex.
* Less flexible (single inheritance limits reuse in some languages).

---

## 2️⃣ Composition

### Definition:

* Composition is a **"has-a"** relationship.
* It builds complex types by combining objects of other classes.
* The containing class delegates work to its composed objects.

### Example:

```java
class Engine {
    void start() { System.out.println("Engine started"); }
}

class Car {
    private Engine engine = new Engine(); // Car has an Engine

    void startCar() {
        engine.start(); // delegation
        System.out.println("Car started");
    }
}
```

### Pros:

* More flexible and modular.
* Allows changing behavior at runtime by swapping components.
* Avoids problems of tight coupling and fragile hierarchies.

### Cons:

* Slightly more boilerplate code (delegation).
* Requires more design upfront.

---

## 3️⃣ When to Use Which?

| Aspect         | Inheritance                           | Composition                           |
| -------------- | ------------------------------------- | ------------------------------------- |
| Relationship   | “is-a” (Dog **is-a** Animal)          | “has-a” (Car **has-a** Engine)        |
| Coupling       | Tight coupling                        | Loose coupling                        |
| Flexibility    | Less flexible, static at compile time | More flexible, dynamic at runtime     |
| Code reuse     | Via inheritance chain                 | Via delegation                        |
| Changes impact | Changes in parent affect children     | Changes localized to composed classes |

---

## 4️⃣ Summary

* **Inheritance**: Use when there is a clear hierarchical relationship, and you want to extend or specialize behavior.
* **Composition**: Prefer when you want to build complex objects from simpler ones, or when behavior should be easily changeable.

---

## 53. How do you identify classes and responsibilities from requirements?

Identifying **classes and responsibilities** from requirements is a foundational step in object-oriented design. Here’s a detailed approach to tackle this, perfect for interviews:

---

# How to Identify Classes and Responsibilities from Requirements

---

## Step 1: Understand and Analyze Requirements

* Carefully **read and clarify** the requirements.
* Identify **nouns and verbs** — they often hint at classes and responsibilities.

---

## Step 2: Identify Candidate Classes (Nouns)

* Look for **nouns and noun phrases** in the requirements — they usually represent entities, objects, or concepts.
* Examples: *User*, *Order*, *Product*, *ChatRoom*, *Message*, *Payment*.
* Group related nouns into possible classes.

---

## Step 3: Identify Responsibilities (Verbs & Actions)

* Extract **verbs and verb phrases** describing actions or behaviors related to these nouns.
* These become **methods or responsibilities** of classes.
* Example: *User can register, login, update profile* → class `User` has methods `register()`, `login()`, `updateProfile()`.

---

## Step 4: Define Class Relationships

* Determine relationships such as:

    * **Association** (uses/has-a)
    * **Inheritance** (is-a)
    * **Aggregation/Composition** (whole-part)
* Example: `Order` has multiple `OrderItems` (composition).

---

## Step 5: Refine and Group Responsibilities

* Apply **Single Responsibility Principle** (SRP): each class should have one responsibility.
* If a class seems to have too many responsibilities, consider splitting it.
* Assign behaviors logically to the most relevant class.

---

## Step 6: Use Modeling Tools

* Create **UML diagrams** to visualize classes, attributes, methods, and relationships.
* Helps detect missing or extra classes.

---

## Example: Simple E-commerce Scenario

**Requirement snippet:**
“A user can place an order containing multiple products. Each product has a price and description. The system should calculate the total price for an order.”

* **Nouns → Classes:**

    * User
    * Order
    * Product

* **Responsibilities (verbs):**

    * User: placeOrder()
    * Order: addProduct(), calculateTotal()
    * Product: getPrice(), getDescription()

* **Relationships:**

    * Order *has many* Products (composition)
    * User *places* Orders (association)

---

## Additional Tips

* Ask clarifying questions if requirements are ambiguous.
* Look for real-world analogies.
* Start simple, then iterate and refine as you learn more.
* Remember, responsibilities reflect **what the system needs to do**, classes are **the entities that have these responsibilities**.

---

## 54. What are design patterns? Name some and their use cases.

Here’s a detailed explanation of **design patterns** along with some common examples and their typical use cases — ideal for interview prep:

---

# What Are Design Patterns?

**Design Patterns** are proven, reusable solutions to common software design problems. They provide a template or best practice that developers can apply to structure their code effectively and make it easier to maintain, extend, and understand.

Patterns are not finished code but guidelines or blueprints.

---

# Types of Design Patterns

Design patterns are typically categorized into three groups:

| Category   | Purpose                                         |
| ---------- | ----------------------------------------------- |
| Creational | Deal with object creation mechanisms            |
| Structural | Deal with object composition and relationships  |
| Behavioral | Deal with object interaction and responsibility |

---

# Common Design Patterns with Examples and Use Cases

### 1. Creational Patterns

* **Singleton**
  *Ensure a class has only one instance and provide a global point of access.*
  **Use case:** Database connection pool, logger.

* **Factory Method**
  *Define an interface for creating an object, but let subclasses decide which class to instantiate.*
  **Use case:** GUI toolkit where buttons differ by OS.

* **Builder**
  *Separate object construction from its representation to create complex objects step-by-step.*
  **Use case:** Creating complex objects like HTML documents or configurations.

---

### 2. Structural Patterns

* **Adapter**
  *Allow incompatible interfaces to work together.*
  **Use case:** Integrating third-party APIs with different interfaces.

* **Decorator**
  *Add responsibilities to objects dynamically without altering their structure.*
  **Use case:** Adding scrolling or borders to UI components.

* **Facade**
  *Provide a simplified interface to a complex subsystem.*
  **Use case:** Simplify usage of complex libraries or frameworks.

---

### 3. Behavioral Patterns

* **Observer**
  *Define a one-to-many dependency so that when one object changes, all dependents are notified.*
  **Use case:** Event handling systems, MVC frameworks.

* **Strategy**
  *Define a family of algorithms, encapsulate each one, and make them interchangeable.*
  **Use case:** Sorting algorithms, payment methods.

* **Command**
  *Encapsulate a request as an object, allowing parameterization and queuing.*
  **Use case:** Undo/redo operations, task scheduling.

---

# Summary Table

| Pattern   | Category   | Purpose                                       | Example Use Case               |
| --------- | ---------- | --------------------------------------------- | ------------------------------ |
| Singleton | Creational | Single instance of a class                    | Logger, DB connection          |
| Factory   | Creational | Create objects without specifying exact class | GUI toolkit, document creation |
| Builder   | Creational | Step-wise construction of complex objects     | Building complex objects       |
| Adapter   | Structural | Interface compatibility                       | API integration                |
| Decorator | Structural | Dynamic behavior addition                     | UI enhancements                |
| Facade    | Structural | Simplify subsystem interface                  | Simplified library interface   |
| Observer  | Behavioral | Notify dependents of state changes            | Event systems, notifications   |
| Strategy  | Behavioral | Switchable algorithms                         | Payment methods, sorting       |
| Command   | Behavioral | Encapsulate requests as objects               | Undo/Redo, task queues         |

---

## 55. Explain the Singleton design pattern and its real-world use.

Here's a detailed explanation of the **Singleton design pattern** along with its real-world use:

---

# Singleton Design Pattern

---

## What is Singleton?

The **Singleton** pattern ensures that a class has **only one instance** throughout the application and provides a **global point of access** to that instance.

---

## Why use Singleton?

* To control access to resources that are shared and must have a single point of coordination.
* To avoid creating multiple instances that can cause inconsistent behavior or resource waste.

---

## Key Characteristics

* **Single instance:** Only one object of the class exists.
* **Global access:** The instance is accessible globally.
* **Lazy initialization:** The instance is created when first needed (optional).
* **Thread safety:** In multi-threaded environments, care must be taken to prevent multiple instances.

---

## Typical Implementation in Java

```java
public class Singleton {
    // Static variable to hold the one instance
    private static Singleton instance;

    // Private constructor to prevent instantiation
    private Singleton() { }

    // Public method to provide access to the instance
    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }

    // Other methods of the class
    public void doSomething() {
        System.out.println("Singleton instance is working.");
    }
}
```

---

## Real-World Use Cases

* **Logger:** A logging class that records logs in a consistent manner across the entire application.
* **Configuration Manager:** Centralized management of application configuration parameters.
* **Database Connection Pool:** Ensures only one pool manages all DB connections.
* **Cache:** A shared cache that all parts of an application use.
* **Thread Pool Manager:** To coordinate thread usage in an application.

---

## Example: Logger Singleton

```java
public class Logger {
    private static Logger instance;

    private Logger() { }

    public static synchronized Logger getInstance() {
        if (instance == null) instance = new Logger();
        return instance;
    }

    public void log(String message) {
        System.out.println("Log: " + message);
    }
}
```

Anywhere in the app:

```java
Logger logger = Logger.getInstance();
logger.log("This is a log message.");
```

All log messages funnel through the same Logger instance, ensuring consistent behavior.

---

## Summary

| Pros                                | Cons                                            |
| ----------------------------------- | ----------------------------------------------- |
| Controlled access to sole instance  | Can introduce global state (harder to test)     |
| Reduces memory usage (one instance) | Can cause concurrency issues if not thread-safe |
| Useful for shared resources         | Overuse can lead to tight coupling              |

---

## 56. How would you design a parking lot (OOP level)?

Designing a parking lot at the **OOP level** is a classic system design question that tests your ability to model real-world entities and their relationships with classes and responsibilities.

Here’s a detailed approach with example classes and explanations:

---

# Designing a Parking Lot (OOP Level)

---

## Step 1: Understand the Problem

A parking lot allows vehicles to park in designated spots. It has different types of spots (e.g., compact, large, handicapped) and vehicles (motorcycles, cars, buses). The system should:

* Assign parking spots to vehicles
* Track occupied and free spots
* Possibly handle entry/exit and payment

---

## Step 2: Identify Main Entities (Classes)

* **ParkingLot** — The main class managing the parking lot.
* **ParkingSpot** — Represents a parking spot with a type and availability.
* **Vehicle** — Base class for vehicles.
* **VehicleType** — Enum or class representing vehicle types (Motorcycle, Car, Bus).
* **Ticket** — Represents a parking ticket issued when a vehicle parks.
* **ParkingRate** (optional) — Pricing strategy per vehicle type/time.

---

## Step 3: Define Class Responsibilities

### 1. Vehicle

* Attributes: licensePlate, vehicleType
* Subclasses: Motorcycle, Car, Bus

### 2. ParkingSpot

* Attributes: spotId, spotType (compact, large, handicapped), isAvailable
* Method: assignVehicle(), removeVehicle()

### 3. ParkingLot

* Attributes: list of ParkingSpots, map of occupied spots to vehicles
* Methods:

    * parkVehicle(vehicle) → assign a suitable spot
    * freeSpot(spotId) → mark spot as free
    * findAvailableSpot(vehicleType)

### 4. Ticket

* Attributes: ticketId, vehicle, spot, entryTime, exitTime
* Methods: calculateFee()

---

## Step 4: Define Relationships

* A **ParkingLot** has many **ParkingSpots**
* A **Vehicle** is assigned to a **ParkingSpot**
* A **Ticket** associates a **Vehicle** with a **ParkingSpot**

---

## Sample Code Sketch (Java-like pseudocode)

```java
enum VehicleType { MOTORCYCLE, CAR, BUS }
enum SpotType { COMPACT, LARGE, HANDICAPPED }

abstract class Vehicle {
    String licensePlate;
    VehicleType type;
    public Vehicle(String licensePlate, VehicleType type) {
        this.licensePlate = licensePlate;
        this.type = type;
    }
}

class Motorcycle extends Vehicle {
    public Motorcycle(String licensePlate) {
        super(licensePlate, VehicleType.MOTORCYCLE);
    }
}

class Car extends Vehicle {
    public Car(String licensePlate) {
        super(licensePlate, VehicleType.CAR);
    }
}

class Bus extends Vehicle {
    public Bus(String licensePlate) {
        super(licensePlate, VehicleType.BUS);
    }
}

class ParkingSpot {
    String spotId;
    SpotType spotType;
    boolean isAvailable;
    Vehicle parkedVehicle;

    public ParkingSpot(String spotId, SpotType spotType) {
        this.spotId = spotId;
        this.spotType = spotType;
        this.isAvailable = true;
    }

    public boolean canFitVehicle(Vehicle vehicle) {
        // Simplified logic for example:
        if (!isAvailable) return false;
        switch(vehicle.type) {
            case MOTORCYCLE:
                return true; // Motorcycle fits anywhere
            case CAR:
                return spotType == SpotType.COMPACT || spotType == SpotType.LARGE;
            case BUS:
                return spotType == SpotType.LARGE;
        }
        return false;
    }

    public void assignVehicle(Vehicle vehicle) {
        this.parkedVehicle = vehicle;
        this.isAvailable = false;
    }

    public void removeVehicle() {
        this.parkedVehicle = null;
        this.isAvailable = true;
    }
}

class ParkingLot {
    List<ParkingSpot> spots;

    public ParkingLot(List<ParkingSpot> spots) {
        this.spots = spots;
    }

    public ParkingSpot parkVehicle(Vehicle vehicle) {
        for (ParkingSpot spot : spots) {
            if (spot.canFitVehicle(vehicle)) {
                spot.assignVehicle(vehicle);
                return spot;
            }
        }
        return null; // No spot available
    }

    public void freeSpot(String spotId) {
        for (ParkingSpot spot : spots) {
            if (spot.spotId.equals(spotId)) {
                spot.removeVehicle();
                break;
            }
        }
    }
}
```

---

## Step 5: Possible Extensions

* Handle payment and time-based fees with a `Ticket` class.
* Add multiple parking levels or zones.
* Support reservations or priority parking for handicapped vehicles.
* Use Observer pattern to notify when spots become free.
* Add concurrency handling for multiple entry gates.

---

# Summary

| Component         | Responsibility                            |
| ----------------- | ----------------------------------------- |
| Vehicle           | Holds vehicle details                     |
| ParkingSpot       | Knows if it’s free and if a vehicle fits  |
| ParkingLot        | Assigns spots and manages the overall lot |
| Ticket (optional) | Tracks parking duration and payment       |

---

## 57. How would you design a library management system?

Designing a **Library Management System** is a classic OOP and system design problem. Let me walk you through the key steps and components, focusing on class design and responsibilities.

---

# Designing a Library Management System (OOP Level)

---

## Step 1: Understand the Requirements

A typical library system should support:

* Managing **books** with details (title, author, ISBN, copies)
* Managing **users** who borrow and return books
* Tracking **book availability**
* Borrowing and returning books
* Managing **fines** for late returns (optional)
* Supporting different types of users (students, librarians, etc.)

---

## Step 2: Identify Main Entities (Classes)

* **Library** — Central class that manages books and users
* **Book** — Represents a book with details like title, author, ISBN
* **BookItem** — Represents a physical copy of a Book (each book can have multiple copies)
* **User** — Represents a library user who can borrow books
* **Librarian** (optional subclass of User) — Manages the library operations
* **Loan** — Represents the borrowing record when a user borrows a BookItem
* **Catalog** — Manages searching and indexing of books

---

## Step 3: Define Class Responsibilities

### 1. Book

* Attributes: `title`, `author`, `isbn`
* Methods: (mostly getters/setters)

### 2. BookItem

* Attributes: `barcode`, `status` (AVAILABLE, BORROWED, LOST)
* Methods: `isAvailable()`

### 3. User

* Attributes: `userId`, `name`, `borrowedBooks`
* Methods: `borrowBook(BookItem)`, `returnBook(BookItem)`

### 4. Loan

* Attributes: `loanId`, `user`, `bookItem`, `borrowDate`, `dueDate`, `returnDate`
* Methods: `isOverdue()`, `calculateFine()`

### 5. Library

* Attributes: `catalog`, `users`, `loans`
* Methods:

    * `addBook(Book, numberOfCopies)`
    * `registerUser(User)`
    * `borrowBook(userId, bookId)`
    * `returnBook(userId, bookItemId)`
    * `searchBook(criteria)`

### 6. Catalog

* Methods: `searchByTitle()`, `searchByAuthor()`, `searchByISBN()`

---

## Step 4: Relationships

* Library **has many** BookItems and Users
* User **borrows many** BookItems via Loans
* Book **has many** BookItems (copies)
* Loan **links** User and BookItem

---

## Sample Code Sketch (Java-like pseudocode)

```java
class Book {
    String isbn;
    String title;
    String author;

    // constructor, getters
}

class BookItem {
    String barcode;
    Book book;
    enum Status { AVAILABLE, BORROWED, LOST }
    Status status;

    boolean isAvailable() {
        return status == Status.AVAILABLE;
    }
}

class User {
    String userId;
    String name;
    List<Loan> borrowedBooks;

    boolean borrowBook(BookItem bookItem) {
        if (bookItem.isAvailable()) {
            // create loan
            return true;
        }
        return false;
    }
    void returnBook(BookItem bookItem) { /* ... */ }
}

class Loan {
    String loanId;
    User user;
    BookItem bookItem;
    Date borrowDate;
    Date dueDate;
    Date returnDate;

    boolean isOverdue() { /* compare dates */ }
    double calculateFine() { /* ... */ }
}

class Library {
    Map<String, Book> books; // isbn -> Book
    Map<String, BookItem> bookItems; // barcode -> BookItem
    Map<String, User> users; // userId -> User
    List<Loan> loans;

    void addBook(Book book, int numCopies) {
        books.put(book.isbn, book);
        for (int i = 0; i < numCopies; i++) {
            BookItem item = new BookItem(generateBarcode(), book, Status.AVAILABLE);
            bookItems.put(item.barcode, item);
        }
    }

    boolean borrowBook(String userId, String isbn) {
        User user = users.get(userId);
        for (BookItem item : bookItems.values()) {
            if (item.book.isbn.equals(isbn) && item.isAvailable()) {
                item.status = BookItem.Status.BORROWED;
                // create loan, assign to user
                return true;
            }
        }
        return false; // no available copy
    }

    void returnBook(String barcode) {
        BookItem item = bookItems.get(barcode);
        item.status = BookItem.Status.AVAILABLE;
        // update loan returnDate
    }

    // search methods ...
}
```

---

## Step 5: Extensions & Enhancements

* **Reservation system** to queue requests for popular books.
* **Notification system** for due dates and overdue books.
* **Fine calculation and payment integration**.
* Support **different user roles** (librarian, member).
* **Inventory management** for lost or damaged books.
* **Multi-branch libraries** with distributed catalog.

---

## Summary Table

| Class    | Responsibility                               |
| -------- | -------------------------------------------- |
| Library  | Manage books, users, borrowing and returning |
| Book     | Represent book metadata                      |
| BookItem | Represent physical copies with status        |
| User     | Borrow and return books                      |
| Loan     | Track borrowing records and due dates        |
| Catalog  | Provide search functionality                 |

---

## 58. How would you design a Splitwise-like system?

Designing a **Splitwise-like system** (an expense-sharing app) is a classic system design problem involving user management, expense tracking, and balancing debts. Here’s a detailed breakdown from an OOP and high-level architecture perspective:

---

# Designing a Splitwise-like System

---

## Step 1: Understand the Core Requirements

* Users can create or join groups (friends, roommates, travel groups).
* Users can add expenses specifying who paid and who owes.
* System tracks balances between users — who owes whom and how much.
* Support different currencies (optional).
* Settle debts or mark expenses as paid.
* Show summaries of balances (net owed or owed by each user).

---

## Step 2: Identify Main Entities (Classes)

* **User** — Represents a user of the system.
* **Group** — Represents a collection of users sharing expenses.
* **Expense** — Represents an expense paid by one user and shared among others.
* **ExpenseShare** — Represents how much each participant owes for a given expense.
* **Balance** — Represents net owed amounts between users.
* **Payment** — Represents settlement transactions between users.

---

## Step 3: Define Class Responsibilities

### 1. User

* Attributes: userId, name, email
* Methods: joinGroup(), createExpense()

### 2. Group

* Attributes: groupId, groupName, list of Users
* Methods: addUser(), removeUser(), addExpense()

### 3. Expense

* Attributes: expenseId, amount, paidBy (User), date, list of ExpenseShare
* Methods: calculateShares()

### 4. ExpenseShare

* Attributes: user, amountOwed

### 5. Balance

* Attributes: user1, user2, netAmount (user1 owes user2 if positive)
* Methods: updateBalance()

### 6. Payment

* Attributes: paymentId, fromUser, toUser, amount, date

---

## Step 4: Relationships

* A **Group** has many **Users**.
* A **Group** has many **Expenses**.
* An **Expense** has many **ExpenseShares** (one per participant).
* Balances are tracked between pairs of Users.

---

## Step 5: Basic Workflow

1. **Create group** and add users.
2. **Add expense** to group: specify payer and amount.
3. **Split expense** equally or by shares.
4. **Update balances** between users.
5. **Show balance sheet** summarizing debts.
6. Users can **settle payments** which update balances.

---

## Sample Code Sketch (Simplified)

```java
class User {
    String userId;
    String name;
    String email;
}

class Group {
    String groupId;
    String groupName;
    List<User> users = new ArrayList<>();
    List<Expense> expenses = new ArrayList<>();

    void addUser(User user) {
        users.add(user);
    }

    Expense addExpense(String expenseId, double amount, User paidBy, Map<User, Double> shares) {
        Expense expense = new Expense(expenseId, amount, paidBy);
        expense.calculateShares(shares);
        expenses.add(expense);
        return expense;
    }
}

class Expense {
    String expenseId;
    double amount;
    User paidBy;
    List<ExpenseShare> shares = new ArrayList<>();

    Expense(String expenseId, double amount, User paidBy) {
        this.expenseId = expenseId;
        this.amount = amount;
        this.paidBy = paidBy;
    }

    void calculateShares(Map<User, Double> shareMap) {
        for (Map.Entry<User, Double> entry : shareMap.entrySet()) {
            shares.add(new ExpenseShare(entry.getKey(), entry.getValue()));
        }
    }
}

class ExpenseShare {
    User user;
    double amountOwed;
    ExpenseShare(User user, double amount) {
        this.user = user;
        this.amountOwed = amount;
    }
}

class Balance {
    User user1;
    User user2;
    double netAmount; // Positive means user1 owes user2

    void updateBalance(double amount) {
        netAmount += amount;
    }
}
```

---

## Step 6: Important Details & Extensions

* **Balance Optimization:** Instead of tracking every transaction, maintain net balances between pairs to reduce complexity.
* **Multiple currencies:** Handle exchange rates.
* **Notifications:** Notify users when new expenses are added or payments made.
* **Payments and Settlements:** Support paying off debts partially or fully.
* **Expense types:** Allow unequal splits or percentage-based shares.
* **Security & Privacy:** Ensure users see only their own groups and balances.

---

## High-Level Architecture Components

* **API Layer:** User interface or mobile apps interact via REST APIs.
* **Service Layer:** Handles business logic (expense splitting, balance updating).
* **Database:** Stores users, groups, expenses, balances, payments.
* **Notification Service:** Push/email notifications for updates.
* **Caching:** For quick balance retrieval.

---

## Summary Table

| Component    | Responsibility                           |
| ------------ | ---------------------------------------- |
| User         | Represents a system user                 |
| Group        | Manages users and expenses               |
| Expense      | Represents an expense paid by a user     |
| ExpenseShare | Tracks share owed by each participant    |
| Balance      | Maintains net owed amounts between users |
| Payment      | Represents settlements/payments          |

---

## 59. How would you implement LRU cache?

Implementing an **LRU (Least Recently Used) Cache** is a classic coding problem, often asked in interviews to test your understanding of data structures and algorithm design.

---

# What is an LRU Cache?

An LRU cache stores a fixed number of items. When the cache is full and a new item needs to be added, it evicts the **least recently used** item. “Recently used” means accessed or inserted recently.

---

# Key Requirements

* **get(key):** Return the value if the key exists in the cache, else -1.
* **put(key, value):** Insert or update the value for the key.
* On insert, if the cache exceeds capacity, evict the least recently used item.
* Both operations should run in **O(1)** time complexity.

---

# How to implement LRU Cache?

To achieve O(1) for both get and put, we use:

1. **Hash Map (Dictionary):** To quickly access cache entries by key.
2. **Doubly Linked List:** To keep track of usage order (most recently used at head, least recently used at tail).

---

# Explanation:

* When a key is accessed or updated, move it to the **front (head)** of the linked list.
* When inserting a new key and the cache is full, remove the **tail** (least recently used).
* Hash map stores key → node pointer in linked list for O(1) access.

---

# Pseudocode / Implementation (Python)

```python
class Node:
    def __init__(self, key, value):
        self.key = key
        self.value = value
        self.prev = None
        self.next = None

class LRUCache:
    def __init__(self, capacity: int):
        self.capacity = capacity
        self.cache = {}  # key -> Node
        # Dummy nodes to avoid edge conditions
        self.head = Node(0, 0)  
        self.tail = Node(0, 0)
        self.head.next = self.tail
        self.tail.prev = self.head

    def _remove(self, node):
        # Remove node from linked list
        prev_node = node.prev
        next_node = node.next
        prev_node.next = next_node
        next_node.prev = prev_node

    def _add_to_front(self, node):
        # Add node right after head
        node.next = self.head.next
        node.prev = self.head
        self.head.next.prev = node
        self.head.next = node

    def get(self, key: int) -> int:
        if key not in self.cache:
            return -1
        node = self.cache[key]
        # Move accessed node to front (most recently used)
        self._remove(node)
        self._add_to_front(node)
        return node.value

    def put(self, key: int, value: int) -> None:
        if key in self.cache:
            # Update existing node and move to front
            node = self.cache[key]
            node.value = value
            self._remove(node)
            self._add_to_front(node)
        else:
            if len(self.cache) == self.capacity:
                # Remove LRU from linked list and hashmap
                lru = self.tail.prev
                self._remove(lru)
                del self.cache[lru.key]
            # Add new node to front
            new_node = Node(key, value)
            self.cache[key] = new_node
            self._add_to_front(new_node)
```

---

# How this works:

* `get(key)` looks up in hash map, returns value if exists, else -1.
* Accessing a node moves it to the front of the doubly linked list.
* `put(key, value)` updates existing node or inserts a new one.
* If cache is full, removes the least recently used node at the tail before insertion.

---

# Time and Space Complexity

* Both `get` and `put` operations run in **O(1)** time.
* Space complexity is **O(capacity)** due to storage in hashmap and linked list.

---

## 60. How would you model a restaurant reservation system?

Designing a **restaurant reservation system** is a classic design problem that combines managing users, restaurants, tables, and time slots efficiently. Here's a detailed explanation with key components and a possible approach.

---

# Designing a Restaurant Reservation System

---

## Step 1: Understand the Requirements

* Users can search restaurants by location, cuisine, or name.
* Users can view available tables for a specific date and time.
* Users can book/reserve tables.
* System must prevent double booking of the same table/time slot.
* Users can cancel or modify reservations.
* Restaurants can manage their tables and availability.
* Optional: Support waitlists, notifications, and special requests.

---

## Step 2: Identify Key Entities and Their Attributes

| Entity          | Description                            | Key Attributes                                   |
| --------------- | -------------------------------------- | ------------------------------------------------ |
| **User**        | Person making a reservation            | userId, name, contactInfo                        |
| **Restaurant**  | Restaurant where reservations are made | restaurantId, name, address, cuisine, rating     |
| **Table**       | Physical table in a restaurant         | tableId, restaurantId, seats (capacity)          |
| **Reservation** | Booking made by a user for a table     | reservationId, userId, tableId, datetime, status |
| **TimeSlot**    | Discrete time intervals to book tables | startTime, endTime                               |

---

## Step 3: Define Relationships

* A **Restaurant** has multiple **Tables**.
* A **User** can have multiple **Reservations**.
* A **Table** can have many **Reservations** over time, but only one per time slot.
* **Reservation** ties a User, Table, and TimeSlot together.

---

## Step 4: Class Design (Simplified)

```java
class User {
    String userId;
    String name;
    String contactInfo;
    List<Reservation> reservations;
}

class Restaurant {
    String restaurantId;
    String name;
    String address;
    String cuisine;
    List<Table> tables;
}

class Table {
    String tableId;
    String restaurantId;
    int capacity;  // number of seats
}

enum ReservationStatus {
    CONFIRMED,
    CANCELLED,
    COMPLETED
}

class Reservation {
    String reservationId;
    User user;
    Table table;
    LocalDateTime startTime;
    LocalDateTime endTime;
    ReservationStatus status;
}
```

---

## Step 5: Workflow & Key Operations

### 1. Search for Restaurants

* Filter by location, cuisine, rating.

### 2. Check Table Availability

* Given a restaurant and desired date/time, find tables not booked for that slot.
* Check existing reservations for the restaurant’s tables in the requested time window.

### 3. Make a Reservation

* Select an available table.
* Create a `Reservation` record.
* Mark the table as booked for the time slot.

### 4. Modify / Cancel Reservation

* Update or delete reservation.
* Release the table’s slot accordingly.

---

## Step 6: Handling Concurrency & Double Booking

* Use transactions or locking when booking tables to prevent race conditions.
* Alternatively, optimistic locking or atomic DB operations to ensure no double bookings.
* Maintain an index or calendar per table for quick availability lookups.

---

## Step 7: Optional Features & Enhancements

* **Waitlist:** Allow users to queue if no tables are available.
* **Notifications:** Email/SMS reminders for upcoming reservations.
* **Special Requests:** Capture dietary preferences or accessibility needs.
* **Dynamic Pricing:** Charge differently during peak hours.
* **Cancellation Policies:** Handle penalties or fees for no-shows.

---

## Step 8: High-Level Architecture Components

* **API Layer:** To handle user requests (search, book, cancel).
* **Reservation Service:** Manages bookings and availability checks.
* **Database:** Stores users, restaurants, tables, reservations.
* **Notification Service:** Sends booking confirmations and reminders.
* **Caching Layer:** For frequently accessed data (restaurant info, availability).

---

## Summary Table

| Component           | Responsibility                            |
| ------------------- | ----------------------------------------- |
| User                | Book and manage reservations              |
| Restaurant          | Provide details and manage tables         |
| Table               | Represents seating availability           |
| Reservation         | Booking details tying user and table/time |
| Reservation Service | Handles booking logic and availability    |

---

## 61. Explain the Observer pattern with a real example.

Let me explain the **Observer pattern** with a real-world example.

---

# What is the Observer Pattern?

The **Observer pattern** is a behavioral design pattern where an object, called the **subject**, maintains a list of dependents, called **observers**, and notifies them automatically of any state changes, usually by calling one of their methods.

It's mainly used to implement **publish-subscribe** mechanisms and allows a clean separation between the subject and the observers.

---

# Key Concepts

* **Subject:** The object that holds the data and sends notifications.
* **Observer:** The object that wants to be informed when the subject changes.
* **Notification:** The action where the subject updates the observers about changes.

---

# Real-world Example: News Publisher and Subscribers

Imagine a news app:

* **NewsPublisher (Subject):** Publishes news articles.
* **Subscribers (Observers):** Users who subscribe to receive notifications when new articles are published.

---

# How it works:

* Subscribers register themselves with the NewsPublisher.
* When NewsPublisher releases a new article, it notifies all subscribers.
* Subscribers then get the update and can act on it (e.g., show notification, update UI).

---

# Example Code in Java

```java
import java.util.*;

// Observer interface
interface Subscriber {
    void update(String news);
}

// Concrete Observer
class User implements Subscriber {
    private String name;

    public User(String name) {
        this.name = name;
    }

    @Override
    public void update(String news) {
        System.out.println(name + " received news: " + news);
    }
}

// Subject interface
interface NewsPublisher {
    void subscribe(Subscriber subscriber);
    void unsubscribe(Subscriber subscriber);
    void notifySubscribers();
}

// Concrete Subject
class NewsAgency implements NewsPublisher {
    private List<Subscriber> subscribers = new ArrayList<>();
    private String latestNews;

    public void publishNews(String news) {
        this.latestNews = news;
        notifySubscribers();
    }

    @Override
    public void subscribe(Subscriber subscriber) {
        subscribers.add(subscriber);
    }

    @Override
    public void unsubscribe(Subscriber subscriber) {
        subscribers.remove(subscriber);
    }

    @Override
    public void notifySubscribers() {
        for (Subscriber subscriber : subscribers) {
            subscriber.update(latestNews);
        }
    }
}

// Demo
public class ObserverPatternDemo {
    public static void main(String[] args) {
        NewsAgency agency = new NewsAgency();

        User user1 = new User("Alice");
        User user2 = new User("Bob");

        agency.subscribe(user1);
        agency.subscribe(user2);

        agency.publishNews("Breaking News: New Java Version Released!");
        // Output:
        // Alice received news: Breaking News: New Java Version Released!
        // Bob received news: Breaking News: New Java Version Released!

        agency.unsubscribe(user1);

        agency.publishNews("Sports Update: Local Team Wins!");
        // Output:
        // Bob received news: Sports Update: Local Team Wins!
    }
}
```

---

# Summary

| Role         | Description                                             |
| ------------ | ------------------------------------------------------- |
| Subject      | NewsAgency publishes news and manages subscribers       |
| Observer     | Users subscribe/unsubscribe and get notified on updates |
| Notification | When news is published, all subscribers are notified    |

---

The Observer pattern helps **loosely couple** the subject and observers so you can add or remove observers dynamically without changing the subject.

---

## 62. What is a Factory pattern and when would you use it?

Here’s a detailed explanation of the **Factory Pattern**, with examples and use cases.

---

# What is the Factory Pattern?

The **Factory Pattern** is a **creational design pattern** that provides an interface for creating objects in a superclass, but allows subclasses to alter the type of objects that will be created. Instead of calling a constructor directly, you call a factory method.

---

# Why use Factory Pattern?

* **Encapsulates object creation**: Hides the complex logic of object creation from the client.
* **Promotes loose coupling**: Clients depend on interfaces or abstract classes, not concrete implementations.
* **Makes code easier to maintain and extend**: New types can be added without modifying client code.
* Supports **Open/Closed Principle** — open for extension, closed for modification.

---

# Types of Factory Patterns

* **Simple Factory (not a GoF pattern)**: A class with a method that returns different types of objects based on input.
* **Factory Method**: Defines an interface for creating an object, but lets subclasses decide which class to instantiate.
* **Abstract Factory**: Provides an interface to create families of related or dependent objects without specifying their concrete classes.

---

# Simple Factory Example

Imagine a notification system that can send different types of notifications (Email, SMS, Push):

```java
// Product interface
interface Notification {
    void notifyUser();
}

// Concrete Products
class EmailNotification implements Notification {
    public void notifyUser() {
        System.out.println("Sending Email Notification");
    }
}

class SMSNotification implements Notification {
    public void notifyUser() {
        System.out.println("Sending SMS Notification");
    }
}

// Factory class
class NotificationFactory {
    public static Notification createNotification(String type) {
        if (type == null || type.isEmpty())
            return null;
        switch (type) {
            case "EMAIL":
                return new EmailNotification();
            case "SMS":
                return new SMSNotification();
            default:
                throw new IllegalArgumentException("Unknown notification type");
        }
    }
}

// Client code
public class FactoryPatternDemo {
    public static void main(String[] args) {
        Notification notification = NotificationFactory.createNotification("EMAIL");
        notification.notifyUser();  // Output: Sending Email Notification
    }
}
```

---

# When to use the Factory Pattern?

* When you don't want the client code to depend on concrete classes directly.
* When the creation process is complex or requires some logic.
* When you want to manage or centralize object creation.
* When your system needs to be easily extensible for new types without changing existing code.
* When you want to control or limit the set of objects created.

---

# Summary

| Aspect            | Explanation                                                                   |
| ----------------- | ----------------------------------------------------------------------------- |
| Purpose           | Encapsulate object creation logic                                             |
| Benefits          | Loose coupling, easier maintenance                                            |
| Common use cases  | Creating related objects, managing families of products, polymorphic creation |
| Common variations | Simple Factory, Factory Method, Abstract Factory                              |

---

## 63. How would you implement a message queue in LLD?

Implementing a **Message Queue** at a **Low-Level Design (LLD)** means focusing on the core classes, data structures, and interactions that make it work, without diving into infrastructure details like distributed systems or persistence.

---

# What is a Message Queue?

A **Message Queue** allows asynchronous communication between components by storing messages in a queue until consumers are ready to process them.

---

# Key Features to Model:

* **Producers**: Components that send/publish messages.
* **Consumers**: Components that receive/process messages.
* **Queue**: Stores messages in order (FIFO).
* **Message**: The data payload.
* **Acknowledgement**: Consumer acknowledges message processing.
* **Visibility Timeout**: Temporarily hide a message until acknowledged.
* **Persistence (optional)**: Store messages durably (out of scope for simple LLD).

---

# Core Classes & Components

### 1. Message

```java
class Message {
    String id;         // Unique identifier
    String payload;    // Actual message content
    long timestamp;    // Time of creation
}
```

### 2. Queue

* Stores messages in FIFO order.
* Supports enqueue (publish) and dequeue (consume) operations.

```java
class MessageQueue {
    Queue<Message> queue = new LinkedList<>();

    public synchronized void enqueue(Message msg) {
        queue.offer(msg);
        notifyAll();  // Notify waiting consumers
    }

    public synchronized Message dequeue() throws InterruptedException {
        while (queue.isEmpty()) {
            wait(); // wait if no messages
        }
        return queue.poll();
    }
}
```

### 3. Producer

* Sends messages to the queue.

```java
class Producer {
    MessageQueue queue;

    public Producer(MessageQueue queue) {
        this.queue = queue;
    }

    public void send(String payload) {
        Message msg = new Message(UUID.randomUUID().toString(), payload, System.currentTimeMillis());
        queue.enqueue(msg);
    }
}
```

### 4. Consumer

* Receives messages from the queue and processes them.

```java
class Consumer implements Runnable {
    MessageQueue queue;

    public Consumer(MessageQueue queue) {
        this.queue = queue;
    }

    public void run() {
        try {
            while (true) {
                Message msg = queue.dequeue();
                process(msg);
            }
        } catch (InterruptedException e) {
            Thread.currentThread().interrupt();
        }
    }

    private void process(Message msg) {
        System.out.println("Processing message: " + msg.payload);
        // Acknowledge or handle failure (simplified here)
    }
}
```

---

# Optional Enhancements

* **Acknowledgement:** Track message processing success/failure.
* **Visibility Timeout:** Temporarily hide messages after dequeue to avoid duplicate processing.
* **Dead Letter Queue:** Handle messages that repeatedly fail.
* **Multiple Queues/Topics:** Support multiple queues or pub/sub.
* **Persistence:** Save messages to disk or database for durability.

---

# Diagram (Conceptual)

```
Producer --> [MessageQueue] --> Consumer
```

---

# Summary

| Component    | Responsibility                              |
| ------------ | ------------------------------------------- |
| Message      | Encapsulates data to be sent                |
| MessageQueue | Stores messages and handles enqueue/dequeue |
| Producer     | Sends messages into the queue               |
| Consumer     | Retrieves and processes messages            |

---

This simple LLD models a basic in-memory message queue suitable for learning or small apps. Real-world systems like Kafka or RabbitMQ add many features on top, such as partitioning, replication, persistence, and distributed coordination.

---

## 64. What is the Repository pattern?

Here’s a detailed explanation of the **Repository pattern**:

---

# What is the Repository Pattern?

The **Repository pattern** is a **design pattern** used to abstract the data access layer, providing a **clean separation** between the business logic and the code that interacts with the database or other storage mechanisms.

It acts like an **in-memory collection** of domain objects, allowing clients to add, remove, and query objects without dealing directly with database operations.

---

# Why use the Repository Pattern?

* **Decouples business logic from data access code** — your service layer doesn’t care *how* data is stored.
* **Centralizes data logic** in one place — easier to maintain, update, or swap database technologies.
* **Improves testability** — you can mock repository interfaces for unit tests.
* Encourages adherence to **Single Responsibility Principle** by separating concerns.

---

# Key Concepts

* **Repository Interface:** Defines the contract for data operations (CRUD).
* **Repository Implementation:** Contains concrete data access logic (e.g., SQL queries, ORM calls).
* **Domain Objects:** The entities or models being persisted.

---

# Example (Java-like pseudocode)

Suppose you have a `User` entity and want to access users from a database.

```java
// Domain model
class User {
    String id;
    String name;
    String email;
}

// Repository interface
interface UserRepository {
    User findById(String id);
    List<User> findAll();
    void save(User user);
    void delete(String id);
}

// Concrete implementation (using, e.g., JDBC or ORM)
class UserRepositoryImpl implements UserRepository {
    // Assume we have a database connection here

    @Override
    public User findById(String id) {
        // code to query DB and return user
    }

    @Override
    public List<User> findAll() {
        // code to query DB and return list of users
    }

    @Override
    public void save(User user) {
        // code to insert/update user in DB
    }

    @Override
    public void delete(String id) {
        // code to delete user from DB
    }
}
```

---

# How to Use

```java
UserRepository userRepository = new UserRepositoryImpl();
User user = userRepository.findById("123");
user.setName("New Name");
userRepository.save(user);
```

Your business/service layer uses `UserRepository` without knowing *how* data is stored.

---

# Summary

| Aspect               | Explanation                                   |
| -------------------- | --------------------------------------------- |
| Purpose              | Abstract data access and separate concerns    |
| Benefits             | Cleaner code, easier testing, maintainability |
| Use Cases            | Any system interacting with databases or APIs |
| Common in frameworks | Spring Data JPA, Hibernate Repositories       |

---

## 65. How would you implement undo-redo in a text editor?

Implementing **undo-redo** in a text editor is a classic problem that beautifully demonstrates command history management and state control.

---

# Key Idea

* Maintain **two stacks**: one for **undo** operations, one for **redo** operations.
* Every user action (like typing, deleting) is represented as a **command** that can be executed, undone, and redone.
* When an action is done, push it onto the undo stack.
* When undo is called, pop from undo stack, reverse the action, and push it onto redo stack.
* When redo is called, pop from redo stack, execute the action again, and push it back onto undo stack.

---

# Design Approach: Command Pattern

Each user action is encapsulated as a **Command** object with:

* `execute()`
* `undo()`

---

# Components

1. **Command Interface**
2. **Concrete Commands** (e.g., InsertTextCommand, DeleteTextCommand)
3. **Editor** (text content and cursor position)
4. **Undo and Redo stacks**

---

# Simplified Java-like Example

```java
// Command interface
interface Command {
    void execute();
    void undo();
}

// Receiver: Text Editor
class TextEditor {
    StringBuilder text = new StringBuilder();
    int cursor = 0;

    public void insert(String str) {
        text.insert(cursor, str);
        cursor += str.length();
    }

    public void delete(int length) {
        text.delete(cursor - length, cursor);
        cursor -= length;
    }

    public String getText() {
        return text.toString();
    }

    public void setCursor(int position) {
        cursor = position;
    }

    public int getCursor() {
        return cursor;
    }
}

// Concrete Command: Insert Text
class InsertTextCommand implements Command {
    private TextEditor editor;
    private String textToInsert;
    private int position;

    public InsertTextCommand(TextEditor editor, String text) {
        this.editor = editor;
        this.textToInsert = text;
    }

    @Override
    public void execute() {
        position = editor.getCursor();
        editor.insert(textToInsert);
    }

    @Override
    public void undo() {
        editor.setCursor(position + textToInsert.length());
        editor.delete(textToInsert.length());
        editor.setCursor(position);
    }
}

// Undo-Redo Manager
class UndoRedoManager {
    private Stack<Command> undoStack = new Stack<>();
    private Stack<Command> redoStack = new Stack<>();

    public void executeCommand(Command cmd) {
        cmd.execute();
        undoStack.push(cmd);
        redoStack.clear(); // clear redo after new action
    }

    public void undo() {
        if (!undoStack.isEmpty()) {
            Command cmd = undoStack.pop();
            cmd.undo();
            redoStack.push(cmd);
        }
    }

    public void redo() {
        if (!redoStack.isEmpty()) {
            Command cmd = redoStack.pop();
            cmd.execute();
            undoStack.push(cmd);
        }
    }
}
```

---

# How it works

```java
TextEditor editor = new TextEditor();
UndoRedoManager manager = new UndoRedoManager();

Command insertHello = new InsertTextCommand(editor, "Hello");
manager.executeCommand(insertHello);
System.out.println(editor.getText());  // Output: Hello

manager.undo();
System.out.println(editor.getText());  // Output: (empty string)

manager.redo();
System.out.println(editor.getText());  // Output: Hello
```

---

# Additional considerations

* **Multiple types of commands:** Insert, Delete, Replace, Format.
* **Batching commands:** Group multiple edits as one undoable action.
* **Cursor management:** Careful tracking of cursor positions.
* **Memory limits:** Limit undo history size.
* **Persistence:** Save history across sessions.

---

# Summary

| Aspect          | Explanation                                    |
| --------------- | ---------------------------------------------- |
| Undo Stack      | Stores executed commands for undoing           |
| Redo Stack      | Stores undone commands for redoing             |
| Command Pattern | Encapsulates actions with execute & undo       |
| Editor State    | Modified by commands, cursor handled carefully |

---

## 66. How would you design a Notification Service (OOP level)?

Designing a **Notification Service** at the **Object-Oriented Programming (OOP) level** involves identifying core classes, their responsibilities, and interactions to send notifications through multiple channels (like Email, SMS, Push).

---

# Requirements (Basic)

* Support sending notifications via multiple channels (Email, SMS, Push).
* Notifications have content and recipient info.
* Allow adding new notification types easily.
* Decouple notification sending logic from notification types.
* Possibly support different priorities or scheduling (optional).

---

# Key Design Principles

* Use **Interface/Abstract class** for notification channels (Open/Closed Principle).
* Use **Factory or Strategy Pattern** to choose notification type dynamically.
* Single Responsibility Principle: separate message creation from sending logic.

---

# Core Classes and Interfaces

### 1. Notification (Interface or Abstract Class)

```java
public interface Notification {
    void send();
}
```

### 2. Concrete Notifications

```java
class EmailNotification implements Notification {
    private String recipientEmail;
    private String message;

    public EmailNotification(String recipientEmail, String message) {
        this.recipientEmail = recipientEmail;
        this.message = message;
    }

    @Override
    public void send() {
        // Logic to send email
        System.out.println("Sending Email to " + recipientEmail + ": " + message);
    }
}

class SMSNotification implements Notification {
    private String phoneNumber;
    private String message;

    public SMSNotification(String phoneNumber, String message) {
        this.phoneNumber = phoneNumber;
        this.message = message;
    }

    @Override
    public void send() {
        // Logic to send SMS
        System.out.println("Sending SMS to " + phoneNumber + ": " + message);
    }
}

class PushNotification implements Notification {
    private String deviceId;
    private String message;

    public PushNotification(String deviceId, String message) {
        this.deviceId = deviceId;
        this.message = message;
    }

    @Override
    public void send() {
        // Logic to send Push notification
        System.out.println("Sending Push Notification to device " + deviceId + ": " + message);
    }
}
```

### 3. Notification Factory (Optional, for creating notification objects dynamically)

```java
public class NotificationFactory {
    public static Notification createNotification(String type, String recipient, String message) {
        switch (type.toUpperCase()) {
            case "EMAIL":
                return new EmailNotification(recipient, message);
            case "SMS":
                return new SMSNotification(recipient, message);
            case "PUSH":
                return new PushNotification(recipient, message);
            default:
                throw new IllegalArgumentException("Invalid notification type");
        }
    }
}
```

### 4. NotificationService

```java
public class NotificationService {
    public void sendNotification(Notification notification) {
        notification.send();
    }
}
```

---

# Example Usage

```java
public class Demo {
    public static void main(String[] args) {
        NotificationService service = new NotificationService();

        Notification email = new EmailNotification("user@example.com", "Welcome!");
        Notification sms = new SMSNotification("+1234567890", "Your OTP is 1234");
        Notification push = new PushNotification("device123", "You have a new message");

        service.sendNotification(email);
        service.sendNotification(sms);
        service.sendNotification(push);

        // Using factory
        Notification notif = NotificationFactory.createNotification("EMAIL", "user2@example.com", "Hello again!");
        service.sendNotification(notif);
    }
}
```

---

# Extensibility & Best Practices

* To add a new notification type (e.g., Slack, WhatsApp), create a new class implementing `Notification`.
* Use **Dependency Injection** to inject notification senders or factories for better testability.
* Add **queueing** or **retry** mechanisms in `NotificationService` for reliability.
* Add **logging** and **error handling**.
* Support **batch notifications** or **templates** as an enhancement.

---

# Summary

| Class/Interface     | Responsibility                            |
| ------------------- | ----------------------------------------- |
| Notification        | Interface defining send contract          |
| EmailNotification   | Concrete class to send emails             |
| SMSNotification     | Concrete class to send SMS                |
| PushNotification    | Concrete class to send push notifications |
| NotificationFactory | Create notification objects dynamically   |
| NotificationService | Orchestrates sending notifications        |

---

## 67. How do you apply the Strategy pattern in system design?

The **Strategy pattern** is a powerful behavioral design pattern used frequently in system design to make a system flexible and extensible.

---

## What is the Strategy Pattern?

* The **Strategy pattern** defines a family of algorithms, encapsulates each one as a separate class, and makes them interchangeable.
* It lets the algorithm vary independently from clients that use it.
* Essentially, it enables **selecting an algorithm at runtime**.

---

## Why use Strategy Pattern?

* To avoid **conditional logic** (like `if-else` or `switch-case`) scattered around your code.
* To **encapsulate** varying behavior.
* To **adhere to Open/Closed Principle** — add new strategies without modifying existing code.
* To **promote code reusability and testability** by isolating algorithms.

---

## How to apply Strategy pattern in system design?

### Steps:

1. **Identify the behavior/algorithm that varies** and needs to be interchangeable.
2. Define a **Strategy interface** representing the common behavior.
3. Implement **concrete strategy classes** implementing the Strategy interface.
4. Create a **Context** class that uses a Strategy object.
5. The client sets or changes the Strategy object dynamically.

---

## Example: Payment Processing System

Imagine you are designing a payment system supporting multiple payment methods (Credit Card, PayPal, Crypto).

### Strategy Interface:

```java
public interface PaymentStrategy {
    void pay(double amount);
}
```

### Concrete Strategies:

```java
public class CreditCardPayment implements PaymentStrategy {
    @Override
    public void pay(double amount) {
        System.out.println("Paying $" + amount + " using Credit Card.");
        // Credit card payment logic
    }
}

public class PayPalPayment implements PaymentStrategy {
    @Override
    public void pay(double amount) {
        System.out.println("Paying $" + amount + " using PayPal.");
        // PayPal payment logic
    }
}

public class CryptoPayment implements PaymentStrategy {
    @Override
    public void pay(double amount) {
        System.out.println("Paying $" + amount + " using Cryptocurrency.");
        // Crypto payment logic
    }
}
```

### Context Class:

```java
public class PaymentContext {
    private PaymentStrategy strategy;

    public void setPaymentStrategy(PaymentStrategy strategy) {
        this.strategy = strategy;
    }

    public void pay(double amount) {
        strategy.pay(amount);
    }
}
```

### Usage:

```java
PaymentContext paymentContext = new PaymentContext();

paymentContext.setPaymentStrategy(new CreditCardPayment());
paymentContext.pay(100.0);  // Paying $100.0 using Credit Card.

paymentContext.setPaymentStrategy(new PayPalPayment());
paymentContext.pay(200.0);  // Paying $200.0 using PayPal.

paymentContext.setPaymentStrategy(new CryptoPayment());
paymentContext.pay(300.0);  // Paying $300.0 using Cryptocurrency.
```

---

## Other Use Cases in System Design

* **Sorting algorithms**: Different sorting strategies for data.
* **Compression algorithms**: Choose between gzip, zip, etc.
* **Authentication mechanisms**: OAuth, JWT, API key, etc.
* **Logging strategies**: Console, file, or remote logging.
* **Routing strategies**: Different load balancing algorithms.

---

## Benefits

| Advantage                        | Explanation                                  |
| -------------------------------- | -------------------------------------------- |
| Flexible algorithm selection     | Switch strategies at runtime                 |
| Cleaner code                     | Avoids bulky conditional statements          |
| Adheres to Open/Closed Principle | Add new algorithms without modifying clients |
| Enhances testability             | Test strategies in isolation                 |

---

## 68. What is the difference between Abstract class and Interface?

Understanding the difference between **Abstract Classes** and **Interfaces** is fundamental in OOP and system design.

Here’s a detailed comparison:

---

### 1. **Purpose**

* **Abstract Class:**

    * Used to provide a **base class** with some shared implementation.
    * Can have **both abstract methods** (without implementation) and **concrete methods** (with implementation).
    * Represents an **"is-a" relationship**.

* **Interface:**

    * Used to define a **contract or capability** that a class can implement.
    * Only declares **method signatures** (until Java 8, now can have default/static methods).
    * Represents a **"can-do" relationship**.

---

### 2. **Method Implementation**

| Feature                       | Abstract Class | Interface                                                             |
| ----------------------------- | -------------- | --------------------------------------------------------------------- |
| Can have implemented methods? | Yes            | Before Java 8: No <br> Since Java 8: Yes (default and static methods) |
| Can have abstract methods?    | Yes            | Yes (method signatures only)                                          |

---

### 3. **Multiple Inheritance**

* **Abstract Class:**

    * A class can **extend only one abstract class** (single inheritance).
* **Interface:**

    * A class can **implement multiple interfaces** (multiple inheritance of type).

---

### 4. **Fields and Variables**

| Feature                      | Abstract Class                                        | Interface                                                            |
| ---------------------------- | ----------------------------------------------------- | -------------------------------------------------------------------- |
| Can have instance variables? | Yes (can have fields with different access modifiers) | No instance variables; can have `public static final` constants only |
| Can have constructors?       | Yes (can have constructors to initialize state)       | No constructors                                                      |

---

### 5. **Access Modifiers**

* **Abstract Class:** Methods and fields can have any access modifier (`private`, `protected`, `public`).
* **Interface:** Methods are implicitly **public** (cannot have private or protected methods until Java 9 introduced private methods in interfaces).

---

### 6. **When to Use**

| Use Case                                                      | Recommendation              |
| ------------------------------------------------------------- | --------------------------- |
| Shared code among related classes                             | Use Abstract Class          |
| Define a contract for unrelated classes                       | Use Interface               |
| Need multiple inheritance of type                             | Use Interface               |
| Need to add methods without breaking existing implementations | Interface (default methods) |

---

### Example in Java

```java
// Abstract class
abstract class Animal {
    void breathe() {
        System.out.println("Breathing");
    }

    abstract void makeSound();
}

// Interface
interface Flyable {
    void fly();
}

class Bird extends Animal implements Flyable {
    @Override
    void makeSound() {
        System.out.println("Chirp chirp");
    }

    @Override
    public void fly() {
        System.out.println("Flying");
    }
}
```

---

### Summary Table

| Feature               | Abstract Class              | Interface                                           |
| --------------------- | --------------------------- | --------------------------------------------------- |
| Inheritance           | Single                      | Multiple                                            |
| Method Implementation | Yes (abstract + concrete)   | Usually only abstract, default allowed since Java 8 |
| Fields                | Yes (instance and static)   | Only static final constants                         |
| Constructors          | Yes                         | No                                                  |
| Access Modifiers      | Any                         | Methods are public by default                       |
| Usage                 | Base class with shared code | Contract/capability declaration                     |

---

## 69. What is a state machine and where would you use it?

Understanding **state machines** is really useful for modeling complex systems that behave differently based on their internal state.

---

## What is a State Machine?

A **State Machine** (or Finite State Machine, FSM) is a computational model used to design algorithms and systems that can be in one of a finite number of **states** at any time. The system transitions between these states in response to **events** or **inputs**.

---

### Key Concepts:

* **State:** A condition or situation during the life of an object (e.g., “Idle”, “Running”, “Paused”).
* **Event/Input:** Something that triggers a change (e.g., user action, timer).
* **Transition:** Movement from one state to another caused by an event.
* **Action:** Optional work done during a transition or within a state.

---

## Why use a State Machine?

* To **model complex behavior** clearly and explicitly.
* To ensure **valid state transitions** only (e.g., prevent invalid operations).
* To **reduce bugs** caused by unexpected states.
* To **improve maintainability** and readability of code.
* Useful when system behavior depends heavily on current state and events.

---

## Where would you use a State Machine?

* **UI workflows:** e.g., multi-step forms, wizard navigation.
* **Protocol design:** TCP connection states (CLOSED, LISTEN, SYN\_SENT, ESTABLISHED).
* **Games:** Player states like walking, jumping, attacking.
* **Order processing:** Order states like New, Paid, Shipped, Delivered.
* **Embedded systems:** Traffic light control, elevator control.
* **Parsing:** Lexical analyzers use state machines.
* **Workflow engines:** Business process flows.

---

## Simple Example: Traffic Light Controller

| State  | Event         | Next State |
| ------ | ------------- | ---------- |
| Green  | Timer expires | Yellow     |
| Yellow | Timer expires | Red        |
| Red    | Timer expires | Green      |

---

## Code Sketch (Java-like):

```java
enum State {
    GREEN, YELLOW, RED
}

class TrafficLight {
    private State currentState = State.RED;

    public void onTimer() {
        switch(currentState) {
            case RED:
                currentState = State.GREEN;
                break;
            case GREEN:
                currentState = State.YELLOW;
                break;
            case YELLOW:
                currentState = State.RED;
                break;
        }
        System.out.println("Current state: " + currentState);
    }
}
```

---

## Summary

| Aspect     | Description                                             |
| ---------- | ------------------------------------------------------- |
| Definition | Model describing system states & transitions            |
| Use cases  | UI flows, protocols, games, embedded systems            |
| Benefits   | Clear behavior modeling, fewer bugs, easier maintenance |

---

## 70. How would you write extensible and maintainable classes?

Writing **extensible** and **maintainable** classes is essential for building software that can grow and adapt over time without becoming a tangled mess. Here's a detailed explanation with principles and practices:

---

## What does it mean?

* **Extensible**: You can add new features or behaviors with minimal changes to existing code.
* **Maintainable**: The code is easy to understand, debug, and modify by you or others later.

---

## Key Principles & Best Practices

### 1. **Single Responsibility Principle (SRP)**

Each class should have **one and only one reason to change** — it should do one thing well.

* Avoid classes that try to do too many unrelated tasks.
* Example: Separate `UserAuthentication` from `UserProfileManagement`.

### 2. **Open/Closed Principle (OCP)**

Classes should be **open for extension but closed for modification**.

* Design your classes so that you can add new behaviors by **adding new code**, not changing existing code.
* Use **interfaces**, **abstract classes**, and **polymorphism**.

### 3. **Use Interfaces and Abstract Classes**

* Define clear contracts using interfaces or abstract classes.
* Let multiple implementations vary independently.

### 4. **Favor Composition over Inheritance**

* Prefer assembling behavior using smaller reusable components rather than deep inheritance trees.
* Composition leads to more flexible and testable designs.

### 5. **Encapsulation**

* Keep data (fields) **private**.
* Expose only necessary behaviors via **methods**.
* Protect internal state from inconsistent changes.

### 6. **Clear Naming and Documentation**

* Use **meaningful class, method, and variable names**.
* Document intent, especially for complex logic.

### 7. **Keep Classes Cohesive**

* Group related data and behaviors together.
* Avoid unrelated methods in the same class.

### 8. **Dependency Injection**

* Pass dependencies into classes rather than hardcoding them.
* Makes testing and changing implementations easier.

### 9. **Avoid Premature Optimization**

* Focus on clean design first.
* Optimize later when necessary.

---

## Example: Designing a Notification System (simplified)

```java
// Interface: Open for new notification types
public interface NotificationSender {
    void send(String message, String recipient);
}

// Concrete Implementation: Email
public class EmailSender implements NotificationSender {
    @Override
    public void send(String message, String recipient) {
        // email sending logic
        System.out.println("Email sent to " + recipient + ": " + message);
    }
}

// Concrete Implementation: SMS
public class SmsSender implements NotificationSender {
    @Override
    public void send(String message, String recipient) {
        // SMS sending logic
        System.out.println("SMS sent to " + recipient + ": " + message);
    }
}

// Client class depends on abstraction, not implementation
public class NotificationService {
    private NotificationSender sender;

    public NotificationService(NotificationSender sender) {
        this.sender = sender; // Dependency Injection
    }

    public void notify(String message, String recipient) {
        sender.send(message, recipient);
    }
}
```

**How is this extensible and maintainable?**

* To add PushNotification, just create another class implementing `NotificationSender`.
* No need to modify `NotificationService`.
* Classes have a single responsibility.
* `NotificationService` depends on the abstraction, enabling easier testing/mocking.

---

## Summary

| Practice                        | Why?                                           |
| ------------------------------- | ---------------------------------------------- |
| Single Responsibility           | Easier to understand and change                |
| Open/Closed Principle           | Add features without breaking existing code    |
| Use Interfaces/Abstract Classes | Flexible implementations                       |
| Favor Composition               | Flexible and reusable components               |
| Encapsulation                   | Protect internal state                         |
| Dependency Injection            | Decouples code for testability and flexibility |
| Clear Naming/Documentation      | Improves readability                           |

---

## 71. How would you design a Payment Gateway LLD?

Designing a **Payment Gateway (Low-Level Design)** involves modeling the core classes, their relationships, and key interactions for processing payments securely and reliably.

Here’s a detailed LLD approach with example classes and explanation:

---

## Requirements Recap (Simplified)

* Process different payment methods (Credit Card, Debit Card, Net Banking, Wallet)
* Handle payment authorization, capture, refund
* Support multiple payment providers/gateways
* Track payment status (Pending, Success, Failed)
* Log transactions for audit
* Handle errors and retries

---

## Core Entities / Classes

### 1. **Payment**

Represents a payment request.

```java
public class Payment {
    private String paymentId;
    private double amount;
    private PaymentMethod paymentMethod;
    private PaymentStatus status;
    private String currency;
    private String userId;
    private Date createdAt;
    // getters and setters
}
```

* `paymentId`: Unique payment identifier.
* `amount`, `currency`: Payment amount & currency.
* `paymentMethod`: Enum or class (CreditCard, DebitCard, etc.).
* `status`: Enum (Pending, Success, Failed).
* `userId`: User making the payment.

---

### 2. **PaymentMethod (Interface)**

Defines the contract for different payment types.

```java
public interface PaymentMethod {
    PaymentResponse authorize(Payment payment);
    PaymentResponse capture(Payment payment);
    PaymentResponse refund(Payment payment);
}
```

---

### 3. **Concrete Payment Methods**

Example: CreditCardPayment

```java
public class CreditCardPayment implements PaymentMethod {
    private String cardNumber;
    private String cardHolderName;
    private String expiryDate;
    private String cvv;

    @Override
    public PaymentResponse authorize(Payment payment) {
        // Call to bank’s authorization API
        return new PaymentResponse(true, "Authorized");
    }

    @Override
    public PaymentResponse capture(Payment payment) {
        // Call to capture API
        return new PaymentResponse(true, "Captured");
    }

    @Override
    public PaymentResponse refund(Payment payment) {
        // Refund API call
        return new PaymentResponse(true, "Refunded");
    }
}
```

Similar classes: `DebitCardPayment`, `NetBankingPayment`, `WalletPayment`, etc.

---

### 4. **PaymentResponse**

Result of payment operations.

```java
public class PaymentResponse {
    private boolean success;
    private String message;
    private String transactionId;
    // constructor, getters
}
```

---

### 5. **PaymentProcessor**

Handles processing by delegating to the appropriate payment method.

```java
public class PaymentProcessor {
    public PaymentResponse processPayment(Payment payment) {
        PaymentMethod method = getPaymentMethod(payment.getPaymentMethod());
        PaymentResponse response = method.authorize(payment);
        if (response.isSuccess()) {
            // Optionally capture payment
            response = method.capture(payment);
        }
        return response;
    }

    private PaymentMethod getPaymentMethod(PaymentMethodType type) {
        // Factory or DI to return correct PaymentMethod instance
    }
}
```

---

### 6. **TransactionLogger**

Logs all payment transactions for audit.

```java
public class TransactionLogger {
    public void log(Payment payment, PaymentResponse response) {
        // Save details to DB or file system
    }
}
```

---

### 7. **Exceptions and Retry**

Custom exceptions for failures, and retry logic in `PaymentProcessor` for transient errors.

---

## Interaction Flow

1. Client calls `PaymentProcessor.processPayment(payment)`.
2. `PaymentProcessor` fetches the right `PaymentMethod` implementation.
3. Calls `authorize()`, then `capture()` on success.
4. Logs the transaction.
5. Returns result to client.

---

## Diagram (Class-level)

```
+-------------------+        +--------------------+
|   PaymentProcessor |<>------|  PaymentMethod     |<|--+
+-------------------+        +--------------------+   |
| +processPayment()  |                                  |
+-------------------+                                  |
                                                      |
                +-----------------+   +--------------------+
                | CreditCardPayment|   |  NetBankingPayment |
                +-----------------+   +--------------------+
```

---

## Summary

* Use **Strategy pattern** for multiple payment types (`PaymentMethod` interface).
* Decouple processing (`PaymentProcessor`) from payment implementations.
* Support authorization, capture, refund as core methods.
* Log all transactions.
* Handle errors and retries gracefully.

---

## 72. What is a class diagram and how do you draw one?

Here’s a detailed explanation:

---

## What is a Class Diagram?

A **Class Diagram** is a type of static **UML (Unified Modeling Language)** diagram that visually represents the **structure** of a system by showing its:

* **Classes** (blueprints for objects),
* Their **attributes** (data/properties),
* Their **methods** (functions/behavior),
* And **relationships** between classes (associations, inheritance, dependencies).

---

### Why use Class Diagrams?

* To **visualize** the design and structure of an application before or during development.
* To **communicate** system design with stakeholders and team members.
* To **document** system architecture.
* To help with **code generation** in some tools.

---

## Key Components of a Class Diagram

| Element           | Description                           | UML Notation                                                                          |
| ----------------- | ------------------------------------- | ------------------------------------------------------------------------------------- |
| **Class**         | Represents an entity or concept       | Rectangle divided into 3 parts: <br> 1) Class name <br> 2) Attributes <br> 3) Methods |
| **Attributes**    | Data fields / properties of the class | Listed in second section with visibility (`+` public, `-` private, `#` protected)     |
| **Methods**       | Functions/operations of the class     | Listed in third section with visibility                                               |
| **Relationships** | Connections between classes           | See types below                                                                       |

---

## Types of Relationships

| Relationship Type                | Description                                        | UML Symbol                                         |
| -------------------------------- | -------------------------------------------------- | -------------------------------------------------- |
| **Association**                  | Basic connection, "uses" or "has"                  | Solid line                                         |
| **Multiplicity**                 | Number of instances involved                       | Numbers near association ends (e.g., 1..\*, 0..1)  |
| **Inheritance (Generalization)** | "Is-a" relationship; subclass inherits superclass  | Solid line with hollow triangle pointing to parent |
| **Aggregation**                  | Whole-part relationship (weak)                     | Solid line with hollow diamond at whole side       |
| **Composition**                  | Strong whole-part (part can't exist without whole) | Solid line with filled diamond at whole side       |
| **Dependency**                   | One class depends on another                       | Dashed arrow                                       |

---

## How to Draw a Class Diagram (Step-by-step)

1. **Identify Classes**

    * Find key entities in the system (e.g., User, Order, Product).

2. **Add Attributes & Methods**

    * List important properties and operations of each class.

3. **Define Relationships**

    * Identify associations, inheritance, aggregations, compositions.

4. **Add Multiplicities**

    * Specify how many instances participate in relationships.

5. **Use proper visibility**

    * Mark attributes and methods as `+` (public), `-` (private), `#` (protected).

6. **Organize layout**

    * Arrange classes and relationships clearly for readability.

---

## Simple Example: Library System (Partial)

```
+-------------------+
|     Book          |
+-------------------+
| -title: String    |
| -author: String   |
| -isbn: String     |
+-------------------+
| +checkout()       |
| +returnBook()     |
+-------------------+

         1           *
+-------------------+        +------------------+
|     Library       |<>------|     BookCopy     |
+-------------------+        +------------------+
| -name: String     |        | -copyId: String   |
+-------------------+        | -isAvailable: Bool|
| +addBookCopy()    |        +------------------+
+-------------------+        | +markAvailable()  |
                             | +markUnavailable()|
                             +------------------+
```

* **Library** has many (**1..**\* ) **BookCopies** (aggregation).
* Book has attributes and methods.
* `<>` hollow diamond = aggregation.

---

## Tools for Drawing Class Diagrams

* Visual Paradigm
* Lucidchart
* draw\.io
* StarUML
* PlantUML (text-to-diagram)

---

## 73. How do you model relationships: aggregation vs composition?

Aggregation and composition are two important ways to model relationships between classes, especially to represent "whole-part" hierarchies. They describe how objects are connected and how their lifecycles relate.

---

## Aggregation vs Composition: Overview

| Aspect               | Aggregation                                             | Composition                                             |
| -------------------- | ------------------------------------------------------- | ------------------------------------------------------- |
| Meaning              | "Has-a" relationship (weak whole-part)                  | Strong "Has-a" relationship (strong whole-part)         |
| Ownership            | Whole and part have independent lifecycles              | Whole owns the part; part can't exist without whole     |
| Lifecycle Dependency | Part can exist independently of whole                   | Part is created and destroyed along with whole          |
| UML Notation         | Hollow diamond at the whole side                        | Filled (black) diamond at the whole side                |
| Example              | A `Team` has `Players` (players can exist outside team) | A `House` has `Rooms` (rooms don't exist without house) |

---

## Details with Examples

### 1. Aggregation

* Represents a **weak** ownership.
* The part object can exist independently.
* Example: A **University** aggregates **Departments**. Departments can exist even if the university closes (maybe they join another university).

**Code Example:**

```java
class Department {
    String name;
}

class University {
    List<Department> departments;  // Aggregation: departments can exist without university
}
```

**UML Symbol:**

```
University <>---- Department
(Hollow diamond)
```

---

### 2. Composition

* Represents **strong** ownership.
* The part's lifecycle depends on the whole.
* When the whole is destroyed, parts are also destroyed.
* Example: A **Car** is composed of **Engine** and **Wheels**. Without the car, these parts don't meaningfully exist.

**Code Example:**

```java
class Engine {
    // Engine details
}

class Car {
    private Engine engine; // Composition: engine lifecycle bound to car

    public Car() {
        this.engine = new Engine();
    }
}
```

**UML Symbol:**

```
Car ◆---- Engine
(Filled diamond)
```

---

## Summary Table

| Feature          | Aggregation              | Composition                  |
| ---------------- | ------------------------ | ---------------------------- |
| Ownership        | Weak (shared ownership)  | Strong (exclusive ownership) |
| Lifecycle        | Part can outlive whole   | Part destroyed with whole    |
| UML Notation     | Hollow diamond           | Filled diamond               |
| Use Case Example | Library aggregates Books | House composes Rooms         |

---

## How to decide which one to use?

* If the part can exist without the whole → **Aggregation**
* If the part cannot exist without the whole → **Composition**

---

## 74. How would you handle concurrency in a ticket booking system?

Handling **concurrency** in a ticket booking system is critical to prevent problems like **overbooking** or inconsistent data when multiple users try to book the same seat/ticket simultaneously.

---

## Key Challenges

* Multiple users trying to book the **same ticket/seat** at the same time.
* Preventing **double booking**.
* Maintaining **data consistency**.
* Handling high traffic efficiently.

---

## Common Approaches to Handle Concurrency

### 1. **Database-level Concurrency Control**

* Use **transactions** with appropriate isolation levels (e.g., **Serializable**, **Repeatable Read**) to prevent dirty reads and race conditions.
* **Row-level locking**: Lock the seat/record when a booking is in progress.
* **Optimistic Locking**:

    * Read current version (timestamp or version number) of the seat record.
    * When updating (booking), check if the version is unchanged.
    * If changed, reject and retry booking.
* **Pessimistic Locking**:

    * Lock the seat record before booking, so others wait.

**Example:**

```sql
BEGIN TRANSACTION;
SELECT * FROM seats WHERE seat_id = 101 FOR UPDATE;  -- Locks row
-- Check if seat is available
UPDATE seats SET status = 'booked' WHERE seat_id = 101;
COMMIT;
```

---

### 2. **Application-level Locks**

* Use distributed locks if multiple app servers exist.
* Tools like **Redis** with RedLock algorithm or **Zookeeper** can manage distributed locks.
* Acquire lock before processing booking; release after done.

---

### 3. **Atomic Operations**

* Use atomic DB operations or compare-and-swap (CAS) mechanisms to update seat status.
* For example, update only if seat is free:

```sql
UPDATE seats SET status = 'booked' WHERE seat_id = 101 AND status = 'available';
```

Check number of rows affected; if 0, booking failed due to seat already booked.

---

### 4. **Queue-based Booking**

* Use a **message queue** to serialize booking requests.
* Booking requests are processed one at a time, ensuring no concurrent booking for same seat.
* Adds latency but very safe.

---

### 5. **Seat Reservation with Timeout**

* When user selects a seat, **reserve it temporarily** (e.g., 5 minutes).
* During reservation period, block others from booking.
* If user doesn’t complete payment, release the seat.

---

### 6. **Eventual Consistency and Compensation**

* In complex distributed systems, sometimes eventual consistency is acceptable.
* Use compensating transactions to fix errors after the fact.

---

## Summary Table

| Approach                      | Pros                          | Cons                                  |
| ----------------------------- | ----------------------------- | ------------------------------------- |
| DB Transactions (Row Locking) | Strong consistency, simple    | Can cause contention, performance hit |
| Optimistic Locking            | Scalable, less blocking       | Requires retries                      |
| Distributed Locks             | Works for multi-server setups | Adds complexity                       |
| Atomic DB Updates             | Simple, efficient             | Limited to DB capabilities            |
| Queue-based Booking           | Guarantees order              | Adds latency, complexity              |
| Seat Reservation              | Good UX, prevents race window | Requires timeout management           |

---

## Example Flow (Optimistic Locking):

1. Read seat availability + version.
2. User tries to book seat.
3. Update seat status with `WHERE seat_id=X AND version=Y`.
4. If update count = 0, reject booking (someone else booked it).
5. Else success.

---

## 75. Design a task scheduling system (like Trello).

Let’s design a **Task Scheduling System** similar to **Trello** with a focus on core features, scalability, and maintainability.

---

# Design: Task Scheduling System (Trello-like)

---

## Requirements (Core Features)

1. Users can **create boards** (projects).
2. Boards have **lists** (columns, e.g., To Do, In Progress, Done).
3. Lists contain **tasks/cards** with details like title, description, due date, labels.
4. Users can **assign tasks** to members.
5. Tasks can have comments, attachments, checklists.
6. Support **real-time collaboration** (optional).
7. Support notifications for updates.
8. Handle large scale: many users, boards, and tasks.

---

## High-Level Components

* **User Service:** Manage user accounts.
* **Board Service:** Create/manage boards.
* **List Service:** Manage lists inside boards.
* **Task Service:** Create/manage tasks.
* **Notification Service:** Notify users on updates.
* **Collaboration / Real-time Service:** WebSocket or push updates.
* **Database(s):** Store users, boards, lists, tasks, comments.

---

## Data Model (Simplified)

| Entity  | Key Attributes                                                                        |
| ------- | ------------------------------------------------------------------------------------- |
| User    | userId, name, email                                                                   |
| Board   | boardId, name, ownerId, list of lists                                                 |
| List    | listId, name, boardId, position/order                                                 |
| Task    | taskId, title, description, listId, assignedUserId, dueDate, labels, status, comments |
| Comment | commentId, taskId, authorId, content, createdAt                                       |

---

## Class Diagram (Conceptual)

```
+----------------+          +---------------+          +----------------+
|     User       |          |     Board     |          |      List      |
+----------------+          +---------------+          +----------------+
| -userId        |<>------- | -boardId      |<>------- | -listId        |
| -name          | 1      * | -name         | 1      * | -name          |
| -email         |          | -ownerId      |          | -boardId       |
+----------------+          +---------------+          +----------------+
                                                      
                                                      
                         +----------------+
                         |      Task      |
                         +----------------+
                         | -taskId        |
                         | -title         |
                         | -description   |
                         | -listId        |
                         | -assignedUserId|
                         | -dueDate       |
                         | -labels        |
                         +----------------+
                                |
                                *  
                             +---------+
                             |Comment  |
                             +---------+
```

---

## Detailed Explanation

### Boards & Lists

* A **Board** is like a project workspace.
* Each board contains multiple **Lists** (columns).
* Lists order is important (can be moved).

### Tasks (Cards)

* Tasks belong to a list.
* Tasks have title, description, assigned users, due date, labels, comments.
* Tasks can move between lists (drag and drop).

### Comments

* Users can comment on tasks.
* Comments stored with timestamps and authors.

---

## API Design (Sample endpoints)

* `POST /boards` - Create board
* `GET /boards/{boardId}` - Get board details with lists and tasks
* `POST /boards/{boardId}/lists` - Add list to board
* `POST /lists/{listId}/tasks` - Add task to list
* `PUT /tasks/{taskId}` - Update task (move between lists, update details)
* `POST /tasks/{taskId}/comments` - Add comment to task
* `GET /users/{userId}/notifications` - Fetch notifications

---

## Handling Real-time Collaboration

* Use **WebSocket** or **Socket.IO** for real-time updates.
* When one user updates a task or list order, send update events to others.
* Optimistic UI updates with conflict resolution.

---

## Scalability & Persistence

* Use **NoSQL DB** (e.g., MongoDB) or **relational DB** depending on query needs.
* Indexing on boardId, listId, taskId for fast retrieval.
* Cache popular boards/tasks using Redis or similar.
* Use microservices to separate concerns (User service, Board service, Task service).

---

## Optional Features

* Checklists on tasks.
* Attachments (files/images).
* Notifications via email/push.
* User roles and permissions per board.

---

## Summary

| Layer                    | Responsibility                                                    |
| ------------------------ | ----------------------------------------------------------------- |
| Client/UI                | Render boards, lists, tasks; support drag-drop; real-time updates |
| API Gateway              | Entry point for all client requests                               |
| Board/List/Task Services | Business logic to manage boards, lists, tasks                     |
| Database                 | Store persistent data                                             |
| Real-time Service        | Handle WebSocket connections for live updates                     |
| Notification Service     | Send notifications on task updates                                |

---

If you want, I can also help you with a detailed **sequence diagram**, specific **class implementations**, or **database schema** for this design!

---

### 🔹 **76–100: Advanced Topics, Patterns, and Trade-Offs**

## 76. What is eventual consistency and how do you design for it?

**Eventual consistency** is a consistency model used in distributed systems to achieve high availability and partition tolerance (as per the CAP theorem). It means that:

> **All nodes will eventually hold the same data**, but **they may not be consistent at any given moment in time**.

---

## 🔧 Why Use Eventual Consistency?

* Needed in **distributed databases** and **replicated systems** (e.g., DynamoDB, Cassandra, Amazon S3).
* Supports **high availability** and **partition tolerance** (especially during network failures).
* Ideal for systems where **immediate consistency is not critical**, such as:

    * Social media feeds
    * Caching systems
    * Email notifications
    * Shopping cart syncing

---

## ✅ Real-world Example

Imagine you're posting a tweet. After hitting "Tweet":

* Your tweet shows up immediately on your profile (one replica).
* Friends in other locations may see the tweet a few seconds later (eventual sync).

---

## 🔄 How to Design for Eventual Consistency

Here’s how to build a system that can safely tolerate eventual consistency:

---

### 1. **Use Asynchronous Writes / Replication**

* Changes are **written to one node** and **replicated in the background** to others.
* Often done using **message queues** or **log-based replication**.

**Example**:

```text
Client → Primary DB → Kafka → Replica DBs
```

---

### 2. **Design for Idempotency**

* **Repeated operations** should have the same effect as a single one.
* Prevents issues if the same message is processed more than once.

**Example**: Marking a notification as read multiple times should not cause errors.

---

### 3. **Conflict Resolution**

* When different replicas have conflicting changes, you need resolution strategies:

    * **Last Write Wins (LWW)**
    * **Merge strategies** (e.g., CRDTs – Conflict-free Replicated Data Types)
    * **Manual resolution** (e.g., alert user to choose version)

---

### 4. **Use Versioning / Timestamps**

* Store a **version number** or **timestamp** with each record.
* Helps in determining the most recent update during synchronization.

---

### 5. **Background Sync / Reconciliation Jobs**

* Periodic background jobs that **reconcile** inconsistencies between replicas.

---

### 6. **User Feedback (UI Design)**

* Show users that data is being **synced** or **pending update**.
* Example: Gmail's "Saving…" or Google Docs' "All changes saved in Drive".

---

### 7. **Eventual Consistency Boundaries**

* Identify which parts of your system **must be strongly consistent** and which can tolerate **eventual consistency**.

---

## 🧠 Example Architecture: Shopping Cart (Eventually Consistent)

1. User adds an item to the cart.
2. Update is written to the cache (fast), queued to update DB.
3. DB update might lag, but the user sees an immediate response.
4. Queue retries on failure.
5. Background job reconciles cart data nightly.

---

## 🆚 Eventual Consistency vs Strong Consistency

| Feature       | Strong Consistency    | Eventual Consistency   |
| ------------- | --------------------- | ---------------------- |
| Read Accuracy | Always latest value   | Might see stale data   |
| Performance   | Slower (locks, sync)  | Faster (async updates) |
| Availability  | Lower under partition | Higher                 |
| Use Cases     | Banking, Auth, Stock  | Feeds, Caching, Logs   |

---

## ✅ When to Use Eventual Consistency

Use it when:

* **High availability** is more important than strict accuracy.
* Systems can tolerate **stale data** for a short time.
* You want to support **offline mode** or **sync later** behavior.

---

## 77. Explain CQRS and Event Sourcing.

**CQRS (Command Query Responsibility Segregation)** and **Event Sourcing** are architectural patterns often used in complex, high-scale, or distributed systems to improve **performance**, **scalability**, and **auditability**.

---

## 🔹 CQRS (Command Query Responsibility Segregation)

### 💡 Concept:

CQRS separates the **read** and **write** operations of a system into different models.

---

### ✅ Key Ideas:

| Operation Type | Responsibility    | Characteristics                   |
| -------------- | ----------------- | --------------------------------- |
| **Command**    | Write/update data | Changes state, often async        |
| **Query**      | Read data         | No side effects, can be optimized |

---

### 📌 Why use CQRS?

* Optimize **reads and writes separately**.
* Allow **scaling read and write models independently**.
* Use different **data models** for commands and queries.
* Support **complex business logic** for commands.
* Improve **performance** and **security**.

---

### 🧱 Example:

Let’s say you’re building an e-commerce system:

* **Command**: AddItemToCart → modifies the cart state.
* **Query**: GetCartSummary → reads from a read-optimized cache or DB.

```text
[Client]
   |
   |---> Command --> [Write Model] --> [Event or DB]
   |
   |---> Query  --> [Read Model/Projection]
```

---

### ⚖️ When to use CQRS?

* Systems with **high read-to-write ratio**.
* **Complex domains** with different needs for reading and writing.
* When you want **eventual consistency** between writes and reads.

---

## 🔹 Event Sourcing

### 💡 Concept:

Event Sourcing is a pattern where **state changes are stored as a sequence of events**, not as direct updates to the data.

Instead of updating rows, you **append events** that describe the change.

---

### ✅ Key Ideas:

* The **current state** is derived by **replaying all past events**.
* Events are **immutable** and stored in an **event store**.
* Supports **rebuilding state**, **auditing**, **debugging**, and **time travel**.

---

### 🧱 Example:

Let’s say you manage a bank account:

Instead of storing just the balance, store:

1. `AccountOpened`
2. `MoneyDeposited(100)`
3. `MoneyWithdrawn(50)`

You can derive the current balance by **replaying events**: 100 - 50 = 50.

---

### 💾 Event Store vs Traditional DB

| Event Store            | Traditional DB          |
| ---------------------- | ----------------------- |
| Append-only log        | CRUD operations         |
| Full history available | Only latest state       |
| Replayable / auditable | Hard to audit           |
| Better suited for CQRS | Generic CRUD operations |

---

### 🔁 Rebuilding State:

You can rebuild any entity’s state by:

```java
AccountState replay(List<AccountEvent> events) {
    AccountState state = new AccountState();
    for (AccountEvent event : events) {
        state.apply(event);
    }
    return state;
}
```

---

## 🔄 CQRS + Event Sourcing: How They Work Together

* **Commands** generate **events**.
* Events are stored in an **event store**.
* **Projections** (read models) are built asynchronously by subscribing to events.

```text
[Command] → [Event Handler] → [Event Store]
                                 ↓
                       [Read Model Projector]
                                 ↓
                          [Read DB or Cache]
```

---

## ✅ Benefits

### CQRS

* Separation of concerns
* Better scalability
* Optimized read/write models

### Event Sourcing

* Full audit trail
* Recoverable system state
* Enables complex workflows (like sagas)

---

## ⚠️ Challenges

* Increased complexity (especially eventual consistency)
* Need for idempotent event processing
* More infrastructure: event store, queues, projections
* Harder debugging in async environments

---

## 🔍 Use Cases

* Banking systems (audit required)
* Order processing (state transitions)
* Messaging platforms (history of messages)
* Collaborative editing (document versions)
* IoT systems (sensor event logs)

---

## ✅ Summary

| Pattern        | Purpose                        | Typical Use                        |
| -------------- | ------------------------------ | ---------------------------------- |
| CQRS           | Separate read and write models | Read-heavy or complex systems      |
| Event Sourcing | Persist changes as events      | Audit/log/history critical systems |

---

## 78. How do you handle data migration in distributed systems?

Handling **data migration in distributed systems** is a complex task that requires careful planning, consistency strategies, monitoring, and rollback mechanisms. The goal is to **move or transform data across systems or versions** with **minimal downtime**, **data loss**, or **inconsistency**.

---

## 🔧 Common Use Cases

* Schema changes (adding/removing columns, indexes)
* Moving from one database to another (e.g., SQL → NoSQL)
* Sharding or rebalancing data across nodes
* Upgrading database versions
* Migrating to cloud-based storage or distributed DBs

---

## ✅ Key Challenges

| Challenge               | Description                                             |
| ----------------------- | ------------------------------------------------------- |
| **Consistency**         | Ensuring no data is lost or duplicated during migration |
| **Downtime**            | Keeping the system running or minimizing downtime       |
| **Data Volume**         | Migrating large datasets efficiently                    |
| **Application Changes** | Syncing schema and application-level changes            |
| **Fault Tolerance**     | Ensuring recovery from partial failures                 |

---

## 🧭 Step-by-Step Approach

### 1. **Plan the Migration**

* Define scope and critical paths.
* Identify data sources and targets.
* Decide between **online** vs **offline** migration.
* Choose the **migration strategy** (see below).

---

### 2. **Choose a Migration Strategy**

#### 🔁 Full Migration (Offline)

* System is taken offline → Data migrated → System restarted.
* Best for small systems or non-critical data.

#### 🧵 Blue-Green Deployment

* Run old and new systems in parallel.
* Switch traffic gradually after data sync.

#### 🔄 Dual Writes (for Live Migrations)

* Both old and new systems receive writes temporarily.
* Ensures no data is lost during cut-over.

#### 🕑 Change Data Capture (CDC)

* Use binlogs or events to track changes in real-time.
* Tools: **Debezium**, **Kafka Connect**, **AWS DMS**

---

### 3. **Migrate Data in Batches**

* Use **chunking** to move data in manageable pieces.
* Example: 10,000 rows at a time to avoid overwhelming the network.

---

### 4. **Ensure Idempotency & Ordering**

* Make migration processes **idempotent** (safe to run multiple times).
* Maintain **ordering guarantees** if updates are dependent.

---

### 5. **Consistency Strategy**

| Strategy       | Description                                       |
| -------------- | ------------------------------------------------- |
| **Strong**     | Use locks, versioning, or synchronous updates     |
| **Eventual**   | Allow temporary inconsistency, sync in background |
| **Quiescence** | Freeze writes temporarily for a safe switch       |

---

### 6. **Validate Migrated Data**

* Use hashing, row counts, and checksums to validate.
* Compare pre- and post-migration snapshots.

---

### 7. **Monitoring and Logging**

* Monitor latency, throughput, errors.
* Use centralized logs (e.g., ELK, Grafana, Prometheus) for observability.

---

### 8. **Rollback Strategy**

* Always prepare for failure:

    * Backup original data.
    * Use feature flags or toggles.
    * Keep old system operational temporarily.

---

## 💡 Real-World Tools

| Tool                   | Use Case                  |
| ---------------------- | ------------------------- |
| **Apache Kafka**       | Event log replication     |
| **Debezium**           | Change Data Capture (CDC) |
| **Flyway / Liquibase** | Schema migrations         |
| **AWS DMS**            | Cloud-based DB migrations |
| **Google Datastream**  | Live replication          |

---

## 🧠 Example Scenario: Migrating from Monolith DB to Sharded DB

1. **Phase 1**: Read from monolith, write to both (dual writes)
2. **Phase 2**: Backfill old data into sharded DB
3. **Phase 3**: Redirect reads to new DB
4. **Phase 4**: Monitor for consistency
5. **Phase 5**: Decommission old DB

---

## ✅ Best Practices

* **Test migration** on a staging environment.
* Use **feature toggles** to switch logic at runtime.
* Build **idempotent migration scripts**.
* **Document everything**: schema changes, scripts, and cut-over steps.
* Always ensure **data durability and consistency guarantees**.

---

## 79. How would you design a pub-sub system like Kafka?

Designing a **Pub-Sub (Publish-Subscribe)** system like **Apache Kafka** involves building a high-throughput, fault-tolerant, scalable, and distributed messaging system that decouples producers and consumers. Below is a detailed explanation with design components, use cases, and architectural diagrams.

---

## 🧠 Goal of a Pub-Sub System

To allow **producers** to send messages to **topics**, and **consumers** to subscribe to those topics and receive messages asynchronously.

---

## ✅ Core Requirements

* High throughput (millions of messages/sec)
* Durability and persistence
* Scalability (horizontal and vertical)
* Partitioning for parallelism
* Fault tolerance
* Consumer group management
* At-least-once or exactly-once delivery

---

## 🧱 Key Components

| Component                      | Role                                                            |
| ------------------------------ | --------------------------------------------------------------- |
| **Producer**                   | Sends (publishes) messages to a topic                           |
| **Topic**                      | Logical channel to which producers send and consumers subscribe |
| **Partition**                  | Topics are split into partitions to scale horizontally          |
| **Broker**                     | Stores messages and manages topics/partitions                   |
| **Consumer**                   | Reads (subscribes) messages from topics                         |
| **Consumer Group**             | Group of consumers that share the load of a topic               |
| **Zookeeper/Metadata Service** | Manages brokers, topics, partitions, and coordination           |

---

## 🖼️ High-Level Architecture

```text
          +-------------+         +-------------------+
          |   Producer  |  --->   |  Broker (Topic A) |
          +-------------+         +-------------------+
                                          |
                      +------------------+-----------------+
                      | Partition 0      | Partition 1     |
                      | Msg1, Msg2, ...  | MsgX, MsgY, ... |
                      +------------------+-----------------+
                                ↓                    ↓
                         +-------------+      +-------------+
                         | Consumer C1 |      | Consumer C2 |
                         +-------------+      +-------------+
```

---

## ⚙️ Internal Data Flow (Step-by-Step)

### 🟢 1. **Producer Sends Message**

* Message is written to a **partition** of a **topic** (based on key, hash, or round-robin).
* Written **sequentially** to disk (append-only log).
* Optionally **acknowledged** to the producer (ACK settings can be `0`, `1`, `all`).

### 🟡 2. **Broker Stores Message**

* Messages are stored durably using an append-only log.
* Data is replicated across multiple brokers (leader-follower).
* Data is retained based on time or size policies.

### 🔵 3. **Consumer Subscribes and Polls**

* Consumer subscribes to a **topic** (or partition).
* Reads messages sequentially by offset.
* Commits offset manually or automatically (depending on config).

### 🔄 4. **Consumer Group Coordination**

* Each partition is assigned to one consumer in the group.
* Consumers maintain **offset** (where they left off).
* If a consumer dies, others **rebalance** and take over.

---

## 🔐 Reliability and Fault Tolerance

* **Replication**: Each partition has replicas (leader + followers).
* **Leader Election**: If a leader broker fails, another replica is promoted.
* **Durability**: Messages are flushed to disk before ACKs (based on config).
* **Idempotency**: Producers can send the same message safely without duplication.

---

## ⚙️ Scalability

* Scale **brokers horizontally**: More partitions → more parallelism.
* Scale **consumers in a group**: Each reads from different partitions.
* Topics can be **sharded** using custom keys or consistent hashing.

---

## 🧩 Data Structures

* **Topic**: A logical collection of partitions.
* **Partition**: A sequential, append-only log.
* **Message**: Consists of key, value, timestamp, and offset.
* **Offset**: Pointer to track message read position.

---

## ✅ Delivery Semantics

| Type          | Description                                        |
| ------------- | -------------------------------------------------- |
| At-most-once  | Messages may be lost but never duplicated          |
| At-least-once | Messages are never lost but may be duplicated      |
| Exactly-once  | Messages are neither lost nor duplicated (hardest) |

Kafka supports **idempotent producers** and **transactional writes** for exactly-once semantics.

---

## 💡 Optional Enhancements

* **Schema Registry** (e.g., for Avro): Ensure producers/consumers agree on message format.
* **Dead Letter Queues**: For handling message processing failures.
* **Compression**: GZIP, Snappy, or LZ4 for message batching.
* **Monitoring & Metrics**: Expose metrics to Prometheus, ELK, etc.

---

## 🔧 Tech Stack (if building your own)

| Concern         | Technology / Design                              |
| --------------- | ------------------------------------------------ |
| Message Storage | Append-only log files (custom format or RocksDB) |
| Coordination    | Zookeeper / Raft / etcd                          |
| Networking      | Netty / gRPC / HTTP                              |
| Persistence     | Filesystem / SSD / Cloud storage                 |
| Fault Tolerance | Raft or Paxos for leader election                |
| APIs            | REST, gRPC, Kafka-compatible API                 |

---

## 🧪 Real-world Use Cases

* Log aggregation
* Stream processing (Kafka + Flink/Spark)
* Event sourcing
* Audit logging
* Communication between microservices

---

## ✅ Summary

| Feature                       | Kafka-Like Design                     |
| ----------------------------- | ------------------------------------- |
| Decouples producers/consumers | ✔️                                    |
| Persistent message log        | ✔️ Durable storage per partition      |
| High throughput               | ✔️ Batched, compressed writes/read    |
| Scalability                   | ✔️ Add brokers, partitions, consumers |
| Reliability                   | ✔️ Replication, acknowledgments       |

---

## 80. How would you implement distributed locking?

Implementing **distributed locking** is essential when you have multiple instances of an application (distributed system) trying to coordinate access to shared resources—such as database rows, cache entries, or files—to prevent **race conditions**, **double processing**, or **data corruption**.

---

## ✅ Goals of Distributed Locking

* **Mutual exclusion**: Only one node holds the lock at a time.
* **Fault tolerance**: Locks should be released if the node crashes.
* **Fairness**: Locks should be granted in order.
* **Availability**: Locking mechanism should be highly available and performant.

---

## 🔑 Common Implementations

### 1. **Using Redis (Redlock Algorithm)**

Redis is commonly used due to its speed and simplicity.

#### ✔️ How it works:

* Use `SET key value NX PX timeout` to acquire the lock:

  ```bash
  SET lock:resource1 UUID-NODE-ID NX PX 3000
  ```

    * `NX`: only set if not exists.
    * `PX 3000`: expires in 3000ms.

* To release:

    * Only delete the key if it’s owned by the same UUID.
    * Use a **Lua script** to ensure atomic check and delete.

#### ✅ Advantages:

* Simple, fast.
* Expiry prevents deadlocks.
* Works with Redis clusters (with Redlock for safety).

#### 🔁 Redlock (Robust algorithm):

* Proposed by Redis creator.
* Acquire lock on **majority of N Redis nodes** within time window.
* Requires synchronized clocks and consistent Redis deployments.

#### ❗ Caveats:

* Not a perfect consensus algorithm.
* Use carefully for critical financial or transactional operations.

---

### 2. **Using ZooKeeper (Ephemeral Sequential Nodes)**

Zookeeper is widely used in distributed systems for coordination.

#### ✔️ How it works:

* Clients create an **ephemeral sequential znode** under a lock path.
* The client with the **lowest sequence number** owns the lock.
* Others **watch the node just before them** and wait for deletion.

#### ✅ Advantages:

* Fair ordering of lock acquisition.
* Automatically releases locks on client disconnects (ephemeral).
* Strong consistency guarantees (ZAB protocol).

#### ❗ Disadvantages:

* Slower than Redis.
* Operational complexity of maintaining Zookeeper cluster.

---

### 3. **Using Database Row Locks**

Use database-level locking mechanisms like:

* `SELECT FOR UPDATE` (in RDBMS like PostgreSQL, MySQL)
* Insert a row in a lock table with a unique constraint.

#### ✅ Advantages:

* Leverages existing DB.
* Simple for small systems.

#### ❌ Limitations:

* Not horizontally scalable.
* Tightly coupled to DB performance and availability.

---

### 4. **Using Consul or Etcd (With RAFT Consensus)**

Both Consul and Etcd offer APIs for distributed coordination and locks.

#### ✔️ How it works:

* Use atomic key-value operations with TTL.
* Leverages **RAFT** for strong consistency.

#### ✅ Advantages:

* Strong consistency and high availability.
* Suitable for microservice coordination (e.g., leader election).

---

## 🧱 Example: Redis Lock Pseudocode (Java)

```java
public boolean acquireLock(String key, String value, long ttlMillis) {
    return redis.set(key, value, SetParams.setParams().nx().px(ttlMillis)) != null;
}

public void releaseLock(String key, String value) {
    String lua = """
        if redis.call("get", KEYS[1]) == ARGV[1] then
            return redis.call("del", KEYS[1])
        else
            return 0
        end
    """;
    redis.eval(lua, List.of(key), List.of(value));
}
```

---

## ⚠️ Key Design Considerations

| Aspect              | What to Watch For                                |
| ------------------- | ------------------------------------------------ |
| **Deadlocks**       | Always use TTLs or heartbeats                    |
| **Race conditions** | Atomic operations are a must                     |
| **Clock skew**      | Especially in Redlock, keep clock drift low      |
| **Failover**        | Locks should auto-expire or migrate              |
| **Idempotency**     | Actions guarded by locks should be safe to retry |

---

## 🧠 Real-World Examples

| Use Case                         | Lock Scope                        |
| -------------------------------- | --------------------------------- |
| E-commerce checkout              | Lock per order or product stock   |
| Cron job runner in microservices | Lock per task                     |
| Leader election                  | Lock per cluster or service group |
| Distributed queue consumers      | Lock per queue partition          |

---

## ✅ Summary

| Method      | Use When                                      | Tools          |
| ----------- | --------------------------------------------- | -------------- |
| Redis Lock  | Fast, simple locks, less critical ops         | Redis, Redlock |
| ZooKeeper   | Need ordering, fairness, or leader election   | Apache ZK      |
| DB Lock     | Small-scale or already DB-centric systems     | SQL DBs        |
| Etcd/Consul | Microservice coordination, strong consistency | Etcd, Consul   |

---

## 81. What is idempotency and how do you enforce it in APIs?

**Idempotency** is a property of an operation that ensures **no matter how many times it is performed, the result remains the same** as if it were performed once.

---

## ✅ Why Idempotency Matters in APIs

In **distributed systems** and **networked APIs**, retries may happen due to:

* Timeouts
* Network failures
* Client retries
* Load balancer retries

To avoid **duplicate actions** (like double charges or double order creation), APIs must be idempotent.

---

## 📌 Real-World Example

### ❌ Non-idempotent behavior:

```http
POST /orders
Body: { "item": "iPhone", "qty": 1 }
```

* If client retries due to timeout, it might **create multiple orders**.

### ✅ Idempotent behavior:

```http
POST /orders
Headers: Idempotency-Key: abc123
Body: { "item": "iPhone", "qty": 1 }
```

* Server processes the first request, stores the result with key `abc123`.
* On retries with the same key, it **returns the same response** without creating a new order.

---

## 🛠️ How to Enforce Idempotency in APIs

### 🔹 1. **Use an Idempotency Key**

* Client sends a unique header:

  ```
  Idempotency-Key: <unique-uuid>
  ```
* Server stores result (status + response) in a persistent store.
* On subsequent calls with the same key:

    * Return cached result.
    * Do **not** reprocess.

#### ✅ Good for:

* **POST**, **PATCH**, or any unsafe methods.
* Payment APIs, order processing, email sending.

### 🔹 2. **PUT, DELETE are Naturally Idempotent**

These HTTP methods should already be idempotent:

* `PUT /user/123 {"name": "John"}` → sets the same state every time
* `DELETE /user/123` → multiple calls delete the same user (no harm in repeating)

### 🔹 3. **Database Constraints**

Use:

* **Unique keys** (e.g., order\_id, payment\_id)
* **Transactions**: Ensure "insert-if-not-exists" logic
* UPSERT operations (e.g., `INSERT ON CONFLICT DO NOTHING`)

### 🔹 4. **Token-based Deduplication**

Use a deduplication token (like a UUID or hash) generated on the client:

* Save it in a database with a status (e.g., `processed`, `failed`)
* Reuse the result if the token already exists

---

## 🧱 Simple Example: Payment API with Idempotency Key

```http
POST /payments
Idempotency-Key: payment-abc-uuid
Body: { amount: 100, to: "xyz" }
```

### Backend flow:

1. Check if `payment-abc-uuid` exists in `idempotency_keys` table.
2. If found, return previous result.
3. Else:

    * Begin transaction.
    * Process payment.
    * Save result with idempotency key.
    * Commit and return response.

---

## 🧠 Important Considerations

| Factor           | Explanation                                                         |
| ---------------- | ------------------------------------------------------------------- |
| **Storage**      | Store idempotency keys in a persistent store (e.g., DB, Redis).     |
| **TTL**          | Set expiry (e.g., 24h) for idempotency keys to avoid memory bloat.  |
| **Uniqueness**   | Clients must generate a new UUID per intent.                        |
| **Side effects** | All downstream operations (DB, email, etc.) must honor idempotency. |

---

## 🚫 Common Mistakes

* Not saving side effects (e.g., DB writes, logs) under the same idempotency context.
* Using random IDs server-side and ignoring duplicate client requests.
* Not returning consistent responses on retries.

---

## ✅ Summary

| Concept      | Description                                   |
| ------------ | --------------------------------------------- |
| Idempotency  | Repeatable operation gives same result        |
| Enforce via  | Idempotency keys, database checks, UPSERT     |
| HTTP Methods | `GET`, `PUT`, `DELETE` → should be idempotent |
| When needed  | Payments, orders, emails, any write operation |

---

## 82. What is the role of an API Gateway?

An **API Gateway** is a crucial component in modern **microservices architecture**. It acts as a **single entry point** for all client requests and routes them to the appropriate backend services.

---

## ✅ Role of an API Gateway

### 1. **Request Routing**

* Routes incoming requests to the correct microservice.
* Acts like a **traffic cop**: `GET /users/123` → `User Service`, `POST /orders` → `Order Service`.

---

### 2. **Authentication and Authorization**

* Verifies user credentials (e.g., JWT token, OAuth2).
* Prevents unauthorized access before reaching internal services.

---

### 3. **Rate Limiting and Throttling**

* Protects backend services from overuse or abuse.
* E.g., limit `100 requests/minute` per IP or token.

---

### 4. **Load Balancing**

* Distributes incoming traffic across multiple instances of a service.
* Ensures high availability and scalability.

---

### 5. **Caching**

* Caches frequently requested responses (e.g., product listings).
* Reduces latency and load on backend services.

---

### 6. **Request/Response Transformation**

* Modifies headers, query params, or body formats.
* Example: converts XML → JSON or renames request fields.

---

### 7. **Logging and Monitoring**

* Logs request/response metadata for observability.
* Integrates with tools like ELK stack, Prometheus, Grafana.

---

### 8. **Security and SSL Termination**

* Acts as a centralized point for HTTPS.
* Removes SSL burden from downstream services.

---

### 9. **API Versioning and Documentation**

* Supports multiple API versions (e.g., `/v1`, `/v2`).
* Some gateways (e.g., Kong, Apigee) support auto-documentation and developer portals.

---

## 🖼️ High-Level Architecture

```
[ Client / Mobile App / Browser ]
               |
        [ API Gateway ]
        /      |       \
 [User Service][Order Service][Inventory Service]
```

---

## 🔧 Common API Gateway Tools

| Tool                            | Features                                       |
| ------------------------------- | ---------------------------------------------- |
| **Kong**                        | Open-source, plugins, scalable, Lua-based      |
| **Nginx**                       | Lightweight reverse proxy with gateway plugins |
| **AWS API Gateway**             | Fully managed, integrated with Lambda, IAM     |
| **Apigee**                      | Enterprise-grade, analytics, monetization      |
| **Zuul / Spring Cloud Gateway** | Java-based, great for Spring microservices     |

---

## 🧠 Example Use Case

A mobile app calls:

```http
POST /api/v1/orders
Authorization: Bearer <JWT>
```

The API Gateway:

1. Validates the JWT.
2. Logs the request.
3. Rate-limits based on the user.
4. Routes to `Order Service`.
5. Returns the response.

---

## ✅ Summary

| Role               | Purpose                                   |
| ------------------ | ----------------------------------------- |
| Single entry point | Simplifies client interactions            |
| Routing            | Forwards requests to appropriate services |
| Security           | Auth, SSL, rate-limiting                  |
| Monitoring         | Centralized logging and metrics           |
| Resilience         | Caching, retries, load balancing          |

---

## 83. What is the difference between orchestration and choreography in microservices?

In microservices architecture, **orchestration** and **choreography** are two distinct ways of coordinating interactions between services.

---

## 🔁 1. **Orchestration**

### ✅ Definition:

Orchestration means **centralized control** — a single service (called an orchestrator) controls and coordinates the interactions between other services.

### 🧠 Analogy:

Like a conductor in an orchestra who directs all instruments.

### 📌 Characteristics:

* A central orchestrator **invokes services** in a predefined sequence.
* Services are **passive** — they just respond to commands.
* Easier to manage complex workflows.
* Tightly coupled coordination logic.

### 📘 Example:

Imagine a **Travel Booking System**:

* Orchestrator (Booking Service) performs:

    1. Call Flight Service
    2. If successful, call Hotel Service
    3. If successful, call Payment Service
    4. Return confirmation

All steps are managed by the orchestrator.

### 🔧 Tools:

* **Camunda**, **Netflix Conductor**, **AWS Step Functions**, **Temporal**

---

## 🎭 2. **Choreography**

### ✅ Definition:

Choreography means **decentralized coordination** — each service knows when to act based on **events** it receives.

### 🧠 Analogy:

Like a dance, where each dancer (service) follows a common rhythm but **acts independently**.

### 📌 Characteristics:

* Services **emit and listen to events**.
* No central coordinator.
* Loosely coupled services.
* More scalable and flexible, but harder to debug.

### 📘 Example:

Same **Travel Booking System**, using events:

1. User triggers a booking → `BookingRequested` event.
2. Flight Service listens → books flight → emits `FlightBooked`.
3. Hotel Service listens to `FlightBooked` → books hotel → emits `HotelBooked`.
4. Payment Service listens to `HotelBooked` → charges → emits `PaymentCompleted`.

There’s **no central brain** — services react to events and trigger others.

### 🔧 Tools:

* **Apache Kafka**, **RabbitMQ**, **EventBridge**, **NATS**, **Axon**

---

## 🆚 Orchestration vs. Choreography

| Feature            | Orchestration                            | Choreography                          |
| ------------------ | ---------------------------------------- | ------------------------------------- |
| Coordination Style | Centralized                              | Decentralized                         |
| Control            | Orchestrator controls the flow           | Each service listens/reacts to events |
| Flexibility        | Less flexible (but more predictable)     | Highly flexible (but harder to trace) |
| Coupling           | More tightly coupled                     | Loosely coupled                       |
| Debugging          | Easier (single flow)                     | Harder (distributed event chains)     |
| Complexity         | Central logic grows as flow gets complex | Complexity spread across services     |
| Example Tools      | Camunda, Temporal, Step Functions        | Kafka, RabbitMQ, EventBridge          |

---

## 🏁 When to Use What?

| Use Orchestration When:                | Use Choreography When:                     |
| -------------------------------------- | ------------------------------------------ |
| You need clear workflow control        | You prefer autonomous services             |
| Centralized failure handling is needed | Event-driven architectures are ideal       |
| Easy debugging is a priority           | High scalability and loose coupling needed |
| You use workflow engines (e.g., BPMN)  | You use message/event brokers              |

---

## 84. What is a saga pattern and when is it useful?

The **Saga Pattern** is a design pattern used to manage **data consistency across multiple services** in **distributed systems**, especially when traditional database transactions (**ACID**) are not possible across microservices.

---

## 🧩 Why Saga Pattern?

In a **monolith**, we can use a **single database transaction**:

> "Book flight + reserve hotel + deduct payment" all succeed or all fail.

In **microservices**, each service has its **own database**, so **distributed transactions (2PC)** are often:

* Complex
* Slow
* Fragile

👉 That's where **Saga Pattern** helps — it replaces **distributed transactions** with a series of **local transactions** and **compensating actions**.

---

## ✅ What is the Saga Pattern?

A **Saga** is a sequence of **local transactions** in different services, where:

* Each step is a **local transaction**.
* If one step fails, the saga triggers **compensating transactions** to undo previous steps.

---

## 🧭 Two Types of Saga Patterns

### 1. **Choreography-Based Saga** (Decentralized)

* Services **listen to events** and **react**.
* No central coordinator.

#### Example:

1. `Order Service`: creates order → emits `OrderCreated`
2. `Inventory Service`: reserves stock → emits `InventoryReserved`
3. `Payment Service`: charges → emits `PaymentSuccessful`
4. If any step fails → emitting a `PaymentFailed` event causes `Inventory Service` and `Order Service` to compensate.

✅ **Simple, loosely coupled**
❌ Harder to track and debug flow

---

### 2. **Orchestration-Based Saga** (Centralized)

* A **central orchestrator** manages the saga and calls services.
* Services return success/failure.
* Orchestrator handles compensation.

#### Example:

1. Orchestrator: call `Order Service`
2. Then: call `Inventory Service`
3. Then: call `Payment Service`
4. On failure → orchestrator calls compensating methods in reverse

✅ **Easier to track and debug**
❌ Tighter coupling to the orchestrator

---

## 🏦 Real-World Use Case: Bank Transfer (Saga)

Transfer money from **Account A to Account B**:

### Saga steps:

1. Debit `Account A` (Service A)
2. Credit `Account B` (Service B)

### If credit fails:

* Saga calls a **compensating transaction** to refund `Account A`.

---

## 🔧 Example Implementation (Orchestration)

```java
// Orchestrator pseudo-code
startSaga() {
  try {
    orderService.createOrder();
    inventoryService.reserveStock();
    paymentService.chargeCustomer();
  } catch (Exception e) {
    paymentService.refund();
    inventoryService.releaseStock();
    orderService.cancelOrder();
  }
}
```

---

## 🔁 Compensating Transactions

Each service must implement **reverse logic** to undo its effect:

* Order → cancel order
* Inventory → release reserved items
* Payment → refund

---

## 📌 When to Use Saga Pattern?

Use it when:

* You need **eventual consistency** across services.
* You can't use distributed transactions (2PC is not feasible).
* Your system spans multiple **databases or services**.
* You can tolerate **temporary inconsistency**.

---

## ⚠️ Challenges

| Challenge              | Description                              |
| ---------------------- | ---------------------------------------- |
| Compensating logic     | Must be carefully designed               |
| Complex workflows      | Hard to scale with many steps            |
| Debugging event chains | Especially in choreography-based sagas   |
| Partial failures       | Need robust retry and timeout strategies |

---

## ✅ Summary

| Feature    | Saga Pattern                                         |
| ---------- | ---------------------------------------------------- |
| Purpose    | Manage transactions across microservices             |
| Key Ideas  | Local transactions + compensation                    |
| Types      | Choreography (event-driven), Orchestration (central) |
| Use When   | Distributed DBs, need for eventual consistency       |
| Benefits   | Avoids 2PC, better fault tolerance                   |
| Trade-offs | Complexity, requires compensation logic              |

---

## 85. How do you prevent cascading failures in distributed systems?

Preventing **cascading failures** in distributed systems is critical to building resilient, fault-tolerant architectures. A cascading failure occurs when a failure in one component causes a chain reaction that leads to system-wide outages.

---

## ✅ Common Techniques to Prevent Cascading Failures

---

### 1. **Circuit Breaker Pattern**

* Prevents a failing service from being bombarded with requests.
* Automatically “breaks the circuit” (blocks calls) if failures exceed a threshold.
* After a timeout, it allows a few test calls to check recovery.

#### 📘 Example:

```java
if (failureCount > threshold) {
   throw new CircuitBreakerOpenException();
}
```

**Tools**: Resilience4j, Hystrix (deprecated), Sentinel, Spring Cloud Circuit Breaker

---

### 2. **Timeouts and Retries**

* Set **reasonable timeouts** on all remote calls to avoid waiting indefinitely.
* Combine with **exponential backoff** and **jitter** for retries.

#### ✅ Good Practice:

```bash
Call payment service → timeout in 2s → retry 2 times with 2s, 4s delays
```

---

### 3. **Rate Limiting and Throttling**

* Protect services from being overwhelmed by too many requests.
* Can be applied per IP, user, or API token.

#### ✅ Use:

* Token bucket
* Leaky bucket
* Fixed window counters

---

### 4. **Bulkheads**

* Isolate parts of the system so failure in one does not bring down the rest.
* Like watertight compartments in a ship.

#### 📘 Example:

If the `Inventory Service` fails, ensure `Search Service` still runs.

**Implementation**: Use separate thread pools or containers per service type.

---

### 5. **Graceful Degradation / Fallbacks**

* Provide a degraded but functional response when a service is unavailable.

#### 📘 Example:

If the recommendation engine fails, show popular products instead.

---

### 6. **Health Checks and Auto-Healing**

* Use **liveness** and **readiness probes** to detect failing services.
* Auto-restart unhealthy instances using Kubernetes, ECS, etc.

---

### 7. **Load Shedding**

* Drop low-priority or excess requests when under pressure.
* Better to serve fewer users well than all users poorly.

---

### 8. **Service Isolation and Redundancy**

* Avoid tight coupling — one service’s failure should not directly affect others.
* Use redundant instances, replicas, or failover strategies.

---

### 9. **Backpressure Handling**

* In streaming or messaging systems (like Kafka), use **backpressure** to slow down producers when consumers lag.

---

### 10. **Observability and Alerting**

* Use logs, metrics, and distributed tracing to detect anomalies early.
* Set alerts to catch slowdowns or error spikes before they escalate.

---

## 🧠 Real-World Example

### E-commerce Checkout Flow:

* Services: Cart → Inventory → Payment → Order
* If `Payment Service` slows:

    * Circuit breaker opens after 5 failures.
    * Requests are rejected early.
    * Retry is enabled with backoff.
    * Order service uses fallback: place order on hold.

---

## ✅ Summary Table

| Technique              | Purpose                                  |
| ---------------------- | ---------------------------------------- |
| Circuit Breaker        | Stops repeated calls to failing services |
| Timeouts + Retries     | Prevents hangs, adds resilience          |
| Rate Limiting          | Prevents overload                        |
| Bulkheads              | Contain failures                         |
| Graceful Degradation   | Provide minimal service                  |
| Health Checks          | Restart unhealthy components             |
| Load Shedding          | Drop excess load to stay healthy         |
| Backpressure           | Balance producers and consumers          |
| Isolation & Redundancy | Avoid failure propagation                |

---

## 86. How would you design a zero-downtime deployment pipeline?

Designing a **zero-downtime deployment pipeline** ensures your application is updated without any interruption or downtime for users. This is crucial for highly available systems, especially in production environments where uptime is critical.

---

## Key Goals for Zero-Downtime Deployment:

* Users should **never experience service unavailability**.
* New version deploys **seamlessly without interrupting ongoing requests**.
* Rollback should be quick and safe if issues occur.
* Deployment should be **automated and repeatable**.

---

# How to Design a Zero-Downtime Deployment Pipeline

---

## 1. **Use Blue-Green or Canary Deployment Strategies**

### Blue-Green Deployment

* Maintain two identical environments: **Blue (current)** and **Green (new)**.
* Deploy new version to Green.
* Switch traffic from Blue to Green after testing.
* If Green has issues, switch back to Blue.

### Canary Deployment

* Deploy new version to a small subset of servers or users.
* Monitor system health and errors.
* Gradually increase traffic to new version.
* Rollback immediately if problems detected.

---

## 2. **Load Balancer with Health Checks**

* Use a load balancer (e.g., Nginx, HAProxy, AWS ELB) to route traffic.
* Health checks ensure only healthy instances receive traffic.
* During deployment, instances failing health checks are removed from the pool.

---

## 3. **Service Registry and Discovery**

* Register instances with service registry (e.g., Consul, Eureka).
* Deploy new instances, register them, then deregister old instances gracefully.
* Enables smooth traffic switching.

---

## 4. **Rolling Updates**

* Update instances **one by one** or in small batches.
* Old instances continue serving while new ones are deployed.
* Ensures some capacity is always available.

---

## 5. **Database Schema Migrations with Backward Compatibility**

* Deploy schema changes **without breaking** the old and new versions.
* Use techniques like:

    * Additive migrations (add columns, tables)
    * Avoid destructive changes until all versions use new schema
    * Use feature flags for new DB features

---

## 6. **Session Management**

* Use **stateless services** or **external session stores** (Redis, Memcached).
* Ensures that sessions persist across deployments.

---

## 7. **Automated Testing and Monitoring**

* Run integration, smoke, and canary tests on new versions.
* Monitor performance, errors, and user metrics continuously.

---

## 8. **Rollback Strategy**

* Automate rollback in case of deployment failures.
* Can be as simple as switching back load balancer target or redeploying previous version.

---

## Example Workflow of Zero-Downtime Deployment Pipeline

```plaintext
1. Build & Test new version
2. Deploy to Green environment or subset of servers (Canary)
3. Run smoke tests and health checks
4. Gradually shift traffic from Blue to Green / Canary to full
5. Monitor system health and logs
6. Deregister old instances from service registry/load balancer
7. If failure detected, rollback by switching traffic back
```

---

## Tools & Technologies Supporting Zero-Downtime Deployment

| Tool / Platform       | Use Case                         |
| --------------------- | -------------------------------- |
| Kubernetes            | Rolling updates, health checks   |
| AWS Elastic Beanstalk | Blue-green deployment            |
| Jenkins, GitLab CI/CD | Automate build and deployment    |
| Istio, Linkerd        | Service mesh for traffic routing |
| Spinnaker             | Deployment orchestration         |
| Terraform             | Infrastructure as code           |

---

## Summary

| Technique                         | Purpose                                      |
| --------------------------------- | -------------------------------------------- |
| Blue-Green Deployment             | Complete environment switch without downtime |
| Canary Deployment                 | Gradual rollout with monitoring              |
| Load Balancer & Health Checks     | Route traffic only to healthy instances      |
| Rolling Updates                   | Deploy instances incrementally               |
| Backward Compatible DB Migrations | Avoid breaking changes in DB schema          |
| Stateless Services                | Avoid session loss during deployment         |
| Automated Testing & Monitoring    | Ensure deployment quality & detect failures  |
| Rollback Strategy                 | Quickly revert to previous stable state      |

---

## 87. How do you handle monitoring and alerting in large-scale systems?

Handling **monitoring and alerting** in large-scale systems is crucial for maintaining system health, detecting issues early, and ensuring reliability. Here’s a detailed explanation with best practices and examples.

---

## 1. **Why Monitoring and Alerting?**

* Track system performance and resource usage.
* Detect failures, bottlenecks, and anomalies proactively.
* Understand system behavior and troubleshoot issues quickly.
* Ensure SLAs (Service Level Agreements) and SLOs (Service Level Objectives) are met.

---

## 2. **Key Components of Monitoring**

### a) **Metrics Collection**

* Quantitative measurements of system behavior.
* Examples: CPU usage, memory consumption, request latency, error rates, throughput.

### b) **Logs Aggregation**

* Detailed records of system events and transactions.
* Examples: Application logs, system logs, audit logs.

### c) **Distributed Tracing**

* Tracks requests as they travel through distributed microservices.
* Helps pinpoint latency or failure sources.

### d) **Health Checks**

* Regular checks (liveness, readiness) to verify service availability.

---

## 3. **Types of Metrics**

| Metric Type         | Example                                           |
| ------------------- | ------------------------------------------------- |
| System Metrics      | CPU, memory, disk, network IO                     |
| Application Metrics | Request rates, success/fail counts, queue lengths |
| Business Metrics    | Number of sign-ups, orders completed, revenue     |
| Custom Metrics      | Domain-specific data like cache hit rate          |

---

## 4. **Monitoring Tools**

* **Prometheus + Grafana**: Popular open-source metrics collection & visualization.
* **ELK Stack (Elasticsearch, Logstash, Kibana)**: For log aggregation and search.
* **Jaeger / Zipkin**: Distributed tracing.
* **Datadog, New Relic, Splunk**: Commercial monitoring platforms.
* **Cloud Provider Tools**: AWS CloudWatch, Google Cloud Monitoring.

---

## 5. **Alerting Best Practices**

### a) **Define Clear Alerting Rules**

* Based on thresholds or anomaly detection.
* Example: Alert if error rate > 5% for 5 minutes.

### b) **Severity Levels**

* Critical, warning, info.
* Helps prioritize response.

### c) **Avoid Alert Fatigue**

* Use aggregation, deduplication, and suppression.
* Alert only on actionable issues.

### d) **Use Multiple Channels**

* Email, SMS, PagerDuty, Slack, Opsgenie.

### e) **Runbooks and Automation**

* Provide steps to troubleshoot or auto-remediate.

---

## 6. **Monitoring Architecture in Large-Scale Systems**

```plaintext
[Applications / Services]
       ↓ (Metrics & Logs)
[Metrics Collection System (Prometheus)]
       ↓
[Storage & Aggregation]
       ↓
[Visualization (Grafana), Alert Manager]
       ↓
[Alert Delivery (PagerDuty, Slack)]
```

---

## 7. **Example: Monitoring a Microservices-based System**

* Each service exports Prometheus metrics endpoint.
* Central Prometheus server scrapes metrics periodically.
* Logs shipped via Fluentd/Logstash to Elasticsearch.
* Jaeger collects traces for latency analysis.
* Alerts configured on Prometheus Alertmanager.
* Critical alerts go to PagerDuty; non-critical to Slack.

---

## 8. **Additional Tips**

* Monitor **infrastructure** (VMs, containers) and **application-level** metrics.
* Use **synthetic monitoring**: simulate user actions to detect issues before real users.
* Track **SLOs and SLIs**: e.g., 99.9% uptime, request latency under 200ms.
* Use **correlation IDs** to connect logs, metrics, and traces.

---

## Summary

| Aspect              | Best Practice / Tool                     |
| ------------------- | ---------------------------------------- |
| Metrics Collection  | Prometheus, CloudWatch                   |
| Logs Aggregation    | ELK Stack, Splunk                        |
| Distributed Tracing | Jaeger, Zipkin                           |
| Alerting            | PagerDuty, Slack, Alertmanager           |
| Visualization       | Grafana                                  |
| Alert Design        | Thresholds, severity levels, avoid noise |
| Automation          | Runbooks, auto-remediation               |

---

## 88. What metrics would you track for health checks?

When designing **health checks** in a large-scale system, the goal is to track metrics that reliably indicate whether a service or component is functioning correctly and can serve traffic. Here’s a detailed explanation:

---

## Key Metrics to Track for Health Checks

### 1. **Liveness Metrics**

These tell if the service is **alive** (not crashed or hung).

* **Process status**: Is the process running?
* **Heartbeat**: Periodic signals to confirm the app is responsive.
* **Thread availability**: No deadlocks or thread starvation.
* **Memory usage**: Not exceeding thresholds that could cause crashes.
* **CPU utilization**: Avoid CPU exhaustion.

*Example*: Kubernetes liveness probe checks if an HTTP endpoint returns 200 OK.

---

### 2. **Readiness Metrics**

These indicate if the service is **ready to accept requests**.

* **Database connectivity**: Can the service reach its DB?
* **Cache connectivity**: Is Redis/Memcached reachable?
* **External dependencies**: Are required APIs/services available?
* **Configuration loaded**: Is the app fully configured?
* **Initialization complete**: Has startup finished?

*Example*: Kubernetes readiness probe ensures traffic is only sent when these checks pass.

---

### 3. **Error Rate**

* Number or percentage of failed requests in a recent time window.
* High error rates indicate degraded health.

---

### 4. **Latency / Response Time**

* Average or percentile (p95/p99) response times.
* Excessive latency may indicate underlying issues.

---

### 5. **Resource Availability**

* Disk space available (avoid disk full).
* Network availability / packet loss.

---

### 6. **Queue Length / Backlog**

* Length of request or job queues.
* Large backlogs may mean the service is overwhelmed.

---

### 7. **Custom Domain-specific Checks**

* For example, for an e-commerce service:

    * Is payment gateway integration healthy?
    * Are order processing workflows running?

---

## Example: Health Check Endpoint Response

```json
{
  "status": "healthy",
  "database": "connected",
  "cache": "connected",
  "errorRate": "0.5%",
  "latencyP95": "120ms",
  "diskSpace": "70% free",
  "queueLength": "5"
}
```

---

## Summary Table

| Metric          | Purpose                           | Example Check                  |
| --------------- | --------------------------------- | ------------------------------ |
| Process Alive   | Ensure service process is running | TCP port open, heartbeat       |
| DB Connectivity | Check DB connection health        | Query simple SELECT 1          |
| Cache Health    | Check cache availability          | Ping Redis or Memcached        |
| External APIs   | Verify dependencies               | Ping or health endpoint        |
| Error Rate      | Detect service degradation        | % errors > threshold           |
| Latency         | Detect slowness                   | p95 latency < target threshold |
| Disk Space      | Prevent disk full issues          | Available disk > 10%           |
| Queue Length    | Detect overload                   | Queue size < threshold         |

---

## 89. What is blue-green deployment and how is it implemented?

Here’s a detailed explanation of **Blue-Green Deployment** and how it’s implemented, especially in large-scale systems:

---

## What is Blue-Green Deployment?

**Blue-Green Deployment** is a deployment strategy designed to reduce downtime and risk by running two identical production environments called **Blue** and **Green**.

* **Blue environment**: The currently live/active production environment serving all user traffic.
* **Green environment**: The new version of the application that you want to deploy and test.

**Goal:** Switch traffic from Blue to Green only after you verify Green is working correctly, achieving **zero downtime** and an easy rollback path.

---

## How Does Blue-Green Deployment Work?

1. **Prepare the Green environment**: Deploy the new application version on the Green environment while Blue continues to serve live traffic.
2. **Test Green**: Perform smoke tests, integration tests, and user acceptance tests on Green to verify everything works.
3. **Switch Traffic**: Once confident, redirect incoming user traffic from Blue to Green — often done via load balancer or DNS update.
4. **Monitor Green**: Keep monitoring the Green environment for issues.
5. **Rollback (if needed)**: If issues arise, switch traffic back to Blue immediately.
6. **Cleanup**: After successful deployment and stability, Blue environment can be updated for the next release or kept as a backup.

---

## Benefits of Blue-Green Deployment

* **Zero downtime** during deployment.
* Easy and quick **rollback** to the previous version.
* Reduces deployment risk by allowing thorough testing before switching traffic.
* Can minimize user impact during upgrades.

---

## How to Implement Blue-Green Deployment

### 1. Infrastructure Setup

* Maintain **two identical environments** with the same setup (servers, database, configuration).
* Ensure the environments are isolated so Green can be updated without impacting Blue.

### 2. Traffic Switching

* Use a **load balancer** (e.g., AWS ELB, Nginx, HAProxy) or **DNS switch** to route user requests.
* Load balancer directs all traffic to Blue initially.
* After Green is ready, update load balancer rules or DNS to point to Green.

### 3. Database Considerations

* Database can be shared or duplicated.
* When shared, ensure schema changes are backward compatible.
* For complex migrations, use feature toggles or phased rollouts.

### 4. Automation & CI/CD Integration

* Automate deployment to Green environment using CI/CD pipelines.
* Automate health checks and smoke tests before switching traffic.
* Automate traffic switch process for fast rollback.

---

## Example Scenario (Simplified)

| Step | Action                                               |
| ---- | ---------------------------------------------------- |
| 1    | Blue environment runs v1.0 live in production        |
| 2    | Deploy v2.0 to Green environment                     |
| 3    | Run automated tests and manual verification on Green |
| 4    | Update load balancer to send 100% traffic to Green   |
| 5    | Monitor Green for issues                             |
| 6    | If problems, revert load balancer back to Blue       |

---

## Tools Supporting Blue-Green Deployment

* **Kubernetes**: Can manage multiple environments with services and selectors.
* **AWS Elastic Beanstalk**: Supports Blue-Green out of the box.
* **Spinnaker**: Multi-cloud continuous delivery platform with Blue-Green support.
* **HashiCorp Terraform**: Infrastructure as code to automate environment provisioning.

---

## Summary Table

| Aspect         | Description                               |
| -------------- | ----------------------------------------- |
| Environments   | Two identical environments (Blue & Green) |
| Deployment     | Deploy new version on Green               |
| Testing        | Test Green before switching traffic       |
| Traffic Switch | Load balancer or DNS switch               |
| Rollback       | Switch back to Blue if needed             |
| Use Cases      | Critical systems, zero downtime needs     |

---

## 90. How do you decide between SQL and NoSQL?

Deciding between **SQL** (relational) and **NoSQL** (non-relational) databases is fundamental in system design, as it impacts scalability, performance, and data consistency. Here’s a detailed explanation with factors to consider and examples.

---

## What Are SQL and NoSQL Databases?

* **SQL Databases**: Use structured schema, tables with rows and columns, and support ACID transactions. Examples: MySQL, PostgreSQL, Oracle, SQL Server.
* **NoSQL Databases**: Schema-less or flexible schema, various data models (key-value, document, column-family, graph), designed for scalability and flexibility. Examples: MongoDB (document), Cassandra (wide-column), Redis (key-value), Neo4j (graph).

---

## How to Decide Between SQL and NoSQL?

### 1. **Data Structure and Schema**

| Use SQL if:                          | Use NoSQL if:                                        |
| ------------------------------------ | ---------------------------------------------------- |
| Your data is highly structured       | Your data is unstructured or semi-structured         |
| Strong schema enforcement is needed  | Schema flexibility or frequent schema changes        |
| Complex relationships & joins needed | Relationships are simple or handled in the app layer |

---

### 2. **Consistency vs Availability**

| Use SQL if:                             | Use NoSQL if:                                  |
| --------------------------------------- | ---------------------------------------------- |
| Strong consistency (ACID) is critical   | Eventual consistency is acceptable             |
| Transactions and complex queries needed | High availability & partition tolerance needed |

---

### 3. **Scalability**

| Use SQL if:                          | Use NoSQL if:                                           |
| ------------------------------------ | ------------------------------------------------------- |
| Vertical scaling (scale-up) suffices | Need horizontal scaling (scale-out) across many servers |
| Moderate data volume                 | Massive data volume & distributed architecture          |

---

### 4. **Query Patterns**

| Use SQL if:                             | Use NoSQL if:                                                                |
| --------------------------------------- | ---------------------------------------------------------------------------- |
| Complex queries, joins, aggregations    | Simple lookups, key-based queries, or aggregate queries on denormalized data |
| Ad-hoc queries with flexible conditions | Queries optimized for predefined access patterns                             |

---

### 5. **Use Cases**

| SQL Database Use Cases                            | NoSQL Database Use Cases                |
| ------------------------------------------------- | --------------------------------------- |
| Banking, financial systems requiring transactions | Real-time analytics, IoT data ingestion |
| ERP, CRM with complex relational data             | Content management, social networks     |
| Data warehousing, reporting                       | Session stores, caching                 |

---

## Example Scenario

* **E-commerce application**:

    * Use **SQL** for order management, inventory where transactional integrity is crucial.
    * Use **NoSQL** for product catalogs, user sessions, and logs where schema flexibility and scalability matter.

---

## Summary Table

| Factor       | SQL Database               | NoSQL Database              |
| ------------ | -------------------------- | --------------------------- |
| Schema       | Fixed, structured          | Flexible, schema-less       |
| Transactions | Supports ACID              | Often eventual consistency  |
| Scalability  | Vertical scaling           | Horizontal scaling          |
| Querying     | Complex queries, joins     | Simple or aggregate queries |
| Use Cases    | Financial, enterprise apps | Big data, real-time apps    |

---

## 91. What are common security pitfalls in web system design?

Security is critical in web system design, and overlooking common pitfalls can lead to vulnerabilities and serious breaches. Here’s a detailed breakdown of the **common security pitfalls** in web system design, with explanations and examples:

---

## Common Security Pitfalls in Web System Design

### 1. **Improper Authentication & Authorization**

* Weak or missing authentication controls allow attackers to impersonate users.
* Lack of role-based access control (RBAC) or improper authorization checks can expose sensitive data or operations.

*Example*: Allowing users to access admin features without verifying roles.

---

### 2. **SQL Injection**

* Failing to sanitize or parameterize database queries lets attackers inject malicious SQL.

*Example*: Using user input directly in SQL queries without prepared statements.

---

### 3. **Cross-Site Scripting (XSS)**

* Allowing untrusted user input to be rendered in webpages without proper encoding leads to malicious scripts running in users’ browsers.

*Example*: A comment field accepting `<script>` tags that steal cookies.

---

### 4. **Cross-Site Request Forgery (CSRF)**

* Attacker tricks a logged-in user’s browser into submitting unwanted requests to the web app.

*Example*: A malicious webpage causing a user’s browser to transfer funds unknowingly.

---

### 5. **Insecure Direct Object References (IDOR)**

* Exposing internal object identifiers (like file names or user IDs) without access checks.

*Example*: Users manipulating URL parameters to access other users’ data.

---

### 6. **Lack of Encryption**

* Not using HTTPS or failing to encrypt sensitive data at rest and in transit.

*Example*: Sending passwords or session tokens over plain HTTP.

---

### 7. **Poor Session Management**

* Using predictable session IDs, not expiring sessions properly, or exposing session tokens in URLs.

*Example*: Session fixation attacks or session hijacking.

---

### 8. **Insufficient Logging and Monitoring**

* Not logging security-relevant events or failing to monitor them for suspicious activity.

*Example*: Missing alerts on multiple failed login attempts.

---

### 9. **Unvalidated Redirects and Forwards**

* Redirecting users to URLs based on untrusted input without validation, enabling phishing or open redirect attacks.

---

### 10. **Misconfigured Security Headers**

* Missing or misconfigured HTTP headers like Content Security Policy (CSP), X-Frame-Options, HSTS.

*Example*: Allowing clickjacking due to lack of X-Frame-Options.

---

### 11. **Using Outdated or Vulnerable Libraries**

* Including third-party dependencies with known vulnerabilities.

---

### 12. **Excessive Permissions**

* Giving services, databases, or users more permissions than necessary (principle of least privilege ignored).

---

## How to Mitigate These Pitfalls

* Implement **strong authentication** (multi-factor authentication, OAuth).
* Use **parameterized queries** or ORM to avoid SQL injection.
* Encode and sanitize all user inputs to prevent XSS.
* Use **CSRF tokens** and verify them on sensitive requests.
* Validate access controls on every resource access.
* Enforce **HTTPS everywhere** and encrypt sensitive data.
* Manage sessions securely (secure cookies, timeouts).
* Enable comprehensive logging and real-time monitoring.
* Validate and whitelist redirects.
* Set security headers properly.
* Keep dependencies updated and audit them.
* Apply the **principle of least privilege**.

---

## Summary Table

| Pitfall                  | Description                              | Mitigation                      |
| ------------------------ | ---------------------------------------- | ------------------------------- |
| Authentication flaws     | Weak login or access control             | Use MFA, RBAC, strong passwords |
| SQL Injection            | Malicious SQL via untrusted inputs       | Use prepared statements         |
| XSS                      | Injected scripts in pages                | Sanitize & encode user input    |
| CSRF                     | Unauthorized requests via user’s browser | Use CSRF tokens                 |
| IDOR                     | Unauthorized object access               | Validate access per resource    |
| No Encryption            | Data sent/stored in plaintext            | Use HTTPS & encryption          |
| Poor Session Management  | Session hijacking or fixation            | Secure, expire sessions         |
| Insufficient Logging     | Missed intrusion detection               | Implement logging & monitoring  |
| Open Redirects           | Redirects to malicious sites             | Validate redirect URLs          |
| Missing Security Headers | Lack of protective HTTP headers          | Set CSP, HSTS, X-Frame-Options  |
| Vulnerable Libraries     | Use of outdated components               | Regular vulnerability scanning  |
| Excessive Permissions    | Too many privileges                      | Apply least privilege principle |

---

## 92. What is JWT and how does it work?

Here’s a detailed explanation of **JWT (JSON Web Token)** and how it works, especially in the context of web authentication and authorization.

---

## What is JWT?

**JWT (JSON Web Token)** is a compact, URL-safe token format used to securely transmit information between parties as a JSON object. It’s widely used for **authentication** and **authorization** in web systems.

* JWTs are **self-contained tokens** that include claims (data) about a user or system.
* They are digitally signed to ensure integrity and authenticity.
* Can be used in stateless authentication systems, avoiding the need for server-side session storage.

---

## Structure of JWT

A JWT consists of **three parts** separated by dots (`.`):

```
header.payload.signature
```

1. **Header**
   Contains metadata about the token, such as:

    * Type of token (JWT)
    * Signing algorithm (e.g., HMAC SHA256)

   Example (JSON):

   ```json
   {
     "alg": "HS256",
     "typ": "JWT"
   }
   ```

2. **Payload**
   Contains the **claims** or the data you want to transmit, such as:

    * `sub` (subject, e.g., user ID)
    * `iat` (issued at timestamp)
    * `exp` (expiration time)
    * Custom claims (like roles, permissions)

   Example (JSON):

   ```json
   {
     "sub": "1234567890",
     "name": "John Doe",
     "admin": true,
     "iat": 1516239022
   }
   ```

3. **Signature**
   Created by encoding the header and payload, then signing them with a secret key or private key using the algorithm specified in the header.
   This ensures the token **has not been tampered** with.

---

## How JWT Works (Authentication Flow)

1. **User Login**: User sends login credentials to the server.
2. **Server Verification**: Server verifies credentials and generates a JWT with user info.
3. **Token Sent**: Server sends the JWT to the client (usually in the response body or HTTP-only cookie).
4. **Client Stores Token**: Client stores the JWT (localStorage, sessionStorage, or cookie).
5. **Client Sends Token**: On subsequent requests, client includes JWT in the HTTP header (usually `Authorization: Bearer <token>`).
6. **Server Validates Token**: Server verifies the signature and claims to authenticate the user.
7. **Access Granted/Denied**: If valid, the server processes the request; otherwise, it rejects it.

---

## Why Use JWT?

* **Stateless authentication**: No need for server-side session storage.
* **Scalable**: Easy to use across distributed systems and microservices.
* **Compact & URL-safe**: Suitable for web, mobile, and API clients.
* **Flexible**: Can include any user data or permissions as claims.

---

## Example JWT Token (Base64 encoded parts)

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
.
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiYWRtaW4iOnRydWV9
.
TJVA95OrM7E2cBab30RMHrHDcEfxjoYZgeFONFh7HgQ
```

---

## Security Considerations

* Always **sign** JWTs using strong algorithms and keep keys secret.
* Use **HTTPS** to protect tokens in transit.
* Set **expiration times** (`exp`) to limit token lifetime.
* Avoid storing sensitive information in the payload as it’s **not encrypted** (only base64 encoded).
* Consider using **refresh tokens** to issue new JWTs securely.

---

## 93. How would you design a multi-tenant architecture?

Designing a **multi-tenant architecture** means building a system that serves multiple independent tenants (clients, organizations, or users) from a **single instance** of the software, while isolating their data and configurations.

Here’s a detailed explanation and approach:

---

## What is Multi-Tenancy?

* **Multi-tenancy** means **multiple tenants share the same application instance**, infrastructure, and resources.
* Each tenant’s data and configurations are isolated and secure.
* Used in SaaS (Software as a Service) apps where many customers use the same software but have isolated environments.

---

## Key Design Goals in Multi-Tenant Architecture

* **Data Isolation**: Ensure tenant data privacy & security.
* **Scalability**: Support many tenants efficiently.
* **Customization**: Allow tenant-specific configurations.
* **Maintainability**: Manage and update system easily for all tenants.
* **Cost-efficiency**: Share infrastructure while avoiding duplication.

---

## Multi-Tenancy Models

### 1. **Database per Tenant**

* Each tenant has a separate database instance.
* Strong data isolation.
* Easier to backup/restore per tenant.
* More costly and complex to manage many databases.

**Use case**: High security or regulatory requirements.

---

### 2. **Schema per Tenant**

* One database, but separate schema per tenant.
* Moderate isolation.
* Easier management than database-per-tenant.
* Requires DBMS that supports multiple schemas (e.g., PostgreSQL).

---

### 3. **Shared Schema (Row-level Isolation)**

* All tenants share tables; tenant ID column partitions data.
* Most cost-effective and scalable.
* Requires strong application logic for tenant isolation.
* Risk of data leaks if tenant ID filtering is missed.

**Use case**: Many tenants, smaller data per tenant.

---

## Components of Multi-Tenant System Design

| Component                          | Considerations                                          |
| ---------------------------------- | ------------------------------------------------------- |
| **Tenant Identification**          | Detect tenant from login, domain, or request header.    |
| **Authentication & Authorization** | Per-tenant user management & access control.            |
| **Data Isolation**                 | Via DB model (per tenant, schema, or row-level).        |
| **Configuration Management**       | Tenant-specific settings stored and loaded dynamically. |
| **Resource Management & Scaling**  | Scale based on tenant usage, isolate heavy tenants.     |
| **Monitoring & Logging**           | Track tenant-specific logs and performance.             |
| **Deployment**                     | Single deployment or isolated deployment per tenant.    |

---

## Example Flow (Shared Schema Model)

1. User logs in with tenant-specific credentials.
2. System identifies tenant (e.g., subdomain: tenant1.app.com).
3. All DB queries filter data by tenant ID.
4. Application loads tenant-specific configurations.
5. User performs actions, limited to tenant’s data.

---

## Challenges & Solutions

| Challenge             | Solution                                                 |
| --------------------- | -------------------------------------------------------- |
| Data leakage risk     | Enforce strict tenant ID filtering everywhere            |
| Performance isolation | Use rate limiting, resource quotas per tenant            |
| Backup & restore      | Tenant-specific backups or snapshots                     |
| Customization support | Use feature flags or tenant-specific config              |
| Upgrades & migrations | Design zero-downtime, backward-compatible schema changes |

---

## Summary Table

| Model               | Isolation Level | Cost   | Complexity | Use Case                                     |
| ------------------- | --------------- | ------ | ---------- | -------------------------------------------- |
| Database per Tenant | High            | High   | High       | Regulated, sensitive data                    |
| Schema per Tenant   | Medium          | Medium | Medium     | Moderate tenant count, some isolation needed |
| Shared Schema       | Low (logical)   | Low    | Low        | Large tenant base, cost sensitive            |

---

## 94. What is an eventual consistency mechanism in DynamoDB?

Let me explain **eventual consistency in DynamoDB** in detail:

---

## What is Eventual Consistency?

**Eventual consistency** means that when data is updated in a distributed system, **all copies of that data will become consistent over time**, but not necessarily immediately after the update.

* Reads may return **stale data** temporarily.
* After some delay, all replicas converge to the latest value.
* This model offers **higher availability and performance** but trades off immediate consistency.

---

## Eventual Consistency in DynamoDB

Amazon DynamoDB is a fully managed NoSQL database designed for high availability and scalability.

* DynamoDB **replicates data across multiple Availability Zones (AZs)** within a region.
* To maximize read throughput and availability, DynamoDB supports two read consistency models:

    * **Eventually Consistent Reads** (default)
    * **Strongly Consistent Reads**

---

### How Eventual Consistency Works in DynamoDB

* When you perform a **write (PutItem, UpdateItem, DeleteItem)**, DynamoDB asynchronously replicates this write across multiple storage nodes (AZs).
* If you immediately read the data with **eventual consistency**, DynamoDB may return the **old value** from a replica that hasn’t yet received the update.
* Over a short period (usually milliseconds), replicas synchronize, and **all reads will reflect the latest write**.

---

### Why Use Eventual Consistency?

* **Higher read throughput**: Eventual consistency allows DynamoDB to serve reads from multiple replicas.
* **Lower latency**: Reads can be served faster because they don’t need to wait for synchronization.
* **Better availability**: System can continue serving reads even if some replicas are temporarily out of sync.

---

### When Not to Use Eventual Consistency?

* When your application requires **strong correctness guarantees**, e.g., bank transactions, inventory updates where reading stale data is unacceptable.
* For those scenarios, DynamoDB offers **strongly consistent reads**, which always return the latest committed data (but with potentially higher latency and lower availability).

---

## Example: Reading Data with Eventual Consistency

```python
import boto3

dynamodb = boto3.resource('dynamodb')
table = dynamodb.Table('MyTable')

# Eventually consistent read (default)
response = table.get_item(
    Key={'UserId': '123'}
)
item = response.get('Item')
```

* The data returned here might be slightly stale if a recent update hasn’t propagated yet.
* If you want strong consistency, specify `ConsistentRead=True`.

---

## Summary

| Consistency Model    | Description                         | Use Cases                     | Pros                          | Cons                           |
| -------------------- | ----------------------------------- | ----------------------------- | ----------------------------- | ------------------------------ |
| Eventual Consistency | Reads may return stale data briefly | High throughput, low latency  | Fast reads, high availability | Possible stale reads           |
| Strong Consistency   | Reads always reflect latest write   | Critical correctness required | Latest data guaranteed        | Higher latency, less available |

---

## 95. What are retry mechanisms and exponential backoff?

Here's a detailed explanation of **retry mechanisms** and **exponential backoff**, common concepts used in building resilient distributed systems.

---

## What Are Retry Mechanisms?

**Retry mechanisms** are strategies where a client or service automatically **retries a failed operation** (like a network request or a database call) instead of failing immediately. This is useful when failures are temporary, such as:

* Network glitches
* Temporary service unavailability
* Rate limiting or throttling

### Why Retry?

* Improve system robustness and fault tolerance.
* Handle transient errors gracefully.
* Avoid propagating failures to users or dependent services.

---

## How Do Retries Work?

* When an operation fails (e.g., a request times out or returns a 500 error), the system tries the operation again.
* Retries may be immediate or delayed.
* Usually, a **maximum retry count** is set to avoid infinite retries.
* Some retries use a **fixed delay** between attempts; others use more advanced timing strategies.

---

## What is Exponential Backoff?

**Exponential backoff** is a retry strategy where the delay between retries **increases exponentially** after each failed attempt.

### How it Works

* After the 1st failure: wait 2^0 = 1 unit time (e.g., 1 second)
* After the 2nd failure: wait 2^1 = 2 seconds
* After the 3rd failure: wait 2^2 = 4 seconds
* After the 4th failure: wait 2^3 = 8 seconds
* … and so on.

### Why Use Exponential Backoff?

* Avoid overwhelming the failing service with rapid retries (thundering herd problem).
* Give the system time to recover before retrying.
* Spread out retry attempts to reduce contention and improve overall system stability.

---

## Adding Jitter (Randomness)

* Sometimes **jitter** (a random variation) is added to the backoff time to prevent multiple clients from retrying simultaneously.
* For example, wait time = random between 0 and `2^retryCount` seconds.

---

## Simple Retry with Exponential Backoff (Pseudo-code)

```python
max_retries = 5
base_delay = 1  # seconds

for attempt in range(max_retries):
    try:
        perform_operation()
        break  # success, exit loop
    except TemporaryError:
        wait_time = base_delay * (2 ** attempt)
        wait_time += random_jitter()
        sleep(wait_time)
else:
    raise Exception("Operation failed after retries")
```

---

## Use Cases for Retry + Exponential Backoff

* API calls to external services prone to transient failures.
* Database connection retries.
* Message queue consumers failing to process messages temporarily.
* Network communications that might be unstable.

---

## Summary

| Concept             | Purpose                                           | Benefits                                   |
| ------------------- | ------------------------------------------------- | ------------------------------------------ |
| Retry Mechanism     | Automatically retry failed operations             | Handle transient errors gracefully         |
| Exponential Backoff | Increase wait time exponentially after each retry | Prevent overload, improve system stability |
| Jitter              | Add randomness to backoff interval                | Avoid synchronized retries causing spikes  |

---

## 96. How would you handle GDPR compliance in system design?

Handling **GDPR compliance** in system design is crucial for any application that processes personal data of individuals in the European Union. Here’s a detailed explanation on what GDPR is, key principles, and how to design systems that comply with it.

---

## What is GDPR?

**GDPR (General Data Protection Regulation)** is a European Union regulation that governs how personal data of EU citizens must be collected, processed, stored, and protected.

* Applies to any organization processing EU residents' data, regardless of location.
* Non-compliance can lead to heavy fines (up to 4% of annual global turnover).

---

## Key GDPR Principles Relevant to System Design

1. **Data Minimization**
   Only collect and store the minimum personal data necessary.

2. **Purpose Limitation**
   Use personal data only for the specific purposes stated to the user.

3. **Consent Management**
   Collect explicit, informed consent from users before processing their data.

4. **Right to Access & Portability**
   Users can request a copy of their data and receive it in a portable format.

5. **Right to Erasure ("Right to be Forgotten")**
   Users can request deletion of their personal data.

6. **Data Security & Confidentiality**
   Protect personal data against unauthorized access or breaches.

7. **Data Breach Notification**
   Notify authorities and affected users within 72 hours if a breach occurs.

8. **Accountability & Auditability**
   Maintain records of data processing activities and compliance measures.

---

## How to Handle GDPR in System Design

### 1. **Data Inventory & Classification**

* Identify what personal data you collect, where it is stored, and how it flows through the system.
* Classify data by sensitivity.

### 2. **Data Minimization & Purpose Specification**

* Design data collection forms and APIs to collect only necessary data.
* Enforce purpose constraints in your backend.

### 3. **Consent Management**

* Implement explicit consent capture with clear user interfaces.
* Store consent metadata (timestamp, scope).
* Allow users to withdraw consent easily.

### 4. **User Rights Management**

* **Data Access & Portability:** Provide APIs or portals for users to download their data in standard formats (JSON, CSV).
* **Data Erasure:** Design deletion workflows that permanently remove or anonymize user data from all systems, including backups.

### 5. **Data Security**

* Use encryption at rest and in transit.
* Implement strict access controls and audit logging.
* Regularly update and patch systems.

### 6. **Data Breach Handling**

* Implement monitoring to detect breaches.
* Have processes to report breaches within 72 hours.
* Notify impacted users promptly.

### 7. **Data Residency & Cross-Border Transfers**

* Store data in compliant geographic locations.
* Use compliant mechanisms for data transfer outside EU (e.g., Standard Contractual Clauses).

### 8. **Privacy by Design & Default**

* Embed privacy controls early in the design process.
* Default settings should be privacy-friendly.

---

## Example: User Data Flow with GDPR Compliance

1. User signs up → explicit consent recorded.
2. Data stored encrypted with tenant/owner metadata.
3. User requests data → system exports data report.
4. User requests deletion → system triggers workflow to erase data.
5. Access control checks on every data request.
6. Audit logs keep track of data access and modifications.

---

## Tech & Tools That Help With GDPR

* Encryption libraries (e.g., AWS KMS, HashiCorp Vault)
* Consent management platforms
* Data masking/anonymization tools
* Audit logging frameworks
* Identity and access management (IAM) solutions

---

## Summary Table

| GDPR Aspect         | Design Considerations                          |
| ------------------- | ---------------------------------------------- |
| Data Minimization   | Collect/store only necessary data              |
| Consent Management  | Capture, store, and manage user consents       |
| User Rights         | Support access, portability, and deletion      |
| Security            | Encrypt data, control access, monitor breaches |
| Compliance Auditing | Keep detailed logs and processing records      |

---

## 97. What is a content delivery network (CDN) and how does it reduce latency?

Here's a detailed explanation of **Content Delivery Network (CDN)** and how it helps reduce latency:

---

## What is a Content Delivery Network (CDN)?

A **Content Delivery Network (CDN)** is a geographically distributed network of servers designed to deliver web content (like images, videos, scripts, stylesheets, and even dynamic content) to users **efficiently and quickly**.

* CDNs cache copies of your website’s static assets at multiple locations worldwide called **edge servers** or **PoPs (Points of Presence)**.
* When a user requests content, it is served from the nearest edge server rather than the origin server.

---

## How Does a CDN Work?

1. **Content Replication:** The CDN provider caches your website's static content across multiple edge servers around the globe.
2. **User Request Routing:** When a user visits your site, their request is automatically routed to the nearest CDN edge server based on proximity, network conditions, and load.
3. **Serving Cached Content:** The edge server delivers cached content immediately if available.
4. **Origin Fetching (if needed):** If the edge server does not have the requested content, it fetches it from the origin server, caches it, and then serves the user.
5. **Content Refresh:** Cached content is refreshed or invalidated periodically to keep it up to date.

---

## How Does a CDN Reduce Latency?

Latency is the delay between a user's request and the response. CDNs reduce latency by:

### 1. **Geographical Proximity**

* Serving content from edge servers close to the user minimizes the physical distance data must travel.
* This reduces the round-trip time (RTT), which is a big factor in latency.

### 2. **Reduced Network Hops**

* By caching content closer, the request bypasses multiple network routers and intermediary servers, reducing delays.

### 3. **Optimized Routing**

* CDNs use intelligent routing algorithms to pick the fastest and least congested path for delivering content.

### 4. **Load Distribution**

* CDNs spread traffic across multiple edge servers, preventing overload on the origin server and avoiding bottlenecks.

### 5. **TCP/HTTP Optimization**

* CDNs often use optimizations like TCP connection reuse, HTTP/2 multiplexing, and compression to speed up content delivery.

---

## Additional Benefits of CDNs

* **Improved Availability & Scalability:** Absorbs traffic spikes and DDoS attacks.
* **Bandwidth Savings:** Origin servers serve fewer requests, reducing bandwidth cost.
* **Security:** Many CDNs provide SSL/TLS, Web Application Firewall (WAF), and bot mitigation.

---

## Real-world Example

Say a user in Tokyo requests an image hosted on a server in New York.

* Without CDN: Request goes all the way to New York and back, causing higher latency (\~200+ ms).
* With CDN: Request is served from the nearest Tokyo edge server, reducing latency to a few milliseconds.

---

## Summary Table

| Aspect                  | Without CDN                  | With CDN                     |
| ----------------------- | ---------------------------- | ---------------------------- |
| Content Source          | Origin server (far away)     | Nearest edge server (close)  |
| Latency                 | High (long network distance) | Low (short distance)         |
| Server Load             | High on origin server        | Distributed across CDN nodes |
| Handling Traffic Spikes | Difficult                    | More resilient and scalable  |

---

## 98. How would you design a search auto-suggestion system?

Designing a **search auto-suggestion system** (like Google’s search box suggestions) is a common system design interview question. Here's a detailed breakdown of how to approach it:

---

## Requirements

**Functional:**

* Given a user’s input prefix, return a list of relevant search suggestions.
* Suggestions update as the user types (real-time or near real-time).
* Support a large volume of queries and users.
* Suggestions can be personalized or global/popular.

**Non-functional:**

* Low latency (sub-100ms response).
* High availability.
* Scalability to millions of users.
* Efficient storage and retrieval.

---

## High-Level Approach

1. **Data Sources for Suggestions:**

    * Popular search queries (aggregated from logs).
    * Personalized suggestions (based on user’s history).
    * Trending queries (recent spikes).
    * Dictionary or static autocomplete dataset.

2. **Core Functionality:**

    * Efficiently find all suggestions matching the input prefix.
    * Rank suggestions by relevance, popularity, recency, or personalization.

---

## Key Components

### 1. **Frontend**

* Captures user input dynamically.
* Sends prefix queries to backend with every keystroke (debounced to reduce load).
* Displays ranked suggestions.

### 2. **API Layer**

* Receives prefix requests.
* Queries suggestion data stores.
* Returns ranked suggestions.

### 3. **Data Storage / Indexing**

* Stores search terms and metadata (popularity, timestamps).
* Supports fast prefix lookup.

Possible data structures:

* **Trie (Prefix Tree):**
  Efficient prefix lookup, but expensive to maintain for huge datasets.

* **Inverted Index:**
  Used by search engines, maps prefixes to candidate suggestions.

* **Sorted Key-Value Store:**
  Use key-value stores (like Redis, Cassandra) with lexicographical ordering for prefix scans.

* **ElasticSearch or Solr:**
  Full-text search engines with autocomplete features.

### 4. **Ranking Engine**

* Rank results based on:

    * Popularity (click-through rate, frequency).
    * Freshness (trending topics).
    * Personalization (user profile, past searches).
* May use machine learning models.

### 5. **Data Pipeline**

* Ingest user search logs.
* Aggregate and update popularity scores periodically.
* Update indexes and caches.

---

## Workflow

1. User types prefix `"micr"`.
2. Frontend sends `micr` to API.
3. API queries the autocomplete index for keys starting with `"micr"`.
4. Retrieves candidate suggestions like `"microsoft"`, `"microeconomics"`, `"microphone"`.
5. Ranking engine orders suggestions based on scores.
6. API returns top N suggestions to the frontend.

---

## Scalability Considerations

* **Caching:** Cache popular prefixes to reduce load.
* **Sharding:** Partition index by prefix ranges or hash.
* **Asynchronous Updates:** Update indexes asynchronously to handle new trends.
* **Load Balancing:** Distribute user requests across multiple servers.
* **Rate Limiting & Debouncing:** Prevent overload from too many keystrokes.

---

## Example Data Structure: Trie with Scores

```text
          root
          /  \
         m    t
         |    |
         i    ...
         |
         c
         |
         r (microsoft: 1000, microphone: 500)
```

* Each node stores a map of next characters.
* Leaf or intermediate nodes hold a list of top suggestions with their scores.

---

## Example Tech Stack

* **Frontend:** React + debounce logic
* **API:** REST/GraphQL service
* **Storage:** Redis (for fast in-memory prefix lookup), ElasticSearch (for advanced search & ranking)
* **Data Pipeline:** Kafka + Spark for log processing & aggregation

---

## Summary Table

| Component      | Purpose                            | Technologies                    |
| -------------- | ---------------------------------- | ------------------------------- |
| Frontend       | Capture input and show suggestions | JavaScript frameworks           |
| API Layer      | Serve autocomplete requests        | Node.js, Python, Java           |
| Data Storage   | Store & index suggestions          | Redis, ElasticSearch, Cassandra |
| Ranking Engine | Rank suggestions                   | Custom logic, ML models         |
| Data Pipeline  | Process logs & update data         | Kafka, Spark, Hadoop            |

---

## 99. How do you handle schema changes in microservices?

Handling schema changes in microservices is a critical aspect of maintaining system stability and enabling continuous delivery. Here's a detailed explanation with strategies and examples:

---

## What is the Problem?

* Each microservice typically owns its own database/schema.
* Schema changes (like adding/removing columns, changing data types) can impact the service itself and services it interacts with.
* Changes must be handled carefully to avoid breaking existing consumers or data loss.

---

## Key Challenges

* Schema changes need to be **backward and forward compatible**.
* Multiple versions of a microservice may coexist during deployments.
* Coordination among teams/services if data is shared or exchanged.

---

## Best Practices and Strategies to Handle Schema Changes

### 1. **Backward and Forward Compatibility**

* **Backward compatible:** New version can read old data and handle missing fields gracefully.
* **Forward compatible:** Older versions can ignore new fields added by the new schema.

**Example:**
If you add a new optional column to a table, old versions ignoring that column should still work.

---

### 2. **Use Schema Versioning**

* Keep track of schema versions.
* Use versioned APIs or message formats.
* Consumers specify or negotiate schema versions.

---

### 3. **Make Additive Changes**

* Prefer additive changes like adding new columns or tables.
* Avoid destructive changes (dropping columns) until all consumers migrate.

---

### 4. **Use Feature Toggles**

* Roll out schema changes with feature toggles.
* Gradually enable new features that depend on schema changes.

---

### 5. **Database Migration Tools**

* Use tools like **Flyway**, **Liquibase**, or built-in migration frameworks.
* Apply incremental migrations and keep migration scripts version-controlled.
* Migrations should be automated and reversible.

---

### 6. **Event-Driven Schema Evolution**

* If using event-driven architecture (Kafka, RabbitMQ), use schema registries (like **Confluent Schema Registry**) with formats like Avro or Protobuf.
* Evolve schemas with compatibility settings (backward/forward/full compatibility).

---

### 7. **Dual Writes / Read from Multiple Schemas**

* Temporarily support both old and new schemas during migration.
* Example: Write to both old and new schema versions; read prefers the new.

---

### 8. **Consumer-Driven Contracts**

* Use contract testing to ensure services correctly handle schema changes.
* Update consumer contracts before changing producer schemas.

---

### 9. **Graceful Deprecation**

* Communicate and coordinate schema deprecations.
* Provide timelines for consumers to migrate.
* Remove old schema parts only after consumers have migrated.

---

## Example Scenario

You want to add a new field `middleName` to the `User` service’s database.

**Step-by-step:**

1. **Add nullable `middleName` column** (additive, backward compatible).
2. **Deploy the service with code handling missing `middleName` gracefully.**
3. **Update client services to start sending and using `middleName`.**
4. **After all clients migrate, mark `middleName` as NOT NULL if desired.**
5. **Eventually clean up old code if any.**

---

## Summary Table

| Strategy                    | Description                                     | Example Tools/Techniques         |
| --------------------------- | ----------------------------------------------- | -------------------------------- |
| Additive changes            | Add columns, avoid dropping fields immediately  | Database migrations (Flyway)     |
| Schema versioning           | Maintain versioned APIs/schemas                 | API versioning, Avro schemas     |
| Backward/Forward compatible | Design changes that don’t break old/new clients | Optional fields, defaults        |
| Event-driven evolution      | Use schema registry for event formats           | Confluent Schema Registry (Avro) |
| Consumer contracts          | Use contract testing                            | Pact, Spring Cloud Contract      |
| Feature toggles             | Gradual rollout                                 | LaunchDarkly, custom toggles     |

---

## 100. How do you scale a system to handle 10 million users?

Scaling a system to handle **10 million users** is a classic system design challenge. Here’s a detailed breakdown of how to approach it, including architecture, components, and best practices:

---

## Key Goals When Scaling to Millions of Users

* **Performance:** Fast response times under high load.
* **Scalability:** Ability to grow horizontally and handle more users.
* **Availability:** System should be highly available with minimal downtime.
* **Maintainability:** Easy to monitor, upgrade, and debug.
* **Cost Efficiency:** Optimize resource usage.

---

## Step-by-Step Approach

### 1. **Understand User Behavior & Load Patterns**

* Peak traffic vs average traffic.
* Read-heavy or write-heavy system?
* Usage patterns (batch jobs, real-time, etc.)

---

### 2. **Use Distributed Architecture**

* **Microservices or modular components**: Decouple features to scale independently.
* Deploy services across multiple servers or containers.

---

### 3. **Load Balancing**

* Use load balancers (e.g., AWS ELB, NGINX, HAProxy) to distribute incoming requests evenly.
* Health checks to route traffic away from unhealthy nodes.

---

### 4. **Database Scaling**

* **Read Replicas:** Offload read traffic to replicas.
* **Sharding (Partitioning):** Split data horizontally across multiple database servers based on user ID or region.
* **Use NoSQL or NewSQL:** Depending on consistency and data model, consider scalable stores like Cassandra, DynamoDB, or Google Spanner.
* **Caching:** Use caches like Redis or Memcached for frequently accessed data.

---

### 5. **Caching Layer**

* Use multi-level caches:

    * Client-side cache (browser/localStorage).
    * CDN for static content.
    * Server-side in-memory cache (Redis/Memcached).
* Cache database query results and API responses.

---

### 6. **Asynchronous Processing**

* Use message queues (Kafka, RabbitMQ) for non-critical or batch tasks.
* Avoid blocking user requests with heavy processing.

---

### 7. **Use CDN for Static Content**

* Offload images, videos, scripts, CSS to CDN.
* Reduce latency and bandwidth on origin servers.

---

### 8. **Auto-Scaling**

* Automatically add/remove server instances based on load metrics (CPU, memory, request count).
* Use cloud services (AWS Auto Scaling, GCP Autoscaler).

---

### 9. **Monitoring & Alerting**

* Track key metrics: CPU, memory, response times, error rates, DB latency.
* Tools: Prometheus, Grafana, ELK stack, Datadog.

---

### 10. **Data Consistency & Partition Tolerance**

* Decide on consistency model (eventual vs strong consistency) based on use case.
* Use CQRS or Event Sourcing if complex workflows.

---

## Example Architecture for 10M Users

```
            Users
              |
          [DNS & CDN]
              |
        [Load Balancer]
         /            \
    [App Servers]   [App Servers] (auto-scaled)
         |               |
    [Cache Layer (Redis/Memcached)]
         |
    [Databases (Sharded + Replicated)]
         |
    [Message Queues / Async Workers]
```

---

## Additional Tips

* **Database connection pooling:** Optimize DB connections.
* **API Rate limiting:** Protect against abuse.
* **Use stateless services:** Easier to scale horizontally.
* **Graceful degradation:** Serve limited functionality under heavy load.

---

## Summary Table

| Aspect           | Approach/Tool                                        |
| ---------------- | ---------------------------------------------------- |
| Load Balancing   | NGINX, AWS ELB, HAProxy                              |
| Database Scaling | Read replicas, sharding, NoSQL (Cassandra, DynamoDB) |
| Caching          | Redis, Memcached, CDN                                |
| Async Processing | Kafka, RabbitMQ                                      |
| Auto-scaling     | AWS Auto Scaling, Kubernetes HPA                     |
| Monitoring       | Prometheus, Grafana, Datadog                         |

---