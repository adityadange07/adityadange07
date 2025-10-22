# LEVEL 3: ADVANCED (4+ Years Experience)

# Advanced Testing

## 242. What's the difference between unit, integretion, and E2E testing?

Absolutely, Aditya! Let’s break down the **differences between Unit, Integration, and End-to-End (E2E) testing** in a clear, structured way:

---

## **1. Unit Testing**

**Definition:**

* Tests **individual components** or **units** of code (usually a single method or class) in isolation.

**Purpose:**

* Verify that **each component works correctly** on its own.

**Characteristics:**

* **Scope:** Smallest testable units (functions, classes).
* **Dependencies:** Usually **mocked or stubbed** to isolate the unit.
* **Speed:** Very fast.
* **Tools (Java):** JUnit, TestNG, Mockito.

**Example:**

```java
@Test
void testAddNumbers() {
    Calculator calc = new Calculator();
    int result = calc.add(2, 3);
    assertEquals(5, result);
}
```

* Here, only the `add` method is tested independently.

---

## **2. Integration Testing**

**Definition:**

* Tests **multiple components together** to ensure they work correctly as a group.

**Purpose:**

* Verify that **interactions between components** (modules, classes, or services) function as expected.

**Characteristics:**

* **Scope:** Groups of components or subsystems.
* **Dependencies:** Real dependencies may be used (e.g., database, APIs) or partially mocked.
* **Speed:** Slower than unit tests.
* **Tools (Java):** Spring Boot Test, JUnit, Testcontainers, H2 database.

**Example:**

* Test a Spring service that retrieves data from a database:

```java
@SpringBootTest
class UserServiceIntegrationTest {
    
    @Autowired
    UserService userService;

    @Test
    void testGetUserById() {
        User user = userService.getUserById(1L);
        assertNotNull(user);
        assertEquals("Aditya", user.getName());
    }
}
```

* Here, the **service interacts with the database**, testing component integration.

---

## **3. End-to-End (E2E) Testing**

**Definition:**

* Tests the **entire application flow** from start to finish, simulating real user scenarios.

**Purpose:**

* Ensure the **system as a whole works correctly**, including UI, backend, database, and external services.

**Characteristics:**

* **Scope:** Full application or system.
* **Dependencies:** All real components are used (or sometimes in a staging environment).
* **Speed:** Slowest among the three.
* **Tools (Java):** Selenium, Cypress, RestAssured, Cucumber.

**Example:**

* Test a user registration flow in a web app:

  1. Open browser → go to registration page.
  2. Fill form → submit.
  3. Check database → user record created.
  4. Verify confirmation email sent.

---

## **4. Comparison Table**

| Aspect           | Unit Test               | Integration Test                    | End-to-End Test                    |
| ---------------- | ----------------------- | ----------------------------------- | ---------------------------------- |
| **Scope**        | Single class/method     | Multiple components                 | Entire application/system          |
| **Dependencies** | Mocked                  | Real or partially mocked            | Real components and environment    |
| **Speed**        | Fast                    | Moderate                            | Slow                               |
| **Purpose**      | Verify individual logic | Verify interactions between modules | Verify complete workflow for users |
| **Example**      | Testing `add()` method  | Service fetching data from DB       | User registration flow in web app  |

---

💡 **Analogy:**

* **Unit Test:** Check if one gear in a machine works.
* **Integration Test:** Check if several connected gears turn smoothly together.
* **E2E Test:** Turn the whole machine on and see if it performs the full task correctly.

---

If you want, I can also **draw a visual diagram showing Unit → Integration → E2E testing hierarchy**, which is very interview-friendly.

Do you want me to create that diagram?

---

## 243. How do you mock external RESt APIs in tests?

Absolutely, Aditya! Mocking external REST APIs is crucial for **unit and integration testing** to avoid calling real services, which can be slow, unreliable, or have side effects. Here’s a detailed explanation with approaches and examples in **Java/Spring Boot**:

---

## **1. Why Mock External APIs?**

* Avoid **network calls** during tests.
* Ensure **predictable responses**.
* Test your **application logic independently** of external systems.
* Simulate **edge cases** like timeouts, errors, or unusual responses.

---

## **2. Approaches to Mock External APIs**

### **A. Using Mockito / Mocking RestTemplate**

* If your service uses `RestTemplate` to call an API:

