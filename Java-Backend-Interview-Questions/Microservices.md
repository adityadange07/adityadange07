## 311. What is microservices architecture?

**Answer:**
**Microservices Architecture** is an architectural style that structures an application as a collection of loose coupled services.
*   **Characteristics:**
    *   Highly maintainable and testable.
    *   Loosely coupled.
    *   Independently deployable.
    *   Organized around business capabilities.
    *   Owned by a small team.

---

## 312. Microservices vs monolith?

**Answer:**

| Feature | Monolith | Microservices |
| :--- | :--- | :--- |
| **Structure** | Single codebase, single deployment unit (WAR/JAR). | Multiple codebases, multiple deployment units. |
| **Scaling** | Scale the entire app (duplicate the whole server). | Scale individual services (only the busy ones). |
| **Complexity** | Simple to develop initially, hard to maintain as it grows. | Complex to manage (distributed system fallacies), easier to maintain per service. |
| **Technology** | Bound to one technology stack. | Polgyglot (can use different tech for different services). |

---

## 313. Advantages & disadvantages of microservices?

**Answer:**
*   **Advantages:**
    *   **Agility:** Faster deployment cycles.
    *   **Scalability:** Targeted scaling.
    *   **Resilience:** Failure in one service doesn't crash the whole system.
    *   **Freedom:** Freedom to choose technology.
*   **Disadvantages:**
    *   **Complexity:** Distributed systems are hard (Network latency, consistency, distributed transactions).
    *   **Operational Overhead:** Needs robust DevOps/Infrastructure (Docker, K8s).
    *   **Testing:** End-to-end testing is harder.

---

## 314. What is service discovery?

**Answer:**
**Service Discovery** is a mechanism that allows services to find each other dynamically without hardcoding IP addresses and ports.
*   **Problem:** In cloud environments, IP addresses change frequently (dynamic scaling).
*   **Solution:** Services register themselves with a "Registry" (Server). Clients ask the Registry for the address of a service.
*   **Tools:** Netflix Eureka, Consul, Zookeeper, Kubernetes (built-in).

---

## 315. What is Eureka?

**Answer:**
**Netflix Eureka** is a Service Registry (Discovery Server) from the Spring Cloud Netflix stack.
*   **Eureka Server:** The central registry where all services register.
*   **Eureka Client:** The microservices that register with the server and fetch the registry to find other services.
*   **Heartbeat:** Clients send heartbeats every 30s to renew their lease. If missing, they are evicted.

---

## 316. What is API Gateway?

**Answer:**
An **API Gateway** is a server that acts as a single entry point into the system.
*   **Role:** It routes requests to the appropriate backend microservice.
*   **Features:**
    *   **Routing:** (e.g., `/user/**` -> User Service).
    *   **Security:** Authentication/Authorization (OAuth2).
    *   **Rate Limiting:** Prevent abuse.
    *   **Monitoring/Logging:** Centralized traffic analysis.

---

## 317. What is Spring Cloud Gateway?

