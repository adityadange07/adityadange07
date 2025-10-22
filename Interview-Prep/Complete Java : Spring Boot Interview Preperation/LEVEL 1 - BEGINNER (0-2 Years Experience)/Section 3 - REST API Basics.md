# LEVEL 1: BEGINNER (0-2 Years Experience)

# REST API Basics

## 52. What is HTTP? Common HTTP methods?

### **52. What is HTTP and Common HTTP Methods**

---

### **🔹 1. What is HTTP?**

**HTTP (HyperText Transfer Protocol)** is a **protocol for communication between a client and a server** on the web.

* It is a **request-response protocol**:

  1. **Client** sends a request to the server.
  2. **Server** processes the request and sends a response back.

* **Stateless Protocol:** Each HTTP request is independent; the server does not retain any previous request information unless managed via sessions or cookies.

* **Port:** Default HTTP port is **80**, HTTPS port is **443** (secure).

---

### **🔹 2. Common HTTP Methods**

| Method      | Description                                                      | Idempotent?   | Typical Use Case                       |
| ----------- | ---------------------------------------------------------------- | ------------- | -------------------------------------- |
| **GET**     | Requests data from a server. Does **not modify** server state.   | ✅ Yes         | Fetch user info, list of products      |
| **POST**    | Submits data to a server to **create a new resource**.           | ❌ No          | Create new user, submit form           |
| **PUT**     | Updates an existing resource completely.                         | ✅ Yes         | Update user profile                    |
| **PATCH**   | Updates a resource **partially**.                                | ❌/✅ Partially | Update user email only                 |
| **DELETE**  | Deletes a resource on the server.                                | ✅ Yes         | Delete a user or record                |
| **HEAD**    | Similar to GET but **returns headers only**, no body.            | ✅ Yes         | Check if a resource exists or modified |
| **OPTIONS** | Returns **HTTP methods supported** by the server for a resource. | ✅ Yes         | Preflight request in CORS              |
| **TRACE**   | Echoes back the request for diagnostic purposes.                 | ✅ Yes         | Debugging                              |
| **CONNECT** | Establishes a tunnel to the server (often for HTTPS).            | ❌ No          | Proxy connection                       |

---

### **🔹 3. Example: HTTP Request & Response**

**GET Request (Client → Server):**

```
GET /users/1 HTTP/1.1
Host: example.com
```