```java
@Service
public class UserService {
    private final RestTemplate restTemplate;

    public UserService(RestTemplate restTemplate) {
        this.restTemplate = restTemplate;
    }

    public String getUserName(Long id) {
        String url = "https://external-api.com/users/" + id;
        ResponseEntity<User> response = restTemplate.getForEntity(url, User.class);
        return response.getBody().getName();
    }
}
```

**Test with Mockito:**

```java
@SpringBootTest
class UserServiceTest {

    @Mock
    private RestTemplate restTemplate;

    @InjectMocks
    private UserService userService;

    @Test
    void testGetUserName() {
        User mockUser = new User(1L, "Aditya");
        ResponseEntity<User> response = new ResponseEntity<>(mockUser, HttpStatus.OK);

        Mockito.when(restTemplate.getForEntity(
                "https://external-api.com/users/1", User.class))
               .thenReturn(response);

        String name = userService.getUserName(1L);
        assertEquals("Aditya", name);
    }
}
```

✅ **Advantages:** Simple, works well for **unit tests**, fully isolated.

---

### **B. Using MockWebServer (from OkHttp)**

* Useful for **integration-style tests** or when you want to simulate a real HTTP server.

```java
MockWebServer mockServer = new MockWebServer();
mockServer.start();

mockServer.enqueue(new MockResponse()
        .setBody("{\"id\":1,\"name\":\"Aditya\"}")
        .addHeader("Content-Type", "application/json"));

String baseUrl = mockServer.url("/users/1").toString();
RestTemplate restTemplate = new RestTemplate();
ResponseEntity<User> response = restTemplate.getForEntity(baseUrl, User.class);

assertEquals("Aditya", response.getBody().getName());

mockServer.shutdown();
```

✅ **Advantages:** Simulates a real HTTP server, supports **response delays, errors, and multiple endpoints**.

---

### **C. Using WireMock**

* **WireMock** runs a local server and stubs HTTP endpoints.
* Great for **integration tests and contract testing**.

**Example:**

```java
@ExtendWith(SpringExtension.class)
@SpringBootTest
@AutoConfigureWireMock(port = 8089)
class UserServiceWireMockTest {

    @Autowired
    private UserService userService;

    @Test
    void testGetUserName() {
        stubFor(get(urlEqualTo("/users/1"))
                .willReturn(aResponse()
                        .withHeader("Content-Type", "application/json")
                        .withBody("{\"id\":1,\"name\":\"Aditya\"}")));

        String name = userService.getUserName(1L);
        assertEquals("Aditya", name);
    }
}
```

✅ **Advantages:**

* Supports **complex scenarios**: delays, errors, stateful responses.
* Can **reuse stubs across tests**.
* Closer to real API behavior.

---

### **D. Using @RestClientTest (Spring Boot)**

* Lightweight **Spring Boot slice test** for REST clients:

```java
@RestClientTest(UserService.class)
class UserServiceRestClientTest {

    @Autowired
    private UserService userService;

    @Autowired
    private MockRestServiceServer server;

    @Test
    void testGetUserName() {
        server.expect(requestTo("https://external-api.com/users/1"))
              .andRespond(withSuccess("{\"id\":1,\"name\":\"Aditya\"}", MediaType.APPLICATION_JSON));

        String name = userService.getUserName(1L);
        assertEquals("Aditya", name);
    }
}
```

✅ **Advantages:** Tight integration with Spring, auto-configures `RestTemplate` or `WebClient`.

---

## **3. Best Practices**

1. **Unit Tests:** Use **Mockito** to mock the client (`RestTemplate`/`WebClient`).
2. **Integration Tests:** Use **MockWebServer or WireMock** for realistic HTTP interactions.
3. **E2E Tests:** Use **WireMock** or a **staging environment** for external API calls.
4. **Simulate Failures:** Test **timeouts, 5xx errors, malformed responses**.
5. **Keep Tests Fast:** Avoid calling the real external API in automated tests.

---

💡 **Analogy:**

* Mocking external APIs = **pretend the delivery guy is at the door**, so you can test your app logic without waiting for the real delivery.

---

If you want, I can also **create a diagram showing how RestTemplate/WebClient calls are intercepted and mocked** for tests—very handy for interviews.

Do you want me to create that diagram?

---

## 244. What are TestContainers? How to use with Spring Boot?

Absolutely, Aditya! Let’s break down **Testcontainers** and how it’s used with **Spring Boot** step by step.

---

## **1. What are Testcontainers?**

