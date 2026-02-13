## 351. What is REST?

**Answer:**
**REST (Representational State Transfer)** is an architectural style for designing networked applications.
*   **Key Principles:**
    1.  **Client-Server:** Decoupled UI and data storage.
    2.  **Stateless:** No session data on server; every request must contain all info.
    3.  **Cacheable:** Responses must define themselves as cacheable or not.
    4.  **Uniform Interface:** Resources identified by URLs, manipulated by HTTP methods.
    5.  **Layered System:** Client doesn't know if it's connected to end server or load balancer.

---

## 352. REST vs SOAP?

**Answer:**

| Feature | REST | SOAP |
| :--- | :--- | :--- |
| **Protocol** | Architectural Style (uses HTTP). | Protocol. |
| **Format** | JSON, XML, Plain Text, HTML. | XML only. |
| **Performance** | Lightweight (JSON), caching support. | Heavyweight (XML envelope, parsing). |
| **Security** | HTTPS, OAuth2. | WS-Security (Built-in). |
| **Usage** | Web APIs, Mobile apps. | Enterprise, Banking, Legacy systems. |

---

## 353. What are HTTP methods?

**Answer:**
Common HTTP verbs used in REST:
1.  **GET:** Retrieve a resource (Safe, Cacheable).
2.  **POST:** Create a new resource (Not Idempotent).
3.  **PUT:** Update/Replace a resource (Idempotent).
4.  **PATCH:** Partial update of a resource.
5.  **DELETE:** Remove a resource (Idempotent).

---

## 354. What is idempotent method?

**Answer:**
An **Idempotent** HTTP method is one that can be called multiple times without changing the result beyond the initial application.
*   **Idempotent:** `GET`, `PUT`, `DELETE`, `HEAD`, `OPTIONS`.
    *   `DELETE /user/1`: First call deletes it. Second call returns 404 (or 200), but the server state (user is gone) remains the same.
*   **Not Idempotent:** `POST`.
    *   `POST /user`: Calling it twice creates two users.

---

## 355. What are HTTP status codes?

**Answer:**
*   **2xx (Success):**
    *   `200 OK`: Success.
    *   `201 Created`: Resource created (POST).
    *   `204 No Content`: Success but no body (DELETE/PUT).
*   **4xx (Client Error):**
    *   `400 Bad Request`: Invalid input.
    *   `401 Unauthorized`: Authentication missing.
    *   `403 Forbidden`: Authorization missing (Role).
    *   `404 Not Found`: Resource doesn't exist.
    *   `405 Method Not Allowed`: Wrong HTTP verb.
*   **5xx (Server Error):**
    *   `500 Internal Server Error`: Bug/Exception.
    *   `503 Service Unavailable`: Server overloaded/down.

---

## 356. What is statelessness?

**Answer:**
**Statelessness** means the server does **not** store any client context (Session) between requests.
*   **Mechanism:** Every request from the client must contain all the information necessary to understand and process the request (e.g., Auth Token in header).
*   **Benefit:** Allows the server to scale horizontally easily (any server can handle any request).

---

## 357. What is HATEOAS?

**Answer:**
**HATEOAS (Hypermedia As The Engine Of Application State)** is a constraint of REST.
*   **Concept:** The API response should include **links** to related actions/resources, guiding the client on "what to do next".
*   **Example:**
    ```json
    {
      "id": 1,
      "name": "John",
      "_links": {
        "self": { "href": "/users/1" },
        "orders": { "href": "/users/1/orders" }
      }
    }
    ```

---

## 358. What is content negotiation?

**Answer:**
**Content Negotiation** is the mechanism used for serving different representations of a resource at the same URI, so that the user agent can specify which is best suited for the user.
*   **Headers:**
    *   `Accept`: Client tells Server what format it wants (e.g., `application/json` or `application/xml`).
    *   `Content-Type`: Client tells Server what format it is sending.

---

## 359. What is API versioning strategies?

**Answer:**
Since APIs evolve, versioning is crucial to avoid breaking changes.
1.  **URI Versioning:** `/api/v1/products` (Easiest to read/cache).
2.  **Request Param:** `/api/products?version=1` (Avoids valid URI pollution).
3.  **Header Versioning:** `X-API-VERSION: 1` (Keeps URL clean).
4.  **Media Type (Content Negotiation):** `Accept: application/vnd.myapi.v1+json`.

---

## 360. What is OpenAPI/Swagger?