**Response (Server → Client):**

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "Aditya",
  "email": "aditya@example.com"
}
```

---

### **🔹 4. Idempotency and Safety**

* **Idempotent Methods:** Repeating the request **has the same effect** (GET, PUT, DELETE).
* **Safe Methods:** Does **not modify** server state (GET, HEAD).
* **Non-Idempotent:** POST is **not idempotent**, repeating may create duplicate resources.

---

💡 **Interview Tip:**

> "HTTP is a stateless request-response protocol. GET, POST, PUT, DELETE, and PATCH are the most commonly used methods in REST APIs."

---

If you want, I can next explain **Difference between GET vs POST**, which is one of the most frequently asked follow-up questions in interviews.

Do you want me to cover that next?

---

## 53. What are HTTP status codes (200,404,500)?

### **53. What are HTTP Status Codes**

**HTTP Status Codes** are **standardized codes sent by the server in response to a client’s HTTP request**. They indicate **whether the request was successful, failed, or requires further action**.

* Sent as part of the **HTTP response**.
* Helps clients (browsers, apps, APIs) understand the **result of their request**.

---

### **🔹 1. Categories of HTTP Status Codes**

| Category          | Range   | Meaning                                                             |
| ----------------- | ------- | ------------------------------------------------------------------- |
| **Informational** | 100–199 | Request received, continuing process. Rarely used by clients.       |
| **Success**       | 200–299 | Request was successfully processed.                                 |
| **Redirection**   | 300–399 | Further action required (like redirecting).                         |
| **Client Error**  | 400–499 | Error caused by client request (invalid input, unauthorized, etc.). |
| **Server Error**  | 500–599 | Error on the server side while processing the request.              |

---

### **🔹 2. Common HTTP Status Codes**

| Code                          | Category     | Description                                             | Example Use                         |
| ----------------------------- | ------------ | ------------------------------------------------------- | ----------------------------------- |
| **200 OK**                    | Success      | Request succeeded, response contains requested data     | Fetching user info via GET          |
| **201 Created**               | Success      | Resource successfully created                           | Creating a new user via POST        |
| **204 No Content**            | Success      | Request succeeded, but no content to return             | Deleting a resource                 |
| **301 Moved Permanently**     | Redirection  | Resource permanently moved to new URL                   | URL redirection                     |
| **302 Found**                 | Redirection  | Resource temporarily available at another URL           | Temporary redirect                  |
| **400 Bad Request**           | Client Error | Server cannot process request due to invalid input      | Malformed JSON in POST request      |
| **401 Unauthorized**          | Client Error | Authentication required or failed                       | Accessing secured API without token |
| **403 Forbidden**             | Client Error | Client authenticated but not allowed to access resource | User role lacks permission          |
| **404 Not Found**             | Client Error | Requested resource does not exist                       | GET /users/999                      |
| **500 Internal Server Error** | Server Error | Generic server error                                    | Exception occurred in server code   |
| **502 Bad Gateway**           | Server Error | Invalid response from upstream server                   | Gateway/proxy issue                 |
| **503 Service Unavailable**   | Server Error | Server temporarily unable to handle request             | Maintenance or overload             |

---

### **🔹 3. Example: HTTP Response**

**Request:**

```
GET /users/1 HTTP/1.1
Host: example.com
```

**Response:**

```
HTTP/1.1 200 OK
Content-Type: application/json

{
  "id": 1,
  "name": "Aditya"
}
```

**If user not found:**

```
HTTP/1.1 404 Not Found
Content-Type: application/json

