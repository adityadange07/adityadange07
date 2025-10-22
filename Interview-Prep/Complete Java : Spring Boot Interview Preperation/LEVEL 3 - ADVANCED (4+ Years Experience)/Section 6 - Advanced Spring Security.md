# LEVEL 3: ADVANCED (4+ Years Experience)

# Advanced Spring Security

## 203. How do you implement OAuth2 and JWT in Spring Boot?

Absolutely, Aditya! Implementing **OAuth2** and **JWT** in Spring Boot is very common in modern applications for secure authentication and authorization. Let’s break it down step by step.

---

## **1. What is OAuth2 and JWT?**

| Concept                  | Description                                                                                                                                                                         |
| ------------------------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **OAuth2**               | Protocol for **authorization**, letting a client access resources on behalf of a user. It defines **roles like Resource Owner, Client, Authorization Server, and Resource Server**. |
| **JWT (JSON Web Token)** | **Compact, URL-safe token** that securely transmits claims between parties. Used for **authentication** and stateless authorization.                                                |

* **Typical Flow**:

  1. User logs in → receives **JWT token** from Authorization Server
  2. Client sends JWT with each request → Resource Server verifies JWT → grants access

---

## **2. Dependencies in Spring Boot**

Add the following dependencies in `pom.xml`:

```xml
<!-- Spring Security -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-security</artifactId>
</dependency>

<!-- OAuth2 Resource Server -->
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-resource-server</artifactId>
</dependency>

<!-- JWT Support -->
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-api</artifactId>
    <version>0.11.5</version>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-impl</artifactId>
    <version>0.11.5</version>
</dependency>
<dependency>
    <groupId>io.jsonwebtoken</groupId>
    <artifactId>jjwt-jackson</artifactId>
    <version>0.11.5</version>
</dependency>
```

---

## **3. JWT Token Generation**

```java
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import java.util.Date;

public class JwtUtil {
    private static final String SECRET_KEY = "mySecretKey12345";

    public static String generateToken(String username) {
        return Jwts.builder()
                .setSubject(username)
                .setIssuedAt(new Date())
                .setExpiration(new Date(System.currentTimeMillis() + 3600000)) // 1 hour
                .signWith(SignatureAlgorithm.HS256, SECRET_KEY)
                .compact();
    }
}
```

* Token contains **claims** (username, roles, expiry)
* Signed with a **secret key**

---

## **4. JWT Token Validation**

```java
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.Claims;

public class JwtUtil {

    public static Claims validateToken(String token) {
        return Jwts.parser()
                .setSigningKey("mySecretKey12345")
                .parseClaimsJws(token)
                .getBody();
    }
}
```

* Parse the token → verify signature → extract claims

---