**Testcontainers** is a **Java library** that allows you to **run lightweight, throwaway instances of Docker containers** for your tests.

* Ideal for **integration testing** with databases, message brokers, or any service your app depends on.
* Ensures your tests **run against real services** instead of mocks.

**Key Features:**

* Supports **any Docker container**.
* Works with **JUnit 4/5, Spock, and Spring Boot**.
* Automatically manages **container lifecycle** (start, stop, cleanup).
* Provides **dynamic ports, logs, and wait strategies**.

---

## **2. Why Use Testcontainers?**

* Realistic testing against **Postgres, MySQL, Kafka, Redis, MongoDB**, etc.
* Avoids **dependency on local or shared environments**.
* **Reproducible tests** for CI/CD pipelines.
* Works well for **integration and end-to-end testing**.

---

## **3. How Testcontainers Works**

1. You define a **container** in your test.
2. Testcontainers **pulls the image** (if not available).
3. Container starts **on a random free port**.
4. Your application uses the container for testing.
5. Container is **stopped automatically** after tests.

---

## **4. Example: Spring Boot + PostgreSQL**

**Step 1: Add Dependency**

```xml
<dependency>
    <groupId>org.testcontainers</groupId>
    <artifactId>postgresql</artifactId>
    <version>1.20.3</version>
    <scope>test</scope>
</dependency>
<dependency>
    <groupId>org.testcontainers</groupId>
    <artifactId>junit-jupiter</artifactId>
    <version>1.20.3</version>
    <scope>test</scope>
</dependency>
```

---

**Step 2: Create Test with Container**

```java
@SpringBootTest
@Testcontainers
class UserRepositoryIntegrationTest {

    @Container
    static PostgreSQLContainer<?> postgresContainer = new PostgreSQLContainer<>("postgres:15")
            .withDatabaseName("testdb")
            .withUsername("test")
            .withPassword("test");

    @Autowired
    private UserRepository userRepository;

    @DynamicPropertySource
    static void properties(DynamicPropertyRegistry registry) {
        registry.add("spring.datasource.url", postgresContainer::getJdbcUrl);
        registry.add("spring.datasource.username", postgresContainer::getUsername);
        registry.add("spring.datasource.password", postgresContainer::getPassword);
    }

    @Test
    void testSaveAndFindUser() {
        User user = new User();
        user.setName("Aditya");
        userRepository.save(user);

        User fetchedUser = userRepository.findById(user.getId()).orElseThrow();
        assertEquals("Aditya", fetchedUser.getName());
    }
}
```

**Explanation:**

* `@Container` → Defines a Testcontainer instance.
* `DynamicPropertySource` → Injects container JDBC URL into Spring Boot.
* Test runs against a **real PostgreSQL instance in a Docker container**.

---

## **5. Using Testcontainers for Kafka / Redis / Elasticsearch**

```java
// Kafka example
@Container
static KafkaContainer kafka = new KafkaContainer(DockerImageName.parse("confluentinc/cp-kafka:7.5.0"));
```

* Works the same way: container starts, app connects dynamically, container stops after tests.

---

## **6. Advantages over Traditional Mocks**

| Mocking                     | Testcontainers                                  |
| --------------------------- | ----------------------------------------------- |
| Fast, simple                | Slightly slower, but real environment           |
| May not catch config issues | Catches real configuration & environment issues |
| Cannot test actual protocol | Uses real TCP/HTTP/DB protocols                 |
| Not suitable for E2E tests  | Perfect for integration & E2E tests             |

---

💡 **Analogy:**

* Mocks = **pretend Lego blocks**, fast but not real.
* Testcontainers = **real Lego pieces**, slower but you see exactly how it works.

---

If you want, I can also **draw a diagram showing Spring Boot test connecting to a Testcontainer DB or Kafka instance**, which is very interview-friendly.

Do you want me to create that diagram?

---

## 245. How do you write parameterized tests to JUnit5?

Absolutely, Aditya! Let’s go step by step on **writing parameterized tests in JUnit 5**, which are very useful for running the same test logic with **different inputs**.

---

## **1. What is a Parameterized Test?**

* A **parameterized test** allows you to **run the same test multiple times** with different arguments.
* Reduces **code duplication** and improves test coverage.

**Annotation used:** `@ParameterizedTest` (JUnit 5, `junit-jupiter`)

---

## **2. Common Sources of Parameters**

