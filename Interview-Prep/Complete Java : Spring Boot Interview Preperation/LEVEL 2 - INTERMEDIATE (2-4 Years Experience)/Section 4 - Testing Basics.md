# LEVEL 2: INTERMEDIATE (2-4 Years Experience)

# Testing Basics

## 137. What is JUnit? Basic annotations?

### **What is JUnit?**

**JUnit** is a **popular open-source testing framework** in Java used to write and run **unit tests**.

* **Purpose:** Verify that individual units of code (methods/classes) work as expected.

* **Version:** JUnit 5 is the latest major version, consisting of:

  * **JUnit Platform** → foundation for running tests.
  * **JUnit Jupiter** → new programming model (annotations, assertions).
  * **JUnit Vintage** → supports older JUnit 3/4 tests.

* **Integration:** Works with IDEs (Eclipse, IntelliJ), build tools (Maven, Gradle), and CI/CD pipelines.

---

## **Basic JUnit Annotations**

| Annotation           | Description                                                                  |
| -------------------- | ---------------------------------------------------------------------------- |
| `@Test`              | Marks a method as a test method.                                             |
| `@BeforeEach`        | Runs **before each test method**; used to set up test data.                  |
| `@AfterEach`         | Runs **after each test method**; used for cleanup.                           |
| `@BeforeAll`         | Runs **once before all test methods** in the class; method must be `static`. |
| `@AfterAll`          | Runs **once after all test methods** in the class; method must be `static`.  |
| `@Disabled`          | Skips/ignores a test method or class.                                        |
| `@RepeatedTest`      | Runs a test multiple times.                                                  |
| `@ParameterizedTest` | Runs a test multiple times with different input values.                      |
| `@DisplayName`       | Sets a custom display name for test methods/classes.                         |

---

## **Example JUnit Test Class**

```java
import org.junit.jupiter.api.*;

import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    Calculator calculator;

    @BeforeEach
    void setup() {
        calculator = new Calculator();
    }

    @Test
    void testAdd() {
        int result = calculator.add(5, 3);
        assertEquals(8, result); // Assert that 5+3=8
    }

    @Test
    @Disabled
    void testSubtract() {
        int result = calculator.subtract(5, 3);
        assertEquals(2, result);
    }

    @AfterEach
    void cleanup() {
        calculator = null;
    }
}
```

* **`@BeforeEach`** → initialize `Calculator` before each test.
* **`@Test`** → actual test method.
* **`assertEquals()`** → assertion to verify result.
* **`@AfterEach`** → cleanup after test.
* **`@Disabled`** → skip the test method.

---

💡 **Interview Tip:**

> "JUnit is a framework for unit testing in Java. Use `@Test` for test methods, `@BeforeEach`/`@AfterEach` for setup and cleanup, and assertions like `assertEquals` to verify behavior."

---

I can next explain **JUnit Assertions (`assertEquals`, `assertTrue`, `assertThrows`)** with examples, which is a very common follow-up topic.

Do you want me to cover that?

---

## 138. What is @Mockito? When to use @Mock?

### **What is `@Mock` in Mockito?**

**Mockito** is a popular **Java mocking framework** used for **unit testing**, especially to **mock dependencies** of the class under test.

* **Purpose:** Allows testing a class **in isolation** by creating **fake objects** (mocks) that simulate the behavior of real dependencies.
* **Integration:** Often used with **JUnit** for unit testing.

---

## **1. `@Mock` Annotation**

* **Definition:** `@Mock` is used to **create and inject mock objects** automatically.
* **Purpose:** Replace real objects with **mock objects** that **do not execute actual logic**.
* **Requirement:** Must be initialized using `MockitoAnnotations.openMocks(this)` or with `@ExtendWith(MockitoExtension.class)` in JUnit 5.

**Example:**

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;

import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

class UserServiceTest {

    @Mock
    UserRepository userRepository; // dependency to be mocked

    @InjectMocks
    UserService userService; // class under test

    @BeforeEach
    void setup() {
        MockitoAnnotations.openMocks(this); // initialize mocks
    }

