# Microservices Interview Questions & Answers (Deep Dive)

## 1. What is Microservices Architecture?
**Deep Dive:**
It's an architectural style where an application is a suite of small services, each running in its own process and communicating with lightweight mechanisms (HTTP/Messaging).
**Key Characteristics (The 12-Factor App):**
- **Decentralized Data Management:** Database per service pattern. No huge shared schema.
- **Smart Endpoints, Dumb Pipes:** Bus (Kafka/RabbitMQ) doesn't contain logic; services do.
- **Infrastructure as Code:** Automated CI/CD.
- **Fail Fast:** Designed for failure (Resilience).

## 2. Microservices Communication Internals
**Synchronous (REST/Feign):**
- **Blocking:** Thread waits for response. Risk of Thread Pool exhaustion in high load.
- **Circuit Breaker:** Essential to prevent cascading failure.

**Asynchronous (Kafka/RabbitMQ):**
- **Event-Driven:** Service A publishes `OrderCreatedEvent`. Service B (Inventory) and C (Notification) consume it.
- **Pros:** Decoupling. Service A is fast. Service B/C can be down and process later.
- **Cons:** **Eventual Consistency**. Harder to debug.

## 3. Circuit Breaker (Resilience4j / Hystrix) Internals
**State Transitions:**
1.  **CLOSED (Success):** Standard state. Requests pass through.
    - *Metric:* Failure Rate (e.g., > 50% fails in last 100 calls).
2.  **OPEN (Fail):** If threshold reached, circuit opens. **All requests fail immediately** (Fail Fast) with a `CallNotPermittedException`. No load on failing service.
    - *Timer:* Stays open for `waitDurationInOpenState` (e.g., 60s).
3.  **HALF-OPEN (Probe):** After timer expires, allows a **limited number of requests** (e.g., 10) to pass.
    - If they succeed -> Switch to **CLOSED**.
    - If they fail -> Switch back to **OPEN**.

## 4. Saga Design Pattern (Distributed Transactions)
**Problem:** Service A (Order) commits. Service B (Payment) fails. How to rollback Service A?
**Solution: Saga**
1.  **Choreography (Events):**
    - Order Svc: Emits `OrderCreated`.
    - Payment Svc: Listens. Deducts money. Emits `PaymentProcessed`.
    - Inventory Svc: Listens to `PaymentProcessed`. Emits `InventoryReserved`.
    - *Rollback:* If Payment fails, it emits `PaymentFailed`. Order Svc listens to this and executes `CancelOrder` (Compensating Transaction).
    - *Pro:* Decentralized. *Con:* Cyclic dependencies, hard to visualize.
2.  **Orchestration (Command):**
    - **Orchestrator Service:** Talks to Order, then Payment, then Inventory.
    - If Payment fails, Orchestrator explicitly calls `Order.undo()`.
    - *Pro:* Central logic. Easier monitoring. *Con:* SPOF (Single Point of Failure) if not scaled.

## 5. Service Discovery (Eureka) Internals
- **Registration:** Client sends IP:Port to Server on startup.
- **Heartbeat:** Client sends pulse every 30s (`leaseRenewalInterval`).
- **Lease Expiration:** If no beat for 90s, Server evicts instance.
- **Self-Preservation Mode:** If Server fails to receive heartbeats from >85% of instances (network partition), it STOPs evicting instances to protect the registry. It assumes network issue, not instance crash.

## 6. Kafka Architecture Deep Dive
- **Topic Partitions:** A topic is split into partitions (`P0`, `P1`, `P2`).
- **Parallelism:** 1 Partition = 1 Consumer instance (in a group). 3 partitions = Max 3 Consumers reading in parallel.
- **Replication Factor:** Copies of data. Leader handles R/W. Followers just replicate.
- **ISR (In-Sync Replicas):** Replicas that are caught up with Leader. Only ISRs can become new Leader.
- **Ack Config:**
    - `ack=0`: Fire & forget (Fastest, High Data Loss).
    - `ack=1`: Leader received (Med speed, Low Loss).
    - `ack=all`: All ISRs received (Slowest, Zero Loss).

## 7. Configuration Management (Spring Cloud Config)
**Mechanism:**
1.  Push config change to Git.
2.  Webhook calls `/monitor` on Config Server (or use Spring Cloud Bus).
3.  Config Server triggers refresh event via Message Bus (RabbitMQ/Kafka).
4.  All Microservices listening to Bus receive event.
5.  Services refresh `@RefreshScope` beans without restart.

## 8. Idempotency Implementation
**Scenario:** Payment Service receives "Charge $10" message twice due to network retry.
**Solution:**
1.  Client sends `Idempotency-Key` (UUID).
2.  Service checks Distributed Lock (Redis) or DB Unique Constraint on `(transaction_id)`.
3.  If exists, return previous result. If not, process.

## 9. API Gateway (Rate Limiting)
**Token Bucket Algorithm:**
- User gets a bucket with N tokens (capacity).
- Tokens refill at rate R tokens/sec.
- Each request consumes 1 token.
- If bucket empty, reject request (429 Too Many Requests).
- Implemented in Redis + Lua script / Spring Cloud Gateway filters.

## 10. Contract Testing (Pact)
**Consumer-Driven Contract:**
- **Consumer** defines expectations (JSON schema, status code) -> Generates `.pact` file.
- **Provider** runs this pact file against its API in CI pipeline.
- If API breaks contract, Build Fails. Matches production traffic without spinning up full env.