{
  "error": "User not found"
}
```

---

### **🔹 4. Importance in REST APIs**

* Communicate **success or failure** of operations.
* Allow **clients to handle responses appropriately**.
* Facilitate **debugging and monitoring**.

---

💡 **Interview Tip:**

> "HTTP status codes indicate the result of a request: 2xx for success, 3xx for redirection, 4xx for client errors, and 5xx for server errors. They are crucial for REST API communication."

---

If you want, I can next explain **Difference between 200, 201, 204, 400, 401, 403, 404, and 500**, which is commonly asked in interviews.

Do you want me to cover that next?

---

## 54. What is REST Api?

### **54. What is a REST API**

**REST (Representational State Transfer) API** is an **architectural style for designing networked applications**. It allows **clients to communicate with servers over HTTP** using **standard HTTP methods** to perform CRUD (Create, Read, Update, Delete) operations on resources.

> Simply: A **REST API exposes data and functionality** of a server to clients (web, mobile, or other services) in a **stateless and standardized way**.

---

### **🔹 1. Key Principles of REST**

1. **Stateless**

   * Each request from client contains all necessary information.
   * Server does not store client context between requests.

2. **Client-Server Architecture**

   * Separation of concerns:

     * Client handles UI and user experience.
     * Server handles data and business logic.

3. **Resources**

   * Everything is treated as a **resource**, identified by a **URI (Uniform Resource Identifier)**.
   * Example: `/users/1` represents a user resource with ID 1.

4. **Standard HTTP Methods**

   * **GET** – Retrieve a resource.
   * **POST** – Create a new resource.
   * **PUT** – Update an existing resource completely.
   * **PATCH** – Update an existing resource partially.
   * **DELETE** – Remove a resource.

5. **Representation of Resources**

   * Resources can be represented in **JSON, XML, or other formats**.
   * JSON is most commonly used in modern web APIs.

6. **Uniform Interface**

   * Standardized way to interact with resources using HTTP methods and URIs.

---

### **🔹 2. REST API Example**

#### **Endpoints for User Management**

| HTTP Method | URI        | Description                      |
| ----------- | ---------- | -------------------------------- |
| GET         | `/users`   | Get list of all users            |
| GET         | `/users/1` | Get user with ID 1               |
| POST        | `/users`   | Create a new user                |
| PUT         | `/users/1` | Update user with ID 1 completely |
| PATCH       | `/users/1` | Update user with ID 1 partially  |
| DELETE      | `/users/1` | Delete user with ID 1            |

#### **Example JSON Response**

```json
{
  "id": 1,
  "name": "Aditya",
  "email": "aditya@example.com"
}
```

---

### **🔹 3. Features of REST API**

* **Stateless communication** – Server doesn’t store session information.
* **Cacheable** – Responses can be cached to improve performance.
* **Layered system** – Can use intermediaries like proxies or gateways.
* **Scalable** – Works well for distributed systems and microservices.

---

### **🔹 4. Advantages**

1. **Simplicity** – Uses standard HTTP methods and URIs.
2. **Platform-independent** – Works across web, mobile, or desktop clients.
3. **Scalability** – Statelessness allows horizontal scaling.
4. **Interoperability** – JSON/XML formats make it easy to integrate.
5. **Flexible** – Can be used with any programming language.

---

💡 **Interview Tip:**

> "REST API is a stateless, HTTP-based service that exposes resources using URIs. It uses standard methods like GET, POST, PUT, PATCH, DELETE to perform CRUD operations and commonly returns data in JSON format."

---

If you want, I can next explain **Difference between REST and SOAP**, which is a commonly asked follow-up question in interviews.

Do you want me to cover that next?

---

## 55. What is JSON?

### **55. What is JSON**

**JSON (JavaScript Object Notation)** is a **lightweight data interchange format** that is **easy for humans to read and write**, and **easy for machines to parse and generate**.

It is widely used in **REST APIs** to **send and receive data between a client and a server**.

---

### **🔹 1. Key Characteristics**

1. **Text-based** – JSON is plain text.
2. **Language-independent** – Supported by almost all programming languages (Java, Python, JavaScript, C#, etc.).
3. **Lightweight** – Minimal syntax, easy to transmit over network.
4. **Structured Data** – Represents data as **objects (key-value pairs)** and **arrays**.

---

### **🔹 2. JSON Syntax Rules**

* Data is written as **key-value pairs**.
* Keys must be **strings in double quotes**.
* Values can be:

  * String: `"Aditya"`
  * Number: `25`
  * Boolean: `true` / `false`
  * Null: `null`
  * Array: `[1, 2, 3]`
  * Object: `{ "key": "value" }`

---

### **🔹 3. JSON Example**

```json
{
  "id": 1,
  "name": "Aditya",
  "email": "aditya@example.com",
  "roles": ["Admin", "User"],
  "active": true,
  "profile": {
    "age": 25,
    "city": "Nagpur"
  }
}
```

**Explanation:**

* `id`, `name`, `email` → key-value pairs
* `roles` → array of strings
* `active` → boolean
* `profile` → nested JSON object

---

### **🔹 4. JSON vs XML**

| Feature         | JSON                                       | XML                             |
| --------------- | ------------------------------------------ | ------------------------------- |
| **Syntax**      | Lightweight, less verbose                  | Verbose, uses tags              |
| **Readability** | Easy for humans                            | Less readable                   |
| **Data Types**  | Supports numbers, strings, arrays, objects | Everything is string by default |
| **Parsing**     | Faster and simpler                         | Slower and more complex         |
| **Common Use**  | REST APIs, JavaScript                      | SOAP APIs, configuration files  |

---

### **🔹 5. Advantages of JSON**

1. **Lightweight and fast** – Small size and simple structure.
2. **Human-readable** – Easy to understand and debug.
3. **Language-independent** – Can be parsed and generated by any language.
4. **Easy integration with REST APIs** – Most modern web services use JSON for data transfer.

---

💡 **Interview Tip:**

> "JSON is a lightweight, text-based format for exchanging data, widely used in REST APIs because it is human-readable, language-independent, and easy to parse."

---

If you want, I can next explain **Difference between JSON and XML**, which is commonly asked in interviews.

Do you want me to cover that next?

---

## 56. What is @RestController vs @Controller?

### **56. Difference Between `@RestController` and `@Controller` in Spring**

Both `@Controller` and `@RestController` are **annotations in Spring MVC** used to define controllers, but they **serve different purposes** depending on whether you are building a **web page** or a **REST API**.

---

### **🔹 1. `@Controller`**

* **Purpose:** Used to define a **Spring MVC controller** that handles **web requests and returns views** (like JSP, Thymeleaf).
* **Response Type:** Typically returns a **view name**, which is resolved by a **ViewResolver** to render HTML pages.
* **Requires `@ResponseBody`** if you want to return raw data (JSON/XML).

**Example: Returning a web page**

```java
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class WebController {

    @GetMapping("/welcome")
    public String welcomePage(Model model) {
        model.addAttribute("message", "Welcome to Spring MVC");
        return "welcome"; // Returns "welcome.html" or "welcome.jsp"
    }
}
```

**Example: Returning JSON with `@ResponseBody`**

```java
@GetMapping("/user")
@ResponseBody
public User getUser() {
    return new User(1, "Aditya");
}
```

---

### **🔹 2. `@RestController`**

* **Purpose:** Used to define a **RESTful controller** that **returns data directly** (JSON/XML) instead of a view.
* **Response Type:** Automatically serializes **Java objects to JSON or XML** and returns in HTTP response body.
* Combines **`@Controller` + `@ResponseBody`** automatically.

**Example: Returning JSON directly**

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class UserRestController {

    @GetMapping("/user")
    public User getUser() {
        return new User(1, "Aditya"); // Returned as JSON automatically
    }
}
```

