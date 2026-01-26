# Testing (JUnit & Mockito) Interview Questions & Answers

## 1. What is JUnit? Annotations
**Detailed Explanation**: JUnit is a standard testing framework for Java.
*   **Annotatations (JUnit 5)**:
    *   **`@Test`**: Marks a method as a test.
    *   **`@BeforeEach`** (Junit 4: `@Before`): Runs before *each* test method.
    *   **`@AfterEach`** (Junit 4: `@After`): Runs after *each* test method.
    *   **`@BeforeAll`** (Junit 4: `@BeforeClass`): Runs *once* before all tests (Must be static).
    *   **`@AfterAll`** (Junit 4: `@AfterClass`): Runs *once* after all tests.

**Example**:
```java
class CalculatorTest {
    @BeforeEach
    void setup() { System.out.println("Start"); }

    @Test
    void testAdd() {
        assertEquals(2, 1+1);
    }
}
```

---

## 2. Difference between JUnit 4 and JUnit 5
**Detailed Explanation**:
*   **JUnit 4**:
    *   One generic definition (monolithic jar).
    *   Annotations: `@Before`, `@After`, `@BeforeClass`.
    *   Architecture: Runners.
*   **JUnit 5 (Jupiter)**:
    *   Modular (Platform + Jupiter + Vintage).
    *   Annotations: `@BeforeEach`, `@AfterEach`, `@BeforeAll`.
    *   Support for **Lambda Expressions** and **Nested Tests**.

---

## 3. How to test a private method?
**Detailed Explanation**:
*   **Concept**: Ideally, you **should not** test private methods directly. You should test the *public* method that calls it.
*   **If you MUST**: Use **Reflection** (PowerMock or Java Reflection API) to bypass access controls.
*   **Why avoid**: Testing private methods breaks encapsulation. If you refactor the private method, tests break.

**Example (Reflection)**:
```java
Method m = MyClass.class.getDeclaredMethod("privateMethod");
m.setAccessible(true); // Bypass private
m.invoke(obj);
```

---

## 4. What is Mockito? Why do we use it?
**Detailed Explanation**: Mockito is a mocking framework. It allows you to create dummy objects (mocks) to simulate the behavior of real dependencies.
*   **Why**: To perform **Unit Testing**. Unit tests should test *only* the specific class, not its dependencies (like DB or External API). We mock the DB/API so we can test the Logic in isolation.

---

## 5. Difference between @Mock and @InjectMocks
**Detailed Explanation**:
*   **`@Mock`**: Creates a mock object (Dependency).
    *   E.g., `UserRepository` (doesn't talk to real DB).
*   **`@InjectMocks`**: Creates the **real object** (Code under test) and **injects** the mocked dependencies into it.
    *   E.g., `UserService` (gets the mocked `UserRepository` inside it).

**Example**:
```java
@ExtendWith(MockitoExtension.class)
class UserServiceTest {
    @Mock
    UserRepository repo; // Mock

    @InjectMocks
    UserService service; // Real, with 'repo' injected

    @Test
    void test() {
        when(repo.findUser()).thenReturn("Alice"); // Define behavior
        service.getUser(); // Uses mock
    }
}
```

---

## 6. How to write a test case for a void method?
**Detailed Explanation**: You cannot assert the return value (since it is void).
*   **Approach**:
    1.  **Verify Side Effects**: Check if it changed some state or called another method.
    2.  **`verify()` (Mockito)**: Check if a dependency method was called `n` times.

**Example**:
```java
// Testing: service.deleteUser(1) -> calls repo.delete(1)
@Test
void testDelete() {
    service.deleteUser(1);
    verify(repo, times(1)).deleteById(1); // Check call happened
}
```

---

## 7. What is Code Coverage? Tools used (Jacoco).
**Detailed Explanation**:
*   **Definition**: A metric that measures what percentage of your source code is executed when your tests run.
*   **Tool**: **JaCoCo** (Java Code Coverage).
*   **Goal**: Typically > 80%. It highlights missing test cases (e.g., "You never tested the `else` block").

---

## 8. Integration Testing vs Unit Testing
**Detailed Explanation**:
*   **Unit Testing**:
    *   Tests one class/method in isolation.
    *   Mocks all dependencies.
    *   Fast.
*   **Integration Testing**:
    *   Tests how modules work *together*.
    *   Connects to real (or embedded) DB, starts Spring Context.
    *   Slower.
    *   Annotation: `@SpringBootTest`.

---

## 9. How to test Exception scenarios?
**Detailed Explanation**:
*   **Goal**: Verify that your code throws the *correct exception* when invalid input is given.
*   **JUnit 5**: Use `assertThrows()`.

**Example**:
```java
@Test
void testException() {
    assertThrows(IllegalArgumentException.class, () -> {
        calculator.divide(10, 0); // Should throw
    });
}
```

---

## 10. Contract Testing
**Detailed Explanation**: Ensuring that two services (Consumer and Provider) can communicate.
*   **Tools**: Pact, Spring Cloud Contract.
*   **Process**: Consumer defines a contract ("I need field 'name'"). Provider verifies this contract in its build pipeline. If Provider renames 'name' to 'fullname', the build fails.