| Source Annotation  | Description                                             |
| ------------------ | ------------------------------------------------------- |
| `@ValueSource`     | Single array of literals (int, double, string, etc.)    |
| `@EnumSource`      | All or selected constants from an Enum                  |
| `@CsvSource`       | Comma-separated values for multiple parameters per test |
| `@CsvFileSource`   | CSV file as parameter source                            |
| `@MethodSource`    | Static or instance method returns a Stream of arguments |
| `@ArgumentsSource` | Custom argument provider                                |

---

## **3. Examples**

### **A. Using @ValueSource**

```java
@ParameterizedTest
@ValueSource(ints = {2, 4, 6, 8})
void testEvenNumbers(int number) {
    assertTrue(number % 2 == 0);
}
```

* Test runs **4 times**, once for each number.

---

### **B. Using @EnumSource**

```java
enum Color { RED, GREEN, BLUE }

@ParameterizedTest
@EnumSource(Color.class)
void testColors(Color color) {
    assertNotNull(color);
}
```

---

### **C. Using @CsvSource**

```java
@ParameterizedTest
@CsvSource({
    "1, 2, 3",
    "2, 3, 5",
    "5, 7, 12"
})
void testAddition(int a, int b, int expectedSum) {
    assertEquals(expectedSum, a + b);
}
```

* Supports **multiple arguments per test**.

---

### **D. Using @CsvFileSource**

* Useful when you have many test cases in a CSV file (`test-data.csv`):

```csv
1,2,3
2,3,5
5,7,12
```

```java
@ParameterizedTest
@CsvFileSource(resources = "/test-data.csv", numLinesToSkip = 0)
void testAdditionFromCSV(int a, int b, int expectedSum) {
    assertEquals(expectedSum, a + b);
}
```

---

### **E. Using @MethodSource**

* Provides **dynamic test data** via a method:

```java
static Stream<Arguments> provideNumbersForAddition() {
    return Stream.of(
        Arguments.of(1, 2, 3),
        Arguments.of(2, 3, 5),
        Arguments.of(5, 7, 12)
    );
}

@ParameterizedTest
@MethodSource("provideNumbersForAddition")
void testAdditionWithMethodSource(int a, int b, int expectedSum) {
    assertEquals(expectedSum, a + b);
}
```

---

### **4. Advantages of Parameterized Tests**

* Avoids **repetition** in test code.
* **Easily extendable** by adding more parameters.
* Works with **JUnit 5 assertions and dynamic data sources**.
* Can be combined with **mocking** for complex scenarios.

---

💡 **Analogy:**

* Think of parameterized tests as **a single recipe you cook multiple times with different ingredients**—you’re testing the recipe logic, not each ingredient individually.

---

If you want, I can also **create a diagram showing how JUnit 5 parameterized tests run with multiple inputs**, which is very **interview-friendly**.

Do you want me to create that diagram?

---

## 246. What is the role of @DataJpaTest, @WebMvcTest, @SpringBootTest?

Absolutely, Aditya! Let’s break down the **role of @DataJpaTest, @WebMvcTest, and @SpringBootTest** in **Spring Boot testing**, which is essential for writing effective tests.

---

## **1. @DataJpaTest**

**Purpose:**

* Used for **testing JPA repositories** (database layer) in isolation.

**Characteristics:**

* Loads **only JPA-related components** (`@Entity`, `@Repository`).
* Configures **in-memory database** by default (H2, HSQLDB, Derby).
* Does **not load full Spring context** (faster than `@SpringBootTest`).
* Useful for **unit or integration tests of repositories**.

**Example:**

```java
@DataJpaTest
class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    void testSaveAndFindUser() {
        User user = new User();
        user.setName("Aditya");
        userRepository.save(user);

        User fetchedUser = userRepository.findById(user.getId()).orElseThrow();
        assertEquals("Aditya", fetchedUser.getName());
    }
}
```

✅ **Key point:** Only **JPA layer is loaded**, controllers and services are ignored.

---

## **2. @WebMvcTest**

**Purpose:**

* Used for **testing Spring MVC controllers** in isolation.

**Characteristics:**

* Loads **only controller layer** and related MVC components (`@Controller`, `@RestController`, `@ControllerAdvice`).
* Does **not load full Spring context** (faster).
* Use **MockMvc** to test HTTP requests/responses.
* Other beans like services or repositories need to be **mocked manually** using `@MockBean`.

**Example:**

