
## 701. What is unit testing?

**Answer:**
**Unit Testing** is a software testing method where individual units or components of a software are tested (in isolation) to validate that each unit performs as expected.
*   **Unit:** The smallest testable part of an application (e.g., a single method or class).
*   **Goal:** Isolate each part of the program and show that the individual parts are correct.

---

## 702. What is JUnit?

**Answer:**
**JUnit** is a unit testing framework for the Java programming language.
*   **Role:** Provides annotations and assertions to write and run repeatable tests.
*   **Integration:** Works with build tools (Maven, Gradle) and IDEs (IntelliJ, Eclipse).

---

## 703. JUnit 4 vs JUnit 5?

**Answer:**
*   **Architecture:** JUnit 5 = Platform + Jupiter (New API) + Vintage (Backwards compatibility).
*   **Annotations:**
    *   `@Before` -> `@BeforeEach`
    *   `@After` -> `@AfterEach`
    *   `@BeforeClass` -> `@BeforeAll`
    *   `@Ignore` -> `@Disabled`
*   **Features:** JUnit 5 supports Lambda expressions, nested tests, and dynamic tests.

---

## 704. What is @Test annotation?

**Answer:**
**`@Test`** marks a method as a test method.
*   **JUnit 4:** `org.junit.Test`.
*   **JUnit 5:** `org.junit.jupiter.api.Test`.
*   **Behavior:** The test runner executes any method annotated with `@Test`.

---

## 705. What is @BeforeEach and @AfterEach?

**Answer:**
*   **`@BeforeEach`:** Executed **before** each test method (e.g., setting up fresh data/mocks). Replaces `@Before`.
*   **`@AfterEach`:** Executed **after** each test method (e.g., cleaning up resources). Replaces `@After`.

---

## 706. What is parameterized test?

**Answer:**
Allows running the same test method multiple times with different arguments.
*   **Annotation:** `@ParameterizedTest` (JUnit 5).
*   **Source:** `@ValueSource`, `@CsvSource`, `@MethodSource`.
*   **Example:** Testing a `isPrime(int n)` method with values 2, 3, 5, 7, 11.

---

## 707. What is assertion?

**Answer:**
**Assertions** accept a boolean condition and throw an error if the condition is false (stopping the test).
*   **Class:** `org.junit.jupiter.api.Assertions`.
*   **Methods:** `assertEquals()`, `assertTrue()`, `assertNotNull()`, `assertThrows()` (Check for exceptions).

---

## 708. What is Mockito?

**Answer:**
**Mockito** is a mocking framework for unit tests in Java.
*   **Goal:** Simulate the behavior of dependencies (e.g., Database, External API) so you can test your service logic in isolation.
*   **Concept:** "Don't access the real DB, just pretend the DB returned this User."

---

## 709. What is @Mock and @InjectMocks?

**Answer:**
*   **`@Mock`:** Creates a mock object (dummy dependency). e.g., `UserRepository`.
*   **`@InjectMocks`:** Creates an instance of the class under test and injects the mocks into it. e.g., `UserService`.
*   **Usage:**
    ```java
    @Mock UserRepository userRepo;
    @InjectMocks UserService userService; // userService.userRepo will be the mock
    ```

---

## 710. What is stubbing?

**Answer:**
**Stubbing** defines the behavior of a mock object.
*   **Syntax:** `when(mock.method()).thenReturn(value);`
*   **Example:**
    ```java
    when(userRepo.findById(1)).thenReturn(Optional.of(new User("Alice")));
    ```
*   **Verification:** `verify(mock).method();` ensures a method was called.

---

## 711. What is verify in Mockito?

**Answer:**
**`verify()`** checks that a method was called with specific arguments on a mock object.
*   **Usage:** `verify(mock).save(user);`
*   **Counts:** `verify(mock, times(2)).call();`, `verify(mock, never()).call();`.
*   **Goal:** Ensure side effects (like sending email, saving to DB) happened.

---

## 712. What is spy vs mock?

