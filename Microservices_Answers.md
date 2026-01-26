# Microservices Interview Questions & Answers

## 1. What is Microservices Architecture? Pros and Cons vs Monolithic.
**Detailed Explanation**:
*   **Microservices Architecture**: A design approach where a single application is composed of many loosely coupled and independently deployable smaller services. Each service runs in its own process and communicates with lightweight mechanisms (HTTP/Messaging).
*   **Monolithic**: All modules (User, Product, Order) are bundled into a single deployable unit (e.g., one WAR file).
*   **Pros of Microservices**:
    1.  **Scalability**: Scale only the service that needs it (e.g., Scale 'Order Service' during Black Friday, leave 'User Service' alone).
    2.  **Technology Freedom**: Use Java for one service, Python for AI, Node.js for UI.
    3.  **Resilience**: Failure in one service doesn't crash the whole app.
    4.  **Deployment**: Faster, independent deployments.
*   **Cons**:
    1.  **Complexity**: Harder to develop, test, and monitor distributed systems.
    2.  **Data Integrity**: Hard to maintain ACID properties across databases (Distributed Transaction).
    3.  **Network Latency**: Communication over network is slower than in-memory calls.

---

## 2. How do Microservices communicate?
**Detailed Explanation**:
1.  **Synchronous (Blocking)**:
    *   **REST (HTTP)**: Most common. Service A calls Service B's API and waits for response.
    *   **Feign Client**: Declarative REST client in Spring Cloud to make calling APIs easier.
2.  **Asynchronous (Non-Blocking)**:
    *   **Message Broker (Kafka/RabbitMQ)**: Service A sends a message (Event) to a Queue/Topic. Service B picks it up later. Decoupled and high throughput.

**Example**:
```java
// Synchronous (Feign)
@FeignClient(name = "order-service")
public interface OrderClient {
    @GetMapping("/orders/{id}")
    OrderDTO getOrder(@PathVariable Long id);
}

// Asynchronous (Kafka)
kafkaTemplate.send("order-topic", new OrderEvent(id, "CREATED"));
```

---

## 3. API Gateway and its role.
**Detailed Explanation**: An entry point for all clients (Web, Mobile). It sits between the client and the backend microservices.
*   **Roles**:
    1.  **Routing**: Route request `/users` to User Service, `/orders` to Order Service.
    2.  **Authentication/Security**: Validate JWT token once here, instead of in every service.
    3.  **Rate Limiting**: Limit number of requests to prevent DDoS.
    4.  **Protocol Translation**: Convert HTTPS to internal gRPC/HTTP.
*   **Tools**: Spring Cloud Gateway, Netflix Zuul, Kong.

**Example**:
`Client -> API Gateway (Auth Check) -> Service A`

---

## 4. Service Discovery (Eureka)
**Detailed Explanation**: Pattern to locate network locations (IP & Port) of service instances dynamically.
*   **Eureka Server**: A phonebook (Registry). services register themselves here.
*   **Eureka Client**: Services (e.g., Order Service) that register with Eureka and query it to find other services (e.g., "Where is User Service?").
*   **Client-Side Load Balancing (Ribbon/LoadBalancer)**: The client (Order Service) gets a list of IPs for "User Service" from Eureka, picks one (Round Robin), and calls it.

**Example**:
1.  User Service starts -> Registers IP 10.0.0.1:8080 with Eureka.
2.  Order Service asks Eureka -> "Give me User Service".
3.  Eureka returns [10.0.0.1:8080].

---

## 5. What is a Circuit Breaker? (Resilience4j)
**Detailed Explanation**: A pattern to prevent cascading failures. If Service A relies on Service B, and Service B is down, Service A should stop calling it and fail fast instead of waiting and hanging threads.
*   **States**:
    1.  **Closed**: Normal. Requests flow through. Counts failures.
    2.  **Open**: Threshold reached (e.g., 50% fail). Request BLOCKED immediately. Fallback returned.
    3.  **Half-Open**: After a wait time, allow limited test requests. If successful -> Closed. If fail -> Open.

**Example**:
```java
@CircuitBreaker(name = "userService", fallbackMethod = "fallbackUser")
public String getUser(String id) {
    return restTemplate.getForObject("http://user-service/" + id, String.class);
}

// Fallback logic
public String fallbackUser(String id, Throwable t) {
    return "Default User (Service Unavailable)";
}
```