```java
@WebMvcTest(UserController.class)
class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService;

    @Test
    void testGetUser() throws Exception {
        User user = new User(1L, "Aditya");
        Mockito.when(userService.getUserById(1L)).thenReturn(user);

        mockMvc.perform(get("/users/1"))
               .andExpect(status().isOk())
               .andExpect(jsonPath("$.name").value("Aditya"));
    }
}
```

✅ **Key point:** Only **web layer is loaded**, other dependencies are **mocked**.

---

## **3. @SpringBootTest**

**Purpose:**

* Used for **full integration tests** by loading the **entire Spring Boot context**.

**Characteristics:**

* Starts **all beans**, including controllers, services, repositories, configurations.
* Can start **embedded server** if needed (`webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT`).
* Slower than slice tests (`@DataJpaTest`, `@WebMvcTest`) but **tests full app behavior**.
* Useful for **end-to-end integration tests**.

**Example:**

```java
@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
class UserIntegrationTest {

    @Autowired
    private TestRestTemplate restTemplate;

    @Test
    void testGetUser() {
        ResponseEntity<User> response = restTemplate.getForEntity("/users/1", User.class);
        assertEquals(HttpStatus.OK, response.getStatusCode());
        assertEquals("Aditya", response.getBody().getName());
    }
}
```

✅ **Key point:** **Full Spring context is loaded**, suitable for **integration or end-to-end tests**.

---

## **4. Comparison Table**

| Annotation        | Scope                    | Beans Loaded                    | Database  | Use Case                  | Speed |
| ----------------- | ------------------------ | ------------------------------- | --------- | ------------------------- | ----- |
| `@DataJpaTest`    | Repository / JPA layer   | Only JPA components             | In-memory | Testing repositories      | Fast  |
| `@WebMvcTest`     | Web / Controller layer   | Controllers + MVC related beans | No        | Testing controllers       | Fast  |
| `@SpringBootTest` | Full application context | All beans                       | Optional  | Integration / E2E testing | Slow  |

---

💡 **Analogy:**

* **@DataJpaTest** → Test **just the engine** of a car.
* **@WebMvcTest** → Test **just the steering and controls**.
* **@SpringBootTest** → Test **the whole car in real driving conditions**.

---

If you want, I can also **create a diagram showing these three annotations and which layers of Spring Boot they load**, which is **interview-friendly and easy to remember**.

Do you want me to create that diagram?

---

## 247. How do you implement test data builders and object mothers?

Absolutely, Aditya! Let’s go step by step on **implementing Test Data Builders and Object Mothers** in Java, which are very useful for writing **clean, maintainable tests** with complex objects.

---

## **1. Why Use Test Data Builders / Object Mothers?**

* Tests often require **complex objects with many fields**.
* Creating objects directly in tests leads to **verbose and repetitive code**.
* **Test Data Builder** & **Object Mother** patterns help **centralize object creation** and improve **readability**.

---

## **2. Test Data Builder Pattern**

**Definition:**

* A **builder class** that provides a **fluent API** to construct test objects.
* Makes tests **readable, flexible, and maintainable**.

**Example:**

Assume we have a `User` entity:

```java
public class User {
    private Long id;
    private String name;
    private int age;
    private String email;

    // getters, setters, constructors
}
```

**Create a Builder:**

```java
public class UserBuilder {
    private Long id = 1L;
    private String name = "Default Name";
    private int age = 25;
    private String email = "default@example.com";

    public UserBuilder withId(Long id) {
        this.id = id;
        return this;
    }

    public UserBuilder withName(String name) {
        this.name = name;
        return this;
    }

    public UserBuilder withAge(int age) {
        this.age = age;
        return this;
    }

    public UserBuilder withEmail(String email) {
        this.email = email;
        return this;
    }

    public User build() {
        return new User(id, name, age, email);
    }
}
```

**Usage in Test:**

```java
@Test
void testUserCreation() {
    User user = new UserBuilder()
                    .withName("Aditya")
                    .withAge(30)
                    .build();

    assertEquals("Aditya", user.getName());
    assertEquals(30, user.getAge());
}
```

✅ **Advantages:**

* Avoids **duplicated object creation code**.
* **Fluent API** makes tests readable.
* Can **set only the fields you care about**, defaults used for others.

---

## **3. Object Mother Pattern**

**Definition:**

* A class that **centralizes creation of test objects** with **predefined variations**.
* Often used for **common objects used across multiple tests**.

**Example:**