**Output:**

```json
{
  "id": 1,
  "name": "Aditya"
}
```

---

### **🔹 3. Key Differences**

| Feature                   | @Controller                             | @RestController                     |
| ------------------------- | --------------------------------------- | ----------------------------------- |
| **Response**              | Returns a **view** (HTML/JSP/Thymeleaf) | Returns **data** (JSON/XML)         |
| **@ResponseBody needed?** | Yes, to return JSON                     | No, implicit                        |
| **Use case**              | Web applications rendering pages        | RESTful APIs / Microservices        |
| **Combination**           | Only controller logic                   | Controller + @ResponseBody behavior |

---

### **🔹 4. Summary**

* Use `@Controller` when building **traditional web apps** with UI views.
* Use `@RestController` when building **REST APIs** where the server returns **JSON/XML** directly.

---

💡 **Interview Tip:**

> "`@RestController` is essentially `@Controller` + `@ResponseBody`. Use `@RestController` for REST APIs, and `@Controller` for returning web pages."

---

If you want, I can next explain **Difference between @RequestMapping and @GetMapping/@PostMapping in Spring**, which is a commonly asked follow-up question.

Do you want me to cover that next?

---

## 57. What is the process of creating a REST API (with example)?

### **57. Process of Creating a REST API in Spring Boot (with Example)**

Creating a REST API in Spring Boot involves **defining resources, creating a controller, service, and repository layers**, and **mapping HTTP requests to methods**. Here’s a step-by-step guide with an example.

---

## **Step 1: Setup Spring Boot Project**