**Answer:**
*   **Mock:** A completely dummy object. Methods do nothing (return null/default) unless stubbed.
    *   `@Mock`
*   **Spy:** A wrapper around a **real** object. Spies call real methods unless specifically stubbed.
    *   `@Spy`
    *   **Use Case:** Test a method of a class while mocking other methods of the **same** class.

---

## 713. What is BDD testing?

**Answer:**
**Behavior-Driven Development (BDD)** focuses on the behavior of the application from the end-user's perspective.
*   **Language:** Gherkin (Given, When, Then).
*   **Frameworks:** Cucumber, JBehave.
*   **Goal:** Collaboration between developers, QA, and business stakeholders.

---

## 714. What is TDD?

**Answer:**
**Test-Driven Development (TDD)** is a development process where you write tests **before** writing the actual code.
*   **Cycle:** Red (Write failing test) -> Green (Write minimal code to pass) -> Refactor (Clean up code).
*   **Benefit:** High test coverage, cleaner design, confidence in refactoring.

---

## 715. What is test coverage?

**Answer:**
**Test Coverage** is a metric that measures the amount of code executed by your tests.
*   **Types:** Line coverage, Method coverage, Branch coverage.
*   **Goal:** Identify untested parts of the application. High coverage != Bug-free code.

---

## 716. What is code coverage tools?

**Answer:**
Tools that generate coverage reports during the build process.
*   **Java:** JaCoCo (Java Code Coverage), Cobertura.
*   **Integration:** SonarQube visualizes coverage and sets quality gates (e.g., "Fail build if coverage < 80%").

---

## 717. What is branch coverage?

**Answer:**
**Branch Coverage** checks whether every execution path (branch) in a control structure (if, switch, loops) has been executed.
*   **Example:** For `if (A && B)`, verify tests cover:
    1.  A=true, B=true
    2.  A=false
    3.  A=true, B=false
*   **Significance:** Stronger metric than line coverage.

---

## 718. What is mutation testing?

**Answer:**
**Mutation Testing** evaluates the quality of your **tests** (not code) by introducing small bugs (mutations) into the code and checking if tests fail.
*   **Concept:** If a test passes despite a bug, the test is weak.
*   **Tool:** PITest (PIT).

---

## 719. What is integration testing?

**Answer:**
**Integration Testing** verifies that different modules or services work together correctly.
*   **Scope:** Larger than unit tests. Includes DB, Message Queues, External APIs (often using TestContainers).
*   **Speed:** Slower than unit tests.

---

## 720. What is @SpringBootTest?

**Answer:**
**`@SpringBootTest`** is an annotation for Spring Boot integration tests.
*   **Behavior:** Starts up the full Spring ApplicationContext (Ioc Container).
*   **Usage:** Used to test the interaction between multiple beans or the entire application flow.
*   **Web Environment:** Can mimic a web server using `webEnvironment = WebEnvironment.MOCK` or `RANDOM_PORT`.

---

## 721. What is @WebMvcTest?

**Answer:**
**`@WebMvcTest`** is a specialized test annotation for testing the Spring MVC Controller layer.
*   **Behavior:** Only scans for the Controller and related components (`@ControllerAdvice`, `Converter`, `Filter`). Access to Service/Repository layers must be mocked.
*   **Speed:** Faster than `@SpringBootTest` as it doesn't load whole context.

---

## 722. What is @DataJpaTest?

**Answer:**
**`@DataJpaTest`** is a specialized test annotation for testing the Persistence/Repository layer.
*   **Behavior:**
    *   Configures an in-memory embedded database.
    *   Scans for `@Entity` classes and configured Spring Data JPA repositories.
    *   Transactional (Rolls back at the end of each test).

---

## 723. What is MockMvc?

**Answer:**
**MockMvc** provides support for testing Spring MVC applications without starting a full HTTP server.
*   **Usage:** Perform requests and define expectations.
*   **Example:**
    ```java
    mockMvc.perform(get("/users/1"))
           .andExpect(status().isOk())
           .andExpect(jsonPath("$.name").value("Alice"));
    ```