```java
public class UserMother {

    public static User defaultUser() {
        return new User(1L, "Default Name", 25, "default@example.com");
    }

    public static User adminUser() {
        return new User(2L, "Admin", 35, "admin@example.com");
    }

    public static User guestUser() {
        return new User(3L, "Guest", 20, "guest@example.com");
    }
}
```

**Usage in Test:**

```java
@Test
void testDefaultUser() {
    User user = UserMother.defaultUser();
    assertEquals("Default Name", user.getName());
}

@Test
void testAdminUser() {
    User user = UserMother.adminUser();
    assertEquals("Admin", user.getName());
}
```

✅ **Advantages:**

* Centralizes **common test data**.
* Easy to **reuse across multiple tests**.
* Simplifies test setup.

---

## **4. Test Data Builder vs Object Mother**

| Aspect      | Test Data Builder                    | Object Mother                      |
| ----------- | ------------------------------------ | ---------------------------------- |
| Flexibility | High (customize fields per test)     | Low (predefined objects)           |
| Reusability | Moderate (per test object)           | High (common objects across tests) |
| Readability | Fluent API                           | Simple method calls                |
| Use Case    | Complex objects with variable fields | Standard test objects              |

---

## **5. Best Practices**

1. Use **Test Data Builder** for objects with **many optional fields**.
2. Use **Object Mother** for **common or default objects** reused across tests.
3. Combine both: **Object Mother returns builders** for maximum flexibility.

**Example Hybrid:**

```java
public class UserMother {
    public static UserBuilder defaultUser() {
        return new UserBuilder()
                    .withId(1L)
                    .withName("Default Name")
                    .withAge(25)
                    .withEmail("default@example.com");
    }
}

// Test
User user = UserMother.defaultUser().withName("Aditya").build();
```

✅ This gives you **best of both worlds**.

---

💡 **Analogy:**

* **Builder** → “I want to build my own Lego figure, piece by piece.”
* **Object Mother** → “Here’s a ready-made Lego figure you can use.”

---

If you want, I can also **draw a diagram showing Test Data Builder and Object Mother workflow** which is **interview-friendly** and easy to remember.

Do you want me to create that diagram?

---

## 248. What is contract testing? Pact framework?

Absolutely, Aditya! Let’s go step by step on **Contract Testing** and the **Pact framework**, which are essential for testing microservices communication.

---

## **1. What is Contract Testing?**

**Definition:**

* **Contract Testing** ensures that two services (typically a **consumer** and a **provider**) can communicate correctly.
* It verifies that the **API contract** agreed upon by both services is honored.

**Key Idea:**

* Consumer defines **what it expects** (request/response).
* Provider tests whether it **fulfills those expectations**.
* Helps catch **integration issues before runtime**.

**When to use:**

* Microservices communicating over **HTTP/REST** or **message queues**.
* When **integration tests are expensive or slow**.

---

### **2. Types of Contract Testing**

| Type                | Description                                               |
| ------------------- | --------------------------------------------------------- |
| **Consumer-driven** | Consumer defines the contract; provider tests against it. |
| **Provider-driven** | Provider defines the contract; consumers adapt.           |

---

## **3. What is Pact Framework?**

**Definition:**

* **Pact** is a **consumer-driven contract testing framework**.
* Written for **microservices testing** across languages.
* Ensures **provider service meets the consumer’s expectations**.

**Workflow:**

1. **Consumer writes a contract (Pact file)** → specifies request/response expectations.
2. **Provider tests against the Pact file** → verifies API meets the contract.
3. Pact can be **shared via files or a Pact Broker**.

---

## **4. How Pact Works**

### **Step 1: Consumer Test**

```java
@ExtendWith(PactConsumerTestExt.class)
class UserServiceConsumerTest {

    @Pact(consumer = "UserServiceConsumer", provider = "UserServiceProvider")
    public RequestResponsePact createPact(PactDslWithProvider builder) {
        return builder
            .uponReceiving("A request for user with ID 1")
            .path("/users/1")
            .method("GET")
            .willRespondWith()
            .status(200)
            .body("{\"id\":1,\"name\":\"Aditya\"}")
            .toPact();
    }

    @Test
    @PactTestFor(pactMethod = "createPact")
    void testGetUser(MockServer mockServer) {
        User user = new UserClient(mockServer.getUrl()).getUserById(1);
        assertEquals("Aditya", user.getName());
    }
}
```

* Pact file is generated after this test.
* It contains **request/response expectations**.