---

## 6. Fault Tolerance in Microservices.
**Detailed Explanation**: The ability of a system to continue operating properly in the event of the failure of some of its components.
*   **Strategies**:
    1.  **Circuit Breaker**: Stop calling failing services.
    2.  **Retry**: Retry transient failures (e.g., Network glitch).
    3.  **Fallback**: Return default cache/static data.
    4.  **Bulkhead**: Isolate resources (Thread pools) so one heavy service doesn't drain the whole system.
    5.  **Timeouts**: Never wait forever.

---

## 7. Saga Design Pattern (Choreography vs Orchestration)
**Detailed Explanation**: Solution for Distributed Transactions. Instead of one big transaction (ACID), it breaks it into a sequence of local transactions. If one fails, execute **Compensating Transactions** to undo changes.
1.  **Choreography (Event-based)**: Decentralized. Service A does work -> publishes Event -> Service B listens, does work -> publishes Event.
    *   *Pros*: Simple for few services.
    *   *Cons*: Confusing chain of events (spaghetti) for complex flows.
2.  **Orchestration (Command-based)**: Central Coordinator (Orchestrator). It calls Service A, then Service B, then Service C. If B fails, it tells A to undo.
    *   *Pros*: Easy to visualize and manage.

**Example**:
*Order Process*:
1. Stock Service: Reserve Stock (Commit).
2. Payment Service: Charge Card (Fail).
3. Saga: Call Stock Service -> Release Stock (Compensate).

---

## 8. Centralized Configuration (Spring Cloud Config)
**Detailed Explanation**: Managing properties for 50+ microservices in individual `application.properties` is a nightmare.
*   **Spring Cloud Config Server**: Stores configs for all services in a central Git repo.
*   **Mechanism**: Services point to Config Server URL. On startup, they fetch their specific config.
*   **Benefit**: Change config in Git -> Refresh services without redeploying code (`/actuator/refresh`).

---

## 9. Distributed Tracing (Zipkin, Sleuth)
**Detailed Explanation**:
*   **Problem**: A user request hits Gateway -> Service A -> Service B -> DB. If it's slow, where is the bottleneck? Logs are scattered.
*   **Spring Cloud Sleuth**: Assigns a unique **Trace ID** to the entire chain and a **Span ID** for each step. Adds these to logs.
*   **Zipkin**: A UI tool that collects these traces and visualizes the timeline/latency graph.

**Example**:
Log: `[OrderService, 5f4e3c, 1b2a3d] - Processing Order...`
(TraceID: 5f4e3c is same across User, Order, and Payment logs).

---

## 10. How to handle failures in Microservices?
**Detailed Explanation**: Combine multiple patterns:
1.  **Timeouts**: Fail fast if service responds slowly.
2.  **Retries**: Automatic retry for 503 errors.
3.  **Circuit Breakers**: Stop calls to dead services.
4.  **Dead Letter Queues (DLQ)**: Save failed messages for manual inspection.
5.  **Idempotency**: Ensure retries don’t duplicate data.
6.  **Monitoring/Alerting**: Prometheus/Grafana to detect issues early.

---

## 11. Kafka Architecture
**Detailed Explanation**: A distributed streaming platform.
*   **Producer**: Sends messages.
*   **Consumer**: Reads messages.
*   **Broker**: A Kafka server. A cluster has multiple brokers.
*   **Topic**: A category/feed name (like a table in DB).
*   **Partition**: Topics are split into partitions to allow parallel processing.
*   **Offset**: Unique ID of a message within a partition. Tracks progress.
*   **Consumer Group**: A group of consumers working together. Each partition is consumed by ONLY ONE consumer in a group (Parallelism).

---

## 12. Kafka vs RabbitMQ
**Detailed Explanation**:
*   **Kafka**:
    *   **Model**: Log-based (Store & Forward). Messages persist for retention period.
    *   **Pull-based**: Consumers pull data.
    *   **Throughput**: Extremely high (Millions/sec).
    *   **Use Case**: Event streaming, Logs, Big Data pipelines.