**Answer:**
**OpenAPI Specification (OAS)** is a standard for documenting REST APIs. **Swagger** is a set of tools implementing OAS.
*   **Purpose:**
    1.  **Documentation:** Generates interactive UI (`/swagger-ui.html`) to test endpoints.
    2.  **Code Gen:** Generate client SDKs from the YAML/JSON spec.
*   **Spring Boot:** Use `springdoc-openapi` library to automatically generate docs from code annotations.

---

## 361. What is synchronous communication?

**Answer:**
**Synchronous Communication** is when the client sends a request and **waits** (blocks) for the response from the service.
*   **Protocol:** HTTP/REST, gRPC.
*   **Pros:** Simple to understand, real-time consistency.
*   **Cons:** Blocking (resource waste), cascading failures if downstream is slow, tight coupling.

---

## 362. What is asynchronous communication?

**Answer:**
**Asynchronous Communication** is when the client sends a message and **does not wait** for an immediate response.
*   **Protocol:** AMQP (RabbitMQ), Kafka.
*   **Pros:** Non-blocking, decoupled, handles spikes (buffering), better resilience.
*   **Cons:** Complexity (eventual consistency), harder to debug.

---

## 363. REST vs gRPC?

**Answer:**
| Feature | REST | gRPC |
| :--- | :--- | :--- |
| **Protocol** | HTTP/1.1 (mostly). | HTTP/2 (Binary). |
| **Format** | JSON (Text). | Protocol Buffers (Binary). |
| **Performance** | Slower (parsing text). | Faster (compact binary, multiplexing). |
| **Streaming** | Limited (Server-Sent Events). | Full support (Bi-directional streaming). |
| **Usage** | Public APIs (Browser compatible). | Internal Microservices communication. |

---

## 364. What is Feign Client?

**Answer:**
**Spring Cloud OpenFeign** is a declarative REST client.
*   **How:** You define an interface and annotate it with `@FeignClient`. Spring generates the implementation at runtime.
*   **Benefit:** Removes boilerplate code required when using `RestTemplate`.
*   **Integration:** Integrates with Eureka (Load Balancing) and Resilience4j (Circuit Breaker).

---

## 365. What is RestTemplate?

**Answer:**
**RestTemplate** is a synchronous client to perform HTTP requests in Spring.
*   **Status:** In maintenance mode (deprecated features).
*   **Usage:**
    ```java
    String result = restTemplate.getForObject("http://user-service/users/1", String.class);
    ```

---

## 366. What is WebClient?

**Answer:**
**WebClient** is a reactive, non-blocking HTTP client introduced in Spring WebFlux.
*   **Features:** Supports both Sync and Async operations.
*   **Future:** It is the recommended replacement for `RestTemplate`.
*   **Usage:**
    ```java
    Mono<String> result = webClient.get().uri("/users/1").retrieve().bodyToMono(String.class);
    ```

---

## 367. What is connection timeout vs read timeout?

**Answer:**
*   **Connection Timeout:** The time limit to **establish a connection** (TCP handshake) with the server. If server is down/unreachable, this triggers.
*   **Read Timeout:** The time limit to **receive data** (the response) after the connection is established. If server is slow processing, this triggers.

---

## 368. What is retry mechanism?

**Answer:**
A **Retry Mechanism** re-executes a failed request automatically.
*   **Policies:**
    *   **Simple:** Retry 3 times.
    *   **Backoff:** Wait 1s, then 2s, then 4s (Exponential).
    *   **Jitter:** Add random delay to prevent "thundering herd" problem.
*   **Tools:** Spring Retry, Resilience4j.

---

## 369. What is idempotency key?

**Answer:**
An **Idempotency Key** is a unique value (UUID) sent in the HTTP Header (`Idempotency-Key`) by the client to ensure idempotency for non-idempotent operations (like POST).
*   **Flow:**
    1.  Client POSTs with `Key: 123`.
    2.  Server processes and saves result mapped to `123`.
    3.  Network fails. Client retries POST with `Key: 123`.
    4.  Server sees `123` is already processed. Returns cached result instead of creating duplicate.

---

## 370. What are common REST best practices?

**Answer:**
1.  **Nouns for Resources:** Use `/users`, not `/getUsers`.
2.  **Plural Nouns:** `/users/1` instead of `/user/1`.
3.  **HTTP Status Codes:** Use correct codes (201 Created, 400 Bad Request) instead of 200 for everything.
4.  **Versioning:** Always version your API (`/v1`).
5.  **Pagination:** Limit result sizes.
6.  **SSL:** Always use HTTPS.