---

### **Step 2: Provider Test**

```java
@Provider("UserServiceProvider")
@PactFolder("pacts")
class UserServiceProviderTest {

    @TestTemplate
    @ExtendWith(PactVerificationInvocationContextProvider.class)
    void pactVerificationTestTemplate(PactVerificationContext context) {
        context.verifyInteraction();
    }
}
```

* Provider reads the Pact file and **verifies it can satisfy the consumer contract**.

---

## **5. Advantages of Contract Testing**

* Catches **integration issues early**.
* **Independent testing** of microservices without running full system.
* Reduces **end-to-end test complexity**.
* Provides **clear documentation** of APIs.

---

## **6. Consumer vs Provider in Pact**

| Role     | Responsibility                             |
| -------- | ------------------------------------------ |
| Consumer | Defines the contract (what it expects)     |
| Provider | Tests and ensures it fulfills the contract |

---

💡 **Analogy:**

* Consumer: “I expect my coffee with 2 sugars.”
* Provider: “Let me check I can make coffee with exactly 2 sugars.”
* Pact ensures **no surprises when the consumer orders coffee**.

---

If you want, I can also **draw a diagram showing Pact workflow: Consumer → Pact file → Provider → Verification**, which is very **interview-friendly**.

Do you want me to create that diagram?

---

## 249. How do you implement perfoemance testing?

Absolutely, Aditya! Let’s go step by step on **implementing performance testing** for Java/Spring Boot applications, including tools, strategies, and best practices.

---

## **1. What is Performance Testing?**

**Definition:**
Performance testing measures how a system behaves under **expected or peak load**, focusing on:

* **Response time** – How fast APIs respond.
* **Throughput** – Number of requests the system can handle per unit time.
* **Resource utilization** – CPU, memory, threads, database connections.

**Goal:**

* Identify **bottlenecks** before production.
* Ensure **system stability under load**.

---

## **2. Types of Performance Testing**

| Type                         | Description                                             |
| ---------------------------- | ------------------------------------------------------- |
| **Load Testing**             | Test system under **expected load**                     |
| **Stress Testing**           | Test system under **extreme load**                      |
| **Spike Testing**            | Test system under **sudden load spikes**                |
| **Endurance / Soak Testing** | Test system under **continuous load** for long duration |
| **Scalability Testing**      | Determine how system **scales** with increased load     |

---

## **3. Tools for Performance Testing**

### **Popular Tools:**

1. **JMeter**

   * Open-source, GUI and CLI, supports HTTP, SOAP, JDBC, Kafka, etc.
   * Can simulate thousands of users and analyze metrics.

2. **Gatling**

   * Scala-based, good for **HTTP API testing**, supports detailed reports.

3. **Locust**

   * Python-based, distributed load testing, easy for scripting scenarios.

4. **Spring Boot Actuator + Metrics**

   * Monitor response times, memory, and threads during load tests.

5. **Profilers**

   * Tools like **VisualVM, YourKit, JProfiler** to analyze **CPU and memory usage**.

---

## **4. Steps to Implement Performance Testing**

### **Step 1: Identify Critical Scenarios**

* Choose **high-traffic endpoints** or **business-critical flows**.
* Example: `/api/login`, `/api/bookAppointment`, `/api/payment`.

---

### **Step 2: Define Performance Goals**

* **Response time:** < 500ms for 95% of requests
* **Throughput:** 1000 requests/sec
* **Resource usage:** CPU < 80%, Memory < 70%

---

### **Step 3: Prepare Test Data**

* Use **realistic datasets** in the database.
* Use **Test Data Builders / Object Mothers** for generating mock data.

---

### **Step 4: Write Test Scripts**

#### **JMeter Example:**

1. Create a **Thread Group** → simulates concurrent users.
2. Add **HTTP Request Sampler** → call REST endpoints.
3. Add **Listeners** → View Results Tree, Aggregate Report.
4. Run **load test** and capture metrics.

#### **Gatling Example:**

```scala
class UserSimulation extends Simulation {

  val httpConf = http.baseUrl("http://localhost:8080")

  val scn = scenario("Load Test Login")
    .exec(http("Login Request")
    .get("/api/login")
    .check(status.is(200)))

  setUp(
    scn.inject(atOnceUsers(1000))
  ).protocols(httpConf)
}
```

* **Inject users gradually or all at once**.

---

### **Step 5: Monitor Metrics**