    @Test
    void testGetUserById() {
        User mockUser = new User(1, "Alice");
        when(userRepository.findById(1)).thenReturn(mockUser); // define behavior

        User user = userService.getUserById(1);

        assertEquals("Alice", user.getName());
        verify(userRepository, times(1)).findById(1); // verify method call
    }
}
```

---

## **2. Key Points About `@Mock`**

* Creates a **mock instance** of the class or interface.
* Methods return **default values** (0, null, false) unless **stubbed** with `when(...).thenReturn(...)`.
* Used for **dependencies** like repositories, services, or external APIs.
* Helps **isolate the class under test** from its dependencies.

---

## **3. Difference Between `@Mock` and `@InjectMocks`**

| Annotation     | Purpose                                                                  |
| -------------- | ------------------------------------------------------------------------ |
| `@Mock`        | Creates **mock objects** for dependencies.                               |
| `@InjectMocks` | Creates **real instance of class under test** and injects mocks into it. |

---

## **4. When to Use `@Mock`**

* When the class under test **depends on other classes** (services, repositories).
* When you **don’t want to call actual database, API, or service**.
* For **isolated unit testing** to ensure **only the class under test is tested**.

---

💡 **Interview Tip:**

> "`@Mock` in Mockito creates fake objects to simulate dependencies. Use it when you want to isolate the class under test and avoid calling real methods like database operations."

---

I can next explain **`@Spy` vs `@Mock` in Mockito**, which is another common interview question.

Do you want me to cover that?

---

## 139. What is the difference between @Mock, @MockBean, and @Spy?

### **Difference Between `@Mock`, `@MockBean`, and `@Spy` in Java Testing**

These annotations are commonly used in **Mockito** and **Spring Boot tests** to create mock or spy objects, but they have **different purposes and scopes**.

---

## **1. `@Mock` (Mockito)**

* **Framework:** Mockito
* **Purpose:** Creates a **mock instance** of a class or interface.
* **Behavior:**

  * Methods return **default values** (`null`, `0`, `false`) unless stubbed.
  * The mock is **not a real object**; no real logic is executed.
  * Used in **unit tests** to **isolate dependencies**.
* **Initialization:** Must be initialized with `MockitoAnnotations.openMocks(this)` or use `@ExtendWith(MockitoExtension.class)` in JUnit 5.

**Example:**

```java
@Mock
UserRepository userRepository;

@InjectMocks
UserService userService; // userRepository injected as mock
```

* **Use Case:** Unit testing classes in isolation.

---

## **2. `@MockBean` (Spring Boot)**

* **Framework:** Spring Boot Test
* **Purpose:** Creates a **mock bean in the Spring ApplicationContext**.
* **Behavior:**

  * Replaces an **actual Spring bean** with a **mock**.
  * Works with `@SpringBootTest` or other Spring integration tests.
  * Automatically injected into the **Spring context**.
* **Use Case:** Integration testing when you want to **mock a dependency bean** while testing Spring components.

**Example:**

```java
@SpringBootTest
class UserServiceTest {

    @MockBean
    UserRepository userRepository; // replaces actual bean in context

    @Autowired
    UserService userService; // uses mocked userRepository
}
```

* **Key Difference:** Unlike `@Mock`, `@MockBean` works **within Spring context**.

---

## **3. `@Spy` (Mockito)**

* **Framework:** Mockito
* **Purpose:** Creates a **spy object**, which is a **real instance wrapped in a spy**.
* **Behavior:**

  * Calls **real methods** by default.
  * You can **stub specific methods** to return custom values.
  * Useful when you want **partial mocking**.

**Example:**

```java
@Spy
List<String> list = new ArrayList<>();

