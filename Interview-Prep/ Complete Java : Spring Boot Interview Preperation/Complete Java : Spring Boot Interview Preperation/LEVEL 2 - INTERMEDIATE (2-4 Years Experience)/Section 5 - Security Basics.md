# LEVEL 2: INTERMEDIATE (2-4 Years Experience)

# Security Basics

## 142. What is Authentication vs Authorization?

### **Authentication vs Authorization**

These are **two fundamental concepts in security**, often used in web applications, APIs, and systems, but they serve **different purposes**.

---

## **1. Authentication**

* **Definition:** The process of **verifying the identity** of a user or system.
* **Purpose:** Ensures that the user is **who they claim to be**.
* **Typical Methods:**

  * Username and password
  * OTP (One-Time Password)
  * Biometric (fingerprint, face recognition)
  * Tokens (JWT, OAuth tokens)
* **Question Answered:** *“Who are you?”*

**Example:**

* User enters username and password → system checks credentials → grants access if valid.

---

## **2. Authorization**

* **Definition:** The process of **checking permissions** to access a resource or perform an action.
* **Purpose:** Determines **what the authenticated user is allowed to do**.
* **Typical Methods:**

  * Role-based access control (RBAC)
  * Attribute-based access control (ABAC)
  * Access control lists (ACLs)
* **Question Answered:** *“What can you do?”*

**Example:**

* User is authenticated → system checks role → allows reading a file but denies writing it.

---

## **3. Key Differences**

| Feature          | Authentication                    | Authorization                                    |
| ---------------- | --------------------------------- | ------------------------------------------------ |
| **Purpose**      | Verify identity                   | Verify permissions                               |
| **Question**     | Who are you?                      | What can you do?                                 |
| **When Checked** | First (login)                     | After authentication                             |
| **Methods**      | Password, OTP, biometric, tokens  | Roles, privileges, policies                      |
| **Example**      | Logging in with username/password | Accessing admin panel or restricted API endpoint |

---

## **4. Real-Life Analogy**

* **Authentication:** Showing your ID card at the gate.
* **Authorization:** Being allowed to enter a specific room based on your role.

---

💡 **Interview Tip:**

> "Authentication verifies who the user is, while authorization determines what the user is allowed to do. Authentication always happens **before** authorization."

---

I can next explain **JWT Authentication flow in Spring Boot**, which is a very common interview topic.

Do you want me to cover that?

---

## 143. What is Spring Security?

### **What is Spring Security?**

**Spring Security** is a **powerful and highly customizable authentication and access-control framework** for Java applications, primarily used in **Spring-based applications**.

* **Purpose:** Provides **security features** like authentication, authorization, protection against common attacks (CSRF, XSS), and secure session management.
* **Integration:** Works seamlessly with **Spring Boot, Spring MVC, and Spring REST APIs**.

---

## **1. Key Features of Spring Security**

| Feature                           | Description                                                                              |
| --------------------------------- | ---------------------------------------------------------------------------------------- |
| **Authentication**                | Verifies identity of users (username/password, OAuth, JWT, LDAP).                        |
| **Authorization**                 | Controls access to resources based on roles/permissions.                                 |
| **Password Management**           | Supports password encoding (BCrypt, SCrypt) for secure storage.                          |
| **CSRF Protection**               | Guards against Cross-Site Request Forgery attacks.                                       |
| **Session Management**            | Prevents session fixation, concurrent sessions, and manages timeouts.                    |
| **Method Security**               | Supports `@PreAuthorize`, `@PostAuthorize`, and other method-level security annotations. |
| **Integration with OAuth2 / JWT** | Supports modern authentication mechanisms for REST APIs.                                 |

---

## **2. How Spring Security Works**

1. **Filter Chain:** Spring Security uses a **chain of filters** (`SecurityFilterChain`) to intercept incoming requests.
2. **Authentication Manager:** Validates credentials against a configured **UserDetailsService** or other authentication providers.
3. **Authorization:** Checks **roles/authorities** to allow or deny access to endpoints.
4. **Security Context:** Stores **authenticated user details** for the session/request.