* **Spring Boot Actuator + Micrometer**

  * `/actuator/metrics` → response times, DB connections, memory.
* **JVM Profiling** → CPU, heap, GC behavior.
* **Database Monitoring** → slow queries, connection pool usage.

---

### **Step 6: Analyze Results**

* Check for **bottlenecks**:

  * Slow APIs → optimize queries or caching.
  * High CPU → check loops or algorithms.
  * High memory → check object creation, leaks, GC tuning.
* Compare results with **performance goals**.

---

### **Step 7: Optimize & Retest**

* Implement **caching, async processing, connection pooling, indexing**.
* Retest to verify improvements.

---

## **5. Best Practices**

1. **Test in an environment similar to production**.
2. **Start small and gradually increase load**.
3. **Use realistic test data**.
4. **Monitor server, JVM, and database metrics simultaneously**.
5. **Automate load tests** in CI/CD pipelines if possible.

---

💡 **Analogy:**

* Performance testing is like **stress-testing a bridge** with cars. You check how much weight it can handle **safely** and identify weak points before opening it to the public.

---

If you want, I can also **create a visual workflow showing Performance Testing steps with JMeter/Gatling + Spring Boot monitoring**, which is **very interview-friendly**.

Do you want me to create that diagram?

---

## 250. What is mutation testing?

Absolutely, Aditya! Let’s go step by step on **mutation testing**, an advanced testing technique that is gaining popularity for improving test quality.

---

## **1. What is Mutation Testing?**

**Definition:**

* Mutation testing is a **technique to evaluate the effectiveness of your unit tests**.
* It works by **making small changes (mutations) to your source code** and checking if your tests **catch the errors**.

**Goal:**

* Identify **weak tests** that may not catch bugs.
* Improve **code coverage quality**, not just quantity.

---

### **How it Works:**

1. **Mutants Creation**

   * A tool makes **small changes to your code**, called **mutants**.
   * Example mutations:

     * Replace `+` with `-`
     * Change `>` to `<`
     * Replace `true` with `false`

2. **Run Tests**

   * Your unit tests are executed against each mutant.

3. **Check Detection**

   * If a test **fails**, the mutant is considered **killed** → test is effective.
   * If a test **passes**, the mutant **survives** → test is weak, needs improvement.

---

## **2. Example**

Suppose we have this method:

```java
public int add(int a, int b) {
    return a + b;
}
```

**Mutation:** Change `+` to `-`

```java
public int add(int a, int b) {
    return a - b;  // mutant
}
```

**Unit Test:**

```java
@Test
void testAdd() {
    assertEquals(5, calculator.add(2, 3));
}
```

* If test fails → mutant is **killed** ✅
* If test passes → mutant **survives**, test is **not robust** ❌

---

## **3. Mutation Testing Tools for Java**

| Tool       | Description                                                            |
| ---------- | ---------------------------------------------------------------------- |
| **Pitest** | Most popular Java mutation testing tool. Integrates with Maven/Gradle. |
| **Jester** | Older Java tool, less maintained.                                      |
| **Major**  | Mutation testing for Java bytecode.                                    |

---

### **Pitest Example (Maven)**

**pom.xml dependency:**

```xml
<plugin>
    <groupId>org.pitest</groupId>
    <artifactId>pitest-maven</artifactId>
    <version>1.11.12</version>
</plugin>
```

**Run Mutation Tests:**

```bash
mvn org.pitest:pitest-maven:mutationCoverage
```

**Result:**

* Shows **mutation score** = percentage of mutants killed
* Highlights **surviving mutants** → areas where tests are weak

---

## **4. Advantages**

* Ensures **tests catch real bugs**, not just code coverage.
* Improves **test quality and reliability**.
* Highlights **gaps in test cases**.

---

## **5. Best Practices**

1. Use mutation testing on **critical modules** first.
2. Combine with **unit tests and integration tests**.
3. Don’t overuse on **huge codebases** (can be slow).
4. Focus on **surviving mutants** to improve test coverage.

---

💡 **Analogy:**

* Mutation testing is like a **simulated attack on your code** to see if your “defense” (unit tests) can catch the intruder.
* If your tests fail to catch the “attacker,” your tests are **weak** and need improvement.

---

If you want, I can also **create a diagram showing Mutation Testing workflow: Original Code → Mutants → Test Run → Mutant Killed/Survived**, which is **very interview-friendly**.

Do you want me to create that diagram?

---