@Test
void testSpy() {
    list.add("Hello");
    doReturn(100).when(list).size(); // override size()
    assertEquals(100, list.size()); // size is stubbed, other methods use real logic
}
```

* **Use Case:** When you want to **partially mock a real object** while keeping its real behavior for other methods.

---

## **4. Quick Comparison Table**

| Annotation  | Framework   | Creates          | Default Behavior                       | Use Case                             |
| ----------- | ----------- | ---------------- | -------------------------------------- | ------------------------------------ |
| `@Mock`     | Mockito     | Mock object      | Returns default values, no real logic  | Unit tests for isolated dependencies |
| `@MockBean` | Spring Boot | Mock Spring bean | Replaces actual Spring bean in context | Integration tests with Spring Boot   |
| `@Spy`      | Mockito     | Spy object       | Calls real methods unless stubbed      | Partial mocking of real objects      |

---

💡 **Interview Tip:**

> "`@Mock` is for isolated unit testing, `@MockBean` is for replacing Spring beans in integration tests, and `@Spy` is for partial mocking of real objects where some methods retain real behavior."

---

I can next explain **`doReturn()` vs `when()` in Mockito**, which is another common point of confusion in interviews.

Do you want me to cover that?

---

## 140. How do you test REST controllers using MockMvc?

### **Testing REST Controllers Using `MockMvc` in Spring Boot**

**`MockMvc`** is a **Spring testing utility** that allows you to **test Spring MVC controllers** without starting the full HTTP server. It simulates **HTTP requests and responses**, making it ideal for unit or integration testing REST APIs.

---

## **1. Key Points**

* **Framework:** Spring MVC Test (part of `spring-test`)
* **Purpose:**

  * Test controller endpoints, request mappings, response status, headers, and body.
  * Perform **GET, POST, PUT, DELETE** requests in tests.
* **Advantages:**

  * Fast (no server start).
  * Allows testing **Spring MVC behavior**, including validation, filters, interceptors, and security.

---

## **2. Setup `MockMvc`**

* Use **`@WebMvcTest`** for **controller slice testing**.
* Autowire `MockMvc`.
* Mock dependencies (services) with **`@MockBean`**.

**Example:**

```java
@WebMvcTest(UserController.class)
class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService; // mock service dependency

    @Test
    void testGetUserById() throws Exception {
        User mockUser = new User(1, "Alice");
        when(userService.getUserById(1)).thenReturn(mockUser);

        mockMvc.perform(get("/users/1"))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.name").value("Alice"));
    }

    @Test
    void testCreateUser() throws Exception {
        User user = new User(2, "Bob");
        when(userService.createUser(any(User.class))).thenReturn(user);

        mockMvc.perform(post("/users")
                .contentType(MediaType.APPLICATION_JSON)
                .content("{\"id\":2,\"name\":\"Bob\"}"))
                .andExpect(status().isCreated())
                .andExpect(jsonPath("$.name").value("Bob"));
    }
}
```

---

## **3. Key Methods in `MockMvc`**

| Method                                           | Purpose                                           |
| ------------------------------------------------ | ------------------------------------------------- |
| `perform(MockHttpServletRequestBuilder request)` | Execute HTTP request (GET, POST, etc.)            |
| `andExpect(ResultMatcher matcher)`               | Assert expected outcome (status, content, header) |
| `andReturn()`                                    | Returns `MvcResult` for further assertions        |
| `jsonPath(String expression)`                    | Extract fields from JSON response                 |

---

## **4. Common Request Builders**

* `get("/url")` → GET request
* `post("/url")` → POST request
* `put("/url")` → PUT request
* `delete("/url")` → DELETE request
* `.content(String json)` → Request body
* `.contentType(MediaType.APPLICATION_JSON)` → Set content type

---

## **5. Advantages of Using MockMvc**

* Tests **only the web layer**, not the entire application.
* Works with **JUnit 5**, Mockito, and Spring Boot test annotations.
* Supports **validation, exception handling**, and **security filters**.
* Fast and **isolated from actual HTTP server**.

---

💡 **Interview Tip:**

> "Use `MockMvc` to simulate HTTP requests to your REST controllers. Combine `@WebMvcTest` and `@MockBean` for controller slice testing, then assert status, headers, and JSON content using `andExpect()`."

---

I can next explain **how to test REST controllers with `@SpringBootTest` vs `@WebMvcTest`**, which is another common interview question.

Do you want me to cover that?

---

## 141. What is @SpringBootTest vs @WebMvcTest?

### **Difference Between `@SpringBootTest` and `@WebMvcTest` in Spring Boot**

Both annotations are used for **testing Spring Boot applications**, but they serve **different purposes** and **load different parts of the application context**.

---

## **1. `@SpringBootTest`**

* **Purpose:** Loads the **full Spring application context** for integration testing.
* **Behavior:**

  * All beans (controllers, services, repositories, etc.) are loaded.
  * Can start the **embedded server** (Tomcat) if required.
  * Suitable for **end-to-end integration tests**.
* **Use Case:** Testing **complete application flow**, including controllers, services, repositories, database access, and configurations.

**Example:**

```java
@SpringBootTest
class UserServiceIntegrationTest {

    @Autowired
    private UserService userService;

    @Test
    void testGetUser() {
        User user = userService.getUserById(1);
        assertEquals("Alice", user.getName());
    }
}
```

* Pros: Full context, real database, real beans.
* Cons: Slower, heavy for small unit tests.

---

## **2. `@WebMvcTest`**

* **Purpose:** Loads **only the web layer** (controllers, `@ControllerAdvice`, filters) for **slice testing**.
* **Behavior:**

  * **Controllers are loaded**, but **services, repositories, and other beans are not** unless explicitly mocked with `@MockBean`.
  * Does **not start the full application** or the embedded server by default.
* **Use Case:** Testing **REST controllers or MVC controllers in isolation**.

**Example:**

```java
@WebMvcTest(UserController.class)
class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService; // mock service dependency

    @Test
    void testGetUser() throws Exception {
        when(userService.getUserById(1)).thenReturn(new User(1, "Alice"));

        mockMvc.perform(get("/users/1"))
               .andExpect(status().isOk())
               .andExpect(jsonPath("$.name").value("Alice"));
    }
}
```

* Pros: Fast, isolates controller layer, easy to mock dependencies.
* Cons: Cannot test service/repository layer or full integration.

---

## **3. Key Differences**

| Feature             | `@SpringBootTest`                     | `@WebMvcTest`                                              |
| ------------------- | ------------------------------------- | ---------------------------------------------------------- |
| **Context Loaded**  | Full application context              | Only web layer (controllers, filters, `@ControllerAdvice`) |
| **Dependencies**    | All beans autowired                   | Services, repositories must be mocked (`@MockBean`)        |
| **Embedded Server** | Can start real server                 | Does not start server by default                           |
| **Use Case**        | Integration testing, end-to-end tests | Unit testing controllers (slice testing)                   |
| **Speed**           | Slower                                | Faster                                                     |

---

💡 **Interview Tip:**

> "`@SpringBootTest` is for full integration tests with the entire Spring context. `@WebMvcTest` is for testing controllers in isolation, using mocks for service/repository layers."

---

I can next explain **how to test services using `@MockBean` and `@InjectMocks` with JUnit and Mockito**, which is another commonly asked scenario.

Do you want me to cover that?

---