---

## 724. What is TestRestTemplate?

**Answer:**
**`TestRestTemplate`** is a convenient alternative to `RestTemplate` for integration tests.
*   **Features:**
    *   Fault tolerant (doesn't throw exceptions on 4xx/5xx errors).
    *   Works well with `@SpringBootTest(webEnvironment = RANDOM_PORT)`.
    *   Great for end-to-end HTTP testing against a real server.

---

## 725. What is embedded database?

**Answer:**
An **Embedded Database** runs within the same JVM process as the application during tests.
*   **Examples:** H2, HSQLDB, Derby.
*   **Use Case:** Provides a clean, fast, temporary database for testing without needing an external MySQL/Postgres instance.

---

## 726. What is test profile?

**Answer:**
**Test Profile** allows you to define beans or configurations specifically for the "test" environment.
*   **Usage:** `@ActiveProfiles("test")` on the test class.
*   **Config:** `application-test.yml` (e.g., disable caching, use H2 DB, mock external URLs).

---

## 727. How to test async code?

**Answer:**
Testing `@Async` or `CompletableFuture` requires waiting for the thread to complete.
*   **Awaitility:** A library to express expectations of an asynchronous system in a concise and easy-to-read manner.
    ```java
    await().atMost(5, SECONDS).until(() -> service.getStatus() == "DONE");
    ```

---

## 728. How to test exception scenarios?

**Answer:**
1.  **JUnit 5:** `assertThrows(CustomException.class, () -> service.method());`
2.  **MockMvc:** `.andExpect(status().isBadRequest())` or `.andExpect(result -> assertTrue(result.getResolvedException() instanceof MyException))`.

---

## 729. How to test caching?

**Answer:**
To verify caching (`@Cacheable`), you need to check if the underlying method was called only once.
1.  Enable Caching in Test Config.
2.  Call method twice.
3.  `verify(repo, times(1)).findById(id);` -> If called only once, cache is working.

---

## 730. How to test Kafka listener?

**Answer:**
Use `@EmbeddedKafka` (from `spring-kafka-test`).
1.  **Setup:** `@EmbeddedKafka(partitions = 1, topics = { "test-topic" })`
2.  **Produce:** Send a message to the embedded broker using `KafkaTemplate`.
3.  **Verify:** Use strict waiting (Awaitility) to check if the Listener processed the message (e.g., side effect in DB or CountDownLatch).

---

## 731. What is Postman?

**Answer:**
**Postman** is a popular API client aimed at developers to create, share, test, and document APIs.
*   **Features:** Send requests, view responses, write tests in JavaScript, automate with Newman (CLI), mock servers.

---

## 732. What is RestAssured?

**Answer:**
**RestAssured** is a Java DSL (Domain Specific Language) for simplifying testing of REST based services.
*   **Usage:** Highly maintainable BDD-like syntax.
    ```java
    given().param("key", "value").when().get("/users").then().statusCode(200);
    ```

---

## 733. How to test REST APIs?

**Answer:**
1.  **Status Codes:** Verify 200 OK, 404 Not Found, 400 Bad Request, 500 Server Error.
2.  **Headers:** Check Content-Type, Authorization, Custom Headers.
3.  **Payload:** Validate JSON/XML body structure and data correctness.
4.  **Logic:** Test business rules (e.g., cannot delete active user).

---

## 734. What is contract testing?

**Answer:**
**Contract Testing** verifies that the interaction between two services (Consumer and Provider) adheres to a shared "contract".
*   **Goal:** Ensure that changes in the Provider don't break the Consumer.
*   **Focus:** Messages/API schema, not internal logic.

---

## 735. What is Pact?

**Answer:**
**Pact** is a code-first tool for testing HTTP and message integrations using contract tests.
*   **Consumer-Driven:** The consumer defines expectations (the pact).
*   **Verification:** The provider verifies it meets those expectations.

---

## 736. What is schema validation?

**Answer:**
**Schema Validation** ensures that the JSON/XML response matches a predefined structure (Schema).
*   **JSON Schema:** Defines field types, required fields, and constraints.
*   **RestAssured:** `body(matchesJsonSchemaInClasspath("schema.json"))`.

---

## 737. What is negative testing?

**Answer:**
**Negative Testing** ensures the application handles invalid input or unexpected user behavior gracefully.
*   **Examples:** Sending text in a numeric field, missing required headers, accessing unauthorized resources.
*   **Goal:** Verify proper Error Codes (4xx) and Error Messages.

---

## 738. What is performance testing?

**Answer:**
**Performance Testing** evaluates how a system performs in terms of responsiveness and stability under a particular workload.
*   **Types:** Load, Stress, Endurance, Spike, Volume, Scalability testing.

---

## 739. What is JMeter?

**Answer:**
**Apache JMeter** is a pure Java application designed to load test functional behavior and measure performance.
*   **Capabilities:** Simulate heavy load on a server, group of servers, network, or object to test its strength or to analyze overall performance under different load types.

---

## 740. What is load testing strategy?

**Answer:**
1.  **Baseline:** Test with normal load.
2.  **Spike:** Sudden burst of users.
3.  **Soak/Endurance:** Long duration (e.g., 24h) to find memory leaks.
4.  **Stress:** Test beyond breaking point to see how it fails (Graceful vs Crash).

---

## 741. What is test pyramid?

**Answer:**
**Test Pyramid** is a framework for balancing different types of tests.
1.  **Unit Tests (Base):** Fast, cheap, numerous. (70%)
2.  **Integration Tests (Middle):** Verify interactions. Slower. (20%)
3.  **E2E / UI Tests (Top):** Slow, expensive, fragile. Fewest. (10%)

---

## 742. What is flaky test?

**Answer:**
A **Flaky Test** is a test that sometimes passes and sometimes fails without any changes to the code.
*   **Causes:** Threading issues (race conditions), Network instability, Dependency on unpredictable data (Time, Random), Shared state.

---

## 743. How to reduce flaky tests?

**Answer:**
1.  **Isolation:** No shared state between tests.
2.  **Determinism:** Mock non-deterministic dependencies (Time, Random).
3.  **Wait Mechanisms:** Use dynamic waits (Awaitility) instead of `Thread.sleep()`.
4.  **Containerization:** Use TestContainers for consistent DB/Service environment.

---

## 744. What is mocking external services?

**Answer:**
When your service depends on a 3rd party API (e.g., Stripe, SendGrid), testing against the live API is slow, expensive, and flaky.
*   **Solution:** Create a mock server that simulates the external service's behavior (Stubbing).

---

## 745. What is WireMock?

**Answer:**
**WireMock** is a simulator for HTTP-based APIs.
*   **Usage:** Run a WireMock server in your test, match requests (URL, Method, Body), and return canned responses (Status 200, JSON Body).
*   **Goal:** Test your HTTP client logic without hitting the real internet.

---

## 746. What is TestContainers?

**Answer:**
**TestContainers** is a Java library that supports JUnit tests, providing lightweight, throwaway instances of common databases, Selenium web browsers, or anything else that can run in a Docker container.
*   **Code:** `new PostgreSQLContainer("postgres:15")`.
*   **Benefit:** Real integration test against a real DB (not H2), ensuring compatibility.

---

## 747. What is end-to-end testing?

**Answer:**
**End-to-End (E2E) Testing** validates the entire software flow from start to finish.
*   **Scope:** UI -> Backend -> Database -> 3rd Party.
*   **Tools:** Selenium, Cypress, Playwright.
*   **Goal:** Simulate real user scenarios (e.g., "User logs in, adds item to cart, pays").

---

## 748. What is CI testing?

**Answer:**
**Continuous Integration (CI) Testing** involves running automated tests every time code is committed to the repository.
*   **Pipeline:** build -> unit tests -> integration tests -> report.
*   **Goal:** Catch bugs early (Shift Left).

---

## 749. What is canary testing?

**Answer:**
**Canary Testing** involves rolling out a new version of the application to a small subset of users (Canaries) before a full rollout.
*   **Goal:** Verify reliability in production with minimal impact. If error rate rises, rollback immediately.

---

## 750. What is chaos testing?

**Answer:**
**Chaos Testing (Chaos Engineering)** involves intentionally injecting failures into a system to test its resilience.
*   **Tool:** Chaos Monkey.
*   **Actions:** Kill random pods, add network latency, simulate high CPU.
*   **Goal:** Ensure the system can withstand turbulent conditions in production.

---

## 751. What is fault injection?

**Answer:**
**Fault Injection** is a testing technique which aids in understanding how the system behaves when stressed or subjected to failure.
*   **Examples:** Introducing network latency, packet loss, or service crashes.
*   **Goal:** Improve system robustness and error handling.

---

## 752. What is regression testing?

**Answer:**
**Regression Testing** verifies that recent code changes have not adversely affected existing features.
*   **When:** After every deployment, bug fix, or feature addition.
*   **Automation:** Crucial for regression to be effective (too slow manually).

---

## 753. What is smoke testing?

**Answer:**
**Smoke Testing** (Build Verification Testing) determines if the deployed build is stable or not.
*   **Scope:** Covers critical paths (e.g., Application starts, Login works).
*   **Result:** Pass -> Continue testing. Fail -> Reject build immediately.

---

## 754. What is sanity testing?

**Answer:**
**Sanity Testing** is a subset of regression testing performed after a bug fix to verify that the specific issue is resolved and no related functionality is broken.
*   **Focus:** Narrower and deeper than smoke testing, but faster than full regression.

---

## 755. What is boundary value testing?

**Answer:**
**Boundary Value Analysis** tests the input values at the boundaries of the valid ranges.
*   **Theory:** Bugs are most likely to happen at boundaries (e.g., < 0, 0, 1, 99, 100, > 100).
*   **Example:** For age 18-65, test 17, 18, 19, 64, 65, 66.

---

## 756. What is equivalence partitioning?

**Answer:**
**Equivalence Partitioning** divides input data into partitions of valid and invalid values.
*   **Assumption:** All values in a partition behave similarly. If one works, all work.
*   **Example:** For age 18-65. Valid partition: 30. Invalid partitions: 10, 80.
*   **Goal:** Reduce number of test cases.

---

## 757. What is test data management?

**Answer:**
**Test Data Management (TDM)** involves planning, designing, storing, and managing data used for software testing.
*   **Challenges:** PII protection (masking), data consistency across environments, generating realistic volume.
*   **Tools:** Delphix, synthesized data scripts.

---

## 758. What is parallel test execution?

**Answer:**
**Parallel Test Execution** runs multiple tests simultaneously to reduce the overall execution time.
*   **JUnit 5:** Supports parallel execution config (`junit.jupiter.execution.parallel.enabled=true`).
*   **Risk:** Thread safety issues if tests share state (static variables, same DB rows).

---

## 759. How to test microservices?

**Answer:**
1.  **Unit:** Test internal logic of each service.
2.  **Contact:** Test API compatibility (Pact).
3.  **Integration:** Test service + DB/Broker (TestContainers).
4.  **Component:** Test service in isolation with mocks.
5.  **E2E:** Test flow across multiple services.

---

## 760. How to test distributed transactions?

**Answer:**
Testing **SAGA** or widespread transactions is complex.
*   **Focus:** Consistency and Compensation.
*   **Scenario:** Order Service -> Payment Service -> Inventory Service.
*   **Failure Test:** Simulate Payment failure and assert that Inventory is restored (Compensation triggered).

---

## 761. What is blue-green testing?

**Answer:**
**Blue-Green Deployment** is a technique that reduces downtime and risk by running two identical production environments called Blue and Green.
*   **Blue:** Current live environment.
*   **Green:** New version of the application.
*   **Testing:** Run tests on Green. Once satisfied, switch the router/load balancer to point to Green.
*   **Rollback:** Switch back to Blue instantly if issues arise.

---

## 762. What is API mocking?

**Answer:**
**API Mocking** creates a simulated version of an API that mimics the behavior of the real API.
*   **Use Case:**
    *   Testing when the real API is unavailable or under development.
    *   Simulating edge cases (timeouts, errors) that are hard to trigger in real systems.
    *   Reducing costs/latency of third-party API calls.
*   **Tools:** WireMock, Postman Mock Servers, Mockoon.

---

## 763. What is security testing?

**Answer:**
**Security Testing** uncovers vulnerabilities, threats, and risks in the software.
*   **Goal:** Prevent malicious attacks and ensure data integrity/confidentiality.
*   **Types:**
    *   **Vulnerability Scanning:** Automated checks for known issues.
    *   **Security Scanning:** Network and system weakness checks.
    *   **Risk Assessment:** Analyzing security risks.

---

## 764. What is penetration testing?

**Answer:**
**Penetration Testing (Pen Test)** is a simulated cyberattack against your system to check for exploitable vulnerabilities.
*   **Manual vs Automated:** often a mix of both.
*   **Phases:** Reconnaissance, Scanning, Exploitation, Maintaining Access, Analysis.
*   **Outcome:** A report detailing security gaps to be fixed.

---

## 765. What is static code analysis?

**Answer:**
**Static Code Analysis** (SAST - Static Application Security Testing) analyzes source code **without executing it**.
*   **Purpose:** Find bugs, security vulnerabilities, code smells, and non-compliance with coding standards early.
*   **Tools:** SonarQube, Checkstyle, SpotBugs, PMD.
*   **Timing:** Usually runs in the CI/CD pipeline.

---

## 766. What is dynamic testing?

**Answer:**
**Dynamic Testing** (DAST - Dynamic Application Security Testing) analyzes the application **while it is running**.
*   **Purpose:** Find runtime issues like memory leaks, performance bottlenecks, and security vulnerabilities that only appear during execution.
*   **Includes:** Unit tests, integration tests, system tests, and acceptance tests.

---

## 767. What is acceptance testing?

**Answer:**
**Acceptance Testing (UAT - User Acceptance Testing)** determines if the system meets the business requirements and is ready for delivery.
*   **Audience:** Performed by the client or end-users.
*   **Focus:** Functionality and usability from a user's perspective, not technical implementation.
*   **Types:** Alpha Testing (internal), Beta Testing (external users).

---

## 768. What is user story testing?

**Answer:**
**User Story Testing** verifies that a specific feature (User Story) meets its **Acceptance Criteria**.
*   **Process:**
    1.  Developer writes code for the story.
    2.  QA/Dev writes tests based on the "Given-When-Then" criteria.
    3.  Story is "Done" only when all acceptance tests pass.

---

## 769. What is performance bottleneck detection?

**Answer:**
A **Bottleneck** is a point in the system that limits overall performance (e.g., slow DB query, high CPU usage).
*   **Detection Steps:**
    1.  **Load Test:** Apply stress to the system.
    2.  **Monitor:** Watch metrics (CPU, Memory, Disk I/O, Network, Latency).
    3.  **Analyze:** Identify the component with the highest latency or resource consumption.
    4.  **Profile:** Use profiling tools to find the exact code/query causing the issue.

---

## 770. What is profiling in testing?

**Answer:**
**Profiling** is a form of dynamic analysis that measures the complexity of the code in terms of:
*   **Memory Usage:** (e.g., Memory Leaks, high object creation).
*   **CPU Usage:** (e.g., inefficient algorithms, loops).
*   **Thread Execution:** (e.g., deadlocks, contention).
*   **Tools:** JProfiler, VisualVM, YourKit.

---

## 771. How to test multi-threaded code?

**Answer:**
Testing **Multi-threaded code** is difficult due to non-determinism (race conditions).
*   **Approaches:**
    *   **Stress Testing:** Run the test thousands of times to catch rare race conditions ().
    *   **CountDownLatch:** Use latches to force threads to wait for each other and run simultaneously.
    *   **Tools:**  or  (Java Concurrency Stress tests).
    *   **Avoid:**  in tests (flaky).

---

## 772. What is stress testing?

**Answer:**
**Stress Testing** evaluates system stability under **extreme** conditions (beyond normal operational limits).
*   **Goal:** Determine the "Breaking Point" of the system.
*   **Example:** Sending 10x the expected traffic until the server crashes or becomes unresponsive to see how it recovers.

---

## 773. What is soak testing?

**Answer:**
**Soak Testing (Endurance Testing)** involves running a system at a significant load for an **extended period** (e.g., 24-48 hours).
*   **Goal:** Detect issues that only appear over time, such as:
    *   Memory Leaks.
    *   Database connection pool exhaustion.
    *   Log file accumulation filling up disk space.

---

## 774. What is test strategy document?

**Answer:**
A **Test Strategy Document** is a high-level plan defining the testing approach for the software development cycle.
*   **Components:**
    *   **Scope:** What will be tested (and what won't).
    *   **Types:** Unit, Integration, E2E, Performance, Security.
    *   **Tools:** JUnit, Selenium, JMeter.
    *   **Environment:** Dev, QA, Staging, Prod.
    *   **Risks:** Potential blockers.

---

## 775. What is quality gate?

**Answer:**
A **Quality Gate** is a set of criteria that must be met before software can move from one stage of the pipeline to another.
*   **Example (SonarQube Quality Gate):**
    *   Code Coverage > 80%.
    *   No Critical Bugs.
    *   No Security Vulnerabilities.
    *   Technical Debt Ratio < 5%.
*   **Result:** If the gate fails, the build fails.

---

## 776. What is test automation framework?

**Answer:**
A **Test Automation Framework** is a set of guidelines, coding standards, and tools used to create and run automated tests.
*   **Types:**
    *   **Linear:** Record and Playback.
    *   **Modular:** Scripts broken into small, independent modules.
    *   **Data-Driven:** Test logic is separated from test data (reads from CSV/Excel).
    *   **Keyword-Driven:** Uses keywords (Action words) to define tests.
    *   **Hybrid:** Combination of the above.

---

## 777. What is cross-browser testing?

**Answer:**
**Cross-Browser Testing** ensures that a web application works correctly across different web browsers (Chrome, Firefox, Safari, Edge) and OS combinations.
*   **Goal:** Consistent behavior and UI rendering.
*   **Tools:** Selenium Grid, BrowserStack, Sauce Labs.

---

## 778. What is mobile API testing?

**Answer:**
**Mobile API Testing** focuses on the backend APIs that power mobile applications.
*   **Specific Challenges:**
    *   **Network:** Testing on slow/unstable networks (latency, packet loss).
    *   **Battery:** Efficient API calls to save battery.
    *   **Versioning:** Supporting older versions of the app on older APIs.
    *   **Device Fragmentation:** Different screen sizes/OS affecting data payload requirements.

---

## 779. What is contract-first development?

**Answer:**
**Contract-First Development** involves defining the API contract (e.g., OpenAPI/Swagger YAML) **before** writing any code.
*   **Process:**
    1.  Define API spec (endpoints, request/response models).
    2.  Review and agree with frontend/mobile teams.
    3.  Generate code (interfaces/DTOs) from the spec.
    4.  Implement the logic.
*   **Benefit:** Parallel development (Frontend can mock based on contract while Backend builds it).

---

## 780. What is shift-left testing?

**Answer:**
**Shift-Left Testing** is the practice of moving testing **earlier** in the software development lifecycle (SDLC).
*   **Traditional:** Requirements -> Design -> Code -> **Test**.
*   **Shift-Left:** Requirements -> **Test Design** -> Code + **Unit Test**.
*   **Goal:** Find and fix defects early when they are cheaper to fix.