---

## **3. Basic Example in Spring Boot**

**Dependencies:**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
```

**Security Configuration (Spring Boot 3+):**

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/admin/**").hasRole("ADMIN")
                .anyRequest().authenticated()
            )
            .formLogin(Customizer.withDefaults())
            .httpBasic(Customizer.withDefaults());
        return http.build();
    }
}
```

**Explanation:**

* `/admin/**` → accessible only to users with **ADMIN** role.
* Other endpoints → require authentication.
* Supports **form login** and **HTTP Basic authentication**.

---

## **4. Advantages of Spring Security**

* Centralized **security management**.
* Highly **customizable** for authentication and authorization.
* Protects against **common vulnerabilities** automatically.
* Integrates with **JWT, OAuth2, LDAP, SAML** easily.

---

💡 **Interview Tip:**

> "Spring Security is a framework to secure Spring applications. It handles authentication (who you are) and authorization (what you can do) with filters, roles, and method-level annotations."

---

I can next explain **how JWT works with Spring Security for REST APIs**, which is a hot topic in interviews.

Do you want me to cover that?

---

## 144. How do you secure REST APIs using Spring Security?

### **Securing REST APIs Using Spring Security**

Securing REST APIs is essential to **authenticate users** and **authorize access** to endpoints. Spring Security provides a robust framework to do this, often using **JWT (JSON Web Tokens)** for stateless authentication.

---

## **1. Key Concepts for Securing REST APIs**

| Concept                  | Description                                                     |
| ------------------------ | --------------------------------------------------------------- |
| **Authentication**       | Verify the identity of the client (e.g., username/password).    |
| **Authorization**        | Grant access to endpoints based on roles/permissions.           |
| **Stateless APIs**       | REST APIs are usually **stateless**; no HTTP session is used.   |
| **JWT (JSON Web Token)** | Compact, URL-safe token containing **user identity and roles**. |
| **Filter Chain**         | Spring Security intercepts requests via **filters**.            |

---

## **2. Steps to Secure REST APIs Using Spring Security**

### **Step 1: Add Dependencies**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-api</artifactId>
    <version>0.11.5</version>
</dependency>
```

---

### **Step 2: Configure Security Filter Chain**

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain filterChain(HttpSecurity http) throws Exception {
        http
            .csrf(csrf -> csrf.disable()) // disable CSRF for REST
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/api/admin/**").hasRole("ADMIN")
                .requestMatchers("/api/user/**").hasAnyRole("USER", "ADMIN")
                .anyRequest().authenticated()
            )
            .sessionManagement(sess -> sess.sessionCreationPolicy(SessionCreationPolicy.STATELESS))
            .httpBasic(Customizer.withDefaults()); // or JWT filter

        return http.build();
    }
}
```

* **CSRF Disabled:** REST APIs are usually **stateless**, so CSRF protection is often disabled.
* **Stateless Session:** Uses `SessionCreationPolicy.STATELESS` so Spring Security **does not create sessions**.
* **Role-Based Access:** Admin endpoints restricted to **ADMIN role**.

---

### **Step 3: Implement JWT Authentication (Optional)**

1. **Generate JWT** after successful login:

```java
String jwt = Jwts.builder()
                 .setSubject(username)
                 .claim("roles", roles)
                 .setIssuedAt(new Date())
                 .setExpiration(new Date(System.currentTimeMillis() + 3600000)) // 1 hour
                 .signWith(SignatureAlgorithm.HS256, secretKey)
                 .compact();
```

2. **JWT Filter** to validate requests:

```java
public class JwtAuthenticationFilter extends OncePerRequestFilter {

    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain filterChain)
            throws ServletException, IOException {

        String authHeader = request.getHeader("Authorization");
        if (authHeader != null && authHeader.startsWith("Bearer ")) {
            String token = authHeader.substring(7);
            // validate token and set authentication in SecurityContext
        }
        filterChain.doFilter(request, response);
    }
}
```

3. **Register JWT Filter in Security Config:**

```java
http.addFilterBefore(jwtAuthenticationFilter(), UsernamePasswordAuthenticationFilter.class);
```

---

### **Step 4: Role-Based Endpoint Security**

```java
@RestController
@RequestMapping("/api/admin")
public class AdminController {

    @GetMapping("/dashboard")
    public String dashboard() {
        return "Admin Dashboard";
    }
}
```

* Only users with `ADMIN` role can access `/api/admin/dashboard`.

---

## **3. Advantages of Securing REST APIs with Spring Security**

* Centralized **authentication and authorization**.
* Supports **JWT, OAuth2, and Basic Auth**.
* Works with **role-based and method-level security** (`@PreAuthorize`).
* Handles **stateless security** for REST APIs efficiently.

---

💡 **Interview Tip:**

> "For REST APIs, use **stateless security** with Spring Security. Authenticate users via JWT or OAuth2, authorize endpoints by roles, and disable sessions and CSRF for stateless behavior."

---

I can next explain **difference between Basic Auth, JWT, and OAuth2 in Spring Security**, which is another frequently asked interview question.

Do you want me to cover that?

---

## 145. What is BasicAuth vs JWT?

### **Basic Authentication vs JWT (JSON Web Token) in Spring Security**

Both **Basic Auth** and **JWT** are common methods for authenticating clients in web applications and APIs, but they work **very differently**.

---

## **1. Basic Authentication (Basic Auth)**

* **Definition:** Sends the **username and password** encoded in **Base64** with every HTTP request.

* **Mechanism:**

  1. Client sends `Authorization: Basic <Base64(username:password)>`.
  2. Server decodes and validates credentials.
  3. Each request requires credentials.

* **Characteristics:**

  * **Stateless** or session-based depending on implementation.
  * Credentials are sent **with every request** → usually combined with **HTTPS** for security.
  * Simple to implement.

**Example (HTTP Header):**

```
Authorization: Basic dXNlcjpwYXNzd29yZA==
```

* `dXNlcjpwYXNzd29yZA==` → Base64 encoded `user:password`.

* **Pros:** Simple, supported by browsers and tools.

* **Cons:** Credentials exposed in every request, not suitable for mobile/SPA without HTTPS, no token revocation, cannot carry extra information easily.

---

## **2. JWT (JSON Web Token)**

* **Definition:** Token-based authentication where the server issues a **signed token** after login.

* **Mechanism:**

  1. Client logs in with username/password.
  2. Server generates a **JWT** containing user identity and roles.
  3. Client sends `Authorization: Bearer <JWT>` with requests.
  4. Server validates the token signature and extracts user info.

* **JWT Structure:**

  ```
  HEADER.PAYLOAD.SIGNATURE
  ```

  * Header → Algorithm & type
  * Payload → Claims (user, roles, expiration)
  * Signature → Ensures token integrity

**Example (HTTP Header):**

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

* **Pros:**

  * Stateless → no server session needed.
  * Can store **user info and roles** inside token.
  * Can be used across **different services** (microservices).
  * Expiration and revocation can be handled.

* **Cons:**

  * Slightly more complex to implement.
  * Token must be stored securely on the client (localStorage or cookies).

---

## **3. Key Differences**

| Feature                            | Basic Auth                           | JWT                                   |
| ---------------------------------- | ------------------------------------ | ------------------------------------- |
| **Credentials sent every request** | Yes                                  | No, token sent                        |
| **State**                          | Can be stateful or stateless         | Stateless                             |
| **Security**                       | Requires HTTPS to secure credentials | Token signed; HTTPS recommended       |
| **Contains user info**             | No                                   | Yes (claims in payload)               |
| **Revocation**                     | Hard (logout invalidates session)    | Token revocation required logic       |
| **Use case**                       | Simple APIs, internal tools          | Modern REST APIs, SPAs, microservices |