*   **RabbitMQ**:
    *   **Model**: Queue-based (Smart Broker, Dumb Consumer). Messages deleted after ack.
    *   **Push-based**: Pushes data to consumer.
    *   **Complexity**: Supports complex routing logic (Exchanges).
    *   **Use Case**: Transactional/Complex routing needs.

---

## 13. Handling Dead Letter Queues (DLQ)
**Detailed Explanation**: A queue where messages are sent if they cannot be processed successfully after max retries.
*   **Scenario**: Consumer tries to process Order JSON, but JSON is malformed. It will fail forever.
*   **Solution**: After 3 retires, move message to `order-topic-dlq`.
*   **Processing**: Developers inspect DLQ messages, fix the issue (bug or data), and replay them.

---

## 14. Idempotency in Consumers
**Detailed Explanation**: Ensuring that processing the same message twice has the same effect as processing it once.
*   **Why Needed**: Kafka guarantees "At Least Once" delivery. Duplicate messages *will* happen.
*   **Solution**: Track processed message IDs in a separate DB table.
    *   Step 1: check if `msg_id` exists in processed_table.
    *   Step 2: If yes, Ack and ignore.
    *   Step 3: If no, Process logic + Insert `msg_id`. (Do this in a Transaction).

---

## 15. Designing a resilient Microservices system.
**Detailed Explanation**:
1.  **Eliminate SPOF**: No Single Point of Failure. Replicate everything (multiple instances of services).
2.  **Graceful Degradation**: If Recommendations Service is down, show "Popular Items" instead of error page.
3.  **Rate Limiting**: Protect your services from spikes.
4.  **Asynchronous Communication**: Decouple critical paths.
5.  **Observability**: Centralized Logging (ELK) + Metrics.

---

## 16. Two-Phase Commit (2PC) vs Saga.
**Detailed Explanation**:
*   **2PC (Two-Phase Commit)**:
    *   Strict consistency (ACID).
    *   Lock resources in ALL databases until transaction finishes.
    *   **Not suitable for Microservices** because it blocks resources and is slow/fragile (Coordinator failure blocks everything).
*   **Saga**:
    *   Eventual consistency (BASE).
    *   No locking across services.
    *   Uses compensating actions for undo.
    *   **Preferred for Microservices**.

---

## 17. Security in Microservices (OAuth2, Keycloak)
**Detailed Explanation**:
*   **OAuth2 / OIDC**: Standard protocol for delegated authorization.
*   **Keycloak / Auth0**: Identity Provider (IdP). Manages Users, Roles, Logins.
*   **Flow**:
    1.  User logs in via Keycloak -> Gets **JWT (Access Token)**.
    2.  User calls API Gateway with Token.
    3.  Gateway validates signature.
    4.  Gateway forwards request + Token to Order Service.
    5.  Order Service calls Inventory Service (Propagates Token).
*   **JWT**: Contains User details (Claims) + Roles. Signed to prevent tampering.

---

## 18. Rate Limiting in Microservices.
**Detailed Explanation**: Limiting the number of requests a user/client can make in a given timeframe.
*   **Goal**: Prevent abuse (DDoS) and ensure fair usage.
*   **Algorithms**: Token Bucket, Leaky Bucket.
*   **Implementation**: Often done at **API Gateway** (e.g., using Redis to store counters).
*   **Response**: `429 Too Many Requests`.

---

## 19. Strategies for migrating Monolith to Microservices.
**Detailed Explanation**: Do NOT rewrite everything at once (Big Bang).
*   **Strangler Fig Pattern**:
    1.  Put a Gateway/Proxy in front of Monolith.
    2.  Identify one functionality (e.g., Search).
    3.  Build new Search Microservice.
    4.  Update Gateway to route Search traffic to new service.
    5.  Old Monolith search code becomes dead (Strangle it).
    6.  Repeat until Monolith is gone.

---

## 20. Contract Testing in Microservices.
**Detailed Explanation**:
*   **Problem**: Service A (Consumer) relies on Service B (Provider). If B changes API response field name, A breaks.
*   **Solution**: Contract Testing (Pact / Spring Cloud Contract).
    *   Service A defines a **Contract** ("I expect JSON with field `userId`").
    *   This contract is used to **automatically test** Service B during B's build process.
    *   If B changes `userId` to `id`, B's build fails. Prevents breaking changes before deployment.