**Answer:**
**Spring Cloud Gateway** is the modern API Gateway built on Spring 5, Spring Boot 2, and Project Reactor (Non-blocking).
*   **Successor:** It replaced Netflix Zuul (Blocking).
*   **Components:**
    *   **Route:** Destination URI + Predicates.
    *   **Predicate:** Matches request (e.g., Path=/api/**, Header=X).
    *   **Filter:** Modifies request/response (e.g., AddHeader, StripPrefix).

---

## 318. What is load balancing?

**Answer:**
**Load Balancing** distributes incoming network traffic across multiple servers (instances of a microservice) to ensure no single server is overwhelmed.
*   **Server-Side LB:** Hardware/Nginx receives traffic and distributes it.
*   **Client-Side LB:** The **Client** (Microservice A) knows the list of available instances of Service B (from Discovery Service) and picks one itself.
    *   **Tool:** **Spring Cloud LoadBalancer** (Replaced Netflix Ribbon).

---

## 319. What is circuit breaker?

**Answer:**
**Circuit Breaker** is a pattern to prevent cascading failures.
*   **Concept:** If a service (Service B) is slow or down, the caller (Service A) should stop calling it ("Trip the circuit") and return a fallback response immediately, instead of waiting for a timeout.
*   **States:**
    *   **Closed:** Requests pass through (Happy path).
    *   **Open:** Requests fail fast (Fallback).
    *   **Half-Open:** Allow a few requests to check if the service recovered.

---

## 320. What is Resilience4j?

**Answer:**
**Resilience4j** is a lightweight fault tolerance library designed for Java 8 and functional programming.
*   **Successor:** It replaced Netflix Hystrix (Deprecated).
*   **Modules:**
    *   **CircuitBreaker:** Stop calls to failing services.
    *   **RateLimiter:** Limit number of requests.
    *   **Retry:** Automatic retries for transient failures.
    *   **Bulkhead:** Limit concurrent calls to a specific service.
    *   **TimeLimiter:** Timeout limits.

---

## 321. What is distributed configuration?

**Answer:**
**Distributed Configuration** is the practice of managing configuration properties (DB URLs, credentials, feature flags) for all microservices in a centralized place, rather than hardcoding them in each service's `application.properties`.
*   **Benefit:** Change configuration without redeploying the service.
*   **Security:** Secrets can be encrypted.

---

## 322. What is Spring Cloud Config?

**Answer:**
**Spring Cloud Config** provides server-side and client-side support for externalized configuration in a distributed system.
*   **Config Server:** A central place to manage external properties for applications across all environments. It usually builds on top of a **Git** repository.
*   **Config Client:** Microservices that connect to the Config Server on startup to fetch their configuration.

---

## 323. What is centralized logging?

**Answer:**
**Centralized Logging** aggregates logs from all microservices into a single location for searching and analysis.
*   **Problem:** In microservices, checking logs on 50 different servers via SSH is impossible.
*   **Stack:** **ELK Stack** (Elasticsearch, Logstash, Kibana) or **EFK Stack** (Elasticsearch, Fluentd, Kibana).

---

## 324. What is distributed tracing?

**Answer:**
**Distributed Tracing** is a method used to profile and monitor applications, especially those built using a microservices architecture.
*   **Goal:** To track a single request as it propagates across multiple services.
*   **Key Concepts:**
    *   **Trace ID:** Unique ID for the whole workflow.
    *   **Span ID:** Unique ID for a specific operation within a service.

---

## 325. What is Zipkin?

**Answer:**
**Zipkin** is a distributed tracing system.
*   **Purpose:** It helps gather timing data needed to troubleshoot latency problems in service architectures.
*   **UI:** Provides a dashboard to visualize the dependency graph and the timeline of a request trace.

---

## 326. What is Sleuth?

**Answer:**
**Spring Cloud Sleuth** implements a distributed tracing solution for Spring Cloud.
*   **Role:** It automatically adds **Trace ID** and **Span ID** to your logs (SLF4J/MDC).
*   **Integration:** It integrates with Zipkin to send traces for visualization.
*   **Note:** In Spring Boot 3, Sleuth is replaced by **Micrometer Tracing**.

---

## 327. What is observability?

**Answer:**
**Observability** is the measure of how well you can understand the internal states of a system from its external outputs.
*   **Three Pillars:**
    1.  **Logs:** (Discrete events) "What happened?"
    2.  **Metrics:** (Aggregatable data) "Is it healthy? What is the trend?" (Prometheus/Grafana).
    3.  **Traces:** (Request flow) "Where did it happen? How long did it take?"

---

## 328. What is health check?

**Answer:**
A **Health Check** is an endpoint (e.g., `/actuator/health`) that monitoring systems or load balancers ping to determine if an application instance is running and able to accept traffic.
*   **Status:** UP, DOWN, OUT_OF_SERVICE.

---

## 329. What is liveness vs readiness probe?

**Answer:**
Concepts used in **Kubernetes**:
*   **Liveness Probe:** "Is the container running?"
    *   If fails: Kubernetes **restarts** the container (assumes deadlock).
*   **Readiness Probe:** "Is the container ready to accept traffic?"
    *   If fails: Kubernetes **stops sending traffic** to this pod (removes from Load Balancer) until it passes. Usage: Waiting for DB connection or cache warming.

---

## 330. What is container orchestration?

**Answer:**
**Container Orchestration** automates the deployment, management, scaling, and networking of containers.
*   **Tool:** **Kubernetes (K8s)** is the industry standard.
*   **Responsibilities:**
    *   Provisioning and deployment.
    *   Scaling (up and down).
    *   Load balancing.
    *   Self-healing (restarting failed containers).

---

## 331. What is Saga pattern?

**Answer:**
**Saga Pattern** is a failure management pattern for distributed transactions.
*   **Problem:** ACID transactions don't span across multiple microservices (2PC is slow/complex).
*   **Solution:** A sequence of local transactions. Each local transaction updates the DB and publishes a message/event to trigger the next transaction.
*   **Compensation:** If a step fails, the Saga executes **compensating transactions** (undo operations) to reverse the changes made by previous steps.

---

## 332. Orchestration vs choreography?

**Answer:**
Two ways to implement Saga:
*   **Choreography (Decentralized):** Services exchange events without a central coordinator. Service A says "Order Created", Service B listens and does "Reserve Stock".
    *   *Pro:* Simple, loose coupling. *Con:* Hard to track complex flows.
*   **Orchestration (Centralized):** A central Orchestrator (service) tells participants what to do.
    *   *Pro:* Easy to manage/visualize. *Con:* Single point of failure/logic concentration.

---

## 333. What is eventual consistency?

**Answer:**
**Eventual Consistency** is a consistency model used in distributed systems (AP in CAP theorem).
*   **Concept:** Data is not immediately consistent across all nodes/services.
*   **Guarantee:** If no new updates are made, eventually all accesses will return the last updated value.
*   **Trade-off:** We accept temporary inconsistency for higher availability and partition tolerance.

---

## 334. What is idempotency?

**Answer:**
**Idempotency** means that making multiple identical requests has the same effect as making a single request.
*   **Context:** Crucial in microservices (retries due to network failure).
*   **Example:** `DELETE /user/1` is idempotent (result is "user deleted" whether called 1 or 10 times). `POST /user` is **not** idempotent (creates 10 users).
*   **Solution:** Use unique request IDs to de-duplicate operations.

---

## 335. What is API versioning?

**Answer:**
**API Versioning** allows you to alter the API logic/structure without breaking existing clients.
*   **Strategies:**
    1.  **URI Versioning:** `/api/v1/users` (Most common, clear).
    2.  **Header Versioning:** `Accept-Version: v1` (Clean URL, harder to test in browser).
    3.  **Media Type Versioning:** `Accept: application/vnd.company.v1+json`.

---

## 336. What is blue-green deployment?

**Answer:**
**Blue-Green Deployment** is a release strategy to reduce downtime and risk.
*   **Setup:** Two identical environments (Blue = Live, Green = Idle/Staging).
*   **Process:** Deploy new version to Green. Test it.
*   **Switch:** Switch the Load Balancer/Router to point traffic from Blue to Green.
*   **Rollback:** Switch back to Blue instantly if issues arise.

---

## 337. What is canary release?

**Answer:**
**Canary Release** is a technique to reduce the risk of introducing a new software version in production.
*   **Process:** Roll out the change to a **small subset of users** (e.g., 5%) first.
*   **Monitor:** Watch metrics (errors, latency).
*   **Propagate:** If successful, gradually increase traffic to 100%.

---

## 338. What is service mesh?

**Answer:**
**Service Mesh** is a dedicated infrastructure layer for handling service-to-service communication.
*   **Tool:** **Istio**, **Linkerd**.
*   **Features:** Traffic management, Security (mTLS), Observability (Tracing).
*   **Implementation:** Usually implemented as a lightweight network proxy (**Sidecar**) deployed alongside the application code.

---

## 339. What is sidecar pattern?

**Answer:**
**Sidecar Pattern** deploys components of an application into a separate process or container (Sidecar) to provide isolation and encapsulation.
*   **Analogy:** A motorcycle sidecar attached to the main bike.
*   **Usage:** Logging agents, Configuration proxies (Envoy), Service Mesh proxies. The main app focuses on business logic; the sidecar handles infrastructure concerns.

---

## 340. How do you secure microservices?

**Answer:**
**Security** in microservices involves multiple layers:
1.  **Edge Security:** API Gateway handles Authentication (OAuth2/OIDC) and acts as the entry point.
2.  **Service-to-Service:**
    *   **mTLS (Mutual TLS):** Encrypts traffic and verifies identity (Service Mesh).
    *   **Token Relay:** Pass the JWT token from the Gateway downstream to other services.
3.  **Network:** Private VPCs, firewalls.

---

## 341. How to handle distributed transactions?

**Answer:**
Handling distributed transactions (transactions spanning multiple services/DBs) is complex. Common strategies:
1.  **Saga Pattern (Preferred):** Sequence of local transactions with compensating actions.
2.  **Two-Phase Commit (2PC):** Strict consistency but poor performance/availability.
3.  **Eventual Consistency:** Accept that data might be out of sync for a few milliseconds, reconciling later via background processes.

---

## 342. What is 2PC?

**Answer:**
**Two-Phase Commit (2PC)** is a protocol for distributed transactions.
*   **Phase 1 (Prepare):** Identify a Coordinator. The Coordinator asks all participants: "Can you commit?". Participants lock resources and vote "Yes" or "No".
*   **Phase 2 (Commit/Rollback):**
    *   If all vote "Yes": Coordinator sends "Commit".
    *   If any vote "No": Coordinator sends "Rollback".

---

## 343. Why avoid 2PC in microservices?

**Answer:**
*   **Blocking:** It is a blocking protocol. If the Coordinator crashes during Phase 2, resources remain locked indefinitely.
*   **Performance:** High latency due to multiple round-trips and locking.
*   **Coupling:** Tightly couples services (they all must be up).
*   **CAP Theorem:** It favors Consistency over Availability, which contradicts the goal of highly available microservices.

---

## 344. What is bulkhead pattern?

**Answer:**
**Bulkhead Pattern** isolates elements of an application into pools so that if one fails, the others continue to function.
*   **Analogy:** A ship's hull is divided into bulkheads. If one section floods, the ship doesn't sink.
*   **Implementation:** Separate thread pools for different downstream services. If Service A is slow and exhausts its thread pool, Service B's thread pool remains unaffected.

---

## 345. What is retry pattern?

**Answer:**
**Retry Pattern** automatically retries a failed operation (hoping the failure was transient/temporary).
*   **Config:**
    *   **Max Attempts:** How many times to retry (e.g., 3).
    *   **Backoff:** How long to wait between retries (e.g., Fixed 1s, or Exponential).
*   **Caution:** Only retry **idempotent** operations. Avoid "Retry Storms" (DDoS-ing your own services).

---

## 346. What is timeout handling?

**Answer:**
**Timeout Handling** ensures that a request doesn't wait forever for a response.
*   **Reason:** Prevent threads from being blocked indefinitely by a slow dependency.
*   **Practice:** Always set a timeout (e.g., 2 seconds) for any external call (DB, HTTP). If the timeout is reached, abort and return a fast failure or fallback.

---

## 347. What is rate limiting?

**Answer:**
**Rate Limiting** controls the rate of traffic sent or received by a network interface controller.
*   **Purpose:** Protect services from being overwhelmed (DoS protection, fair usage policy).
*   **Algorithms:** Token Bucket, Leaky Bucket, Fixed Window.
*   **Tools:** Redis (distributed counter), Resilience4j, API Gateway.

---

## 348. How to handle database per service?

**Answer:**
**Database per Service** is a core microservice pattern where each service has its *own* private database.
*   **Challenge:** Joining data across services.
*   **Solution:**
    *   **API Composition:** Calls Service A and Service B, then combines results in memory (API Gateway/BFF).
    *   **Data Replication (CQRS):** Service A publishes an event on update; Service B consumes it and updates a read-only local copy of A's data.

---

## 349. How to manage inter-service communication?

**Answer:**
1.  **Synchronous (REST/gRPC):** Simple, real-time query. Good for "Read" operations. Tightly coupled.
2.  **Asynchronous (Messaging - RabbitMQ/Kafka):** Decoupled, eventual consistency. Good for "Write" operations (e.g., "Order Placed" event).
3.  **Hybrid:** Use Sync for queries and Async for updates.

---

## 350. Common production issues in microservices?

**Answer:**
1.  **Network Latency:** Too many "chatty" calls.
2.  **Distributed Traceability:** Hard to debug issues spanning 5 services (needs Zipkin).
3.  **Configuration Drift:** Environments going out of sync (needs Spring Cloud Config).
4.  **Cascading Failures:** One service crashing causes others to crash (needs Circuit Breakers).
5.  **Data Consistency:** Maintaining integrity across databases.