## **5. Spring Security Configuration**

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .csrf().disable()
            .authorizeRequests()
            .antMatchers("/auth/**").permitAll()
            .anyRequest().authenticated()
            .and()
            .sessionManagement().sessionCreationPolicy(SessionCreationPolicy.STATELESS)
            .and()
            .addFilter(new JwtAuthenticationFilter(authenticationManager()));
    }
}
```

* Stateless authentication → no sessions
* `/auth/**` endpoints are **public** for login/registration
* All other endpoints **require JWT**

---

## **6. JWT Authentication Filter**

```java
public class JwtAuthenticationFilter extends OncePerRequestFilter {

    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain filterChain)
            throws ServletException, IOException {

        String header = request.getHeader("Authorization");
        if (header != null && header.startsWith("Bearer ")) {
            String token = header.substring(7);
            Claims claims = JwtUtil.validateToken(token);
            String username = claims.getSubject();

            UsernamePasswordAuthenticationToken auth =
                new UsernamePasswordAuthenticationToken(username, null, new ArrayList<>());
            SecurityContextHolder.getContext().setAuthentication(auth);
        }
        filterChain.doFilter(request, response);
    }
}
```

* Extract JWT from `Authorization` header
* Validate token
* Set `SecurityContext` for authorization

---

## **7. OAuth2 Integration (Optional)**

Spring Boot makes OAuth2 easy:

```properties
spring.security.oauth2.client.registration.google.client-id=YOUR_CLIENT_ID
spring.security.oauth2.client.registration.google.client-secret=YOUR_CLIENT_SECRET
spring.security.oauth2.client.registration.google.scope=email,profile
```

* Users can log in using **Google / GitHub / Facebook**
* OAuth2 provider issues **access tokens**, which can be further wrapped as JWT

---

## **8. Flow Summary**

1. **User Login** → validate credentials
2. **Generate JWT** → return to client
3. **Client sends JWT** in every request
4. **Server validates JWT** → allows or denies access
5. **Optional OAuth2** → third-party authorization

---

💡 **Interview Tips:**

* Highlight **stateless nature** of JWT → scales well
* Mention **refresh tokens** for long-lived sessions
* Explain **difference between OAuth2 and JWT**:

  * OAuth2 = protocol for authorization
  * JWT = token format used in authentication

---

If you want, I can make a **diagram showing JWT + OAuth2 flow in Spring Boot**, which is **very useful for whiteboard interviews**.

Do you want me to make that diagram?

---

## 204. What is a stateless session? How does JWT help?

Absolutely, Aditya! Let’s break down **stateless sessions** and how **JWT** fits into the picture.

---

## **1. What is a Stateless Session?**

* A **stateless session** means the **server does NOT store any session information** about the client.
* Every client request contains **all the information needed** for the server to process it.

### **Key Points:**

| Aspect         | Stateless                      | Stateful                               |
| -------------- | ------------------------------ | -------------------------------------- |
| Server storage | No session info                | Stores session in memory or DB         |
| Scalability    | High (multiple servers easily) | Limited (need session replication)     |
| Authentication | Token-based (JWT, OAuth2)      | Session ID (stored in server)          |
| Example        | REST APIs                      | Traditional web apps using HttpSession |

---

### **Why Stateless is Popular in REST APIs**

1. **Horizontal scaling friendly** → any server can handle requests
2. **No dependency on server memory** → reduces overhead
3. **Simpler failover and load balancing**

---

## **2. How JWT Helps in Stateless Sessions**

**JWT (JSON Web Token)** is perfect for stateless authentication:

1. **Server signs a token** after user login
2. **Client stores the token** (local storage, browser, or mobile app)
3. **Client sends the token** with every request in `Authorization` header:

```
Authorization: Bearer <JWT_TOKEN>
```

4. **Server validates the token** using a **secret key or public key**
5. **No server-side session storage needed** → stateless

---

### **JWT Structure**

A JWT has **3 parts**:

1. **Header** – algorithm and token type
2. **Payload** – claims like username, roles, expiry
3. **Signature** – ensures token integrity

Example:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9
.
eyJzdWIiOiJhZGl0eWEiLCJyb2xlIjoiVVNFUiIsImV4cCI6MTcwMDAwMDAwfQ
.
sTt3x2FGdWx6xN8cJKpT4ZkG1sh1QJ8F3R2bXNfGx0s
```

---

### **Flow of JWT in Stateless Session**

1. **Login Request:** User sends username/password
2. **Server Response:** Generates JWT → sends back to client
3. **Subsequent Requests:** Client sends JWT
4. **Server Validation:** Verifies signature, expiry, and claims → processes request

No server-side session data is stored.

---

### **3. Benefits of JWT for Stateless Sessions**

* **Scalable:** No session replication needed
* **Cross-platform:** Works with mobile, web, microservices
* **Secure:** Signed tokens prevent tampering
* **Self-contained:** Token carries user identity and roles

---

💡 **Interview Tip:**

* Emphasize **stateless = no server memory for sessions**
* JWT makes REST APIs **scalable and stateless**
* Mention **security best practices**: short expiry, HTTPS, refresh tokens

---

If you want, I can draw a **diagram showing stateless session flow using JWT**, which makes it very clear in interviews.

Do you want me to make that diagram?

---

## 205. How do you implement two-factor authentication (2FA)?

Absolutely, Aditya! Implementing **Two-Factor Authentication (2FA)** adds an extra security layer on top of traditional username/password authentication. Let’s break it down step by step.

---

## **1. What is Two-Factor Authentication (2FA)?**

* **2FA** requires **two independent factors** to verify a user’s identity:

  1. **Something you know** → password, PIN
  2. **Something you have** → OTP via SMS/email, authenticator app, hardware token
  3. *(Optional) Something you are → biometrics like fingerprint or face)*

* Even if the password is compromised, the attacker cannot log in without the second factor.

---

## **2. Types of 2FA**

| Type                                | Description                               | Example                     |
| ----------------------------------- | ----------------------------------------- | --------------------------- |
| SMS-based OTP                       | Send a one-time password via SMS          | 123456                      |
| Email OTP                           | Send a one-time password via email        | verification code           |
| TOTP (Time-based One-Time Password) | Generate codes via authenticator apps     | Google Authenticator, Authy |
| Push Notification                   | Approve login via mobile app notification | Duo Security                |

---

## **3. Implementing 2FA in Spring Boot (Typical Flow)**

### **Step 1: User Login (First Factor)**

* User submits **username and password**.
* Spring Security validates credentials.
* If valid, generate a **temporary session/token** for 2FA step.

---

### **Step 2: Generate OTP / TOTP (Second Factor)**

#### **Option A: SMS / Email OTP**

```java
public String generateOtp(String userId) {
    String otp = String.valueOf(new Random().nextInt(999999));
    // Save OTP in DB or cache with expiry
    // Send OTP via SMS or Email
    return otp;
}
```

* Store OTP with **expiry time** (5–10 minutes).
* Send OTP to user via **SMS API (Twilio, AWS SNS)** or **email**.

#### **Option B: TOTP (Authenticator App)**

* Use libraries like **Google Authenticator** or **java-totp**.
* Each user has a **secret key**, shared during registration.
* User scans QR code → authenticator app generates 6-digit TOTP.

---

### **Step 3: Verify OTP / TOTP**

```java
public boolean verifyOtp(String userId, String enteredOtp) {
    String storedOtp = getOtpFromCache(userId);
    return storedOtp.equals(enteredOtp);
}
```

* If **valid**, generate **JWT token or full authentication session**.
* If **invalid**, deny access.

---

### **Step 4: Secure the Flow**

1. OTP/TOTP should **expire quickly**.
2. Limit **max retries** to prevent brute-force attacks.
3. Use **HTTPS** for all requests.
4. Log all authentication attempts for **audit**.

---

### **4. Example: Spring Security 2FA Flow**

1. **POST /login** → validate username/password → temporary 2FA token
2. **POST /verify-otp** → validate OTP/TOTP → generate **JWT**
3. **All API calls** → JWT included in `Authorization` header → stateless session

---

### **5. Optional Enhancements**

* **Remember this device** → skip 2FA for trusted devices
* **Backup codes** → for offline recovery
* **Push notifications** → approve login on mobile app instead of entering OTP

---

💡 **Interview Tips:**

* Emphasize **extra security layer**
* Explain **why stateless JWT + 2FA** works well for REST APIs
* Discuss **trade-offs**: SMS OTP is easier but less secure than TOTP

---

If you want, I can make a **diagram showing 2FA flow with Spring Boot + JWT**, which is perfect for interviews.

Do you want me to make that diagram?

---

## 206. How does CSRF protection work in Spring?

Absolutely, Aditya! Let’s go step by step on **CSRF protection** in Spring, which is a very common security topic for interviews.

---

## **1. What is CSRF?**

**CSRF (Cross-Site Request Forgery)** is an attack where:

* An **attacker tricks a logged-in user** into submitting a request to a web application without their consent.
* Since the user is already authenticated, the server **processes the request**, potentially causing unauthorized actions (like changing password, transferring funds).

**Example:**

```html
<img src="https://bank.com/transfer?amount=1000&to=attacker" />
```

* If a user is logged in to `bank.com`, this image request could trigger a transfer.

---

## **2. How CSRF Protection Works in Spring**

Spring Security protects against CSRF attacks by **using a CSRF token**:

1. **Server generates a unique CSRF token** per session.
2. **Token is included in forms** or as a header for state-changing requests (POST, PUT, DELETE).
3. **Server validates the token** on each request.
4. If the token is missing or invalid → request is **rejected**.

---

### **3. Enabling CSRF in Spring Security**

Spring Security **enables CSRF protection by default** for state-changing HTTP methods.

```java
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .csrf() // CSRF enabled by default
            .and()
            .authorizeRequests()
            .antMatchers("/public/**").permitAll()
            .anyRequest().authenticated();
    }
}
```

---

### **4. Using CSRF Token in Forms (Thymeleaf example)**

```html
<form action="/updateProfile" method="post">
    <input type="hidden" th:name="${_csrf.parameterName}" th:value="${_csrf.token}"/>
    <input type="text" name="email"/>
    <button type="submit">Update</button>
</form>
```

* `${_csrf.token}` → generated by Spring Security
* `${_csrf.parameterName}` → usually `"_csrf"`

---

### **5. Using CSRF Token in REST APIs**

* For **AJAX / REST calls**, send the CSRF token in **HTTP header**:

```javascript
fetch("/updateProfile", {
  method: "POST",
  headers: {
    "Content-Type": "application/json",
    "X-CSRF-TOKEN": csrfToken
  },
  body: JSON.stringify({ email: "aditya@example.com" })
});
```

* Spring Security expects the header `X-CSRF-TOKEN` by default.

---

### **6. CSRF & Stateless JWT APIs**

* If your API is **stateless** and uses **JWT tokens**, CSRF protection is **usually not required**:

  * Why? JWT is sent in **Authorization header**, not cookies
  * CSRF attacks rely on **cookies automatically sent by the browser**

* For **cookie-based sessions**, CSRF is essential.

---

### **7. Summary / Interview Points**

1. CSRF = attacker forces a logged-in user to perform unintended actions.
2. Spring Security uses **unique CSRF tokens** per session to validate requests.
3. Tokens can be sent via **hidden form fields** or **headers** for AJAX.
4. **JWT-based stateless APIs** generally don’t need CSRF protection.

---

💡 **Analogy:**

* **CSRF Token = secret handshake**
* The server checks: “Does this request know the secret handshake?”
* If yes → valid request, if no → reject

---

If you want, I can make a **diagram showing CSRF attack vs Spring CSRF protection flow**, which is **super helpful for interviews**.

Do you want me to make that diagram?

---

## 207. What is the difference between pre-auth and post-auth filters?

Absolutely, Aditya! Let’s break down **pre-authentication** and **post-authentication filters** in Spring Security with clarity.

---

## **1. Overview of Filters in Spring Security**

* Spring Security uses a **filter chain** (`FilterChainProxy`) to process HTTP requests.
* Filters can be applied **before or after authentication**, depending on their purpose.

---

## **2. Pre-Authentication Filters**

### **Definition:**

* Filters that run **before the authentication process**.
* Responsible for **extracting credentials** or performing **request-level checks** **before the user is authenticated**.

### **Common Use Cases:**

1. Extract JWT token from the `Authorization` header.
2. Validate API keys or OAuth2 access tokens.
3. Logging, request tracing, or IP whitelisting.
4. Pre-processing request headers or request parameters.

### **Example in Spring Security:**

```java
public class JwtRequestFilter extends OncePerRequestFilter {

    @Override
    protected void doFilterInternal(HttpServletRequest request,
                                    HttpServletResponse response,
                                    FilterChain filterChain) throws ServletException, IOException {
        String token = request.getHeader("Authorization");
        if (token != null) {
            // Validate JWT and set authentication
        }
        filterChain.doFilter(request, response);
    }
}
```

* Runs **before authentication**.
* Sets the `SecurityContext` if valid.

---

## **3. Post-Authentication Filters**

### **Definition:**

* Filters that run **after the authentication process** is complete.
* Typically handle **authorization, logging, or additional processing** for authenticated users.

### **Common Use Cases:**

1. Role-based access control checks (authorization).
2. Logging authenticated requests.
3. Modifying response headers for authenticated users.
4. Auditing or metrics collection.

### **Example in Spring Security:**

* `FilterSecurityInterceptor` is a built-in **post-auth filter**:

  * Checks if the **authenticated user** has the **required role/authority** for the requested URL.

---

## **4. Key Differences:**

| Aspect              | Pre-Auth Filter                         | Post-Auth Filter                                                   |
| ------------------- | --------------------------------------- | ------------------------------------------------------------------ |
| **Execution**       | Before authentication                   | After authentication                                               |
| **Purpose**         | Extract credentials, preliminary checks | Authorization, auditing, response modifications                    |
| **SecurityContext** | May not be set yet                      | Already set, user is authenticated                                 |
| **Examples**        | JWT filter, API key filter              | FilterSecurityInterceptor, logging filters for authenticated users |

---

### **5. Typical Flow in Spring Security:**

```
HTTP Request → Pre-Auth Filters → Authentication Manager → SecurityContext set → Post-Auth Filters → Controller
```

---

💡 **Interview Tip:**

* Emphasize: **Pre-auth filters handle authentication-related tasks**, **Post-auth filters handle authorization & post-processing**.
* Mention **common pre-auth example: JWT extraction**, **common post-auth example: role validation**.

---

If you want, I can **draw a diagram showing Spring Security filter chain with pre-auth and post-auth filters**, which is **very helpful in interviews**.

Do you want me to make that diagram?

---

## 208. How does SecurityFilterChain work in Spring Boot 3+?

Absolutely, Aditya! In **Spring Boot 3+** (Spring Security 6), the **`SecurityFilterChain`** replaces the old `WebSecurityConfigurerAdapter` approach and provides a **more flexible, functional way** to configure security. Let’s break it down.

---

## **1. What is SecurityFilterChain?**

* `SecurityFilterChain` is a **Spring Bean** that defines the **order and configuration of security filters** applied to HTTP requests.
* Each chain contains a **sequence of filters** that process requests **for authentication and authorization**.
* Multiple `SecurityFilterChain` beans can be defined to **apply different security rules to different URL patterns**.

---

## **2. Defining a SecurityFilterChain Bean**

In Spring Boot 3+, you define it like this:

```java
@Configuration
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .csrf().disable() // disable CSRF for APIs
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/public/**").permitAll() // public endpoints
                .anyRequest().authenticated() // other endpoints need authentication
            )
            .httpBasic(Customizer.withDefaults()) // basic auth (or use JWT filter)
            .sessionManagement(session -> session
                .sessionCreationPolicy(SessionCreationPolicy.STATELESS) // stateless session
            );

        return http.build();
    }
}
```

* `http.authorizeHttpRequests()` → define which URLs are public or protected
* `http.sessionManagement()` → configure stateless sessions (JWT-based)
* `http.build()` → builds the filter chain as a Spring Bean

---

## **3. How SecurityFilterChain Works Internally**

1. **Incoming Request** → enters Spring Security’s **FilterChainProxy**.

2. **FilterChainProxy** checks all `SecurityFilterChain` beans.

3. If a chain **matches the request URL pattern**, its **filters are executed** in order:

   * `ChannelProcessingFilter` → ensures HTTPS
   * `CorsFilter` → handles CORS
   * `CsrfFilter` → validates CSRF token
   * `SecurityContextPersistenceFilter` → sets up SecurityContext
   * `AuthenticationFilter` → authenticates user
   * `AuthorizationFilter` → checks roles/permissions
   * `ExceptionTranslationFilter` → handles access denied or authentication failures
   * `FilterSecurityInterceptor` → final authorization decision

4. After the chain completes, the request reaches your **controller**.

---

## **4. Multiple SecurityFilterChains**

* You can define **different chains for different URL patterns**:

```java
@Bean
public SecurityFilterChain adminSecurity(HttpSecurity http) throws Exception {
    http
        .securityMatcher("/admin/**") // only applies to /admin/*
        .authorizeHttpRequests(auth -> auth.anyRequest().hasRole("ADMIN"))
        .httpBasic();
    return http.build();
}

@Bean
public SecurityFilterChain apiSecurity(HttpSecurity http) throws Exception {
    http
        .securityMatcher("/api/**")
        .authorizeHttpRequests(auth -> auth.anyRequest().authenticated())
        .sessionManagement(session -> session.sessionCreationPolicy(SessionCreationPolicy.STATELESS));
    return http.build();
}
```

* **Spring selects the first chain that matches the request URL.**

---

## **5. Key Points / Interview Tips**

* **Spring Boot 3+ removed `WebSecurityConfigurerAdapter`** → now **bean-based configuration**
* **`SecurityFilterChain` = functional, flexible, multiple chains for different URLs**
* Filters inside a chain are **executed in a specific order** (authentication → authorization → post-processing)
* Supports **stateless APIs** (JWT) and traditional session-based apps

---

💡 **Analogy:**
Think of `SecurityFilterChain` as a **pipeline**: each HTTP request goes through a **series of filters** (guards) before it reaches the controller, and you can have **different pipelines for different endpoints**.

---

If you want, I can **draw a diagram showing SecurityFilterChain flow with multiple URL-based chains**, which is **very helpful for interviews**.

Do you want me to make that diagram?

---

## 209. What is UserDetailsService and how do you implement it?

Absolutely, Aditya! Let’s go step by step on **`UserDetailsService`** in Spring Security and how to implement it.

---

## **1. What is UserDetailsService?**

* **`UserDetailsService`** is a **core interface in Spring Security**.
* Its purpose is to **load user-specific data** during authentication.
* It has **one main method**:

```java
UserDetails loadUserByUsername(String username) throws UsernameNotFoundException;
```

* Returns a **`UserDetails` object** that contains:

  * Username
  * Password (usually hashed)
  * Roles / authorities
  * Account status (enabled, locked, expired, etc.)

* Spring Security uses this method to **authenticate the user**.

---

## **2. UserDetails Interface**

The `UserDetails` object contains information about the user:

```java
public interface UserDetails {
    Collection<? extends GrantedAuthority> getAuthorities();
    String getPassword();
    String getUsername();
    boolean isAccountNonExpired();
    boolean isAccountNonLocked();
    boolean isCredentialsNonExpired();
    boolean isEnabled();
}
```

* You can either **use Spring’s built-in `User` class** or create your own custom implementation.

---

## **3. Implementing UserDetailsService**

### **Step 1: Create an Entity for User**

```java
@Entity
public class AppUser {
    @Id
    private Long id;
    private String username;
    private String password;
    private String role;
    private boolean enabled;
}
```

---

### **Step 2: Create a Repository**

```java
public interface UserRepository extends JpaRepository<AppUser, Long> {
    Optional<AppUser> findByUsername(String username);
}
```

---

### **Step 3: Implement UserDetailsService**

```java
@Service
public class CustomUserDetailsService implements UserDetailsService {

    @Autowired
    private UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        AppUser appUser = userRepository.findByUsername(username)
                .orElseThrow(() -> new UsernameNotFoundException("User not found"));

        // Convert AppUser to Spring Security UserDetails
        return User.builder()
                .username(appUser.getUsername())
                .password(appUser.getPassword())
                .roles(appUser.getRole()) // ROLE_USER, ROLE_ADMIN
                .disabled(!appUser.isEnabled())
                .build();
    }
}
```

---

### **4. Integrate with SecurityFilterChain**

```java
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http, CustomUserDetailsService userDetailsService) throws Exception {
    return http
            .authorizeHttpRequests(auth -> auth.anyRequest().authenticated())
            .userDetailsService(userDetailsService) // link your service
            .httpBasic(Customizer.withDefaults())
            .build();
}
```

---

### **5. Key Points / Interview Notes**

1. **`UserDetailsService` = bridge between your database and Spring Security**.
2. You must **return a `UserDetails` object** containing username, password, roles.
3. Supports **custom user tables** and **custom authentication logic**.
4. Works well with **JWT / stateless authentication**.

---

💡 **Analogy:**
Think of `UserDetailsService` as a **user loader**: when Spring Security sees a login request, it asks `UserDetailsService`:

*"Hey, give me the user info for this username so I can check credentials and roles."*

---

If you want, I can **draw a diagram showing how Spring Security interacts with UserDetailsService during authentication**, which is perfect for interviews.

Do you want me to make that diagram?

---

## 210. How do you implement role-based access control (RBAC)?

Absolutely, Aditya! Let’s go step by step on **Role-Based Access Control (RBAC) in Spring Boot** and how to implement it effectively.

---

## **1. What is RBAC?**

**Role-Based Access Control (RBAC)** is a method to **restrict system access based on user roles**:

* Each user is assigned **one or more roles**.
* Each role has **permissions/authorities** to perform certain actions.
* Access to APIs or resources is **granted/denied based on role**.

**Example:**

| User    | Role  | Permissions                  |
| ------- | ----- | ---------------------------- |
| Alice   | ADMIN | CREATE, READ, UPDATE, DELETE |
| Bob     | USER  | READ, UPDATE                 |
| Charlie | GUEST | READ                         |

---

## **2. RBAC in Spring Boot (Spring Security)**

Spring Security supports RBAC **using roles and authorities**:

1. **Roles** → high-level categories (e.g., ADMIN, USER)
2. **Authorities** → fine-grained permissions (e.g., WRITE_PRIVILEGES)

> Note: By default, Spring Security **prefixes roles with `ROLE_`**.

---

## **3. Steps to Implement RBAC**

### **Step 1: Define User and Role Entities**

```java
@Entity
public class Role {
    @Id
    private Long id;
    private String name; // e.g., ROLE_ADMIN
}

@Entity
public class AppUser {
    @Id
    private Long id;
    private String username;
    private String password;
    private boolean enabled;

    @ManyToMany(fetch = FetchType.EAGER)
    private Set<Role> roles;
}
```

---

### **Step 2: Load User with Roles**

Implement **UserDetailsService**:

```java
@Service
public class CustomUserDetailsService implements UserDetailsService {

    @Autowired
    private UserRepository userRepository;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        AppUser appUser = userRepository.findByUsername(username)
                .orElseThrow(() -> new UsernameNotFoundException("User not found"));

        Set<GrantedAuthority> authorities = appUser.getRoles().stream()
                .map(role -> new SimpleGrantedAuthority(role.getName()))
                .collect(Collectors.toSet());

        return new User(appUser.getUsername(), appUser.getPassword(), authorities);
    }
}
```

* **Roles are mapped to `GrantedAuthority`** for Spring Security.

---

### **Step 3: Secure Endpoints Based on Roles**

**Option A: Using `SecurityFilterChain`**

```java
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    http
        .authorizeHttpRequests(auth -> auth
            .requestMatchers("/admin/**").hasRole("ADMIN")
            .requestMatchers("/user/**").hasAnyRole("USER","ADMIN")
            .anyRequest().authenticated()
        )
        .httpBasic(Customizer.withDefaults());
    return http.build();
}
```

**Option B: Using Method-Level Security (`@PreAuthorize`)**

```java
@RestController
@RequestMapping("/api")
public class UserController {

    @GetMapping("/admin/data")
    @PreAuthorize("hasRole('ADMIN')")
    public String adminData() {
        return "Admin Data";
    }

    @GetMapping("/user/data")
    @PreAuthorize("hasAnyRole('USER','ADMIN')")
    public String userData() {
        return "User Data";
    }
}
```

* Enable method security:

```java
@EnableMethodSecurity(prePostEnabled = true)
@Configuration
public class MethodSecurityConfig {}
```

---

### **4. Key Points / Interview Notes**

1. **Roles and authorities** are central to RBAC.
2. Can be applied **URL-based** (via `SecurityFilterChain`) or **method-based** (`@PreAuthorize`).
3. Always **prefix roles with `ROLE_`** in Spring Security.
4. Works seamlessly with **stateless JWT authentication**.

---

💡 **Analogy:**

* **User = employee**, **Role = job title**, **Authority = what they can do in the system**.
* Spring Security **checks the user’s role/authority before allowing access**.

---

If you want, I can **draw a diagram showing RBAC flow with JWT, UserDetailsService, and roles checking**, which is super useful for interviews.

Do you want me to make that diagram?

---

## 211. How do you implement method-level security?

Absolutely, Aditya! Let’s go step by step on **method-level security in Spring Boot** and how to implement it effectively.

---

## **1. What is Method-Level Security?**

* **Method-level security** allows you to **secure specific methods** in your service or controller classes based on **roles or permissions**, instead of securing entire URLs.
* Provides **fine-grained access control** at the method level.

**Example:**

* Only admins can access `deleteUser()`
* Users and admins can access `viewProfile()`

---

## **2. Enable Method-Level Security**

In Spring Boot 3+ (Spring Security 6+), use:

```java
@EnableMethodSecurity(prePostEnabled = true)
@Configuration
public class MethodSecurityConfig {}
```

* `prePostEnabled = true` → enables `@PreAuthorize` and `@PostAuthorize` annotations.

---

## **3. Annotations for Method-Level Security**

### **A. @PreAuthorize**

* Checks **before** method execution.
* Example:

```java
@PreAuthorize("hasRole('ADMIN')")
public void deleteUser(Long id) {
    // Only admins can delete users
}
```

* You can also check multiple roles:

```java
@PreAuthorize("hasAnyRole('ADMIN', 'MANAGER')")
public void updateUser(User user) {}
```

---

### **B. @PostAuthorize**

* Checks **after** method execution.
* Useful when you need to inspect the **returned object**:

```java
@PostAuthorize("returnObject.username == authentication.name")
public User getUser(Long id) {
    return userRepository.findById(id).orElseThrow();
}
```

---

### **C. @Secured**

* Simpler annotation for **roles only**.
* Example:

```java
@Secured("ROLE_ADMIN")
public void deleteUser(Long id) {}
```

> Note: Roles must include `ROLE_` prefix with `@Secured`.

---

### **D. @RolesAllowed** (JSR-250)

* Another alternative for **role-based security**:

```java
@RolesAllowed({"ROLE_ADMIN", "ROLE_MANAGER"})
public void updateUser(User user) {}
```

* Requires enabling JSR-250: `@EnableMethodSecurity(jsr250Enabled = true)`

---

## **4. Example: Full Setup**

### **User Entity**

```java
@Entity
public class AppUser {
    @Id private Long id;
    private String username;
    private String password;
    private boolean enabled;

    @ManyToMany(fetch = FetchType.EAGER)
    private Set<Role> roles;
}
```

### **Service with Method-Level Security**

```java
@Service
public class UserService {

    @PreAuthorize("hasRole('ADMIN')")
    public void deleteUser(Long id) {
        // delete logic
    }

    @PreAuthorize("hasAnyRole('USER','ADMIN')")
    public User getUser(Long id) {
        return userRepository.findById(id).orElseThrow();
    }
}
```

### **Security Configuration**

```java
@Configuration
@EnableMethodSecurity(prePostEnabled = true)
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http.authorizeHttpRequests(auth -> auth.anyRequest().authenticated())
            .httpBasic(Customizer.withDefaults());
        return http.build();
    }
}
```

---

## **5. Key Points / Interview Notes**

1. **Method-level security = fine-grained security** at service or controller layer.
2. **@PreAuthorize** → pre-method checks, **@PostAuthorize** → post-method checks.
3. Supports **role checks**, **expression-based access**, and **custom conditions**.
4. Works with **JWT or session-based authentication**.
5. **Enabling it is mandatory** using `@EnableMethodSecurity`.

---

💡 **Analogy:**

* **URL-based security** = “Is the user allowed to enter the building?”
* **Method-level security** = “Is the user allowed to access this specific room inside the building?”

---

If you want, I can make a **diagram showing how Spring Security calls `UserDetailsService` → authenticates → method-level security checks roles before executing service methods**, which is very useful for interviews.

Do you want me to make that diagram?

---

## 212. How do you secure microservices communication?

Absolutely, Aditya! Securing **microservices communication** is a crucial topic in distributed systems. Let’s go step by step.

---

## **1. Why Securing Microservices Communication is Important**

* Microservices often communicate over **HTTP, gRPC, or messaging systems (Kafka, RabbitMQ)**.
* Unsecured communication can lead to:

  * **Data leakage**
  * **Man-in-the-middle attacks**
  * **Unauthorized access to services**

---

## **2. Common Approaches for Securing Microservices**

### **A. HTTPS / TLS**

* Always use **HTTPS for REST/gRPC endpoints**.
* Ensures **encryption in transit**.
* Each microservice should have a **TLS certificate** (self-signed or from a CA).

**Example (Spring Boot):**

```properties
server.port=8443
server.ssl.key-store=classpath:keystore.p12
server.ssl.key-store-password=changeit
server.ssl.key-store-type=PKCS12
server.ssl.key-alias=server
```

---

### **B. Authentication & Authorization**

#### **1. JWT (JSON Web Tokens)**

* Each request carries a **JWT token** issued by an **auth service**.
* Microservices **verify the token** before processing the request.

**Flow:**

1. Client logs in → gets JWT from Auth Service.
2. Client calls Service A with JWT.
3. Service A verifies JWT → calls Service B with **same or new JWT**.
4. Service B verifies JWT → returns response.

**Example (Spring Boot with JWT Filter):**

```java
http
    .authorizeHttpRequests(auth -> auth.anyRequest().authenticated())
    .oauth2ResourceServer(oauth2 -> oauth2.jwt());
```

---

#### **2. OAuth2 / OpenID Connect**

* Use **centralized auth server** (Keycloak, Okta, Auth0).
* Microservices act as **resource servers**.
* Tokens include **roles and scopes** for RBAC.

---

### **C. Service-to-Service Authentication**

* **Mutual TLS (mTLS)**: both client and server **authenticate each other** using certificates.
* Prevents **unauthorized services** from communicating.

---

### **D. API Gateway / Service Mesh**

#### **1. API Gateway**

* Acts as a **security enforcement point**.
* Handles:

  * Authentication & authorization
  * Rate limiting
  * Logging & monitoring

**Example: Spring Cloud Gateway with JWT filter**

#### **2. Service Mesh (Istio, Linkerd)**

* Automatically enforces **mTLS between services**.
* Handles **service-to-service encryption** without changing app code.

---

### **E. Message Broker Security**

If microservices communicate via **Kafka, RabbitMQ**:

* Enable **TLS for brokers**
* Authenticate clients using **SASL / SSL certificates**
* Authorize topics/queues per service

---

### **3. Best Practices**

1. **Always encrypt traffic** (TLS/HTTPS/mTLS).
2. **Centralize authentication** (Auth server, JWT/OAuth2).
3. **Use short-lived tokens** to minimize risk.
4. **Validate tokens on every service call**.
5. **Use API gateway or service mesh** for additional security and observability.
6. **Audit & log** service-to-service requests for compliance.

---

### **4. Diagram Flow**

**Client → API Gateway → Microservice A → Microservice B**

* **JWT / OAuth2 token passed along**
* **mTLS ensures encrypted service-to-service communication**

---

💡 **Interview Tip:**

* Highlight **JWT + API Gateway + HTTPS/mTLS**.
* Mention **service mesh** as advanced approach.
* Emphasize **defense-in-depth**: each layer should enforce security.

---

If you want, I can **draw a detailed diagram showing secured microservices communication with JWT, API Gateway, and mTLS**, which is **very useful for interviews**.

Do you want me to make that diagram?

---

## 213. How to implement OAuth authentication in Spring Boot?

Absolutely, Aditya! Let’s go step by step on **implementing OAuth 2.0 authentication in Spring Boot**. I’ll focus on the most common setup: **using Spring Security with an external OAuth provider** (e.g., Google, Keycloak, Okta) and a **resource server**.

---

## **1. What is OAuth 2.0?**

* OAuth 2.0 is an **authorization framework** that allows an application to **access resources on behalf of a user**.
* Key roles:

  1. **Resource Owner** – the user
  2. **Client** – your application
  3. **Authorization Server** – issues tokens
  4. **Resource Server** – API/server hosting resources

**Flow:**
`Client → Auth Server → Access Token → Resource Server → Protected API`

---

## **2. Add Dependencies**

For Spring Boot 3+:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-client</artifactId>
</dependency>

<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-oauth2-resource-server</artifactId>
</dependency>
```

* `oauth2-client` → for web login via OAuth providers
* `oauth2-resource-server` → to secure APIs with JWT / OAuth tokens

---

## **3. Configure Application Properties**

For example, **Google OAuth**:

```properties
spring.security.oauth2.client.registration.google.client-id=your-client-id
spring.security.oauth2.client.registration.google.client-secret=your-client-secret
spring.security.oauth2.client.registration.google.scope=openid,profile,email
spring.security.oauth2.client.registration.google.redirect-uri={baseUrl}/login/oauth2/code/{registrationId}

spring.security.oauth2.client.provider.google.authorization-uri=https://accounts.google.com/o/oauth2/v2/auth
spring.security.oauth2.client.provider.google.token-uri=https://oauth2.googleapis.com/token
spring.security.oauth2.client.provider.google.user-info-uri=https://www.googleapis.com/oauth2/v3/userinfo
spring.security.oauth2.client.provider.google.user-name-attribute=sub
```

* `registration` → client configuration
* `provider` → endpoints of the OAuth provider

---

## **4. Configure Security in Spring Boot**

### **A. OAuth2 Login (Web Application)**

```java
@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/public/**").permitAll()
                .anyRequest().authenticated()
            )
            .oauth2Login(Customizer.withDefaults()); // OAuth2 login
        return http.build();
    }
}
```

* Users are redirected to the OAuth provider’s login page.
* After login, **Spring Security creates an `OAuth2User`** representing the authenticated user.

---

### **B. Resource Server (APIs with JWT)**

```java
@Configuration
@EnableWebSecurity
public class ResourceServerConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        http
            .authorizeHttpRequests(auth -> auth
                .requestMatchers("/api/public/**").permitAll()
                .anyRequest().authenticated()
            )
            .oauth2ResourceServer(oauth2 -> oauth2.jwt()); // validate JWT tokens
        return http.build();
    }
}
```

* Secures REST APIs using **JWT tokens issued by Auth Server**.

---

## **5. Accessing User Details**

After login, you can access user details via `OAuth2User`:

```java
@RestController
public class UserController {

    @GetMapping("/user")
    public String user(@AuthenticationPrincipal OAuth2User principal) {
        return "Hello, " + principal.getAttribute("name");
    }
}
```

* `@AuthenticationPrincipal` injects the **authenticated OAuth2 user**.
* You can access attributes like `email`, `name`, `picture`.

---

## **6. Key Points / Interview Notes**

1. **OAuth2 Login** → Web login with providers (Google, GitHub, Keycloak).
2. **Resource Server** → Secures APIs via JWT tokens.
3. Spring Boot 3+ **does not need WebSecurityConfigurerAdapter**; use `SecurityFilterChain`.
4. `oauth2Login()` → redirects to OAuth provider
5. `oauth2ResourceServer().jwt()` → validates tokens for APIs

---

💡 **Analogy:**

* **OAuth2 Login** → “I don’t have a password, I’ll log in using Google/Keycloak.”
* **Resource Server** → “I trust the token from the Auth Server, let me allow access based on it.”

---

If you want, I can create a **diagram showing OAuth2 authentication flow in Spring Boot with client, authorization server, and resource server**, which is perfect for interviews.

Do you want me to make that diagram?

---