---

💡 **Interview Tip:**

> "Basic Auth sends credentials with every request and is simple but less secure. JWT issues a signed token after login, making REST APIs stateless and suitable for distributed systems."

---

I can next explain **OAuth2 vs JWT in Spring Security**, which is a common interview follow-up.

Do you want me to cover that?

---

## 146. What are HTTP status codes: 401,403,404,500,502,503?

### **Common HTTP Status Codes and Their Meaning**

HTTP status codes are **standardized codes** sent by the server to indicate the result of a client’s request. Here are the ones you asked about:

---

## **1. 401 Unauthorized**

* **Meaning:** The client is **not authenticated**.
* **When it occurs:**

  * User tries to access a resource without valid credentials.
  * Example: Accessing `/api/user` without a valid JWT token.
* **Response:** Server asks for authentication.

**Example:**

```json
{
  "status": 401,
  "error": "Unauthorized",
  "message": "Authentication required"
}
```

---

## **2. 403 Forbidden**

* **Meaning:** The client is **authenticated but not authorized** to access the resource.
* **When it occurs:**

  * User has valid credentials but lacks **permissions/role**.
  * Example: A `USER` trying to access `/admin/dashboard`.
* **Response:** Server refuses access.

**Example:**

```json
{
  "status": 403,
  "error": "Forbidden",
  "message": "Access denied"
}
```

---

## **3. 404 Not Found**

* **Meaning:** The requested resource **does not exist** on the server.
* **When it occurs:**

  * Incorrect URL, resource deleted, or endpoint not implemented.

**Example:**

```json
{
  "status": 404,
  "error": "Not Found",
  "message": "The requested resource was not found"
}
```

---

## **4. 500 Internal Server Error**

* **Meaning:** The server encountered an **unexpected condition**.
* **When it occurs:**

  * Unhandled exceptions in code.
  * Database errors, null pointers, or configuration issues.

**Example:**

```json
{
  "status": 500,
  "error": "Internal Server Error",
  "message": "Something went wrong on the server"
}
```

---

## **5. 502 Bad Gateway**

* **Meaning:** The server **acting as a gateway** received an invalid response from an **upstream server**.
* **When it occurs:**

  * Reverse proxy issues, API gateway forwarding problems, or backend service failure.

**Example:**

```json
{
  "status": 502,
  "error": "Bad Gateway",
  "message": "Upstream server error"
}
```

---

## **6. 503 Service Unavailable**

* **Meaning:** The server is **temporarily unable to handle the request**.
* **When it occurs:**

  * Server overload, maintenance, or backend downtime.
* **Response Header:** Often includes `Retry-After` to indicate when to retry.

**Example:**

```json
{
  "status": 503,
  "error": "Service Unavailable",
  "message": "Server is temporarily unavailable. Try again later."
}
```

---

### **Summary Table**

| Status Code | Meaning               | Typical Cause                              |
| ----------- | --------------------- | ------------------------------------------ |
| **401**     | Unauthorized          | No or invalid credentials                  |
| **403**     | Forbidden             | Authenticated but insufficient permissions |
| **404**     | Not Found             | Resource/endpoint does not exist           |
| **500**     | Internal Server Error | Server-side exception                      |
| **502**     | Bad Gateway           | Invalid response from upstream server      |
| **503**     | Service Unavailable   | Server overloaded or down for maintenance  |

---

💡 **Interview Tip:**

> "401 means you’re not authenticated, 403 means you don’t have permission, 404 means resource missing, 500 is a server error, 502 is an upstream server error, and 503 is temporary unavailability."

---

I can next explain **common Spring Boot exception handling for these HTTP status codes**, which is a frequently asked interview topic.

Do you want me to cover that?

---