1. Use **Spring Initializr** ([https://start.spring.io/](https://start.spring.io/)) or IDE (IntelliJ/Eclipse).
2. Add dependencies:

   * `Spring Web` → For REST API
   * `Spring Data JPA` → For database access (optional)
   * `H2` / `MySQL` → Database (optional)

---

## **Step 2: Define the Entity (Model)**

Create a class representing a resource (e.g., User):

```java
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;

@Entity
public class User {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private String email;

    // Constructors
    public User() {}
    public User(String name, String email) {
        this.name = name;
        this.email = email;
    }

    // Getters and Setters
    public Long getId() { return id; }
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }
    public String getEmail() { return email; }
    public void setEmail(String email) { this.email = email; }
}
```

---

## **Step 3: Create Repository Layer**

Interface to interact with the database using Spring Data JPA:

```java
import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

@Repository
public interface UserRepository extends JpaRepository<User, Long> {
    // JpaRepository provides CRUD methods
}
```

---

## **Step 4: Create Service Layer (Optional but Recommended)**

Encapsulates business logic:

```java
import org.springframework.stereotype.Service;
import java.util.List;

@Service
public class UserService {

    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public List<User> getAllUsers() {
        return userRepository.findAll();
    }

    public User getUserById(Long id) {
        return userRepository.findById(id).orElse(null);
    }

    public User createUser(User user) {
        return userRepository.save(user);
    }

    public User updateUser(Long id, User userDetails) {
        User user = getUserById(id);
        if(user != null) {
            user.setName(userDetails.getName());
            user.setEmail(userDetails.getEmail());
            return userRepository.save(user);
        }
        return null;
    }

    public void deleteUser(Long id) {
        userRepository.deleteById(id);
    }
}
```

---

## **Step 5: Create REST Controller**

Maps HTTP requests to service methods:

```java
import org.springframework.web.bind.annotation.*;
import java.util.List;

@RestController
@RequestMapping("/api/users")
public class UserController {

    private final UserService userService;

    public UserController(UserService userService) {
        this.userService = userService;
    }

    // GET all users
    @GetMapping
    public List<User> getAllUsers() {
        return userService.getAllUsers();
    }

    // GET user by ID
    @GetMapping("/{id}")
    public User getUserById(@PathVariable Long id) {
        return userService.getUserById(id);
    }

    // POST create new user
    @PostMapping
    public User createUser(@RequestBody User user) {
        return userService.createUser(user);
    }

    // PUT update existing user
    @PutMapping("/{id}")
    public User updateUser(@PathVariable Long id, @RequestBody User user) {
        return userService.updateUser(id, user);
    }

    // DELETE user
    @DeleteMapping("/{id}")
    public void deleteUser(@PathVariable Long id) {
        userService.deleteUser(id);
    }
}
```

---

## **Step 6: Configure `application.properties`**

For example, using H2 in-memory database:

```properties
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.h2.console.enabled=true
spring.jpa.hibernate.ddl-auto=update
```

---

## **Step 7: Run the Application**

1. Run the Spring Boot application.
2. Access endpoints using tools like **Postman** or **curl**:

| HTTP Method | URL               | Description                 |
| ----------- | ----------------- | --------------------------- |
| GET         | `/api/users`      | Fetch all users             |
| GET         | `/api/users/{id}` | Fetch user by ID            |
| POST        | `/api/users`      | Create new user (JSON body) |
| PUT         | `/api/users/{id}` | Update existing user        |
| DELETE      | `/api/users/{id}` | Delete user                 |

---

### **🔹 Example JSON for POST /api/users**

```json
{
  "name": "Aditya",
  "email": "aditya@example.com"
}
```

**Response:**

```json
{
  "id": 1,
  "name": "Aditya",
  "email": "aditya@example.com"
}
```

---

### **Step 8: Testing**

* Use **Postman**, **Swagger**, or **curl** to test CRUD operations.
* Verify database entries using H2 console: `http://localhost:8080/h2-console`.

---

💡 **Interview Tip:**

> "Creating a REST API in Spring Boot involves defining a **model/entity**, creating a **repository** for database interaction, a **service layer** for business logic, and a **@RestController** to handle HTTP requests. Use `@GetMapping`, `@PostMapping`, `@PutMapping`, and `@DeleteMapping` to map endpoints."

---

If you want, I can next explain **How to handle exceptions in a Spring Boot REST API**, which is important for production-ready APIs.

Do you want me to cover that next?

---