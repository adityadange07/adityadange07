## ✅ Top 100 Java Unit Testing Interview Questions

---

### 🔹 1–20: **JUnit (Basics & Advanced)**

## 1. What is unit testing in Java?

**Unit Testing in Java** is a software testing technique where individual units or components of a program (typically methods or classes) are tested in isolation from the rest of the application. The goal is to validate that each unit performs as expected.

---

## 🔍 **Definition**

A **unit** is the smallest testable part of an application, such as a method or function.
**Unit testing** ensures that each part of the code works correctly on its own before it is integrated with other parts.

In Java, **JUnit** is the most commonly used unit testing framework.

---

## ✅ **Why Unit Testing is Important**

1. **Early bug detection** – Find problems early in the development cycle.
2. **Code reliability** – Ensures that code behaves as intended.
3. **Facilitates refactoring** – Confidently change code without breaking functionality.
4. **Documentation** – Unit tests show how code is expected to behave.
5. **Reduces debugging time** – Fewer issues later in integration or system testing.

---

## 🛠️ **Popular Unit Testing Framework: JUnit**

**JUnit** is a widely-used testing framework in Java. It provides annotations and assertions to write and run tests.

---

## 📘 **Basic Example of Unit Testing in Java**

Let’s say we have a simple Java class `Calculator`:

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }
}
```

### ✅ Now, let’s write a unit test using **JUnit 5**:

```java
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;

public class CalculatorTest {

    @Test
    public void testAdd() {
        Calculator calc = new Calculator();
        int result = calc.add(10, 5);
        assertEquals(15, result);
    }

    @Test
    public void testSubtract() {
        Calculator calc = new Calculator();
        int result = calc.subtract(10, 5);
        assertEquals(5, result);
    }
}
```

### 🔍 Explanation of Key Parts:

* `@Test`: Annotation marking a method as a test case.
* `assertEquals(expected, actual)`: Verifies that the expected result equals the actual output.
* The tests **run independently** from the application logic.

---

## 🧪 **How to Run Unit Tests**

* In an IDE like IntelliJ or Eclipse, right-click the test file and choose **Run**.
* Or use **build tools** like:

    * **Maven**: `mvn test`
    * **Gradle**: `gradle test`

---

## 📌 Best Practices for Unit Testing

* Test **one method** at a time.
* Use **clear and descriptive** test names.
* Avoid dependencies on external systems (e.g., databases).
* Run tests frequently during development.
* Maintain high **code coverage** (percentage of code tested).

---

## 🧠 Summary

| Aspect            | Detail                                           |
| ----------------- | ------------------------------------------------ |
| Purpose           | Test individual units of code                    |
| Framework         | JUnit (most common in Java)                      |
| Benefits          | Detect bugs early, better code quality           |
| Example Tools     | JUnit, Mockito (for mocking), TestNG             |
| Typical Structure | Class under test + test class with @Test methods |

---

## 2. What is JUnit? Why is it used?

Here's a **detailed explanation** of **JUnit**, including **why it’s used**, and an example to solidify the concept.

---

## ✅ **What is JUnit?**

**JUnit** is an **open-source unit testing framework** for the Java programming language. It provides a simple and standardized way to write and run tests on small units of code, such as methods or classes.

It’s part of the **xUnit family** of testing frameworks, which also includes NUnit (C#), PyUnit (Python), etc.

---

## 🔧 **Why is JUnit Used?**

JUnit is used to:

1. ✅ **Test individual units** of code to ensure they function as expected.
2. 🔁 **Automate testing**, so that tests can be rerun quickly after changes.
3. 🐞 **Detect bugs early** in the development cycle.
4. 🧪 **Ensure code quality** by validating behavior through repeatable test cases.
5. 🔄 **Support test-driven development (TDD)** – writing tests before code.

---

## 📘 **Example: Using JUnit in Java**

Suppose you have a class called `Calculator`:

```java
public class Calculator {
    public int multiply(int a, int b) {
        return a * b;
    }
}
```

### Writing a JUnit Test for This Class (Using JUnit 5):

```java
import static org.junit.jupiter.api.Assertions.assertEquals;
import org.junit.jupiter.api.Test;

public class CalculatorTest {

    @Test
    public void testMultiply() {
        Calculator calc = new Calculator();
        int result = calc.multiply(3, 4);
        assertEquals(12, result);
    }
}
```

---

## 📚 **Key JUnit Concepts**

| Concept        | Description                                                               |
| -------------- | ------------------------------------------------------------------------- |
| `@Test`        | Marks a method as a test case                                             |
| `assertEquals` | Asserts that two values are equal                                         |
| `@BeforeEach`  | Runs before each test case (used to set up test data)                     |
| `@AfterEach`   | Runs after each test case (used to clean up)                              |
| `@BeforeAll`   | Runs once before all tests (used for one-time setup, e.g., DB connection) |
| `@AfterAll`    | Runs once after all tests (e.g., for cleanup)                             |

---

## 🧪 **JUnit vs Manual Testing**

| Aspect            | Manual Testing       | JUnit (Automated Testing)     |
| ----------------- | -------------------- | ----------------------------- |
| Time-consuming    | Yes                  | No (fast and repeatable)      |
| Repeatable        | Difficult            | Easy                          |
| Accuracy          | Prone to human error | Very accurate                 |
| Integration in CI | Difficult            | Seamless with CI/CD pipelines |

---

## ⚙️ **JUnit + Tools**

* **Build tools**: Maven, Gradle
* **Mocking**: Mockito (for testing components in isolation)
* **IDE support**: IntelliJ, Eclipse, VS Code

---

## 🧠 Summary

| Feature          | Description                                                    |
| ---------------- | -------------------------------------------------------------- |
| What is JUnit?   | A Java framework for writing and running unit tests            |
| Why use it?      | To ensure code correctness, catch bugs early, automate testing |
| Common use cases | TDD, regression testing, CI/CD pipelines                       |

---

## 3. What are the differences between JUnit 4 and JUnit 5?

Knowing the **differences between JUnit 4 and JUnit 5** is important for interviews, especially if you're working with modern Java projects.

---

## ✅ **Quick Summary:**

| Feature                   | **JUnit 4**           | **JUnit 5**                                   |
| ------------------------- | --------------------- | --------------------------------------------- |
| **Released**              | 2006                  | 2017                                          |
| **Architecture**          | Single monolithic jar | Modular: 3 separate components                |
| **Annotations**           | Limited               | Improved and expanded                         |
| **Extension support**     | Runners (limited)     | Extensions (flexible and powerful)            |
| **Java version required** | Java 5+               | Java 8+                                       |
| **Dynamic tests**         | ❌ Not supported       | ✅ Supported                                   |
| **Tagging tests**         | ❌ Not supported       | ✅ Supported with `@Tag`                       |
| **Dependency Injection**  | ❌ Not supported       | ✅ Supported for test constructors and methods |
| **Assumptions**           | Basic                 | Improved and extended                         |

---

## 🔍 **Core Architecture Differences**

### ✅ JUnit 4 (Monolithic)

* All features are packed into **one single library (junit.jar)**.
* Limited flexibility for adding plugins or extending functionality.

### ✅ JUnit 5 (Modular & Modern)

JUnit 5 is composed of **three main modules**:

| Module           | Purpose                                                           |
| ---------------- | ----------------------------------------------------------------- |
| `JUnit Platform` | Launches testing frameworks on the JVM                            |
| `JUnit Jupiter`  | New programming model and APIs (replaces JUnit 4's `@Test`, etc.) |
| `JUnit Vintage`  | Supports running JUnit 3 and 4 tests on JUnit 5 platform          |

---

## 📘 **Annotation Differences**

| Purpose                  | JUnit 4                 | JUnit 5                   |
| ------------------------ | ----------------------- | ------------------------- |
| Test method              | `@Test`                 | `@Test`                   |
| Setup before each test   | `@Before`               | `@BeforeEach`             |
| Teardown after each test | `@After`                | `@AfterEach`              |
| Setup before all tests   | `@BeforeClass` (static) | `@BeforeAll` (can use DI) |
| Teardown after all tests | `@AfterClass` (static)  | `@AfterAll`               |
| Ignore test              | `@Ignore`               | `@Disabled`               |
| Expected exception       | `@Test(expected = ...)` | Use `assertThrows()`      |
| Grouping tests           | ❌ Not supported         | `@Nested` classes         |

---

## 🧪 **JUnit 5 Exclusive Features**

1. **`@DisplayName`** – Customize test names.
2. **`@Tag`** – Tag tests for filtering.
3. **Dynamic Tests** – Use `@TestFactory` to create tests at runtime.
4. **Dependency Injection** – Inject parameters into test methods (e.g., `TestInfo`, `TestReporter`).
5. **Better Assertions & Assumptions** – More expressive with `assertAll`, `assertThrows`, `assumeTrue`, etc.

---

## ✅ **Example Comparison**

### ✅ JUnit 4:

```java
import org.junit.Test;
import static org.junit.Assert.assertEquals;

public class CalculatorTest {
    @Test
    public void testAdd() {
        assertEquals(5, 2 + 3);
    }
}
```

### ✅ JUnit 5:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

class CalculatorTest {
    @Test
    void testAdd() {
        assertEquals(5, 2 + 3);
    }
}
```

---

## 💡 Interview Tip

When asked about this, briefly mention:

* Modular structure of JUnit 5
* Better annotations and support for modern Java (lambdas, streams, etc.)
* Backward compatibility via **JUnit Vintage**

---

## 🧠 Summary

| Criteria           | JUnit 4                   | JUnit 5                                |
| ------------------ | ------------------------- | -------------------------------------- |
| Architecture       | Single jar                | Modular (Platform + Jupiter + Vintage) |
| Java Compatibility | Java 5+                   | Java 8+                                |
| Extension Model    | Limited (Runners)         | Powerful and flexible (Extensions)     |
| New Features       | Fewer                     | Many (Tags, Dynamic Tests, DI, etc.)   |
| Migration          | No backward compatibility | Backward compatible with JUnit Vintage |

---

## 4. What annotations are used in JUnit 5?

Understanding **annotations in JUnit 5** is essential for writing clean, structured, and powerful tests. JUnit 5 offers a modern and flexible set of annotations that improve on JUnit 4.

---

## ✅ **List of Commonly Used JUnit 5 Annotations**

| Annotation | Description |
| ---------- | ----------- |

### 🔹 **1. @Test**

Marks a method as a test method.

```java
@Test
void testAddition() {
    assertEquals(5, 2 + 3);
}
```

---

### 🔹 **2. @BeforeEach**

Runs **before** each test method.

* Good for setting up test data or resources.

```java
@BeforeEach
void setup() {
    // Code that runs before each test
}
```

---

### 🔹 **3. @AfterEach**

Runs **after** each test method.

* Used for cleaning up resources.

```java
@AfterEach
void tearDown() {
    // Code that runs after each test
}
```

---

### 🔹 **4. @BeforeAll**

Runs **once before all test methods** in the class.

* Must be **static** unless you use test instance lifecycle `@TestInstance(Lifecycle.PER_CLASS)`.

```java
@BeforeAll
static void init() {
    // Runs once before all tests
}
```

---

### 🔹 **5. @AfterAll**

Runs **once after all test methods** in the class.

```java
@AfterAll
static void cleanUp() {
    // Runs once after all tests
}
```

---

### 🔹 **6. @DisplayName**

Sets a custom name for a test method or class.

* Useful for making test outputs more readable.

```java
@DisplayName("Adding two positive numbers")
@Test
void additionTest() {
    assertEquals(5, 2 + 3);
}
```

---

### 🔹 **7. @Disabled**

Disables a test class or method (i.e., skips it).

* Used to temporarily ignore failing or unfinished tests.

```java
@Disabled("Work in progress")
@Test
void skippedTest() {
    // Will not run
}
```

---

### 🔹 **8. @Nested**

Defines a nested test class to group related tests.

* Great for organizing tests logically.

```java
@Nested
class AddTests {
    @Test
    void addPositive() {
        assertEquals(5, 2 + 3);
    }
}
```

---

### 🔹 **9. @Tag**

Allows categorizing tests (e.g., smoke, regression, slow).

* Useful when running subsets of tests.

```java
@Tag("smoke")
@Test
void quickTest() {
    assertTrue(true);
}
```

---

### 🔹 **10. @TestInstance**

Controls the lifecycle of the test class:

* `PER_METHOD` (default): New instance for each test.
* `PER_CLASS`: One instance for the entire class (allows non-static `@BeforeAll`).

```java
@TestInstance(TestInstance.Lifecycle.PER_CLASS)
class MyTest {
    @BeforeAll
    void init() { /* non-static */ }
}
```

---

### 🔹 **11. @TestFactory**

Used to create **dynamic tests** at runtime.

```java
@TestFactory
Collection<DynamicTest> dynamicTests() {
    return List.of(
        DynamicTest.dynamicTest("1st test", () -> assertTrue(1 < 2)),
        DynamicTest.dynamicTest("2nd test", () -> assertEquals(4, 2 * 2))
    );
}
```

---

### 🔹 **12. @RepeatedTest**

Runs a test **multiple times**.

```java
@RepeatedTest(3)
void repeatedTest() {
    System.out.println("Run this test 3 times");
}
```

---

### 🔹 **13. @ParameterizedTest** *(Requires additional imports)*

Runs the same test with different input values.

```java
@ParameterizedTest
@ValueSource(ints = {1, 2, 3})
void testWithDifferentInts(int num) {
    assertTrue(num > 0);
}
```

---

## 🧠 Summary Table

| Annotation           | Purpose                             |
| -------------------- | ----------------------------------- |
| `@Test`              | Marks a test method                 |
| `@BeforeEach`        | Runs before each test method        |
| `@AfterEach`         | Runs after each test method         |
| `@BeforeAll`         | Runs once before all tests          |
| `@AfterAll`          | Runs once after all tests           |
| `@DisplayName`       | Custom name for test or class       |
| `@Disabled`          | Disables a test                     |
| `@Nested`            | Groups related tests in inner class |
| `@Tag`               | Categorizes tests                   |
| `@TestInstance`      | Controls test class lifecycle       |
| `@TestFactory`       | Generates dynamic tests             |
| `@RepeatedTest`      | Repeats test N times                |
| `@ParameterizedTest` | Runs test with multiple inputs      |

---

## 5. How do you write a basic test case in JUnit?

This is fundamental in interviews and real-world Java development.

---

## ✅ **How to Write a Basic Test Case in JUnit (JUnit 5)**

A **test case** is a method that verifies whether a specific part of your code (typically a method) works as expected.

---

### 🔧 **Step-by-Step: Basic JUnit 5 Test Case**

### 🔹 **1. Create a Class to Test**

Let’s say you have a simple class `Calculator.java`:

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

---

### 🔹 **2. Create a Test Class**

Create a separate class named `CalculatorTest.java`.

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class CalculatorTest {

    @Test
    void testAdd() {
        Calculator calc = new Calculator();
        int result = calc.add(2, 3);
        assertEquals(5, result); // Expected: 5, Actual: result
    }
}
```

---

## 🔍 **Explanation of Code**

| Element                          | Description                                               |
| -------------------------------- | --------------------------------------------------------- |
| `@Test`                          | Marks the method as a test case                           |
| `Calculator calc = ...`          | Create an instance of the class to test                   |
| `assertEquals(expected, actual)` | Checks that the actual result matches the expected result |
| `void testAdd()`                 | Test method name (should describe what it tests)          |

---

## ⚙️ **How to Run the Test**

### ✅ In an IDE (like IntelliJ/Eclipse):

* Right-click on the test class or method → **Run**.
* Green bar = pass, Red bar = fail.

### ✅ Using Maven:

Make sure you have this in your `pom.xml`:

```xml
<dependency>
  <groupId>org.junit.jupiter</groupId>
  <artifactId>junit-jupiter</artifactId>
  <version>5.9.2</version> <!-- Or latest -->
  <scope>test</scope>
</dependency>
```

Then run:

```bash
mvn test
```

---

## 🧪 **What Happens If the Test Fails?**

If the actual value is not equal to the expected value, the test will fail and show something like:

```
expected: <5> but was: <4>
```

---

## 📌 Best Practices for Writing Test Cases

* ✅ Test **one thing** per test method.
* ✅ Use **meaningful method names** (e.g., `testAdditionWithPositiveNumbers`)
* ✅ Include **setup** in `@BeforeEach` if repeated.
* ✅ Keep your test logic **clean and independent**.

---

## 🧠 Summary

| Step | Action                                             |
| ---- | -------------------------------------------------- |
| 1️⃣  | Create a class with logic (e.g., Calculator)       |
| 2️⃣  | Write a separate test class (e.g., CalculatorTest) |
| 3️⃣  | Use `@Test` and assertions                         |
| 4️⃣  | Run tests with IDE or build tools                  |

---

## 6. What is the purpose of `@BeforeEach` and `@AfterEach`?

Understanding `@BeforeEach` and `@AfterEach` is essential for writing **clean, reusable, and organized unit tests** in JUnit 5.

---

## ✅ **Purpose of `@BeforeEach` and `@AfterEach` in JUnit 5**

| Annotation    | Purpose                                                                |
| ------------- | ---------------------------------------------------------------------- |
| `@BeforeEach` | Runs **before each test method**. Used to set up test data or objects. |
| `@AfterEach`  | Runs **after each test method**. Used to clean up or reset state.      |

---

## 🔍 **Why Use Them?**

Instead of repeating setup or cleanup code in every test method, you can:

* **Initialize shared objects once per test** with `@BeforeEach`
* **Release resources or reset variables** with `@AfterEach`

This makes your test code:

* ✅ Cleaner
* ✅ Less repetitive
* ✅ More maintainable

---

## 🧪 **Example**

Let’s say you are testing a `Calculator` class.

### 🔹 Calculator.java

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }

    public int subtract(int a, int b) {
        return a - b;
    }
}
```

### 🔹 CalculatorTest.java

```java
import org.junit.jupiter.api.*;

import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {

    Calculator calc;

    @BeforeEach
    void setup() {
        calc = new Calculator(); // Runs before each test
        System.out.println("Setting up Calculator instance");
    }

    @AfterEach
    void cleanup() {
        System.out.println("Cleaning up after test");
    }

    @Test
    void testAddition() {
        assertEquals(5, calc.add(2, 3));
    }

    @Test
    void testSubtraction() {
        assertEquals(2, calc.subtract(5, 3));
    }
}
```

### 🧾 Output When Running Tests:

```
Setting up Calculator instance
Cleaning up after test
Setting up Calculator instance
Cleaning up after test
```

This shows that:

* `@BeforeEach` runs **before each test** (`testAddition`, `testSubtraction`)
* `@AfterEach` runs **after each test**

---

## 🧠 Summary

| Annotation    | Runs When?           | Common Use                        |
| ------------- | -------------------- | --------------------------------- |
| `@BeforeEach` | Before every `@Test` | Initialize or set up resources    |
| `@AfterEach`  | After every `@Test`  | Cleanup, reset, or teardown logic |

---

## 7. How is `@BeforeAll` different from `@BeforeEach`?

This is a common area of confusion in JUnit interviews. Let’s break it down clearly and with an example.

---

## ✅ **Difference Between `@BeforeAll` and `@BeforeEach`**

| Feature            | `@BeforeEach`                   | `@BeforeAll`                          |
| ------------------ | ------------------------------- | ------------------------------------- |
| **Runs when?**     | Before **each** test method     | **Once** before **all** test methods  |
| **Usage**          | Set up per-test data or objects | Initialize expensive/shared resources |
| **Is it static?**  | ❌ No (uses instance methods)    | ✅ Yes (must be `static` by default)   |
| **Test lifecycle** | Run before every test case      | Run only once, before all test cases  |

---

## 🧪 **Example to Demonstrate the Difference**

```java
import org.junit.jupiter.api.*;

public class ExampleTest {

    @BeforeAll
    static void globalSetup() {
        System.out.println("BeforeAll: Run once before all tests");
    }

    @BeforeEach
    void setup() {
        System.out.println("BeforeEach: Run before each test");
    }

    @Test
    void testOne() {
        System.out.println("Executing Test 1");
    }

    @Test
    void testTwo() {
        System.out.println("Executing Test 2");
    }
}
```

### ✅ Output:

```
BeforeAll: Run once before all tests
BeforeEach: Run before each test
Executing Test 1
BeforeEach: Run before each test
Executing Test 2
```

---

## 💡 When to Use Each

| Scenario                                 | Use           |
| ---------------------------------------- | ------------- |
| You need a fresh object before each test | `@BeforeEach` |
| You want to connect to a DB once         | `@BeforeAll`  |
| You want to reset shared state per test  | `@BeforeEach` |
| You want to load configuration once      | `@BeforeAll`  |

---

## ⚙️ `@BeforeAll` and Non-Static Use

If you don’t want to use `static`, add this annotation to your class:

```java
@TestInstance(TestInstance.Lifecycle.PER_CLASS)
```

Then you can write:

```java
@BeforeAll
void setupAll() {
    // Now non-static works
}
```

---

## 🧠 Summary Table

| Annotation    | Runs When                    | Must Be Static     | Common Use Case                          |
| ------------- | ---------------------------- | ------------------ | ---------------------------------------- |
| `@BeforeEach` | Before **every test method** | ❌ No               | Reset test-specific state                |
| `@BeforeAll`  | Once **before all tests**    | ✅ Yes (by default) | Load config, connect DB, expensive setup |

---

## 8. What does `@Test` do in JUnit?

Understanding `@Test` is absolutely essential — it's the **core annotation** in JUnit.

---

## ✅ **What is `@Test` in JUnit?**

`@Test` is an **annotation** used to mark a **method as a test case**. When JUnit runs the test class, it looks for methods annotated with `@Test` and executes them as individual tests.

---

## 🔍 **Purpose of `@Test`**

* Tells JUnit: “This method is a test.”
* Allows JUnit to run the method, check assertions, and report pass/fail.
* Can be combined with assertions to validate behavior.

---

## 🔧 **Basic Example (JUnit 5)**

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class CalculatorTest {

    @Test
    void testAddition() {
        int result = 2 + 3;
        assertEquals(5, result); // ✅ Test passes if 2 + 3 == 5
    }
}
```

---

## 🧪 What Happens Behind the Scenes?

* JUnit detects `@Test` methods.
* It **runs each `@Test` method independently**.
* If the method runs without throwing an exception and all assertions pass, the test **passes**.
* If any assertion fails or an unhandled exception is thrown, the test **fails**.

---

## 🛠️ Used With Assertions

Assertions help verify results inside `@Test` methods:

* `assertEquals(expected, actual)`
* `assertTrue(condition)`
* `assertThrows(Exception.class, () -> code)`

---

## 📛 What if `@Test` Is Missing?

JUnit will **not recognize the method as a test**, even if it contains assertions:

```java
void testSomething() {
    assertEquals(5, 2 + 3);  // ❌ Won’t be run by JUnit
}
```

---

## 🧠 Summary

| Feature       | Details                                  |
| ------------- | ---------------------------------------- |
| Purpose       | Marks a method as a test case            |
| Return Type   | `void` (no return value)                 |
| Accessibility | Usually `public` or `default` in JUnit 5 |
| Parameters    | Typically no arguments                   |
| Test outcome  | Depends on assertions or exceptions      |

---

## 9. How do you assert results in JUnit? What are some commonly used assertion methods?

Assertions are **the heart of JUnit testing**. They are used to **verify that the actual output of code matches the expected result**.

---

## ✅ **What Is an Assertion in JUnit?**

An **assertion** is a **static method** that checks whether a condition is true. If the assertion fails, the test **fails**.

JUnit uses the class `org.junit.jupiter.api.Assertions` (in JUnit 5).

---

## 🧪 **How Do You Use Assertions?**

You write assertions inside a `@Test` method:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class MathTest {

    @Test
    void testAddition() {
        int result = 2 + 3;
        assertEquals(5, result); // Passes if result is 5
    }
}
```

---

## 🔧 **Commonly Used Assertion Methods in JUnit 5**

| Assertion Method                            | Description                                                |
| ------------------------------------------- | ---------------------------------------------------------- |
| `assertEquals(expected, actual)`            | ✅ Checks if values are equal                               |
| `assertNotEquals(expected, actual)`         | ❌ Checks values are **not** equal                          |
| `assertTrue(condition)`                     | ✅ Checks if condition is true                              |
| `assertFalse(condition)`                    | ❌ Checks if condition is false                             |
| `assertNull(value)`                         | ✅ Checks if value is `null`                                |
| `assertNotNull(value)`                      | ❌ Checks if value is **not** `null`                        |
| `assertArrayEquals(expected, actual)`       | ✅ Checks if two arrays are equal                           |
| `assertThrows(Exception.class, () -> code)` | ✅ Verifies that a specific exception is thrown             |
| `assertAll(...)`                            | ✅ Groups multiple assertions, all must pass                |
| `fail(message)`                             | ❌ Forces a test to fail (used for unreachable code checks) |

---

## 🧪 **Examples of Assertions**

### 🔹 `assertEquals`

```java
assertEquals(10, calculator.add(7, 3));
```

### 🔹 `assertNotEquals`

```java
assertNotEquals(5, calculator.subtract(10, 3));
```

### 🔹 `assertTrue` / `assertFalse`

```java
assertTrue(name.startsWith("A"));
assertFalse(list.isEmpty());
```

### 🔹 `assertNull` / `assertNotNull`

```java
assertNull(result);
assertNotNull(user.getId());
```

### 🔹 `assertThrows`

```java
assertThrows(ArithmeticException.class, () -> {
    int x = 1 / 0;
});
```

### 🔹 `assertAll` (Grouped assertions)

```java
assertAll("User Properties",
    () -> assertEquals("John", user.getName()),
    () -> assertNotNull(user.getEmail()),
    () -> assertTrue(user.getAge() > 18)
);
```

### 🔹 `fail`

```java
if (someUnexpectedCondition) {
    fail("This code path should never be reached!");
}
```

---

## 🧠 Summary

| Use Case           | Assertion Method                   |
| ------------------ | ---------------------------------- |
| Check equality     | `assertEquals` / `assertNotEquals` |
| Boolean conditions | `assertTrue` / `assertFalse`       |
| Null checks        | `assertNull` / `assertNotNull`     |
| Exception testing  | `assertThrows`                     |
| Group checks       | `assertAll`                        |
| Force fail         | `fail`                             |

---

## 10. What is the use of `assertThrows()`?

The `assertThrows()` is a very useful assertion in JUnit that allows you to **verify that a specific exception is thrown** during the execution of a block of code.

---

## ✅ **What Is the Purpose of `assertThrows()`?**

The primary use of `assertThrows()` is to **verify that the code under test throws the expected exception** when it encounters a particular condition. This is important for testing **error handling** and **exceptional conditions** in your code.

If the **expected exception** is not thrown, the test will **fail**.

---

## 🔧 **Syntax of `assertThrows()`**

```java
assertThrows(ExpectedException.class, () -> {
    // Code that should throw the exception
});
```

* **`ExpectedException.class`**: The class type of the expected exception (e.g., `IllegalArgumentException.class`).
* **Code Block**: The code that you expect to throw the exception when executed.

---

## 🧪 **Example of `assertThrows()`**

### Scenario: We want to test a method that throws an exception when dividing by zero.

```java
public class Calculator {
    public int divide(int a, int b) {
        if (b == 0) {
            throw new ArithmeticException("Cannot divide by zero");
        }
        return a / b;
    }
}
```

### Test Class Using `assertThrows()`

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {

    @Test
    void testDivideByZero() {
        Calculator calculator = new Calculator();

        // Verify that an ArithmeticException is thrown when dividing by zero
        assertThrows(ArithmeticException.class, () -> {
            calculator.divide(10, 0); // This should throw ArithmeticException
        });
    }
}
```

---

## 🔍 **Explanation of the Example**

1. **Method to Test**: The `divide` method throws an `ArithmeticException` if you try to divide by zero.

2. **Assertion**: `assertThrows(ArithmeticException.class, () -> calculator.divide(10, 0))`

    * We are asserting that **an `ArithmeticException`** is thrown when calling `calculator.divide(10, 0)`.

3. If the exception is thrown, the test will pass. If no exception or a different exception is thrown, the test will fail.

---

## 🔧 **Why Use `assertThrows()`?**

* **Test Negative Cases**: You can ensure that your code behaves correctly when given invalid input.
* **Check Specific Exceptions**: You can validate that a specific type of exception is thrown (e.g., `IllegalArgumentException`, `NullPointerException`, `ArithmeticException`).
* **Test Error Handling**: Ensures that your error-handling logic (e.g., `try-catch` blocks) works as expected.

---

## 🧠 **Key Takeaways**

| Assertion        | Purpose                                                              |
| ---------------- | -------------------------------------------------------------------- |
| `assertThrows()` | Verifies that the **expected exception** is thrown by the code block |

---

## 11. How do you disable a test case in JUnit?

In JUnit, sometimes you may want to **temporarily disable** a test case (e.g., while working on it, debugging, or skipping known issues). This can be done easily with annotations.

---

## ✅ **Disabling a Test in JUnit**

In JUnit 5, you can disable a test using the `@Disabled` annotation.

---

### 🔧 **Using `@Disabled` in JUnit 5**

The `@Disabled` annotation is used to **skip a test method or an entire class**. When a test is disabled, JUnit will **not execute** it during the test run.

#### Syntax

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.Disabled;

public class MyTests {

    @Test
    @Disabled("Test is disabled temporarily due to known bug")
    void testSomething() {
        // This test will be skipped
    }

    @Test
    void testAnotherThing() {
        // This test will run as usual
    }
}
```

### 🧪 **What Happens**

* The **`testSomething()`** will be **skipped** during test execution, and no result (pass/fail) will be recorded for it.
* The **`testAnotherThing()`** will be executed as normal.

---

## 📅 **Optional: Adding a Reason to Disable**

The `@Disabled` annotation can also accept a **reason** as a parameter to explain why the test is disabled:

```java
@Disabled("Temporarily disabled due to issue #123")
```

This message will be shown in the test report or logs, providing context for the decision to disable the test.

---

## ⚙️ **Disabling an Entire Test Class**

You can also disable all tests in a class by adding `@Disabled` at the **class level**:

```java
@Disabled("All tests in this class are disabled due to refactor")
public class RefactorTests {

    @Test
    void testA() {
        // This test will not run
    }

    @Test
    void testB() {
        // This test will not run
    }
}
```

---

## 🔒 **When to Use `@Disabled`**

* **Temporarily Disable Tests**: For tests that are under development or temporarily known to fail.
* **Known Bugs or Limitations**: When there's a bug that prevents a test from passing and you don't want to fail the entire test suite.
* **Test Maintenance**: If tests need updates and are not currently relevant for the build, disable them until they're fixed.

---

## 🧠 **Key Points**

| Annotation  | Purpose                                                     |
| ----------- | ----------------------------------------------------------- |
| `@Disabled` | Skips or disables the execution of the test method or class |

---

## 12. What is the purpose of `@Nested` in JUnit 5?

The `@Nested` annotation in JUnit 5 is a powerful feature that allows you to **group related test methods** inside a test class. This is particularly useful for **organizing** tests when you have a **complex class with multiple behaviors** that need to be tested in different scenarios.

---

## ✅ **What Is the Purpose of `@Nested`?**

The `@Nested` annotation allows you to define **nested test classes** inside a test class, which can help:

1. **Group tests by functionality or feature**.
2. **Create more readable, structured test cases** by grouping related tests under logical sections.
3. **Share setup (`@BeforeEach`, `@AfterEach`)** within a specific group of tests.
4. **Improve organization** when testing different states or conditions of a class.

---

## 🔧 **How to Use `@Nested`**

A nested test class is a class annotated with `@Nested` within another test class.

### 🧪 **Example: Grouping Related Tests Using `@Nested`**

Let’s say you have a `BankAccount` class that allows for deposit and withdrawal.

### 🔹 BankAccount.java (Class Under Test)

```java
public class BankAccount {
    private int balance = 0;

    public void deposit(int amount) {
        balance += amount;
    }

    public void withdraw(int amount) {
        if (amount > balance) {
            throw new IllegalArgumentException("Insufficient funds");
        }
        balance -= amount;
    }

    public int getBalance() {
        return balance;
    }
}
```

### 🔹 BankAccountTest.java (JUnit Test Class)

```java
import org.junit.jupiter.api.*;

import static org.junit.jupiter.api.Assertions.*;

public class BankAccountTest {

    BankAccount account;

    @BeforeEach
    void setUp() {
        account = new BankAccount();
    }

    @Nested
    class DepositTests {

        @Test
        void testDepositIncreasesBalance() {
            account.deposit(100);
            assertEquals(100, account.getBalance());
        }

        @Test
        void testDepositMultipleTimes() {
            account.deposit(50);
            account.deposit(50);
            assertEquals(100, account.getBalance());
        }
    }

    @Nested
    class WithdrawalTests {

        @Test
        void testWithdrawDecreasesBalance() {
            account.deposit(100);
            account.withdraw(50);
            assertEquals(50, account.getBalance());
        }

        @Test
        void testWithdrawThrowsExceptionIfInsufficientFunds() {
            account.deposit(50);
            assertThrows(IllegalArgumentException.class, () -> account.withdraw(100));
        }
    }
}
```

---

### 🧑‍🏫 **Explanation of Code**

* **`@Nested`**: The `DepositTests` and `WithdrawalTests` classes are annotated with `@Nested`, which means they are logically grouped under the main test class `BankAccountTest`. These nested classes group the deposit-related tests and withdrawal-related tests.
* **Test Structure**: Each nested class contains tests related to its feature, and you can organize your tests in a way that matches the structure of your class.
* **Setup**: The `setUp()` method in the outer class is shared among the nested tests, so you don't need to duplicate the initialization of the `BankAccount` object.

### ✅ **What You Get With `@Nested`**

* **Logical Grouping**: Group tests by related functionality, like deposits and withdrawals.
* **Cleaner Tests**: Avoid mixing different types of tests in the same class.
* **Better Readability**: Makes it easier to understand and maintain tests when features grow.

---

## ⚙️ **Important Considerations**

* **Test Lifecycle**: Each nested class can still use `@BeforeEach` and `@AfterEach` methods, but these will be executed **for each test method in the nested class**.
* **Scope of Variables**: Instance variables (e.g., `account`) are **shared between all test methods** in the **outer class**, but they should be re-initialized in `@BeforeEach` to ensure a fresh state for each test.

---

## 🧠 **Key Takeaways**

| Feature        | Description                                                        |
| -------------- | ------------------------------------------------------------------ |
| `@Nested`      | Used to define **nested test classes** within a test class         |
| Grouping Tests | Helps group related test methods logically                         |
| Reusability    | Shared setup code is easy to reuse across nested tests             |
| Test Structure | Organizes tests in a hierarchical structure, improving readability |

---

## 13. What is parameterized testing in JUnit?

**Parameterized testing** in JUnit is a technique that allows you to run the same test with **multiple sets of input data**. This helps to **avoid writing repetitive test code** and makes your tests more efficient by testing various scenarios with minimal code.

---

## ✅ **Purpose of Parameterized Testing**

* **Test a method with multiple inputs**: Instead of writing individual test methods for each set of input data, parameterized tests allow you to run the same test logic with different parameters.
* **Code Reusability**: Reduces the need for writing multiple test methods for similar logic, leading to cleaner and more maintainable test code.
* **Improves Test Coverage**: Tests various combinations of inputs in one place.

---

## 🔧 **How to Write Parameterized Tests in JUnit 5**

JUnit 5 supports parameterized tests through the `@ParameterizedTest` annotation. You use this annotation in combination with **source annotations** that provide data to the test method.

### 🧪 **Basic Example: Using `@ParameterizedTest` with `@ValueSource`**

Let’s say you want to test the `isEven()` method, which checks if a number is even.

#### 🔹 Code Under Test

```java
public class MathUtils {
    public boolean isEven(int number) {
        return number % 2 == 0;
    }
}
```

#### 🔹 Parameterized Test Using `@ValueSource`

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.ValueSource;

import static org.junit.jupiter.api.Assertions.*;

public class MathUtilsTest {

    MathUtils mathUtils = new MathUtils();

    @ParameterizedTest
    @ValueSource(ints = {2, 4, 6, 8})  // Test with multiple even numbers
    void testIsEven(int number) {
        assertTrue(mathUtils.isEven(number));  // Should be true for even numbers
    }

    @ParameterizedTest
    @ValueSource(ints = {1, 3, 5, 7})  // Test with multiple odd numbers
    void testIsNotEven(int number) {
        assertFalse(mathUtils.isEven(number));  // Should be false for odd numbers
    }
}
```

### 🔍 **Explanation**

* **`@ParameterizedTest`**: Marks the test method to run **multiple times** with different parameters.
* **`@ValueSource`**: Provides a source of input values for the test method. In this example, we use `@ValueSource(ints = {...})` to provide an array of integers.
* **Test Method**: The method `testIsEven` will be executed **once for each value** in the `@ValueSource` array. The value of each test run is passed into the method as the `number` parameter.

---

## 🔧 **Other Common Source Annotations**

1. **`@ValueSource`**: Used to provide a list of simple values like integers, strings, etc.

    * Example: `@ValueSource(ints = {1, 2, 3})`

2. **`@CsvSource`**: Provides a source of CSV (comma-separated) values. Useful for testing multiple parameters.

    * Example:

   ```java
   @ParameterizedTest
   @CsvSource({
       "1, 2, 3",  // First set: 1 + 2 = 3
       "2, 3, 5",  // Second set: 2 + 3 = 5
       "4, 5, 9"   // Third set: 4 + 5 = 9
   })
   void testAddition(int a, int b, int expectedResult) {
       assertEquals(expectedResult, a + b);
   }
   ```

3. **`@MethodSource`**: Provides test data from a static method that returns a stream of arguments.

    * Example:

   ```java
   @ParameterizedTest
   @MethodSource("numberProvider")
   void testEvenNumbers(int number) {
       assertTrue(number % 2 == 0);
   }

   static Stream<Integer> numberProvider() {
       return Stream.of(2, 4, 6, 8);
   }
   ```

4. **`@EnumSource`**: Provides test data from an enum type.

    * Example:

   ```java
   enum Color { RED, GREEN, BLUE }

   @ParameterizedTest
   @EnumSource(Color.class)  // Tests with all enum constants
   void testEnum(Color color) {
       assertNotNull(color);
   }
   ```

---

## ⚙️ **Benefits of Parameterized Tests**

* **Less Repetition**: You don’t need to write multiple test methods for different inputs. The same logic can be tested with various inputs using the same test method.
* **Improved Test Coverage**: Test the same logic across different edge cases or input combinations efficiently.
* **Clearer Test Code**: Makes tests more compact and easier to maintain.

---

## 🧠 **Key Takeaways**

| Feature              | Description                                                 |
| -------------------- | ----------------------------------------------------------- |
| `@ParameterizedTest` | Marks a test method as a parameterized test.                |
| `@ValueSource`       | Provides a list of simple values (e.g., ints, strings).     |
| `@CsvSource`         | Provides test data in CSV format (multiple parameters).     |
| `@MethodSource`      | Uses a method to provide arguments for parameterized tests. |
| `@EnumSource`        | Provides values from an enum type.                          |

---

## 14. How do you write a parameterized test in JUnit 5?

Writing **parameterized tests** in JUnit 5 is quite simple and flexible. It allows you to run the same test method with different sets of input data, making your test code more concise, reusable, and efficient.

### 🔧 **Steps to Write a Parameterized Test in JUnit 5**

1. **Use `@ParameterizedTest`** to mark a test method as parameterized.
2. **Provide a source of parameters** for the test method using one of the available annotations, like `@ValueSource`, `@CsvSource`, `@MethodSource`, or `@EnumSource`.
3. **Write assertions** inside the test method to check if the result matches the expected output for each parameter set.

---

## 🧪 **Examples of Parameterized Tests in JUnit 5**

### 1. **Using `@ValueSource`**

The `@ValueSource` annotation is used to provide a simple list of values (such as integers, strings, etc.) to a test method. It's one of the most common ways to write parameterized tests when you only need a single argument for each test.

#### **Example: Testing Even Numbers**

Let’s say we want to test if the numbers are even.

#### Code Under Test (Method)

```java
public class MathUtils {
    public boolean isEven(int number) {
        return number % 2 == 0;
    }
}
```

#### Parameterized Test Class

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.ValueSource;
import static org.junit.jupiter.api.Assertions.*;

public class MathUtilsTest {

    MathUtils mathUtils = new MathUtils();

    @ParameterizedTest
    @ValueSource(ints = {2, 4, 6, 8})  // Passing even numbers
    void testIsEven(int number) {
        assertTrue(mathUtils.isEven(number));  // Should return true for even numbers
    }

    @ParameterizedTest
    @ValueSource(ints = {1, 3, 5, 7})  // Passing odd numbers
    void testIsNotEven(int number) {
        assertFalse(mathUtils.isEven(number));  // Should return false for odd numbers
    }
}
```

### **Explanation**:

* `@ParameterizedTest` marks the test method as parameterized.
* `@ValueSource(ints = {2, 4, 6, 8})` provides a set of integers (even numbers) for the test.
* The test will be run **once for each value in the `@ValueSource` array**.

---

### 2. **Using `@CsvSource`**

`@CsvSource` allows you to provide **multiple arguments** for each test case in a **CSV format**. It’s useful when you need to pass **multiple parameters** to the test method.

#### **Example: Testing Addition**

We can use `@CsvSource` to test an addition method with multiple sets of input parameters and expected results.

#### Code Under Test (Method)

```java
public class MathUtils {
    public int add(int a, int b) {
        return a + b;
    }
}
```

#### Parameterized Test Class

```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvSource;
import static org.junit.jupiter.api.Assertions.*;

public class MathUtilsTest {

    MathUtils mathUtils = new MathUtils();

    @ParameterizedTest
    @CsvSource({
        "1, 2, 3",    // Test: 1 + 2 = 3
        "2, 3, 5",    // Test: 2 + 3 = 5
        "4, 5, 9"     // Test: 4 + 5 = 9
    })
    void testAddition(int a, int b, int expectedSum) {
        assertEquals(expectedSum, mathUtils.add(a, b));  // Check if the sum is correct
    }
}
```

### **Explanation**:

* `@CsvSource` allows you to specify **multiple parameters** in each test case as comma-separated values.
* The method `testAddition` is executed once for each row in the `@CsvSource` list, and the values are passed into the method as parameters.

---

### 3. **Using `@MethodSource`**

`@MethodSource` provides a way to pass test data from an **external method**. The method that provides the data can return a stream, collection, or array of arguments.

#### **Example: Using a Method to Provide Parameters**

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.MethodSource;
import static org.junit.jupiter.api.Assertions.*;

import java.util.stream.Stream;

public class MathUtilsTest {

    MathUtils mathUtils = new MathUtils();

    // Test data provider method
    static Stream<int[]> additionTestData() {
        return Stream.of(
            new int[] {1, 2, 3},
            new int[] {2, 3, 5},
            new int[] {4, 5, 9}
        );
    }

    @ParameterizedTest
    @MethodSource("additionTestData")  // Link to the method providing test data
    void testAddition(int a, int b, int expectedSum) {
        assertEquals(expectedSum, mathUtils.add(a, b));  // Check if the sum is correct
    }
}
```

### **Explanation**:

* The **`additionTestData`** method provides the test data as a stream of integer arrays.
* The `@MethodSource("additionTestData")` tells JUnit to call the `additionTestData` method to retrieve the test data.
* The test method is executed for each array returned by the `additionTestData` method.

---

### 4. **Using `@EnumSource`**

`@EnumSource` is used to run a parameterized test with each value from an **enum type**.

#### **Example: Testing Enum Values**

Suppose you have an enum for the days of the week, and you want to test if the `isWeekend` method works correctly.

#### Code Under Test (Method)

```java
public enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY;

    public boolean isWeekend() {
        return this == SATURDAY || this == SUNDAY;
    }
}
```

#### Parameterized Test Class

```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.EnumSource;
import static org.junit.jupiter.api.Assertions.*;

public class DayTest {

    @ParameterizedTest
    @EnumSource(Day.class)  // All enum constants will be used as test data
    void testIsWeekend(Day day) {
        if (day == Day.SATURDAY || day == Day.SUNDAY) {
            assertTrue(day.isWeekend());  // Check if weekends return true
        } else {
            assertFalse(day.isWeekend());  // Check if weekdays return false
        }
    }
}
```

### **Explanation**:

* `@EnumSource(Day.class)` provides all constants from the `Day` enum as parameters to the test method.
* The test checks if `isWeekend` returns the correct result for each day.

---

## 🧠 **Key Points to Remember**

| Annotation           | Description                                             |
| -------------------- | ------------------------------------------------------- |
| `@ParameterizedTest` | Marks the test as parameterized.                        |
| `@ValueSource`       | Provides simple values (e.g., ints, strings) to a test. |
| `@CsvSource`         | Provides multiple parameters per test in CSV format.    |
| `@MethodSource`      | Provides parameters from an external method.            |
| `@EnumSource`        | Provides parameters from enum constants.                |

---

## 15. What is the use of `@Tag` and how do you filter test execution based on tags?

The `@Tag` annotation in JUnit 5 is used to **categorize** and **filter** tests based on tags, making it easier to organize and execute specific subsets of tests. Tags can be used to group tests by functionality, importance, or any other categorization that makes sense for your project. You can also use tags to **filter tests** during test execution, such as running only tests that have a specific tag or excluding certain tests from being executed.

---

## ✅ **Purpose of `@Tag` in JUnit 5**

* **Categorization**: Helps organize tests by categories, such as "smoke", "performance", "regression", etc.
* **Test Filtering**: Allows you to run or exclude specific tests based on the tag(s) they are associated with.
* **Test Reporting**: Makes it easier to analyze test results by grouping tests in the reports based on their tags.

---

## 🔧 **Using `@Tag` in JUnit 5**

The `@Tag` annotation can be applied at the class level or the method level. You can use one or more tags to categorize tests.

### 🔹 **Example: Using `@Tag` to Categorize Tests**

Let’s say you have tests that are categorized into "smoke" tests and "regression" tests.

#### **Test Class with Tags**

```java
import org.junit.jupiter.api.Tag;
import org.junit.jupiter.api.Test;

import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {

    @Test
    @Tag("smoke")
    void testAddition() {
        assertEquals(5, 2 + 3);
    }

    @Test
    @Tag("regression")
    void testSubtraction() {
        assertEquals(2, 5 - 3);
    }

    @Test
    @Tag("smoke")
    void testMultiplication() {
        assertEquals(6, 2 * 3);
    }

    @Test
    @Tag("regression")
    void testDivision() {
        assertEquals(2, 6 / 3);
    }
}
```

### **Explanation**:

* The test methods `testAddition()` and `testMultiplication()` are tagged with `"smoke"`, while `testSubtraction()` and `testDivision()` are tagged with `"regression"`.
* You can now group these tests into categories, making it easy to filter them when running the tests.

---

## 🔧 **Filtering Test Execution Based on Tags**

JUnit 5 provides multiple ways to filter tests based on tags. You can filter tests using **JUnit command line options** or through **build tools** like Maven or Gradle.

### 🔹 **Using `@Tag` with Maven**

If you're using Maven, you can specify which tests to include or exclude based on tags when running the tests with the `mvn` command.

#### **Running Tests with Specific Tags (e.g., "smoke")**

To run only tests with the `"smoke"` tag, you can use the following command:

```bash
mvn test -Dgroups="smoke"
```

#### **Excluding Tests with Specific Tags**

To **exclude** tests with a certain tag, you can use the following command:

```bash
mvn test -Dgroups="!regression"
```

### 🔹 **Using `@Tag` with Gradle**

If you're using Gradle, you can filter tests by tags in the `build.gradle` file or through the command line.

#### **Running Tests with Specific Tags**

In `build.gradle`:

```groovy
test {
    useJUnitPlatform {
        includeTags 'smoke'
    }
}
```

Command line:

```bash
gradle test --include-tags smoke
```

#### **Excluding Tests with Specific Tags**

In `build.gradle`:

```groovy
test {
    useJUnitPlatform {
        excludeTags 'regression'
    }
}
```

Command line:

```bash
gradle test --exclude-tags regression
```

### 🔹 **Using `@Tag` with IDEs (e.g., IntelliJ IDEA)**

If you're using an IDE like IntelliJ IDEA, you can filter tests based on tags directly through the test runner configuration.

1. In IntelliJ IDEA, right-click on the test class or method and select **Run with Coverage** or **Run**.
2. Under **Run/Debug Configurations**, you can specify tags using the **JUnit** runner's **Tags** option.

---

## 🧑‍🏫 **Example: Filtering Tests Based on Tags**

Let’s assume the same `CalculatorTest` from earlier, where we have `"smoke"` and `"regression"` tags.

If you only want to run the **smoke tests**, you can configure Maven, Gradle, or your IDE to run only tests that are tagged as `"smoke"`.

#### Maven Command:

```bash
mvn test -Dgroups="smoke"
```

#### Gradle Command:

```bash
gradle test --include-tags smoke
```

#### IntelliJ IDEA:

* Use the test runner configuration to **include only the `"smoke"` tag**.

---

## ✅ **Key Benefits of `@Tag`**

| Feature                 | Description                                                                           |
| ----------------------- | ------------------------------------------------------------------------------------- |
| **Categorization**      | Helps categorize tests into logical groups (e.g., smoke, regression, etc.).           |
| **Filtering Execution** | Allows filtering tests based on tags (e.g., running only smoke tests).                |
| **Organizing Tests**    | Makes it easier to maintain large test suites by grouping related tests.              |
| **Selective Execution** | Run only a subset of tests for specific scenarios (e.g., CI/CD, pre-release testing). |

---

## 🧠 **Key Takeaways**

* **`@Tag`** is used to **categorize** tests and **filter** them during execution based on their tags.
* You can apply multiple tags to a test method or class to categorize it into different categories.
* Tags can be used with build tools (e.g., Maven, Gradle) or IDEs to selectively run tests based on tags.

---

## 16. How do you run a group of test classes together?

Running a group of test classes together in JUnit can be done in several ways, depending on your needs and the tools you're using. In JUnit 5, there are a few common methods to group and execute multiple test classes together.

### 1. **Using a Test Suite (JUnit 5)**

JUnit 5 does not provide a direct "suite" mechanism like JUnit 4 does. Instead, it uses the `@SelectClasses` and `@SelectPackages` annotations to specify which test classes to run.

#### **Example: Grouping Test Classes with `@SelectClasses`**

You can create a suite class to group multiple test classes together. Here's an example:

#### **Test Suite Class (JUnit 5)**

```java
import org.junit.platform.suite.api.SelectClasses;
import org.junit.platform.suite.api.Suite;

@Suite
@SelectClasses({CalculatorTest.class, MathUtilsTest.class, UserServiceTest.class})
public class TestSuite {
    // No test methods here, just a grouping mechanism
}
```

### **Explanation:**

* `@Suite`: This annotation marks the class as a test suite.
* `@SelectClasses`: This annotation tells JUnit to include specific classes in the test suite. In this case, we are running `CalculatorTest`, `MathUtilsTest`, and `UserServiceTest` together.

To run the suite, you would simply execute the `TestSuite` class, and it will run all the tests from the specified classes.

#### **Alternative: Using `@SelectPackages`**

If you have all your tests in a specific package and want to run them together, you can use `@SelectPackages`:

```java
import org.junit.platform.suite.api.SelectPackages;
import org.junit.platform.suite.api.Suite;

@Suite
@SelectPackages("com.myapp.tests")  // Specifies the package containing all tests
public class TestSuite {
    // No test methods here, just a grouping mechanism
}
```

### 2. **Using Maven**

With Maven, you can specify groups of test classes to run using **test suites** or **profiles** in the `pom.xml` file.

#### **Example: Running Test Suites in Maven**

In JUnit 5, you would generally use **`maven-surefire-plugin`** to run your tests. You can group test classes in the `pom.xml` file by specifying the classes or packages you want to include in the tests.

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-surefire-plugin</artifactId>
            <version>3.0.0-M5</version>
            <configuration>
                <suiteXmlFiles>
                    <suiteXmlFile>src/test/resources/testng.xml</suiteXmlFile>
                </suiteXmlFiles>
            </configuration>
        </plugin>
    </plugins>
</build>
```

In this configuration, you can link to a test suite XML file (such as TestNG XML), which includes all the classes you want to run together.

Alternatively, you can define specific test classes directly in the configuration:

```xml
<configuration>
    <includes>
        <include>**/CalculatorTest.class</include>
        <include>**/MathUtilsTest.class</include>
    </includes>
</configuration>
```

### 3. **Using Gradle**

In **Gradle**, you can group multiple test classes or packages together for execution by configuring the `test` task.

#### **Example: Running Specific Test Classes in Gradle**

You can specify which test classes to run using the `include` method inside the `test` block of your `build.gradle` file:

```groovy
test {
    useJUnitPlatform()  // Use JUnit 5
    include '**/CalculatorTest.class'
    include '**/MathUtilsTest.class'
}
```

This configuration will ensure that only `CalculatorTest` and `MathUtilsTest` are executed.

#### **Example: Running Tests from a Package in Gradle**

You can also include tests by package:

```groovy
test {
    useJUnitPlatform()  // Use JUnit 5
    include '**/tests/CalculatorTest.class'
    include '**/tests/MathUtilsTest.class'
}
```

This configuration runs all the tests in the specified classes or packages.

---

## 4. **Using IDEs (e.g., IntelliJ IDEA, Eclipse)**

Most Integrated Development Environments (IDEs) like IntelliJ IDEA or Eclipse allow you to run multiple test classes together by creating **Run Configurations**. Here's how you can do it:

### 🔹 **IntelliJ IDEA**

1. **Select Multiple Test Classes**: In the Project pane, select the test classes you want to run.
2. **Right-click and Choose "Run"**: Right-click on the selected classes and choose "Run".
3. **Create a Run Configuration**:

    * Go to **Run > Edit Configurations**.
    * Click the **"+"** icon to create a new configuration.
    * Choose **JUnit** and specify the classes or packages to be included.

### 🔹 **Eclipse**

1. **Select Multiple Test Classes**: In the Project Explorer, hold down **Ctrl** (or **Cmd** on macOS) and select the test classes.
2. **Right-click and Choose "Run As > JUnit Test"**.

---

## ✅ **Key Points for Running Test Classes Together**

* **JUnit 5**: Use `@Suite` along with `@SelectClasses` or `@SelectPackages` to group tests.
* **Maven**: Specify test suites or classes in the `pom.xml` using the `maven-surefire-plugin`.
* **Gradle**: Use the `test` task in `build.gradle` to specify which tests to run.
* **IDEs**: Most IDEs allow you to create **Run Configurations** to run multiple test classes together.

---

## 17. How can you test exceptions using JUnit?

Testing exceptions in JUnit ensures that your code behaves as expected when it encounters error conditions. JUnit provides several ways to verify that exceptions are thrown during testing. In JUnit 5, there are specific mechanisms to handle exception testing.

### Methods for Testing Exceptions in JUnit 5

#### 1. **Using `assertThrows()`**

The most common and recommended approach to test if an exception is thrown in JUnit 5 is by using the `assertThrows()` method.

* **`assertThrows()`** checks whether a specific exception is thrown during the execution of a block of code (like a lambda expression).
* It also allows you to assert that the exception message or other properties are correct.

#### Syntax:

```java
assertThrows(ExpectedExceptionType.class, () -> {
    // Code that should throw the exception
});
```

#### Example: Testing an Exception using `assertThrows()`

Consider the following method that divides two numbers:

```java
public class Calculator {
    public int divide(int dividend, int divisor) {
        if (divisor == 0) {
            throw new ArithmeticException("Cannot divide by zero");
        }
        return dividend / divisor;
    }
}
```

To test this method for an exception when dividing by zero, you can write the following test case:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class CalculatorTest {

    @Test
    void testDivideByZeroThrowsException() {
        Calculator calculator = new Calculator();

        // Using assertThrows to check if ArithmeticException is thrown
        ArithmeticException exception = assertThrows(ArithmeticException.class, () -> {
            calculator.divide(5, 0);
        });

        // You can also assert the message of the exception
        assertEquals("Cannot divide by zero", exception.getMessage());
    }
}
```

### **Explanation:**

* **`assertThrows(ArithmeticException.class, () -> calculator.divide(5, 0))`**: This checks if the `divide` method throws an `ArithmeticException` when dividing by zero.
* **`assertEquals("Cannot divide by zero", exception.getMessage())`**: After catching the exception, we assert that the exception message matches the expected message.

---

#### 2. **Using `@Test` with `expected` Attribute (JUnit 4-style)**

In JUnit 4, you could use the `expected` attribute in the `@Test` annotation to specify the type of exception that should be thrown. However, in JUnit 5, this approach is **deprecated**, and you should prefer `assertThrows()` instead.

**JUnit 4 Example:**

```java
@Test(expected = ArithmeticException.class)
public void testDivideByZero() {
    Calculator calculator = new Calculator();
    calculator.divide(5, 0);
}
```

While this works in JUnit 4, **JUnit 5 does not support the `expected` attribute in the `@Test` annotation**, so it's better to use `assertThrows()` for exception handling.

---

#### 3. **Testing Multiple Exception Types (Chaining with `assertThrows`)**

You can also test for multiple exception types or a variety of exceptions by chaining `assertThrows()` in your tests. You might want to verify that multiple exceptions can be thrown in different scenarios.

```java
@Test
void testMultipleExceptions() {
    Calculator calculator = new Calculator();

    // Check if ArithmeticException is thrown for divide by zero
    ArithmeticException exception1 = assertThrows(ArithmeticException.class, () -> {
        calculator.divide(5, 0);
    });
    assertEquals("Cannot divide by zero", exception1.getMessage());

    // Check if IllegalArgumentException is thrown for invalid input
    IllegalArgumentException exception2 = assertThrows(IllegalArgumentException.class, () -> {
        throw new IllegalArgumentException("Invalid input");
    });
    assertEquals("Invalid input", exception2.getMessage());
}
```

---

### **Exception Testing in JUnit 5: Key Features**

* **Clearer Assertions**: `assertThrows()` is more flexible and clearer than the old JUnit 4 `expected` attribute.
* **Exception Object Access**: `assertThrows()` gives you access to the actual exception object, so you can check the exception message or other details.
* **Chaining Tests**: You can test multiple exception scenarios within the same test method using `assertThrows()`.

---

### **Additional Tips for Testing Exceptions**

1. **Checking Multiple Aspects of an Exception**:

    * You can assert various properties of the exception like the message, cause, or specific methods (e.g., `getMessage()`, `getCause()`).

   Example:

   ```java
   @Test
   void testExceptionMessageAndCause() {
       IllegalArgumentException exception = assertThrows(IllegalArgumentException.class, () -> {
           throw new IllegalArgumentException("Invalid value", new RuntimeException("Cause of error"));
       });
       assertEquals("Invalid value", exception.getMessage());
       assertEquals("Cause of error", exception.getCause().getMessage());
   }
   ```

2. **Custom Exceptions**:
   If you have custom exceptions, you can test them in the same way as built-in exceptions.

   ```java
   public class CustomException extends RuntimeException {
       public CustomException(String message) {
           super(message);
       }
   }

   @Test
   void testCustomException() {
       assertThrows(CustomException.class, () -> {
           throw new CustomException("Custom exception occurred");
       });
   }
   ```

---

### **Summary**

* **`assertThrows()`** is the preferred and recommended approach to test if exceptions are thrown in JUnit 5.
* The exception is captured and returned so you can assert additional details like the message or cause.
* You should avoid using the `expected` attribute from JUnit 4, as it's not available in JUnit 5.
* Use `assertThrows()` to check for specific exceptions, and you can assert exception messages, causes, or other details.

---

## 18. What is the difference between `assertEquals()` and `assertSame()`?

The difference between `assertEquals()` and `assertSame()` in JUnit primarily lies in how they compare the values being tested. Here’s a breakdown of each method:

### 1. **`assertEquals()`**:

* **Purpose**: It checks if two objects are **equally equivalent** in value, meaning it compares the contents of the objects.
* **Type of Comparison**: It uses the **`equals()`** method of the objects to compare them.
* **When to Use**: Use `assertEquals()` when you want to check if the **values** of two objects are the same, regardless of whether they are the exact same object in memory.

#### Example:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    @Test
    void testEquals() {
        String str1 = new String("Hello");
        String str2 = new String("Hello");

        // Check if the values of str1 and str2 are the same
        assertEquals(str1, str2);  // This will pass because the values are equal ("Hello")
    }
}
```

**Explanation**:

* Here, `str1` and `str2` have the same content ("Hello"), so the assertion passes even though they are **different objects** (because `assertEquals()` checks for value equality).
* Internally, the `equals()` method is used to compare the values of the strings.

---

### 2. **`assertSame()`**:

* **Purpose**: It checks if two objects refer to the **same object in memory**, i.e., whether they are the **same instance**.
* **Type of Comparison**: It uses the **`==`** operator to check for **reference equality** (i.e., they must refer to the exact same object in memory).
* **When to Use**: Use `assertSame()` when you want to ensure that two variables point to the **exact same object** in memory, not just have the same value.

#### Example:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    @Test
    void testSame() {
        String str1 = new String("Hello");
        String str2 = str1;

        // Check if str1 and str2 point to the same object
        assertSame(str1, str2);  // This will pass because str2 refers to the same object as str1
    }
}
```

**Explanation**:

* In this case, `str2` is assigned the reference of `str1`, meaning they both refer to the same object in memory.
* `assertSame(str1, str2)` checks that both `str1` and `str2` point to the **same memory location** and passes because they do.

---

### **Key Differences Between `assertEquals()` and `assertSame()`**

| **Aspect**               | **`assertEquals()`**                                                            | **`assertSame()`**                                                                          |
| ------------------------ | ------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **What it compares**     | Compares the **values** of the objects.                                         | Compares the **memory references** (i.e., whether both variables point to the same object). |
| **Equality Method Used** | Uses the object's **`equals()`** method for comparison.                         | Uses the **`==`** operator to compare memory addresses (references).                        |
| **Typical Use Case**     | Used when you care about the **value** of the objects being the same.           | Used when you care about whether two variables refer to the **same object** in memory.      |
| **Example Use Case**     | Comparing strings, numbers, or other values to see if they are logically equal. | Checking if two references point to the same instance of an object.                         |

---

### **Practical Example**

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

public class ComparisonTest {

    @Test
    void testEqualsExample() {
        String str1 = new String("Test");
        String str2 = new String("Test");

        // This will pass because the values of str1 and str2 are the same.
        assertEquals(str1, str2); // str1 and str2 have the same content "Test"
    }

    @Test
    void testSameExample() {
        String str1 = new String("Test");
        String str2 = str1;

        // This will pass because str2 refers to the same object as str1
        assertSame(str1, str2);  // Both refer to the same memory location
    }
}
```

---

### **Summary of Key Differences**

* **`assertEquals()`** checks if **two objects have the same value** (e.g., `equals()` method for comparing values).
* **`assertSame()`** checks if **two references point to the exact same object in memory** (i.e., reference equality with `==`).

You should choose `assertEquals()` when you're interested in checking if the **values** are the same, and `assertSame()` when you want to confirm that two references point to the **same instance** of an object.

---

## 19. How do you test timeouts in JUnit?

Testing timeouts in JUnit is useful to ensure that your code or test cases do not exceed a certain time limit, helping you detect performance issues or infinite loops. Both JUnit 4 and JUnit 5 provide ways to test timeouts.

### **Testing Timeouts in JUnit 4**

In **JUnit 4**, you can specify a timeout directly in the `@Test` annotation. The test will fail if it exceeds the specified time limit (in milliseconds).

#### **Example**:

```java
import org.junit.Test;
import static org.junit.Assert.*;

public class TimeoutTest {

    @Test(timeout = 1000) // Timeout after 1000 milliseconds (1 second)
    public void testMethod() throws InterruptedException {
        // Simulate a method that runs within the time limit
        Thread.sleep(500); // Sleep for 500ms
        assertTrue(true);
    }

    @Test(timeout = 1000) // Timeout after 1000 milliseconds (1 second)
    public void testMethodWithTimeoutFailure() throws InterruptedException {
        // Simulate a method that exceeds the timeout
        Thread.sleep(1500); // Sleep for 1500ms (Exceeds 1 second timeout)
        assertTrue(true); 
    }
}
```

### **Explanation**:

* **`@Test(timeout = 1000)`**: Specifies that the test method should complete within 1000 milliseconds (1 second). If the method takes longer, the test will fail.
* In the first test, the method runs within the 1000ms timeout, so it passes.
* In the second test, the method sleeps for 1500ms, which exceeds the timeout and causes the test to fail.

---

### **Testing Timeouts in JUnit 5**

In **JUnit 5**, the `@Test` annotation does **not** directly support the `timeout` attribute. Instead, you use the `assertTimeout()` or `assertTimeoutPreemptively()` methods from the `org.junit.jupiter.api.Assertions` class.

#### 1. **Using `assertTimeout()`**

* `assertTimeout()` ensures that the code inside the provided executable completes within the given time limit.
* If the code execution exceeds the timeout, the test fails.

#### **Example**:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

import java.time.Duration;

public class TimeoutTest {

    @Test
    void testMethod() {
        assertTimeout(Duration.ofMillis(1000), () -> {
            // Simulate a method that runs within the time limit
            Thread.sleep(500); // Sleep for 500ms
        });
    }

    @Test
    void testMethodWithTimeoutFailure() {
        assertTimeout(Duration.ofMillis(1000), () -> {
            // Simulate a method that exceeds the timeout
            Thread.sleep(1500); // Sleep for 1500ms (Exceeds 1 second timeout)
        });
    }
}
```

### **Explanation**:

* **`assertTimeout(Duration.ofMillis(1000), executable)`**: The first argument specifies the maximum duration for the test, and the second argument is the **executable block** (like a lambda) that contains the code being tested.
* In the first test, the code sleeps for 500ms, which is within the 1000ms timeout, so it passes.
* In the second test, the code sleeps for 1500ms, which exceeds the timeout, causing the test to fail.

#### 2. **Using `assertTimeoutPreemptively()`**

* **`assertTimeoutPreemptively()`** works similarly to `assertTimeout()` but with a slight difference. It **interrupts** the running test if the timeout is exceeded, making it more suitable for tests where the timeout should stop execution immediately if exceeded.

#### **Example**:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

import java.time.Duration;

public class TimeoutTest {

    @Test
    void testMethodWithPreemptiveTimeout() {
        assertTimeoutPreemptively(Duration.ofMillis(1000), () -> {
            // Simulate a method that exceeds the timeout
            Thread.sleep(1500); // Sleep for 1500ms (Exceeds 1 second timeout)
        });
    }
}
```

### **Explanation**:

* **`assertTimeoutPreemptively(Duration.ofMillis(1000), executable)`**: The test is preemptively terminated if the execution time exceeds the specified duration. This is more strict than `assertTimeout()`, which allows the method to finish before checking the timeout.
* In this case, the method sleeps for 1500ms, which exceeds the timeout and causes the test to fail immediately.

---

### **Key Differences Between `assertTimeout()` and `assertTimeoutPreemptively()`**

| **Method**                        | **Behavior**                                                                             | **Use Case**                                                                       |
| --------------------------------- | ---------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------- |
| **`assertTimeout()`**             | Allows the test method to run to completion, then checks if the time exceeded the limit. | Use when you want the test to run completely before checking the timeout.          |
| **`assertTimeoutPreemptively()`** | Immediately interrupts the test if the timeout is exceeded.                              | Use when you need to ensure the test stops immediately if the timeout is exceeded. |

---

### **Summary**

* **JUnit 4**: Use the `timeout` parameter in the `@Test` annotation to specify the time limit for a test method.
* **JUnit 5**: Use `assertTimeout()` or `assertTimeoutPreemptively()` to test if the code execution stays within the time limit. `assertTimeout()` allows the method to finish before checking the timeout, while `assertTimeoutPreemptively()` stops the method immediately if the timeout is exceeded.

These methods are useful for testing performance or ensuring that your code does not run indefinitely due to bugs like infinite loops.

---

## 20. Can you explain the JUnit lifecycle?

The **JUnit lifecycle** refers to the sequence of events that occur during the execution of a test class in JUnit. Understanding the lifecycle is essential to managing test setup, execution, and teardown efficiently. Both JUnit 4 and JUnit 5 have similar principles in the lifecycle, but there are differences in the specifics, particularly with annotations and how lifecycle hooks are handled.

Here’s an explanation of the JUnit lifecycle:

### **JUnit Lifecycle Overview**

The lifecycle can be broadly divided into the following phases:

1. **Test Class Initialization**
2. **Test Method Execution**
3. **Test Method Cleanup**
4. **Test Class Cleanup**

### **JUnit 4 Lifecycle**

In JUnit 4, the lifecycle hooks are provided by annotations like `@Before`, `@After`, `@BeforeClass`, and `@AfterClass`. Here's the order in which the methods are executed:

1. **Before Class (`@BeforeClass`)**:

    * Runs once before any test methods in the test class.
    * It is used for **one-time setup** for the entire class, such as initializing shared resources.
    * This method must be **static**.

2. **Before (`@Before`)**:

    * Runs before each test method.
    * This is used for **setup** before every individual test, such as initializing test data or objects.
    * **Not static**.

3. **Test Method (`@Test`)**:

    * Runs each test method.
    * The test method contains the code that is being tested.

4. **After (`@After`)**:

    * Runs after each test method.
    * It’s used for **cleanup** after each test, such as clearing test data or releasing resources.
    * **Not static**.

5. **After Class (`@AfterClass`)**:

    * Runs once after all test methods in the test class.
    * It is used for **cleaning up** shared resources, like closing database connections or releasing static resources.
    * This method must be **static**.

#### **JUnit 4 Lifecycle Example**:

```java
import org.junit.Before;
import org.junit.After;
import org.junit.BeforeClass;
import org.junit.AfterClass;
import org.junit.Test;

public class JUnit4LifecycleExample {

    @BeforeClass
    public static void beforeClass() {
        System.out.println("Before Class: Executed once before any tests.");
    }

    @Before
    public void setUp() {
        System.out.println("Before Test: Executed before each test method.");
    }

    @Test
    public void test1() {
        System.out.println("Test 1: Executing test 1.");
    }

    @Test
    public void test2() {
        System.out.println("Test 2: Executing test 2.");
    }

    @After
    public void tearDown() {
        System.out.println("After Test: Executed after each test method.");
    }

    @AfterClass
    public static void afterClass() {
        System.out.println("After Class: Executed once after all tests.");
    }
}
```

#### **Output**:

```
Before Class: Executed once before any tests.
Before Test: Executed before each test method.
Test 1: Executing test 1.
After Test: Executed after each test method.
Before Test: Executed before each test method.
Test 2: Executing test 2.
After Test: Executed after each test method.
After Class: Executed once after all tests.
```

### **JUnit 5 Lifecycle**

In **JUnit 5**, the lifecycle is a bit more flexible and uses annotations like `@BeforeEach`, `@AfterEach`, `@BeforeAll`, and `@AfterAll`. Here’s the execution order:

1. **Before All (`@BeforeAll`)**:

    * Runs once before any test methods in the test class.
    * It’s used for **one-time setup** for the entire test class.
    * **Must be static**, similar to `@BeforeClass` in JUnit 4.

2. **Before Each (`@BeforeEach`)**:

    * Runs before each test method.
    * It’s used to **set up** resources or state before every individual test.
    * **Not static**, unlike `@BeforeClass`.

3. **Test Method (`@Test`)**:

    * The actual test method that executes the test logic.

4. **After Each (`@AfterEach`)**:

    * Runs after each test method.
    * It’s used for **cleanup** after each individual test.
    * **Not static**, unlike `@AfterClass`.

5. **After All (`@AfterAll`)**:

    * Runs once after all test methods in the test class.
    * It’s used for **cleaning up** shared resources or global state.
    * **Must be static**, similar to `@AfterClass` in JUnit 4.

#### **JUnit 5 Lifecycle Example**:

```java
import org.junit.jupiter.api.BeforeAll;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.AfterAll;

public class JUnit5LifecycleExample {

    @BeforeAll
    public static void beforeAll() {
        System.out.println("Before All: Executed once before any tests.");
    }

    @BeforeEach
    public void setUp() {
        System.out.println("Before Each: Executed before each test method.");
    }

    @Test
    public void test1() {
        System.out.println("Test 1: Executing test 1.");
    }

    @Test
    public void test2() {
        System.out.println("Test 2: Executing test 2.");
    }

    @AfterEach
    public void tearDown() {
        System.out.println("After Each: Executed after each test method.");
    }

    @AfterAll
    public static void afterAll() {
        System.out.println("After All: Executed once after all tests.");
    }
}
```

#### **Output**:

```
Before All: Executed once before any tests.
Before Each: Executed before each test method.
Test 1: Executing test 1.
After Each: Executed after each test method.
Before Each: Executed before each test method.
Test 2: Executing test 2.
After Each: Executed after each test method.
After All: Executed once after all tests.
```

### **Key Differences Between JUnit 4 and JUnit 5 Lifecycle**

| **Aspect**                  | **JUnit 4**                              | **JUnit 5**                                                                                |
| --------------------------- | ---------------------------------------- | ------------------------------------------------------------------------------------------ |
| **Before Class**            | `@BeforeClass` (static)                  | `@BeforeAll` (static)                                                                      |
| **Before Each**             | `@Before`                                | `@BeforeEach`                                                                              |
| **Test Method**             | `@Test`                                  | `@Test`                                                                                    |
| **After Each**              | `@After`                                 | `@AfterEach`                                                                               |
| **After Class**             | `@AfterClass` (static)                   | `@AfterAll` (static)                                                                       |
| **Annotations for Setup**   | `@BeforeClass`, `@Before`                | `@BeforeAll`, `@BeforeEach`                                                                |
| **Annotations for Cleanup** | `@AfterClass`, `@After`                  | `@AfterAll`, `@AfterEach`                                                                  |
| **Flexibility**             | Limited flexibility with lifecycle hooks | More flexibility and enhanced capabilities like `@Nested` classes and lifecycle extensions |

### **Other Lifecycle Considerations in JUnit 5**

#### **`@Nested` Classes**:

* **JUnit 5** allows you to use `@Nested` classes, which have their own lifecycle methods. These are especially useful for grouping related tests.

#### **Lifecycle Extensions**:

* **JUnit 5** provides more flexibility in lifecycle management through extensions. You can create custom extensions to hook into specific lifecycle events, such as before or after all tests.

---

### **Summary**

* **JUnit 4**:

    * `@BeforeClass` and `@AfterClass` run once for the entire class (must be static).
    * `@Before` and `@After` run before and after each test method.
* **JUnit 5**:

    * `@BeforeAll` and `@AfterAll` run once for the entire class (must be static).
    * `@BeforeEach` and `@AfterEach` run before and after each test method.
    * JUnit 5 provides more flexibility with lifecycle hooks and supports `@Nested` classes and extensions.

Understanding the lifecycle of JUnit tests ensures that setup and cleanup are handled correctly, and tests are isolated, making them more reliable and maintainable.

Let me know if you'd like to explore more about the lifecycle in JUnit or specific use cases!

---

### 🔹 21–40: **Mockito (Mocking & Stubbing)**

## 21. What is Mockito?

**Mockito** is a popular **mocking framework** used in unit testing in Java. It allows you to create mock objects, which simulate the behavior of real objects for the purpose of testing. This is particularly useful in unit testing when the real objects or external dependencies (like databases, web services, file systems, etc.) are difficult to work with or not necessary to the scope of the unit test.

Mocking is the process of simulating the behavior of complex objects in isolation. With Mockito, you can **mock interfaces or classes** and define their behavior to ensure that your tests are focused on the logic of the code you're testing rather than on the behavior of external components.

### **Key Features of Mockito**:

* **Mocking**: Create mock objects that simulate the behavior of real objects.
* **Stubbing**: Specify what a mock object should return when specific methods are called.
* **Verification**: Check if certain methods were called on a mock object.
* **Spy**: Create a partial mock where some methods of the real object are called and others are stubbed.

### **Why Use Mockito?**

* **Isolation**: Mockito helps isolate the unit being tested by replacing external dependencies with mocks. This ensures tests focus on specific logic without being affected by external systems.
* **Control**: You can control the behavior of mocked dependencies, making it easier to test different scenarios (success, failure, edge cases).
* **No Need for Actual Implementations**: Mockito allows you to mock complex or hard-to-test objects without needing their actual implementation, improving test speed and reliability.
* **Simplifies Testing**: It simplifies testing by allowing you to mock out dependencies instead of requiring an actual implementation.

---

### **Basic Concepts in Mockito**

1. **Mocking**: Creating mock objects of a class or interface.
2. **Stubbing**: Defining the behavior of the mocked objects (i.e., what a mocked method should return when invoked).
3. **Verification**: Checking that certain interactions with mocks took place (e.g., did a method get called a certain number of times?).
4. **Spying**: Partial mocking of real objects (keeping real behavior for some methods while mocking others).

### **Mockito Annotations**

* **@Mock**: Used to create mock objects.
* **@InjectMocks**: Used to automatically inject the mocks into the object under test.
* **@Spy**: Used to create a partial mock, where real methods are called but some are stubbed.
* **@Captor**: Used to create argument captors for verifying arguments passed to mock methods.
* **@RunWith(MockitoJUnitRunner.class)**: In JUnit 4, this runner initializes the mocks and handles annotations.

### **Basic Example in JUnit 5 with Mockito**

Here’s a simple example to demonstrate how Mockito works in unit testing:

#### Example: Testing a Service that Depends on a Repository

Let's say we have the following service and repository classes:

```java
// A simple service that depends on a repository
public class UserService {
    private UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public boolean userExists(String username) {
        return userRepository.findByUsername(username) != null;
    }
}

// A simple repository interface
public interface UserRepository {
    User findByUsername(String username);
}
```

Now, we want to test the `userExists` method without relying on the actual `UserRepository`.

#### Step 1: Create Mocks for Dependencies

We can mock the `UserRepository` interface using Mockito:

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;

import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

public class UserServiceTest {

    @Mock
    private UserRepository userRepository;  // Mock the UserRepository

    private UserService userService;

    @BeforeEach
    public void setUp() {
        MockitoAnnotations.openMocks(this);  // Initialize the mocks
        userService = new UserService(userRepository);  // Inject the mock into the service
    }

    @Test
    public void testUserExists() {
        // Arrange: Stub the behavior of the mock
        User mockUser = new User("testuser");
        when(userRepository.findByUsername("testuser")).thenReturn(mockUser);

        // Act: Call the method under test
        boolean exists = userService.userExists("testuser");

        // Assert: Verify the result
        assertTrue(exists);

        // Verify that the method on the mock was called once
        verify(userRepository, times(1)).findByUsername("testuser");
    }

    @Test
    public void testUserDoesNotExist() {
        // Arrange: Stub the behavior of the mock
        when(userRepository.findByUsername("nonexistent")).thenReturn(null);

        // Act: Call the method under test
        boolean exists = userService.userExists("nonexistent");

        // Assert: Verify the result
        assertFalse(exists);
    }
}
```

### **Explanation of the Example**:

1. **Mocking**:

    * `@Mock` is used to create a mock `UserRepository` object.
    * `MockitoAnnotations.openMocks(this)` initializes the mock objects and injects them into the test class.

2. **Stubbing**:

    * In the `testUserExists` test method, `when(userRepository.findByUsername("testuser")).thenReturn(mockUser)` stubs the behavior of the mock to return a `User` object when the `findByUsername` method is called.

3. **Verification**:

    * `verify(userRepository, times(1)).findByUsername("testuser")` verifies that the `findByUsername` method was called exactly once with the argument `"testuser"`.

4. **Assertions**:

    * We use assertions (`assertTrue()` and `assertFalse()`) to verify the result returned by the `userExists` method.

### **Common Mockito Methods**

1. **`when()`**: Used to stub a method call to return a specific value.

   ```java
   when(mockObject.method()).thenReturn(value);
   ```

2. **`verify()`**: Used to verify that a method was called on a mock object.

   ```java
   verify(mockObject).method();
   ```

3. **`times()`**: Used to specify the number of times a method is expected to be called.

   ```java
   verify(mockObject, times(1)).method();
   ```

4. **`any()`**: Used to match any argument of a specific type.

   ```java
   when(mockObject.method(any(String.class))).thenReturn(value);
   ```

5. **`doThrow()`**: Used for stubbing methods that will throw an exception.

   ```java
   doThrow(new RuntimeException()).when(mockObject).method();
   ```

6. **`reset()`**: Resets the behavior of a mock, clearing its interactions and stubbing.

   ```java
   reset(mockObject);
   ```

---

### **Mockito with JUnit 5**

Mockito works well with JUnit 5, and you can use annotations such as `@Mock`, `@InjectMocks`, and `@ExtendWith(MockitoExtension.class)` for seamless integration.

#### Example with `@ExtendWith` in JUnit 5:

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

@ExtendWith(MockitoExtension.class)  // Initialize mocks automatically in JUnit 5
public class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;

    @Test
    public void testUserExists() {
        User mockUser = new User("testuser");
        when(userRepository.findByUsername("testuser")).thenReturn(mockUser);

        boolean exists = userService.userExists("testuser");

        assertTrue(exists);
        verify(userRepository).findByUsername("testuser");
    }
}
```

Here, `@ExtendWith(MockitoExtension.class)` is used to automatically initialize mocks and inject them into the `UserService` class.

---

### **Summary of Key Features**

* **Mocking**: Create mock objects to simulate real objects.
* **Stubbing**: Control what methods on mocks return.
* **Verification**: Verify that certain methods were called on mock objects.
* **Spying**: Partial mocking, allowing you to call real methods on an object and mock some methods.
* **JUnit 5 Integration**: Mockito works seamlessly with JUnit 5 using `@ExtendWith` and other annotations.

Mockito makes unit testing easier by allowing you to focus on testing business logic rather than dealing with complex dependencies or external systems.

---

## 22. Why do we use mocking in unit tests?

Mocking in unit tests is a powerful technique used to isolate the component being tested by replacing its dependencies with mock objects. Mocking helps ensure that unit tests are focused on the logic of the unit itself, rather than being influenced by external systems or complex interactions. Here's why mocking is so important and commonly used in unit testing:

### **1. Isolation of the Unit Under Test**

In unit testing, the goal is to test only the behavior of the unit you're focusing on, such as a method or a class, and not the behavior of its external dependencies (e.g., database, file system, web services). If these dependencies are real (i.e., if the unit tests rely on actual database queries or network calls), the tests can become:

* **Slow**: Interactions with external systems can be time-consuming.
* **Unreliable**: External systems may change, become unavailable, or introduce variability, leading to flaky tests.
* **Hard to control**: It becomes difficult to test specific edge cases, especially if the real system is complex or unpredictable.

By using **mocking**, you replace these external dependencies with **mock objects** that simulate their behavior in a controlled way. This allows you to focus solely on testing the logic of the unit.

### **2. Control over Behavior and Responses**

When you use mocks, you can define the behavior of external dependencies in a precise manner. This is especially useful when you need to test specific scenarios, such as:

* **Simulating errors**: You can make a mock object throw exceptions, allowing you to test how your code handles error scenarios without needing the real service or system to fail.
* **Testing different return values**: You can specify that a mock method returns certain values depending on the inputs, which helps in testing various edge cases or conditions.

For example, if you're testing a service that makes a call to a database, you can mock the database to return predefined data, allowing you to test how your service handles that data without needing to connect to an actual database.

### **3. Speed and Efficiency**

Real dependencies often involve operations that take time, such as network calls, disk I/O, or database operations. These can slow down your tests significantly. By using mocks, you eliminate the need to rely on external resources, making your tests run much faster.

For example:

* Mocking a network call to a REST API might take milliseconds to return a predefined response, whereas making an actual network request could take seconds or even fail due to network issues.

By mocking, unit tests can execute quickly and repeatedly without worrying about performance or availability of external systems.

### **4. Deterministic Testing**

Mocks provide **deterministic behavior**, meaning that the behavior of mock objects is predictable and controlled. This allows for more **consistent** test results. Real dependencies may change over time, introducing unpredictability in test results (e.g., database content might change, an API might change its response).

For example:

* A mock object always returns the same value for a method call, ensuring that the test result is consistent every time the test runs.

This helps avoid **flaky tests**, where tests might pass or fail randomly due to external factors.

### **5. Simplifying Complex Dependencies**

In many applications, classes and methods interact with a number of other components. For example, a service class might depend on several other services, databases, or web APIs. Without mocking, it would be difficult to isolate the specific behavior of the service you're testing because the test would also involve the behavior of all its dependencies.

Mocking allows you to **mock only the dependencies** that are needed for a particular test. This keeps the test simple and focused. You can simulate different behaviors for each mock and test how the service responds to various conditions, without needing to set up complex real-world scenarios.

For example:

* If you're testing a service that depends on a payment gateway, you can mock the payment gateway, so your test focuses on how the service processes the payment rather than testing the actual payment gateway.

### **6. Testing Edge Cases**

Mocks allow you to easily simulate **edge cases** or rare conditions that might be hard to reproduce using real objects. These include situations like:

* A database being down.
* A network failure when making an API request.
* A file being missing or corrupted.

By using mocks, you can simulate these scenarios by making the mock object throw exceptions or return unusual values. This makes it much easier to test your code's behavior under these conditions.

### **7. Verifying Interactions**

Mocking frameworks like **Mockito** also allow you to **verify** that certain interactions with the mock objects occurred as expected. For instance, you can verify whether a method was called, how many times it was called, and with which arguments.

This is particularly useful for testing if certain actions, such as saving data to a database or making a network call, are triggered in the expected way.

For example:

```java
verify(mockService, times(1)).processPayment(any());
```

This verifies that the `processPayment()` method on the `mockService` was called exactly once.

### **8. Avoiding Side Effects**

Using real dependencies in unit tests can cause **side effects**. For example, making a test call to a real database could modify test data, and running tests with a real web API could result in the creation of unwanted records.

Mocks prevent these side effects by isolating the code under test and preventing changes to external systems or shared states.

### **Examples of Dependencies That Are Commonly Mocked:**

1. **Databases**: When testing a class that interacts with a database, you can mock the database calls to avoid needing a real database connection.
2. **Web Services/REST APIs**: When testing services that make HTTP requests, you can mock the response from the API to simulate different scenarios.
3. **File Systems**: For testing classes that interact with files or directories, you can mock the file I/O operations.
4. **Third-party Services**: Any external service (e.g., payment gateways, messaging services, etc.) can be mocked to avoid actual communication with external systems.

---

### **Summary**

Mocking is used in unit testing for several key reasons:

* **Isolation**: It isolates the unit under test from its dependencies.
* **Control**: Mocks allow precise control over the behavior of dependencies.
* **Speed**: Tests are faster without real dependencies.
* **Deterministic Results**: Mocks provide predictable and consistent behavior.
* **Edge Case Testing**: Mocks can simulate rare or exceptional conditions easily.
* **Interaction Verification**: You can verify the expected interactions with dependencies.

By using mocking, we ensure that our unit tests are focused, fast, and reliable, providing clear insights into the behavior of the code being tested.

---

## 23. How do you mock a class using Mockito?

To **mock a class** using **Mockito**, you can use the `Mockito.mock()` method or the `@Mock` annotation. Here's a breakdown of both approaches, followed by a detailed example.

### **1. Using `Mockito.mock()`**

The `Mockito.mock()` method creates a mock of a given class or interface. This method is useful for simple mocking when you don't need to rely on annotations.

#### **Syntax**:

```java
SomeClass mockObject = Mockito.mock(SomeClass.class);
```

### **2. Using `@Mock` Annotation**

The `@Mock` annotation is a more convenient way to create mocks in combination with `@ExtendWith(MockitoExtension.class)` in JUnit 5 or `@RunWith(MockitoJUnitRunner.class)` in JUnit 4.

#### **Syntax**:

```java
@Mock
SomeClass mockObject;
```

You need to initialize the mock objects with `MockitoAnnotations.openMocks(this)` or use a test runner/extension to make it work.

---

### **Detailed Example: Mocking a Class Using Mockito**

Let’s say we have the following class structure:

```java
// Service class we want to test
public class UserService {
    private UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User getUserByUsername(String username) {
        return userRepository.findByUsername(username);
    }
}

// Repository class (dependency we want to mock)
public class UserRepository {
    public User findByUsername(String username) {
        // Imagine this is a real database call
        return null;
    }
}

// User class
public class User {
    private String username;

    public User(String username) {
        this.username = username;
    }

    public String getUsername() {
        return username;
    }
}
```

In this example, the `UserService` class depends on the `UserRepository` class, and we want to test the `UserService` class without needing a real `UserRepository`. We'll mock `UserRepository` using Mockito.

---

### **Mocking with `Mockito.mock()`**

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

public class UserServiceTest {

    private UserRepository userRepositoryMock;  // Create the mock
    private UserService userService;

    @BeforeEach
    public void setUp() {
        // Create the mock object for UserRepository
        userRepositoryMock = Mockito.mock(UserRepository.class);

        // Inject the mock object into UserService
        userService = new UserService(userRepositoryMock);
    }

    @Test
    public void testGetUserByUsername() {
        // Arrange: Stub the behavior of the mock object
        User mockUser = new User("testuser");
        when(userRepositoryMock.findByUsername("testuser")).thenReturn(mockUser);

        // Act: Call the method under test
        User user = userService.getUserByUsername("testuser");

        // Assert: Verify the result
        assertNotNull(user);
        assertEquals("testuser", user.getUsername());
    }
}
```

### **Explanation of the Example**:

1. **Creating the mock**:

    * `userRepositoryMock = Mockito.mock(UserRepository.class);` creates a mock of the `UserRepository` class. This mock will simulate the behavior of the real `UserRepository`.

2. **Stubbing the mock**:

    * `when(userRepositoryMock.findByUsername("testuser")).thenReturn(mockUser);` tells Mockito to return a specific `User` object when the `findByUsername()` method is called with the argument `"testuser"`.

3. **Testing the `UserService`**:

    * `userService.getUserByUsername("testuser")` calls the method under test.

4. **Assertions**:

    * We use `assertNotNull(user)` to check that the returned user is not null.
    * We use `assertEquals("testuser", user.getUsername())` to verify that the returned user’s username matches the expected value.

5. **Verification (optional)**:

    * If you want to verify that a certain method on the mock was called, you can use `verify()`:

   ```java
   verify(userRepositoryMock).findByUsername("testuser");
   ```

---

### **Mocking with `@Mock` Annotation (JUnit 5)**

If you're using JUnit 5, you can use the `@Mock` annotation along with the `@ExtendWith(MockitoExtension.class)` extension to create and inject mocks automatically.

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

@ExtendWith(MockitoExtension.class)  // Mockito extension for JUnit 5
public class UserServiceTest {

    @Mock
    private UserRepository userRepositoryMock;  // Mock the UserRepository

    @InjectMocks
    private UserService userService;  // Inject the mock into UserService

    @Test
    public void testGetUserByUsername() {
        // Arrange: Stub the behavior of the mock object
        User mockUser = new User("testuser");
        when(userRepositoryMock.findByUsername("testuser")).thenReturn(mockUser);

        // Act: Call the method under test
        User user = userService.getUserByUsername("testuser");

        // Assert: Verify the result
        assertNotNull(user);
        assertEquals("testuser", user.getUsername());
    }
}
```

### **Explanation of the `@Mock` and `@InjectMocks` Annotations**:

* **`@Mock`**: The `@Mock` annotation is used to automatically create a mock object for `UserRepository`.
* **`@InjectMocks`**: The `@InjectMocks` annotation tells Mockito to inject the mocked dependencies into the `UserService` instance. Mockito automatically calls the constructor and injects the mock.

---

### **Additional Mockito Methods for Mocking**

1. **`when()`**: Defines what the mocked method will return.

   ```java
   when(mockObject.method()).thenReturn(returnValue);
   ```

2. **`doReturn()`**: Similar to `when()`, but can be used for methods that do not return a value or are final methods.

   ```java
   doReturn(returnValue).when(mockObject).method();
   ```

3. **`verify()`**: Used to verify that a method was called on the mock object.

   ```java
   verify(mockObject).method();
   ```

4. **`reset()`**: Resets the behavior of a mock object.

   ```java
   reset(mockObject);
   ```

---

### **Summary**

Mocking is a critical technique in unit testing, and Mockito provides powerful and easy-to-use methods for mocking both interfaces and classes. Here are the key steps:

* **`Mockito.mock(Class.class)`**: For creating mock objects of classes or interfaces.
* **`@Mock` and `@InjectMocks` annotations**: For simplifying the creation and injection of mocks in JUnit 5.
* **Stubbing**: Define the behavior of mocks using `when().thenReturn()`.
* **Verification**: Use `verify()` to ensure certain methods are called.

This helps isolate the unit being tested and control its behavior, making unit tests more focused and reliable.

---

## 24. What is the difference between `@Mock` and `@InjectMocks`?

The annotations `@Mock` and `@InjectMocks` are commonly used in **Mockito** for creating and injecting mock objects in unit tests. Here's the key difference between the two:

### **1. `@Mock` Annotation**

* **Purpose**: The `@Mock` annotation is used to create mock objects of **dependencies** that are used by the class you're testing.
* **What It Does**: It automatically creates a mock version of the class or interface you specify and allows you to control its behavior during testing.
* **Usage**: You apply `@Mock` to the dependencies of the class under test.

#### Example:

```java
@Mock
private UserRepository userRepositoryMock;  // Mocks the UserRepository
```

In this example, `userRepositoryMock` is a mock object of the `UserRepository` class. You can then define behavior for this mock using Mockito’s `when()` method.

---

### **2. `@InjectMocks` Annotation**

* **Purpose**: The `@InjectMocks` annotation is used to **automatically inject the mock objects** (created using `@Mock`) into the **class under test**.
* **What It Does**: It creates an instance of the class under test and injects the mock objects into its constructor or fields (depending on how the class is constructed).
* **Usage**: You apply `@InjectMocks` to the class you're testing.

#### Example:

```java
@InjectMocks
private UserService userService;  // Injects the mock objects into this class
```

In this example, `userService` is the class you're testing, and the mock object (`userRepositoryMock`) will be injected into the `UserService` instance. Mockito uses the mock dependency to construct the `UserService` during the test setup.

---

### **How They Work Together**

These annotations are used in combination to create **mock dependencies** and inject them into the class under test.

* `@Mock`: Creates mock versions of the dependencies of the class you're testing.
* `@InjectMocks`: Automatically injects the mocked dependencies into the class under test.

### **Example of Both in Action**

```java
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

@ExtendWith(MockitoExtension.class)
public class UserServiceTest {

    @Mock
    private UserRepository userRepositoryMock;  // Mock UserRepository

    @InjectMocks
    private UserService userService;  // Inject mocks into UserService

    @Test
    public void testGetUserByUsername() {
        // Arrange: Stub the behavior of the mock object
        User mockUser = new User("testuser");
        when(userRepositoryMock.findByUsername("testuser")).thenReturn(mockUser);

        // Act: Call the method under test
        User user = userService.getUserByUsername("testuser");

        // Assert: Verify the result
        assertNotNull(user);
        assertEquals("testuser", user.getUsername());
    }
}
```

### **In this example**:

* **`@Mock`** creates a mock object of the `UserRepository` class.
* **`@InjectMocks`** creates an instance of `UserService` and automatically injects the mocked `userRepositoryMock` into the `userService` instance.

### **Summary of Differences**

| **Annotation**     | **Purpose**                                                                  | **What it Creates**                                                |
| ------------------ | ---------------------------------------------------------------------------- | ------------------------------------------------------------------ |
| **`@Mock`**        | Creates mock objects for dependencies that are used by the class under test. | Mock object of the specified class or interface.                   |
| **`@InjectMocks`** | Injects the mock objects (created with `@Mock`) into the class under test.   | An instance of the class being tested, with dependencies injected. |

By using `@Mock` and `@InjectMocks` together, you can easily create mock objects for the dependencies of a class and inject them into the class being tested, allowing for focused and isolated unit tests.

---

## 25. How does `@Spy` differ from `@Mock`?

The `@Spy` and `@Mock` annotations in **Mockito** are both used to create mock objects, but they serve different purposes and have distinct behavior.

Here’s a detailed explanation of how they differ:

### **1. `@Mock` Annotation**

* **Purpose**: The `@Mock` annotation is used to create **mock objects**. A mock object is a completely simulated version of the real object.
* **Behavior**:

    * By default, mock objects do **nothing**. They return default values (like `null`, `0`, or `false`) unless explicitly told to do otherwise using `when()` and `thenReturn()`.
    * It allows you to **stub** behavior for methods (i.e., define the return value or exception).
* **Typical Use Case**: Used when you want to isolate the class under test from all of its dependencies and when you don’t need any real behavior from the dependencies (i.e., all behaviors are controlled by stubbing).

#### Example:

```java
@Mock
private List<String> mockedList; // Creates a mock List

@Test
void testMock() {
    when(mockedList.size()).thenReturn(10); // Stub the method to return 10
    System.out.println(mockedList.size()); // Prints 10
}
```

In this example, the mock object of `List<String>` will return `10` for the `size()` method. If we didn't stub it, it would return the default value (which is `0` for `size()` on a list).

### **2. `@Spy` Annotation**

* **Purpose**: The `@Spy` annotation is used to **partially mock** real objects. A spy allows you to mock only specific methods of an existing real object, while leaving others to behave as they would in the real implementation.
* **Behavior**:

    * A spy creates a real instance of the object, and you can selectively mock some methods. The methods that are not stubbed will behave as normal.
    * Unlike a mock, which always returns default values, a spy **calls the real methods** unless explicitly told to stub a particular method using `doReturn()`, `when()`, etc.
* **Typical Use Case**: Used when you need to mock a real object but still want some of its methods to behave as normal, allowing for partial control over its behavior.

#### Example:

```java
@Spy
private List<String> spyList = new ArrayList<>(); // Creates a spy of a real List

@Test
void testSpy() {
    spyList.add("Hello"); // Adds a real item to the list
    doReturn(10).when(spyList).size(); // Mock the size method to return 10
    System.out.println(spyList.size()); // Prints 10 (stubbed size)
    spyList.add("World");
    System.out.println(spyList); // Prints [Hello, World] (real add method)
}
```

In this example, the `spyList` is a **real `ArrayList`**. We mock the `size()` method to return `10`, but the real `add()` method works normally.

### **Key Differences Between `@Mock` and `@Spy`**

| **Feature**          | **`@Mock`**                                                                    | **`@Spy`**                                                                      |
| -------------------- | ------------------------------------------------------------------------------ | ------------------------------------------------------------------------------- |
| **Object Creation**  | Creates a **completely mock object** (no real behavior).                       | Creates a **real object** and allows selective stubbing of methods.             |
| **Default Behavior** | Methods return **default values** (e.g., `null`, `0`, `false`) unless stubbed. | Methods call **real implementations** unless explicitly stubbed.                |
| **Use Case**         | Used when you want to isolate the class under test from all dependencies.      | Used when you want to use a real object, but selectively mock specific methods. |
| **Mocking Behavior** | All methods need to be explicitly stubbed.                                     | Real methods are used by default unless explicitly stubbed.                     |
| **Example Usage**    | `List<String> mockList = Mockito.mock(List.class);`                            | `List<String> spyList = Mockito.spy(new ArrayList<>());`                        |

### **When to Use `@Mock` vs `@Spy`?**

* **Use `@Mock`**: When you want to completely mock an object and control all its behavior (i.e., you don't want the real implementation to be involved in the test).
* **Use `@Spy`**: When you want to use the real object but need to override or mock certain methods to control specific behaviors while leaving the rest of the object’s behavior intact.

---

### **Important Considerations**

* **Partial Mocking**: `@Spy` is useful for partial mocking, whereas `@Mock` cannot be used for partial mocking since mock objects don't invoke real methods by default.

* **Spying on Real Objects**: Be cautious when using `@Spy` on real objects because sometimes it can lead to unexpected behavior if you mistakenly forget to stub a method. It's generally safer to mock everything unless you specifically need the real behavior.

* **Calling Real Methods**: If you spy on a real object (using `@Spy`), you need to be cautious about calling real methods during the test, as the real behavior can interfere with your test's expectations. Always remember to stub the methods you want to mock.

---

### **Example Comparison: Mock vs Spy**

#### **Mocking with `@Mock`**:

```java
@Mock
private List<String> mockList;

@Test
void testMockBehavior() {
    when(mockList.size()).thenReturn(5);
    assertEquals(5, mockList.size());  // Mock returns 5
}
```

#### **Spying with `@Spy`**:

```java
@Spy
private List<String> spyList = new ArrayList<>();

@Test
void testSpyBehavior() {
    spyList.add("Hello");
    doReturn(5).when(spyList).size();  // Stubbing size method
    assertEquals(5, spyList.size());  // Spy returns mocked value for size
    assertEquals(1, spyList.size());  // Real behavior for add() method
}
```

---

### **Summary**

* **`@Mock`**: Creates a mock object with no real behavior, and you need to explicitly define how it should behave (stub the methods).
* **`@Spy`**: Creates a real object and allows you to selectively mock methods, keeping the real behavior for others.

In essence:

* **`@Mock`** is for complete isolation from the real object.
* **`@Spy`** is for using a real object with some methods controlled via stubbing.

---

## 26. What is stubbing in Mockito?

**Stubbing** in **Mockito** refers to the practice of specifying the behavior of mock objects when certain methods are called. This is done by defining **what the mocked methods should return** when invoked with specific arguments. Essentially, stubbing allows you to control the behavior of mock objects to return predefined values or perform certain actions during testing, without needing to rely on the actual implementation.

### **Key Concept of Stubbing**

* **Stubbing** is used to define what a **mocked method** should return when it is called with specific arguments.
* In Mockito, stubbing is done using the `when(...).thenReturn(...)` syntax.

### **How to Stub Methods in Mockito**

When using **Mockito**, you typically stub a method on a mock object to control its behavior during a test.

#### **Stubbing Syntax**

```java
when(mockObject.method(arg1, arg2)).thenReturn(value);
```

Here:

* `mockObject`: The mock object whose method is being stubbed.
* `method(arg1, arg2)`: The method you want to stub.
* `thenReturn(value)`: The value you want to return when the method is called with the specified arguments.

### **Example: Stubbing with Mockito**

Imagine you have a service class `CalculatorService` that depends on a `Calculator` class. You want to write a test where you mock the `Calculator` to control its behavior.

#### **Class under test (CalculatorService)**:

```java
public class CalculatorService {
    private Calculator calculator;

    public CalculatorService(Calculator calculator) {
        this.calculator = calculator;
    }

    public int add(int a, int b) {
        return calculator.add(a, b);  // Calling the method on the mock object
    }
}
```

#### **Dependency class (Calculator)**:

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;  // Actual implementation
    }
}
```

#### **Test class using Mockito with Stubbing**:

```java
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

public class CalculatorServiceTest {

    private Calculator calculatorMock;
    private CalculatorService calculatorService;

    @BeforeEach
    public void setUp() {
        // Create a mock object of the Calculator class
        calculatorMock = mock(Calculator.class);
        
        // Inject the mock into the CalculatorService
        calculatorService = new CalculatorService(calculatorMock);
    }

    @Test
    public void testAdd() {
        // Stubbing the behavior of the mock
        when(calculatorMock.add(3, 5)).thenReturn(8);
        
        // Call the method under test
        int result = calculatorService.add(3, 5);
        
        // Verify the result
        assertEquals(8, result);
        
        // Verify that the add method on the mock was called with specific arguments
        verify(calculatorMock).add(3, 5);
    }
}
```

### **Explanation of the Test**:

1. **Creating the Mock**:

    * `calculatorMock = mock(Calculator.class);` creates a mock object of `Calculator`.
2. **Stubbing the `add()` Method**:

    * `when(calculatorMock.add(3, 5)).thenReturn(8);` stubs the `add()` method of the mock `Calculator` object. When `add(3, 5)` is called, the mock will return `8`.
3. **Calling the Method Under Test**:

    * `calculatorService.add(3, 5)` calls the method of the `CalculatorService` class, which internally calls the mocked `Calculator` object.
4. **Assertions**:

    * `assertEquals(8, result);` checks that the result of `add(3, 5)` is `8`, which was the stubbed value.
5. **Verifying Method Calls**:

    * `verify(calculatorMock).add(3, 5);` checks that the `add()` method on the mock object was indeed called with the specified arguments.

### **Common Scenarios for Stubbing**

1. **Return Values**:

    * Return specific values when a method is called:

      ```java
      when(mockObject.someMethod()).thenReturn(someValue);
      ```

2. **Throwing Exceptions**:

    * You can stub a method to throw an exception when called:

      ```java
      when(mockObject.someMethod()).thenThrow(new RuntimeException("Error occurred"));
      ```

3. **Multiple Returns**:

    * You can specify that the mocked method returns different values on consecutive calls:

      ```java
      when(mockObject.someMethod()).thenReturn(value1).thenReturn(value2);
      ```

4. **Stubbing Void Methods**:

    * For methods that return `void`, you can use `doNothing()`, `doThrow()`, etc.:

      ```java
      doNothing().when(mockObject).someVoidMethod();
      ```

### **Advanced Stubbing Examples**

#### **Stubbing for Multiple Consecutive Calls**:

```java
when(mockObject.someMethod())
    .thenReturn(value1)  // First call will return value1
    .thenReturn(value2)  // Second call will return value2
    .thenReturn(value3); // Third call will return value3
```

#### **Stubbing Void Methods**:

For methods that don't return a value (`void` methods), you need to use the `do...when` syntax:

```java
doNothing().when(mockObject).voidMethod();
doThrow(new RuntimeException()).when(mockObject).voidMethod();
```

#### **Stubbing with Argument Matching**:

You can use argument matchers like `any()` or `eq()` to match arguments dynamically.

```java
when(mockObject.someMethod(anyInt())).thenReturn(value);
```

This would make the `someMethod()` return `value` for any integer passed as an argument.

### **Conclusion**

* **Stubbing** in Mockito is the process of defining the behavior of a mock object, specifying what it should return when specific methods are called with certain arguments.
* It's done using the `when(...).thenReturn(...)` syntax, where you specify the method and the return value.
* Stubbing allows you to isolate your unit tests from real dependencies, making it possible to simulate and control the behavior of those dependencies during testing.

Stubbing is a powerful feature that makes unit tests more predictable and manageable, allowing you to test a class in isolation from the behavior of its dependencies.

---

## 27. How do you verify method calls in Mockito?

In **Mockito**, you can verify if certain methods were called on a mock object and how many times they were called. This is helpful for ensuring that your code interacts with its dependencies as expected during the test.

Mockito provides the `verify()` method to verify that the mocked methods are called with specific arguments and to check the number of times those methods were invoked.

### **Basic Syntax for Verifying Method Calls**

The basic syntax for verifying a method call is as follows:

```java
verify(mockObject).methodCall(arguments);
```

Where:

* `mockObject` is the mock object you're verifying.
* `methodCall(arguments)` specifies the method you want to verify and the arguments it was called with.

### **Key Use Cases for Verifying Method Calls**

1. **Verify that a method was called exactly once**.
2. **Verify that a method was called with specific arguments**.
3. **Verify that a method was called a certain number of times**.
4. **Verify that a method was never called**.

---

### **1. Verify that a method was called**

To verify that a method was called **at least once** with specific arguments:

```java
verify(mockObject).methodName(arg1, arg2);
```

#### Example:

```java
@Test
void testVerifyMethodCall() {
    // Arrange
    Calculator calculator = mock(Calculator.class);

    // Act
    calculator.add(3, 5);

    // Assert
    verify(calculator).add(3, 5);  // Verify that add(3, 5) was called
}
```

In this example, the `add(3, 5)` method on the mock `Calculator` object is verified to be called.

---

### **2. Verify the Number of Method Calls**

You can also verify how many times a method was called using the `times()` method.

#### Syntax:

```java
verify(mockObject, times(numberOfCalls)).methodCall(arguments);
```

* `times(numberOfCalls)` checks if the method was called exactly that many times.

#### Example:

```java
@Test
void testVerifyNumberOfCalls() {
    // Arrange
    Calculator calculator = mock(Calculator.class);

    // Act
    calculator.add(3, 5);
    calculator.add(3, 5);
    calculator.add(3, 5);

    // Assert
    verify(calculator, times(3)).add(3, 5);  // Verify that add(3, 5) was called 3 times
}
```

In this case, the `add(3, 5)` method is called 3 times, and the `verify()` method ensures that the call count matches the expectation.

---

### **3. Verify that a method was called at most once**

You can use `verify()` with `times(1)` to check if a method was called **exactly once**:

#### Example:

```java
@Test
void testVerifyMethodCalledOnce() {
    // Arrange
    Calculator calculator = mock(Calculator.class);

    // Act
    calculator.add(3, 5);

    // Assert
    verify(calculator, times(1)).add(3, 5);  // Verify that add(3, 5) was called exactly once
}
```

---

### **4. Verify that a method was never called**

You can verify that a method was **never** called on the mock object using `times(0)`:

#### Example:

```java
@Test
void testVerifyMethodNeverCalled() {
    // Arrange
    Calculator calculator = mock(Calculator.class);

    // Act
    // No method call is made to calculator

    // Assert
    verify(calculator, times(0)).add(3, 5);  // Verify that add(3, 5) was never called
}
```

In this case, since no method is called, `verify()` checks that `add(3, 5)` was never invoked.

---

### **5. Verify method call order using `InOrder`**

You can also verify the order in which methods were called on mocks by using **`InOrder`**.

#### Example:

```java
@Test
void testVerifyMethodCallOrder() {
    // Arrange
    Calculator calculator = mock(Calculator.class);
    CalculatorService service = new CalculatorService(calculator);

    // Act
    service.add(3, 5);
    service.subtract(10, 5);

    // Create InOrder verifier
    InOrder inOrder = inOrder(calculator);

    // Assert that the methods were called in the specified order
    inOrder.verify(calculator).add(3, 5);
    inOrder.verify(calculator).subtract(10, 5);
}
```

In this example, `inOrder.verify()` ensures that `add(3, 5)` was called first and `subtract(10, 5)` was called afterward.

---

### **6. Verify method call with Argument Matchers**

You can also verify method calls with argument matchers like `any()`, `eq()`, `isNull()`, etc.

#### Example:

```java
@Test
void testVerifyMethodCallWithMatchers() {
    // Arrange
    Calculator calculator = mock(Calculator.class);

    // Act
    calculator.add(3, 5);
    calculator.add(10, 20);

    // Assert
    verify(calculator).add(eq(3), eq(5));  // Verify that add was called with specific arguments
    verify(calculator).add(anyInt(), anyInt());  // Verify that add was called with any integers
}
```

Here, `eq(3)` ensures that `3` was passed as the first argument, and `anyInt()` allows any integer as the second argument.

---

### **7. Verifying a method was called a specific number of times (other than 1)**

You can verify that a method is called a specific number of times using the `times()` method.

#### Example:

```java
@Test
void testVerifyMultipleCalls() {
    // Arrange
    List<String> mockList = mock(List.class);

    // Act
    mockList.add("one");
    mockList.add("two");
    mockList.add("three");

    // Assert
    verify(mockList, times(3)).add(anyString());  // Verify that add() was called 3 times
}
```

---

### **Summary of Common `verify()` Methods**

| **Verification Type**                               | **Usage**                                                                                        |
| --------------------------------------------------- | ------------------------------------------------------------------------------------------------ |
| **Verify method called once**                       | `verify(mockObject).methodCall(arguments);`                                                      |
| **Verify method called a specific number of times** | `verify(mockObject, times(n)).methodCall(arguments);` (e.g., `times(2)`)                         |
| **Verify method was never called**                  | `verify(mockObject, times(0)).methodCall(arguments);`                                            |
| **Verify call order**                               | `InOrder inOrder = inOrder(mockObject);` and `inOrder.verify(mockObject).methodCall(arguments);` |
| **Verify method called with argument matchers**     | `verify(mockObject).methodCall(anyString());` or `eq()`, `any()`, etc.                           |

---

### **Conclusion**

* **`verify()`** in Mockito allows you to check whether methods on mock objects were called during the test and ensures that your code interacts with the mock objects as expected.
* You can verify the number of times methods were called, the arguments passed, and even the order of calls.
* It is an essential tool for **behavior-driven testing**, ensuring your mock objects are used correctly in unit tests.

---

## 28. What is `when().thenReturn()` used for?

In **Mockito**, the `when().thenReturn()` syntax is used for **stubbing** methods on mock objects. It allows you to define **what a mocked method should return** when it is called with specific arguments.

### **Purpose of `when().thenReturn()`**

* **`when()`**: This method is used to specify the **method call** on the mock object that you want to **stub**.
* **`thenReturn()`**: This method specifies the **return value** for the method when it is called with the specified arguments.

In essence, `when().thenReturn()` is used to **define the behavior** of mocked methods so that you can control what values the mock object will return during the test, instead of relying on the actual implementation.

---

### **Syntax**

```java
when(mockObject.methodCall(arguments)).thenReturn(returnValue);
```

Where:

* **`mockObject`**: The mock object you created using `Mockito.mock()` or `@Mock`.
* **`methodCall(arguments)`**: The method on the mock object that you want to stub, along with the arguments you want to check.
* **`thenReturn(returnValue)`**: Specifies the value to return when the method is called with the given arguments.

---

### **Example**

Let's say we have a `Calculator` class with an `add` method, and we want to mock this method in a test to return a specific value instead of performing the actual addition.

#### **Calculator Class** (Real Class):

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

#### **Test with `when().thenReturn()`**:

```java
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

public class CalculatorTest {

    private Calculator calculatorMock;

    @BeforeEach
    public void setUp() {
        // Create a mock of the Calculator class
        calculatorMock = mock(Calculator.class);
    }

    @Test
    public void testAddMethod() {
        // Stub the 'add' method to return 10 when called with arguments 5 and 5
        when(calculatorMock.add(5, 5)).thenReturn(10);

        // Call the method under test
        int result = calculatorMock.add(5, 5);

        // Assert that the result is what we mocked (10)
        assertEquals(10, result);
    }
}
```

### **Explanation:**

1. **Mock Creation**: `calculatorMock = mock(Calculator.class);` creates a mock object of the `Calculator` class.
2. **Stubbing the Method**: `when(calculatorMock.add(5, 5)).thenReturn(10);` defines that when the `add` method is called with `5` and `5`, it should return `10` (instead of performing the real addition).
3. **Method Call**: `int result = calculatorMock.add(5, 5);` calls the mocked `add` method.
4. **Assertion**: `assertEquals(10, result);` checks that the result is the mocked value (`10`).

### **How `when().thenReturn()` Works**

* The **`when()`** part specifies the method that you want to stub (in this case, `calculatorMock.add(5, 5)`).
* The **`thenReturn()`** part tells Mockito to **return a specific value** (in this case, `10`) when the specified method is called with the specified arguments.

---

### **Advanced Use Cases for `when().thenReturn()`**

1. **Stubbing Methods with Multiple Return Values**:

    * You can specify different return values for consecutive calls to the same method using `thenReturn()`:

   ```java
   when(calculatorMock.add(5, 5)).thenReturn(10).thenReturn(15);
   ```

   The first call will return `10`, and the second call will return `15`.

2. **Stubbing Methods to Throw Exceptions**:

    * You can use `thenThrow()` to make a method throw an exception instead of returning a value:

   ```java
   when(calculatorMock.add(5, 5)).thenThrow(new RuntimeException("Error"));
   ```

3. **Stubbing Void Methods**:

    * For methods that return `void`, use `doNothing()`, `doThrow()`, or `doAnswer()` for stubbing:

   ```java
   doNothing().when(calculatorMock).reset();
   doThrow(new RuntimeException()).when(calculatorMock).reset();
   ```

---

### **Summary**

* **`when().thenReturn()`** in Mockito is used to stub a mocked method. It defines what value the method should return when called with specific arguments.
* It helps control the behavior of mock objects in unit tests, allowing you to isolate the behavior of the class under test and ensure predictable results.
* You can also use `thenThrow()` to simulate exceptions and `thenAnswer()` for more complex behavior.

---

## 29. What is the use of `doReturn().when()`?

In **Mockito**, the **`doReturn().when()`** syntax is an alternative to **`when().thenReturn()`** for stubbing methods, particularly useful in certain situations where **`when().thenReturn()`** does not work, such as when stubbing **void methods** or when working with methods that are **final**, **static**, or **private**.

### **Difference Between `when().thenReturn()` and `doReturn().when()`**

* **`when().thenReturn()`** is commonly used for stubbing methods on mocks where you expect a **return value** from the method.
* **`doReturn().when()`** is used as a more **flexible approach** when stubbing methods, especially in scenarios where the **method has side effects** (like void methods), or when you want to stub **final**, **static**, or **private** methods that `when().thenReturn()` cannot handle directly.

In short, `doReturn().when()` is typically used in more **specialized cases**, while `when().thenReturn()` is the most common way to stub methods in Mockito.

---

### **Syntax of `doReturn().when()`**

```java
doReturn(returnValue).when(mockObject).methodCall(arguments);
```

Where:

* **`mockObject`**: The mock object you created using `Mockito.mock()` or `@Mock`.
* **`methodCall(arguments)`**: The method you want to stub and the arguments it is called with.
* **`returnValue`**: The value you want the mocked method to return when it is called.

---

### **Key Use Cases for `doReturn().when()`**

1. **Stubbing Void Methods**:
   If you have a mock object where the method you are stubbing is a **void method** (i.e., methods that do not return any value), using `doReturn().when()` is the recommended approach.

   ```java
   // Instead of using `when()`, use `doReturn()`
   doReturn(null).when(mockObject).voidMethod();
   ```

2. **Stubbing Methods That Cannot Be Stubbed Using `when().thenReturn()`**:
   Some methods, like **final**, **static**, or **private** methods, cannot be stubbed with `when().thenReturn()` directly. In these cases, `doReturn().when()` can be used as a workaround.

---

### **Example of `doReturn().when()` for Void Methods**

Suppose you have a `DatabaseService` class with a void method `updateRecord()`. Since the method doesn't return anything, you cannot use `when().thenReturn()`. Instead, you use `doReturn().when()` to mock it.

#### **DatabaseService Class** (Real Class):

```java
public class DatabaseService {
    public void updateRecord(String record) {
        // Some database logic to update a record
    }
}
```

#### **Test Using `doReturn().when()`**:

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

public class DatabaseServiceTest {

    private DatabaseService dbServiceMock;

    @BeforeEach
    public void setUp() {
        // Create a mock object for DatabaseService
        dbServiceMock = mock(DatabaseService.class);
    }

    @Test
    public void testUpdateRecord() {
        // Stub the void method updateRecord()
        doReturn(null).when(dbServiceMock).updateRecord("someRecord");

        // Call the method under test
        dbServiceMock.updateRecord("someRecord");

        // Verify that the method was called
        verify(dbServiceMock).updateRecord("someRecord");
    }
}
```

### **Explanation**:

1. **Mock Creation**: `dbServiceMock = mock(DatabaseService.class);` creates a mock object of `DatabaseService`.
2. **Stubbing Void Method**: `doReturn(null).when(dbServiceMock).updateRecord("someRecord");` stubs the void method `updateRecord` on the mock object.

    * Here, `doReturn(null)` indicates that the `updateRecord` method should return `null` (though void methods don't return anything, this syntax is just to fulfill the requirement for the call).
3. **Method Call**: `dbServiceMock.updateRecord("someRecord");` calls the method on the mock.
4. **Verification**: `verify(dbServiceMock).updateRecord("someRecord");` verifies that `updateRecord` was called with the expected argument.

---

### **Example of `doReturn().when()` for Final Methods**

In Mockito, you cannot directly mock **final methods** using `when().thenReturn()`. However, **`doReturn().when()`** allows you to mock final methods.

#### **Calculator Class** (with a Final Method):

```java
public class Calculator {
    public final int add(int a, int b) {
        return a + b;
    }
}
```

#### **Test Using `doReturn().when()`**:

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

public class CalculatorTest {

    private Calculator calculatorMock;

    @BeforeEach
    public void setUp() {
        // Create a mock object of the final Calculator class
        calculatorMock = mock(Calculator.class);
    }

    @Test
    public void testAddMethod() {
        // Stubbing the final method using doReturn().when()
        doReturn(10).when(calculatorMock).add(5, 5);

        // Call the method under test
        int result = calculatorMock.add(5, 5);

        // Assert the expected result
        assertEquals(10, result);
    }
}
```

### **Explanation**:

* **Stubbing Final Method**: `doReturn(10).when(calculatorMock).add(5, 5);` allows us to mock the final `add()` method to return `10` when called with the arguments `5` and `5`.
* **Method Call and Assertion**: We call `add(5, 5)` and assert that the result is `10`, as expected.

---

### **When to Use `doReturn().when()`**

* **Void Methods**: When stubbing void methods that don't return a value (e.g., methods that perform actions or have side effects).
* **Final Methods**: When stubbing final methods (methods in final classes or methods marked as `final`).
* **Private Methods**: When stubbing private methods (though Mockito also has `spy()` to handle this in some cases).
* **Static Methods**: Mockito doesn't directly support static method mocking, but `doReturn().when()` can sometimes work with static methods when using **Mockito with PowerMock** (PowerMock is an extension of Mockito).

---

### **Summary of `doReturn().when()` vs `when().thenReturn()`**

| **Feature**         | **`when().thenReturn()`**                                   | **`doReturn().when()`**                                                  |
| ------------------- | ----------------------------------------------------------- | ------------------------------------------------------------------------ |
| **Void Methods**    | Cannot be used with void methods directly.                  | Can be used for void methods.                                            |
| **Final Methods**   | Cannot mock final methods directly.                         | Can mock final methods.                                                  |
| **Private Methods** | Cannot mock private methods directly.                       | Can be used to mock private methods, with some limitations.              |
| **Static Methods**  | Cannot mock static methods.                                 | Can mock static methods when used with PowerMock (outside core Mockito). |
| **Usage**           | Most commonly used for non-void methods with return values. | Used for void methods, final methods, and some edge cases.               |

**`doReturn().when()`** provides more flexibility and is preferred when you encounter situations where **`when().thenReturn()`** fails to work, especially with void, final, and static methods.

---

## 30. How do you mock void methods?

Mocking **void methods** in **Mockito** requires a different approach compared to methods that return a value. In Mockito, since void methods don't return anything, you can't use `when().thenReturn()` to mock them. Instead, you use **`doReturn()`**, **`doNothing()`**, **`doThrow()`**, or **`doAnswer()`** to specify the behavior of the void method when called.

### **Approaches to Mock Void Methods in Mockito**

1. **`doNothing()`** – The default behavior for void methods. It indicates that the method should do nothing when called.
2. **`doThrow()`** – Specifies that the method should throw an exception when called.
3. **`doAnswer()`** – Used for more advanced mocking, where you can define custom behavior for the void method.
4. **`doReturn()`** – Used in some cases to mock void methods, especially when used with the `when()` structure.

---

### **1. `doNothing()` (Default Behavior)**

By default, Mockito assumes that void methods should **do nothing**. If you don't specify anything, the void method will just **execute without any side effects**.

#### Example of `doNothing()` (No need to explicitly call it):

```java
public class DatabaseService {
    public void updateRecord(String record) {
        // Some database logic
    }
}

@Test
void testVoidMethod() {
    // Arrange
    DatabaseService dbServiceMock = mock(DatabaseService.class);
    
    // Act
    dbServiceMock.updateRecord("record1");
    
    // Verify the method was called (no side effects)
    verify(dbServiceMock).updateRecord("record1");
}
```

In this case, `updateRecord()` does nothing, and you don’t need to explicitly use `doNothing()`. However, if you want to explicitly mock a void method, you can use `doNothing()`.

---

### **2. `doReturn()` for Void Methods**

You can use **`doReturn()`** to mock void methods, but it’s more of a workaround in specific situations (like with `when().thenReturn()` for void methods).

#### Example of `doReturn()` for Void Methods:

```java
@Test
void testVoidMethodWithDoReturn() {
    // Arrange
    DatabaseService dbServiceMock = mock(DatabaseService.class);
    
    // Stubbing the void method using doReturn()
    doReturn(null).when(dbServiceMock).updateRecord("record1");
    
    // Act
    dbServiceMock.updateRecord("record1");
    
    // Verify that the void method was called
    verify(dbServiceMock).updateRecord("record1");
}
```

However, using `doReturn()` is **less common** compared to `doNothing()` for void methods.

---

### **3. `doThrow()` for Throwing Exceptions**

You can use **`doThrow()`** to make a void method throw an exception when called. This is useful when you want to simulate error conditions in your tests.

#### Example of `doThrow()` for Void Methods:

```java
@Test
void testVoidMethodThrowingException() {
    // Arrange
    DatabaseService dbServiceMock = mock(DatabaseService.class);
    
    // Stubbing the void method to throw an exception
    doThrow(new RuntimeException("Database error")).when(dbServiceMock).updateRecord("record1");
    
    // Act & Assert
    Exception exception = assertThrows(RuntimeException.class, () -> {
        dbServiceMock.updateRecord("record1");
    });
    
    // Verify that the exception was thrown
    assertEquals("Database error", exception.getMessage());
}
```

Here, **`doThrow()`** is used to make `updateRecord()` throw a `RuntimeException` when called with the argument `"record1"`.

---

### **4. `doAnswer()` for Custom Behavior**

If you need custom behavior, you can use **`doAnswer()`** to define what should happen when the void method is invoked. This is useful for simulating complex side effects or interactions.

#### Example of `doAnswer()` for Void Methods:

```java
import org.mockito.invocation.InvocationOnMock;
import org.mockito.stubbing.Answer;

@Test
void testVoidMethodWithCustomBehavior() {
    // Arrange
    DatabaseService dbServiceMock = mock(DatabaseService.class);
    
    // Stubbing the void method with custom behavior
    doAnswer(new Answer<Void>() {
        @Override
        public Void answer(InvocationOnMock invocation) {
            System.out.println("Custom behavior for updateRecord called");
            return null;
        }
    }).when(dbServiceMock).updateRecord("record1");
    
    // Act
    dbServiceMock.updateRecord("record1");
    
    // Verify that the void method was called
    verify(dbServiceMock).updateRecord("record1");
}
```

In this example, `doAnswer()` allows you to provide **custom behavior** (in this case, printing a message) when `updateRecord()` is called.

---

### **Summary of Mocking Void Methods in Mockito**

| **Method**        | **Usage**                                                    | **Example**                                                                                                      |
| ----------------- | ------------------------------------------------------------ | ---------------------------------------------------------------------------------------------------------------- |
| **`doNothing()`** | Default behavior for void methods. Does nothing when called. | `doNothing().when(mockObject).voidMethod();`                                                                     |
| **`doReturn()`**  | Stubs void methods, can be used in some edge cases.          | `doReturn(null).when(mockObject).voidMethod();`                                                                  |
| **`doThrow()`**   | Makes a void method throw an exception when called.          | `doThrow(new RuntimeException()).when(mockObject).voidMethod();`                                                 |
| **`doAnswer()`**  | Allows custom behavior when a void method is called.         | `doAnswer(invocation -> { System.out.println("Custom behavior"); return null; }).when(mockObject).voidMethod();` |

---

### **Conclusion**

* Use **`doNothing()`** for most void methods when you don’t need to specify custom behavior.
* Use **`doThrow()`** if you want the void method to throw an exception.
* Use **`doAnswer()`** for more complex or custom behaviors when the void method is called.
* **`doReturn()`** is a less common approach for void methods but can be used in specific situations where you need to mock behavior with a workaround.

---

## 31. What does `verifyNoMoreInteractions()` do?

In **Mockito**, the method **`verifyNoMoreInteractions()`** is used to **verify that no other interactions** have occurred with a mock object after the specified interactions have been verified.

### **Purpose of `verifyNoMoreInteractions()`**

The main purpose of **`verifyNoMoreInteractions()`** is to ensure that **no unexpected interactions** (method calls) have been made with the mock object beyond those that were explicitly verified.

This is particularly useful in unit tests where you want to make sure that **only the expected interactions** happened with the mock, and no extra method calls were made.

### **When to Use `verifyNoMoreInteractions()`**

You would typically use `verifyNoMoreInteractions()` after verifying the expected interactions on the mock. This ensures that the mock object was not called in any other unexpected way during the test.

---

### **Syntax**

```java
verifyNoMoreInteractions(mockObject);
```

Where:

* **`mockObject`**: The mock object you want to check for no further interactions.

---

### **Example of `verifyNoMoreInteractions()`**

Let's say you are testing a service class that interacts with a `DatabaseService` mock. You verify that a specific method on the mock was called, and then you use `verifyNoMoreInteractions()` to ensure that **no other methods** were called.

#### **Example Code**:

```java
import static org.mockito.Mockito.*;

public class MyServiceTest {

    @Test
    public void testServiceMethod() {
        // Arrange
        DatabaseService dbServiceMock = mock(DatabaseService.class);
        MyService myService = new MyService(dbServiceMock);

        // Act
        myService.processData("data");

        // Verify the expected interaction
        verify(dbServiceMock).saveData("data");

        // Ensure no other interactions with the mock
        verifyNoMoreInteractions(dbServiceMock);
    }
}
```

### **Explanation**:

1. **Mock Creation**: `DatabaseService dbServiceMock = mock(DatabaseService.class);` creates a mock object of `DatabaseService`.
2. **Method Call**: `myService.processData("data");` calls the method under test in `MyService` that interacts with the mock.
3. **Interaction Verification**: `verify(dbServiceMock).saveData("data");` verifies that the `saveData()` method was called on the mock with `"data"`.
4. **No Further Interactions**: `verifyNoMoreInteractions(dbServiceMock);` checks that no other methods were called on the mock after `saveData()`. If any other method was called, this will throw an exception.

### **When Will `verifyNoMoreInteractions()` Fail?**

`verifyNoMoreInteractions()` will fail (throw an `AssertionError`) if there were any **unexpected interactions** with the mock object that weren't explicitly verified.

For example, if you modify the test and call another method on the mock after `saveData()`, like this:

```java
dbServiceMock.deleteData("data");
```

Then the test will fail because the mock `dbServiceMock` was called with an additional `deleteData()` method, which wasn't expected or verified.

---

### **Why Use `verifyNoMoreInteractions()`?**

* **Avoiding Unwanted Behavior**: Helps ensure that no additional method calls (which may indicate bugs or unexpected behavior) occur on the mock object during the test.
* **Clarity and Precision in Tests**: Ensures that only the specific method calls you're interested in are verified, leading to more precise and controlled tests.
* **Cleanliness**: Ensures that the mock object was used in a controlled and expected manner without any "leakage" of method calls.

---

### **Summary of `verifyNoMoreInteractions()`**

* **Purpose**: Verifies that no further interactions were made with a mock object beyond those explicitly verified.
* **When to Use**: After verifying the expected interactions, to make sure there are no unexpected method calls.
* **Failure Condition**: The test fails if there are any additional, unverified interactions with the mock.

---

**In short**, `verifyNoMoreInteractions()` is a useful tool in unit tests to ensure that your mock objects are only being used in the ways you expect, making your tests more robust and predictable.

---

## 32. How do you simulate exceptions in Mockito?

In **Mockito**, you can simulate exceptions in mocked methods using the **`doThrow()`**, **`when().thenThrow()`**, or **`doAnswer()`** methods. These methods allow you to specify that a method should throw an exception when it is called.

Simulating exceptions is useful for testing error handling and ensuring that your code behaves correctly when an exception occurs.

### **1. `doThrow()`**

The **`doThrow()`** method is used to simulate an exception for **void methods**. Void methods are methods that do not return a value, and because they don't return anything, you can't use `when().thenThrow()` with them. Instead, `doThrow()` is used for stubbing void methods to throw an exception when called.

#### **Syntax**:

```java
doThrow(new ExceptionType("Message")).when(mockObject).voidMethod(arguments);
```

#### **Example**:

```java
@Test
void testVoidMethodThrowingException() {
    // Arrange
    DatabaseService dbServiceMock = mock(DatabaseService.class);

    // Stubbing void method to throw an exception
    doThrow(new RuntimeException("Database error")).when(dbServiceMock).updateRecord("record1");

    // Act & Assert
    RuntimeException exception = assertThrows(RuntimeException.class, () -> {
        dbServiceMock.updateRecord("record1");
    });

    assertEquals("Database error", exception.getMessage());
}
```

In this example:

* **`doThrow(new RuntimeException("Database error"))`**: Stubs the `updateRecord()` method to throw a `RuntimeException` when called.
* The test then verifies that the exception is actually thrown.

---

### **2. `when().thenThrow()`**

The **`when().thenThrow()`** method is used to simulate an exception for **non-void methods** (methods that return a value). You use this method when you want to throw an exception from a method that is expected to return a value.

#### **Syntax**:

```java
when(mockObject.methodCall(arguments)).thenThrow(new ExceptionType("Message"));
```

#### **Example**:

```java
@Test
void testMethodThrowingException() {
    // Arrange
    Calculator calculatorMock = mock(Calculator.class);
    
    // Stubbing the method to throw an exception
    when(calculatorMock.divide(10, 0)).thenThrow(new ArithmeticException("Division by zero"));

    // Act & Assert
    ArithmeticException exception = assertThrows(ArithmeticException.class, () -> {
        calculatorMock.divide(10, 0);
    });

    assertEquals("Division by zero", exception.getMessage());
}
```

In this example:

* **`when(calculatorMock.divide(10, 0)).thenThrow(new ArithmeticException("Division by zero"))`**: Stubs the `divide()` method to throw an `ArithmeticException` when dividing by zero.
* The test then checks that the exception is thrown as expected.

---

### **3. `doAnswer()` for Custom Exception Handling**

You can use **`doAnswer()`** when you need more control over the exception, especially if you want to dynamically throw different exceptions based on certain conditions or inputs.

#### **Syntax**:

```java
doAnswer(invocation -> {
    throw new ExceptionType("Message");
}).when(mockObject).methodCall(arguments);
```

#### **Example**:

```java
@Test
void testMethodThrowingCustomException() {
    // Arrange
    DatabaseService dbServiceMock = mock(DatabaseService.class);

    // Stubbing method to throw an exception based on some logic
    doAnswer(invocation -> {
        String record = invocation.getArgument(0);
        if ("badRecord".equals(record)) {
            throw new IllegalArgumentException("Invalid record");
        }
        return null; // Void method
    }).when(dbServiceMock).updateRecord(anyString());

    // Act & Assert
    IllegalArgumentException exception = assertThrows(IllegalArgumentException.class, () -> {
        dbServiceMock.updateRecord("badRecord");
    });

    assertEquals("Invalid record", exception.getMessage());
}
```

In this example:

* **`doAnswer()`** is used to simulate throwing an exception when a specific condition (`"badRecord"`) is met.
* If the input `"badRecord"` is passed to `updateRecord()`, it throws an `IllegalArgumentException`.

---

### **4. Simulating Checked Exceptions**

You can also simulate **checked exceptions** (like `IOException` or `SQLException`) in a similar way.

#### Example with Checked Exception:

```java
@Test
void testCheckedException() throws Exception {
    // Arrange
    FileService fileServiceMock = mock(FileService.class);
    
    // Stubbing the method to throw a checked exception
    when(fileServiceMock.readFile(anyString())).thenThrow(new IOException("File not found"));

    // Act & Assert
    IOException exception = assertThrows(IOException.class, () -> {
        fileServiceMock.readFile("nonexistentFile.txt");
    });

    assertEquals("File not found", exception.getMessage());
}
```

In this example:

* **`when(fileServiceMock.readFile(anyString())).thenThrow(new IOException("File not found"))`**: Stubs `readFile()` to throw an `IOException` when called.

---

### **Summary of Methods to Simulate Exceptions in Mockito**

| **Method**               | **Use Case**                                                   | **Syntax**                                                                          |
| ------------------------ | -------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| **`doThrow()`**          | Simulate exceptions for void methods.                          | `doThrow(new Exception()).when(mockObject).voidMethod();`                           |
| **`when().thenThrow()`** | Simulate exceptions for non-void methods that return a value.  | `when(mockObject.methodCall()).thenThrow(new Exception());`                         |
| **`doAnswer()`**         | Allows custom exception throwing or other behaviors in a mock. | `doAnswer(invocation -> { throw new Exception(); }).when(mockObject).methodCall();` |

---

### **Summary**

* **`doThrow()`**: Used for void methods to simulate an exception when they are called.
* **`when().thenThrow()`**: Used for non-void methods to simulate an exception when the method is called.
* **`doAnswer()`**: Allows for custom behavior, including throwing exceptions dynamically based on conditions.
* You can simulate **both checked and unchecked exceptions** in Mockito using these methods, depending on whether the method under test is void or returns a value.

---

## 33. Can you mock static methods in Mockito?

Yes, **Mockito** can mock **static methods**, but this feature is available **only in Mockito 3.4.0 and higher** through the **Mockito-inline** extension. By default, **Mockito** does not support mocking static methods. However, with the **Mockito-inline** dependency, you can mock static methods, as well as final methods, constructors, and other elements that are not traditionally mockable.

### **How to Mock Static Methods in Mockito**

To mock static methods in **Mockito**, you need to use the **`Mockito.mockStatic()`** method, which is part of the **Mockito-inline** extension. This method allows you to specify the behavior of static methods during your tests.

### **Steps to Mock Static Methods in Mockito**

1. **Add the Mockito-inline dependency** (if you're using **Mockito 3.x or higher**).
2. Use **`Mockito.mockStatic()`** inside a try-with-resources block or in the test method to ensure that the mock is active only during the test.

---

### **1. Add the `Mockito-inline` Dependency**

To mock static methods, you need to add the `mockito-inline` dependency to your project.

#### **For Maven**:

```xml
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-inline</artifactId>
    <version>4.8.0</version> <!-- Use the latest version -->
    <scope>test</scope>
</dependency>
```

#### **For Gradle**:

```groovy
testImplementation 'org.mockito:mockito-inline:4.8.0' // Use the latest version
```

---

### **2. Example: Mocking Static Methods**

Once you have the **Mockito-inline** dependency, you can mock static methods using `Mockito.mockStatic()`.

#### **Example**: Mocking a Static Method

Suppose you have a class with a static method like this:

```java
public class Utility {
    public static String staticMethod(String input) {
        return "Real Output: " + input;
    }
}
```

Now, you want to mock `staticMethod()` to return a custom value for testing.

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;

class StaticMethodTest {

    @Test
    void testMockStaticMethod() {
        // Arrange
        try (MockedStatic<Utility> mockedStatic = mockStatic(Utility.class)) {
            // Stubbing the static method
            mockedStatic.when(() -> Utility.staticMethod("test")).thenReturn("Mocked Output");

            // Act
            String result = Utility.staticMethod("test");

            // Assert
            assertEquals("Mocked Output", result);
        }
    }
}
```

#### **Explanation**:

1. **`mockStatic(Utility.class)`**: This mocks all static methods in the `Utility` class. It returns a `MockedStatic<Utility>` object.
2. **`mockedStatic.when(() -> Utility.staticMethod("test")).thenReturn("Mocked Output")`**: This stubs the static method to return `"Mocked Output"` when called with the argument `"test"`.
3. **`try (MockedStatic<Utility> mockedStatic = mockStatic(Utility.class))`**: The mock is active inside the try block, and it is automatically cleaned up after the block ends (using **auto-closeable**).
4. **`assertEquals("Mocked Output", result)`**: Verifies that the static method returns the mocked output.

---

### **3. Mocking Multiple Static Methods**

You can also mock **multiple static methods** at the same time.

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;

class StaticMethodTest {

    @Test
    void testMockMultipleStaticMethods() {
        // Arrange
        try (MockedStatic<Utility> mockedStatic = mockStatic(Utility.class)) {
            mockedStatic.when(() -> Utility.staticMethod("test1")).thenReturn("Mocked Output 1");
            mockedStatic.when(() -> Utility.staticMethod("test2")).thenReturn("Mocked Output 2");

            // Act
            String result1 = Utility.staticMethod("test1");
            String result2 = Utility.staticMethod("test2");

            // Assert
            assertEquals("Mocked Output 1", result1);
            assertEquals("Mocked Output 2", result2);
        }
    }
}
```

In this case, we mock **two different static method calls** with different return values.

---

### **4. Verify Static Method Calls**

You can also **verify** that the static method was called with the correct arguments.

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;

class StaticMethodTest {

    @Test
    void testVerifyStaticMethodCall() {
        // Arrange
        try (MockedStatic<Utility> mockedStatic = mockStatic(Utility.class)) {
            // Act
            Utility.staticMethod("test");

            // Assert
            mockedStatic.verify(() -> Utility.staticMethod("test"));
        }
    }
}
```

Here, we verify that **`Utility.staticMethod("test")`** was called during the test.

---

### **5. Resetting Static Mocks**

By default, Mockito resets the static mock automatically after the try-with-resources block ends. However, if you need to reset it manually (which is rare), you can use **`mockedStatic.reset()`**.

---

### **6. Caveats**

* **Performance**: Mocking static methods can lead to slower tests because it adds overhead for mocking. Only use this approach when necessary.
* **Test Scope**: Always use the try-with-resources block or a similar mechanism to ensure that mocks are limited to the test method.
* **Static State**: Static mocks might lead to **shared state** across tests if not cleaned up properly, so ensure mocks are reset or scoped correctly.

---

### **Summary**

* **Mockito** allows mocking of **static methods** starting from **Mockito 3.4.0** using the **`mockito-inline`** extension.
* **`Mockito.mockStatic()`** is used to mock static methods, and it should be used in a try-with-resources block to ensure proper cleanup.
* You can stub, verify, and even mock multiple static methods with this approach.

By following this pattern, you can mock static methods just like any other method in **Mockito**, allowing you to write more flexible unit tests even for classes that rely on static methods.

---

## 34. How is mocking final classes handled in newer versions of Mockito?

In **newer versions of Mockito** (starting from **Mockito 2.x and beyond**), you can now mock **final classes and methods**, which was not possible in earlier versions. This feature is enabled by **Mockito's ability to mock final methods and classes**, thanks to the use of **bytecode manipulation**. This is made possible by **Mockito-inline** (or **Mockito with inline mock maker**), which allows mocking final methods, final classes, and even static methods, constructors, and private methods.

### **How Mocking Final Classes Works in Mockito (Newer Versions)**

Mockito uses **bytecode manipulation** (via **Byte Buddy**) to mock final classes, final methods, and other normally unmockable elements. When you mock final classes or methods, Mockito generates a subclass of the final class at runtime and intercepts the method calls to return the specified mock behavior.

However, this mocking is only possible if you're using **Mockito 2.1.0** or higher along with the **Mockito-inline** extension.

### **Steps to Mock Final Classes and Methods in Mockito**

1. **Add the `Mockito-inline` dependency** to your project.
2. Use the `mock()` method to mock final classes or final methods.
3. Mockito will automatically handle mocking of final classes and methods.

---

### **1. Add the `Mockito-inline` Dependency**

For **Mockito 2.1.0** and higher, if you need to mock **final classes**, you need to include the **Mockito-inline** dependency.

#### **For Maven**:

```xml
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-inline</artifactId>
    <version>4.8.0</version> <!-- Use the latest version -->
    <scope>test</scope>
</dependency>
```

#### **For Gradle**:

```groovy
testImplementation 'org.mockito:mockito-inline:4.8.0' // Use the latest version
```

---

### **2. Example: Mocking a Final Class**

Suppose you have a **final class** like this:

```java
public final class FinalClass {
    public String finalMethod(String input) {
        return "Real Output: " + input;
    }
}
```

Without the `Mockito-inline` dependency, Mockito wouldn't be able to mock `finalClass` or `finalMethod` directly. However, with **Mockito-inline**, you can mock it like this:

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;

class FinalClassTest {

    @Test
    void testMockFinalClass() {
        // Arrange: Mocking the final class
        FinalClass finalClassMock = mock(FinalClass.class);

        // Stubbing the final method to return mocked behavior
        when(finalClassMock.finalMethod("test")).thenReturn("Mocked Output");

        // Act: Calling the mocked method
        String result = finalClassMock.finalMethod("test");

        // Assert: Verifying the mocked behavior
        assertEquals("Mocked Output", result);
    }
}
```

#### **Explanation**:

1. **`mock(FinalClass.class)`**: Mocks the final class `FinalClass`.
2. **`when(finalClassMock.finalMethod("test")).thenReturn("Mocked Output")`**: Stubs the `finalMethod()` to return `"Mocked Output"` instead of the real implementation.
3. The test then verifies that the mocked return value (`"Mocked Output"`) is returned.

---

### **3. Example: Mocking Final Methods in Final Classes**

You can mock **final methods** of any class, not just final classes, by using **Mockito-inline**.

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;

class FinalMethodTest {

    @Test
    void testMockFinalMethod() {
        // Arrange: Mocking the final class
        FinalClass finalClassMock = mock(FinalClass.class);

        // Stubbing a final method in the final class to return a mocked value
        when(finalClassMock.finalMethod("test")).thenReturn("Mocked Final Method");

        // Act: Calling the mocked method
        String result = finalClassMock.finalMethod("test");

        // Assert: Verifying the mocked behavior
        assertEquals("Mocked Final Method", result);
    }
}
```

This allows you to mock the **final method** (`finalMethod()`) just like any regular method, and you can control its behavior using `when().thenReturn()`.

---

### **4. How Mockito Handles Mocking Final Classes**

* **Mockito-inline** makes use of **Byte Buddy**, which is a library that allows bytecode manipulation at runtime. It generates subclasses of the final class or method and intercepts method calls to return the mocked behavior.
* This is different from traditional mocking, where Mockito uses proxies to intercept method calls. **Byte Buddy** allows the interception of method calls for classes and methods that are normally unmockable (like **final methods**, **final classes**, and **static methods**).

---

### **5. Limitations and Considerations**

* **Performance Overhead**: Mocking final methods and classes can incur a slight performance penalty due to the use of bytecode manipulation.
* **Complexity**: Mocking final classes or methods might make tests harder to understand and maintain, especially when dealing with complex final classes.
* **Mockito Configuration**: Make sure the **Mockito-inline** extension is enabled to use this feature. Without it, Mockito will not mock final classes or methods.

---

### **Summary**

* **Mockito** can mock final classes and final methods starting from **Mockito 2.1.0** or later with the **Mockito-inline** extension.
* Use **`Mockito.mock()`** as usual, and Mockito will handle mocking final classes and methods at runtime using **bytecode manipulation**.
* This feature helps to write unit tests for classes that are marked as **final** or have **final methods**, which were previously difficult or impossible to mock.

To mock final methods and classes, make sure to include the **`mockito-inline`** dependency and enjoy the benefits of mocking even traditionally unmockable elements in your tests.

---

## 35. How do you reset a mock?

In **Mockito**, you can reset a mock to its original state using the **`Mockito.reset()`** method. This is useful when you want to clear any interactions, stubbing, or state modifications on a mock during or between tests.

Resetting a mock is generally done in certain scenarios like:

* When you have multiple tests that share a mock and want to clear its previous interactions or stubbing between tests.
* When you want to ensure that the mock's state does not carry over between test methods.

### **How to Reset a Mock**

The **`Mockito.reset()`** method can be used to reset one or more mocks to their default state.

### **Syntax:**

```java
Mockito.reset(mockObject);
```

You can reset **multiple mocks** at once by passing them as arguments to `reset()`.

```java
Mockito.reset(mock1, mock2, mock3);
```

---

### **Example: Resetting a Mock**

Let’s say you have a mock of a `DatabaseService` class and you want to reset it between test methods.

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;

class DatabaseServiceTest {

    private DatabaseService dbServiceMock;

    @BeforeEach
    void setup() {
        // Create a new mock instance before each test
        dbServiceMock = mock(DatabaseService.class);
    }

    @Test
    void testMethod1() {
        // Stubbing a method
        when(dbServiceMock.getData("key")).thenReturn("Data 1");

        // Calling the mocked method
        String result = dbServiceMock.getData("key");

        // Assert the result
        assertEquals("Data 1", result);

        // Reset the mock at the end of the test if needed
        reset(dbServiceMock);
    }

    @Test
    void testMethod2() {
        // Reset the mock at the beginning of the test if needed
        reset(dbServiceMock);

        // Stubbing a method
        when(dbServiceMock.getData("key")).thenReturn("Data 2");

        // Calling the mocked method
        String result = dbServiceMock.getData("key");

        // Assert the result
        assertEquals("Data 2", result);
    }
}
```

### **Explanation**:

1. **`Mockito.reset(mock)`**: In the `testMethod1()`, you can reset the mock at the end to clear all the previous interactions and stubbing.
2. In `testMethod2()`, you could reset the mock at the beginning of the test to ensure no previous state or interactions affect the current test.

---

### **When Should You Use `Mockito.reset()`?**

* **When a Mock Is Shared Between Tests**: If a single mock is shared between multiple test methods (which isn't a common practice in clean tests, but sometimes necessary in complex setups), you can use `reset()` to ensure the mock does not carry state from one test to another.

* **After Verifying Interactions**: If you've verified interactions on the mock and want to clear them, you can use `reset()` to clear out any recorded interactions.

* **To Clear Stubbing**: If you want to clear previous stubbing and set new behavior on a mock, you can reset the mock and re-stub it with fresh behavior.

---

### **Important Considerations**

* **Not Usually Recommended in Every Test**: Typically, it's better to **avoid resetting mocks** in unit tests because tests should ideally be independent and mock state should be isolated per test. Instead, create new mocks for each test case or use **JUnit lifecycle methods** like `@BeforeEach` or `@BeforeAll` to initialize mocks for each test.

* **Potential Performance Impact**: While resetting mocks is generally efficient, unnecessary resetting can make tests more complex and potentially slower if done repeatedly across many tests.

* **Mockito's `@Mock` and `@InjectMocks` with `MockitoAnnotations.initMocks()`**: When using `@Mock` annotations, mocks are typically re-initialized at the start of each test via `MockitoAnnotations.initMocks(this)` or the `@ExtendWith(MockitoExtension.class)` extension in JUnit 5. Therefore, resetting might not be needed if you're re-initializing mocks in each test.

---

### **Summary**

* **`Mockito.reset()`** clears all interactions and stubbing on a mock object, returning it to its initial state.
* It’s typically used when you need to clear state between tests or ensure the mock is in a clean state for the next test.
* **Best practice** is to avoid resetting mocks unless necessary. Try to keep tests independent and isolate the mock's state per test.

---

## 36. How do you mock a list or collection?

Mocking collections, such as a **`List`**, **`Set`**, or **`Map`**, in **Mockito** follows the same principles as mocking any other object. You can use **Mockito's `mock()`** method to mock these collections. Once mocked, you can define the behavior of these collections (like returning specific elements when accessed, throwing exceptions, etc.).

### **Mocking a List or Collection in Mockito**

Mockito allows you to mock **`List`**, **`Set`**, and other collections to simulate the behavior of real collections. You can stub methods of these collections (e.g., `add()`, `remove()`, `get()`, `size()`, etc.) to return specific values as required by your tests.

Here’s how you can mock a collection like **`List`** or **`Set`**:

---

### **1. Mocking a `List`**

You can mock a **`List`** in Mockito and define the behavior for methods such as `get()`, `size()`, and `add()`.

#### **Example: Mocking a `List`**

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;
import java.util.List;

class MockListTest {

    @Test
    void testMockList() {
        // Mocking the List
        List<String> mockedList = mock(List.class);

        // Stubbing the behavior
        when(mockedList.get(0)).thenReturn("Hello");
        when(mockedList.size()).thenReturn(2);

        // Testing the mocked behavior
        System.out.println(mockedList.get(0));  // Output: Hello
        System.out.println(mockedList.size());  // Output: 2

        // Verifying the interaction
        verify(mockedList).get(0);  // Verify that get(0) was called
        verify(mockedList).size();  // Verify that size() was called
    }
}
```

#### **Explanation**:

* **`mock(List.class)`**: Creates a mock of a `List` (or any other collection).
* **`when(mockedList.get(0)).thenReturn("Hello")`**: Stubs the `get(0)` method to return `"Hello"` when the `List` is accessed at index 0.
* **`when(mockedList.size()).thenReturn(2)`**: Stubs the `size()` method to return `2`.
* **`verify()`**: Verifies that the mocked methods (`get(0)` and `size()`) were actually called.

---

### **2. Mocking a `Set`**

You can also mock a **`Set`** (or any other collection) in the same way. Here's an example for mocking a `Set`:

#### **Example: Mocking a `Set`**

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;
import java.util.Set;

class MockSetTest {

    @Test
    void testMockSet() {
        // Mocking the Set
        Set<String> mockedSet = mock(Set.class);

        // Stubbing the behavior
        when(mockedSet.contains("Apple")).thenReturn(true);
        when(mockedSet.size()).thenReturn(3);

        // Testing the mocked behavior
        System.out.println(mockedSet.contains("Apple"));  // Output: true
        System.out.println(mockedSet.size());  // Output: 3

        // Verifying the interaction
        verify(mockedSet).contains("Apple");
        verify(mockedSet).size();
    }
}
```

This mocks a **`Set`** and stubs the `contains()` and `size()` methods.

---

### **3. Mocking a `Map`**

Similarly, you can mock a **`Map`** and define behavior for methods like `get()`, `put()`, `size()`, etc.

#### **Example: Mocking a `Map`**

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;
import java.util.Map;

class MockMapTest {

    @Test
    void testMockMap() {
        // Mocking the Map
        Map<String, String> mockedMap = mock(Map.class);

        // Stubbing the behavior
        when(mockedMap.get("key1")).thenReturn("value1");
        when(mockedMap.size()).thenReturn(2);

        // Testing the mocked behavior
        System.out.println(mockedMap.get("key1"));  // Output: value1
        System.out.println(mockedMap.size());  // Output: 2

        // Verifying the interaction
        verify(mockedMap).get("key1");
        verify(mockedMap).size();
    }
}
```

This mocks a **`Map`** and stubs the `get()` and `size()` methods.

---

### **4. Mocking Collection Additions**

You can also mock methods like `add()`, `remove()`, or `put()` to simulate modifying the collection.

#### **Example: Mocking `add()` for a `List`**

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;
import java.util.List;

class MockListAddTest {

    @Test
    void testMockListAdd() {
        // Mocking the List
        List<String> mockedList = mock(List.class);

        // Stubbing the behavior for the add() method to do nothing
        doNothing().when(mockedList).add("item1");

        // Calling the method
        mockedList.add("item1");

        // Verifying the interaction
        verify(mockedList).add("item1");  // Verifying that add() was called
    }
}
```

In this example, we mock the **`add()`** method of the **`List`** to perform no action when the `add()` method is called.

---

### **5. Use of `@Mock` with Collections**

When using the **`@Mock`** annotation in **JUnit 5** with **Mockito**, you can automatically mock collections.

```java
import org.junit.jupiter.api.Test;
import org.mockito.Mock;
import java.util.List;

class MockAnnotationTest {

    @Mock
    List<String> mockedList;

    @Test
    void testMockList() {
        // Stubbing the behavior
        when(mockedList.get(0)).thenReturn("Mocked Item");

        // Calling the mocked method
        String result = mockedList.get(0);

        // Assert the result
        assertEquals("Mocked Item", result);
    }
}
```

You can initialize mocks using **Mockito annotations** by using **`@ExtendWith(MockitoExtension.class)`** in **JUnit 5**.

---

### **6. Commonly Used Collection Methods to Mock**

Here are some commonly used methods from collections that you can mock:

* **`add()`**: Adds an element to the collection.
* **`remove()`**: Removes an element from the collection.
* **`contains()`**: Checks if the collection contains a specific element.
* **`size()`**: Returns the number of elements in the collection.
* **`clear()`**: Removes all elements from the collection.
* **`get()`**: Retrieves an element at a given index (for `List` or `Map`).
* **`put()`**: Adds a key-value pair to a `Map`.

---

### **Summary**

* **Mocking Collections**: You can use **Mockito** to mock collections like **`List`**, **`Set`**, and **`Map`** by using `mock()` and stubbing methods like `get()`, `size()`, `contains()`, etc.
* **Stubbing Collection Methods**: Methods like `get()`, `contains()`, and `add()` can be stubbed to return specific values or perform certain actions.
* **Verification**: Use `verify()` to check that the mocked collection methods were called with expected arguments.

By mocking collections in your unit tests, you can simulate their behavior and control how they interact with the rest of your application without relying on real data structures.

---

## 37. What is the use of `ArgumentCaptor` in Mockito?

In **Mockito**, the **`ArgumentCaptor`** is used to capture the arguments passed to a mocked method during the test execution. This is useful when you need to verify or assert the actual values passed to a method, especially when dealing with void methods or when the method call doesn't return a value.

It allows you to **intercept** the arguments passed to the mock and capture them for later inspection.

### **When to Use `ArgumentCaptor`?**

* **Capturing Arguments**: When you want to capture arguments passed to a method on a mocked object to verify their values.
* **Verifying Method Interactions**: Useful for verifying that the correct arguments are passed to a method, especially for **void methods** or methods where the return value is not important.
* **Test Cases Where Return Value Isn't Enough**: When you need to verify the actual data passed to a method but cannot rely on the return value alone.

### **How to Use `ArgumentCaptor`**

1. **Create an ArgumentCaptor**: You create an instance of `ArgumentCaptor` for the type of argument you want to capture.
2. **Capture Arguments**: Use `ArgumentCaptor` with `verify()` to capture the arguments passed to the mock method.
3. **Assert Captured Arguments**: After capturing, you can perform assertions on the captured arguments.

### **Syntax**

```java
ArgumentCaptor<Type> captor = ArgumentCaptor.forClass(Type.class);
verify(mockObject).method(captor.capture());
Type capturedArgument = captor.getValue();
```

### **Example of Using `ArgumentCaptor`**

Let’s take an example where you have a method in a service class that takes a list and adds a value to it.

#### **Code Under Test**

```java
public class MyService {
    private List<String> dataList;

    public MyService(List<String> dataList) {
        this.dataList = dataList;
    }

    public void addData(String data) {
        dataList.add(data);
    }
}
```

#### **Test Using `ArgumentCaptor`**

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;
import org.mockito.ArgumentCaptor;
import java.util.List;

class MyServiceTest {

    @Test
    void testAddData() {
        // Mocking the List
        List<String> mockList = mock(List.class);

        // Create instance of MyService
        MyService myService = new MyService(mockList);

        // Calling method under test
        myService.addData("Test Data");

        // Create ArgumentCaptor for String
        ArgumentCaptor<String> captor = ArgumentCaptor.forClass(String.class);

        // Verifying the interaction and capturing the argument passed to the add() method
        verify(mockList).add(captor.capture());

        // Get the captured value
        String capturedArgument = captor.getValue();

        // Assert that the correct argument was passed to the method
        assertEquals("Test Data", capturedArgument);
    }
}
```

### **Explanation:**

1. **Mock List**: We mock the `List` (which is passed to `MyService`).
2. **ArgumentCaptor**: We create an `ArgumentCaptor<String>` to capture the argument passed to the `add()` method of the mocked `List`.
3. **`verify()`**: We use `verify(mockList).add(captor.capture())` to capture the argument passed to `add()`.
4. **Capture the Argument**: After the method call, we use `captor.getValue()` to get the captured argument.
5. **Assertion**: We assert that the captured argument matches the expected value (`"Test Data"`).

### **Using `ArgumentCaptor` for Void Methods**

`ArgumentCaptor` is particularly useful when mocking **void methods** since void methods don’t return values that you can verify. You can use it to capture the argument passed to the void method.

#### **Example: Void Method with `ArgumentCaptor`**

```java
public class MyService {
    private List<String> dataList;

    public MyService(List<String> dataList) {
        this.dataList = dataList;
    }

    public void updateData(String data) {
        dataList.add(data);
    }
}

class MyServiceTest {

    @Test
    void testUpdateData() {
        List<String> mockList = mock(List.class);

        MyService myService = new MyService(mockList);

        // Call the void method
        myService.updateData("Updated Data");

        // Capture the argument passed to the updateData method
        ArgumentCaptor<String> captor = ArgumentCaptor.forClass(String.class);

        // Verify the method call and capture the argument
        verify(mockList).add(captor.capture());

        // Assert the captured value
        assertEquals("Updated Data", captor.getValue());
    }
}
```

Here, **`updateData`** is a **void method**, but we can still capture the argument passed to it (the `"Updated Data"` string) using **`ArgumentCaptor`**.

### **Common Use Cases for `ArgumentCaptor`**

1. **Verifying Argument Values**: When you need to check that a method received the expected arguments.
2. **Verifying Void Methods**: For void methods where the only thing you can verify is the argument that was passed to them.
3. **Complex Assertions**: When the argument passed to the method is an object or collection, and you want to verify its state or properties.

### **Summary**

* **`ArgumentCaptor`** is a useful feature in **Mockito** for capturing arguments passed to mocked methods, especially void methods or methods with no return value.
* It allows you to **verify** the arguments passed to methods and **perform assertions** on them.
* It is most useful in **void methods** or when the method call itself doesn't return anything you can verify directly.

---

## 38. What is deep stubbing and when is it useful?

**Deep Stubbing** in **Mockito** is a feature that allows you to stub methods of mock objects that return other mock objects. In other words, it's the process of mocking not only the direct method call but also any subsequent method calls on the objects returned by those methods. This is especially useful when dealing with complex objects or chains of method calls where you want to control behavior deeply without actually having to instantiate the entire object hierarchy.

### **What is Deep Stubbing?**

Deep stubbing is the ability to mock **method chains** or **nested method calls** on mock objects. This is typically done when a method returns another mock object, and you want to stub methods on that returned object as well.

In **Mockito**, you can achieve deep stubbing by calling **`Mockito.when()`** on methods that return mocked objects and chain multiple method calls on the same mock.

### **Example of Deep Stubbing**

Let's consider a scenario where you have a method that returns an object, and you want to stub a method on that returned object as well.

#### **Code Under Test:**

```java
public class UserService {

    private DatabaseService databaseService;

    public UserService(DatabaseService databaseService) {
        this.databaseService = databaseService;
    }

    public String getUserDetails(String userId) {
        User user = databaseService.findUser(userId);  // This returns a User object.
        return user.getName();  // We want to mock this method.
    }
}

class DatabaseService {
    public User findUser(String userId) {
        // Simulate fetching user from the database.
        return new User();
    }
}

class User {
    public String getName() {
        // Simulates returning a user's name.
        return "John Doe";
    }
}
```

In the example above, `getUserDetails()` calls `findUser()` of `DatabaseService` to get a `User` object and then calls `getName()` on the `User` object. To test `getUserDetails()`, you would need to mock both `findUser()` and `getName()`.

#### **Example of Deep Stubbing in Mockito**

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;

class UserServiceTest {

    @Test
    void testGetUserDetails() {
        // Mock DatabaseService and User
        DatabaseService mockDatabaseService = mock(DatabaseService.class);
        User mockUser = mock(User.class);

        // Stubbing the findUser method to return a mocked User object
        when(mockDatabaseService.findUser("user123")).thenReturn(mockUser);

        // Stubbing the getName method to return a specific value
        when(mockUser.getName()).thenReturn("John Doe");

        // Create an instance of UserService with the mocked DatabaseService
        UserService userService = new UserService(mockDatabaseService);

        // Call the method under test
        String userName = userService.getUserDetails("user123");

        // Assert the expected result
        assertEquals("John Doe", userName);
    }
}
```

In the above example:

* We mock both the **`DatabaseService`** and **`User`**.
* We stub the `findUser()` method to return the `mockUser` mock.
* We stub the `getName()` method on the `mockUser` to return `"John Doe"`.
* This way, both the call to `findUser()` and the subsequent call to `getName()` are effectively mocked, allowing us to test `getUserDetails()`.

### **Deep Stubbing with `Mockito`'s `lenient()`**

Deep stubbing can sometimes result in unnecessary `StubbingException` errors if some methods are not explicitly stubbed. You can use **`lenient()`** stubbing to avoid such exceptions.

```java
lenient().when(mockDatabaseService.findUser("user123")).thenReturn(mockUser);
```

This ensures that even if `findUser()` is not called or stubbed in certain cases, it won't throw a `StubbingException`.

### **Deep Stubbing with `@Mock` and `MockitoAnnotations.initMocks()`**

You can use **Mockito annotations** with deep stubbing. For example:

```java
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;

class UserServiceTest {

    @Mock
    private DatabaseService mockDatabaseService;
    
    @Mock
    private User mockUser;

    @InjectMocks
    private UserService userService;

    @Test
    void testGetUserDetails() {
        // Stubbing the mock behavior
        when(mockDatabaseService.findUser("user123")).thenReturn(mockUser);
        when(mockUser.getName()).thenReturn("John Doe");

        // Call the method under test
        String userName = userService.getUserDetails("user123");

        // Assert the expected result
        assertEquals("John Doe", userName);
    }
}
```

Here, `@Mock` is used to mock the required dependencies (`DatabaseService` and `User`), and **`@InjectMocks`** automatically injects those mocks into the `UserService`.

### **When is Deep Stubbing Useful?**

1. **Complex Object Chains**: When you have methods that return objects, and you want to mock their behavior as well. For example, if a method returns another object which has further methods to mock.

    * Example: Mocking a `Map` that returns other mock objects, or chaining method calls on deeply nested objects.

2. **Interacting with Multiple Layers**: If your code interacts with different layers (e.g., service layer calling a repository which returns entities) and you want to mock all the layers in the chain.

3. **Testing Complex Systems**: In some complex applications, you might have many objects collaborating with each other, and mocking all methods (using deep stubbing) makes it easier to control the behavior without creating an actual implementation.

4. **Avoiding Actual Object Creation**: Deep stubbing allows you to avoid the complexity of manually creating mock objects or setting up real objects for all the components involved.

### **Limitations of Deep Stubbing**

While deep stubbing is powerful, there are a few things to consider:

1. **Not Always Ideal for Test Clarity**: Deep stubbing can make tests harder to understand and maintain, as it hides the real implementation details. It can also make tests more fragile, as they depend heavily on the mocked behavior of various methods.

2. **Performance**: Deep stubbing might have a small performance overhead, as Mockito needs to create more mocks and manage a more complex object structure.

3. **Mockito's Default Behavior**: By default, Mockito does **not** support deep stubbing. You must explicitly use **`lenient()`** or configure your tests to enable deep stubbing.

### **Conclusion**

**Deep Stubbing** is useful when you need to mock a chain of method calls on mocked objects. It's a powerful feature for dealing with complex object structures and testing scenarios where multiple method calls return mock objects. However, it should be used judiciously because it can make tests harder to understand and maintain.

---

## 39. How do you mock method chaining?

**Mocking method chaining** is a technique in **Mockito** where you mock a series of method calls on an object that returns another object, allowing you to simulate behavior for each method in the chain. This is commonly required when the method returns an object, and you want to continue calling methods on that returned object without actually instantiating them.

### **What is Method Chaining?**

Method chaining occurs when multiple methods are called consecutively on the same object. For example, consider the following class:

```java
public class MyClass {
    public MyClass method1() {
        // method logic
        return this;
    }

    public MyClass method2() {
        // method logic
        return this;
    }

    public String method3() {
        return "final method";
    }
}
```

You could chain the methods like this:

```java
MyClass obj = new MyClass();
obj.method1().method2().method3(); // Method chaining
```

In the above example, `method1()` returns the object itself (i.e., `this`), allowing you to chain `method2()` and `method3()`.

### **Mocking Method Chaining in Mockito**

When you mock method chaining, you mock each method in the chain so that it returns a mock object for the next method in the chain. This can be achieved by configuring the mocked methods to return the mocked objects themselves.

#### **Steps to Mock Method Chaining:**

1. **Mock the Object**: Create a mock of the class you are testing.
2. **Stub Each Method in the Chain**: For each method that returns a new object, stub it to return the mock object.
3. **Test the Desired Behavior**: Perform assertions based on the behavior of the chained methods.

### **Example of Mocking Method Chaining in Mockito**

Let’s use the `MyClass` example from above, but this time we will mock the method calls.

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;

class MyClassTest {

    @Test
    void testMethodChaining() {
        // Mock MyClass
        MyClass mockObject = mock(MyClass.class);

        // Stubbing the chained methods
        when(mockObject.method1()).thenReturn(mockObject);  // method1 returns the mockObject
        when(mockObject.method2()).thenReturn(mockObject);  // method2 returns the mockObject
        when(mockObject.method3()).thenReturn("Chained method result"); // method3 returns a result

        // Call the chained methods
        String result = mockObject.method1().method2().method3();

        // Assert the result of the chained method call
        assertEquals("Chained method result", result);

        // Verify the methods were called
        verify(mockObject).method1();
        verify(mockObject).method2();
        verify(mockObject).method3();
    }
}
```

### **Explanation:**

1. **Mocking the Object**: We create a mock of `MyClass` using `mock(MyClass.class)`.
2. **Stubbing the Methods**:

    * `when(mockObject.method1()).thenReturn(mockObject);`: We stub `method1()` to return the same mock object (`mockObject`) so we can continue chaining.
    * `when(mockObject.method2()).thenReturn(mockObject);`: Similarly, `method2()` is stubbed to return `mockObject` for further chaining.
    * `when(mockObject.method3()).thenReturn("Chained method result");`: Finally, `method3()` is stubbed to return the expected result when it’s called at the end of the chain.
3. **Chaining the Method Calls**: We call `method1().method2().method3()` in a chain, just like in the original code. This will execute the stubs and return the result.
4. **Verification**: We use `verify()` to check that each method was called in the chain.

### **Real-World Example**

Let’s assume you are testing a builder pattern or a configuration class that uses method chaining. Here’s an example with a builder class:

```java
public class Builder {
    public Builder step1() {
        // Logic for step1
        return this;
    }

    public Builder step2() {
        // Logic for step2
        return this;
    }

    public String build() {
        return "Built object";
    }
}
```

You can mock this method chaining as follows:

```java
import static org.mockito.Mockito.*;
import org.junit.jupiter.api.Test;

class BuilderTest {

    @Test
    void testBuilderMethodChaining() {
        // Create a mock of Builder class
        Builder mockBuilder = mock(Builder.class);

        // Stub the methods for chaining
        when(mockBuilder.step1()).thenReturn(mockBuilder);
        when(mockBuilder.step2()).thenReturn(mockBuilder);
        when(mockBuilder.build()).thenReturn("Built object");

        // Use the method chain
        String result = mockBuilder.step1().step2().build();

        // Assert the result
        assertEquals("Built object", result);

        // Verify method calls
        verify(mockBuilder).step1();
        verify(mockBuilder).step2();
        verify(mockBuilder).build();
    }
}
```

### **When to Use Method Chaining Mocking**

1. **Builder Patterns**: Many builders use method chaining, and you can mock each method to simulate their execution.
2. **Fluent APIs**: Some APIs provide a fluent interface (methods returning the object itself), and mocking allows you to simulate the behavior of the API without creating actual objects.
3. **Mocking Complex Dependencies**: When a method depends on multiple layers of objects that return more objects (for example, a service that returns a configuration object which itself has methods), deep stubbing and method chaining can help mock such behaviors.

### **Limitations**

1. **Readability**: Method chaining can make tests less readable, especially when many methods are chained together. It's often better to mock only the essential methods and focus on the parts you're testing.
2. **Fragile Tests**: If the method chain changes or the order of calls is modified, it could lead to fragile tests that break easily. You may need to constantly update the mock behavior.
3. **Mockito Limitations**: In some complex cases, Mockito may require additional configuration or libraries (e.g., using `lenient()` for lenient stubbing).

### **Summary**

* **Method chaining** is a technique where multiple methods are called consecutively on the same object.
* **Mocking method chaining** in **Mockito** involves stubbing each method in the chain to return either the mock object itself or a final result.
* **Use deep stubbing** to simulate chained methods, especially in **builder patterns** or **fluent interfaces**.
* Ensure that the tests remain maintainable by mocking only the required methods and keeping the chains manageable.

---

## 40. How do you test private methods (should you?)?

Testing private methods is a topic that often sparks debate in the software development community. The general rule of thumb is that you **should not** directly test private methods, because they are implementation details that are intended to be hidden from the outside world. Instead, you should focus on testing **public methods** that rely on those private methods.

However, there are scenarios where you might feel the need to test private methods directly. Let's break down both approaches: why testing private methods is generally avoided, and how you could test them if needed.

### **Should You Test Private Methods?**

#### **Why You Shouldn't Test Private Methods:**

1. **Private Methods Are Implementation Details**: Private methods are not part of the class's public API, so testing them directly goes against the principle of encapsulation. Tests should focus on the class's behavior (through its public interface), not on how it is implemented internally.

2. **Refactoring and Maintenance**: If your tests are tightly coupled to private methods, any changes in the private methods will likely require you to modify the tests, even if the public behavior remains the same. This makes your tests more fragile and harder to maintain.

3. **Test Behavior, Not Implementation**: The best practice is to write tests that focus on **what the class does**, not how it does it. Private methods should only be tested if they significantly affect the behavior of the public methods, and in most cases, testing the public methods indirectly tests the private methods.

### **When Might You Test Private Methods?**

While you generally shouldn't test private methods directly, there are some cases where it might make sense:

* **Complex Logic**: If a private method contains very complex logic that is crucial to the correct operation of the class, and it can't be easily tested through public methods.
* **Legacy Code**: In some legacy systems, you might not have good public methods that expose the behavior of the private methods, and direct testing might be needed for validation.
* **Code Coverage**: In some cases, achieving high code coverage might require testing private methods. However, this shouldn't be the primary motivation for writing tests.

### **How to Test Private Methods in Java (If Absolutely Necessary)**

If you decide to test private methods, there are several ways you can achieve this in Java, using different techniques. Here are the most common approaches:

### 1. **Using Reflection**

Reflection allows you to access private methods, fields, and constructors in Java. With reflection, you can invoke a private method and validate its behavior.

#### **Example Using Reflection:**

```java
import java.lang.reflect.Method;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class MyClass {

    private String reverseString(String input) {
        return new StringBuilder(input).reverse().toString();
    }
}

class MyClassTest {

    @Test
    void testPrivateMethodUsingReflection() throws Exception {
        MyClass myClass = new MyClass();

        // Get the private method by name and parameter type
        Method method = MyClass.class.getDeclaredMethod("reverseString", String.class);
        
        // Make the method accessible (it's private)
        method.setAccessible(true);

        // Invoke the method with a test input
        String result = (String) method.invoke(myClass, "hello");

        // Assert the result
        assertEquals("olleh", result);
    }
}
```

#### **Explanation:**

* **`getDeclaredMethod()`**: Retrieves the private method by name and parameter type.
* **`setAccessible(true)`**: Allows access to private methods.
* **`invoke()`**: Executes the method on the object.

While reflection gives you the ability to test private methods, it's **not ideal** because it breaks encapsulation and makes the tests more difficult to maintain.

### 2. **Using `@VisibleForTesting` or Custom Annotations**

In some projects, you might see custom annotations like `@VisibleForTesting` used to indicate that a private method is made more visible (for testing purposes). Some teams use this approach when they want to expose private methods for testing but don't want to change the overall design.

However, this should be used sparingly because it can lead to **design smells** if not done carefully.

### 3. **Changing Method Visibility (Refactor to Package-Private or Protected)**

Another approach is to refactor the private method to a package-private (default access) or protected method so that it can be accessed from the test class without violating encapsulation as much. This is still not a recommended practice, but it is a step better than making a method public just for testing.

### 4. **Using PowerMock (Advanced)**

PowerMock is a popular framework that allows you to mock private, static, and final methods. It is typically used in complex cases where traditional mocking is not sufficient.

Here is an example of using PowerMock to mock a private method:

```java
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

class MyClass {
    
    private String privateMethod() {
        return "secret";
    }

    public String publicMethod() {
        return privateMethod();
    }
}

class MyClassTest {

    @Test
    void testPrivateMethodUsingPowerMock() {
        MyClass myClass = spy(new MyClass());
        
        // Mock the private method
        doReturn("mocked value").when(myClass, "privateMethod");
        
        // Test public method that calls private method
        String result = myClass.publicMethod();

        // Assert the result
        assertEquals("mocked value", result);
    }
}
```

This approach uses **PowerMock** to spy on the method and mock its behavior. PowerMock is a powerful tool but should be used cautiously, as it breaks some of the fundamental principles of object-oriented design.

### **Best Practice: Test Public Methods Instead**

Rather than testing private methods directly, consider the following alternatives:

1. **Test Through Public Methods**: If the private method is crucial for the behavior of the public method, writing tests for the public methods indirectly tests the private method.

    * **Example**: If `privateMethod()` is called inside `publicMethod()`, test `publicMethod()` instead. If `publicMethod()` works correctly, `privateMethod()` is being tested indirectly.
2. **Refactor Code**: If a private method is complex and difficult to test indirectly, you might consider refactoring your class to improve testability. For example, you could extract the logic of the private method into a separate, testable class that can be tested directly via its public API.

### **Conclusion**

* **Avoid testing private methods directly**, as they are implementation details. Focus on testing the **behavior** of your classes via their public API.
* If you absolutely need to test private methods, **use reflection**, or tools like **PowerMock**. However, such techniques should be used sparingly.
* A better approach is often to **refactor** the code to improve testability or expose functionality through **public methods** that indirectly test private logic.

By testing through the public API, you ensure that your tests remain robust and maintainable, and that your code is encapsulated properly.

---

### 🔹 41–60: **Spring Boot Testing**

## 41. How do you write unit tests in Spring Boot?

Writing unit tests in **Spring Boot** follows similar principles to unit testing in Java, but with the added benefit of the **Spring Framework** providing tools and annotations to facilitate testing Spring components. Spring Boot makes it easy to write unit tests, integrate testing, and mock Spring-specific functionality. Here’s how you can go about writing unit tests in Spring Boot:

### **1. Setting Up the Environment for Testing**

To write unit tests in Spring Boot, you need the following dependencies:

* **Spring Boot Starter Test**: It includes libraries like JUnit, Mockito, Hamcrest, and Spring Test. You can include it in your `pom.xml` or `build.gradle` file:

#### **Maven (pom.xml)**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

#### **Gradle (build.gradle)**

```gradle
testImplementation 'org.springframework.boot:spring-boot-starter-test'
```

### **2. Unit Testing with JUnit and Spring Boot**

Spring Boot uses **JUnit 5** by default (since Spring 5). The main testing annotations used in Spring Boot are:

* `@SpringBootTest`: It is used to test the entire Spring context. It’s typically used for integration tests rather than unit tests.
* `@WebMvcTest`: It is used to test only the web layer (controllers).
* `@MockBean`: It’s used to add mock beans to the Spring application context, allowing you to mock Spring beans in tests.

### **Writing Unit Tests in Spring Boot**

#### **Basic Unit Test Example**

Consider you have a simple service class and a controller that you want to test.

1. **Service Class**:

```java
@Service
public class MyService {
    public String processData(String input) {
        return "Processed: " + input;
    }
}
```

2. **Controller Class**:

```java
@RestController
public class MyController {

    @Autowired
    private MyService myService;

    @GetMapping("/process")
    public String process(@RequestParam String input) {
        return myService.processData(input);
    }
}
```

#### **Testing the Service Layer (Unit Test)**

To test the service layer, we typically mock any dependencies and test the service methods.

```java
import static org.junit.jupiter.api.Assertions.*;
import org.junit.jupiter.api.Test;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

@ExtendWith(MockitoExtension.class)  // This enables Mockito in JUnit 5
public class MyServiceTest {

    @Mock
    private MyService myService;

    @Test
    void testProcessData() {
        // Arrange
        String input = "Test Input";
        String expectedOutput = "Processed: Test Input";

        // Stubbing the method
        when(myService.processData(input)).thenReturn(expectedOutput);

        // Act
        String result = myService.processData(input);

        // Assert
        assertEquals(expectedOutput, result);
    }
}
```

In this case, the unit test mocks the `MyService` class to isolate the behavior of the method `processData`.

#### **Testing the Controller Layer (Integration Test)**

To test the controller, you can use `@WebMvcTest`, which is tailored for testing controllers. It doesn’t load the entire Spring context but only the web layer (i.e., controllers, filters, etc.). This makes the test faster than using `@SpringBootTest`.

```java
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.context.junit.jupiter.SpringExtension;
import org.springframework.test.web.servlet.MockMvc;

import static org.mockito.Mockito.when;

@ExtendWith(SpringExtension.class)  // Allows Spring extensions in JUnit 5
@WebMvcTest(MyController.class)     // Only loads the controller for testing
public class MyControllerTest {

    @Mock
    private MyService myService;

    @InjectMocks
    private MyController myController;

    @Autowired
    private MockMvc mockMvc;

    @Test
    void testProcessEndpoint() throws Exception {
        // Arrange
        String input = "Test Input";
        String expectedResponse = "Processed: Test Input";
        when(myService.processData(input)).thenReturn(expectedResponse);

        // Act & Assert
        mockMvc.perform(get("/process").param("input", input))
                .andExpect(status().isOk())
                .andExpect(content().string(expectedResponse));
    }
}
```

#### **Explanation**:

* `@WebMvcTest(MyController.class)`: This annotation loads only the web layer (controller) for testing.
* `@Mock`: We mock the service dependency to isolate the controller from the actual service.
* `MockMvc`: It simulates HTTP requests and helps to test the controller's behavior.
* `mockMvc.perform(get("/process"))`: Simulates an HTTP GET request.
* `andExpect(status().isOk())`: Asserts that the HTTP status is `200 OK`.
* `andExpect(content().string(expectedResponse))`: Asserts that the content returned by the controller matches the expected result.

### **3. Mocking Dependencies with `@MockBean`**

In some cases, you want to mock a service or repository that is injected into your controller. You can do this using `@MockBean`, which allows you to mock Spring beans and inject them into the Spring context for testing.

Example using `@MockBean`:

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.test.context.junit.jupiter.SpringExtension;
import static org.mockito.Mockito.when;
import static org.junit.jupiter.api.Assertions.assertEquals;

@ExtendWith(SpringExtension.class)
@SpringBootTest
public class MyServiceIntegrationTest {

    @MockBean
    private MyService myService;  // Mocking the service

    @Test
    void testService() {
        // Arrange
        String input = "Test Input";
        String expectedOutput = "Processed: Test Input";
        when(myService.processData(input)).thenReturn(expectedOutput);

        // Act
        String result = myService.processData(input);

        // Assert
        assertEquals(expectedOutput, result);
    }
}
```

### **4. Testing with `@SpringBootTest`**

If you need to test the entire Spring context (e.g., the service, repository, and controller layers together), you can use `@SpringBootTest`. This annotation loads the full Spring context, which can be useful for integration testing.

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import static org.junit.jupiter.api.Assertions.*;

@SpringBootTest
public class MyServiceFullTest {

    @Autowired
    private MyService myService;

    @Test
    void testServiceMethod() {
        String input = "Test Input";
        String expectedOutput = "Processed: Test Input";
        String result = myService.processData(input);
        assertEquals(expectedOutput, result);
    }
}
```

### **5. Other Useful Testing Features**

* **`@DataJpaTest`**: This annotation is used for testing Spring Data JPA repositories. It configures an in-memory database and loads only the repository layer, making the tests fast and isolated.

* **`@MockBean`**: Useful for mocking beans in integration tests (i.e., replacing actual beans with mock objects).

* **`@TestConfiguration`**: You can use this to define configuration classes specifically for testing purposes, such as creating mock beans or configuring test-specific data sources.

### **Best Practices for Writing Unit Tests in Spring Boot**

1. **Isolate Dependencies**: Use mocks for dependencies (e.g., repositories or services) in unit tests.
2. **Test Public Methods**: Focus on testing public methods and avoid testing private methods.
3. **Write Meaningful Test Names**: Test method names should describe the behavior being tested.
4. **Use `@MockBean` for Integration Tests**: When testing the integration between layers, use `@MockBean` to mock external dependencies like services and repositories.
5. **Use Profiles for Test Configuration**: You can define custom configurations (like test-specific data sources) using `@TestConfiguration`.
6. **Avoid Tight Coupling**: Don’t make your tests depend on private methods or internal workings of your class.

### **Conclusion**

Writing unit tests in Spring Boot involves:

* Using **JUnit 5** for writing tests.
* Testing the **service layer** by mocking dependencies.
* Testing the **controller layer** using `@WebMvcTest`.
* Using **@SpringBootTest** for full integration tests.
* Leveraging **`@MockBean`** to mock Spring beans in integration tests.

By following these principles and making use of Spring Boot's testing annotations, you can write effective and maintainable tests for your application.

---

## 42. What is `@SpringBootTest` used for?

The `@SpringBootTest` annotation is used to write **integration tests** in Spring Boot. It loads the full Spring application context, allowing you to test how different components of your Spring Boot application interact with each other. This annotation is typically used when you need to test your application as a whole or test components that rely on the complete Spring context, such as repositories, services, and controllers together.

### **Key Features and Purpose of `@SpringBootTest`:**

1. **Loads Full Spring Context**:

    * When you annotate a test class with `@SpringBootTest`, Spring Boot loads the complete application context (all beans, configurations, and services) to provide a real Spring environment for the test.
    * This is useful for testing the behavior of your components when they interact with each other, ensuring that Spring’s dependency injection, configuration, and bean management work as expected.

2. **Integration Testing**:

    * `@SpringBootTest` is primarily used for integration testing, where you test how different parts of the application work together. For example, you can test how controllers interact with services and how services interact with repositories or databases.

3. **Embedded Server Support**:

    * By default, `@SpringBootTest` starts an embedded web server (like **Tomcat** or **Jetty**) if your application is a web application. This enables you to perform tests that simulate HTTP requests and responses to ensure that your web layer works correctly.
    * If you don't need an embedded server for testing, you can disable it by setting the `webEnvironment` property.

4. **Simulating Real-World Behavior**:

    * Unlike unit tests where dependencies are mocked, `@SpringBootTest` allows you to test real-world interactions in your application. For example, if you’re testing a REST API, you can make HTTP calls and assert the results without mocking the actual HTTP server.

5. **Customization**:

    * `@SpringBootTest` provides the flexibility to specify the web environment (e.g., whether you want to start the server or not) using the `webEnvironment` attribute.

### **Basic Usage Example**

#### **Example 1: Testing Service Layer**

Let’s say you have a simple service class and you want to test it using the full Spring context.

**Service Class Example**:

```java
@Service
public class MyService {
    public String processData(String input) {
        return "Processed: " + input;
    }
}
```

**Test Class Example**:

```java
import static org.junit.jupiter.api.Assertions.assertEquals;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
public class MyServiceTest {

    @Autowired
    private MyService myService;

    @Test
    void testProcessData() {
        String input = "Test Input";
        String expectedOutput = "Processed: Test Input";

        // Test the method in the real Spring context
        String result = myService.processData(input);

        assertEquals(expectedOutput, result);
    }
}
```

In this example:

* `@SpringBootTest` tells Spring Boot to load the entire application context.
* The service is autowired into the test class, and the test method verifies the behavior of the `processData` method.

#### **Example 2: Testing Controller with Web Environment**

If you want to test the controller layer along with the web environment (i.e., making HTTP requests), you can configure `@SpringBootTest` with the `webEnvironment` attribute.

**Controller Class Example**:

```java
@RestController
public class MyController {

    @Autowired
    private MyService myService;

    @GetMapping("/process")
    public String process(@RequestParam String input) {
        return myService.processData(input);
    }
}
```

**Test Class with Web Environment**:

```java
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.web.servlet.MockMvc;

@SpringBootTest(webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT)
public class MyControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Test
    void testProcessEndpoint() throws Exception {
        String input = "Test Input";
        String expectedResponse = "Processed: Test Input";

        mockMvc.perform(get("/process").param("input", input))
               .andExpect(status().isOk())
               .andExpect(content().string(expectedResponse));
    }
}
```

In this example:

* `webEnvironment = SpringBootTest.WebEnvironment.RANDOM_PORT` starts the embedded web server with a random port, and you can simulate HTTP requests.
* `MockMvc` is used to perform HTTP requests and check the responses.
* The test sends a GET request to `/process` and asserts that the response is the expected output.

### **Attributes of `@SpringBootTest`**

`@SpringBootTest` has a few useful attributes that allow for customization of how the test environment is set up:

* **`webEnvironment`**: This attribute defines how the web environment should be configured.

    * `SpringBootTest.WebEnvironment.MOCK`: The default setting, which does not start a real server but allows Spring to simulate a web environment.
    * `SpringBootTest.WebEnvironment.RANDOM_PORT`: Starts an embedded web server on a random port.
    * `SpringBootTest.WebEnvironment.DEFINED_PORT`: Starts an embedded web server on a specific port (usually 8080).
    * `SpringBootTest.WebEnvironment.NONE`: No web environment is started.

* **`properties`**: You can specify custom properties for the test, overriding application properties.

* **`classes`**: You can specify which classes to load, making the test more focused if needed.

### **Advantages of Using `@SpringBootTest`**

1. **Integration Testing**: It allows you to test your application in a real-world scenario by loading the complete application context, including database, services, controllers, and configurations.

2. **Embedded Server**: By default, it can start an embedded server, which is useful for testing RESTful web services or controllers that interact with an actual web server.

3. **Comprehensive Testing**: It can be used to test end-to-end behavior, where the focus is on verifying how different components of the system (e.g., database, services, controllers) work together.

### **When to Use `@SpringBootTest`**

* **End-to-End Integration Testing**: If you need to verify how different layers of your Spring Boot application (e.g., controllers, services, repositories) work together.
* **Testing Web Layer**: If you need to test the actual HTTP endpoints (e.g., REST controllers), use `@SpringBootTest` with the `webEnvironment` set to start a web server.
* **Realistic Tests**: Use `@SpringBootTest` when you want to simulate how the entire application would behave in a real deployment, including components such as databases, caches, or messaging queues.

### **Conclusion**

`@SpringBootTest` is a powerful annotation that helps you perform integration tests in a Spring Boot application by loading the full application context. It's most commonly used when you need to test the interactions between multiple layers of your application, such as controllers, services, and repositories. It can also simulate web requests using embedded servers, making it ideal for testing web applications.

---

## 43. What is the difference between `@WebMvcTest`, `@DataJpaTest`, and `@SpringBootTest`?

The annotations `@WebMvcTest`, `@DataJpaTest`, and `@SpringBootTest` in Spring Boot are used to write tests for different layers of a Spring application. Each of these annotations focuses on a different part of the application, allowing you to isolate and test specific components of your system more efficiently.

Here’s a detailed comparison of these three annotations:

### 1. **`@WebMvcTest`**: Test the Web Layer (Controller)

* **Purpose**: It is used to test the **web layer** of a Spring Boot application, specifically **controllers**. It helps to test the behavior of REST endpoints, making sure that the controller logic works as expected. It does not load the entire Spring context (e.g., repositories, services, etc.), but focuses only on the web layer.

* **What it does**:

    * Loads only the web-related beans (like `@Controller`, `@RestController`, `@ControllerAdvice`, etc.).
    * Does **not** load the entire Spring application context (no service or repository beans by default).
    * Allows the use of `MockMvc` to perform HTTP requests and test the responses.

* **When to Use**:

    * When you need to **test your controllers** in isolation, without loading the entire Spring context.
    * If you only care about testing the web layer’s functionality, like controller methods and HTTP request/response handling.

* **Example Usage**:

  ```java
  @WebMvcTest(MyController.class)
  public class MyControllerTest {

      @Autowired
      private MockMvc mockMvc;

      @MockBean
      private MyService myService;  // Mocking service layer

      @Test
      void testProcessEndpoint() throws Exception {
          // Arrange
          String input = "Test Input";
          String expectedResponse = "Processed: Test Input";
          when(myService.processData(input)).thenReturn(expectedResponse);

          // Act & Assert
          mockMvc.perform(get("/process").param("input", input))
                 .andExpect(status().isOk())
                 .andExpect(content().string(expectedResponse));
      }
  }
  ```

### 2. **`@DataJpaTest`**: Test the Data Layer (JPA Repositories)

* **Purpose**: It is used for testing **JPA repositories** and the persistence layer. It is a specialized version of `@SpringBootTest` that only focuses on the **data layer**, configuring an in-memory database (H2 by default) to perform database-related tests.

* **What it does**:

    * Configures only the data-related beans, such as `@Entity`, `@Repository`, and related configurations.
    * **Does not** load controllers, services, or other components outside of the persistence layer.
    * **Starts an embedded in-memory database (H2)** for testing purposes, so your tests do not need to rely on an external database.
    * Provides support for **transactions** by rolling back each test method to maintain test isolation.

* **When to Use**:

    * When you need to test **JPA repositories**, database interactions, and CRUD operations.
    * Useful for testing the behavior of repositories in isolation from the rest of the application.

* **Example Usage**:

  ```java
  @DataJpaTest
  public class MyRepositoryTest {

      @Autowired
      private MyRepository myRepository;

      @Test
      void testRepositorySave() {
          // Arrange
          MyEntity entity = new MyEntity("Test");
          
          // Act
          myRepository.save(entity);
          
          // Assert
          assertThat(myRepository.findByName("Test")).isNotNull();
      }
  }
  ```

### 3. **`@SpringBootTest`**: Full Integration Testing (Loads Full Application Context)

* **Purpose**: It is used for **integration testing** where the **entire Spring application context** is loaded. This is the most comprehensive testing annotation because it loads all beans, services, repositories, and controllers, simulating the real application environment.

* **What it does**:

    * Loads the entire Spring context, including all **beans** (services, repositories, controllers, configurations, etc.).
    * Can be used with or without an embedded server, depending on the configuration (`webEnvironment` attribute).
    * Useful for **end-to-end testing** when you need to test how multiple layers of the application (like controllers, services, and repositories) interact with each other.

* **When to Use**:

    * When you want to perform **full integration tests**, verifying that all layers of the application work together as expected.
    * Ideal for testing multiple layers of the application together (e.g., controllers, services, repositories).

* **Example Usage**:

  ```java
  @SpringBootTest
  public class MyServiceIntegrationTest {

      @Autowired
      private MyService myService;

      @Test
      void testServiceMethod() {
          // Arrange
          String input = "Test Input";
          String expectedOutput = "Processed: Test Input";
          
          // Act
          String result = myService.processData(input);
          
          // Assert
          assertEquals(expectedOutput, result);
      }
  }
  ```

### **Key Differences Between `@WebMvcTest`, `@DataJpaTest`, and `@SpringBootTest`**

| **Feature**                       | **`@WebMvcTest`**                                                      | **`@DataJpaTest`**                                          | **`@SpringBootTest`**                                              |
| --------------------------------- | ---------------------------------------------------------------------- | ----------------------------------------------------------- | ------------------------------------------------------------------ |
| **Scope**                         | Focuses on the web layer (controllers)                                 | Focuses on the data layer (JPA repositories)                | Tests the entire Spring Boot application context                   |
| **Loaded Context**                | Only beans related to web layer (controllers, `@RestController`, etc.) | Only beans related to persistence (repositories, `@Entity`) | Loads the entire application context (beans from all layers)       |
| **Use Case**                      | Testing controllers, request/response behavior                         | Testing repositories and database operations                | Full integration testing (controllers, services, repositories)     |
| **Embedded Database**             | No (unless configured separately)                                      | Yes (embedded in-memory database like H2)                   | No (unless configured)                                             |
| **Mocking Services/Repositories** | Can use `@MockBean` to mock services/repositories                      | Does not need mocking; focuses on repository behavior       | Can use `@MockBean` for mock beans in tests                        |
| **Web Server**                    | No embedded web server (unless manually configured)                    | No embedded web server                                      | Starts an embedded web server (if required)                        |
| **Typical Test Tools**            | `MockMvc` for simulating HTTP requests                                 | JPA repository testing                                      | Can use `TestRestTemplate`, `MockMvc`, or standard service testing |

### **When to Use Each Annotation**:

* **Use `@WebMvcTest`** when you want to test the web layer of your application, i.e., the controllers and HTTP request/response flow.
* **Use `@DataJpaTest`** when you need to focus on testing the database layer, i.e., your JPA repositories, with an in-memory database.
* **Use `@SpringBootTest`** when you need to perform full integration testing, including all layers of your application (controllers, services, repositories), and simulate real-world application behavior.

### **Summary**:

* **`@WebMvcTest`**: Best for testing the web layer (controllers).
* **`@DataJpaTest`**: Best for testing the persistence layer (JPA repositories).
* **`@SpringBootTest`**: Best for full integration testing, where you want to load the entire Spring Boot context and test multiple components together.

---

## 44. What is `@MockBean`?

`@MockBean` is an annotation provided by **Spring Boot** used to create and inject **mock** beans into the Spring application context for the purpose of **unit testing** and **integration testing**. It is commonly used in test classes to mock dependencies that are injected into the class under test, such as service or repository beans. By using `@MockBean`, you can replace the actual bean with a mock, allowing you to isolate the class under test and control the behavior of its dependencies.

### **Key Features of `@MockBean`:**

1. **Mocks Spring Beans**: It is used to mock a Spring bean in the **application context**. This is useful when you want to isolate the class being tested by providing a mock version of a dependency.

2. **Automatic Injection**: The mock bean is automatically injected into the Spring application context and into the class under test, just like the real bean would be, so you don’t have to manually wire the mock.

3. **Mockito Integration**: `@MockBean` integrates with **Mockito**, so you can specify the behavior of the mocked bean (using methods like `when().thenReturn()` or `doReturn().when()`) and make assertions based on that mocked behavior.

4. **Test-Specific Mocking**: It allows you to override specific parts of the application context during testing, without modifying the actual application configuration or bean definitions.

### **When to Use `@MockBean`**:

* When you need to **mock a dependency** (e.g., service, repository) in a Spring-managed bean.
* When you want to **isolate the unit under test** and control the behavior of external dependencies (like database interactions, web service calls, etc.).
* In **integration tests** to mock out certain beans while still testing the integration of other parts of the application.

### **Example Usage of `@MockBean`**:

Let’s assume we have a service that depends on a repository and we want to test the service in isolation, mocking the repository.

#### **Example 1: Mocking a Repository in a Service Test**

**Service Class**:

```java
@Service
public class MyService {
    @Autowired
    private MyRepository myRepository;

    public String getProcessedData(String input) {
        return "Processed: " + myRepository.findData(input);
    }
}
```

**Repository Interface**:

```java
public interface MyRepository extends JpaRepository<MyEntity, Long> {
    String findData(String input);
}
```

**Test Class**:

```java
import static org.mockito.Mockito.when;
import static org.junit.jupiter.api.Assertions.assertEquals;
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.mock.mockito.MockBean;

@SpringBootTest
public class MyServiceTest {

    @Autowired
    private MyService myService;

    @MockBean
    private MyRepository myRepository;

    @Test
    void testGetProcessedData() {
        // Arrange
        String input = "Test";
        String expectedData = "Mocked Data";
        when(myRepository.findData(input)).thenReturn(expectedData);

        // Act
        String result = myService.getProcessedData(input);

        // Assert
        assertEquals("Processed: " + expectedData, result);
    }
}
```

### **Explanation**:

1. **`@MockBean`**:

    * `@MockBean` is used to mock `MyRepository` in the test. This mock will be automatically injected into the `MyService` instance in the Spring context.

2. **Mock Behavior**:

    * `when(myRepository.findData(input)).thenReturn(expectedData)` tells Mockito to return `expectedData` whenever the `findData()` method is called with the specified `input`.

3. **Test Logic**:

    * The service’s `getProcessedData()` method is tested, but the actual `MyRepository` bean is mocked. This allows us to control what `findData()` returns and focus on testing the service logic.

### **When to Use `@MockBean` in Integration Tests**:

* **Mocking external services**: If your service interacts with an external system (e.g., a remote API or a database) and you want to avoid actual calls during testing, you can mock those services using `@MockBean`.

* **Partial mocking of beans**: If you need to mock certain methods of a bean but still want to use the rest of the actual bean’s behavior, `@MockBean` is useful.

### **Differences Between `@MockBean` and `@Mock`**:

* **`@MockBean`**:

    * It works at the **Spring context level** by creating a mock and automatically injecting it into the Spring application context.
    * Used when testing with Spring Boot applications to replace specific beans in the context.
* **`@Mock` (Mockito)**:

    * It works at the unit test level and does not automatically integrate with the Spring context. You typically use `@Mock` when you are manually creating mock objects and injecting them into your test using `@InjectMocks` or other mechanisms.

### **Summary**:

* **`@MockBean`** is a Spring Boot-specific annotation used in integration tests to mock beans in the application context. It is useful for isolating the unit under test and controlling the behavior of its dependencies.
* It integrates with **Mockito** to define the mock's behavior and is particularly useful for replacing service or repository beans in tests, ensuring that your tests remain focused on the functionality of the class under test.

---

## 45. How do you test REST controllers in Spring Boot?

Testing REST controllers in **Spring Boot** is a common requirement to ensure that the RESTful APIs behave as expected. To effectively test REST controllers, we often use a combination of **JUnit** and **Spring Test** tools like **`MockMvc`**, which allows simulating HTTP requests and verifying the responses without starting up a full HTTP server.

Here’s how you can test REST controllers in Spring Boot:

### **Steps to Test REST Controllers in Spring Boot**

#### 1. **Set up the Spring Boot Test Context**:

You typically use the `@WebMvcTest` annotation to test only the **web layer** (controllers) in isolation, or you can use `@SpringBootTest` for a broader integration test that loads the full application context.

* **`@WebMvcTest`**: If you want to test the controller independently without starting the full Spring Boot application.
* **`@SpringBootTest`**: If you need to load the full application context, including controllers, services, and repositories.

#### 2. **Use `MockMvc` to Simulate HTTP Requests**:

`MockMvc` allows you to perform HTTP requests against the controllers and verify the status, response content, and other properties.

#### 3. **Write Unit Tests**:

* Create test methods for each endpoint you want to test.
* Use assertions to verify the status, headers, and body of the response.

### **Example: Testing a REST Controller in Spring Boot**

#### **1. Create the REST Controller**

Let’s say you have a simple `UserController` that provides an API to fetch user details.

```java
@RestController
@RequestMapping("/api/users")
public class UserController {

    @Autowired
    private UserService userService;

    @GetMapping("/{id}")
    public ResponseEntity<User> getUser(@PathVariable Long id) {
        User user = userService.getUserById(id);
        if (user == null) {
            return ResponseEntity.status(HttpStatus.NOT_FOUND).build();
        }
        return ResponseEntity.ok(user);
    }
}
```

#### **2. Write a Test for the Controller**

To test this controller, we will use `@WebMvcTest` and `MockMvc` to simulate HTTP requests.

```java
import static org.mockito.Mockito.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.mock.mockito.MockBean;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;
import org.springframework.http.MediaType;

@SpringBootTest
public class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;  // Automatically injected MockMvc instance

    @MockBean
    private UserService userService;  // Mock the service layer

    private User user;

    @BeforeEach
    public void setUp() {
        // Create a sample user object
        user = new User(1L, "John", "Doe");
    }

    @Test
    void testGetUser_Success() throws Exception {
        // Arrange: Mock the service method
        when(userService.getUserById(1L)).thenReturn(user);

        // Act & Assert: Perform GET request and validate response
        mockMvc.perform(get("/api/users/{id}", 1L)
                .accept(MediaType.APPLICATION_JSON))
                .andExpect(status().isOk())  // Expect HTTP 200 OK status
                .andExpect(jsonPath("$.id").value(1))  // Validate the id in the response
                .andExpect(jsonPath("$.firstName").value("John"))  // Validate firstName in the response
                .andExpect(jsonPath("$.lastName").value("Doe"));  // Validate lastName in the response
    }

    @Test
    void testGetUser_NotFound() throws Exception {
        // Arrange: Mock the service method to return null
        when(userService.getUserById(1L)).thenReturn(null);

        // Act & Assert: Perform GET request and expect 404 Not Found
        mockMvc.perform(get("/api/users/{id}", 1L)
                .accept(MediaType.APPLICATION_JSON))
                .andExpect(status().isNotFound());  // Expect HTTP 404 Not Found status
    }
}
```

### **Explanation of Key Parts**:

1. **`@WebMvcTest`**:

    * `@WebMvcTest(UserController.class)` is used to test only the **web layer** (controllers). This annotation will load the controller beans but not other beans such as services or repositories.
    * `@MockBean` is used to mock the `UserService` since the service layer is external to the controller in the test.

2. **`MockMvc`**:

    * `MockMvc` is automatically injected by Spring when using `@WebMvcTest` or `@SpringBootTest`. It allows us to simulate HTTP requests and responses.
    * `mockMvc.perform(get("/api/users/{id}", 1L))`: Simulates an HTTP `GET` request to the `/api/users/{id}` endpoint.
    * `andExpect(status().isOk())`: Verifies that the response status is HTTP 200 (OK).
    * `andExpect(jsonPath("$.id").value(1))`: Verifies the content of the JSON response, specifically that the `id` field is 1.
    * `andExpect(status().isNotFound())`: Verifies that the response status is HTTP 404 (Not Found) when the user is not found.

3. **`@MockBean`**:

    * `@MockBean` is used to mock the `UserService` bean. This ensures that the actual service layer is not called during the test. Instead, you control the service's behavior with Mockito’s `when().thenReturn()`.

4. **`@BeforeEach`**:

    * `@BeforeEach` is used to initialize the data (such as the `User` object) before each test method runs.

### **Other Testing Techniques**:

* **`@SpringBootTest`**: You can use `@SpringBootTest` if you want to load the full Spring Boot context (including services and repositories) for integration testing.
* **`@MockMvc` with `@SpringBootTest`**: You can use `@SpringBootTest` along with `MockMvc` to test the controller and interact with the entire application context if needed.

### **Example of Testing with `@SpringBootTest`**:

If you want to test the entire Spring Boot context, including services and repositories, use `@SpringBootTest`:

```java
@SpringBootTest
public class UserControllerIntegrationTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService;

    @Test
    void testGetUser_Success() throws Exception {
        User user = new User(1L, "John", "Doe");
        when(userService.getUserById(1L)).thenReturn(user);

        mockMvc.perform(get("/api/users/{id}", 1L))
                .andExpect(status().isOk())
                .andExpect(jsonPath("$.id").value(1))
                .andExpect(jsonPath("$.firstName").value("John"))
                .andExpect(jsonPath("$.lastName").value("Doe"));
    }
}
```

### **Conclusion**:

Testing REST controllers in Spring Boot is mainly done using **`MockMvc`**, which allows you to simulate HTTP requests and verify the responses without the need for a running server.

* Use `@WebMvcTest` for testing controllers in isolation, mocking service dependencies with `@MockBean`.
* Use `@SpringBootTest` if you need a full integration test of your application where the entire context is loaded.

By using `MockMvc` and appropriate annotations like `@WebMvcTest` or `@SpringBootTest`, you can efficiently test your Spring Boot REST controllers.

---

## 46. How do you test services with dependencies?

Testing services with dependencies in Spring Boot involves isolating the service layer while ensuring its dependencies (such as repositories, other services, etc.) are either mocked or injected with test-specific behavior. This ensures that you can test the logic of the service independently of the actual dependencies.

### **Steps to Test Services with Dependencies in Spring Boot:**

1. **Use of Mocks for Dependencies**: For any dependency injected into the service (e.g., repositories, external APIs, other services), you will typically mock those dependencies using **Mockito** to control their behavior.

2. **Use of `@MockBean` or `@Mock`**: If you're using Spring Boot’s testing framework, you can use `@MockBean` to mock beans that are part of the Spring context. Alternatively, you can use `@Mock` when you don’t need the Spring context (e.g., with JUnit tests).

3. **Testing Service Logic**: After mocking the dependencies, you can focus on testing the service methods. You verify if the service behaves correctly by using assertions on the results of the method calls.

4. **Use `@InjectMocks` to inject mocks into the service** (if using Mockito in a JUnit-based test).

### **Example 1: Test Service with Dependencies Using `@MockBean`**

#### **1. Service Layer**

Let’s assume you have a service class `UserService` that depends on a repository (`UserRepository`):

```java
@Service
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public User getUserById(Long id) {
        return userRepository.findById(id).orElse(null);
    }

    public User saveUser(User user) {
        return userRepository.save(user);
    }
}
```

#### **2. Writing the Test Class**

To test this service, you will mock the `UserRepository` and inject the mock into the `UserService`.

```java
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.mock.mockito.MockBean;

@SpringBootTest
public class UserServiceTest {

    @Autowired
    private UserService userService;  // Service to be tested

    @MockBean
    private UserRepository userRepository;  // Mocking the repository

    private User user;

    @BeforeEach
    public void setUp() {
        // Setup user data
        user = new User(1L, "John", "Doe");
    }

    @Test
    void testGetUserById_Success() {
        // Arrange: Mock the repository behavior
        when(userRepository.findById(1L)).thenReturn(Optional.of(user));

        // Act: Call the service method
        User result = userService.getUserById(1L);

        // Assert: Verify the result
        assertNotNull(result);
        assertEquals("John", result.getFirstName());
        assertEquals("Doe", result.getLastName());
    }

    @Test
    void testGetUserById_NotFound() {
        // Arrange: Mock the repository to return an empty Optional
        when(userRepository.findById(1L)).thenReturn(Optional.empty());

        // Act: Call the service method
        User result = userService.getUserById(1L);

        // Assert: Verify that the result is null (not found)
        assertNull(result);
    }

    @Test
    void testSaveUser() {
        // Arrange: Mock the repository to return the saved user
        when(userRepository.save(any(User.class))).thenReturn(user);

        // Act: Call the service method
        User result = userService.saveUser(user);

        // Assert: Verify that the saved user matches the expected one
        assertNotNull(result);
        assertEquals("John", result.getFirstName());
        assertEquals("Doe", result.getLastName());
    }
}
```

### **Explanation of the Test**:

1. **`@MockBean`**:

    * `@MockBean` is used to mock the `UserRepository`. This ensures that the real repository isn’t called during the test, and we can control its behavior.
    * This also ensures that the mocked `UserRepository` is injected into the `UserService` in the Spring application context.

2. **Mockito Stubbing**:

    * `when(userRepository.findById(1L)).thenReturn(Optional.of(user))`: This tells Mockito to return a mocked `User` object when `findById` is called with the argument `1L`.
    * `when(userRepository.save(any(User.class))).thenReturn(user)`: This mocks the `save` method of `userRepository` to return the `user` object when any `User` is passed.

3. **Assertions**:

    * We assert that the returned `User` object is not `null` and that its properties match the expected values.
    * The second test verifies that when the user is not found, the service correctly returns `null`.

### **Example 2: Using `@Mock` and `@InjectMocks` for Unit Testing**

If you're using Mockito in a more traditional JUnit test, you can use `@Mock` for dependencies and `@InjectMocks` to inject those mocks into the service.

```java
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Test;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

@ExtendWith(MockitoExtension.class)
public class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;  // The service being tested

    private User user;

    @BeforeEach
    public void setUp() {
        user = new User(1L, "John", "Doe");
    }

    @Test
    void testGetUserById_Success() {
        when(userRepository.findById(1L)).thenReturn(Optional.of(user));

        User result = userService.getUserById(1L);

        assertNotNull(result);
        assertEquals("John", result.getFirstName());
        assertEquals("Doe", result.getLastName());
    }
}
```

### **Key Annotations**:

* **`@MockBean`**: Used in Spring Boot tests to mock beans in the Spring application context, typically in integration tests using `@SpringBootTest`.
* **`@Mock`**: Used with Mockito to create mock objects for dependencies in unit tests.
* **`@InjectMocks`**: Tells Mockito to inject mocked dependencies into the service class automatically.

### **Testing Strategies**:

1. **Unit Testing**:

    * Mock all dependencies of the service.
    * Use **Mockito** or **`@MockBean`** to control and simulate the behavior of the dependencies.
    * Focus only on testing the logic within the service, isolating it from external influences like databases or third-party services.

2. **Integration Testing**:

    * Test the interaction between the service and real or partially mocked dependencies.
    * Use `@SpringBootTest` to load the full Spring application context and `@MockBean` to mock dependencies.
    * You may want to test the service in combination with its repository (or mock the repository to simulate different database states).

### **Summary**:

* **Mock dependencies**: Use `@MockBean` or `@Mock` to mock dependencies like repositories or services.
* **Inject mocks into services**: Use `@InjectMocks` (in traditional JUnit tests) or Spring’s DI to inject mocks into your service class.
* **Verify behavior**: Use Mockito’s `when().thenReturn()` to control the behavior of mocked dependencies and verify the service’s behavior with assertions.

By following these practices, you can test services with dependencies efficiently and in isolation, ensuring that the service logic works correctly without relying on real database or external service calls.

---

## 47. How do you test JPA repositories?

Testing JPA repositories in Spring Boot is an essential part of ensuring that your data access logic works correctly, especially when using **Spring Data JPA**. You can test repositories in two ways:

1. **Unit Testing**: Mocking the JPA repository to isolate it from actual database interaction.
2. **Integration Testing**: Using an actual in-memory database (like H2) to run the repository code against a real database, but in a controlled environment.

In most cases, **integration testing** is preferred for repository testing to ensure that the interaction with the database works correctly and that the JPA queries are functioning as expected.

### **Testing JPA Repositories with Spring Boot**

1. **Set Up the Test Configuration**: Use `@DataJpaTest` for testing JPA repositories in isolation. This annotation is designed to test Spring Data JPA repositories and automatically configures an in-memory database (such as H2) for testing.

2. **Test Data**: Use test data within the repository methods to verify that the repository interacts with the database correctly.

### **Step-by-Step Example of Testing JPA Repositories**

Let's go through an example of testing a simple repository in Spring Boot using an in-memory H2 database.

#### 1. **Define the Entity and Repository**

Let's define a simple entity called `User` and a repository called `UserRepository`.

**`User` Entity**:

```java
import javax.persistence.Entity;
import javax.persistence.Id;

@Entity
public class User {

    @Id
    private Long id;
    private String firstName;
    private String lastName;

    // Getters and Setters
    public Long getId() {
        return id;
    }

    public void setId(Long id) {
        this.id = id;
    }

    public String getFirstName() {
        return firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

    public String getLastName() {
        return lastName;
    }

    public void setLastName(String lastName) {
        this.lastName = lastName;
    }
}
```

**`UserRepository` Interface**:

```java
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository<User, Long> {
    // Custom query methods can be added if needed
    User findByFirstName(String firstName);
}
```

#### 2. **Write the Test Class**

Now, let's write a test class using `@DataJpaTest` to test the repository methods.

**`UserRepositoryTest` Class**:

```java
import static org.junit.jupiter.api.Assertions.*;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;

@DataJpaTest  // Only loads repository beans and an in-memory database (H2 by default)
public class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    public void testSaveAndFindUserById() {
        // Arrange: Create a new user entity
        User user = new User();
        user.setId(1L);
        user.setFirstName("John");
        user.setLastName("Doe");

        // Act: Save the user to the repository
        userRepository.save(user);

        // Assert: Retrieve the user by ID and validate
        User retrievedUser = userRepository.findById(1L).orElse(null);
        assertNotNull(retrievedUser);
        assertEquals("John", retrievedUser.getFirstName());
        assertEquals("Doe", retrievedUser.getLastName());
    }

    @Test
    public void testFindUserByFirstName() {
        // Arrange: Create a user entity and save it
        User user = new User();
        user.setId(2L);
        user.setFirstName("Jane");
        user.setLastName("Doe");
        userRepository.save(user);

        // Act: Find the user by first name
        User retrievedUser = userRepository.findByFirstName("Jane");

        // Assert: Verify the user's first name and last name
        assertNotNull(retrievedUser);
        assertEquals("Jane", retrievedUser.getFirstName());
        assertEquals("Doe", retrievedUser.getLastName());
    }
}
```

### **Explanation of Key Annotations and Concepts**:

1. **`@DataJpaTest`**:

    * This annotation is used to test JPA repositories in isolation. It automatically configures an in-memory database (usually H2) and only scans the relevant JPA components (like repositories).
    * It will **not** load the entire Spring context (like controllers or services), making it faster for testing the repository layer.

2. **`@Autowired`**:

    * This is used to inject the `UserRepository` bean into the test class so that you can call its methods directly.

3. **Test Data Setup**:

    * You create instances of the `User` entity and save them to the database using the repository's `save()` method. The repository’s methods like `findById()` or `findByFirstName()` are then tested to ensure that the repository performs correctly.

4. **Assertions**:

    * `assertNotNull()` is used to ensure that the user is found in the database.
    * `assertEquals()` is used to verify that the properties of the retrieved user match the expected values.

### **Running the Tests**:

* The `@DataJpaTest` annotation automatically configures an in-memory database (H2) for running the tests, so you don’t need to set up an actual database.
* Each test method is run in a clean transaction, which is rolled back after the test completes to ensure a fresh state for each test.

### **Additional Considerations**:

1. **Testing Custom Queries**:

    * If you have custom queries defined in the repository (using the `@Query` annotation or derived query methods), you can test them similarly. The repository will automatically execute the custom queries on the in-memory database during the tests.

2. **Test Data Setup**:

    * You can use **`@BeforeEach`** or **`@BeforeAll`** to set up common test data for your repository tests if needed.

3. **Integration Tests**:

    * **`@SpringBootTest`** can be used if you want to test the repository in the context of the entire Spring application. However, for simple repository tests, `@DataJpaTest` is usually preferred as it is faster and focuses only on the JPA layer.

4. **Transactional Tests**:

    * The tests in `@DataJpaTest` are **transactional**, meaning that each test is wrapped in a transaction that is rolled back after the test finishes. This ensures that the test database is not polluted by test data.

### **Example with Custom Queries**:

If you have a custom query like this in the `UserRepository`:

```java
public interface UserRepository extends JpaRepository<User, Long> {
    @Query("SELECT u FROM User u WHERE u.firstName = :firstName")
    User findUserByFirstNameCustom(@Param("firstName") String firstName);
}
```

You can test it in a similar manner:

```java
@Test
public void testFindUserByFirstNameCustom() {
    // Arrange
    User user = new User();
    user.setId(1L);
    user.setFirstName("John");
    user.setLastName("Doe");
    userRepository.save(user);

    // Act
    User retrievedUser = userRepository.findUserByFirstNameCustom("John");

    // Assert
    assertNotNull(retrievedUser);
    assertEquals("John", retrievedUser.getFirstName());
    assertEquals("Doe", retrievedUser.getLastName());
}
```

### **Summary**:

* **Unit Testing**: Use `@MockBean` and mock the repository if testing in isolation (typically used in service layer tests).
* **Integration Testing**: Use `@DataJpaTest` for testing JPA repositories in an in-memory database (H2) for isolated database interaction tests.
* **Test Assertions**: Verify the behavior of the repository methods by performing CRUD operations and validating the results with assertions like `assertEquals()` and `assertNotNull()`.

By following these practices, you ensure that your repository interactions with the database are working correctly.

---

## 48. What is `@DataJpaTest` and how does it work?

`@DataJpaTest` is a specialized annotation provided by **Spring Boot** for **testing the persistence layer**, especially **Spring Data JPA repositories**. It configures only the components relevant for JPA testing and uses an **embedded in-memory database** by default (like H2).

---

### 🔍 **What `@DataJpaTest` Does:**

When you annotate a test class with `@DataJpaTest`, Spring Boot:

* **Loads only JPA-related components**:

    * `@Entity` classes (your models)
    * `@Repository` beans (Spring Data repositories)
* **Disables full application context loading**, which makes the test lightweight and fast.
* **Sets up an in-memory database** (like H2, HSQL, or Derby) unless you configure otherwise.
* **Rolls back transactions** after each test automatically (to avoid test data leakage).
* Configures:

    * `EntityManager`
    * `DataSource`
    * `JdbcTemplate`
    * `TestEntityManager` (a utility to help with testing JPA)

---

### ✅ **When to Use It:**

Use `@DataJpaTest` when you want to:

* Test **Spring Data repository methods** (e.g., `findById()`, `findByEmail()`)
* Verify the correctness of **custom JPQL/native queries**
* Validate **JPA mappings and relationships** (e.g., `@OneToMany`, `@JoinColumn`)
* Run fast **integration tests** without bootstrapping the entire Spring context

---

### 🧪 Example Usage

#### 👇 Example Entity

```java
@Entity
public class User {
    @Id
    private Long id;
    private String name;

    // Constructors, Getters, Setters
}
```

#### 👇 Repository Interface

```java
public interface UserRepository extends JpaRepository<User, Long> {
    User findByName(String name);
}
```

#### 👇 Test Class Using `@DataJpaTest`

```java
@DataJpaTest
public class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    void testFindByName() {
        // Arrange
        User user = new User();
        user.setId(1L);
        user.setName("Alice");
        userRepository.save(user);

        // Act
        User found = userRepository.findByName("Alice");

        // Assert
        assertNotNull(found);
        assertEquals("Alice", found.getName());
    }
}
```

---

### ⚙️ Optional Configuration

You can customize the behavior with annotations:

* `@AutoConfigureTestDatabase(replace = Replace.NONE)`
  → To use your **real test database** instead of the in-memory one.

* `@Import(SomeConfig.class)`
  → To include custom beans or configuration classes.

---

### 📝 Summary

| Feature           | Description                                                             |
| ----------------- | ----------------------------------------------------------------------- |
| Purpose           | To test Spring Data JPA repositories                                    |
| Loads             | Only JPA-related beans (`@Entity`, `@Repository`)                       |
| Database          | In-memory by default (H2), rollbacks after each test                    |
| Fast?             | Yes, since it avoids full context startup                               |
| Typical Use Cases | Repository method testing, JPA query testing, entity mapping validation |

---

## 49. How do you mock external APIs or RestTemplate in Spring Boot?

Mocking external APIs (like REST endpoints) in Spring Boot is essential when writing **unit tests** that depend on `RestTemplate`, `WebClient`, or other HTTP clients. You want to **simulate the behavior** of the external API **without actually making HTTP calls**.

---

### ✅ **Ways to Mock External APIs in Spring Boot**

#### 1. **Mocking `RestTemplate` using Mockito**

If your service uses `RestTemplate`, you can mock it using `@Mock` or `@MockBean`.

---

### 🔧 **Example: Mocking `RestTemplate` in a Unit Test**

#### 🧩 Service Class

```java
@Service
public class WeatherService {

    @Autowired
    private RestTemplate restTemplate;

    public String getWeather(String city) {
        String url = "https://api.weather.com/v1/" + city;
        return restTemplate.getForObject(url, String.class);
    }
}
```

#### 🧪 Test Class

```java
@ExtendWith(MockitoExtension.class)
public class WeatherServiceTest {

    @InjectMocks
    private WeatherService weatherService;

    @Mock
    private RestTemplate restTemplate;

    @Test
    void testGetWeather() {
        String mockResponse = "Sunny";

        // Mocking RestTemplate
        Mockito.when(restTemplate.getForObject(
                ArgumentMatchers.anyString(),
                ArgumentMatchers.eq(String.class)))
               .thenReturn(mockResponse);

        String result = weatherService.getWeather("London");
        assertEquals("Sunny", result);
    }
}
```

---

### ✅ **Option 2: Using `@MockBean` in Spring Boot Tests**

If you're using `@SpringBootTest`, mock the `RestTemplate` bean like this:

```java
@SpringBootTest
public class WeatherServiceIntegrationTest {

    @Autowired
    private WeatherService weatherService;

    @MockBean
    private RestTemplate restTemplate;

    @Test
    void testWeatherService() {
        Mockito.when(restTemplate.getForObject(Mockito.anyString(), eq(String.class)))
               .thenReturn("Rainy");

        String result = weatherService.getWeather("Paris");
        assertEquals("Rainy", result);
    }
}
```

---

### ✅ **Option 3: Use `MockRestServiceServer` (for Integration-Style Tests)**

If you still want to test the actual HTTP call logic but **avoid real API calls**, use `MockRestServiceServer`.

```java
@RunWith(SpringRunner.class)
@SpringBootTest
public class WeatherServiceRestTest {

    @Autowired
    private RestTemplate restTemplate;

    @Autowired
    private WeatherService weatherService;

    private MockRestServiceServer mockServer;

    @BeforeEach
    public void init() {
        mockServer = MockRestServiceServer.createServer(restTemplate);
    }

    @Test
    public void testMockServer() {
        mockServer.expect(requestTo("https://api.weather.com/v1/London"))
                  .andRespond(withSuccess("Cloudy", MediaType.TEXT_PLAIN));

        String weather = weatherService.getWeather("London");

        assertEquals("Cloudy", weather);
        mockServer.verify();
    }
}
```

---

### ✅ **Option 4: Mocking `WebClient`**

If your service uses `WebClient`, use a library like [`reactor-test`](https://projectreactor.io/docs/test/release/api/) or `WebClient.Builder` with a mock exchange function.

---

### 🔍 Summary Table

| Approach                      | Tool/Annotation                               | Use Case                                       |
| ----------------------------- | --------------------------------------------- | ---------------------------------------------- |
| Unit test with `RestTemplate` | `@Mock` or `Mockito.mock()`                   | Lightweight unit tests                         |
| Spring Boot test              | `@MockBean`                                   | Full Spring context test                       |
| HTTP call simulation          | `MockRestServiceServer`                       | Test REST call logic without real HTTP request |
| `WebClient` support           | `WebClient.Builder`, `ExchangeFunction` mocks | For reactive/non-blocking clients              |

---

## 50. How do you test configuration properties?

Testing configuration properties in Spring Boot is important to ensure that custom values from `application.properties` or `application.yml` are **correctly bound** to your configuration classes.

---

### ✅ **Typical Approach to Testing Configuration Properties**

1. Use a **`@ConfigurationProperties`** class to bind external config.
2. Write a test using:

    * `@SpringBootTest` or `@TestConfiguration`
    * Possibly a **custom properties file** or `@TestPropertySource`
3. Use assertions to verify the bound values.

---

### 🔧 **Step-by-Step Example**

#### 1. **Define a Configuration Properties Class**

```java
@Component
@ConfigurationProperties(prefix = "app")
public class AppProperties {
    private String name;
    private int timeout;

    // Getters and Setters
    public String getName() { return name; }
    public void setName(String name) { this.name = name; }

    public int getTimeout() { return timeout; }
    public void setTimeout(int timeout) { this.timeout = timeout; }
}
```

#### 2. **Add Properties to `application.yml` or `application.properties`**

```properties
# application.properties
app.name=MyApp
app.timeout=30
```

---

### 🧪 3. **Test the Binding with `@SpringBootTest`**

```java
@SpringBootTest
@EnableConfigurationProperties(AppProperties.class)
@TestPropertySource(properties = {
    "app.name=TestApp",
    "app.timeout=45"
})
public class AppPropertiesTest {

    @Autowired
    private AppProperties appProperties;

    @Test
    void testAppPropertiesBinding() {
        assertEquals("TestApp", appProperties.getName());
        assertEquals(45, appProperties.getTimeout());
    }
}
```

---

### 🛠️ Alternative: `@ConfigurationPropertiesScan` in Test

If your config class is not annotated with `@Component`, you can scan it in the test:

```java
@SpringBootTest
@ConfigurationPropertiesScan("com.example.config")
public class AppPropertiesTest {
    // ...
}
```

---

### ✅ Key Annotations Explained

| Annotation                       | Purpose                                                               |
| -------------------------------- | --------------------------------------------------------------------- |
| `@ConfigurationProperties`       | Binds external config to a POJO                                       |
| `@EnableConfigurationProperties` | Enables binding in the test context                                   |
| `@TestPropertySource`            | Overrides properties specifically for testing                         |
| `@SpringBootTest`                | Loads Spring context including config classes                         |
| `@ConfigurationPropertiesScan`   | Scans and registers config classes (if not annotated as `@Component`) |

---

### 🔍 Summary

* Create a POJO with `@ConfigurationProperties`
* Use `@EnableConfigurationProperties` or `@SpringBootTest`
* Use `@TestPropertySource` to simulate different config environments
* Use assertions to verify values are loaded and parsed correctly

---

## 51. How do you test application events?

Testing **application events** in Spring Boot ensures that your event publishing and listening mechanisms are working correctly. This is useful when you're using Spring’s `ApplicationEventPublisher` and event listeners (`@EventListener` or subclassing `ApplicationListener`).

---

## ✅ 1. **What Are Application Events?**

Spring supports a publish-subscribe mechanism where:

* An **event** is an object you define (extending `ApplicationEvent` is optional in modern Spring).
* An **event publisher** sends the event using `ApplicationEventPublisher`.
* An **event listener** handles the event using `@EventListener` or `ApplicationListener`.

---

## ✅ 2. **Testing Application Events – Best Practices**

### 🔍 **Scenario**: Test that an event is published and a listener reacts properly.

---

## 🧩 Step-by-Step Example

### 🧾 Define an Event

```java
public class UserRegisteredEvent {
    private final String email;

    public UserRegisteredEvent(String email) {
        this.email = email;
    }

    public String getEmail() {
        return email;
    }
}
```

---

### 🎯 Create a Listener

```java
@Component
public class WelcomeEmailListener {

    private boolean emailSent = false;

    @EventListener
    public void handleUserRegisteredEvent(UserRegisteredEvent event) {
        // Simulate sending email
        this.emailSent = true;
        System.out.println("Email sent to: " + event.getEmail());
    }

    public boolean isEmailSent() {
        return emailSent;
    }
}
```

---

### 🚀 Publish the Event in a Service

```java
@Service
public class UserService {

    @Autowired
    private ApplicationEventPublisher publisher;

    public void registerUser(String email) {
        // Logic to register user
        publisher.publishEvent(new UserRegisteredEvent(email));
    }
}
```

---

### 🧪 Write a Test

```java
@SpringBootTest
public class ApplicationEventTest {

    @Autowired
    private UserService userService;

    @Autowired
    private WelcomeEmailListener emailListener;

    @Test
    void testUserRegisteredEvent() {
        userService.registerUser("test@example.com");

        // Assert listener responded (could be a flag, mock, etc.)
        assertTrue(emailListener.isEmailSent());
    }
}
```

---

## ✅ Alternative: Use Mockito for Event Listener

If the listener has dependencies, mock them:

```java
@Component
public class WelcomeEmailListener {

    @Autowired
    private EmailService emailService;

    @EventListener
    public void onUserRegistered(UserRegisteredEvent event) {
        emailService.send(event.getEmail());
    }
}
```

### Test:

```java
@SpringBootTest
public class EventWithMockTest {

    @Autowired
    private UserService userService;

    @MockBean
    private EmailService emailService;

    @Test
    void testEmailServiceCalled() {
        userService.registerUser("test@example.com");

        verify(emailService, times(1)).send("test@example.com");
    }
}
```

---

## ✅ Summary

| Goal                       | How to Test                           |
| -------------------------- | ------------------------------------- |
| Event was **published**    | Use mocks or flags in listeners       |
| Listener **handled event** | Spy or mock dependent services        |
| Whole **flow end-to-end**  | Use `@SpringBootTest` with assertions |

---

## 52. How do you test scheduled tasks in Spring Boot?

Testing **scheduled tasks** in Spring Boot (annotated with `@Scheduled`) can be a bit tricky because they rely on time-based triggers, not method calls. However, you **can and should test them** using a few practical strategies depending on your goals.

---

## ✅ 1. **Understanding `@Scheduled` in Spring**

A method annotated with `@Scheduled` runs automatically at a fixed rate, delay, or cron schedule.

```java
@Component
public class ReportScheduler {

    @Scheduled(cron = "0 0 * * * *") // Every hour
    public void generateReport() {
        // Generate report logic
        System.out.println("Report generated.");
    }
}
```

---

## ✅ 2. **Testing Strategy**

Because `@Scheduled` methods run automatically, we typically test them by:

1. **Calling the method directly** (unit test).
2. **Verifying side effects** or **mocking dependencies**.
3. **Using `TestConfiguration`** or **@MockBean** for isolation.
4. Optionally **disabling scheduling** in tests.

---

## 🧪 Example 1: **Unit Testing the Scheduled Method**

If the method does something testable (e.g., calls a service), you can just call it directly.

```java
@SpringBootTest
public class ReportSchedulerTest {

    @Autowired
    private ReportScheduler reportScheduler;

    @Test
    void testGenerateReport() {
        reportScheduler.generateReport();
        // Assert logic or verify calls if using mocks
    }
}
```

---

## 🧪 Example 2: **Mocking a Dependency in a Scheduled Task**

```java
@Component
public class ReportScheduler {

    @Autowired
    private ReportService reportService;

    @Scheduled(fixedDelay = 5000)
    public void generateReport() {
        reportService.generate();
    }
}
```

### Test:

```java
@SpringBootTest
public class ReportSchedulerTest {

    @Autowired
    private ReportScheduler reportScheduler;

    @MockBean
    private ReportService reportService;

    @Test
    void testScheduledTaskCallsService() {
        reportScheduler.generateReport();
        verify(reportService, times(1)).generate();
    }
}
```

---

## 🛠️ Disabling Scheduling in Tests

If you want to prevent all scheduled tasks from running automatically in tests:

```yaml
# application-test.yml
spring:
  task:
    scheduling:
      enabled: false
```

Or programmatically using:

```java
@SpringBootTest(properties = "spring.task.scheduling.enabled=false")
```

Then call the method manually in the test.

---

## 🧪 Example 3: **Test Configuration for Scheduling**

To enable scheduling explicitly for a test:

```java
@TestConfiguration
@EnableScheduling
public class TestSchedulerConfig {
    // Beans if needed
}
```

---

## ⏱️ Want to Test the Actual Triggering? Use `@EnableScheduling` + `Thread.sleep()`

```java
@SpringBootTest
@EnableScheduling
public class RealSchedulerTriggerTest {

    @SpyBean
    private ReportScheduler reportScheduler;

    @Test
    void testSchedulerFires() throws InterruptedException {
        Thread.sleep(6000); // Wait longer than fixedDelay
        verify(reportScheduler, atLeastOnce()).generateReport();
    }
}
```

> ⚠️ **Not recommended for unit tests** — this is more like an integration test.

---

## ✅ Summary

| Goal                             | Recommended Approach                            |
| -------------------------------- | ----------------------------------------------- |
| Test logic of scheduled method   | Call it directly and assert/mock behavior       |
| Prevent auto-run during tests    | Use `spring.task.scheduling.enabled=false`      |
| Verify scheduling actually fires | Use `@SpyBean` + `Thread.sleep()` (integration) |
| Avoid slow tests                 | Prefer unit tests over waiting-based tests      |

---

## 53. How do you isolate layers while testing in Spring Boot?

Isolating layers while testing in Spring Boot is crucial for writing **clean**, **fast**, and **reliable** tests. It helps you test only **one layer at a time** (controller, service, repository) by **mocking dependencies** of that layer.

---

## ✅ Why Isolate Layers?

Each Spring Boot layer should be tested **independently**:

| Layer      | Purpose               | Test Type            | Mock Dependencies      |
| ---------- | --------------------- | -------------------- | ---------------------- |
| Controller | Handle HTTP requests  | Unit / `@WebMvcTest` | ✅ Service layer        |
| Service    | Business logic        | Unit                 | ✅ Repositories or APIs |
| Repository | Database access (JPA) | `@DataJpaTest`       | ❌ Uses real (H2) DB    |

---

## 🔍 1. **Testing the Controller Layer (`@WebMvcTest`)**

* Use `@WebMvcTest` to **load only the web layer**
* Mock services with `@MockBean`

### Example:

```java
@RestController
public class UserController {

    @Autowired
    private UserService userService;

    @GetMapping("/users/{id}")
    public ResponseEntity<User> getUser(@PathVariable Long id) {
        return ResponseEntity.ok(userService.getUserById(id));
    }
}
```

```java
@WebMvcTest(UserController.class)
public class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService;

    @Test
    void testGetUser() throws Exception {
        User mockUser = new User(1L, "Alice");
        when(userService.getUserById(1L)).thenReturn(mockUser);

        mockMvc.perform(get("/users/1"))
               .andExpect(status().isOk())
               .andExpect(jsonPath("$.name").value("Alice"));
    }
}
```

---

## 🔍 2. **Testing the Service Layer (Pure Unit Test)**

* Use `@ExtendWith(MockitoExtension.class)`
* Mock the repository or API clients

```java
public class UserService {

    @Autowired
    private UserRepository userRepository;

    public User getUserById(Long id) {
        return userRepository.findById(id).orElseThrow();
    }
}
```

```java
@ExtendWith(MockitoExtension.class)
public class UserServiceTest {

    @InjectMocks
    private UserService userService;

    @Mock
    private UserRepository userRepository;

    @Test
    void testGetUserById() {
        User mockUser = new User(1L, "Bob");
        when(userRepository.findById(1L)).thenReturn(Optional.of(mockUser));

        User result = userService.getUserById(1L);
        assertEquals("Bob", result.getName());
    }
}
```

---

## 🔍 3. **Testing the Repository Layer (`@DataJpaTest`)**

* Loads **only JPA-related beans**
* Uses **in-memory DB** like H2
* No need to mock anything

```java
@DataJpaTest
public class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    void testSaveAndFind() {
        User user = new User(null, "Carol");
        userRepository.save(user);

        Optional<User> found = userRepository.findById(user.getId());
        assertTrue(found.isPresent());
        assertEquals("Carol", found.get().getName());
    }
}
```

---

## 🧠 Key Annotations for Layer Isolation

| Annotation               | Used For            | Loads Only                      |
| ------------------------ | ------------------- | ------------------------------- |
| `@WebMvcTest`            | Controller layer    | Spring MVC beans                |
| `@DataJpaTest`           | Repository layer    | JPA, H2 DB, no services         |
| `@SpringBootTest`        | Integration testing | Full Spring context             |
| `@MockBean`              | Mock Spring beans   | Used inside `@WebMvcTest`, etc. |
| `@Mock` / `@InjectMocks` | Unit testing        | No Spring context needed        |

---

## ✅ Summary: How to Isolate Layers

| Layer      | Strategy                                  |
| ---------- | ----------------------------------------- |
| Controller | `@WebMvcTest` + `@MockBean`               |
| Service    | JUnit + Mockito (`@Mock`)                 |
| Repository | `@DataJpaTest` (real DB interaction)      |
| Full Stack | `@SpringBootTest` (if integration needed) |

---

## 54. What is `TestEntityManager`?

### ✅ What is `TestEntityManager` in Spring Boot?

`TestEntityManager` is a special utility provided by Spring Boot to **simplify JPA tests** during unit or integration testing. It’s available when using `@DataJpaTest`.

It is an **alternative to the standard `EntityManager`**, but with more convenient methods tailored for testing.

---

## 📌 Why Use `TestEntityManager`?

* Allows **saving, finding, and flushing entities** easily in tests.
* Useful for **setting up data** before testing JPA repositories.
* Provides **cleaner and more readable tests** than using full-blown `EntityManager`.

---

## 📦 Where Does It Come From?

`TestEntityManager` is part of the `spring-boot-starter-test` module under:

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-test</artifactId>
  <scope>test</scope>
</dependency>
```

> Also requires `spring-boot-test-autoconfigure`.

---

## 🧪 Example: Using `TestEntityManager` in a JPA Test

### 1. **Entity**

```java
@Entity
public class User {
    @Id
    @GeneratedValue
    private Long id;

    private String name;

    // Constructors, getters, setters
}
```

### 2. **Repository**

```java
public interface UserRepository extends JpaRepository<User, Long> {
    User findByName(String name);
}
```

### 3. **Test with `TestEntityManager`**

```java
@DataJpaTest
public class UserRepositoryTest {

    @Autowired
    private TestEntityManager entityManager;

    @Autowired
    private UserRepository userRepository;

    @Test
    public void testFindByName() {
        User user = new User();
        user.setName("Alice");

        // Persist the entity using TestEntityManager
        entityManager.persistAndFlush(user);

        // Now test repository
        User found = userRepository.findByName("Alice");
        assertEquals("Alice", found.getName());
    }
}
```

---

## ✅ Common Methods in `TestEntityManager`

| Method                    | Purpose                        |
| ------------------------- | ------------------------------ |
| `persist(entity)`         | Saves entity (without flush)   |
| `persistAndFlush(entity)` | Saves and flushes immediately  |
| `find(Class<T>, id)`      | Finds entity by ID             |
| `flush()`                 | Forces DB synchronization      |
| `remove(entity)`          | Deletes an entity              |
| `clear()`                 | Clears the persistence context |

---

## 🔁 Difference from Regular `EntityManager`

| Feature               | `EntityManager`    | `TestEntityManager`  |
| --------------------- | ------------------ | -------------------- |
| Purpose               | Production runtime | Testing only         |
| Ease of use           | Verbose            | Simplified syntax    |
| Auto-injected in test | ❌ (manual setup)   | ✅ via `@DataJpaTest` |

---

## ✅ Summary

* `TestEntityManager` is a **helper class** for JPA-related testing.
* Available automatically with `@DataJpaTest`.
* Great for **setting up test data**, flushing, or validating JPA interactions.
* Cleaner than using raw `EntityManager` in tests.

---

## 55. What are test slices in Spring Boot?

### ✅ What Are Test Slices in Spring Boot?

**Test slices** in Spring Boot are a feature that allows you to **load only a part (slice) of the application context** for testing a specific layer or component of your application. This keeps tests fast and focused.

---

## 🎯 Why Use Test Slices?

* **Isolate specific layers** (web, data, security, etc.)
* **Speed up tests** by avoiding unnecessary beans
* **Avoid unintended side effects** from other components

---

## 🧪 Common Test Slice Annotations

| Annotation        | Purpose                                         | Loads               |
| ----------------- | ----------------------------------------------- | ------------------- |
| `@WebMvcTest`     | Test controllers (Spring MVC layer)             | Controllers + MVC   |
| `@DataJpaTest`    | Test JPA repositories                           | JPA + H2 database   |
| `@JsonTest`       | Test JSON serialization/deserialization         | Jackson config only |
| `@WebFluxTest`    | Test reactive controllers (WebFlux)             | WebFlux layer       |
| `@RestClientTest` | Test REST clients (`RestTemplate`, `WebClient`) | RestTemplate beans  |
| `@JdbcTest`       | Test JDBC components                            | `JdbcTemplate`, H2  |
| `@GraphQlTest`    | Test GraphQL controllers                        | GraphQL layer only  |

---

## ✅ Example 1: `@WebMvcTest` — Testing the Web Layer

```java
@WebMvcTest(UserController.class)
public class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @MockBean
    private UserService userService;

    @Test
    void shouldReturnUser() throws Exception {
        when(userService.getUser(1L)).thenReturn(new User(1L, "Alice"));

        mockMvc.perform(get("/users/1"))
               .andExpect(status().isOk())
               .andExpect(jsonPath("$.name").value("Alice"));
    }
}
```

> ✅ Loads only Spring MVC-related beans
> ❌ Does **not** load the full application context (e.g., services or repositories unless mocked)

---

## ✅ Example 2: `@DataJpaTest` — Testing Repositories

```java
@DataJpaTest
public class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    void testFindByName() {
        User user = new User(null, "Bob");
        userRepository.save(user);

        User found = userRepository.findByName("Bob");
        assertEquals("Bob", found.getName());
    }
}
```

> ✅ Uses in-memory database (e.g., H2)
> ✅ Configures `EntityManager`, `JdbcTemplate`
> ❌ Does **not** load services, controllers, etc.

---

## ✅ Example 3: `@JsonTest` — Testing Jackson Object Mapping

```java
@JsonTest
public class UserJsonTest {

    @Autowired
    private ObjectMapper objectMapper;

    @Test
    void testSerialize() throws Exception {
        User user = new User(1L, "Charlie");

        String json = objectMapper.writeValueAsString(user);
        assertTrue(json.contains("Charlie"));
    }
}
```

---

## 🧠 Tips for Using Test Slices

* Use **`@MockBean`** to inject mocks into slices.
* Test slices are meant for **unit or component tests**, not full integration tests.
* Combine with `@Import` or `@ContextConfiguration` to bring in additional needed config.
* Test slices **do not load full application properties or `@ComponentScan` beans** unless explicitly added.

---

## ✅ Summary

| Test Slice        | Focus Area         | Real DB? | Needs Mocking?    |
| ----------------- | ------------------ | -------- | ----------------- |
| `@WebMvcTest`     | Controllers        | ❌        | ✅ Services, Repos |
| `@DataJpaTest`    | JPA Repositories   | ✅ H2     | ❌                 |
| `@JsonTest`       | JSON Serialization | N/A      | ❌                 |
| `@RestClientTest` | REST Client Layer  | ❌        | ✅ Remote services |
| `@JdbcTest`       | Plain JDBC logic   | ✅        | ❌                 |

---

## 56. How do you load application.yml or properties in test scope?

### ✅ How Do You Load `application.yml` or `application.properties` in Test Scope?

In Spring Boot, loading configuration files like `application.yml` or `application.properties` in test scope ensures your tests use the right settings (e.g., in-memory DB, mock URLs, feature flags).

---

## 🔹 Spring Boot Automatically Loads Test Config Files

When you run tests, Spring Boot **automatically loads**:

* `application.properties` or `application.yml`
* And if it exists: `application-test.properties` / `application-test.yml`

This depends on the active profile.

---

## ✅ 1. **Default Behavior**

If you just have:

```yaml
# src/test/resources/application.yml
app:
  message: "Hello from test!"
```

Then in a test:

```java
@SpringBootTest
public class SampleTest {

    @Value("${app.message}")
    private String message;

    @Test
    void testAppMessage() {
        assertEquals("Hello from test!", message);
    }
}
```

Spring will load that test-specific config automatically.

---

## ✅ 2. **Using Profiles with `@ActiveProfiles`**

To load `application-test.yml`, you must **activate the profile**:

```yaml
# src/test/resources/application-test.yml
server:
  port: 8085
```

```java
@SpringBootTest
@ActiveProfiles("test")
public class ProfiledTest {

    @Value("${server.port}")
    private int port;

    @Test
    void testPort() {
        assertEquals(8085, port);
    }
}
```

> 💡 `@ActiveProfiles("test")` tells Spring to load `application-test.yml`

---

## ✅ 3. **Using `@TestPropertySource` to Override or Add Inline Properties**

```java
@SpringBootTest
@TestPropertySource(properties = {
    "feature.enabled=true",
    "timeout=30"
})
public class InlinePropertyTest {

    @Value("${timeout}")
    private int timeout;

    @Value("${feature.enabled}")
    private boolean enabled;

    @Test
    void testProps() {
        assertTrue(enabled);
        assertEquals(30, timeout);
    }
}
```

---

## ✅ 4. **Accessing Properties via `@ConfigurationProperties`**

```yaml
# application.yml
my:
  config:
    url: "https://api.example.com"
```

```java
@Component
@ConfigurationProperties(prefix = "my.config")
public class MyConfigProperties {
    private String url;
    // getters and setters
}
```

```java
@SpringBootTest
@ActiveProfiles("test")
public class ConfigPropertiesTest {

    @Autowired
    private MyConfigProperties config;

    @Test
    void testConfigUrl() {
        assertEquals("https://api.example.com", config.getUrl());
    }
}
```

> Make sure you annotate with `@EnableConfigurationProperties` if needed.

---

## ✅ 5. **Loading Custom Property Files**

```java
@SpringBootTest
@TestPropertySource(locations = "classpath:custom-test.properties")
public class CustomFileTest {
    // custom-test.properties will be loaded
}
```

---

## 🔁 Summary: Ways to Load Properties in Tests

| Method                               | Purpose                                   |
| ------------------------------------ | ----------------------------------------- |
| `src/test/resources/application.yml` | Automatically loaded for tests            |
| `@ActiveProfiles("test")`            | Loads `application-test.yml/properties`   |
| `@TestPropertySource`                | Inline or external property file override |
| `@Value("${...}")`                   | Injects values directly                   |
| `@ConfigurationProperties`           | Maps structured config to POJOs           |

---

## 57. How do you run a test with a specific profile?

### ✅ How Do You Run a Test with a Specific Profile in Spring Boot?

In Spring Boot, **profiles** (like `dev`, `test`, `prod`) let you define different configurations for different environments.
To run a test with a **specific profile**, you use the `@ActiveProfiles` annotation.

---

## 🔹 Why Use Profiles in Tests?

* To load specific `application-<profile>.yml` or `.properties` files
* To test different configurations (e.g., mock vs real service)
* To separate test behavior from production behavior

---

## ✅ Step-by-Step: Run a Test with a Profile

### 1. **Create a Profile-Specific Configuration File**

```yaml
# src/test/resources/application-test.yml
service:
  url: "http://mock-service"
```

---

### 2. **Use `@ActiveProfiles("test")` in Your Test**

```java
@SpringBootTest
@ActiveProfiles("test")
public class MyServiceTest {

    @Value("${service.url}")
    private String serviceUrl;

    @Test
    void testServiceUrl() {
        assertEquals("http://mock-service", serviceUrl);
    }
}
```

> ✅ This tells Spring to use the `test` profile and load `application-test.yml`

---

## 🔄 You Can Also Use `@ActiveProfiles` with Sliced Tests

```java
@WebMvcTest(UserController.class)
@ActiveProfiles("test")
public class UserControllerTest {
    // loads test-specific properties
}
```

---

## 🔍 Verifying the Active Profile at Runtime

To check the active profile during the test:

```java
@Autowired
private Environment env;

@Test
void printActiveProfiles() {
    System.out.println(Arrays.toString(env.getActiveProfiles()));
}
```

---

## ✅ Summary

| Use Case                        | Annotation                                     | Notes                        |
| ------------------------------- | ---------------------------------------------- | ---------------------------- |
| Run test with `test` profile    | `@ActiveProfiles("test")`                      | Loads `application-test.yml` |
| Use in controller or repo tests | Works with `@WebMvcTest`, `@DataJpaTest`, etc. |                              |
| Inject properties in test       | Use `@Value` or `@ConfigurationProperties`     |                              |

---

## 58. What is `@TestConfiguration` and how is it different from `@Configuration`?

### ✅ What is `@TestConfiguration` and How is it Different from `@Configuration`?

In Spring, `@Configuration` is used to define beans for the application context, whereas `@TestConfiguration` is specifically used in tests to define **test-specific configurations**. It allows you to customize the application context in a way that is specific to tests, without affecting the global configuration.

---

## 🔹 `@Configuration`

* **Used in Main Application**: It is typically used in the main application to define beans that Spring needs to load into the application context at runtime.
* **Global Scope**: Beans defined with `@Configuration` are loaded for the entire application context (both production and tests).
* **Usage**: Define services, repositories, and other beans to be used throughout the application.

### Example:

```java
@Configuration
public class AppConfig {
    
    @Bean
    public MyService myService() {
        return new MyServiceImpl();
    }
}
```

This class will be picked up by Spring when the application context is initialized, and `MyService` will be available globally.

---

## 🔹 `@TestConfiguration`

* **Used in Test Scope**: It is a specialized annotation designed to **define test-specific configurations** (e.g., mock beans, custom setups) that **only apply to the test context**.
* **Test-Specific Scope**: Beans defined with `@TestConfiguration` are **only used in tests** and do not affect the global application context.
* **Common Use Case**: This is often used to define beans that should be available only in the test context or to override existing beans for testing purposes.

### Example:

```java
@TestConfiguration
public class TestConfig {

    @Bean
    public MyService myService() {
        return new MockMyServiceImpl();
    }
}
```

This configuration is only used during the test execution, and the `MockMyServiceImpl` will replace any real `MyService` beans for the test.

---

## 🔹 Key Differences Between `@TestConfiguration` and `@Configuration`

| Aspect              | `@Configuration`                                      | `@TestConfiguration`                             |
| ------------------- | ----------------------------------------------------- | ------------------------------------------------ |
| **Scope**           | Application-wide                                      | Test-specific                                    |
| **Usage**           | Used to define production beans                       | Used to define beans for tests only              |
| **Visibility**      | Beans are available to the entire application context | Beans are only available within the test context |
| **Context Loading** | Loaded when the application context is loaded         | Loaded only in the test context                  |
| **Common Use**      | Defining beans for the entire application             | Defining mock beans or overriding beans in tests |

---

## ✅ Example: Using `@TestConfiguration` in a Test

### 1. **Test-Specific Bean Replacement**

Let's say you have a service `UserService` that depends on a repository `UserRepository`, but for testing purposes, you want to mock the repository:

```java
@TestConfiguration
public class TestConfig {

    @Bean
    public UserRepository userRepository() {
        return Mockito.mock(UserRepository.class);
    }
}
```

### 2. **Test Class with `@TestConfiguration`**

Now, you can use this configuration in your test class:

```java
@RunWith(SpringRunner.class)
@SpringBootTest
@Import(TestConfig.class)  // Import the test configuration
public class UserServiceTest {

    @Autowired
    private UserService userService;

    @Autowired
    private UserRepository userRepository;

    @Test
    public void testGetUser() {
        // Mock behavior of the repository
        User mockUser = new User(1L, "John Doe");
        when(userRepository.findById(1L)).thenReturn(Optional.of(mockUser));

        User result = userService.getUser(1L);
        assertEquals("John Doe", result.getName());
    }
}
```

In this example, `@TestConfiguration` is used to provide a mock `UserRepository` only in the test context. The real `UserRepository` will not be used in this test.

---

## ✅ Why Use `@TestConfiguration`?

* **Custom test-specific beans**: When you need to define beans that only serve the test purpose, e.g., mocks or test replacements.
* **Isolate test configurations**: It keeps your test configurations separate from your production configurations.
* **No impact on production code**: You can customize beans for testing without affecting the actual production environment or application context.

---

## 🔁 Summary

| Feature         | `@Configuration`                                          | `@TestConfiguration`                                |
| --------------- | --------------------------------------------------------- | --------------------------------------------------- |
| **Purpose**     | Used to configure beans for the whole application context | Used for test-specific configuration beans          |
| **Scope**       | Global, affects both production and test contexts         | Test-specific, only available during test execution |
| **Visibility**  | Beans are globally available                              | Beans are only available in tests                   |
| **Typical Use** | Production-level configuration                            | Mocking dependencies or overriding beans in tests   |

---

## 59. How do you use embedded databases for tests?

### ✅ How to Use Embedded Databases for Tests in Spring Boot?

Embedded databases (such as **H2**, **HSQLDB**, or **Derby**) are commonly used in tests to simulate a real database without needing to connect to an actual external database. Using embedded databases in tests helps speed up testing by reducing setup complexity and provides isolation, ensuring that the tests do not affect a real database.

In Spring Boot, configuring an embedded database for testing is simple. Here's how you can use an embedded database in your tests.

---

## 🔹 1. **Use H2 (or any embedded DB)**

**H2** is a commonly used embedded database in Spring Boot. It’s lightweight, fast, and easy to configure. By default, Spring Boot automatically uses **H2** when it detects the `H2` dependency in the classpath and no other database configuration is provided.

---

### 2. **Basic Configuration for H2 in `application.yml` or `application.properties`**

#### `application-test.yml` (or `application-test.properties`)

You can create a profile-specific configuration to use **H2** during testing:

```yaml
# src/test/resources/application-test.yml
spring:
  datasource:
    url: jdbc:h2:mem:testdb  # In-memory H2 database
    driverClassName: org.h2.Driver
    username: sa
    password: password
    dialect: org.hibernate.dialect.H2Dialect
  h2:
    console:
      enabled: true  # Optional: enable H2 console in the browser
  jpa:
    hibernate:
      ddl-auto: update  # auto-create tables if necessary
```

This configuration sets up an **in-memory H2 database** for testing purposes.

> 💡 **In-Memory Database**: The database is created in memory and is destroyed after the test finishes.

---

### 3. **Configure `@ActiveProfiles` for Test Profile**

You can use `@ActiveProfiles` to specify the test profile so Spring Boot uses `application-test.yml` or `application-test.properties`:

```java
@SpringBootTest
@ActiveProfiles("test")
public class UserServiceTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    void testSaveUser() {
        User user = new User("Alice", "alice@example.com");
        userRepository.save(user);

        Optional<User> found = userRepository.findById(user.getId());
        assertTrue(found.isPresent());
    }
}
```

> ✅ `@ActiveProfiles("test")` ensures Spring Boot uses the configuration in `application-test.yml`.

---

## 🔹 4. **Using `@DataJpaTest` for JPA Repositories**

If you're testing a **JPA repository**, Spring Boot provides the `@DataJpaTest` annotation. This automatically configures an **embedded database** (like **H2**) and sets up the required components (like `EntityManager`).

```java
@DataJpaTest
public class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    void testSaveUser() {
        User user = new User("Bob", "bob@example.com");
        userRepository.save(user);

        Optional<User> found = userRepository.findById(user.getId());
        assertTrue(found.isPresent());
    }
}
```

> ✅ `@DataJpaTest` automatically configures an **in-memory database**, so you don't need to manually configure the database URL or dialect.

---

## 🔹 5. **Using `@TestConfiguration` with Embedded Database**

If you need more flexibility, you can configure the embedded database within a `@TestConfiguration` class. This is useful for overriding beans or customizing the configuration for a specific test.

```java
@TestConfiguration
public class TestConfig {

    @Bean
    public DataSource dataSource() {
        return DataSourceBuilder.create()
                .url("jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1")
                .driverClassName("org.h2.Driver")
                .username("sa")
                .password("password")
                .build();
    }
}
```

```java
@SpringBootTest
@Import(TestConfig.class)
public class CustomDatabaseTest {

    @Autowired
    private DataSource dataSource;

    @Test
    void testCustomDataSource() throws SQLException {
        try (Connection connection = dataSource.getConnection()) {
            assertNotNull(connection);
        }
    }
}
```

> ✅ This allows you to provide custom configuration while using an embedded database.

---

## 🔹 6. **Using `@Transactional` with Embedded Databases**

You can combine **transactional tests** with an embedded database. **Spring Test** ensures that all changes made to the database during the test are rolled back after the test completes.

```java
@Transactional
@SpringBootTest
public class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    void testSaveUser() {
        User user = new User("Charlie", "charlie@example.com");
        userRepository.save(user);

        Optional<User> found = userRepository.findById(user.getId());
        assertTrue(found.isPresent());
    }
}
```

> ✅ `@Transactional` ensures that the database state is rolled back after each test, preventing data contamination between tests.

---

## 🔹 7. **Common Embedded Database Options**

* **H2**: Lightweight, popular in-memory database.
* **HSQLDB**: Another in-memory database with slightly different features.
* **Derby**: In-memory or persistent database with embedded support.

---

### 💡 Benefits of Using Embedded Databases in Tests

* **No external dependencies**: Tests do not require an actual database connection.
* **Speed**: In-memory databases are fast and automatically clean up after each test run.
* **Isolation**: Tests can run in parallel without affecting the real database.
* **Lightweight**: Small footprint, no need for database management during tests.

---

### ✅ Summary

| Aspect                        | Description                                                                          |
| ----------------------------- | ------------------------------------------------------------------------------------ |
| **Common Embedded Databases** | H2, HSQLDB, Derby                                                                    |
| **Configuration**             | Use `application-test.yml` or `application-test.properties` for embedded DB settings |
| **Testing Repositories**      | Use `@DataJpaTest` to automatically configure an embedded database for JPA tests     |
| **Custom Database Config**    | Use `@TestConfiguration` to customize database configuration for specific tests      |
| **Rollback Changes**          | Use `@Transactional` to automatically roll back database changes after each test     |

---

## 60. How do you measure and improve test coverage in Spring Boot apps?

### ✅ How to Measure and Improve Test Coverage in Spring Boot Apps?

Test coverage is a key metric to determine the effectiveness of your tests in covering your codebase. In Spring Boot applications, test coverage helps ensure that your code is well-tested, and any changes to the codebase won’t introduce unintended errors.

Here’s how you can **measure** and **improve** test coverage in your Spring Boot applications.

---

## 🔹 1. **Measuring Test Coverage**

### 1.1 **Using Jacoco for Test Coverage**

**Jacoco** (Java Code Coverage) is a popular tool for measuring code coverage in Java projects. Spring Boot supports Jacoco integration out of the box.

#### Setup Jacoco with Maven:

1. Add the **Jacoco plugin** in your `pom.xml`:

```xml
<build>
    <plugins>
        <!-- Add Jacoco plugin for code coverage -->
        <plugin>
            <groupId>org.jacoco</groupId>
            <artifactId>jacoco-maven-plugin</artifactId>
            <version>0.8.7</version>
            <executions>
                <execution>
                    <goals>
                        <goal>prepare-agent</goal>
                        <goal>report</goal>
                    </goals>
                </execution>
            </executions>
        </plugin>
    </plugins>
</build>
```

2. **Run your tests** with Maven:

```bash
mvn clean test
```

3. **Generate the Coverage Report**: After running the tests, you can generate the code coverage report.

```bash
mvn jacoco:report
```

4. **Check the Coverage Report**: The generated report will typically be found in the `target/site/jacoco/index.html` file. Open this file in a browser to view the coverage details.

---

### 1.2 **Using Jacoco with Gradle**

If you’re using Gradle, follow this configuration:

1. Add the **Jacoco plugin** in your `build.gradle`:

```gradle
plugins {
    id 'jacoco'
}

jacoco {
    toolVersion = "0.8.7"
}

test {
    useJUnitPlatform()
    finalizedBy jacocoTestReport // Generate coverage after tests
}

jacocoTestReport {
    reports {
        html.enabled = true
        xml.enabled = false
    }
}
```

2. **Run your tests** with Gradle:

```bash
./gradlew test jacocoTestReport
```

3. **Access the Coverage Report**: Find the generated report in the `build/reports/jacoco/test/html/index.html` file.

---

### 1.3 **Using SonarQube for Test Coverage (Optional)**

SonarQube is a powerful code quality management tool that integrates well with Maven and Gradle to track test coverage, code smells, and other metrics.

1. **Install SonarQube**: Download and set up [SonarQube](https://www.sonarqube.org/).

2. **Configure Maven**: Add the SonarQube plugin in `pom.xml`:

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.sonarsource.scanner.maven</groupId>
            <artifactId>sonar-maven-plugin</artifactId>
            <version>3.9.0.2155</version>
        </plugin>
    </plugins>
</build>
```

3. **Run the SonarQube Analysis**:

```bash
mvn clean verify sonar:sonar
```

This will push your coverage and other metrics to your SonarQube instance.

---

## 🔹 2. **Improving Test Coverage**

### 2.1 **Focus on Uncovered Areas**

To improve your test coverage, focus on **uncovered** or **partially covered** areas of your code.

1. **Examine the Coverage Report**: Look at the Jacoco report or SonarQube results and identify parts of your application that have low or no coverage (e.g., controllers, services, etc.).

2. **Increase Coverage in Critical Areas**: Prioritize covering core logic, critical paths, and any new feature developments. These areas usually include:

    * Business logic in services
    * Controllers (for API tests)
    * Edge cases and exception handling
    * Validation and error handling

---

### 2.2 **Writing Comprehensive Unit Tests**

To improve coverage, write more detailed and focused unit tests:

1. **Test All Code Paths**:

    * **Happy Path**: The regular scenario where everything works fine.
    * **Edge Cases**: Test with boundary values, null inputs, empty lists, etc.
    * **Error Handling**: Ensure that exceptions, timeouts, and unexpected behavior are handled correctly.

2. **Test Different Scenarios Using Parameterized Tests**: With Spring Boot and JUnit, you can test multiple sets of inputs and outputs for the same method using **parameterized tests**.

```java
@ParameterizedTest
@ValueSource(strings = {"admin", "user"})
void testUserRole(String role) {
    // Test different roles using the same test method
}
```

3. **Mock Dependencies**: Use **mocking frameworks** like **Mockito** to test components independently, ensuring that each part of your system is properly covered.

---

### 2.3 **Write Integration Tests**

While unit tests focus on small components, **integration tests** ensure that multiple components work together correctly.

1. **Use `@SpringBootTest` for Integration Tests**: This annotation helps to load the full Spring context, allowing you to test how different parts of the application (e.g., controllers, services, repositories) interact with each other.

```java
@SpringBootTest
public class UserControllerIntegrationTest {

    @Autowired
    private MockMvc mockMvc;

    @Test
    public void testCreateUser() throws Exception {
        mockMvc.perform(post("/users")
                .contentType(MediaType.APPLICATION_JSON)
                .content("{\"name\":\"John\",\"email\":\"john@example.com\"}"))
                .andExpect(status().isCreated());
    }
}
```

2. **Use `@DataJpaTest` for Testing Repositories**: This focuses on testing the JPA layer (repositories) using an embedded database (e.g., H2).

```java
@DataJpaTest
public class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    public void testFindByEmail() {
        User user = userRepository.save(new User("Alice", "alice@example.com"));
        Optional<User> foundUser = userRepository.findByEmail("alice@example.com");
        assertTrue(foundUser.isPresent());
    }
}
```

---

### 2.4 **Ensure Proper Exception Handling**

Make sure that your tests cover exceptions and error handling:

* **Test for expected exceptions** with `assertThrows()` in JUnit.

```java
@Test
void testServiceThrowsException() {
    assertThrows(SomeException.class, () -> {
        service.methodThatThrowsException();
    });
}
```

---

### 2.5 **Refactor and Use Test Coverage Tools**

If certain classes or methods are difficult to test (e.g., too complex or have a lot of dependencies), **refactor them** to make them more testable:

* **Single Responsibility Principle**: Break down large classes into smaller, more focused ones.
* **Use Dependency Injection**: Ensure that dependencies can be mocked or injected easily.

---

## 🔁 Summary: Measuring & Improving Test Coverage

| Step                             | Description                                                           |
| -------------------------------- | --------------------------------------------------------------------- |
| **Measure Coverage**             | Use tools like **Jacoco** (Maven/Gradle) to measure test coverage.    |
| **Examine Coverage Reports**     | Look for areas with low or no coverage and prioritize them.           |
| **Write Comprehensive Tests**    | Cover edge cases, error handling, and business logic.                 |
| **Write Integration Tests**      | Use `@SpringBootTest` to test full system integration.                |
| **Use Mocking**                  | Mock dependencies using **Mockito** to isolate components.            |
| **Refactor Hard-to-Test Code**   | Refactor complex code to improve testability and simplify tests.      |
| **Leverage Test Coverage Tools** | Use **SonarQube** or **Jacoco** to monitor coverage and code quality. |

---

By continuously measuring and improving your test coverage, you ensure that your Spring Boot applications remain robust and reliable. Let me know if you need help with any specific tools or examples!

---

### 🔹 61–80: **TestNG, TDD, BDD, Coverage Tools**

## 61. What is TestNG and how is it different from JUnit?

### ✅ What is TestNG and How is it Different from JUnit?

**TestNG** (Test Next Generation) is a testing framework inspired by JUnit but with some significant differences and additional features. It is designed to overcome some of JUnit's limitations while providing more flexibility and ease of use.

Here's a comparison between **TestNG** and **JUnit** to help you understand their differences.

---

## 🔹 **What is TestNG?**

TestNG is a testing framework for Java that is designed to be easy to use, flexible, and powerful. It is inspired by JUnit but with several enhancements. It allows you to define test methods, configure tests, and handle execution order, parallel execution, data-driven tests, and more.

### Key Features of TestNG:

1. **Flexible Test Configuration**: TestNG provides advanced configuration annotations (e.g., `@BeforeClass`, `@AfterMethod`).
2. **Test Suite**: You can group and run tests as part of a suite, making it easier to manage large projects.
3. **Parallel Execution**: TestNG allows parallel execution of tests, which can significantly reduce the test run time.
4. **Data-Driven Tests**: Supports parameterized tests natively through `@DataProvider`, allowing multiple sets of input values for a single test method.
5. **Test Dependency**: You can set dependencies between test methods using `dependsOnMethods` or `dependsOnGroups`.
6. **Test Reporting**: TestNG provides detailed test reports out of the box, including success, failure, and skipped test results.

---

## 🔹 **Key Differences Between TestNG and JUnit**

| Feature/Aspect                     | **TestNG**                                                                                                             | **JUnit** (primarily JUnit 4)                                                                                                                            |
| ---------------------------------- | ---------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Annotations**                    | Uses annotations like `@Test`, `@BeforeMethod`, `@AfterMethod`, `@BeforeClass`, `@AfterClass`, `@DataProvider`, etc.   | Uses annotations like `@Test`, `@Before`, `@After`, `@BeforeClass`, `@AfterClass`.                                                                       |
| **Parameterized Tests**            | Uses `@DataProvider` to pass parameters to test methods.                                                               | JUnit 4 uses `@RunWith(Parameterized.class)` or `@ParameterizedTest` (in JUnit 5).                                                                       |
| **Test Execution**                 | Supports parallel test execution (using the `@Test` annotation).                                                       | Does not natively support parallel execution (though can be achieved with external tools like **JUnit 5** or **Maven**).                                 |
| **Test Configuration**             | More flexible configuration with annotations like `@BeforeMethod`, `@BeforeClass`, `@AfterMethod`, `@AfterClass`, etc. | Less flexible, with only `@Before` and `@After` in JUnit 4 (and `@BeforeEach` and `@AfterEach` in JUnit 5).                                              |
| **Test Suites**                    | Allows creation of complex test suites using XML files, enabling tests to be grouped and executed in a specific order. | In JUnit 4, test suites are created using `@RunWith(Suite.class)` or `@Suite` annotations, but the configuration is less flexible.                       |
| **Test Reporting**                 | TestNG generates detailed HTML and XML reports by default.                                                             | JUnit generates basic reports, and for advanced reporting, external tools are required.                                                                  |
| **Test Dependency**                | Supports test dependencies using `dependsOnMethods` and `dependsOnGroups`.                                             | JUnit does not have native support for test dependencies (though JUnit 5 has `@EnabledIf` and `@DisabledIf` for conditionally enabling/disabling tests). |
| **Test Groups**                    | Allows grouping tests using `@Test(groups = "groupName")`.                                                             | JUnit has no direct support for groups, but tests can be categorized using tags or by using third-party extensions.                                      |
| **Framework Type**                 | TestNG is a **testing framework** (handles suite execution, test configuration, etc.).                                 | JUnit is primarily a **unit testing framework**; it can be extended with tools for suite execution or complex scenarios.                                 |
| **Parallel Execution**             | Native support for running tests in parallel.                                                                          | JUnit does not support parallel execution in JUnit 4; JUnit 5 introduces parallel test execution with additional configuration.                          |
| **Support for Exceptions**         | Supports expected exceptions through `@Test(expectedExceptions = ...)`.                                                | JUnit uses `@Test(expected = ...)` to expect exceptions.                                                                                                 |
| **Timeouts**                       | Supports test timeouts via `@Test(timeOut = ...)`.                                                                     | JUnit 4 supports timeouts with `@Test(timeout = ...)` and `@Test(expected = ...)`.                                                                       |
| **Suites and Configuration Files** | TestNG uses **XML configuration files** to define and execute test suites.                                             | JUnit uses annotations, but there is no native support for XML suite configuration.                                                                      |

---

## 🔹 **Advantages of TestNG over JUnit**

1. **Parallel Test Execution**: TestNG makes it easier to run tests in parallel, which can significantly speed up large test suites.
2. **Flexible Test Configurations**: TestNG provides a richer set of annotations for configuring test methods, setup, and teardown at different levels (e.g., method-level, class-level, and suite-level).
3. **Test Dependencies**: TestNG allows you to define dependencies between tests, which is useful in scenarios where certain tests must be executed before others.
4. **Data-Driven Testing**: The `@DataProvider` annotation in TestNG allows easy creation of parameterized tests, which makes it simple to test multiple sets of inputs for a single test method.
5. **Test Groups**: Grouping tests into logical categories is much easier in TestNG and allows for better test management.
6. **Built-in Reports**: TestNG automatically generates detailed HTML and XML reports, whereas in JUnit, you need to rely on external tools for reporting.

---

## 🔹 **Advantages of JUnit over TestNG**

1. **Simplicity**: JUnit’s annotation-based approach is simpler and more intuitive for simple unit tests. TestNG’s configuration can be more complex, especially for beginners.
2. **Wider Adoption**: JUnit is more widely adopted in the Java ecosystem and has more tools, plugins, and integrations available. It is also the default framework in many build tools (Maven, Gradle, etc.).
3. **JUnit 5 Features**: JUnit 5 brings several advanced features such as improved support for parameterized tests, better lifecycle control, and parallel test execution, which address some of TestNG’s features.
4. **Ecosystem Support**: JUnit benefits from a large number of external tools, plugins, and integration support, which is ideal for CI/CD pipelines.

---

## 🔹 **Example: TestNG vs. JUnit Test**

### TestNG Example

```java
import org.testng.annotations.Test;
import org.testng.annotations.BeforeMethod;
import org.testng.annotations.AfterMethod;

public class TestNGExample {

    @BeforeMethod
    public void setUp() {
        System.out.println("Before each test method.");
    }

    @Test
    public void testMethod1() {
        System.out.println("Running Test 1");
    }

    @Test(dependsOnMethods = {"testMethod1"})
    public void testMethod2() {
        System.out.println("Running Test 2 (depends on Test 1)");
    }

    @AfterMethod
    public void tearDown() {
        System.out.println("After each test method.");
    }
}
```

### JUnit Example (JUnit 4)

```java
import org.junit.Before;
import org.junit.After;
import org.junit.Test;

public class JUnitExample {

    @Before
    public void setUp() {
        System.out.println("Before each test method.");
    }

    @Test
    public void testMethod1() {
        System.out.println("Running Test 1");
    }

    @Test
    public void testMethod2() {
        System.out.println("Running Test 2");
    }

    @After
    public void tearDown() {
        System.out.println("After each test method.");
    }
}
```

### JUnit 5 Example

```java
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.Test;

public class JUnit5Example {

    @BeforeEach
    public void setUp() {
        System.out.println("Before each test method.");
    }

    @Test
    public void testMethod1() {
        System.out.println("Running Test 1");
    }

    @Test
    public void testMethod2() {
        System.out.println("Running Test 2");
    }

    @AfterEach
    public void tearDown() {
        System.out.println("After each test method.");
    }
}
```

---

## 🔁 **Summary: TestNG vs. JUnit**

| Feature                 | **TestNG**                                                           | **JUnit**                                                                |
| ----------------------- | -------------------------------------------------------------------- | ------------------------------------------------------------------------ |
| **Configuration**       | More flexible with annotations like `@BeforeMethod`, `@AfterMethod`. | Simpler, but limited in configuration compared to TestNG.                |
| **Test Suite**          | Supports test suites and XML configurations.                         | JUnit has limited support for suites.                                    |
| **Parallel Execution**  | Supports parallel test execution.                                    | Limited support for parallel execution (in JUnit 5).                     |
| **Parameterized Tests** | Uses `@DataProvider` for parameterized tests.                        | JUnit 5 supports parameterized tests natively with `@ParameterizedTest`. |
| **Test Dependency**     | Supports test dependencies (`dependsOnMethods`).                     | No native support for test dependencies.                                 |
| **Reports**             | Built-in HTML and XML reports.                                       | Requires external tools for detailed reporting.                          |

---

### Conclusion:

* **TestNG** is more powerful and flexible, especially when you need advanced features like parallel test execution, dependencies, or complex test configurations.
* **JUnit** is simpler and widely adopted, and with JUnit 5, many features overlap with TestNG. It is ideal for straightforward unit testing and has strong ecosystem support.

The choice between TestNG and JUnit depends on your project needs and personal preferences.

---

## 62. How do you set test priorities in TestNG?

In TestNG, you can set **test priorities** to control the order in which test methods are executed. This is done using the `priority` attribute of the `@Test` annotation. The methods with lower priority values are executed before those with higher priority values. By default, methods without an explicitly defined priority will be executed in an arbitrary order.

### How to Set Test Priorities in TestNG:

You can set priorities by specifying the `priority` attribute in the `@Test` annotation for each test method. The test methods will be executed in the order of their priority values, with lower numbers being executed first.

### Example:

```java
import org.testng.annotations.Test;

public class TestNGPriorityExample {

    @Test(priority = 1)
    public void testFirst() {
        System.out.println("First test");
    }

    @Test(priority = 2)
    public void testSecond() {
        System.out.println("Second test");
    }

    @Test(priority = 0)
    public void testThird() {
        System.out.println("Third test");
    }

    @Test(priority = 3)
    public void testFourth() {
        System.out.println("Fourth test");
    }
}
```

### Output:

```
Third test
First test
Second test
Fourth test
```

### Key Points:

* **Lower Priority Numbers**: Test methods with **lower priority numbers** will run **before** those with higher numbers. In the example, `testThird` has the lowest priority (`0`), so it runs first.
* **Default Priority**: If no priority is specified for a test method, it is considered to have the default priority value of **`0`**.
* **Negative Priority**: You can also use **negative** priority numbers. For example, `priority = -1` will execute that test method before those with priority `0`.

### Example with Negative Priority:

```java
import org.testng.annotations.Test;

public class TestNGPriorityExample {

    @Test(priority = -1)
    public void testLowPriority() {
        System.out.println("Low priority test");
    }

    @Test(priority = 0)
    public void testDefaultPriority() {
        System.out.println("Default priority test");
    }

    @Test(priority = 1)
    public void testHighPriority() {
        System.out.println("High priority test");
    }
}
```

### Output:

```
Low priority test
Default priority test
High priority test
```

---

### Notes:

* **Priority Conflicts**: If two test methods have the same priority, TestNG will run them in an arbitrary order (since TestNG doesn't guarantee an order for methods with the same priority).
* **TestNG's Test Execution Order**: Priorities are used to control the order of execution. By default, TestNG doesn't guarantee the execution order unless priorities are explicitly set.
* **Test Method Dependencies**: You can also combine priorities with test dependencies. For example, if one test depends on the result of another, you can use the `dependsOnMethods` attribute along with priorities to control the execution sequence.

### Use Case:

Setting priorities is useful in scenarios where you want to ensure that certain tests (e.g., initialization tests) run before others, such as setting up a database connection before testing the functionality that relies on it.

---

## 63. What is the `dependsOnMethods` attribute in TestNG?

The `dependsOnMethods` attribute in **TestNG** is used to define **test dependencies**, allowing one test method to depend on the execution of one or more other test methods. This means that a test method will only be executed if the methods it depends on pass (or meet certain conditions).

### **How does `dependsOnMethods` work?**

* When you use `dependsOnMethods`, TestNG ensures that the dependent test methods are executed before the current test method.
* If any of the methods that a test depends on fail, the dependent test will **not** run.
* You can specify multiple methods in the `dependsOnMethods` attribute.

### **Syntax:**

```java
@Test(dependsOnMethods = {"methodName1", "methodName2"})
```

* Here, `methodName1` and `methodName2` are the names of the methods the current test depends on.
* The current test will only run if `methodName1` and `methodName2` pass.

---

### **Example Usage of `dependsOnMethods`:**

```java
import org.testng.annotations.Test;

public class TestNGDependsOnMethodsExample {

    @Test
    public void testFirst() {
        System.out.println("Executing first test.");
    }

    @Test(dependsOnMethods = {"testFirst"})
    public void testSecond() {
        System.out.println("Executing second test, depends on first test.");
    }

    @Test(dependsOnMethods = {"testFirst", "testSecond"})
    public void testThird() {
        System.out.println("Executing third test, depends on first and second tests.");
    }
}
```

### **Output:**

```
Executing first test.
Executing second test, depends on first test.
Executing third test, depends on first and second tests.
```

In this example:

* `testSecond` depends on `testFirst`. TestNG ensures that `testFirst` runs before `testSecond`.
* `testThird` depends on both `testFirst` and `testSecond`. It will only run if both of those tests pass.

---

### **Important Notes on `dependsOnMethods`:**

1. **Failure Behavior**:

    * If a method that another test depends on fails, the dependent test is **skipped**.
    * This is useful when you want to ensure that the tests are executed in a specific order and that tests which depend on others don’t run if the necessary preconditions (other tests) fail.

2. **Test Skipping**:

    * If a dependent method is skipped (due to failure or other reasons), the dependent test will be skipped as well.
    * You can view skipped tests in the test reports generated by TestNG.

3. **Multiple Dependencies**:

    * You can specify multiple methods in the `dependsOnMethods` array. The dependent test will only run if **all** specified methods pass.

4. **Cyclic Dependencies**:

    * TestNG does not allow **cyclic dependencies**, i.e., a method cannot depend on itself, either directly or indirectly, creating a circular dependency.

### **Example with Multiple Dependencies:**

```java
import org.testng.annotations.Test;

public class TestNGMultipleDependsExample {

    @Test
    public void testA() {
        System.out.println("Test A");
    }

    @Test
    public void testB() {
        System.out.println("Test B");
    }

    @Test(dependsOnMethods = {"testA", "testB"})
    public void testC() {
        System.out.println("Test C, depends on A and B.");
    }
}
```

### **Output:**

```
Test A
Test B
Test C, depends on A and B.
```

Here, `testC` depends on both `testA` and `testB`. Therefore, `testC` will only execute if both `testA` and `testB` pass.

---

### **Example with Test Failure and Skipping:**

```java
import org.testng.annotations.Test;

public class TestNGDependsOnFailureExample {

    @Test
    public void testX() {
        System.out.println("Executing test X.");
        // Simulating failure
        throw new RuntimeException("Test X failed!");
    }

    @Test(dependsOnMethods = {"testX"})
    public void testY() {
        System.out.println("Executing test Y.");
    }
}
```

### **Output:**

```
Executing test X.
Test X failed!
Executing test Y.
```

In this example, since `testX` fails, `testY` will **not** be executed, and it will be marked as skipped in the test report.

---

### **Advanced Use:**

You can combine `dependsOnMethods` with other attributes such as `enabled` (to disable certain tests dynamically), `priority`, and `groups` to create more sophisticated test flows.

### **Summary:**

* **`dependsOnMethods`** helps define test dependencies in TestNG.
* You can use it to ensure that certain tests run only after other tests pass.
* It helps manage the execution order and makes sure that essential tests are executed first.

---

## 64. What is TDD (Test-Driven Development)?

### **What is TDD (Test-Driven Development)?**

**Test-Driven Development (TDD)** is a software development methodology where tests are written before writing the actual code to implement the feature. It follows a **test-first** approach, and the key principle of TDD is that tests drive the development process. In TDD, the developer writes a test for a specific functionality, runs the test (which will initially fail), then writes the minimal amount of code to pass the test, and finally refactors the code. This cycle is repeated iteratively.

### **The TDD Cycle:**

TDD follows a very structured cycle known as **Red-Green-Refactor**:

1. **Red** – Write a **failing test**:

    * The first step is to write a test that defines a piece of functionality or behavior that you want to implement. Since you haven't written the code yet, the test will fail. This is the "Red" phase, as the test result will show as failing (red).

2. **Green** – Write the **minimum code to pass the test**:

    * Once the test is written and fails, the next step is to write just enough code to make the test pass. The code is not written with concern for the overall structure or optimization, only enough to pass the test. This is the "Green" phase, where the test will pass and show green.

3. **Refactor** – **Improve the code**:

    * After the test passes, the code may need some refactoring to improve its design, readability, or efficiency. Refactoring is done with the goal of improving the internal structure of the code without changing its external behavior. Since there is a test in place, you can safely refactor and ensure the functionality is still correct. This is the "Refactor" phase.

After these steps, you begin the cycle again for the next piece of functionality or feature.

### **Example of the TDD Cycle:**

Let’s go through a simple example of creating a calculator that adds two numbers using TDD.

#### **1. Red Phase (Write the Failing Test)**

You begin by writing a test for the "add" functionality:

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class CalculatorTest {
    
    @Test
    public void testAddition() {
        Calculator calculator = new Calculator();
        int result = calculator.add(2, 3);
        assertEquals(5, result);
    }
}
```

At this point, the `add` method doesn’t exist, so the test will fail (Red phase).

#### **2. Green Phase (Write Code to Pass the Test)**

Now, you write just enough code to make the test pass.

```java
public class Calculator {
    
    public int add(int a, int b) {
        return a + b;
    }
}
```

Running the test again will result in a **passing** test (Green phase).

#### **3. Refactor Phase (Refactor Code)**

After the test passes, you can refactor the code if necessary, for example, improving variable names or formatting. Since you have a test in place, you are confident that the behavior will remain correct after the refactor.

In this case, there might not be much to refactor, but if the code was more complex, you could clean it up while ensuring that the test still passes.

```java
// No changes needed in this simple example, but in larger projects, you might
// refactor the code to improve structure or efficiency.
```

After refactoring, you can re-run the tests to ensure everything still works as expected.

### **Benefits of TDD:**

1. **Early Bug Detection**:

    * Since tests are written first, bugs are caught early, usually in the development phase. This reduces the number of bugs in the production code.

2. **Simplified Code**:

    * TDD encourages writing only the code that is needed to pass the test, leading to cleaner and simpler code. This also helps reduce over-engineering.

3. **Regression Prevention**:

    * With a comprehensive test suite, any changes or refactoring of the code can be verified by rerunning the tests, ensuring that new changes don’t break existing functionality.

4. **Better Design**:

    * Writing tests first encourages developers to think carefully about how the code should work and how to design it in a modular, maintainable way. It often leads to better code structure and API design.

5. **Confidence in Refactoring**:

    * Since there are tests in place, developers can refactor their code with confidence, knowing that if anything breaks, the tests will catch it.

### **Challenges of TDD:**

1. **Initial Time Investment**:

    * Writing tests first can take more time initially, especially if the codebase is large or complex. However, this time is often compensated by fewer defects and a faster debugging process later.

2. **Requires Skill**:

    * Writing effective tests and following the TDD process requires discipline and experience. Developers need to know how to break down a feature into testable parts and design meaningful tests.

3. **Over-Testing**:

    * There is a potential to write unnecessary tests or overly granular tests that don’t provide significant value. This can make the test suite harder to maintain and slow down development.

4. **Not Ideal for All Types of Projects**:

    * TDD works best for well-defined requirements and functional code. For projects that involve a lot of experimentation or rapidly changing requirements, TDD can be more challenging.

### **TDD vs. Other Development Approaches**:

* **TDD vs. Traditional Development**:

    * Traditional development might involve writing the code first and then writing tests afterwards. This can result in incomplete or poor tests, leading to more bugs slipping through to production.

* **TDD vs. Behavior-Driven Development (BDD)**:

    * While TDD focuses on writing unit tests before code, **BDD** is more concerned with defining behaviors of the system in a human-readable format (often using tools like Cucumber) before writing the actual code. BDD encourages collaboration with stakeholders, while TDD is more focused on individual developer practice.

### **In Summary:**

Test-Driven Development (TDD) is a development methodology where tests are written first to drive the design of the code. It helps ensure that software is robust, reliable, and well-tested. The process follows the **Red-Green-Refactor** cycle: write a failing test, write just enough code to pass the test, and then refactor. TDD promotes early bug detection, better code quality, and confidence in refactoring, but it requires discipline and careful test design.

---

## 65. What are the steps in the TDD cycle?

The **Test-Driven Development (TDD)** cycle consists of three main steps, which are often referred to as the **Red-Green-Refactor** cycle. The cycle is repeated for each small unit of functionality, ensuring that tests guide the development of code. Here's a breakdown of the steps in the TDD cycle:

### **1. Red (Write a Failing Test)**:

* **Goal**: Write a test for a feature or functionality before writing the actual implementation.
* **Action**: Start by writing a test that describes the expected behavior of the feature. Since the functionality doesn't exist yet, this test will fail when it is run.
* **Why it's called "Red"**: The test fails because the feature hasn't been implemented yet, and the test results will show as red.

**Example**:

* You want to add a method `add(int a, int b)` to a calculator class that returns the sum of `a` and `b`.
* Write the test first:

```java
@Test
public void testAddition() {
    Calculator calculator = new Calculator();
    int result = calculator.add(2, 3);
    assertEquals(5, result);
}
```

### **2. Green (Write the Minimum Code to Pass the Test)**:

* **Goal**: Write just enough code to make the test pass.
* **Action**: After writing the test, implement the simplest code that will make the test pass. The goal is to make the test pass as quickly as possible without worrying about optimization or structure.
* **Why it's called "Green"**: The test will pass (show green) after the implementation is done.

**Example**:

* Implement the `add` method in the `Calculator` class:

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b; // Just enough code to pass the test
    }
}
```

### **3. Refactor (Improve the Code)**:

* **Goal**: Refactor the code to improve its design without changing its behavior.
* **Action**: After the test passes, clean up the code. You might want to improve its structure, readability, or efficiency. The goal is to make the code more maintainable and elegant, but without changing its functionality.
* **Why it's called "Refactor"**: The code is refactored to improve quality while ensuring the tests still pass.

**Example**:

* In this simple example, there may not be much to refactor, but as your codebase grows, you will typically clean up variable names, extract methods, or implement design patterns to improve the code structure.

### **Summary of the TDD Cycle**:

1. **Red**: Write a failing test for the new functionality.
2. **Green**: Write just enough code to make the test pass.
3. **Refactor**: Refactor the code to improve its design while ensuring the test still passes.

This cycle is repeated for every new feature or bug fix, allowing you to iteratively develop software with a solid set of tests ensuring the correctness of your code.

---

## 66. How is BDD (Behavior-Driven Development) different from TDD?

**Behavior-Driven Development (BDD)** and **Test-Driven Development (TDD)** are both agile software development practices that aim to improve the quality of code and ensure that the software meets the desired requirements. While they share similarities, they differ in their focus, communication style, and the tools used. Here’s a detailed comparison:

### **Key Differences Between BDD and TDD**:

| **Aspect**              | **TDD (Test-Driven Development)**                                                     | **BDD (Behavior-Driven Development)**                                                                   |
| ----------------------- | ------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| **Focus**               | Focuses on the implementation and correctness of the code itself.                     | Focuses on the behavior and features of the application, from the user's perspective.                   |
| **Test Level**          | Primarily unit tests that test small units of code (methods or functions).            | Tests the behavior of the system at a higher level (integration or functional tests).                   |
| **Test Writing**        | Tests are written in the form of assertions (e.g., `assertEquals()`, `assertTrue()`). | Tests are written in a natural language style, often using "Given-When-Then" format.                    |
| **Communication Style** | Developer-centric, focused on technical aspects of implementation.                    | Collaboration-centric, focused on communication between developers, testers, and business stakeholders. |
| **Syntax**              | Uses standard programming languages and testing frameworks (e.g., JUnit, NUnit).      | Uses human-readable syntax (e.g., Gherkin language) with tools like Cucumber or SpecFlow.               |
| **Collaboration**       | Primarily developer-driven.                                                           | Highly collaborative, involving both developers and non-technical stakeholders.                         |
| **Test Example**        | `assertEquals(5, calculator.add(2, 3));`                                              | `Given I have a calculator, When I add 2 and 3, Then the result should be 5.`                           |
| **Goal**                | Ensure the code is working as expected, focusing on technical correctness.            | Ensure the software meets the business or user expectations by validating behavior.                     |

---

### **1. Focus and Perspective**:

* **TDD** focuses on **testing small units** of the system (such as individual methods or functions) to ensure that the implementation works correctly. It is developer-driven and primarily concerned with **code correctness**.
* **BDD** focuses on **describing the desired behavior** of the system from the perspective of the user or business. BDD emphasizes **collaboration** among developers, testers, and business stakeholders. The focus is on **how the system should behave** rather than just how it is implemented.

### **2. Test Level**:

* **TDD** typically involves writing **unit tests** that check small portions of code in isolation, such as individual methods, classes, or functions.
* **BDD** generally involves writing **higher-level acceptance tests** or **functional tests** that check the behavior of the system from the user's perspective. These tests usually span multiple components or features.

### **3. Test Writing Style**:

* **TDD** tests are written in a typical programming syntax, using assertions like `assertEquals()`, `assertTrue()`, etc., to check expected results against actual outputs.

  **Example (TDD):**

  ```java
  @Test
  public void testAdd() {
      Calculator calculator = new Calculator();
      assertEquals(5, calculator.add(2, 3));
  }
  ```

* **BDD** tests are written in a more **natural language style** using the **Given-When-Then** format to describe the system’s behavior, which is more understandable for non-developers as well.

  **Example (BDD):**

  ```gherkin
  Given I have a calculator
  When I add 2 and 3
  Then the result should be 5
  ```

  BDD tools such as **Cucumber** or **SpecFlow** allow writing tests in this **human-readable** syntax and then map them to executable code.

### **4. Collaboration and Communication**:

* **TDD** is generally **developer-centric**, with developers writing and maintaining the tests. It does not emphasize collaboration with non-technical stakeholders as much as BDD.
* **BDD**, on the other hand, encourages **collaboration between developers, testers, and business stakeholders**. The tests written in BDD are designed to be easily understood by all members of the team, including product owners and other non-technical stakeholders. The goal is to **align the development process with business requirements**.

### **5. Tools**:

* **TDD** uses tools like **JUnit**, **NUnit**, or **TestNG** for writing unit tests.
* **BDD** uses tools like **Cucumber**, **SpecFlow**, or **Behave** for writing behavior-driven tests. These tools translate human-readable scenarios into automated tests.

### **6. Test Examples**:

* **TDD Example (JUnit)**: Testing a simple calculator method.

  ```java
  @Test
  public void testAdd() {
      Calculator calculator = new Calculator();
      assertEquals(5, calculator.add(2, 3));  // Test driven by implementation
  }
  ```

* **BDD Example (Cucumber/Gherkin)**: Testing the behavior of a calculator.

  ```gherkin
  Feature: Addition functionality of the calculator
    Scenario: Adding two numbers
      Given I have a calculator
      When I add 2 and 3
      Then the result should be 5
  ```

  **Cucumber Step Definition**:

  ```java
  @Given("I have a calculator")
  public void iHaveACalculator() {
      // setup code
  }

  @When("I add {int} and {int}")
  public void iAddAnd(int a, int b) {
      result = calculator.add(a, b);
  }

  @Then("the result should be {int}")
  public void theResultShouldBe(int expectedResult) {
      assertEquals(expectedResult, result);
  }
  ```

### **7. Goal**:

* The goal of **TDD** is to **ensure that the code works correctly** by writing tests first, writing just enough code to pass those tests, and then refactoring the code to improve its design.
* The goal of **BDD** is to ensure that the software **meets business and user expectations** by defining behaviors in a natural language and validating those behaviors with automated tests.

---

### **Summary:**

* **TDD** (Test-Driven Development) is a developer-centric process that focuses on writing unit tests before the implementation code to ensure correctness and catch bugs early. It's primarily concerned with **code correctness** at a low level (unit testing).

* **BDD** (Behavior-Driven Development) is a more collaborative approach that focuses on defining the **behavior** of the application from the user's or business's perspective. It encourages collaboration between developers, testers, and stakeholders and uses a **natural language** to describe system behavior, often using tools like **Cucumber** or **SpecFlow**.

In short, while **TDD** focuses on **testing small units of code**, **BDD** focuses on **defining and validating business-driven behavior** in a human-readable format.

---

## 67. What are the benefits of TDD?

**Test-Driven Development (TDD)** offers several benefits that improve the quality, maintainability, and reliability of software. Here are some of the key benefits:

### 1. **Improved Code Quality**:

* **Early Bug Detection**: Since tests are written before the code, you immediately identify issues during development rather than later in the process. This prevents bugs from accumulating and helps identify problems early.
* **Simpler Code**: TDD encourages writing just enough code to pass the tests. This avoids over-engineering and ensures that only the necessary code is written, leading to simpler and more efficient designs.
* **Code Design and Modularity**: TDD often results in better-structured code. Developers need to think about the system in small, manageable parts, leading to better modularization, separation of concerns, and testable code.

### 2. **Faster Debugging**:

* **Test Coverage**: With TDD, you create a comprehensive suite of tests as you develop the software. When bugs occur, you can quickly run the tests to identify where things went wrong, which speeds up the debugging process.
* **Reduces Debugging Time**: Since tests are continuously validated, problems can be traced to their source faster. This eliminates the need to spend long periods figuring out where and why things broke.

### 3. **Confidence in Code Changes and Refactoring**:

* **Safe Refactoring**: With a solid suite of unit tests in place, you can refactor your code with confidence, knowing that any changes you make will be checked by the tests, which reduces the risk of introducing new bugs.
* **Ensures Functionality Is Maintained**: When refactoring or adding new features, the tests help ensure that existing functionality is not broken. Any regression can be quickly identified by rerunning the tests.

### 4. **Better Documentation**:

* **Living Documentation**: The tests themselves serve as a form of documentation, describing the behavior of the code. This makes it easier for other developers (or even future you) to understand the code, its expected behavior, and its boundaries.
* **Describes Intent**: The tests describe what the code is supposed to do, which helps others (and your future self) understand the **intent** behind the code, making the code more understandable and maintainable.

### 5. **Facilitates Incremental Development**:

* **Small, Manageable Steps**: TDD encourages the development of code in small increments. You write a failing test, implement just enough code to pass it, and then refactor. This iterative approach makes the development process more manageable and less overwhelming.
* **Faster Feedback**: With each small change, you receive quick feedback through the tests, allowing you to make adjustments and improvements early in the process.

### 6. **Helps with Writing Testable Code**:

* **Test-Driven Design**: Writing tests first forces you to think about the design and structure of the code before implementation. This leads to code that is **more modular**, **decoupled**, and **easier to test**.
* **Loose Coupling**: By focusing on testable units of code, TDD encourages the design of code that is loosely coupled and highly cohesive, which improves maintainability and extensibility.

### 7. **Better Software Maintenance**:

* **Reduces the Cost of Change**: When writing code in small, testable increments, any future changes are easier to implement. You are more likely to catch issues early, preventing technical debt from accumulating.
* **Prevents Regression**: Automated tests ensure that once a feature works, it continues to work even after changes are made. This helps prevent regression bugs, which are issues that reappear after code changes.

### 8. **Promotes Continuous Integration**:

* **Automated Testing**: TDD works well with Continuous Integration (CI) systems, as tests can be automatically run whenever code is checked into version control. This ensures that the codebase is always in a working state and reduces integration problems.
* **Quick Feedback in CI Pipelines**: With a robust test suite, you can catch integration or functional issues early, preventing bugs from reaching production.

### 9. **Improved Developer Discipline and Focus**:

* **Test-First Mindset**: TDD forces developers to write tests first, which encourages better planning and design upfront. This often leads to more thoughtful, deliberate coding decisions and can reduce the temptation to rush through implementation.
* **Clear Requirements**: Since the tests are written before the code, developers have a clearer understanding of the requirements and expectations of the functionality they're implementing.

### 10. **Helps with Collaboration**:

* **Better Communication**: TDD encourages team members to discuss the behavior and requirements of features before coding begins. This results in better alignment on functionality and design and reduces misunderstandings.
* **Code Reviews and Pair Programming**: TDD can also aid code reviews and pair programming, as test cases make it easier to see whether the code meets the requirements.

### 11. **Prevents Feature Creep**:

* **Focus on the Requirements**: Because you write tests for small pieces of functionality, TDD helps keep you focused on delivering the requirements one step at a time. This prevents **feature creep**, where new features are added without proper planning or consideration.

---

### **Summary of Benefits of TDD**:

* **Higher code quality** and **early bug detection**.
* **Simplified, maintainable** code with **clearer design**.
* **Faster debugging** and **fewer defects** in production.
* **Confidence in refactoring** and making code changes.
* **Living documentation** that describes the expected behavior of the code.
* **Increased collaboration** and better communication among teams.
* **Improved maintainability** and **testability** of the software.

While **TDD** requires an upfront investment in writing tests and may seem time-consuming initially, the long-term benefits significantly outweigh the costs, especially in terms of software quality, maintainability, and developer productivity.

---

## 68. What tools are used for BDD in Java?

In **Behavior-Driven Development (BDD)** for Java, several tools are used to help developers write, execute, and maintain behavior-driven tests in a natural language style, often involving collaboration with stakeholders. Here are some of the most popular tools used for BDD in Java:

### 1. **Cucumber**:

* **Overview**: Cucumber is one of the most widely used BDD tools in the Java ecosystem. It allows you to write tests in a human-readable format using **Gherkin syntax** (Given-When-Then), which can then be mapped to Java methods for execution.
* **How it works**: Cucumber reads feature files written in Gherkin, then runs the tests using step definitions in Java. It integrates easily with testing frameworks like **JUnit** and **TestNG**.
* **Advantages**:

    * Enables collaboration between technical and non-technical team members.
    * Supports **Gherkin syntax**, which is simple to write and understand.
    * Integrates with existing test automation frameworks.

**Example**:

```gherkin
Feature: Addition functionality of calculator
  Scenario: Adding two numbers
    Given I have a calculator
    When I add 2 and 3
    Then the result should be 5
```

**Step Definition in Java**:

```java
@Given("I have a calculator")
public void iHaveACalculator() {
    calculator = new Calculator();
}

@When("I add {int} and {int}")
public void iAddAnd(int a, int b) {
    result = calculator.add(a, b);
}

@Then("the result should be {int}")
public void theResultShouldBe(int expectedResult) {
    assertEquals(expectedResult, result);
}
```

**Maven Dependency**:

```xml
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-java</artifactId>
    <version>YOUR_CUCUMBER_VERSION</version>
    <scope>test</scope>
</dependency>
```

---

### 2. **JBehave**:

* **Overview**: JBehave is another popular BDD framework for Java that allows you to write tests in a story format. It is similar to Cucumber but has its own set of conventions and tools.
* **How it works**: JBehave uses stories written in plain text, and the scenarios in those stories are executed with Java step definitions.
* **Advantages**:

    * Focuses on simplicity and ease of use.
    * Can run with various other Java testing frameworks like **JUnit** and **TestNG**.
    * Provides tools for managing feature files and generating reports.

**Example (Story)**:

```plaintext
Scenario: Adding two numbers
  Given a calculator
  When I add 2 and 3
  Then the result should be 5
```

**Step Definition in Java**:

```java
public class CalculatorSteps {
    private Calculator calculator;
    private int result;

    @Given("a calculator")
    public void givenACalculator() {
        calculator = new Calculator();
    }

    @When("I add $a and $b")
    public void whenIAdd(int a, int b) {
        result = calculator.add(a, b);
    }

    @Then("the result should be $expectedResult")
    public void thenTheResultShouldBe(int expectedResult) {
        assertEquals(expectedResult, result);
    }
}
```

**Maven Dependency**:

```xml
<dependency>
    <groupId>org.jbehave</groupId>
    <artifactId>jbehave-core</artifactId>
    <version>YOUR_JBEHAVE_VERSION</version>
    <scope>test</scope>
</dependency>
```

---

### 3. **Spock Framework**:

* **Overview**: Spock is a testing framework for Java and Groovy that combines features of both **unit testing** and **BDD**. It is especially popular in Groovy-based applications but also works well in Java.
* **How it works**: Spock allows you to write **specifications** in a Groovy-like syntax (which can also be used with Java). It integrates naturally with **JUnit** and supports both **BDD-style** and **traditional testing**.
* **Advantages**:

    * Groovy-based syntax makes the test cases concise and expressive.
    * Supports **BDD-style** testing with a focus on behavior.
    * Provides built-in features like **data-driven tests** and **mocking**.

**Example**:

```groovy
class CalculatorSpec extends Specification {
    def "should add two numbers"() {
        given: "a calculator"
        def calculator = new Calculator()

        when: "I add 2 and 3"
        def result = calculator.add(2, 3)

        then: "the result should be 5"
        result == 5
    }
}
```

**Maven Dependency**:

```xml
<dependency>
    <groupId>org.spockframework</groupId>
    <artifactId>spock-core</artifactId>
    <version>YOUR_SPOCK_VERSION</version>
    <scope>test</scope>
</dependency>
```

---

### 4. **Citrus Framework**:

* **Overview**: Citrus is an integration testing framework that supports **BDD** and **message-based testing**. It is particularly useful for testing enterprise integration patterns, APIs, and messaging systems.
* **How it works**: Citrus enables writing tests that simulate communication between systems or services in a BDD-style format.
* **Advantages**:

    * Specifically designed for integration and contract testing.
    * Supports **message-driven systems**, which makes it ideal for API, web service, and messaging tests.
    * Allows you to write tests in **plain English**, which is useful for collaboration.

**Example**:

```gherkin
Feature: Send a message to the user service
  Scenario: Validating a user registration message
    Given I have a message with valid user details
    When I send the message to the user service
    Then the user service should return a success response
```

**Maven Dependency**:

```xml
<dependency>
    <groupId>org.citrusframework</groupId>
    <artifactId>citrus-core</artifactId>
    <version>YOUR_CITRUS_VERSION</version>
    <scope>test</scope>
</dependency>
```

---

### 5. **Galen Framework**:

* **Overview**: Galen is used for **automated testing of web applications**, especially for UI and layout testing, and supports a BDD approach.
* **How it works**: Galen uses a **Gherkin-like syntax** to define behavior for web UI tests and integrates with Selenium to run the tests.
* **Advantages**:

    * Focuses on UI and layout testing.
    * BDD-style tests are written in simple text.
    * Integrates well with Selenium for web testing.

**Example (Feature)**:

```gherkin
Feature: Validate web page layout
  Scenario: Validate the layout of the home page
    Given I open the home page
    When I check the layout of the page
    Then the header should be aligned to the left
```

**Maven Dependency**:

```xml
<dependency>
    <groupId>com.galenframework</groupId>
    <artifactId>galen-java</artifactId>
    <version>YOUR_GALEN_VERSION</version>
    <scope>test</scope>
</dependency>
```

---

### **Summary of Popular BDD Tools for Java**:

* **Cucumber**: The most widely used BDD tool for Java, using Gherkin syntax to write feature files.
* **JBehave**: Another popular BDD framework similar to Cucumber, using its own story format.
* **Spock Framework**: A Groovy-based testing framework that supports both BDD and traditional unit testing.
* **Citrus Framework**: Specializes in integration and contract testing, with BDD features for message-driven systems.
* **Galen Framework**: Focuses on BDD-style tests for web UI and layout validation, often used with Selenium.

These tools help facilitate collaboration between developers, testers, and stakeholders, ensuring that the software's behavior matches the expected requirements in a simple, understandable way.

---

## 69. What is Cucumber and how does it work with Spring?

### **What is Cucumber?**

**Cucumber** is an open-source tool used for **Behavior-Driven Development (BDD)**. It allows developers, testers, and even non-technical stakeholders to write and understand automated acceptance tests in **plain language**. The tests are written in **Gherkin syntax**, a natural language format that uses keywords like **Given**, **When**, and **Then**. These tests can describe the behavior of an application in a way that is easily understandable by non-developers (business analysts, product owners, etc.).

#### **How Does Cucumber Work?**

Cucumber follows a few key concepts:

1. **Feature Files**:

    * These are plain text files written using **Gherkin syntax**, where you describe the behavior of your application.
    * The syntax is simple and readable by both technical and non-technical people.

2. **Step Definitions**:

    * The **Step Definitions** in Java are the code that maps the steps written in Gherkin to actual executable code.
    * Each **Given**, **When**, and **Then** in a Gherkin feature file corresponds to a method in the Java code that executes the associated action.

3. **Test Runner**:

    * The **Test Runner** class in Java executes the tests. It can be set up using **JUnit** or **TestNG** as the execution framework.

---

### **Gherkin Syntax Example** (Feature File)

The following is an example of a feature file written in **Gherkin syntax** for a simple login functionality:

```gherkin
Feature: Login functionality
  Scenario: Successful login with valid credentials
    Given I am on the login page
    When I enter a valid username and password
    Then I should be redirected to the dashboard

  Scenario: Unsuccessful login with invalid credentials
    Given I am on the login page
    When I enter an invalid username and password
    Then I should see an error message
```

---

### **How Cucumber Works with Spring**

When using Cucumber with **Spring**, you typically want to run **Spring Boot applications** or **Spring-based applications** with Cucumber to test their behavior.

Here’s a breakdown of how Cucumber integrates with Spring:

#### 1. **Spring Test Support**

Cucumber can run in the context of a **Spring Boot** application by leveraging **Spring's testing support**. This allows you to interact with Spring beans, configurations, and the application context during tests.

* You can use Spring to inject beans into Cucumber step definitions.
* You can also set up a Spring application context in Cucumber tests for more realistic integration tests.

#### 2. **Cucumber with Spring Boot Integration**:

To use **Cucumber with Spring Boot**, you need to set up a few dependencies and annotations.

#### **Steps to integrate Cucumber with Spring Boot:**

1. **Add Dependencies**:
   Add Cucumber and Spring Boot test dependencies to your **`pom.xml`** (for Maven) or **`build.gradle`** (for Gradle).

   **Maven Dependency Example**:

   ```xml
   <dependencies>
       <!-- Cucumber dependencies -->
       <dependency>
           <groupId>io.cucumber</groupId>
           <artifactId>cucumber-spring</artifactId>
           <version>YOUR_CUCUMBER_VERSION</version>
           <scope>test</scope>
       </dependency>
       <dependency>
           <groupId>io.cucumber</groupId>
           <artifactId>cucumber-java</artifactId>
           <version>YOUR_CUCUMBER_VERSION</version>
           <scope>test</scope>
       </dependency>
       <dependency>
           <groupId>io.cucumber</groupId>
           <artifactId>cucumber-spring</artifactId>
           <version>YOUR_CUCUMBER_VERSION</version>
           <scope>test</scope>
       </dependency>

       <!-- Spring Boot Test dependency -->
       <dependency>
           <groupId>org.springframework.boot</groupId>
           <artifactId>spring-boot-starter-test</artifactId>
           <scope>test</scope>
       </dependency>
   </dependencies>
   ```

2. **Write Feature Files**:
   Write Gherkin-style feature files to describe the behavior you want to test. Place these files in the `src/test/resources` directory.

   **Example Feature File (`login.feature`)**:

   ```gherkin
   Feature: Login functionality
     Scenario: User logs in with valid credentials
       Given User is on the login page
       When User enters valid username and password
       Then User is redirected to the dashboard
   ```

3. **Create Step Definitions**:
   In **Step Definitions**, you map the steps written in the feature file to actual methods in Java. Spring beans can be injected into these step definition classes.

   **Step Definition Example**:

   ```java
   @SpringBootTest
   @CucumberContextConfiguration
   @ContextConfiguration(classes = YourSpringBootApplication.class)
   public class StepDefinitions {

       @Autowired
       private YourService yourService; // Inject Spring beans into step definitions.

       @Given("User is on the login page")
       public void givenUserIsOnLoginPage() {
           // Code to navigate to login page (if needed).
       }

       @When("User enters valid username and password")
       public void whenUserEntersCredentials() {
           // Simulate user entering credentials and clicking login.
       }

       @Then("User is redirected to the dashboard")
       public void thenUserIsRedirectedToDashboard() {
           // Verify user is on the dashboard.
           assertTrue(yourService.isLoggedIn());
       }
   }
   ```

4. **Cucumber Test Runner**:
   Create a Cucumber test runner class that hooks into Spring's application context and triggers Cucumber to execute the tests.

   **Test Runner Class**:

   ```java
   @RunWith(Cucumber.class)
   @CucumberOptions(
       features = "classpath:features", // Path to your feature files
       plugin = {"pretty", "html:target/cucumber-reports"},
       glue = {"com.yourpackage.stepdefinitions"} // The package containing your step definitions
   )
   @EnableAutoConfiguration
   public class CucumberTest {
   }
   ```

5. **Run the Tests**:

    * You can now run your Cucumber tests like a regular **JUnit** test.
    * The Spring context is loaded, and the Cucumber steps are executed with real Spring beans and services.

#### 3. **Key Annotations in Spring with Cucumber**:

* **@SpringBootTest**: This annotation is used to load the full Spring application context for the test.
* **@CucumberContextConfiguration**: This tells Cucumber to load the Spring context configuration and enables Spring beans to be injected into step definition classes.
* **@ContextConfiguration**: You use this to explicitly specify the Spring configuration class (usually the main application class).
* **@CucumberOptions**: You use this to specify the location of feature files and glue code (step definitions).

---

### **How Cucumber Works with Spring: Workflow**

1. **Feature File**: You write the behavior of your system in a simple, understandable format (using Gherkin syntax).
2. **Step Definitions**: You map each Gherkin step (Given, When, Then) to Java code that interacts with the Spring Boot application.
3. **Cucumber Test Runner**: The runner orchestrates the execution of your tests using JUnit, integrating with Spring for dependency injection and context setup.
4. **Spring Boot Context**: Spring beans and services are available to your step definitions, which means your Cucumber tests can interact with real application components (repositories, services, controllers, etc.).
5. **Execution**: Cucumber will run the scenarios, using the mapped Java methods in the step definitions, ensuring the business logic behaves as expected.

---

### **Advantages of Using Cucumber with Spring Boot**:

1. **Readable Tests**: Since feature files are written in Gherkin syntax, they are highly readable and can be understood by both developers and non-developers (e.g., business analysts, product owners).

2. **Seamless Integration**: Cucumber works seamlessly with Spring Boot, allowing you to write **integration-level tests** that interact with the actual Spring beans, application context, and database if required.

3. **Collaboration**: Encourages collaboration between developers, testers, and business stakeholders. It bridges the communication gap by using a language that everyone understands.

4. **Comprehensive Testing**: With Cucumber and Spring Boot, you can test both **unit-level** and **end-to-end** behavior, ensuring that the system works as expected from a user perspective.

---

### **Conclusion**:

Cucumber is a powerful tool for Behavior-Driven Development (BDD) that can be integrated with Spring Boot to write and execute automated tests in a readable format. It facilitates collaboration, improves code quality, and provides a clear understanding of the system's behavior. By combining Cucumber with Spring Boot, you can create robust integration tests that validate the behavior of your application in a real-world context.

---

## 70. How do you write feature files in BDD?

### **How to Write Feature Files in BDD**

In **Behavior-Driven Development (BDD)**, feature files are written using a domain-specific language called **Gherkin**. Gherkin is designed to be easily readable by both technical and non-technical stakeholders, such as developers, testers, business analysts, and product owners.

Feature files in BDD describe the behavior of an application in a structured, plain-language format, enabling teams to write scenarios that describe system behavior from the user's perspective.

---

### **Key Components of a Gherkin Feature File**

1. **Feature**: A feature is a description of a part of the application you want to test. It should represent a business functionality.

2. **Scenario**: A scenario is a specific example of how the feature should behave under certain conditions. Each scenario contains steps to simulate a particular use case.

3. **Given**, **When**, **Then**: These are the main Gherkin keywords used to define the steps in a scenario.

    * **Given**: Sets up the initial context or preconditions for the scenario.
    * **When**: Describes the action or event that triggers the behavior.
    * **Then**: Defines the expected outcome or result.

4. **And**, **But**: These keywords are used for connecting additional steps, especially when there are multiple conditions or actions.

5. **Examples**: These are used in **Scenario Outlines** to run the same scenario with different sets of data.

---

### **Gherkin Syntax Example** (Feature File)

Here is an example of how to write a **Feature File** in BDD using Gherkin syntax:

#### **Feature File for User Login**

```gherkin
Feature: User login functionality
  In order to access the user dashboard
  As a registered user
  I want to log in to the application

  Scenario: Successful login with valid credentials
    Given I am on the login page
    When I enter valid credentials for username and password
    Then I should be redirected to the dashboard

  Scenario: Unsuccessful login with invalid credentials
    Given I am on the login page
    When I enter invalid credentials for username and password
    Then I should see an error message

  Scenario: Successful login with a remember me option
    Given I am on the login page
    When I enter valid credentials and check the remember me option
    Then I should be redirected to the dashboard
    And I should stay logged in after closing the browser

  Scenario Outline: Unsuccessful login attempts
    Given I am on the login page
    When I enter "<username>" and "<password>"
    Then I should see "<error_message>"

    Examples:
      | username        | password     | error_message        |
      | invalidUser1    | wrongPass1   | Invalid credentials |
      | invalidUser2    | wrongPass2   | Invalid credentials |
```

---

### **Explanation of the Components in the Example**:

1. **Feature**:

    * `Feature: User login functionality`: Describes the feature being tested. In this case, it's testing the login functionality of an application.

2. **Scenario**:

    * `Scenario: Successful login with valid credentials`: Describes a specific situation where the user is able to successfully log in with valid credentials.
    * `Scenario: Unsuccessful login with invalid credentials`: Describes a situation where the login fails due to invalid credentials.
    * `Scenario: Successful login with a remember me option`: Describes a scenario where the login is successful, and the "remember me" option is checked.

3. **Given-When-Then** Steps:

    * `Given I am on the login page`: Describes the initial state or context, which is the login page.
    * `When I enter valid credentials for username and password`: Describes the action the user performs, which is entering valid credentials.
    * `Then I should be redirected to the dashboard`: Describes the expected result or outcome after entering the valid credentials.

4. **Scenario Outline**:

    * `Scenario Outline: Unsuccessful login attempts`: A scenario outline is used to run the same scenario with multiple sets of data.
    * `Examples`: The examples table defines different combinations of `username`, `password`, and `error_message` to test various login attempts.

---

### **Gherkin Syntax for Multiple Scenarios**

You can write **multiple scenarios** under the same feature file. Each scenario tests a specific behavior or use case of the application. The scenarios help to break down different workflows of the feature.

#### Example:

```gherkin
Feature: User Profile Management
  As a registered user
  I want to update my user profile information

  Scenario: Update username successfully
    Given I am logged into my account
    When I change my username to "newUser123"
    Then My username should be updated to "newUser123"

  Scenario: Update email address with invalid format
    Given I am logged into my account
    When I change my email to "invalidEmail"
    Then I should see an error message "Invalid email format"
```

---

### **Steps to Write a Feature File in BDD**

Here’s a structured approach for writing feature files in BDD:

1. **Identify the Feature**:

    * Understand the user stories or functionalities you are developing and testing.
    * Write a **Feature** description that explains the goal and benefit from the user's perspective.

2. **Write Scenarios**:

    * For each user story or test case, identify specific **scenarios** that describe different aspects of the behavior.
    * Each scenario should describe a simple, testable use case.

3. **Define Given-When-Then Steps**:

    * Write clear **Given** steps to set up the initial context.
    * Write **When** steps to describe actions or events that trigger the behavior.
    * Write **Then** steps to define the expected outcome.
    * If necessary, use **And** or **But** for additional details in the steps.

4. **Use Scenario Outlines for Data-Driven Tests**:

    * If you need to run the same scenario with different data sets, use **Scenario Outline** and provide test data in an **Examples** table.

5. **Keep It Simple and Focused**:

    * Focus on business logic. Keep the scenarios simple and specific.
    * Avoid technical details in the feature file; this is meant for business stakeholders to understand.

---

### **Best Practices for Writing Feature Files in BDD**

1. **Use Plain Language**: The language used in feature files should be simple and understandable for all stakeholders, including non-technical ones.
2. **Make Scenarios Independent**: Each scenario should be independent and self-contained. They should be able to run on their own.
3. **Describe Expected Behavior**: Focus on describing the expected behavior of the application, not how it is implemented.
4. **Avoid Too Many Steps**: Keep scenarios short and clear. If a scenario gets too long, consider splitting it into smaller ones.
5. **Use Concrete Examples**: Whenever possible, use real data and concrete examples to make the scenario more realistic and relatable.

---

### **Conclusion**

Writing **Feature Files** in **BDD** helps in defining application behavior in an easily understandable format for all team members. Using **Gherkin syntax** with **Given**, **When**, and **Then** steps, you can describe the behavior of an application from the user's perspective, making it easier to collaborate and automate tests that validate the system's behavior. The main goal is to ensure that all stakeholders, from developers to business analysts, can understand the tests and that the tests are directly aligned with business goals.

---

## 71. What is code coverage in testing?

### **What is Code Coverage in Testing?**

**Code coverage** is a software metric used to measure the percentage of your code that is exercised (executed) by a set of tests. In other words, it quantifies how much of the source code is being tested through your automated tests (unit tests, integration tests, etc.). The goal is to ensure that the tests you write are covering as much of your application code as possible, which can help detect bugs, edge cases, and untested parts of your codebase.

Code coverage provides insight into the effectiveness of your testing efforts, but it should not be the only metric used to assess the quality of your tests. Just because a large percentage of your code is covered by tests does not guarantee that your tests are meaningful or that your application is bug-free.

### **Types of Code Coverage**

Here are some common types of code coverage:

1. **Line Coverage**:

    * This metric measures the percentage of lines of code that have been executed by your tests. It focuses on whether each line in the code is covered by at least one test case.
    * **Example**: If your method has 10 lines of code and your tests cover 8 lines, your line coverage is 80%.

2. **Branch Coverage**:

    * Branch coverage measures whether both the true and false branches of conditional statements (such as `if`, `else`, and `switch` statements) have been executed during testing.
    * **Example**: If there is an `if` statement, branch coverage ensures that the test cases have executed both the `if` block and the `else` block.

3. **Function Coverage**:

    * This metric tracks whether each function or method in your code has been called during testing. It checks whether all functions in the code are being invoked by your test suite.
    * **Example**: If a method is defined in the code but never called by the test, it will not be covered.

4. **Condition Coverage**:

    * Condition coverage ensures that each individual condition in a decision has been evaluated both to `true` and `false`.
    * **Example**: In a condition like `if (a && b)`, condition coverage ensures both `a` and `b` are tested in both `true` and `false` conditions.

5. **Path Coverage**:

    * Path coverage measures whether all possible execution paths through a program (e.g., all combinations of branches) have been exercised by the tests. This is more comprehensive than branch coverage but can be difficult to achieve due to the large number of potential paths in complex code.
    * **Example**: If a function contains multiple if-else blocks and loops, path coverage ensures that all unique combinations of decisions are tested.

6. **Loop Coverage**:

    * Loop coverage measures whether loops in your code (for, while, do-while) are tested for both zero iterations (empty loop) and multiple iterations.
    * **Example**: If a `for` loop runs 3 times, loop coverage ensures that the test checks the loop's behavior for 0, 1, and 3 iterations.

---

### **How to Measure Code Coverage?**

To measure code coverage, you use **code coverage tools** that instrument your code and report on the percentage of lines or branches executed during test runs. These tools can generate detailed reports that show which parts of the code were tested and which were not.

#### **Popular Code Coverage Tools for Java**:

1. **JaCoCo**:

    * A popular code coverage library for Java projects. It integrates well with Maven and Gradle and generates detailed reports.
    * It supports **line**, **branch**, and **method** coverage, among other metrics.

2. **Cobertura**:

    * Another popular code coverage tool for Java that supports **line** and **branch** coverage.
    * Cobertura provides detailed reports and integrates well with build tools like Maven.

3. **Emma**:

    * A code coverage tool for Java applications that supports **method**, **line**, and **block** coverage.
    * Emma can generate various types of reports, including HTML and XML formats.

4. **JUnit + IntelliJ IDEA**:

    * Integrated code coverage tools are available in popular IDEs like IntelliJ IDEA. When running tests with coverage enabled, the IDE shows which lines of code were covered.

5. **SonarQube**:

    * A popular tool for continuous inspection of code quality. It integrates with build systems and displays code coverage metrics as part of a broader quality report.

---

### **Why is Code Coverage Important?**

1. **Ensures Test Thoroughness**:

    * Code coverage helps verify that your test suite exercises the code you're interested in testing. High coverage suggests that more of the code is tested.

2. **Identifies Untested Areas**:

    * It can highlight areas of the code that are not covered by tests, allowing developers to write tests to fill those gaps.

3. **Quality Assurance**:

    * High code coverage can help identify bugs early in the development cycle. With better coverage, you can be more confident that your code behaves as expected.

4. **Improves Code Design**:

    * Writing tests often encourages developers to write cleaner, modular code that is easier to test. For instance, functions or methods that are difficult to test may need refactoring to make them more testable.

5. **Automated Continuous Integration (CI)**:

    * Code coverage tools can be integrated with CI pipelines to enforce coverage thresholds. For example, you can set up your CI server to fail if the coverage drops below a certain percentage.

---

### **What Code Coverage Does Not Guarantee**

1. **Quality of Tests**:

    * Code coverage metrics do not measure the **quality** of the tests. A high percentage of code coverage doesn't mean that your tests are well-designed or comprehensive. You can have 100% code coverage but still miss critical edge cases if your tests are poorly written.

2. **Behavioral Validation**:

    * Code coverage only tells you which code paths were executed, but it does not validate whether the application behaves as expected in those scenarios.

3. **Test Redundancy**:

    * Having high code coverage might lead to redundant tests if the tests are not carefully designed. For example, testing the same method multiple times in the same way can artificially inflate coverage without adding real value.

4. **Complexity in Path Coverage**:

    * Achieving **100% path coverage** can be very challenging in real-world applications, especially for applications with many conditional branches or loops. Testing every possible path through the application is not always feasible.

---

### **Best Practices for Code Coverage**

1. **Target Practical Coverage Levels**:

    * Aim for **high code coverage**, but focus on **important code paths**. Having 100% code coverage might not be feasible, so target a practical level (e.g., 80-90%) that ensures critical features and edge cases are tested.

2. **Write Meaningful Tests**:

    * Rather than just aiming for high coverage, focus on writing **meaningful** tests that validate the core functionality of your application, including edge cases.

3. **Combine Code Coverage with Other Metrics**:

    * Use code coverage in combination with other testing metrics like **mutation testing**, which assesses the quality of your tests by introducing small changes (mutations) and checking if your tests catch them.

4. **Test Core Business Logic**:

    * Ensure the core business logic and critical paths are well covered. This typically includes user authentication, data validation, and key features that affect user experience.

5. **Review Uncovered Code**:

    * Pay attention to uncovered code that is critical or complex. This can be a sign of areas where additional testing or refactoring is needed.

6. **Automate and Integrate with CI**:

    * Integrate code coverage tools into your **continuous integration (CI)** pipeline to track coverage and maintain a consistent level of testing.

---

### **Conclusion**

**Code coverage** is a valuable metric for ensuring your tests exercise your application's code, helping to find bugs and improving code quality. However, it should not be the sole measure of the effectiveness of your testing efforts. A balanced approach that focuses on writing meaningful tests and testing critical code paths, combined with code coverage tools, will provide the best results in ensuring software quality.

---

## 72. What is the use of JaCoCo?

### **What is JaCoCo?**

**JaCoCo** (Java Code Coverage) is a popular, open-source code coverage library for Java applications. It is used to measure and report the percentage of code that is exercised (executed) by your test cases. JaCoCo provides detailed coverage metrics that help developers and teams assess how thoroughly their code is tested.

JaCoCo integrates seamlessly with popular build tools like **Maven** and **Gradle** and can generate code coverage reports in various formats such as **HTML**, **XML**, and **CSV**.

### **Key Features of JaCoCo:**

1. **Code Coverage Measurement**:

    * JaCoCo tracks which lines of code, methods, and branches are executed by the tests, helping you understand how well your code is covered.

2. **Integration with Build Tools**:

    * JaCoCo integrates well with build tools like **Maven** and **Gradle**. You can easily configure it in your build lifecycle, making it simple to run coverage checks as part of your CI/CD pipeline.

3. **Comprehensive Coverage Metrics**:

    * JaCoCo provides detailed reports on:

        * **Line Coverage**: Tracks whether each line in your code was executed.
        * **Branch Coverage**: Tracks whether both the true and false branches of conditional statements (e.g., `if-else` blocks) were executed.
        * **Method Coverage**: Measures if each method in your code was invoked by your tests.
        * **Class Coverage**: Measures whether each class was included in the tests.

4. **Support for Java 8 and Beyond**:

    * JaCoCo supports newer Java features like **lambdas**, **default methods**, and **method references** that are commonly found in Java 8 and later.

5. **Offline Instrumentation**:

    * JaCoCo can instrument your code at **runtime** (via the Java agent) or at **build time** to collect coverage data. This allows for flexibility depending on your testing setup and performance requirements.

6. **CI/CD Integration**:

    * JaCoCo can be easily integrated with **CI/CD** tools like Jenkins, GitLab CI, etc., to automatically generate and report coverage as part of the build process.

7. **User-Friendly Reports**:

    * JaCoCo generates **HTML reports** that are visually easy to read, showing which lines of code are covered and which aren't. This helps identify areas that need more tests.

---

### **How Does JaCoCo Work?**

JaCoCo works by instrumenting the bytecode of your classes during test execution, collecting coverage data on which lines and methods were executed. It can either be configured to run as a **Java Agent** or integrated into the build process using Maven or Gradle plugins.

1. **Java Agent**:

    * JaCoCo runs as a **Java agent** during the test execution. It attaches to the JVM and collects coverage information as your tests run. This is suitable for **runtime instrumentation**.

2. **Build-Time Instrumentation**:

    * JaCoCo can be configured during the **build process** to instrument the compiled classes before running tests. This works well when you want to run tests after the application is built.

---

### **Configuring JaCoCo with Maven**

Here's an example of how you can configure JaCoCo in a **Maven** project:

1. **Add JaCoCo Plugin to `pom.xml`**:

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.jacoco</groupId>
         <artifactId>jacoco-maven-plugin</artifactId>
         <version>0.8.7</version> <!-- Use the latest version -->
         <executions>
           <execution>
             <goals>
               <goal>prepare-agent</goal> <!-- Add this goal to prepare the agent -->
               <goal>report</goal> <!-- Generate the report after the tests -->
             </goals>
           </execution>
         </executions>
       </plugin>
     </plugins>
   </build>
   ```

2. **Run Maven Test**:
   After adding the plugin to your `pom.xml`, you can run the tests with Maven:

   ```bash
   mvn clean test
   ```

3. **Generate JaCoCo Reports**:
   JaCoCo will generate coverage reports in the `target/site/jacoco/` directory (in HTML format by default).

---

### **Configuring JaCoCo with Gradle**

Here’s an example for integrating JaCoCo in a **Gradle** project:

1. **Apply the JaCoCo Plugin** in your `build.gradle` file:

   ```groovy
   plugins {
       id 'java'
       id 'jacoco' // Apply the JaCoCo plugin
   }

   jacoco {
       toolVersion = "0.8.7" // Specify the version of JaCoCo
   }

   test {
       useJUnitPlatform()
       finalizedBy jacocoTestReport // Generate the report after tests
   }

   jacocoTestReport {
       dependsOn test // Generate the report after the tests are run
       reports {
           xml.enabled true
           html.enabled true
       }
   }
   ```

2. **Run Gradle Test**:
   To run the tests and generate coverage reports:

   ```bash
   gradle clean test
   ```

3. **Generate JaCoCo Reports**:
   After the tests are run, JaCoCo will create a report under `build/reports/jacoco/test/html/` in HTML format.

---

### **JaCoCo Report Example**

JaCoCo generates various reports that highlight the test coverage. Here's an example of what you'll see in an **HTML report**:

* **Class-level** coverage, showing which classes have full, partial, or no test coverage.
* **Method-level** coverage, which displays whether all methods in a class are being tested.
* **Line-level** coverage, which shows which specific lines of code have been executed by your tests.
* **Branch coverage**, which indicates whether both branches of conditional statements (`if`, `else`) have been tested.

The reports typically use **color coding** to represent coverage:

* **Green**: Fully covered code.
* **Yellow**: Partially covered code.
* **Red**: Uncovered code.

---

### **Benefits of Using JaCoCo**

1. **Helps Ensure Thorough Testing**:

    * JaCoCo helps identify parts of the codebase that have not been tested, so you can write additional tests to improve test coverage.

2. **Integration with CI/CD Pipelines**:

    * JaCoCo can be integrated with Jenkins or other CI/CD tools to automatically measure and track code coverage as part of your build pipeline, ensuring that test coverage is maintained.

3. **Quality Metrics for Code**:

    * It gives you actionable insights into the quality of your tests and helps ensure that you're covering all critical parts of the code.

4. **Lightweight and Efficient**:

    * JaCoCo is lightweight and has minimal impact on performance, making it suitable for both local and CI-based test runs.

5. **Comprehensive Reports**:

    * JaCoCo provides detailed and user-friendly reports that help in identifying uncovered lines, methods, and branches, so you can prioritize testing efforts.

6. **Supports Different Coverage Types**:

    * It supports line, method, branch, and class coverage, giving a comprehensive view of your tests' effectiveness.

---

### **Best Practices for Using JaCoCo**

1. **Set Coverage Thresholds**:

    * While 100% code coverage is not always achievable or necessary, aim for a practical threshold (e.g., 80-90%) and track it over time to ensure that your tests are effective.

2. **Focus on Critical Code**:

    * Ensure that critical paths, such as business logic and core functionality, have high coverage.

3. **Integrate with CI**:

    * Integrate JaCoCo with your CI pipeline to continuously monitor and enforce code coverage during every build and test run.

4. **Prioritize Meaningful Tests**:

    * While JaCoCo shows you which parts of your code are exercised, it doesn't measure the **quality** of your tests. Focus on writing meaningful tests that check the correctness of your application.

---

### **Conclusion**

**JaCoCo** is a powerful tool for measuring code coverage in Java applications. It provides detailed coverage reports, integrates easily with Maven, Gradle, and CI/CD pipelines, and helps you maintain high-quality test suites. By using JaCoCo effectively, you can identify untested parts of your code, improve test coverage, and ensure that your application behaves as expected. However, remember that **code coverage** is just one measure of test effectiveness; ensuring your tests are meaningful and comprehensive is equally important.

---

## 73. How do you integrate JaCoCo with Maven or Gradle?

### **Integrating JaCoCo with Maven**

To integrate **JaCoCo** with Maven, you need to add the **JaCoCo Maven plugin** to your `pom.xml` file. This plugin helps in collecting code coverage data when running tests, and it can generate detailed reports.

Here are the steps to integrate JaCoCo with Maven:

1. **Add JaCoCo Plugin to `pom.xml`:**

   You need to configure the JaCoCo Maven plugin in the `build` section of your `pom.xml`. Here is an example configuration:

   ```xml
   <build>
     <plugins>
       <plugin>
         <groupId>org.jacoco</groupId>
         <artifactId>jacoco-maven-plugin</artifactId>
         <version>0.8.7</version> <!-- Use the latest version -->
         <executions>
           <!-- This goal prepares JaCoCo agent to collect data -->
           <execution>
             <goals>
               <goal>prepare-agent</goal>
             </goals>
           </execution>
           <!-- This goal generates the coverage report after tests -->
           <execution>
             <goals>
               <goal>report</goal>
             </goals>
             <phase>verify</phase> <!-- Execute after tests are finished -->
           </execution>
         </executions>
       </plugin>
     </plugins>
   </build>
   ```

    * **`prepare-agent`**: This goal prepares JaCoCo to collect code coverage data during test execution.
    * **`report`**: This goal generates a report of the coverage after the tests are run. It will be executed during the `verify` phase of the Maven lifecycle.

2. **Run Tests with Maven:**

   To generate the coverage report, you simply run the tests with Maven:

   ```bash
   mvn clean test
   ```

3. **Generate and View Coverage Report:**

   After running the tests, JaCoCo will generate coverage reports. By default, the report will be placed in the `target/site/jacoco/` directory of your project in **HTML**, **XML**, and **CSV** formats.

   To view the HTML report, open the following file in a browser:

   ```
   target/site/jacoco/index.html
   ```

---

### **Integrating JaCoCo with Gradle**

To integrate **JaCoCo** with **Gradle**, you can apply the JaCoCo plugin in your `build.gradle` file and configure it accordingly. Here are the steps:

1. **Apply JaCoCo Plugin in `build.gradle`:**

   Add the JaCoCo plugin to the `plugins` block:

   ```groovy
   plugins {
       id 'java'
       id 'jacoco' // Add the JaCoCo plugin
   }

   jacoco {
       toolVersion = '0.8.7' // Specify the version of JaCoCo
   }
   ```

2. **Configure the Test Task:**

   In your `build.gradle` file, configure the **test** task to use JaCoCo and generate the report:

   ```groovy
   test {
       useJUnitPlatform() // Enable support for JUnit 5 (optional if using JUnit 4)
       finalizedBy jacocoTestReport // Generate the coverage report after tests
   }

   jacocoTestReport {
       dependsOn test // Ensure the tests are run before generating the report
       reports {
           xml.enabled true // Enable XML format for CI tools
           html.enabled true // Enable HTML format for human-readable reports
           csv.enabled false // Disable CSV report if not needed
       }
   }
   ```

    * **`jacocoTestReport`**: This task generates the coverage report after the tests are run.
    * **`xml.enabled`**: Enables XML reports, useful for integration with CI tools.
    * **`html.enabled`**: Enables HTML reports for easy inspection.

3. **Run Tests with Gradle:**

   To run the tests and generate the coverage report, execute the following command:

   ```bash
   gradle clean test
   ```

4. **View the Coverage Report:**

   After the tests are executed, JaCoCo will generate a coverage report in the `build/reports/jacoco/test/html/` directory.

   You can open the `index.html` file in your browser to view the code coverage summary:

   ```
   build/reports/jacoco/test/html/index.html
   ```

---

### **Key Differences in JaCoCo Integration Between Maven and Gradle**

* **Plugin Declaration**:

    * **Maven**: You add the JaCoCo plugin in the `<plugins>` section of the `pom.xml` file.
    * **Gradle**: You apply the JaCoCo plugin in the `plugins` block of `build.gradle`.

* **JaCoCo Task Configuration**:

    * **Maven**: You configure the execution goals (`prepare-agent`, `report`) in the plugin configuration section.
    * **Gradle**: You configure the `test` task to use the JaCoCo plugin and specify the `jacocoTestReport` task for report generation.

* **Report Locations**:

    * **Maven**: By default, JaCoCo generates reports in the `target/site/jacoco/` directory.
    * **Gradle**: By default, JaCoCo generates reports in the `build/reports/jacoco/test/html/` directory.

---

### **Additional Configuration Options**

Both Maven and Gradle support a range of JaCoCo configuration options. Here are some common ones:

1. **Setting Coverage Thresholds**:

    * You can configure **coverage thresholds** to fail the build if certain coverage criteria (e.g., line or branch coverage) are not met.

    * **Maven** example:

      ```xml
      <configuration>
        <rules>
          <rule>
            <element>CLASS</element>
            <limit>
              <counter>LINE</counter>
              <value>COVEREDRATIO</value>
              <minimum>0.80</minimum> <!-- 80% line coverage threshold -->
            </limit>
          </rule>
        </rules>
      </configuration>
      ```

    * **Gradle** example:

      ```groovy
      jacocoTestCoverageVerification {
          violationRules {
              rule {
                  limit {
                      counter = 'LINE'
                      value = 'COVEREDRATIO'
                      minimum = 0.80 // 80% line coverage threshold
                  }
              }
          }
      }
      ```

2. **Excluding Files/Packages from Coverage**:

    * If you need to exclude certain files or packages from code coverage, you can configure exclusions in your `pom.xml` or `build.gradle`.

    * **Maven** exclusion:

      ```xml
      <configuration>
        <excludes>
          <exclude>**/SomeExcludedClass.java</exclude>
          <exclude>**/tests/**</exclude>
        </excludes>
      </configuration>
      ```

    * **Gradle** exclusion:

      ```groovy
      jacocoTestReport {
          dependsOn test
          classDirectories.setFrom(files(
              fileTree(dir: 'build/classes/java/main', excludes: ['com/example/excluded/**'])
          ))
      }
      ```

---

### **Conclusion**

JaCoCo is a great tool for measuring code coverage in Java applications, and it can be easily integrated with both **Maven** and **Gradle**. By adding the JaCoCo plugin to your build configuration, you can generate detailed coverage reports and track how thoroughly your code is tested.

1. **Maven Integration**: Add JaCoCo to your `pom.xml` and configure the plugin to run during the `test` phase.
2. **Gradle Integration**: Apply the JaCoCo plugin in `build.gradle` and configure the `test` and `jacocoTestReport` tasks.

By integrating JaCoCo into your build process, you can ensure higher test coverage, identify gaps in your tests, and improve the overall quality of your application.

---

## 74. What is a good code coverage percentage?

### **What is a Good Code Coverage Percentage?**

The "ideal" code coverage percentage can vary depending on the context of the project, team, and specific requirements. However, **80% to 90%** is often considered a good benchmark for **unit test coverage** in many software development projects. Here's a more detailed breakdown of what constitutes a good code coverage percentage:

---

### **1. General Guidelines for Code Coverage:**

* **80% to 90% Code Coverage**:

    * This is generally considered a **good target** for most projects. It indicates that the majority of your code is covered by automated tests, but not necessarily all of it.
    * It strikes a balance between writing tests for the most important parts of the codebase while avoiding excessive effort on writing tests for trivial or redundant code.

* **100% Code Coverage**:

    * Achieving **100% code coverage** means that **every line of code** has been executed by your tests.
    * While 100% coverage is ideal from a purely "numbers" perspective, it's not always practical or necessary. **Not all code is equally important to test**, and some code (like getters, setters, or simple utility methods) may not warrant full test coverage.
    * **100% coverage may also give a false sense of security**, because even if the code is covered, it doesn't guarantee the tests are meaningful or effective.

* **Below 80% Code Coverage**:

    * **Below 80%** is typically considered low and may signal insufficient test coverage, which could increase the risk of bugs going unnoticed.
    * If a project consistently falls below 80%, it could be an indication that more tests are needed to ensure the quality and stability of the software.

---

### **Factors to Consider for Code Coverage**

1. **Quality Over Quantity**:

    * **Code coverage percentage** doesn't tell the full story. **Having 80% coverage** is good, but **what matters most is whether the tests are effective**. A high percentage of code coverage doesn’t mean the tests are good if they don't check the behavior of the application properly.
    * For example, you could have a high percentage of coverage but only test trivial code (like getters/setters) or not test edge cases, which would not help in finding bugs.

2. **Critical Code Paths**:

    * Focus on **critical** and **complex logic** in your application. Code that directly affects business logic, security, and user interactions should have **higher coverage** than simple utility methods.
    * For example, code related to authentication, payment processing, or user input validation should be **100% covered**, or at least **thoroughly tested**.

3. **Code Coverage Types**:

    * **Line Coverage**: Ensures each line of code is executed by tests.
    * **Branch Coverage**: Checks if both the true and false branches of conditionals (e.g., `if`/`else` statements) are executed.
    * **Method Coverage**: Verifies if each method is invoked by a test.
    * **Path Coverage**: Ensures different execution paths through the code are covered.

   It’s generally **more important to focus on branch and path coverage**, as they provide a better understanding of how well your tests cover different logical scenarios.

---

### **What to Do with 100% Code Coverage?**

Achieving **100% coverage** doesn’t necessarily indicate that your code is fully tested. Here are some points to keep in mind if you are aiming for or have achieved 100% code coverage:

1. **Avoid Redundant Tests**:

    * If your tests cover trivial methods (e.g., getters, setters, or simple mathematical functions), they might not add much value.
    * In some cases, testing trivial code just to boost coverage can lead to **diminishing returns**, and it can also increase test maintenance overhead.

2. **Meaningful Tests**:

    * Make sure your tests are **meaningful**. Coverage is valuable only if your tests are thoroughly checking **business logic** and **edge cases**.
    * Tests should not just aim to execute lines but should focus on verifying that the application behaves correctly under various conditions.

3. **Review Tests Regularly**:

    * Regularly review the **quality** of the tests, not just their quantity. Code coverage should be one of several indicators of test quality.

4. **Not All Code is Equal**:

    * Some code, such as auto-generated code or library code, may not require extensive tests. For example, libraries like **Guava** or **Apache Commons** are well-tested, and it might not be necessary to write extensive tests for them.

---

### **Common Code Coverage Benchmarks in Different Contexts**

* **Open Source Projects**: These often aim for higher code coverage, typically between **80-90%**, to demonstrate reliability to contributors and users.
* **Enterprise Applications**: In enterprise settings, **80%** coverage is often considered acceptable, but **critical business logic** should be tested thoroughly.
* **Web Applications**: **85-90%** coverage is usually a good target, especially for the core logic, controllers, and services. However, extensive UI testing might not be necessary to achieve 100% coverage.
* **Embedded Systems**: In highly critical systems like those used in **aerospace** or **medical devices**, testing may aim for **close to 100%** coverage, given the high stakes of failure.

---

### **Balancing Code Coverage with Other Metrics**

Code coverage is just one measure of test effectiveness. Here are some additional metrics and practices that should be considered along with coverage:

1. **Test Quality**: Are the tests comprehensive? Are they testing the correct scenarios and edge cases? Code coverage doesn’t guarantee that tests are meaningful.
2. **Mutation Testing**: It helps measure the effectiveness of your tests by introducing small changes (mutations) to your code to see if your tests catch them.
3. **Defect Density**: Keep track of the number of bugs or defects reported in different areas of the codebase to ensure your tests are effective in finding issues.
4. **Code Complexity**: Focus on testing **complex code paths**, rather than aiming for high coverage across trivial or simple code.

---

### **Conclusion:**

* **Good Code Coverage**: **80%-90%** is typically a good target in most projects. It suggests that the application is well-tested while leaving some room for areas that don't need to be tested in depth.
* **Critical Code Coverage**: Ensure that **critical business logic** and **complex code paths** are fully covered, as they are the most likely places where bugs may arise.
* **Meaningful Tests**: Prioritize **quality over quantity**. Focus on testing scenarios that could potentially introduce bugs, rather than writing tests just to achieve high coverage.

By finding a balance between test coverage, code quality, and the meaningfulness of your tests, you can build a more robust, maintainable, and well-tested application.

---

## 75. How do you view code coverage reports?

Viewing code coverage reports is an essential step in ensuring that your tests provide sufficient coverage of your codebase. Once you've configured **JaCoCo** (or other code coverage tools), it generates reports in different formats, typically **HTML**, **XML**, and **CSV**. These reports provide insights into which parts of your code are tested and which are not. Below is a guide on how to view code coverage reports generated by **JaCoCo**.

---

### **1. Viewing HTML Code Coverage Reports (JaCoCo)**

The **HTML report** provides a visual, human-readable view of your code coverage, highlighting the percentage of code covered by tests and showing which lines of code were tested and which weren't.

#### Steps to View the HTML Report:

* After running your tests, JaCoCo will generate an **HTML report** by default. The location of this report depends on your build tool configuration (Maven or Gradle).

    * **Maven**:

        * By default, the JaCoCo HTML report will be generated in the `target/site/jacoco/` directory.
        * Path: `target/site/jacoco/index.html`
    * **Gradle**:

        * By default, the JaCoCo HTML report will be generated in the `build/reports/jacoco/test/html/` directory.
        * Path: `build/reports/jacoco/test/html/index.html`

* **Open the Report**:

    * Navigate to the **HTML report** in your file explorer and open `index.html` in your browser (e.g., Chrome, Firefox, etc.).

    * The HTML report will display coverage statistics for the entire project, and you can drill down into specific packages, classes, and methods.

    * The report usually shows:

        * **Overall coverage** (e.g., percentage of lines covered by tests).
        * **Individual class and method coverage** (which methods/lines were covered).
        * **Color-coding**:

            * **Green** for covered lines.
            * **Red** for uncovered lines.
            * **Yellow** for partially covered lines.

---

### **2. Viewing XML Code Coverage Reports (JaCoCo)**

The **XML report** is often used for **CI/CD tools** and for integration with other tools, like **SonarQube**.

#### Steps to View the XML Report:

* After running your tests, JaCoCo will generate the **XML report** if it's enabled in the configuration. The location depends on your build tool:

    * **Maven**: `target/site/jacoco/jacoco.xml`
    * **Gradle**: `build/reports/jacoco/test/jacocoTestReport.xml`

* **View the XML Report**:

    * Open the **XML file** in a text editor (such as **VS Code**, **IntelliJ IDEA**, or a simple **text editor** like **Notepad**).
    * While XML reports are not as user-friendly as HTML reports, they are highly structured and can be parsed by tools like **SonarQube** or integrated into CI pipelines.

---

### **3. Viewing CSV Code Coverage Reports (JaCoCo)**

The **CSV report** is primarily used for **automation purposes** or for integrating coverage data into other systems or reports.

#### Steps to View the CSV Report:

* After running your tests, JaCoCo will generate the **CSV report** if it's enabled in the configuration.

    * **Maven**: `target/site/jacoco/jacoco.csv`
    * **Gradle**: `build/reports/jacoco/test/jacocoTestReport.csv`

* **View the CSV Report**:

    * Open the **CSV file** using a spreadsheet tool like **Microsoft Excel**, **Google Sheets**, or **LibreOffice Calc**.
    * The CSV file will contain **coverage statistics** in a table format, including which classes, methods, and lines were covered and the percentage of coverage.

---

### **4. Using Code Coverage Tools with CI/CD**

Many teams integrate JaCoCo with CI/CD tools such as **Jenkins**, **GitHub Actions**, **GitLab CI**, or **CircleCI** to automatically generate and display code coverage reports after each build.

* **Jenkins**:

    * You can use the **JaCoCo plugin** for Jenkins to view test results and coverage within Jenkins' UI.
    * The plugin generates a visual report where you can see the coverage for each class and method.

* **GitHub Actions/GitLab CI**:

    * In CI tools, you can configure your pipeline to run tests and generate coverage reports.
    * These reports can be displayed directly in the CI dashboard or integrated with services like **SonarCloud** for more detailed insights.

---

### **5. Using SonarQube for Code Coverage**

For more advanced analysis and long-term tracking, many teams use **SonarQube** to continuously monitor code quality, including test coverage.

* **SonarQube Setup**:

    * After generating JaCoCo reports (typically the **XML format**), configure your CI/CD pipeline to send these reports to **SonarQube**.
    * SonarQube will process these reports and give you an interactive dashboard showing:

        * **Code coverage over time**.
        * **Coverage by file/package**.
        * **Trends** (increase or decrease in coverage).

* **SonarQube Reports**:

    * The **SonarQube dashboard** provides a web-based interface where you can see:

        * Line coverage.
        * Branch coverage.
        * Duplicated code.
        * Hotspots and violations.

---

### **6. IDE Support for Viewing Coverage Reports**

Many IDEs, such as **IntelliJ IDEA** and **Eclipse**, provide built-in support for **JaCoCo** coverage reports.

* **IntelliJ IDEA**:

    * After running tests with coverage enabled, **IntelliJ IDEA** displays a **coverage view** directly in the IDE.
    * The **coverage view** will show the code annotated with **coverage colors** (green, red, yellow) and a summary of the test execution.

* **Eclipse**:

    * You can use **Eclim** or **JaCoCo Eclipse plugin** to run tests and view code coverage directly inside **Eclipse**.
    * Similar to IntelliJ, the code will be highlighted with colors indicating whether a line is covered.

---

### **Best Practices for Viewing and Analyzing Coverage Reports**

1. **Focus on Critical Areas**:

    * Focus on the **critical business logic**, not just high-level or trivial code. While overall coverage is important, testing complex logic is more valuable.

2. **Use Coverage Thresholds**:

    * Set **coverage thresholds** (e.g., 80%-90%) to ensure your code is sufficiently tested. If coverage falls below the threshold, you can be alerted to add more tests.

3. **Leverage Code Coverage Tools**:

    * Use tools like **SonarQube**, **Jenkins**, or **GitHub Actions** to continuously track coverage over time and identify areas of the codebase with low or no test coverage.

4. **Analyze Code Coverage Reports Regularly**:

    * Ensure that **coverage reports** are part of your regular workflow (whether manually or automatically generated by your CI pipeline) to keep an eye on the test coverage over time.

---

### **Conclusion**

Viewing code coverage reports is crucial for understanding how thoroughly your tests cover your codebase. Depending on your build tool (Maven or Gradle), the reports will be generated in different formats (HTML, XML, CSV), each serving a specific purpose:

* **HTML**: User-friendly, human-readable, and visually rich.
* **XML/CSV**: For integration with CI/CD tools or other systems (e.g., SonarQube).

Using these reports, you can identify untested code, ensure critical areas are adequately covered, and track test coverage trends over time.

---

## 76. What is mutation testing?

### **What is Mutation Testing?**

**Mutation testing** is a software testing technique that involves modifying (or mutating) the code in small, controlled ways to check whether the existing tests can detect these changes (i.e., mutations). The idea behind mutation testing is to evaluate the **effectiveness** of your tests: if your tests can detect the changes in the code, they are likely to be robust and comprehensive. If your tests fail to catch the mutations, it indicates that the tests may be missing important scenarios or are not thorough enough.

The core principle of mutation testing is to create **mutants** (i.e., small variations or changes) in the code and run the tests to see if they **kill** (catch) the mutants. If the tests fail to detect the mutation, it means the mutation is not covered by the tests, and the test suite needs improvement.

---

### **How Mutation Testing Works**

1. **Create Mutants**: Mutation testing tools modify the code by introducing small changes, such as:

    * Changing a mathematical operator (`+` → `-`).
    * Reversing a boolean expression (`true` → `false`).
    * Altering the method calls (e.g., replacing a method call with a different one).
    * Changing conditional statements or loops.
    * Modifying variable values.

2. **Run Tests**: Once the mutants are created, the test suite is run to check if the mutants cause any failures.

3. **Kill or Survive**:

    * **Kill**: If the test suite detects and fails the mutant, it's considered "killed," indicating that the test suite is effective in detecting this type of issue.
    * **Survive**: If the test suite does not detect the mutant, it "survives," suggesting a gap in test coverage or the need for additional tests.

4. **Mutation Score**: The result of mutation testing is often expressed as the **mutation score**, which is calculated as:

   $$
   \text{Mutation Score} = \frac{\text{Number of Mutants Killed}}{\text{Total Number of Mutants}} \times 100
   $$

   A high mutation score means your tests are good at catching issues, while a low mutation score suggests that your tests are inadequate or incomplete.

---

### **Example of Mutation Testing**

Let's assume we have a simple method that calculates the sum of two numbers:

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

Mutation testing might introduce the following mutations:

* **Change the `+` to `-`**:

  ```java
  public int add(int a, int b) {
      return a - b;  // Mutation: changed addition to subtraction
  }
  ```

* **Return a constant value instead of the sum**:

  ```java
  public int add(int a, int b) {
      return 10;  // Mutation: changed the result to a fixed value
  }
  ```

* **Change the method name or return type**:

  ```java
  public String add(int a, int b) {
      return String.valueOf(a + b);  // Mutation: changed the return type to String
  }
  ```

Now, if your test suite includes a test for the `add()` method, it should be able to **kill** (i.e., detect and fail) all these mutants. If your test passes even after such mutations, it means your test suite is missing certain cases or not thoroughly testing the method.

---

### **Tools for Mutation Testing in Java**

Several tools can help automate mutation testing in Java:

1. **Pitest (PIT)**:

    * **PIT** is one of the most popular mutation testing tools for Java. It integrates with build tools like **Maven** and **Gradle**, and can automatically mutate your code and run tests.
    * It generates detailed reports about which mutants were killed and which survived, along with the mutation score.

   **Example (Maven Integration)**:

   ```xml
   <plugin>
       <groupId>org.pitest</groupId>
       <artifactId>pitest-maven</artifactId>
       <version>1.6.0</version>
       <executions>
           <execution>
               <goals>
                   <goal>mutationCoverage</goal>
               </goals>
           </execution>
       </executions>
   </plugin>
   ```

2. **Jesters**:

    * **Jesters** is another mutation testing framework for Java. It's simpler than PIT and is integrated into the **JUnit** testing framework.

3. **Mutator**:

    * **Mutator** is a Java mutation testing framework that focuses on creating mutations and running tests against them.

---

### **Benefits of Mutation Testing**

1. **Test Quality Assurance**:

    * Mutation testing helps identify **weaknesses in your tests**, ensuring that they are comprehensive and effective.

2. **Increased Confidence**:

    * A high mutation score suggests that your tests are robust and capable of catching most types of issues, giving you **higher confidence** in the reliability of your software.

3. **Improved Test Coverage**:

    * It identifies **gaps in coverage**. If mutants survive, you can adjust your tests to cover the uncovered scenarios.

4. **Effective at Finding Logical Errors**:

    * It helps to catch **logical errors** or unintended behavior in your application that might not be apparent through traditional test coverage analysis.

---

### **Challenges of Mutation Testing**

1. **Performance Overhead**:

    * Mutation testing can be **time-consuming** and computationally expensive, especially for large codebases with many mutants. Running all possible mutations on large projects can lead to long test cycles.

2. **False Positives/Negatives**:

    * Sometimes, **equivalent mutants** (mutations that don’t actually affect behavior) can survive, which may skew the results. This can happen if a mutation doesn't affect the output of the program, such as changing a `+` to `-` in a non-executed block of code.

3. **Test Maintenance**:

    * Mutation testing requires you to write more comprehensive tests, which might lead to increased **test maintenance** and complexity. If your code changes often, you may need to keep adjusting your tests and re-running mutation tests.

4. **Overkill for Small Projects**:

    * For **small projects** or less critical code, mutation testing might be overkill. It's more valuable for larger and more complex applications where test quality directly impacts stability.

---

### **Best Practices for Mutation Testing**

1. **Use Mutation Testing as a Complement to Traditional Testing**:

    * Don't rely solely on mutation testing. Use it alongside **unit testing** and other test quality metrics like **code coverage**, **test case reviews**, and **static code analysis**.

2. **Focus on High-Risk Areas**:

    * Prioritize mutation testing for **critical code paths** where errors could have a significant impact. This helps to maximize the value of the time spent on mutation testing.

3. **Run Mutation Tests Periodically**:

    * Since mutation testing can be time-intensive, consider running it on a **regular schedule** (e.g., after every major release) rather than after every code change. This balances test effectiveness with resource usage.

---

### **Conclusion**

Mutation testing is an advanced technique used to evaluate the effectiveness of your tests. By deliberately introducing faults (mutants) into the code and checking if the tests detect them, mutation testing helps you identify **weak points** in your test suite and improve the quality of your tests. While it's powerful, it comes with challenges such as performance overhead and false positives. When applied correctly, it can significantly increase the reliability of your software by ensuring that your tests can detect a wide range of errors.

---

## 77. What is PIT (Pitest) in Java testing?

### **What is PIT (Pitest) in Java Testing?**

**PIT (Pitest)** is a popular **mutation testing** tool for **Java** that helps evaluate the quality of your test suite by introducing small modifications (mutations) in your code and checking if your existing tests can detect these changes. In simpler terms, it measures how effective your tests are in catching potential bugs or issues in the code.

Pitest generates **mutants** (modified versions of your code) and runs the tests against them. If the tests "kill" the mutants (i.e., detect the mutations), they are considered effective. If the mutants survive (i.e., the tests do not detect the changes), this indicates a gap in the test coverage or test quality, and your tests might need to be improved.

### **How Pitest (PIT) Works**

1. **Mutant Generation**:

    * PIT generates different types of **mutants** by modifying the code in small ways. These changes could include:

        * Changing arithmetic operators (`+` to `-`).
        * Modifying boolean expressions (`true` to `false`).
        * Altering method invocations.
        * Changing conditional statements (e.g., `if` to `else`).
        * Reversing comparisons (e.g., `a > b` to `a < b`).

2. **Test Execution**:

    * Once the mutants are generated, PIT runs the tests against these mutated versions of the code. The goal is to see if the tests can "kill" the mutants by failing when an incorrect mutation is present.

3. **Mutation Score**:

    * PIT calculates a **mutation score** based on the ratio of killed mutants to total mutants. A high mutation score means your tests are more effective in detecting issues. A low score means your tests might need improvement.

4. **Report Generation**:

    * After the mutation testing process, PIT generates reports that provide insights into which mutants were killed and which survived, helping you identify gaps in your test coverage.

### **Example of Mutation Testing with PIT**

Let's consider a simple Java class:

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

Pitest might generate the following mutations:

* **Mutation 1**: Replace the addition operator (`+`) with subtraction (`-`).

  ```java
  public int add(int a, int b) {
      return a - b;  // Mutation: changed addition to subtraction
  }
  ```

* **Mutation 2**: Replace `a + b` with a fixed value like 10.

  ```java
  public int add(int a, int b) {
      return 10;  // Mutation: changed to return a constant value
  }
  ```

After running the tests, PIT checks if the mutants are "killed" (i.e., tests fail for the mutated code). If any mutants survive, you know that there are gaps in your test coverage or that the tests missed detecting the mutation.

### **Features of PIT (Pitest)**

1. **Integration with Maven and Gradle**:

    * PIT integrates seamlessly with both **Maven** and **Gradle**, allowing you to run mutation tests as part of your build process.

    * **Maven Configuration Example**:

      ```xml
      <plugin>
          <groupId>org.pitest</groupId>
          <artifactId>pitest-maven</artifactId>
          <version>1.6.0</version>
          <executions>
              <execution>
                  <goals>
                      <goal>mutationCoverage</goal>
                  </goals>
              </execution>
          </executions>
      </plugin>
      ```

    * **Gradle Configuration Example**:

      ```gradle
      plugins {
          id 'info.solidsoft.pitest' version '1.6.0'
      }
      ```

2. **Customizable Mutation Strategy**:

    * PIT allows you to customize the mutation strategy. You can choose which types of mutations to apply, including **method calls**, **conditional statements**, **arithmetic operations**, etc.

3. **Incremental Mutation Testing**:

    * PIT supports **incremental mutation testing**, where only the changes made to the code are mutated, rather than re-running mutation tests for the entire codebase. This makes it faster for large codebases.

4. **Comprehensive Reports**:

    * PIT provides detailed reports, which include:

        * **Mutation score**: The ratio of killed mutants to total mutants.
        * **Surviving mutants**: Mutants that were not detected by the tests.
        * **Covered and uncovered lines**: Which parts of the code were tested and which were not.
    * Reports are typically available in **HTML**, **XML**, and **CSV** formats.

5. **Integration with CI Tools**:

    * PIT can be integrated with **CI/CD** tools such as **Jenkins**, **GitLab CI**, **GitHub Actions**, etc., to continuously track mutation testing results and test effectiveness over time.

6. **Parallel Testing**:

    * PIT supports parallel execution of tests, which improves performance by running tests across multiple CPU cores or machines, particularly helpful for large test suites.

---

### **Setting Up PIT in a Maven Project**

1. **Add the PIT Plugin to `pom.xml`**:

    * To enable PIT for mutation testing in a Maven project, add the following configuration to your `pom.xml` file:

   ```xml
   <build>
       <plugins>
           <plugin>
               <groupId>org.pitest</groupId>
               <artifactId>pitest-maven</artifactId>
               <version>1.6.0</version>
               <executions>
                   <execution>
                       <goals>
                           <goal>mutationCoverage</goal>
                       </goals>
                   </execution>
               </executions>
           </plugin>
       </plugins>
   </build>
   ```

2. **Run PIT with Maven**:

    * You can run the mutation tests by executing the following Maven command:

   ```bash
   mvn pitest:mutationCoverage
   ```

3. **View the Results**:

    * Once the tests are run, PIT generates a report in the `target/pit-reports` directory. This includes an **HTML report** that you can open in a browser to visualize the mutation coverage and which tests killed the mutants.

---

### **Benefits of Using PIT (Pitest)**

1. **Improved Test Quality**:

    * PIT helps identify weaknesses in your test suite, ensuring that your tests are more thorough and effective in catching potential bugs.

2. **Focus on Critical Areas**:

    * Mutation testing with PIT allows you to focus on areas where your tests may not be as strong, ensuring that critical parts of your code are well-tested.

3. **Identifying Gaps in Coverage**:

    * PIT helps identify **uncovered code** or scenarios that are not tested, allowing you to write more effective test cases.

4. **Better Test Suite Confidence**:

    * A high mutation score means your test suite is robust, which gives you **higher confidence** in the correctness and reliability of your software.

---

### **Challenges with PIT (Pitest)**

1. **Performance Overhead**:

    * Mutation testing can be **resource-intensive**, especially for large projects. Since PIT runs the tests against numerous mutants, it can lead to longer test execution times, especially if you are testing a large codebase.

2. **Equivalent Mutants**:

    * **Equivalent mutants** are mutants that don’t change the behavior of the program. These can sometimes survive, and although they are not a real problem in the code, they can make the mutation score appear lower than it should be.

3. **False Positives**:

    * PIT may generate **false positives** in certain edge cases, where a mutant survives even though the test suite should have caught it. This can happen due to limitations in the mutation strategy or the nature of the code being tested.

4. **Test Maintenance**:

    * Mutation testing requires that you maintain comprehensive and high-quality tests. If your tests are not robust, you will not get good results from PIT.

---

### **Conclusion**

**PIT (Pitest)** is a powerful **mutation testing** tool for Java that helps improve the quality of your test suite by identifying weaknesses and coverage gaps. By introducing small changes (mutations) to your code and running tests against them, PIT helps you measure the effectiveness of your tests. Although it can be resource-intensive and may result in false positives due to equivalent mutants, it remains an excellent tool for ensuring that your tests are robust and capable of catching bugs. When used alongside traditional testing methods, PIT can significantly boost the confidence in the reliability and correctness of your software.

---

## 78. What is the difference between functional and non-functional tests?

### **Difference Between Functional and Non-Functional Tests**

**Functional Testing** and **Non-Functional Testing** are two major categories of software testing, and they focus on different aspects of the application. Here's a detailed explanation of both:

---

### **1. Functional Testing**

**Functional testing** refers to the testing of the application's features and functions, ensuring that it behaves as expected based on the functional requirements or specifications. The primary objective of functional testing is to verify that the software performs the functions it is supposed to do, and that each feature works correctly according to its specifications.

#### **Key Characteristics of Functional Testing:**

* **Focus**: Verifies the correctness of features, functions, and behaviors of the system.
* **Objective**: To ensure the system behaves according to the defined requirements.
* **Type of Test**: Black-box testing (no knowledge of internal code, only focus on inputs and outputs).
* **Examples**:

    * **Unit Testing**: Testing individual functions or methods in isolation.
    * **Integration Testing**: Testing the interaction between different modules or components.
    * **System Testing**: Testing the entire system against functional requirements.
    * **Acceptance Testing**: Validating if the system meets user needs and requirements (e.g., UAT - User Acceptance Testing).

#### **Examples of Functional Testing:**

* **Login functionality**: Ensuring that a user can log in using valid credentials.
* **Search functionality**: Verifying that a search function returns the correct results based on user input.
* **Data entry**: Ensuring that data entered into a form is saved correctly to the database.

#### **Common Tools for Functional Testing:**

* Selenium
* JUnit
* TestNG
* Cucumber (for BDD)

---

### **2. Non-Functional Testing**

**Non-functional testing** refers to testing the non-functional aspects of an application, such as performance, usability, reliability, scalability, and security. These tests assess how well the software performs under certain conditions, rather than verifying specific functionalities.

#### **Key Characteristics of Non-Functional Testing:**

* **Focus**: Evaluates non-functional attributes such as performance, usability, and security.
* **Objective**: To ensure that the software performs well under different conditions, meets quality standards, and provides a good user experience.
* **Type of Test**: Often involves testing the system under load or stress, and involves measuring the performance, security, and usability aspects.
* **Examples**:

    * **Performance Testing**: Testing how well the system performs in terms of speed, responsiveness, and stability under various conditions.
    * **Load Testing**: Evaluating how the system handles a specific load of users or transactions.
    * **Stress Testing**: Checking how the system behaves under extreme conditions (e.g., very high traffic).
    * **Usability Testing**: Assessing the ease of use and user-friendliness of the application.
    * **Security Testing**: Ensuring that the system is secure from vulnerabilities and threats.

#### **Examples of Non-Functional Testing:**

* **Performance Testing**: How fast an application responds to user actions under normal load.
* **Security Testing**: Checking for vulnerabilities like SQL injection, cross-site scripting (XSS), and ensuring data protection.
* **Load Testing**: Evaluating how the system performs when a large number of users try to access it simultaneously.
* **Usability Testing**: Ensuring that the software is user-friendly, intuitive, and provides a good experience to end-users.

#### **Common Tools for Non-Functional Testing:**

* **Load Testing**: Apache JMeter, LoadRunner
* **Performance Testing**: Gatling, Apache JMeter, LoadRunner
* **Security Testing**: OWASP ZAP, Burp Suite, Fortify
* **Usability Testing**: UserTesting, Hotjar

---

### **Key Differences**

| **Aspect**         | **Functional Testing**                                                                       | **Non-Functional Testing**                                                                                      |
| ------------------ | -------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------- |
| **Focus**          | Verifies the functions/features of the system.                                               | Verifies non-functional attributes like performance and security.                                               |
| **Objective**      | Ensures that the software works as expected according to the functional requirements.        | Ensures that the software performs well under various conditions and meets quality standards.                   |
| **Scope**          | Specific features and behaviors of the system (e.g., user login, search functionality).      | Broader quality aspects like performance, scalability, and security.                                            |
| **Example Tests**  | Unit Testing, Integration Testing, System Testing, Acceptance Testing.                       | Load Testing, Stress Testing, Security Testing, Usability Testing.                                              |
| **Test Type**      | Typically black-box testing.                                                                 | Can involve performance benchmarking, security validation, and usability assessment.                            |
| **Tools**          | Selenium, JUnit, TestNG, Cucumber.                                                           | Apache JMeter, LoadRunner, OWASP ZAP, Burp Suite.                                                               |
| **When it’s done** | Functional testing is done during the development phase to ensure features work as expected. | Non-functional testing is often done after functional testing, typically in staging or production environments. |
| **Test Result**    | Pass or fail based on the expected functionality.                                            | Pass or fail based on performance, security, or user experience metrics.                                        |

---

### **Example Comparison**

#### **Functional Testing Example:**

* **Test Case**: Validate the login functionality.

    * **Expected Behavior**: When the user enters a valid username and password, they should be redirected to the homepage.
    * **Test**: Check if the login button redirects the user after entering correct credentials.

#### **Non-Functional Testing Example:**

* **Test Case**: Validate the performance of the login page under load.

    * **Expected Behavior**: The login page should respond within 2 seconds even when 1000 users attempt to log in simultaneously.
    * **Test**: Simulate 1000 concurrent users logging in and check the response time.

---

### **Conclusion**

* **Functional testing** focuses on verifying that the application’s features work as expected, ensuring that the functionality is correct and meets the specified requirements.
* **Non-functional testing**, on the other hand, focuses on testing the system’s behavior under certain conditions (like performance or security), ensuring the software meets standards for reliability, usability, and scalability.

Both types of testing are essential to ensure a high-quality software product, with functional testing ensuring that features work correctly and non-functional testing ensuring the software can handle real-world scenarios and edge cases efficiently.

---

## 79. What is a flaky test and how do you handle it?

### **What is a Flaky Test?**

A **flaky test** is a test that **sometimes passes and sometimes fails** without any changes in the code being tested. These tests exhibit **unpredictable behavior**, which makes them unreliable. Flaky tests can cause issues in the continuous integration (CI) pipeline and make it harder to trust test results. They introduce uncertainty and can lead to false positives (test passes when it should fail) or false negatives (test fails when it should pass).

#### **Causes of Flaky Tests**

Flaky tests can be caused by various factors, including:

1. **Asynchronous behavior**: Tests that depend on asynchronous operations (e.g., network requests, timers, or database operations) can sometimes fail due to timing issues.
2. **Test dependencies**: If tests depend on the order of execution or on shared state, it can cause tests to behave inconsistently.
3. **External systems**: Tests that depend on external systems (like a database or web service) can fail due to connectivity issues, timeouts, or other external factors.
4. **Race conditions**: In multithreaded or parallel testing, race conditions can cause tests to fail intermittently.
5. **Unstable environment**: Variability in the testing environment, like load on the server, machine resource constraints, or network latency, can result in flaky behavior.
6. **Randomized inputs**: Tests that use random values might behave differently each time, leading to inconsistencies.
7. **Concurrency issues**: If tests are run in parallel and share resources, concurrent access may lead to failures that are not reproducible.

---

### **How to Handle Flaky Tests**

Handling flaky tests involves a combination of **identifying, isolating**, and **fixing** the root causes of instability. Here are strategies for dealing with flaky tests:

---

#### **1. Identifying Flaky Tests**

* **Observe Test Behavior**: Run the tests multiple times to see if the test consistently fails or passes intermittently. Tools like CI pipelines often help detect flaky tests if a test passes in one build and fails in another.
* **Mark as Flaky**: In some cases, you may want to mark the flaky test with a specific label or tag (e.g., `@Flaky`) so it stands out in the test reports.
* **Test Logs and Stack Traces**: Look at the logs or stack traces to identify where the failure occurs and whether it's due to timing, environment issues, or other factors.

---

#### **2. Investigating the Root Cause**

Once you've identified the flaky test, you'll need to determine why it’s behaving unpredictably. Some common steps to isolate the cause include:

* **Check Test Dependencies**: Ensure the test doesn't depend on other tests or shared state. Tests should be isolated and independent.
* **Verify External Dependencies**: If the test depends on external systems like APIs, databases, or third-party services, check for intermittent connectivity issues or unreliable external resources.
* **Inspect Asynchronous Code**: If the test involves asynchronous operations, consider adding appropriate **waits** or **timeouts** to ensure the test completes successfully before assertions are made. Tools like **`CountDownLatch`** or **`CompletableFuture`** can be used to synchronize asynchronous behavior.
* **Review Time Sensitivity**: Tests sensitive to timing issues (e.g., waiting for a certain amount of time or an event) should be adjusted to handle slight delays in a reliable manner.
* **Check for Race Conditions**: If the test involves concurrency, ensure that shared resources are properly synchronized and that tests are thread-safe.
* **Check Test Environment Stability**: Ensure that the environment where the tests are run is stable (e.g., network latency, server load, etc.).

---

#### **3. Fixing Flaky Tests**

Once you’ve identified the cause of the flaky test, the next step is to fix it. Below are some strategies to make flaky tests more reliable:

1. **Eliminate Test Dependencies**:

    * Ensure that tests are **independent** and **isolated**. Tests should not depend on the state or results of other tests. This can be achieved by using **mocks** or **stubs** for external dependencies and resetting shared resources between tests.

2. **Introduce Proper Synchronization**:

    * For asynchronous or multithreaded tests, make sure that the code waits for the necessary conditions (e.g., waiting for a thread to finish or a callback to be invoked). Use tools like `Thread.sleep()`, `CountDownLatch`, or `Semaphore` to handle synchronization properly.
    * **Example**:

      ```java
      CountDownLatch latch = new CountDownLatch(1);
      someAsyncMethod(() -> latch.countDown());
      latch.await(10, TimeUnit.SECONDS);
      ```

3. **Handle External Dependencies**:

    * For tests that rely on external services or databases, consider using **mocking frameworks** (like **Mockito**) or **embedded databases** to ensure that tests don’t fail due to external factors.
    * If possible, use **service virtualization** to simulate external APIs or resources.

4. **Fix Race Conditions**:

    * Ensure that shared resources in multithreaded tests are properly synchronized. Use **synchronization** techniques like `synchronized` blocks or thread-safe data structures.
    * Use **atomic operations** to ensure that tests behave predictably when multiple threads are involved.

5. **Make the Test Deterministic**:

    * Avoid using random values in tests that might cause them to behave unpredictably. If randomness is necessary, consider using a fixed seed to ensure the test behaves consistently across runs.

6. **Improve Time-Dependent Tests**:

    * If a test is time-sensitive (e.g., testing delays or timeouts), ensure that **timeouts** or **delays** are handled reliably. Use testing tools like `Mockito`'s `Mockito.timeout()` or **`Thread.sleep()`** for controlled waits in tests.
    * Be cautious with `Thread.sleep()` as it can be a source of instability in certain environments.

7. **Use Retry Mechanisms**:

    * For truly intermittent tests that cannot be fully stabilized (e.g., due to network instability), consider implementing **retries**. However, use this with caution, as retries can mask underlying issues rather than fixing them.
    * Tools like **JUnit 5** or **TestNG** support retrying failed tests automatically.

        * **Example (JUnit 5)**:

          ```java
          @Test
          @Retry(3)
          public void flakyTest() {
              // Test logic
          }
          ```

8. **Improve Test Environment**:

    * Ensure that the test environment is stable, with consistent configurations and resource availability. This can be achieved through better management of test environments or using tools like **Docker** for isolated and consistent environments.

---

#### **4. Monitor and Continuously Improve**

Even after fixing flaky tests, it's important to **monitor** them over time. Set up continuous integration (CI) pipelines with proper reporting to catch flaky tests early.

* Regularly **review** test logs and build reports to identify recurring flaky tests.
* **Refactor** tests when needed to ensure that they remain isolated, reliable, and performant.

---

### **Conclusion**

A flaky test is a test that behaves inconsistently, passing in some runs and failing in others. Flaky tests are problematic because they undermine the reliability of the testing process. To handle flaky tests, you need to:

* **Identify** the flaky tests by observing their behavior and analyzing the test logs.
* **Investigate** the root cause, focusing on test dependencies, external systems, concurrency, and environmental factors.
* **Fix** the flaky tests by eliminating dependencies, improving synchronization, mocking external services, and ensuring deterministic behavior.
* **Monitor** flaky tests regularly in your CI/CD pipelines and continuously improve the test suite.

By addressing flaky tests effectively, you can improve the reliability of your tests and ensure your application behaves as expected in all situations.

---

## 80. How do you avoid false positives and negatives in unit testing?

### **How to Avoid False Positives and False Negatives in Unit Testing**

**False positives** and **false negatives** are common issues in unit testing that can undermine the reliability of your testing process and the quality of your application.

* **False Positive**: A test passes when it should fail, potentially hiding a defect.
* **False Negative**: A test fails when it should pass, causing unnecessary confusion or delay in the development process.

To ensure that your unit tests are reliable and accurate, it’s essential to minimize both false positives and false negatives.

Here’s a detailed breakdown of how to avoid them:

---

### **1. Ensure Proper Test Setup and Isolation**

**False positives** and **false negatives** can arise if tests depend on external systems or shared states that are not correctly reset.

#### **How to Avoid It:**

* **Isolate Tests**: Each unit test should be **independent**. Ensure that the outcome of one test does not affect the others. This can be done by using mocking or stubbing frameworks (e.g., **Mockito**) to isolate dependencies.
* **Test Initialization**: Ensure that the environment and dependencies are properly set up and reset between tests (e.g., using annotations like `@BeforeEach` and `@AfterEach` in JUnit 5).
* **Use Mocks or Stubs**: Instead of relying on real external systems, mock or stub any dependencies to ensure consistency and control.

#### **Example (JUnit 5)**:

```java
@BeforeEach
void setup() {
    // Set up fresh data before each test
}

@AfterEach
void tearDown() {
    // Reset any state if necessary
}
```

---

### **2. Use Assertions Correctly**

Misusing assertions can lead to false positives and false negatives. For example, using weak assertions or comparing objects incorrectly can cause tests to fail when they shouldn’t or pass when they shouldn’t.

#### **How to Avoid It:**

* **Use precise assertions**: Use the right assertions for the task. For example, use `assertEquals()` for value comparisons and `assertSame()` for reference equality. When comparing floating-point values, ensure that you account for small rounding errors by using a delta in `assertEquals()`.
* **Avoid ambiguous checks**: If a test asserts a condition like `assertTrue(someMethod())`, ensure that the method reliably returns the expected boolean result. Consider adding more meaningful assertions based on expected behavior.

#### **Example**:

```java
assertEquals(expectedValue, actualValue); // Precise comparison
assertTrue(actualValue > 0); // Ensure that the value meets a certain condition
assertNotNull(actualObject); // Validate non-null results
```

---

### **3. Use Timeouts and Handling Asynchronous Code**

Asynchronous or time-sensitive code can cause **false negatives** due to race conditions, delays, or other timing issues. Similarly, improper handling of timeouts can lead to **false positives** if the system under test doesn’t behave as expected under certain conditions.

#### **How to Avoid It:**

* **Use Timeouts**: When testing asynchronous operations, set a reasonable **timeout** to ensure that the test doesn’t hang indefinitely or pass erroneously when the operation never completes.
* **Wait for Asynchronous Code**: Use synchronization mechanisms like `CountDownLatch`, `CompletableFuture`, or `await()` to ensure that asynchronous tasks are properly completed before assertions are made.

#### **Example**:

```java
@Test
void testAsyncOperation() throws InterruptedException {
    CountDownLatch latch = new CountDownLatch(1);
    asyncService.doSomethingAsync(() -> latch.countDown());
    
    // Wait for the asynchronous task to complete within a timeout
    assertTrue(latch.await(5, TimeUnit.SECONDS));
}
```

---

### **4. Avoid Hard-Coding Values**

Hard-coded values in tests can lead to **false positives** when the code changes and the test does not update accordingly.

#### **How to Avoid It:**

* **Use Constants**: For expected values, use constants or configuration values instead of hard-coded literals. This makes tests more maintainable and reduces the likelihood of discrepancies when the code changes.
* **Parameterize Tests**: Use parameterized tests to verify a variety of input values and ensure that the logic holds under different conditions.

#### **Example**:

```java
@Test
@ParameterizedTest
@ValueSource(ints = {1, 2, 3})
void testAddition(int number) {
    assertEquals(5, add(number, 2));
}
```

---

### **5. Ensure Proper Test Coverage**

Tests with poor coverage are more likely to produce **false negatives** because they fail to check edge cases or important code paths.

#### **How to Avoid It:**

* **Use Code Coverage Tools**: Integrate code coverage tools (e.g., **JaCoCo**, **Cobertura**) to ensure that all relevant code paths are covered by tests.
* **Test Edge Cases**: Write tests for edge cases (e.g., empty inputs, null values, boundary conditions) and handle exceptions properly to avoid missing unexpected behaviors.

---

### **6. Avoid Relying on External Systems**

Tests that depend on external services, databases, or APIs are more likely to experience **false negatives** due to intermittent failures or network issues.

#### **How to Avoid It:**

* **Mock External Dependencies**: Use tools like **Mockito** to mock external systems, so your tests are isolated from network failures or system downtime.
* **Use Embedded Databases**: For tests that depend on a database, use embedded databases (e.g., **H2**) to avoid issues with external databases.

#### **Example (Mockito)**:

```java
@Mock
private MyService myService;

@Test
void testServiceCall() {
    when(myService.someMethod()).thenReturn("Expected Result");

    // Assert the expected behavior without hitting a real service
    assertEquals("Expected Result", myService.someMethod());
}
```

---

### **7. Use the Right Testing Strategy**

Depending on the testing strategy, you may encounter situations where test failures are more prone to occur.

#### **How to Avoid It:**

* **Use Unit Testing**: Unit tests should isolate individual units of code and focus on testing small, well-defined behaviors.
* **Mocking and Dependency Injection**: Ensure that dependencies are injected and replaced with mocks or stubs to avoid interacting with real external systems during unit testing.
* **Use Integration Tests Sparingly**: While integration tests are essential, ensure they are used to verify the integration between components rather than unit behavior.

---

### **8. Handle Randomness and Timing Issues**

Tests involving random data or time-based conditions are prone to **false positives** and **false negatives** if not handled properly.

#### **How to Avoid It:**

* **Control Random Inputs**: When randomness is involved, use a **seeded random number generator** to ensure repeatability of tests.
* **Avoid Flaky Tests**: If timing or randomness is causing intermittent failures, refactor the tests to ensure deterministic results.

#### **Example (JUnit 5)**:

```java
@Test
void testRandomNumberGenerator() {
    Random random = new Random(42); // Use a fixed seed for reproducibility
    int result = random.nextInt(100);
    assertEquals(81, result); // Predictable result based on seed
}
```

---

### **9. Use Retry Mechanism for Intermittent Failures**

In certain cases, some failures may be caused by temporary or environmental issues. **Retrying** the test can help avoid false negatives, though this should be used cautiously.

#### **How to Avoid It:**

* **Retry Failed Tests**: Tools like **JUnit 5** and **TestNG** allow you to configure retries for tests that fail intermittently. However, this should be used sparingly, as it can hide underlying issues.

---

### **Conclusion**

To **avoid false positives** and **false negatives** in unit testing:

* Ensure **proper test isolation** and setup/tear down.
* Use **precise assertions** for accurate comparisons.
* Handle **asynchronous code** and timeouts correctly.
* Avoid **hard-coded values** and ensure that tests cover edge cases.
* **Mock external systems** to prevent failures due to network issues or external dependencies.
* Focus on **unit testing** and minimize reliance on external systems or environments.
* Address **randomness and timing issues** to make tests deterministic.

By following these practices, you can create more reliable, accurate tests that provide valuable feedback during development, helping you build high-quality software.

---

### 🔹 81–100: **Advanced, Best Practices & Real Scenarios**

## 81. What is test isolation and why is it important?

### **What is Test Isolation and Why Is It Important?**

**Test isolation** refers to the practice of ensuring that individual unit tests are **independent** of one another. This means each test should only focus on verifying the behavior of the unit being tested, without relying on the state, output, or behavior of other tests.

### **Key Principles of Test Isolation:**

1. **Independent Tests**: Each test should not rely on the outcome or execution order of other tests. It should be able to run in isolation, independently of other tests in the test suite.
2. **No Shared State**: Tests should not modify shared resources or leave any lasting side effects that could affect the results of other tests. This includes variables, files, databases, or other external systems.
3. **No Order Dependencies**: The order in which tests run should not impact their outcome. This means each test must be self-contained, without relying on the setup or teardown of another test.

### **Why Is Test Isolation Important?**

Test isolation is crucial for several reasons, including:

---

### **1. Reliable Test Results**

Tests that are isolated from each other provide **consistent and reliable results**. If one test fails, it should not cause other tests to fail unless they are genuinely broken. When tests are dependent on each other, the failure of one test can cause a cascade of failures, making it hard to pinpoint the root cause of the problem.

#### **Example**:

Without test isolation, a test could pass because another test set up a certain state or dependency. If that dependent test fails or behaves differently, it could cause the seemingly unrelated test to fail as well, even though the underlying code being tested is not faulty.

---

### **2. Easier Debugging**

Isolated tests make it easier to debug issues. If a test fails, it’s clear that the failure is related to the unit under test and not some other external factor. In a non-isolated testing setup, a failure in one test can cause other tests to fail, and debugging becomes more complex because you must trace back through the other tests to figure out what went wrong.

#### **Example**:

* In an isolated test suite, you can clearly see which test fails, and it directly relates to the logic being tested.
* In a non-isolated suite, if a test relies on a database state set by another test, a failure in one test could cause unrelated tests to fail, making it much harder to debug.

---

### **3. Faster Execution**

Isolated tests typically run faster. Since each test does not rely on external systems, shared states, or other tests, they can be run in parallel or independently, without waiting for the setup or teardown of other tests. This results in **faster feedback loops**, which is particularly important in CI/CD pipelines.

#### **Example**:

* If tests are not isolated, you might have to wait for the setup and teardown of dependent tests. This can slow down test execution.
* Isolated tests allow for running tests concurrently, which can speed up the overall test suite execution.

---

### **4. Simplifies Test Maintenance**

As your project grows, **isolated tests are easier to maintain**. When tests are tightly coupled with each other, changes in one part of the code might require changes to many tests, increasing the maintenance burden. With isolated tests, you only need to modify the tests that are directly impacted by the changes in the codebase.

#### **Example**:

* A change to the logic of a method in an isolated unit test requires updating only the specific test that covers that logic.
* In a non-isolated test suite, changing one part of the system could force updates across multiple tests, even if those tests are unrelated.

---

### **5. Helps Avoid Side Effects**

Test isolation helps prevent **side effects** from one test influencing another. Side effects happen when a test modifies a shared resource (e.g., a global variable, a database, a file system) and that modification affects other tests. By isolating tests, side effects are minimized or eliminated entirely.

#### **Example**:

* A test that writes to a file or modifies a database could affect the results of other tests that rely on that file or database being in a certain state. This is especially problematic in integration or system tests where external resources are involved.

---

### **6. Supports Parallel Testing**

Isolated tests can be run in parallel without any conflicts. When tests depend on shared resources, running them concurrently can lead to race conditions, data corruption, and inconsistent results. Test isolation allows parallel execution, which helps scale testing and makes it more efficient.

#### **Example**:

* In an isolated test suite, you can safely run tests on different threads or machines without worrying about shared state causing conflicts.
* In a non-isolated suite, tests might overwrite or alter shared resources, causing failures in concurrent executions.

---

### **How to Achieve Test Isolation**

Here are a few best practices to ensure test isolation:

---

### **1. Mocking External Dependencies**

Use **mocks** or **stubs** to replace external systems or dependencies (e.g., databases, APIs, file systems) with controlled, predictable behaviors. This way, tests don’t rely on external systems, which can be slow or unreliable.

#### **Example (Mockito)**:

```java
@Mock
private MyService myService;

@Test
void testMethod() {
    when(myService.someMethod()).thenReturn("Expected Value");
    
    // Test logic without interacting with the actual MyService
    assertEquals("Expected Value", myService.someMethod());
}
```

---

### **2. Avoiding Shared State**

Ensure that tests do not share state, such as global variables, static fields, or databases. Always reset any shared resources or mock setups between tests.

#### **Example**:

In JUnit, you can use `@BeforeEach` and `@AfterEach` to set up and tear down any resources that could potentially interfere with other tests.

```java
@BeforeEach
void setup() {
    // Reset state or mock setups
}

@AfterEach
void tearDown() {
    // Clean up after the test
}
```

---

### **3. Use Test-Specific Configurations**

If your application uses configuration files (like `application.properties` or `application.yml`), use test-specific configurations to ensure that tests don’t impact the main application’s state.

#### **Example**:

```java
@TestConfiguration
public class TestConfig {
    @Bean
    public MyService myService() {
        return new MyServiceImpl();
    }
}
```

---

### **4. Database Isolation**

If tests rely on a database, use **embedded databases** like **H2** or **in-memory databases** for tests. This ensures that the tests don’t affect the actual production database.

#### **Example (H2 Database)**:

```java
@H2DataSource
@Test
void testDatabaseMethod() {
    // Test using an in-memory H2 database that is isolated from production
}
```

---

### **5. Parallel Test Execution**

Leverage frameworks or CI tools that allow **parallel test execution**. This is easier when tests are isolated, and it can significantly speed up your testing process.

---

### **Conclusion**

Test isolation is crucial for ensuring that your unit tests are **reliable, maintainable**, and **easy to debug**. It helps in preventing side effects, makes tests run faster, and ensures they are independent of each other. By using practices like mocking dependencies, avoiding shared state, using test-specific configurations, and managing resources effectively, you can achieve test isolation and ensure the robustness of your test suite.

---

## 82. How do you write unit tests for legacy code?

### **How to Write Unit Tests for Legacy Code**

Writing unit tests for legacy code can be a challenging task due to several factors, such as lack of documentation, dependencies on external systems, tight coupling, and the absence of test cases. However, it’s a crucial step in improving the maintainability and quality of legacy code. The key is to start small and refactor incrementally while ensuring that existing functionality is preserved.

Here’s a detailed approach to writing unit tests for legacy code:

---

### **1. Understand the Legacy Code and Identify Testable Units**

Before writing unit tests, it’s essential to understand the legacy code. In many cases, the code might not be structured with testing in mind. Therefore, the first step is to identify **units of code** that can be tested in isolation.

#### **Steps:**

* **Read and understand the code**: Spend time understanding the functionality and behavior of the code you’re dealing with. Understand its methods, inputs, outputs, and interactions.
* **Break down large methods or classes**: Legacy code often contains large, monolithic methods or classes. Break them into smaller, more manageable pieces that can be tested.
* **Identify dependencies**: Look for external dependencies (e.g., databases, file systems, external APIs) that may need to be mocked or isolated.

---

### **2. Refactor for Testability (Small Refactors)**

Legacy code is often tightly coupled and difficult to test in its current form. The goal is to **refactor small pieces of code** at a time to improve testability without changing the functionality.

#### **Key Techniques for Refactoring:**

* **Extract methods**: If a method is doing too much, extract smaller, self-contained methods to isolate logic.
* **Break dependencies**: Use **dependency injection** or **factories** to decouple tightly bound components. For example, pass dependencies (like services or repositories) as arguments instead of hard-coding them.
* **Introduce interfaces**: If the code has hard dependencies on specific classes, consider creating interfaces or abstract classes to allow mocking and easier testing.

#### **Example**:

```java
// Legacy method
public void processOrder(Order order) {
    // Complex logic with database access, external services, etc.
    database.save(order);
    emailService.sendConfirmationEmail(order);
}

// Refactor to make it testable
public class OrderProcessor {
    private Database database;
    private EmailService emailService;
    
    public OrderProcessor(Database database, EmailService emailService) {
        this.database = database;
        this.emailService = emailService;
    }

    public void processOrder(Order order) {
        saveOrder(order);
        sendConfirmationEmail(order);
    }
    
    private void saveOrder(Order order) {
        database.save(order);
    }

    private void sendConfirmationEmail(Order order) {
        emailService.sendConfirmationEmail(order);
    }
}
```

---

### **3. Write Tests for Individual Methods**

Once the code is refactored, write unit tests for **individual methods** or components. Start with the most critical parts of the code, and ensure the logic is correct. Use a testing framework like **JUnit**, **TestNG**, or **Spock** to write tests.

#### **Steps:**

* **Write tests for small units**: Test individual methods or classes in isolation before testing complex scenarios.
* **Test inputs and outputs**: For each method, check if it produces the correct output for given inputs, and verify that side effects (like changes in state) are correct.
* **Use mocks for external dependencies**: If your legacy code interacts with external systems (e.g., databases, APIs), use mocking frameworks like **Mockito** to mock these dependencies.

#### **Example (JUnit 5)**:

```java
@Test
void testSaveOrder() {
    // Arrange
    Database mockDatabase = mock(Database.class);
    Order order = new Order("123", "Product A");
    OrderProcessor processor = new OrderProcessor(mockDatabase, mock(EmailService.class));
    
    // Act
    processor.processOrder(order);
    
    // Assert
    verify(mockDatabase).save(order);
}
```

---

### **4. Isolate External Dependencies (Use Mocks or Stubs)**

Legacy code often interacts with external systems (like databases, file systems, or third-party APIs) that are difficult or impossible to unit test. Use **mocking** or **stubbing** to isolate these dependencies so that the unit tests only focus on the logic of the code.

#### **Steps:**

* **Mock external services**: If the legacy code depends on external services, such as databases, APIs, or messaging systems, use a mocking framework (e.g., **Mockito**, **PowerMock**) to simulate these services.
* **Use in-memory databases**: For database interactions, use an in-memory database (like **H2**) to test code that interacts with the database without affecting production systems.
* **Stub complex dependencies**: If mocking is not feasible for complex or non-deterministic dependencies, use stubbing to simulate their behavior in tests.

#### **Example (Mockito)**:

```java
@Mock
private Database mockDatabase;

@Test
void testOrderProcessingWithMock() {
    Order order = new Order("123", "Product A");
    OrderProcessor processor = new OrderProcessor(mockDatabase, mock(EmailService.class));
    
    processor.processOrder(order);
    
    // Verify that the database method is called
    verify(mockDatabase).save(order);
}
```

---

### **5. Write Tests Incrementally (Don’t Test Everything at Once)**

When working with legacy code, it’s often not practical to write tests for the entire system all at once. Instead, start with **small, incremental improvements** and test small parts of the system over time.

#### **Steps:**

* **Start with critical parts**: Focus on testing the most important or risky parts of the code first. For example, areas with complex business logic or where bugs have been previously found.
* **Test after each change**: After refactoring or adding new tests, run your test suite to ensure that you haven’t broken anything. Use a **Continuous Integration (CI)** tool to automate this process.
* **Refactor and test iteratively**: Don’t try to test the entire legacy codebase in one go. Instead, continuously refactor small parts and add tests as you go.

---

### **6. Use Test Coverage Tools**

To ensure you have good coverage of the legacy code, use **code coverage** tools like **JaCoCo** or **Cobertura**. These tools help identify areas of the code that are not covered by tests and may highlight critical areas that need additional test coverage.

#### **Steps:**

* **Run code coverage**: After writing unit tests for a specific part of the code, run a coverage tool to ensure that all branches and paths of the code are tested.
* **Focus on untested areas**: Pay particular attention to uncovered branches or methods, as they may indicate untested edge cases or important logic.

---

### **7. Avoid Large Refactors in One Go**

Avoid doing large refactors without tests, especially if the legacy code is highly coupled or hard to understand. Doing large-scale changes without proper unit tests can break the code or introduce subtle bugs that are hard to track.

#### **Steps:**

* **Refactor incrementally**: Break down your refactoring efforts into smaller, manageable pieces. After each refactor, ensure that the existing tests pass and that no functionality is broken.
* **Write tests after each change**: Whenever you refactor a part of the code, write tests for that specific area to ensure that the changes didn’t introduce errors.

---

### **8. Test Legacy Code in a Realistic Environment (Integration Tests)**

While unit tests are important, it’s also crucial to write **integration tests** for parts of the system that rely on real external resources (like databases or third-party APIs). This ensures that the system behaves correctly in a realistic environment.

#### **Steps:**

* **Use integration tests for critical flows**: Write integration tests to test how the system behaves when interacting with external systems.
* **Use real data or services**: For certain parts of the application, you might need to use real services or external systems to ensure the code functions properly under real conditions.

---

### **9. Be Prepared to Refactor for Testability Over Time**

In many cases, legacy code is not written with testing in mind. You will need to spend some time refactoring and restructuring the code to make it more testable. However, **don’t overdo it**; focus on making small changes that improve testability and avoid large refactors that could break functionality.

#### **Steps:**

* **Test first, refactor later**: Write tests for legacy code as much as possible before doing any major refactoring. Once the tests are in place, you can refactor with more confidence.
* **Refactor in small increments**: Make incremental changes to improve testability, such as breaking up monolithic methods or introducing interfaces for easier mocking.

---

### **Conclusion**

Writing unit tests for legacy code is challenging but essential for improving the maintainability and quality of your codebase. The key strategies include:

* **Understand the code** and identify testable units.
* **Refactor incrementally** for testability without changing functionality.
* **Use mocks and stubs** to isolate external dependencies.
* **Write tests incrementally**, focusing on the most critical parts of the system.
* **Use code coverage tools** to identify untested areas.
* **Be patient** and refactor gradually to avoid breaking changes.

By following these strategies, you can successfully write unit tests for legacy code and improve the reliability of your application over time.

---

## 83. What is a mock vs stub vs fake?

### **Mock vs Stub vs Fake in Testing**

In software testing, especially in unit testing, the terms **mock**, **stub**, and **fake** refer to different types of test doubles used to isolate components under test, manage dependencies, and simulate certain behaviors or conditions in your tests. These test doubles help you test parts of the system independently, ensuring that the focus remains on the unit being tested. Here's a breakdown of each:

---

### **1. Stub**

A **stub** is a test double that provides predefined responses to method calls made during a test. Stubs are used to simulate the behavior of a component that the unit being tested depends on, typically for cases where the actual component’s behavior is either difficult, expensive, or unnecessary to call in the test.

#### **Characteristics of a Stub:**

* **Returns predefined values**: A stub is designed to return a specific value when a method is called, often used for controlling the test environment or conditions.
* **Simplified behavior**: It doesn't verify the behavior of the code being tested; it simply returns data to simulate a situation.
* **Isolates behavior**: Helps isolate the unit under test by replacing external calls or dependencies with predictable, controlled behavior.

#### **Example**:

```java
// A Stub in action:
class DatabaseStub {
    public String fetchUser(String userId) {
        return "John Doe"; // Returns a predefined value
    }
}

@Test
void testFetchUser() {
    DatabaseStub stub = new DatabaseStub();
    String user = stub.fetchUser("123");
    assertEquals("John Doe", user);  // No real database interaction, just a stubbed return
}
```

In this example, the `DatabaseStub` doesn't simulate the full functionality of a database; it simply returns a predefined string when `fetchUser` is called.

---

### **2. Mock**

A **mock** is a test double that not only simulates the behavior of an external dependency, like a stub, but also **verifies** interactions and behavior. Mocks are used to check if certain methods were called with the correct parameters, the number of times they were called, or in a specific order. Mocks help ensure that your code is interacting with its dependencies as expected.

#### **Characteristics of a Mock:**

* **Verification of behavior**: Mocks are used to verify interactions, such as checking if a method was called with the correct arguments.
* **Doesn’t necessarily return predefined values**: Mocks can return predefined values, but their primary role is to track and verify the behavior of the code under test.
* **Used for behavioral testing**: Mocks help ensure that the unit under test interacts with its dependencies correctly.

#### **Example (using Mockito)**:

```java
// A Mock in action (Mockito)
@Test
void testSendEmail() {
    EmailService mockEmailService = mock(EmailService.class);
    
    // Simulate a call to sendEmail, no real service interaction
    doNothing().when(mockEmailService).sendEmail(anyString());
    
    // Call the method under test
    NotificationService notificationService = new NotificationService(mockEmailService);
    notificationService.sendUserNotification("user@example.com");
    
    // Verify that the sendEmail method was called with the expected argument
    verify(mockEmailService).sendEmail("user@example.com");
}
```

In this example, `mockEmailService` simulates the behavior of an email service, and we verify that `sendEmail` was called with the correct parameter (`"user@example.com"`).

---

### **3. Fake**

A **fake** is a test double that has a working implementation, but it's simpler than the real thing. Fakes often provide a lightweight, functional version of a component that can be used in tests, and it is used when you need a component to have some real functionality but don’t want to use the full version (like a real database or a real external API).

#### **Characteristics of a Fake:**

* **Has working functionality**: Unlike mocks or stubs, fakes provide a **simplified** version of a component that can perform real logic, but at a simpler, more controlled scale.
* **Simulates behavior of a real component**: A fake might use in-memory data structures (e.g., an in-memory database or a fake file system) to simulate the real component’s behavior.
* **Can be used in integration or acceptance tests**: Fakes can be used in tests where full integration is needed, but a lightweight version is acceptable.

#### **Example (Fake in memory database)**:

```java
// A Fake in action: In-memory fake database
class FakeDatabase {
    private Map<String, String> data = new HashMap<>();
    
    public void save(String key, String value) {
        data.put(key, value);
    }
    
    public String fetch(String key) {
        return data.get(key);
    }
}

@Test
void testDatabaseSave() {
    FakeDatabase fakeDb = new FakeDatabase();
    fakeDb.save("user1", "John Doe");
    
    // Test the actual saving behavior (real implementation in a fake form)
    String result = fakeDb.fetch("user1");
    assertEquals("John Doe", result);  // Real functionality in a fake environment
}
```

Here, `FakeDatabase` is a simplified version of a real database: it uses an in-memory map to simulate database storage. The fake provides real functionality (storing and fetching data) but doesn’t have the complexity of interacting with a real database.

---

### **Differences Summary**

| Feature                   | **Mock**                                  | **Stub**                                                       | **Fake**                                                 |
| ------------------------- | ----------------------------------------- | -------------------------------------------------------------- | -------------------------------------------------------- |
| **Purpose**               | Verifies interactions and behavior        | Provides predefined responses                                  | Provides working functionality in a simplified form      |
| **Focus**                 | Behavior verification                     | State control (returns values)                                 | Realistic but simplified behavior (in-memory DB, etc.)   |
| **Use Case**              | Test how code interacts with dependencies | Isolate unit under test by controlling dependencies' responses | Simulate real components with simplified implementations |
| **Example Tools**         | Mockito, JMock, EasyMock                  | Mockito (stubbing), JMock                                      | In-memory databases, simple file systems                 |
| **Behavior Verification** | Yes, checks interactions                  | No                                                             | No (or limited)                                          |

---

### **When to Use Each:**

* **Stub**: When you need to provide a controlled environment for a unit test, like returning a specific value when a dependency method is called.
* **Mock**: When you need to ensure that a certain behavior occurs, like ensuring that a method is called with specific parameters, or verifying interaction with a dependency.
* **Fake**: When you want to test in a simplified, controlled environment but still need some real logic, such as an in-memory database or a fake file system.

Each of these test doubles has its own specific role and is useful in different scenarios depending on the type of testing you need to perform. They help ensure that your unit tests are isolated, manageable, and focused on the component under test.

---

## 84. How do you test asynchronous code?

Testing asynchronous code can be tricky because you need to ensure that the test waits for the asynchronous process to complete before making assertions. Fortunately, there are several strategies and tools available in Java to help with testing asynchronous code. Let's look at some common techniques.

### 1. **Using `Future` or `CompletableFuture`**

For asynchronous code that uses `Future` or `CompletableFuture` to represent the result of a computation that may be completed in the future, you can use methods like `get()` to block until the result is available.

#### Example with `CompletableFuture`:

```java
import java.util.concurrent.CompletableFuture;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class AsyncTest {

    @Test
    public void testAsyncMethod() throws Exception {
        // Simulating an asynchronous method
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
            return "Hello, World!";
        });

        // Blocking call to get the result
        String result = future.get();

        // Verifying the result
        assertEquals("Hello, World!", result);
    }
}
```

In this example, `CompletableFuture.supplyAsync()` executes an asynchronous operation. The `get()` method is used to block until the operation completes, and then the result is asserted.

---

### 2. **Using `@Test` with `assertTimeout` in JUnit**

JUnit 5 provides the `assertTimeout` method, which allows you to ensure that asynchronous tasks finish within a given time frame. This can help you verify that an asynchronous operation completes within an expected duration.

#### Example with `assertTimeout`:

```java
import org.junit.jupiter.api.Test;
import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;
import static org.junit.jupiter.api.Assertions.assertTimeout;

public class AsyncTest {

    @Test
    void testAsyncMethodTimeout() {
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
            try {
                TimeUnit.SECONDS.sleep(2); // Simulating delay
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
            return "Hello, World!";
        });

        // Ensure the future completes within 3 seconds
        assertTimeout(java.time.Duration.ofSeconds(3), () -> {
            future.get();  // Wait for the result
        });
    }
}
```

Here, `assertTimeout` checks that the asynchronous method completes within the specified time. If it takes longer, the test fails.

---

### 3. **Using `CountDownLatch`**

A `CountDownLatch` is a synchronization aid that allows one or more threads to wait until a set of operations being performed in other threads completes. You can use this in your test to wait for asynchronous operations to complete.

#### Example with `CountDownLatch`:

```java
import java.util.concurrent.CountDownLatch;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class AsyncTest {

    @Test
    void testAsyncMethodWithCountDownLatch() throws InterruptedException {
        CountDownLatch latch = new CountDownLatch(1);

        // Simulate an asynchronous operation
        new Thread(() -> {
            try {
                Thread.sleep(1000);  // Simulating delay
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
            latch.countDown();  // Signal that the task is complete
        }).start();

        // Wait for the asynchronous task to complete
        latch.await();

        // Proceed with assertions after the async task is completed
        assertEquals(1, latch.getCount());  // The latch should be decremented to 0
    }
}
```

Here, the test waits for the `CountDownLatch` to count down to zero, indicating that the asynchronous task has completed before making assertions.

---

### 4. **Using `@Async` and `@EnableAsync` with Spring**

In Spring, if you're using the `@Async` annotation to mark methods for asynchronous execution, you can use `CompletableFuture` or `ListenableFuture` to test asynchronous behavior. Spring's testing support includes features for testing asynchronous code.

#### Example with `@Async` in Spring:

```java
import org.springframework.scheduling.annotation.Async;
import org.springframework.stereotype.Service;
import org.springframework.test.context.junit.jupiter.SpringExtension;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import static org.junit.jupiter.api.Assertions.assertEquals;
import java.util.concurrent.CompletableFuture;

@Service
public class AsyncService {
    @Async
    public CompletableFuture<String> asyncMethod() throws InterruptedException {
        Thread.sleep(1000);  // Simulate some work
        return CompletableFuture.completedFuture("Async Result");
    }
}

@ExtendWith(SpringExtension.class)
class AsyncServiceTest {

    private AsyncService asyncService = new AsyncService();

    @Test
    void testAsyncMethod() throws Exception {
        CompletableFuture<String> future = asyncService.asyncMethod();
        
        // Wait for the result and check it
        String result = future.get();
        assertEquals("Async Result", result);
    }
}
```

In this example, the `@Async` annotation makes the method run asynchronously. The test waits for the result using `get()` on the `CompletableFuture`.

---

### 5. **Using `@Timeout` for Parallel Execution**

JUnit 5 provides a `@Timeout` annotation that ensures a test does not run longer than the specified timeout, which can be helpful for asynchronous testing, especially when you want to enforce execution time limits on async methods.

#### Example with `@Timeout`:

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.Timeout;

import java.util.concurrent.CompletableFuture;
import java.util.concurrent.TimeUnit;

import static org.junit.jupiter.api.Assertions.assertEquals;

public class AsyncTest {

    @Test
    @Timeout(value = 3, unit = TimeUnit.SECONDS)  // Test will fail if execution takes longer than 3 seconds
    void testAsyncMethodTimeout() throws Exception {
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
            try {
                TimeUnit.SECONDS.sleep(2);  // Simulating delay
            } catch (InterruptedException e) {
                Thread.currentThread().interrupt();
            }
            return "Hello, World!";
        });

        String result = future.get();  // This will block until the result is available
        assertEquals("Hello, World!", result);  // Assert the result
    }
}
```

With `@Timeout`, you ensure that the test fails if the asynchronous method does not finish within the given time.

---

### Key Points to Keep in Mind:

* **Blocking calls**: In unit tests, sometimes you have to block on asynchronous results using `get()`, but make sure you don’t block indefinitely. Always set a reasonable timeout.
* **Test frameworks**: JUnit 5 and Spring offer useful utilities like `@Timeout`, `@Async`, and `CompletableFuture` to manage and test asynchronous code.
* **Synchronization mechanisms**: `CountDownLatch`, `CyclicBarrier`, and `Semaphore` are useful for waiting for threads or asynchronous operations to complete before proceeding with assertions.

By using these techniques, you can effectively test asynchronous code and ensure that your application’s behavior is correct even when working with concurrent processes.

---

## 85. How do you handle multithreaded testing scenarios?

Handling multithreaded testing scenarios can be quite challenging due to the complexity introduced by concurrency, such as race conditions, deadlocks, and timing issues. However, with proper testing strategies, tools, and techniques, you can effectively test multithreaded code. Below are some approaches you can take when dealing with multithreaded testing:

### 1. **Use Synchronization Primitives (e.g., `CountDownLatch`, `CyclicBarrier`)**

Synchronization primitives like `CountDownLatch`, `CyclicBarrier`, or `Semaphore` are useful to manage the timing and order of thread execution during testing.

* **`CountDownLatch`**: Allows one or more threads to wait until a set of operations are completed by other threads.
* **`CyclicBarrier`**: Similar to `CountDownLatch` but reusable after all threads reach the barrier.
* **`Semaphore`**: Controls access to shared resources by a set of threads.

#### Example with `CountDownLatch`:

```java
import java.util.concurrent.CountDownLatch;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class MultiThreadedTest {

    @Test
    void testMultithreadedExecution() throws InterruptedException {
        int threadCount = 5;
        CountDownLatch latch = new CountDownLatch(threadCount);
        final int[] sharedCounter = {0};

        // Create and start 5 threads
        for (int i = 0; i < threadCount; i++) {
            new Thread(() -> {
                // Simulate some work
                try {
                    Thread.sleep(100);  // Simulate work
                    synchronized (sharedCounter) {
                        sharedCounter[0]++;  // Modify shared counter
                    }
                } catch (InterruptedException e) {
                    Thread.currentThread().interrupt();
                } finally {
                    latch.countDown();  // Signal that the thread is done
                }
            }).start();
        }

        // Wait for all threads to finish
        latch.await();

        // Verify the result (all threads should have incremented the counter)
        assertEquals(threadCount, sharedCounter[0]);
    }
}
```

In this example, `CountDownLatch` ensures that the main thread waits for all 5 threads to finish their work before verifying the result.

---

### 2. **Avoiding Shared State (Immutability)**

When testing multithreaded code, shared mutable state can lead to race conditions and unpredictable behavior. If possible, try to design the code in such a way that each thread operates on its own isolated data (or immutable data). This minimizes the chances of encountering concurrency issues.

#### Example with thread-local storage:

```java
public class ThreadLocalExample {

    private static final ThreadLocal<Integer> threadLocalCounter = ThreadLocal.withInitial(() -> 0);

    public static void increment() {
        threadLocalCounter.set(threadLocalCounter.get() + 1);
    }

    public static int getCounter() {
        return threadLocalCounter.get();
    }
}

@Test
void testThreadLocal() throws InterruptedException {
    Thread thread1 = new Thread(() -> {
        ThreadLocalExample.increment();
        ThreadLocalExample.increment();
    });

    Thread thread2 = new Thread(() -> {
        ThreadLocalExample.increment();
    });

    thread1.start();
    thread2.start();

    thread1.join();
    thread2.join();

    // Each thread should have its own counter
    assertEquals(2, ThreadLocalExample.getCounter());  // Should be 1 for each thread
}
```

In this example, `ThreadLocal` ensures each thread maintains its own counter, which prevents concurrency issues from arising.

---

### 3. **Using ExecutorService for Thread Pool Management**

When creating multiple threads, managing them with an `ExecutorService` provides better control over thread execution, making it easier to handle scenarios like timeouts, thread pooling, and waiting for completion.

#### Example with `ExecutorService`:

```java
import java.util.concurrent.*;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertTrue;

public class ExecutorServiceTest {

    @Test
    void testExecutorService() throws InterruptedException, ExecutionException {
        ExecutorService executor = Executors.newFixedThreadPool(3);
        Callable<Integer> task = () -> {
            Thread.sleep(500); // Simulate some work
            return 42;
        };

        // Submit tasks to the executor
        Future<Integer> future1 = executor.submit(task);
        Future<Integer> future2 = executor.submit(task);

        // Wait for the results
        Integer result1 = future1.get();
        Integer result2 = future2.get();

        // Verify results
        assertTrue(result1 == 42);
        assertTrue(result2 == 42);

        executor.shutdown();
    }
}
```

This example uses `ExecutorService` to manage thread execution, submit tasks, and collect results.

---

### 4. **Using `assertTimeout` for Time-Based Assertions**

For multithreaded tests, especially those where threads must finish within a specific time, you can use `assertTimeout` (JUnit 5) to assert that the threads complete their tasks within the expected time limit.

#### Example with `assertTimeout`:

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.Timeout;
import java.util.concurrent.*;

import static org.junit.jupiter.api.Assertions.assertTrue;

public class TimeoutTest {

    @Test
    @Timeout(value = 2, unit = TimeUnit.SECONDS)
    void testMultithreadedWithTimeout() throws InterruptedException, ExecutionException {
        ExecutorService executor = Executors.newFixedThreadPool(2);

        Callable<Integer> task = () -> {
            Thread.sleep(1500);  // Simulate some work
            return 100;
        };

        // Submit tasks and assert that they complete within the timeout
        Future<Integer> future1 = executor.submit(task);
        Future<Integer> future2 = executor.submit(task);

        assertTrue(future1.get() == 100);
        assertTrue(future2.get() == 100);

        executor.shutdown();
    }
}
```

Here, `@Timeout` ensures that the test will fail if the threads don’t complete within the specified time.

---

### 5. **Use of `Atomic` Variables for Shared State**

To avoid issues with thread contention and ensure atomicity, you can use `Atomic` variables like `AtomicInteger`, `AtomicLong`, etc., for shared mutable state. These classes provide thread-safe operations that help prevent race conditions in multithreaded environments.

#### Example with `AtomicInteger`:

```java
import java.util.concurrent.atomic.AtomicInteger;
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class AtomicTest {

    @Test
    void testAtomicCounter() throws InterruptedException {
        AtomicInteger counter = new AtomicInteger(0);
        int threadCount = 5;

        // Create and start threads
        Thread[] threads = new Thread[threadCount];
        for (int i = 0; i < threadCount; i++) {
            threads[i] = new Thread(() -> {
                counter.incrementAndGet();  // Atomically increment counter
            });
            threads[i].start();
        }

        // Wait for all threads to finish
        for (Thread thread : threads) {
            thread.join();
        }

        // Verify that the counter was incremented correctly
        assertEquals(threadCount, counter.get());
    }
}
```

`AtomicInteger` ensures that each increment operation is atomic and thread-safe, preventing race conditions from occurring.

---

### 6. **Verifying Thread Behavior (Using Mocking Frameworks)**

You can also use mocking frameworks like **Mockito** to verify the behavior of threads or other concurrent operations. While you generally don't mock threads directly, you can mock dependencies that interact with threads, such as asynchronous services or thread pools.

#### Example (Mocking a thread pool with Mockito):

```java
import static org.mockito.Mockito.*;
import java.util.concurrent.*;

public class ThreadPoolMockTest {

    @Test
    void testThreadPoolWithMockito() throws InterruptedException, ExecutionException {
        ExecutorService mockExecutor = mock(ExecutorService.class);
        Callable<Integer> task = () -> 42;

        // Mock the submit method to return a completed future
        Future<Integer> mockFuture = mock(Future.class);
        when(mockExecutor.submit(task)).thenReturn(mockFuture);
        when(mockFuture.get()).thenReturn(42);

        // Call the mock submit method
        Future<Integer> future = mockExecutor.submit(task);

        // Verify that the result is as expected
        assertEquals(42, future.get());
        verify(mockExecutor).submit(task);
    }
}
```

In this example, we mock the `ExecutorService` to test how the code interacts with it without actually executing tasks in a real thread pool.

---

### 7. **Test Parallel Execution with `@ParameterizedTest` or `@RepeatedTest`**

JUnit 5 offers the `@ParameterizedTest` and `@RepeatedTest` annotations, which can be used to execute tests concurrently in some scenarios. These tests can be useful for verifying that multithreaded code behaves as expected in repeated or parameterized conditions.

---

### Key Considerations for Multithreaded Testing:

* **Race conditions**: Make sure to identify and test for potential race conditions by controlling the timing and order of thread execution.
* **Test isolation**: Ensure tests are independent of one another, especially when using shared resources.
* **Thread safety**: Use thread-safe constructs like `AtomicInteger`, `CountDownLatch`, `Semaphore`, or `CyclicBarrier` to prevent concurrency issues.
* **Synchronization**: Be mindful of how threads are synchronized in the code under test to avoid deadlocks or improper sequencing.
* **Timeouts**: Always set timeouts to prevent tests from hanging indefinitely.

By employing the right synchronization mechanisms, thread-safe practices, and leveraging testing tools like JUnit, Mockito, or ExecutorService, you can effectively handle and test multithreaded scenarios in Java.

---

## 86. What are integration tests and how are they different from unit tests?

### **What are Integration Tests?**

**Integration tests** are designed to test the interaction between multiple components or systems to ensure they work together as expected. The goal of integration testing is to verify that different parts of the application, such as services, databases, external APIs, or any other system, interact correctly. Unlike unit tests, which test individual components in isolation, integration tests evaluate the collaboration of components in a more real-world environment.

### **Key Characteristics of Integration Tests:**

1. **Multiple Components**: Integration tests check the interaction between multiple components (e.g., database, APIs, third-party services) within the system.
2. **End-to-End Flow**: They often simulate a more realistic environment, involving the actual execution of code that calls external systems, databases, or services.
3. **External Dependencies**: Integration tests may interact with actual services (such as databases, message brokers, file systems, etc.) or mock those services to validate communication.
4. **Data**: These tests might involve real data or a subset of data that mimics the real-world environment.

### **Example of an Integration Test in Spring Boot:**

Consider testing a service that communicates with a database to retrieve user data:

```java
@SpringBootTest
public class UserServiceIntegrationTest {

    @Autowired
    private UserService userService;  // Service under test

    @Autowired
    private UserRepository userRepository;  // Repository to access database

    @Test
    void testFindUserById() {
        // Arrange: Set up the test data
        User user = new User("John", "Doe");
        userRepository.save(user);  // Save data in the real DB

        // Act: Call the service method
        User foundUser = userService.findUserById(user.getId());

        // Assert: Check if the returned user matches the saved data
        assertNotNull(foundUser);
        assertEquals("John", foundUser.getFirstName());
        assertEquals("Doe", foundUser.getLastName());
    }
}
```

In this example, the integration test involves the actual database (`userRepository`) to verify if the `UserService` works as expected when retrieving data. The test checks the complete flow, from saving data to retrieving it from the database.

---

### **How are Integration Tests Different from Unit Tests?**

#### **1. Scope of Testing:**

* **Unit Tests**: Unit tests focus on testing individual components (methods, classes) in isolation. The goal is to verify the logic of a single unit of work, often without dependencies on external systems.

    * **Example**: Testing a `Calculator` class that adds two numbers. The test only checks the addition logic and doesn’t interact with external systems.
* **Integration Tests**: Integration tests, on the other hand, focus on testing how different components or systems work together. They might include external dependencies like databases, message queues, or third-party APIs.

    * **Example**: Testing a service that calls a database to save and retrieve data. The test ensures that the service integrates well with the database.

#### **2. Dependencies:**

* **Unit Tests**: Unit tests typically mock or stub any external dependencies (such as databases, network services, etc.). This ensures the unit test focuses purely on the component’s internal logic.

* **Integration Tests**: Integration tests often use actual external dependencies (e.g., a real database, an actual REST API) to verify that components interact correctly with the outside world.

#### **3. Speed:**

* **Unit Tests**: Unit tests are generally very fast since they don't involve real systems and only test the logic of a small unit of work (like a method).

* **Integration Tests**: Integration tests are slower because they involve actual interactions with external systems, which can take more time (e.g., database writes/reads, API calls).

#### **4. Test Environment:**

* **Unit Tests**: Unit tests run in a controlled, isolated environment, often using mocks, stubs, or fakes to simulate external dependencies.

* **Integration Tests**: Integration tests run in a more complete environment, sometimes requiring a real database, a mock server, or even the entire application running to ensure proper integration.

#### **5. Granularity:**

* **Unit Tests**: Unit tests are granular, testing one small aspect of the application (e.g., a method or function).

* **Integration Tests**: Integration tests are more coarse-grained, testing a broader range of interactions between components (e.g., service-to-database, service-to-API).

---

### **Comparison Table:**

| **Aspect**           | **Unit Tests**                                  | **Integration Tests**                               |
| -------------------- | ----------------------------------------------- | --------------------------------------------------- |
| **Scope**            | Tests individual units/components in isolation  | Tests interaction between multiple components       |
| **Dependencies**     | Mocks or stubs external dependencies            | Uses real or mocked external systems like DBs, APIs |
| **Speed**            | Fast                                            | Slower, due to external system interactions         |
| **Test Environment** | Isolated, minimal dependencies                  | Requires actual components or systems integrated    |
| **Granularity**      | Fine-grained, tests specific methods or classes | Coarse-grained, tests broader application behavior  |
| **Typical Goal**     | Verify correctness of specific functionality    | Verify correct integration between components       |
| **Test Failures**    | Failures are easier to trace to specific code   | Failures may involve multiple components or systems |

---

### **When to Use Unit Tests vs Integration Tests?**

* **Unit Tests**:

    * Used to validate the logic of individual methods or classes.
    * Ensures that individual components are working as expected.
    * Should be run frequently and provide quick feedback.
    * Example: Verifying that a method correctly calculates a result based on inputs.

* **Integration Tests**:

    * Used to verify that multiple components (e.g., services, repositories, APIs) work together as expected.
    * Ensures that the system as a whole behaves correctly when components interact.
    * Runs less frequently than unit tests due to their longer execution time.
    * Example: Ensuring that a service interacts correctly with a database to store and retrieve data.

---

### **Best Practices for Integration Testing:**

1. **Use in Combination with Unit Tests**: While unit tests focus on individual components, integration tests verify the interactions between components. Both are necessary for comprehensive testing.
2. **Use Test Profiles for Isolation**: In Spring Boot, use test profiles to isolate the testing environment (e.g., different database, different API endpoints) for integration tests.
3. **Mock External Systems**: If interacting with external systems (e.g., third-party APIs), consider mocking them to avoid dependencies on live systems during tests.
4. **Focus on Critical Flows**: Integration tests are usually more expensive to run, so focus on critical paths where system components must work together.
5. **Clean Up Data**: When testing with real databases, ensure data is cleaned up after each test to maintain test integrity.

---

### Conclusion:

In summary, **unit tests** focus on validating the correctness of individual units of code in isolation, while **integration tests** focus on verifying that multiple components or systems work together as intended. Both are crucial for building reliable software: unit tests ensure that individual components work correctly, and integration tests ensure that the system as a whole functions as expected.

---

## 87. What’s the difference between black box and white box testing?

### **Black Box Testing vs. White Box Testing**

**Black box testing** and **white box testing** are two fundamental approaches to software testing, each focusing on different aspects of the application. Here's a detailed explanation of both:

---

### **Black Box Testing**

**Black box testing** is a testing approach where the tester does not need to know the internal workings of the application. The focus is on verifying the software’s functionality based on the inputs and expected outputs, without considering how the outputs are produced.

* **Tester’s Knowledge**: The tester does **not** need any knowledge of the internal structure, design, or implementation of the code.
* **Focus**: The focus is on testing the **functionality** of the system, i.e., does the system do what it is supposed to do?
* **Test Cases**: Test cases are based on requirements and specifications (functional requirements) and often involve **input-output** validation.
* **Goal**: To verify that the system works according to the expected behavior.

**Examples of Black Box Testing**:

* **Functional Testing**: Verifying whether a user can log in to the application with valid credentials.
* **Usability Testing**: Ensuring that the user interface is intuitive and user-friendly.
* **Acceptance Testing**: Verifying that the software meets the business requirements.

**Advantages**:

* Focuses on what the software does, not how it does it.
* Useful for validating the system's behavior from an end-user perspective.
* Test cases can be designed from the user’s viewpoint, so it’s more accessible to non-developers.

**Disadvantages**:

* Limited ability to test specific code paths or structures.
* Doesn’t provide insight into the internal issues or errors in the system.

---

### **White Box Testing**

**White box testing** (also known as **clear box**, **glass box**, or **structural testing**) involves testing the internal logic of the application. It requires knowledge of the code structure, and the tester has access to the source code and implementation details.

* **Tester’s Knowledge**: The tester **must** know the internal workings of the software (code, algorithms, design).
* **Focus**: The focus is on verifying the **internal logic**, data flow, and the correctness of the system's implementation.
* **Test Cases**: Test cases are designed based on the internal structure and logic of the code, including paths, branches, conditions, and loops.
* **Goal**: To ensure the internal functionality of the system is correct and efficient, and that all code paths are tested.

**Examples of White Box Testing**:

* **Unit Testing**: Testing individual functions or methods of a class.
* **Code Coverage Testing**: Ensuring all lines of code, branches, and paths are executed during tests.
* **Security Testing**: Verifying that the code handles vulnerabilities like SQL injection or buffer overflow.

**Advantages**:

* Can identify hidden software defects, logic errors, and security vulnerabilities in the code.
* Provides thorough testing of all paths, branches, and loops in the application.
* Easier to pinpoint the root cause of issues since the tester understands the code.

**Disadvantages**:

* Requires knowledge of the code, which may not be available to non-developers.
* Time-consuming since it requires analyzing the code and creating test cases for each possible path.
* Can lead to a focus on testing low-level code rather than overall system functionality.

---

### **Key Differences Between Black Box and White Box Testing**:

| **Aspect**                     | **Black Box Testing**                                                  | **White Box Testing**                                             |
| ------------------------------ | ---------------------------------------------------------------------- | ----------------------------------------------------------------- |
| **Knowledge of Internal Code** | No knowledge required of internal code (external view)                 | Requires knowledge of the internal code and logic (internal view) |
| **Focus**                      | Focus on functionality and behavior of the application                 | Focus on code structure, logic, and internal workings             |
| **Test Basis**                 | Based on specifications, requirements, and use cases                   | Based on code design, source code, and internal structure         |
| **Tester**                     | Can be performed by non-developers (e.g., QA, end-users)               | Requires skilled testers with knowledge of the code (developers)  |
| **Test Cases**                 | Test cases are based on inputs and expected outputs                    | Test cases are based on code logic, paths, and coverage           |
| **Type of Testing**            | Functional testing, acceptance testing, usability testing              | Unit testing, integration testing, path testing                   |
| **Tools**                      | Tools like Selenium, QTP, and TestComplete (for UI testing)            | Tools like JUnit, NUnit, and code coverage tools (e.g., JaCoCo)   |
| **Level of Testing**           | Typically done at higher levels (system, acceptance, integration)      | Typically done at lower levels (unit, integration, code-level)    |
| **Goal**                       | Validate the software meets user requirements and performs as expected | Validate the internal code logic and find vulnerabilities or bugs |

---

### **When to Use Black Box Testing vs White Box Testing?**

* **Black Box Testing**:

    * **When the focus is on user requirements and system behavior** rather than code implementation.
    * **End-user testing** or **acceptance testing**, where the actual functionality matters more than how it is implemented.
    * When testing **third-party software** or **pre-existing systems** where source code is not available.

* **White Box Testing**:

    * **When testing internal code** is required, such as during **unit testing**, **integration testing**, or **security testing**.
    * Useful when verifying the **correctness of code paths, branches**, and **data flow**.
    * When looking to **improve code quality**, check for **code coverage**, or identify **security vulnerabilities**.

---

### **Conclusion**

* **Black Box Testing** focuses on evaluating software functionality from an external perspective (user experience), without knowledge of how it is implemented internally.
* **White Box Testing** focuses on evaluating software from an internal perspective (code correctness and logic), requiring knowledge of the internal code structure and design.

Both testing types are essential and complement each other. Black box testing helps ensure that the application works as expected from the user's point of view, while white box testing ensures the internal workings are implemented correctly and efficiently.

---

## 88. How do you use assertions from AssertJ or Hamcrest?

### **Assertions in AssertJ and Hamcrest**

**AssertJ** and **Hamcrest** are two popular assertion libraries used in Java for writing fluent and readable test assertions. Both libraries provide expressive and flexible ways to validate conditions in tests, and they offer a richer set of assertions compared to JUnit's built-in assertions. Here's a detailed overview of both and how to use them.

---

### **1. AssertJ**

**AssertJ** is a Java library that provides a rich, fluent interface for writing assertions. It allows for writing more readable and expressive assertions in tests.

#### **Key Features of AssertJ**:

* Fluent API: Chain assertions in a natural and readable way.
* Rich Set of Assertions: AssertJ provides many methods to check collections, strings, numbers, exceptions, and more.
* Integration with JUnit: AssertJ can be used seamlessly with JUnit for both unit and integration tests.
* Detailed Error Messages: AssertJ gives more informative error messages when assertions fail.

#### **Basic Syntax Example**:

First, you need to include AssertJ in your project. For Maven:

```xml
<dependency>
    <groupId>org.assertj</groupId>
    <artifactId>assertj-core</artifactId>
    <version>3.22.0</version>
    <scope>test</scope>
</dependency>
```

For Gradle:

```gradle
testImplementation 'org.assertj:assertj-core:3.22.0'
```

Now, let’s look at some common AssertJ assertions.

#### **Examples**:

1. **Basic Assertions**:

   ```java
   import org.assertj.core.api.Assertions;

   @Test
   void testAssertions() {
       String str = "hello";
       int number = 5;
       
       // AssertJ provides fluent assertions
       Assertions.assertThat(str).isEqualTo("hello");  // checks if the string equals "hello"
       Assertions.assertThat(number).isGreaterThan(3);  // checks if number is greater than 3
   }
   ```

2. **Assertions on Collections**:

   ```java
   @Test
   void testCollection() {
       List<String> names = Arrays.asList("John", "Jane", "Tom");
       
       // Check that the list contains specific elements
       Assertions.assertThat(names).contains("Jane").doesNotContain("Peter");
       
       // Check that the list has the correct size
       Assertions.assertThat(names).hasSize(3);
   }
   ```

3. **Assertions on Objects**:

   ```java
   @Test
   void testObjectAssertions() {
       Person person = new Person("John", 25);
       
       // Check that an object’s property is correct
       Assertions.assertThat(person).extracting("name").isEqualTo("John");
       Assertions.assertThat(person).extracting("age").isGreaterThan(18);
   }
   ```

4. **Exception Assertions**:

   ```java
   @Test
   void testException() {
       Assertions.assertThatThrownBy(() -> {
           throw new IllegalArgumentException("Invalid argument");
       }).isInstanceOf(IllegalArgumentException.class)
         .hasMessage("Invalid argument");
   }
   ```

5. **Null Checks**:

   ```java
   @Test
   void testNull() {
       String str = null;
       
       Assertions.assertThat(str).isNull();
   }
   ```

---

### **2. Hamcrest**

**Hamcrest** is another popular library that allows you to write more expressive and readable assertions, often used in combination with JUnit. It focuses on using **matchers** that can be composed together to form more complex checks.

#### **Key Features of Hamcrest**:

* **Matchers**: Hamcrest uses matchers, which allow for flexible and composable assertions.
* **Readable Assertions**: Hamcrest provides a natural language-like style for writing assertions, which improves test readability.
* **Works Well with JUnit**: It's tightly integrated with JUnit for easy use in unit tests.

#### **Basic Syntax Example**:

First, you need to include Hamcrest in your project. For Maven:

```xml
<dependency>
    <groupId>org.hamcrest</groupId>
    <artifactId>hamcrest</artifactId>
    <version>2.2</version>
    <scope>test</scope>
</dependency>
```

For Gradle:

```gradle
testImplementation 'org.hamcrest:hamcrest:2.2'
```

Now, let’s look at some common Hamcrest assertions.

#### **Examples**:

1. **Basic Assertions**:

   ```java
   import static org.hamcrest.MatcherAssert.assertThat;
   import static org.hamcrest.Matchers.*;

   @Test
   void testAssertions() {
       String str = "hello";
       int number = 5;
       
       // Hamcrest assertions
       assertThat(str, is("hello"));  // checks if the string is "hello"
       assertThat(number, greaterThan(3));  // checks if number is greater than 3
   }
   ```

2. **Assertions on Collections**:

   ```java
   @Test
   void testCollection() {
       List<String> names = Arrays.asList("John", "Jane", "Tom");
       
       // Check that the list contains a specific element
       assertThat(names, hasItem("Jane"));
       assertThat(names, not(hasItem("Peter")));
   }
   ```

3. **Assertions on Objects**:

   ```java
   @Test
   void testObjectAssertions() {
       Person person = new Person("John", 25);
       
       // Check that object properties match expected values
       assertThat(person.getName(), is("John"));
       assertThat(person.getAge(), greaterThan(18));
   }
   ```

4. **Exception Assertions**:

   ```java
   @Test
   void testException() {
       Exception exception = assertThrows(IllegalArgumentException.class, () -> {
           throw new IllegalArgumentException("Invalid argument");
       });
       
       // Verify exception message
       assertThat(exception.getMessage(), is("Invalid argument"));
   }
   ```

5. **Null Checks**:

   ```java
   @Test
   void testNull() {
       String str = null;
       
       assertThat(str, is(nullValue()));
   }
   ```

---

### **Key Differences Between AssertJ and Hamcrest**

| **Feature**        | **AssertJ**                                                        | **Hamcrest**                                                    |
| ------------------ | ------------------------------------------------------------------ | --------------------------------------------------------------- |
| **API Style**      | Fluent and chainable syntax                                        | Uses matchers for composing assertions                          |
| **Error Messages** | Rich, clear, and detailed error messages                           | Error messages are less detailed                                |
| **Match Style**    | Focused on easy-to-read assertions with multiple assertion methods | Uses matchers (e.g., `is()`, `greaterThan()`) to compose checks |
| **Library Size**   | Slightly larger library                                            | Smaller and more focused on matchers                            |
| **Integration**    | Fully integrates with JUnit and other testing frameworks           | Commonly integrated with JUnit and other libraries like Mockito |
| **Learning Curve** | More readable and intuitive                                        | Requires learning how to use matchers                           |

---

### **When to Use AssertJ vs. Hamcrest?**

* **Use AssertJ**:

    * When you want a more **fluent and readable syntax** for assertions.
    * When you want **rich error messages** for easier debugging.
    * If you prefer to work with **a single library** for all types of assertions.

* **Use Hamcrest**:

    * If you're working with an existing codebase that already uses Hamcrest.
    * When you need to **compose assertions** using matchers for more complex validation.
    * If you're testing with a **JUnit environment** and prefer matchers or are using libraries like **Mockito** that use Hamcrest for argument matching.

---

### **Conclusion**

Both **AssertJ** and **Hamcrest** offer powerful assertion capabilities to make your tests more readable and maintainable. The choice between the two depends on your preference for a **fluent API** (AssertJ) or **matcher-based composition** (Hamcrest). Both libraries are excellent for improving the expressiveness and clarity of your assertions in tests.

---

## 89. What is the Arrange-Act-Assert pattern in testing?

### **The Arrange-Act-Assert (AAA) Pattern in Testing**

The **Arrange-Act-Assert (AAA)** pattern is a simple and widely used structure for writing unit tests. It helps improve the clarity and readability of tests by organizing them into three distinct sections:

1. **Arrange**: Set up the necessary conditions for the test.
2. **Act**: Execute the functionality that you want to test.
3. **Assert**: Verify that the behavior or result is as expected.

This pattern provides a clear, step-by-step flow to your tests, making them easier to understand and maintain.

---

### **1. Arrange**

The **Arrange** step is where you prepare the test environment. This typically involves:

* **Creating and initializing objects** or mock dependencies.
* **Setting up necessary preconditions** or inputs for the test.
* **Mocking services or repositories** (if necessary).
* **Setting up any required state** for the system under test.

The goal is to arrange the conditions so that the behavior you're going to test occurs under the right circumstances.

#### **Example**:

In the "Arrange" step, you might:

* Create a mock object for a service that a class depends on.
* Initialize an object that you are testing.

```java
// Arrange: Set up necessary objects and state
Calculator calculator = new Calculator();
int a = 5;
int b = 3;
```

---

### **2. Act**

The **Act** step is where you execute the code or method that you want to test. This is the main action you're validating in the test.

#### **Example**:

In the "Act" step, you might:

* Call the method you're testing with the arranged inputs.
* Perform an operation on the object you're testing.

```java
// Act: Perform the action you're testing
int result = calculator.add(a, b);
```

---

### **3. Assert**

The **Assert** step is where you verify that the behavior or result of the action matches what you expected. This is the part of the test that ensures the functionality works as intended.

#### **Example**:

In the "Assert" step, you check whether the output or state after the action is as expected. You can use assertions to compare expected values to actual ones.

```java
// Assert: Check if the result is as expected
assertEquals(8, result);
```

---

### **Full Example of Arrange-Act-Assert Pattern**

Let's put the three steps together in a simple test scenario for a **Calculator** class that adds two numbers.

```java
import static org.junit.jupiter.api.Assertions.assertEquals;
import org.junit.jupiter.api.Test;

public class CalculatorTest {

    @Test
    void testAddition() {
        // Arrange: Set up necessary objects and state
        Calculator calculator = new Calculator();
        int a = 5;
        int b = 3;

        // Act: Perform the action you're testing
        int result = calculator.add(a, b);

        // Assert: Check if the result is as expected
        assertEquals(8, result);
    }
}
```

In this example:

* **Arrange**: We create an instance of `Calculator` and define the inputs `a` and `b`.
* **Act**: We call the `add` method to calculate the result.
* **Assert**: We use `assertEquals` to check that the result is correct (expected 8).

---

### **Benefits of Using the AAA Pattern**

* **Clarity**: The three distinct steps help make the test case easy to read and understand. Anyone reading the test will immediately know what the setup is, what action is being performed, and what the expected result is.
* **Maintainability**: With clear separation of concerns, it's easier to maintain and modify tests over time.
* **Consistency**: The AAA pattern promotes consistency across test cases, making it easier for teams to follow a common style and for new team members to understand the tests quickly.
* **Debugging**: If a test fails, it's easier to pinpoint whether the failure is due to the arrangement, the action, or the assertion.

---

### **Variations of the AAA Pattern**

While the basic structure remains the same, you can adjust the pattern to fit more complex test scenarios:

1. **Arrange-Act-Assert with Multiple Actions**:
   Sometimes the action phase may require more than one step. You can include additional actions within the "Act" phase.

2. **Multiple Assertions**:
   In some cases, you may want to perform multiple assertions in the "Assert" phase to check different aspects of the result.

3. **Exception Testing**:
   When testing exceptions, you can modify the **Assert** phase to verify that the expected exception is thrown.

   Example:

   ```java
   // Arrange
   Calculator calculator = new Calculator();

   // Act and Assert
   assertThrows(ArithmeticException.class, () -> {
       calculator.divide(5, 0);  // Division by zero should throw ArithmeticException
   });
   ```

---

### **Conclusion**

The **Arrange-Act-Assert (AAA)** pattern is a simple yet powerful way to structure unit tests. It helps make tests more readable, maintainable, and consistent. By clearly separating the setup, execution, and verification phases of a test, this pattern makes it easier to identify the cause of test failures and ensures that each test is clear and purposeful.

---

## 90. How do you deal with dependencies that can’t be mocked?

Dealing with **dependencies that can't be mocked** can be a challenging aspect of unit testing, as mocks are typically used to isolate the system under test (SUT) and avoid testing external systems or components (e.g., databases, file systems, network calls). When you encounter dependencies that are difficult to mock, there are several strategies you can employ to ensure that your unit tests remain effective and maintainable.

Here are some approaches for handling dependencies that can’t be mocked:

---

### **1. Use Fakes or Stubs**

Sometimes, mocking isn't an option because the dependency is too complex or hard to simulate. In such cases, you can use **fakes** or **stubs**. These are simple implementations of the real dependency that simulate behavior without relying on the actual implementation.

* **Fakes**: A fake is an implementation of the dependency that provides working functionality but is usually much simpler than the real implementation. For example, a **fake database** might simulate the behavior of a real database but store data in memory instead of persisting it.

* **Stubs**: A stub is a simplified version of a dependency that returns fixed responses. It doesn't implement all of the real behavior but provides the minimum behavior required for the test.

#### **Example**: Using a fake repository

If you can't mock a **repository** for database interaction but still want to test your service, you could write a fake implementation.

```java
public class FakeRepository implements UserRepository {
    private Map<Long, User> dataStore = new HashMap<>();

    @Override
    public User findById(long id) {
        return dataStore.get(id);
    }

    @Override
    public void save(User user) {
        dataStore.put(user.getId(), user);
    }
}
```

You can use this `FakeRepository` in your tests to simulate the repository's behavior without needing to mock a real database.

---

### **2. Use In-Memory Databases for Integration Testing**

If you're dealing with a dependency like a **database**, and you can't easily mock it, you might consider using an **in-memory database** (like **H2** or **HSQLDB**) during testing. This allows you to simulate interactions with a real database but without the overhead or complexity of setting up a full database.

* **In-Memory Databases**: These databases run entirely in memory, meaning they are fast and easily disposable after each test. You can use them to simulate real database interactions in your tests while maintaining isolation.

#### **Example**: Using H2 as an in-memory database

```java
// Maven Dependency for H2 Database
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <version>1.4.200</version>
    <scope>test</scope>
</dependency>
```

In your Spring Boot test, you can configure `@DataJpaTest` to use an in-memory database:

```java
@DataJpaTest
public class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    void testUserRepository() {
        // Given
        User user = new User("John", "Doe");
        userRepository.save(user);

        // When
        User foundUser = userRepository.findById(user.getId()).orElse(null);

        // Then
        assertNotNull(foundUser);
        assertEquals("John", foundUser.getFirstName());
    }
}
```

By using an in-memory database, you can test database interaction without mocking it.

---

### **3. Use Dependency Injection for Configuring Testable Components**

In **Spring Boot** or similar frameworks, you can leverage **Dependency Injection (DI)** to control how dependencies are injected into your components. You can replace real dependencies with **test-specific implementations** that are easier to mock or substitute.

For instance, if you have a service that depends on a third-party API, you can provide a **mocked or fake implementation** of the API service in your test configuration.

#### **Example**: Using `@TestConfiguration` in Spring Boot

```java
@TestConfiguration
public class TestConfig {

    @Bean
    public ExternalApiService externalApiService() {
        return new FakeExternalApiService();
    }
}
```

In your test class:

```java
@SpringBootTest
@Import(TestConfig.class) // Import the test-specific configuration
public class SomeServiceTest {

    @Autowired
    private SomeService someService;

    @Test
    void testServiceWithFakeApi() {
        // Test code using the fake API service
    }
}
```

This allows you to replace real, difficult-to-mock dependencies with simpler ones for testing purposes.

---

### **4. Use Real External Systems in Controlled Environments (e.g., Staging or Mock Servers)**

In some cases, it might be difficult or impossible to mock certain systems (e.g., complex APIs, file systems, or network interactions). Instead of mocking these, you can use real systems but isolate them in **controlled environments**.

* **Mock Servers**: For external APIs, you can use a tool like **WireMock** or **MockServer** to simulate HTTP requests and responses, giving you control over the interaction without hitting the actual external system.

* **Test Environments**: For non-mockable systems (e.g., real external databases or third-party services), you can run tests in a **staging environment** where the actual system is available, but the scope is limited to testing the system under controlled conditions.

#### **Example**: Using WireMock to simulate an external API

```java
@ExtendWith(WireMockExtension.class)
public class ExternalApiTest {

    @Test
    void testExternalApi() {
        // Set up WireMock stub for the external API
        wireMockServer.stubFor(get(urlEqualTo("/external-api"))
                .willReturn(aResponse().withStatus(200).withBody("Mock Response")));

        // Call your service that makes the HTTP request to the external API
        String response = externalApiService.callExternalApi();

        // Assert the response
        assertEquals("Mock Response", response);
    }
}
```

---

### **5. Refactor Code to Make It Testable**

If you're encountering non-mockable dependencies in your system, it might indicate that the code is tightly coupled or difficult to test. In such cases, **refactoring** the code to make it more **testable** can be a good long-term solution.

* **Decouple Components**: Break down large, monolithic classes into smaller, more focused ones. Each class should have a single responsibility and easy-to-mock dependencies.
* **Use Interfaces**: Rely on interfaces for external dependencies so that you can easily swap out implementations for tests.

#### **Example**: Decouple a service from a database dependency

Before refactoring:

```java
public class UserService {
    private final UserRepository userRepository = new UserRepository();

    public User getUserById(int id) {
        return userRepository.findById(id);
    }
}
```

After refactoring:

```java
public class UserService {
    private final UserRepository userRepository;

    public UserService(UserRepository userRepository) {
        this.userRepository = userRepository;
    }

    public User getUserById(int id) {
        return userRepository.findById(id);
    }
}
```

Now, in tests, you can inject a mock or fake `UserRepository` to control the behavior of the `UserService`.

---

### **6. Use Integration Tests for Hard-to-Mock Dependencies**

When dealing with non-mockable dependencies, it might be more appropriate to **write integration tests** instead of unit tests. Integration tests allow you to test the interactions between multiple components in a more realistic environment.

While unit tests aim to isolate a single piece of functionality, integration tests validate how components work together, and they are useful when mocking a dependency is not feasible.

#### **Example**: Testing a service with a real database

```java
@SpringBootTest
public class UserServiceIntegrationTest {

    @Autowired
    private UserService userService;

    @Autowired
    private UserRepository userRepository;

    @Test
    void testServiceWithRealDatabase() {
        User user = new User("John", "Doe");
        userRepository.save(user);

        User foundUser = userService.getUserById(user.getId());

        assertNotNull(foundUser);
        assertEquals("John", foundUser.getFirstName());
    }
}
```

---

### **Conclusion**

When you have dependencies that cannot be mocked, you have several options to deal with them, depending on the situation:

* **Use Fakes or Stubs** for simplified versions of the dependencies.
* **In-memory databases** can simulate real database interactions.
* **Dependency Injection** allows you to replace real dependencies with test-friendly ones.
* **Mock servers** can simulate third-party services, APIs, or other external systems.
* **Refactor code** to make it easier to test and mock dependencies.
* **Integration tests** can be used to test the interactions between components with real dependencies.

By employing these strategies, you can ensure that your tests remain focused and isolated while still testing all necessary dependencies effectively.

---

## 91. What are the SOLID principles and how do they help in writing testable code?

The **SOLID** principles are a set of five design principles intended to help developers create more maintainable, flexible, and testable object-oriented software. These principles encourage a clean, modular design and can significantly improve the quality of code, making it easier to test, understand, and extend. Let's break down each principle and explain how it contributes to writing testable code:

---

### **1. Single Responsibility Principle (SRP)**

**Definition**:
A class should have only one reason to change, meaning it should only have one job or responsibility.

**How it helps with testability**:

* When a class has a single responsibility, it becomes easier to **mock** or **stub** its behavior in tests.
* Smaller, focused classes are easier to **test** because their behavior is well-defined and they have fewer interactions with other parts of the system.
* It avoids **complex interdependencies** and simplifies writing unit tests for each class.

#### **Example**:

```java
// Bad Example: A class that handles both database operations and business logic
public class OrderProcessor {
    public void processOrder(Order order) {
        // Business logic
        saveToDatabase(order);
    }

    private void saveToDatabase(Order order) {
        // DB saving logic
    }
}

// Better: Split responsibilities into two classes
public class OrderProcessor {
    private final OrderRepository orderRepository;

    public OrderProcessor(OrderRepository orderRepository) {
        this.orderRepository = orderRepository;
    }

    public void processOrder(Order order) {
        // Business logic
    }
}

public class OrderRepository {
    public void saveToDatabase(Order order) {
        // DB saving logic
    }
}
```

By splitting the classes, you can test `OrderProcessor` and `OrderRepository` independently, focusing on their specific responsibilities.

---

### **2. Open/Closed Principle (OCP)**

**Definition**:
Software entities (classes, modules, functions, etc.) should be **open for extension**, but **closed for modification**. This means you can extend the behavior of a class without modifying its existing code.

**How it helps with testability**:

* The **extension** of behavior without modifying existing code reduces the risk of breaking existing functionality, making it safer to refactor and extend code without introducing regressions.
* With this principle, you can create **mockable interfaces** that can be easily swapped for different implementations, which is critical for unit testing.
* Test cases can remain stable even as the system evolves because extensions don’t interfere with existing logic.

#### **Example**:

```java
// Open/Closed Example
public abstract class DiscountStrategy {
    public abstract double calculateDiscount(Order order);
}

public class SeasonalDiscount extends DiscountStrategy {
    @Override
    public double calculateDiscount(Order order) {
        // Seasonal discount logic
        return 0.10; // 10% discount
    }
}

public class Order {
    private DiscountStrategy discountStrategy;

    public Order(DiscountStrategy discountStrategy) {
        this.discountStrategy = discountStrategy;
    }

    public double getDiscountedPrice(double price) {
        return price - discountStrategy.calculateDiscount(this);
    }
}
```

You can extend the behavior by adding new `DiscountStrategy` implementations, like `HolidayDiscount`, without modifying the existing `Order` class. This makes the code **extensible** and **testable**.

---

### **3. Liskov Substitution Principle (LSP)**

**Definition**:
Objects of a superclass should be replaceable with objects of its subclasses without affecting the correctness of the program. In other words, derived classes must be substitutable for their base classes.

**How it helps with testability**:

* If subclasses can be used interchangeably with their base class, your tests can **use mock objects** or **substitutes** for the actual classes. This ensures that tests remain valid even when the implementation changes or new subclasses are introduced.
* It also ensures that the behavior of subclasses **does not break existing tests** for base class functionality.

#### **Example**:

```java
// Liskov Substitution Example
public class Rectangle {
    protected int width;
    protected int height;

    public void setWidth(int width) {
        this.width = width;
    }

    public void setHeight(int height) {
        this.height = height;
    }

    public int calculateArea() {
        return width * height;
    }
}

public class Square extends Rectangle {
    @Override
    public void setWidth(int width) {
        this.width = this.height = width;
    }

    @Override
    public void setHeight(int height) {
        this.height = this.width = height;
    }
}
```

Here, `Square` can be used wherever `Rectangle` is used, and the **behavior remains correct**, making it easier to test subclasses without breaking tests for the base class.

---

### **4. Interface Segregation Principle (ISP)**

**Definition**:
Clients should not be forced to depend on interfaces they do not use. It’s better to have multiple **small, specific interfaces** than one **large, general-purpose interface**.

**How it helps with testability**:

* Smaller, focused interfaces make it easier to mock only the methods you need for a specific test scenario.
* By **decoupling** classes through fine-grained interfaces, you can test **individual behaviors** independently, reducing the complexity of test setup.

#### **Example**:

```java
// Bad Example: A large interface
public interface Printer {
    void print();
    void scan();
    void fax();
}

// Better Example: Split into smaller interfaces
public interface Print {
    void print();
}

public interface Scan {
    void scan();
}

public interface Fax {
    void fax();
}
```

With the smaller interfaces, you can **mock only the relevant behavior** for the test at hand, without dealing with unnecessary methods.

---

### **5. Dependency Inversion Principle (DIP)**

**Definition**:
High-level modules should not depend on low-level modules. Both should depend on abstractions (e.g., interfaces). Furthermore, abstractions should not depend on details; details should depend on abstractions.

**How it helps with testability**:

* By depending on **abstractions (interfaces)** rather than concrete implementations, you can easily **mock or stub dependencies** in your unit tests.
* It encourages **loose coupling**, making it easier to isolate the system under test and test it independently from external dependencies.
* Testing becomes easier because the dependencies of a class can be swapped with **mocked or fake implementations**.

#### **Example**:

```java
// Bad Example: Directly depending on a concrete implementation
public class OrderService {
    private PaymentProcessor paymentProcessor = new PaymentProcessor();

    public void processOrder(Order order) {
        paymentProcessor.processPayment(order);
    }
}

// Better Example: Using dependency injection with an interface
public interface PaymentProcessor {
    void processPayment(Order order);
}

public class OrderService {
    private final PaymentProcessor paymentProcessor;

    public OrderService(PaymentProcessor paymentProcessor) {
        this.paymentProcessor = paymentProcessor;
    }

    public void processOrder(Order order) {
        paymentProcessor.processPayment(order);
    }
}
```

By depending on the `PaymentProcessor` interface, the `OrderService` class is easier to **test**, because you can inject a **mock** `PaymentProcessor` during tests.

---

### **How SOLID Principles Help in Writing Testable Code:**

* **Modularization**: By following SOLID principles, you design your system in smaller, independent pieces that are easier to test individually.
* **Loose Coupling**: Dependencies are abstracted through interfaces, making it easier to mock or inject test doubles (mocks, stubs, fakes) for unit testing.
* **Predictable Behavior**: Code adheres to principles like LSP and OCP, which means that new features or changes don’t break existing tests, making your tests more reliable.
* **Isolating Responsibilities**: SRP ensures that each class has one responsibility, making it easier to focus on testing that responsibility without worrying about side effects from other concerns.

By adhering to SOLID principles, you promote **testability** by making code **modular**, **flexible**, and **decoupled**, which ultimately leads to more maintainable and reliable tests.

---

## 92. What’s the role of dependency injection in unit testing?

### The Role of **Dependency Injection (DI)** in Unit Testing

**Dependency Injection (DI)** is a design pattern that allows a class’s dependencies (e.g., other objects or services) to be **injected** from the outside rather than being created inside the class itself. In unit testing, DI plays a crucial role in making the code **more testable**, **flexible**, and **decoupled**, which in turn helps to isolate components for easier and more effective testing.

### Key Benefits of DI in Unit Testing:

1. **Easier to Mock Dependencies:**

    * One of the core advantages of DI is that it allows you to **inject mock objects** into the class being tested. Instead of the class having to create its own dependencies (which may involve complex logic, database calls, or network interactions), you can provide simple mock versions of these dependencies for testing.
    * This means that **unit tests focus on the behavior of the class itself** without having to worry about external systems or complicated setup.

   #### **Example**:

   ```java
   public class UserService {
       private final UserRepository userRepository;

       public UserService(UserRepository userRepository) {
           this.userRepository = userRepository;
       }

       public User getUser(int id) {
           return userRepository.findById(id);
       }
   }
   ```

   In the test case, you can inject a mock `UserRepository`:

   ```java
   @Test
   void testGetUser() {
       UserRepository mockRepo = mock(UserRepository.class);
       UserService userService = new UserService(mockRepo);

       User mockUser = new User(1, "John Doe");
       when(mockRepo.findById(1)).thenReturn(mockUser);

       assertEquals(mockUser, userService.getUser(1));
   }
   ```

   In this case, `UserService` can be tested independently of `UserRepository`, thanks to DI.

---

2. **Decoupling of Components:**

    * DI encourages **loose coupling** between classes. This decoupling makes unit testing easier because classes don't have tightly bound dependencies that must be tested together. Each class can be tested in isolation, using mock or stub versions of its dependencies.
    * By separating concerns, you can focus tests on specific behaviors without worrying about interacting components.

   #### **Example**:

   If `UserService` depends on `UserRepository` and another service `EmailService`, DI allows you to inject **mock** or **stub** versions of both services into `UserService` for testing:

   ```java
   public class UserService {
       private final UserRepository userRepository;
       private final EmailService emailService;

       public UserService(UserRepository userRepository, EmailService emailService) {
           this.userRepository = userRepository;
           this.emailService = emailService;
       }

       public void createUser(User user) {
           userRepository.save(user);
           emailService.sendWelcomeEmail(user);
       }
   }
   ```

   When testing `createUser()`, you can inject mocked `UserRepository` and `EmailService` to isolate the test.

---

3. **Improved Flexibility in Test Setup:**

    * With DI, it’s easy to substitute real dependencies with **mocked or fake objects** for testing purposes. This allows you to simulate various test scenarios without relying on external resources or services, such as databases or APIs.
    * This means that your unit tests can run quickly and consistently in isolation, without being affected by external state or network conditions.

---

4. **Simplifies Test Initialization:**

    * DI helps make test setup simpler by allowing you to **inject pre-configured test doubles** (mocks, stubs, or fakes) into the class being tested. In frameworks like Spring, DI is handled automatically by the container, and you can define the behavior of the test dependencies explicitly using annotations like `@MockBean` or `@Autowired` in test configurations.
    * You can easily configure different types of dependencies for different test cases or environments.

   #### **Example** (Using Spring with DI for Unit Testing):

   ```java
   @SpringBootTest
   public class UserServiceTest {

       @MockBean
       private UserRepository userRepository;

       @Autowired
       private UserService userService;

       @Test
       void testGetUser() {
           User mockUser = new User(1, "John Doe");
           when(userRepository.findById(1)).thenReturn(mockUser);

           User result = userService.getUser(1);
           assertEquals("John Doe", result.getName());
       }
   }
   ```

   Here, `@MockBean` is used to inject a mock `UserRepository`, while `@Autowired` is used to inject the actual `UserService`.

---

5. **Supports Different Testing Approaches:**

    * DI allows you to easily test the same class in different contexts by changing the injected dependencies. This flexibility supports **mocking**, **integration testing**, and even **end-to-end testing**.
    * It also helps ensure **separation of concerns**, making it easier to follow testing strategies like **Test-Driven Development (TDD)** or **Behavior-Driven Development (BDD)**.

---

### How Dependency Injection Helps Unit Testing in Practice:

* **Test Isolation**: DI makes it easy to isolate the class under test by injecting mock dependencies. You can focus on testing just the class’s behavior without worrying about the complexity of its collaborators.
* **Easier to Simulate Edge Cases**: By injecting mocked dependencies, you can simulate various scenarios (e.g., empty responses, exceptions, timeouts) that would be difficult or slow to simulate with real dependencies.
* **Decouples Code from External Systems**: With DI, external systems (such as databases, file systems, web services) can be replaced with mock versions, making tests run faster and more reliably.
* **Consistency**: DI helps ensure that the dependencies are consistently initialized across all tests, reducing test setup errors and making tests easier to maintain.

---

### In Summary:

**Dependency Injection** is essential for writing unit tests because it makes your code more modular, testable, and decoupled. It allows you to **inject mock dependencies**, **easily substitute real components with test doubles**, and **isolate the class under test**, making it easier to write focused, reliable, and maintainable unit tests.

---

## 93. How do you ensure your tests are repeatable?

Ensuring that your tests are **repeatable** is crucial for maintaining the reliability and consistency of your software. A repeatable test means that it produces the same result each time it is run, under the same conditions, regardless of external factors. Achieving repeatability in tests ensures that they are meaningful and trustworthy.

Here are some strategies to ensure your tests are repeatable:

### 1. **Isolate Tests (Test Isolation)**

* **Principle**: Each unit test should test a specific unit of code in isolation, without relying on the state of other tests or external systems.
* **Why it matters**: If tests are dependent on each other, one failing test can cause a cascading effect, leading to other tests failing even if they are logically correct. This breaks the repeatability of tests.
* **How to achieve it**:

    * **Use mocks** or **stubs** for external dependencies (e.g., databases, APIs, file systems) to ensure that tests don’t depend on real-world conditions.
    * **Avoid global state** and static variables that could affect other tests.
    * Use **dependency injection (DI)** to easily substitute dependencies for tests.

#### Example:

```java
// Bad: This test might fail if it depends on the state of the database
public void testGetUser() {
    User user = userService.getUser(1); // It depends on the database having this user
    assertNotNull(user);
}

// Good: Mock the database dependency
@Test
public void testGetUser() {
    User mockUser = new User(1, "John Doe");
    when(userRepository.findById(1)).thenReturn(mockUser);
    User user = userService.getUser(1);
    assertEquals("John Doe", user.getName());
}
```

### 2. **Control External Dependencies (Use Mocks, Stubs, or Fakes)**

* **Principle**: External dependencies, such as databases, third-party services, or external APIs, should be mocked, stubbed, or replaced with fake implementations in unit tests.
* **Why it matters**: Real external systems may change over time, become unavailable, or have slow response times, which can make your tests unreliable and non-repeatable.
* **How to achieve it**:

    * **Mock** database calls, HTTP requests, or other external systems using libraries like **Mockito** or **WireMock**.
    * Use **in-memory databases** or **embedded databases** (e.g., H2) to simulate database interactions in a controlled environment.

#### Example:

```java
@MockBean
private UserRepository userRepository;

@Test
public void testGetUser() {
    User mockUser = new User(1, "John Doe");
    when(userRepository.findById(1)).thenReturn(Optional.of(mockUser));
    User result = userService.getUser(1);
    assertEquals("John Doe", result.getName());
}
```

### 3. **Avoid Test Dependencies on External State**

* **Principle**: Tests should not depend on external state (like the current time, random values, or files that can change between runs).
* **Why it matters**: External factors can make tests produce different results depending on the environment, making them non-repeatable.
* **How to achieve it**:

    * **Mock time-related functions** using tools like **Mockito’s `mockStatic()`** or libraries like **Time4J**.
    * **Use deterministic values** (e.g., fixed values, predefined inputs) for things like random number generation or time.
    * **Reset state** between tests to ensure tests start with the same initial conditions.

#### Example:

```java
// Bad: Test is affected by the current time
@Test
public void testExpiryDate() {
    Date currentDate = new Date();
    assertTrue(orderService.isExpired(currentDate));
}

// Good: Mock the time to make the test repeatable
@Test
public void testExpiryDate() {
    LocalDate fixedDate = LocalDate.of(2021, 1, 1);
    OrderService mockOrderService = mock(OrderService.class);
    when(mockOrderService.getCurrentDate()).thenReturn(fixedDate);
    assertFalse(mockOrderService.isExpired(fixedDate));
}
```

### 4. **Ensure Idempotency (Same Inputs, Same Outputs)**

* **Principle**: Tests should be idempotent, meaning they should produce the same results when run multiple times with the same inputs.
* **Why it matters**: Non-idempotent tests, which are dependent on mutable states or side effects, can cause inconsistent results if run multiple times, leading to flaky tests.
* **How to achieve it**:

    * **Clear or reset the state** before or after each test run (using `@BeforeEach` and `@AfterEach` in JUnit).
    * Ensure tests don’t modify global or shared state that can affect other tests.

#### Example:

```java
@BeforeEach
public void setUp() {
    // Reset shared state before each test
    someService.resetState();
}
```

### 5. **Make Tests Independent of Environment (Environment Variables, Configuration Files, etc.)**

* **Principle**: Tests should not be dependent on the environment in which they are running (e.g., specific system properties, external APIs, or environment variables).
* **Why it matters**: Differences between environments (e.g., local, staging, CI servers) can lead to different test results.
* **How to achieve it**:

    * Use **mocked configurations** or environment variables during tests.
    * Use test profiles or **in-memory configurations** to avoid reliance on external systems.
    * Make sure to reset environment-dependent properties or configurations after each test run.

#### Example:

```java
@TestConfiguration
public class TestConfig {
    @Bean
    public SomeService someService() {
        return new SomeService("test config value");
    }
}
```

### 6. **Avoid Hard Dependencies on External Services**

* **Principle**: Don’t rely on external services (such as a live database, a web service, etc.) during unit tests.
* **Why it matters**: Network latency, downtime, and unpredictable behavior of external services can make tests fail randomly, thus preventing repeatability.
* **How to achieve it**:

    * **Use mocks, stubs, or fakes** for services that involve I/O operations (e.g., database, HTTP calls).
    * Use **integration tests** for testing interactions with external systems instead of including them in unit tests.

#### Example:

```java
@MockBean
private PaymentGateway paymentGateway;

@Test
public void testPaymentProcessing() {
    when(paymentGateway.process(any())).thenReturn(true);
    assertTrue(paymentService.processPayment(paymentDetails));
}
```

### 7. **Test in Isolated, Clean Environments (Containerized Environments)**

* **Principle**: For integration tests or tests involving multiple services, ensure that the test environment is isolated and repeatable.
* **Why it matters**: Tests may depend on the state of a shared database or system, which can lead to issues when tests run in different environments or with different versions of dependencies.
* **How to achieve it**:

    * Use **Docker** to create isolated test environments for integration or system tests (e.g., databases, message brokers).
    * Use tools like **Testcontainers** to manage containerized services during test execution.

---

### 8. **Automate Test Cleanup (Setup and Teardown)**

* **Principle**: Ensure that tests clean up any resources (e.g., database connections, temporary files) after they run.
* **Why it matters**: If tests leave behind files or database entries, they can interfere with other tests, making results unpredictable.
* **How to achieve it**:

    * Use `@BeforeEach` and `@AfterEach` annotations to manage setup and teardown.
    * Ensure that each test is self-contained and doesn’t leave side effects.

#### Example:

```java
@BeforeEach
void setUp() {
    // Set up any initial states
}

@AfterEach
void tearDown() {
    // Clean up after test
}
```

---

### Summary of Best Practices:

* **Isolate tests**: Mock or stub external dependencies.
* **Control external systems**: Avoid real API calls, databases, etc., during unit tests.
* **Reset state**: Ensure tests don't depend on global state or the outcome of previous tests.
* **Mock environment-specific values**: Use mock configurations or profiles.
* **Automate cleanup**: Properly set up and tear down any test resources.

By following these practices, your tests will be **repeatable**, ensuring that they produce consistent results every time they are executed, which is key for reliable software quality and effective continuous integration.

---

## 94. How do you test code that accesses files or databases?

Testing code that accesses files or databases requires careful consideration to ensure that your tests remain **isolated**, **fast**, and **repeatable**. Direct access to files or databases can introduce external dependencies that may affect test reliability. Below are several strategies and techniques for testing code that interacts with files or databases.

### 1. **Mocking or Stubbing File and Database Access**

* **Principle**: Mock or stub out interactions with external resources like files and databases. This isolates the code under test from external systems, making the tests faster and more predictable.
* **Why it matters**: Real file I/O and database operations can be slow, dependent on external state, and can introduce unpredictability into your tests.
* **How to achieve it**:

    * **Mocking File System**: Use libraries like **Mockito** or **EasyMock** to mock file operations such as reading or writing files.
    * **Mocking Database**: Use **Mockito**, **H2** (in-memory database), or **Testcontainers** to simulate database interactions.

#### Example: Mocking File Access

```java
import java.io.File;
import java.io.IOException;
import org.junit.jupiter.api.Test;
import static org.mockito.Mockito.*;

public class FileServiceTest {

    @Test
    void testReadFile() throws IOException {
        // Mocking the File object
        File mockFile = mock(File.class);
        when(mockFile.exists()).thenReturn(true);
        when(mockFile.canRead()).thenReturn(true);

        FileService fileService = new FileService();
        String content = fileService.readFile(mockFile);
        // Asserts that the content was correctly read (e.g., mock behavior)
        assertEquals("Mocked file content", content);
    }
}
```

#### Example: Mocking Database Access

```java
import org.junit.jupiter.api.Test;
import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

public class UserServiceTest {

    @Test
    void testGetUser() {
        // Mocking the database repository
        UserRepository mockRepo = mock(UserRepository.class);
        User mockUser = new User(1, "John Doe");
        when(mockRepo.findById(1)).thenReturn(Optional.of(mockUser));

        UserService userService = new UserService(mockRepo);
        User user = userService.getUser(1);

        assertEquals("John Doe", user.getName());
    }
}
```

### 2. **Use In-Memory Databases (for Database Access)**

* **Principle**: Use in-memory databases such as **H2**, **HSQLDB**, or **Derby** to simulate real database interactions. These databases can run entirely in memory, which means no actual disk I/O, and they provide a clean slate for each test.
* **Why it matters**: In-memory databases allow you to simulate a real database environment without the overhead of setting up or interacting with an actual database server. They are also fast, and you can ensure that each test starts with a fresh, clean state.
* **How to achieve it**:

    * Configure a test profile or use test-specific configurations to point to an in-memory database.
    * Use the **Spring TestContext Framework** for managing the lifecycle of the in-memory database during tests.

#### Example: Using H2 for Testing in Spring Boot

```yaml
# application-test.yml
spring:
  datasource:
    url: jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1
    driverClassName: org.h2.Driver
    username: sa
    password:
    dialect: org.hibernate.dialect.H2Dialect
  h2:
    console:
      enabled: true
```

```java
@SpringBootTest
@AutoConfigureTestDatabase(replace = AutoConfigureTestDatabase.Replace.NONE) // Use the real datasource
public class UserRepositoryTest {

    @Autowired
    private UserRepository userRepository;

    @Test
    public void testCreateUser() {
        User user = new User("John", "Doe");
        userRepository.save(user);
        Optional<User> foundUser = userRepository.findById(user.getId());
        assertTrue(foundUser.isPresent());
    }
}
```

### 3. **Use of Test Containers (for Complex Database or External Systems)**

* **Principle**: Use **Testcontainers** to spin up lightweight Docker containers for testing databases or other external services like message queues or APIs.
* **Why it matters**: Testcontainers allow you to spin up actual database instances in Docker containers during tests. This is useful when you need the full behavior of a specific database but don’t want to rely on a local or remote database during tests.
* **How to achieve it**:

    * Set up **Testcontainers** to start a containerized instance of a database or file system.
    * Ensure that containers are cleaned up after each test to avoid lingering resources.

#### Example: Using Testcontainers with PostgreSQL

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.RegisterExtension;
import org.testcontainers.containers.PostgreSQLContainer;

public class UserServiceTest {

    @RegisterExtension
    static PostgreSQLContainer<?> postgresContainer = new PostgreSQLContainer<>("postgres:latest")
            .withDatabaseName("testdb")
            .withUsername("sa")
            .withPassword("password");

    @Test
    void testDatabaseAccess() {
        String jdbcUrl = postgresContainer.getJdbcUrl();
        System.out.println("JDBC URL: " + jdbcUrl);
        // Run your database test code here using jdbcUrl
    }
}
```

### 4. **Using File System Virtualization for File Access**

* **Principle**: Virtualize the file system using tools like **Jimfs** or **Temporary Files** in JUnit, where files can be created in memory (virtual file system) rather than on disk.
* **Why it matters**: Working with real files can slow down tests and make them dependent on the file system, which can cause issues with permissions or state changes between tests. Virtualizing the file system avoids these issues.
* **How to achieve it**:

    * Use **Jimfs** (a Java in-memory file system) or **java.nio.file.Files** to create temporary files and directories in memory.

#### Example: Using Jimfs for File Testing

```java
import com.google.common.jimfs.Jimfs;
import org.junit.jupiter.api.Test;
import java.nio.file.FileSystem;
import java.nio.file.Files;
import java.nio.file.Path;

public class FileServiceTest {

    @Test
    public void testWriteFile() throws Exception {
        FileSystem fs = Jimfs.newFileSystem();
        Path path = fs.getPath("test.txt");
        Files.write(path, "Hello, Jimfs!".getBytes());

        String content = new String(Files.readAllBytes(path));
        assertEquals("Hello, Jimfs!", content);
    }
}
```

### 5. **File and Database Cleanup (Test Cleanup)**

* **Principle**: Always clean up test data after each test run to ensure the environment is reset.
* **Why it matters**: Test data left behind from a previous test can affect the results of subsequent tests, leading to **non-repeatable tests**.
* **How to achieve it**:

    * Use `@BeforeEach` and `@AfterEach` (JUnit) to set up and tear down the test environment.
    * Manually delete or reset any test data used in the test.

#### Example: File Cleanup After Test

```java
import org.junit.jupiter.api.AfterEach;
import org.junit.jupiter.api.Test;
import java.nio.file.*;

public class FileServiceTest {

    private Path tempFile;

    @Test
    public void testWriteFile() throws Exception {
        tempFile = Files.createTempFile("test", ".txt");
        Files.write(tempFile, "Test data".getBytes());
        assertTrue(Files.exists(tempFile));
    }

    @AfterEach
    public void cleanup() throws Exception {
        Files.deleteIfExists(tempFile);
    }
}
```

---

### Summary of Key Techniques:

1. **Mocking and Stubbing**: Use mocking libraries like **Mockito** to mock file and database access.
2. **In-memory Databases**: Use in-memory databases like **H2** or **HSQLDB** for fast, isolated database tests.
3. **Test Containers**: Use **Testcontainers** to spin up real database containers for integration tests.
4. **File System Virtualization**: Use tools like **Jimfs** to mock file systems in memory.
5. **Cleanup**: Always clean up files and database states after each test to avoid shared state between tests.

By employing these techniques, you can test code that accesses files and databases without relying on external systems, ensuring faster, repeatable, and isolated unit tests.

---

## 95. What is Continuous Testing and how does it work in CI/CD?

### What is Continuous Testing?

**Continuous Testing** is the practice of executing automated tests as part of the software delivery pipeline to obtain immediate feedback on the business risks associated with a software release. It ensures that software changes are validated continuously, enabling fast and reliable delivery of applications.

It plays a **critical role in DevOps and CI/CD (Continuous Integration/Continuous Delivery)** pipelines by detecting bugs early and improving software quality.

---

### Goals of Continuous Testing

* Detect issues early and often.
* Reduce the feedback loop for developers.
* Prevent broken code from being released to production.
* Enable faster and safer releases.

---

### How Continuous Testing Works in CI/CD

Here’s how continuous testing fits into a **CI/CD pipeline**:

#### 1. **Code Commit (Continuous Integration)**

* Developer writes code and commits to a shared version control system (e.g., Git).
* This triggers an automated **build process** on a CI server (e.g., Jenkins, GitHub Actions, GitLab CI, CircleCI).

#### 2. **Automated Build**

* The CI tool compiles the code.
* Dependency management tools (like Maven or Gradle) pull in necessary libraries.

#### 3. **Execute Automated Tests**

Tests are run in multiple layers:

* **Unit Tests** (e.g., JUnit, TestNG) — verify individual units/components.
* **Integration Tests** — verify integration between components.
* **Functional Tests** — test full user flows (e.g., using Selenium, RestAssured).
* **Static Code Analysis** — check code quality (e.g., SonarQube).
* **Code Coverage** — tools like JaCoCo report how much code is tested.

#### 4. **Test Results and Feedback**

* If tests fail, the CI/CD pipeline stops and developers are notified.
* If all tests pass, the build moves to the next stage (e.g., staging deployment or approval gate).

#### 5. **Post-Build Testing (Continuous Delivery/Deployment)**

* In **CD**, further tests may be triggered in staging/QA environments:

    * End-to-End Tests
    * Performance/Load Testing
    * Security Testing (e.g., OWASP scans)

#### 6. **Production Deployment (Optional for CD)**

* If all tests succeed and approvals are in place, the software is deployed automatically to production.

---

### Example: Continuous Testing Workflow in Jenkins

1. Developer pushes code to GitHub.
2. Jenkins detects the change and:

    * Runs unit tests (`JUnit`, `Mockito`)
    * Runs integration tests (`Spring Boot Test`, `Testcontainers`)
    * Runs UI tests (`Selenium`)
3. Jenkins reports results:

    * Fails the build if any test fails.
    * Sends feedback to developers.
4. If all pass, it triggers the next stage (e.g., deploy to test or production environment).

---

### Tools Commonly Used in Continuous Testing

| Layer           | Tools/Frameworks                   |
| --------------- | ---------------------------------- |
| Unit Testing    | JUnit, TestNG, Mockito             |
| Integration     | Spring Boot Test, Testcontainers   |
| UI Testing      | Selenium, Cypress, Playwright      |
| API Testing     | RestAssured, Postman, Karate       |
| Performance     | JMeter, Gatling                    |
| Security        | OWASP ZAP, SonarQube               |
| CI/CD Pipelines | Jenkins, GitLab CI, GitHub Actions |
| Code Quality    | JaCoCo, SonarQube, PMD, Checkstyle |

---

### Benefits of Continuous Testing

* **Faster feedback** to developers.
* **Higher quality** releases.
* **Early detection** of defects.
* **Improved developer confidence** in releases.
* **Reduced cost** of fixing bugs (since they’re caught early).

---

### Summary

Continuous Testing is a key practice in modern software development that integrates automated testing into every stage of the CI/CD pipeline. It helps ensure that software is always in a releasable state and accelerates delivery without sacrificing quality.

---

## 96. How do you test scheduled or cron jobs?

### ✅ How Do You Test Scheduled or Cron Jobs?

In Spring Boot or any Java-based application, **scheduled tasks** (or **cron jobs**) are automated jobs that run at fixed intervals using annotations like `@Scheduled`.

Testing these jobs involves verifying that:

* The job logic executes as expected.
* The job is triggered at the right intervals (only in integration tests).
* It behaves correctly under success/failure scenarios.

---

### 🧪 1. **Unit Testing Scheduled Methods**

You **shouldn't test the scheduler trigger itself** in unit tests. Instead, you isolate and test the business logic **inside** the method.

#### ✅ Example:

```java
@Component
public class ReportScheduler {

    @Autowired
    private ReportService reportService;

    @Scheduled(cron = "0 0 * * * *") // Runs every hour
    public void generateReport() {
        reportService.generateDailyReport();
    }
}
```

#### ✅ Unit Test:

```java
@ExtendWith(MockitoExtension.class)
class ReportSchedulerTest {

    @InjectMocks
    private ReportScheduler reportScheduler;

    @Mock
    private ReportService reportService;

    @Test
    void testGenerateReport_callsServiceMethod() {
        reportScheduler.generateReport();
        verify(reportService).generateDailyReport();
    }
}
```

👉 Here, you're testing the **business logic**, not the scheduling mechanism.

---

### 🧪 2. **Integration Testing with Real Scheduling (Optional)**

This is useful if you want to **test actual scheduling behavior**. For this, you can reduce the cron interval for testing purposes and use `@SpringBootTest`.

```java
@SpringBootTest
@TestPropertySource(properties = {
  "spring.main.allow-bean-definition-overriding=true",
  "scheduling.test=true"
})
class SchedulerIntegrationTest {

    @SpyBean
    private ReportScheduler reportScheduler;

    @Test
    void testSchedulerRuns() throws InterruptedException {
        // Wait enough time for @Scheduled method to trigger
        Thread.sleep(3000); // Dangerous in real unit tests!

        verify(reportScheduler, atLeastOnce()).generateReport();
    }
}
```

> ⚠️ **Caution**: Using `Thread.sleep()` is not recommended in most tests—it can make them flaky and slow.

---

### ✅ 3. **Use of `TaskScheduler` for Manual Triggering (Alternative Approach)**

To test the behavior of the scheduled task in isolation, you can make your scheduler method **public** and call it directly (as in the first example), or **inject a scheduler** and trigger tasks manually in a test.

---

### 🔄 Best Practices

* **Don't test time intervals in unit tests.** Just test the logic.
* **Extract logic** out of scheduled methods into services.
* **Use mocks** to verify interactions.
* **Avoid `Thread.sleep()`** unless absolutely necessary.
* Use `@SpyBean` for verifying scheduled method calls in integration tests.
* Keep the `@Scheduled` annotation only in production-like environments, not in unit testing.

---

### Summary

| Level       | Goal                             | Strategy                                       |
| ----------- | -------------------------------- | ---------------------------------------------- |
| Unit Test   | Verify logic in scheduled method | Call method directly and mock dependencies     |
| Integration | Verify job actually runs         | Use `@SpyBean`, reduce cron time, observe call |
| Production  | Ensure correctness over time     | Monitor via logs, metrics, or observability    |

---

## 97. What is the role of `@Disabled` and when to use it?

### ✅ What is the Role of `@Disabled` in JUnit 5?

`@Disabled` is a **JUnit 5 annotation** used to **skip or ignore a test method or class** during test execution.

---

### 📌 Syntax

```java
@Disabled
@Test
void skippedTest() {
    // This test will not run
}
```

Or with a reason:

```java
@Disabled("Feature not implemented yet")
@Test
void skippedTest() {
    // Skipped with explanation
}
```

---

### 🛠️ When to Use `@Disabled`

| Use Case                             | Description                                                                             |
| ------------------------------------ | --------------------------------------------------------------------------------------- |
| 🔧 **Temporarily Broken Test**       | When a test fails due to a known issue, and you're working on a fix.                    |
| 🧪 **Not Yet Implemented**           | When you're doing **Test-Driven Development (TDD)** and the functionality is pending.   |
| 🚫 **Environment-Specific Behavior** | When a test only works in certain environments (e.g., Linux-only).                      |
| 🔄 **Flaky Tests**                   | When you’re debugging an intermittent failure and need to temporarily exclude the test. |
| 📁 **Disable All Tests in a Class**  | You can disable the whole test class if needed.                                         |

#### Example:

```java
@Disabled("Pending bug fix for null pointer case")
class MyTestClass {

    @Test
    void testSomething() {
        // Will be ignored
    }
}
```

---

### 🧪 Difference from `@Ignore` (JUnit 4)

| JUnit 4                     | JUnit 5                                     |
| --------------------------- | ------------------------------------------- |
| `@Ignore`                   | `@Disabled`                                 |
| Requires `org.junit.Ignore` | Comes from `org.junit.jupiter.api.Disabled` |

---

### 🚨 Best Practices

* Don't leave tests permanently disabled without tracking.
* Add a clear **reason** for disabling using the optional message.
* Prefer to **fix or refactor** failing tests instead of disabling them indefinitely.
* Use **conditional execution** (`@EnabledIf`, `@EnabledOnOs`, etc.) for platform-specific cases instead.

---

### ✅ Summary

* `@Disabled` helps you skip tests temporarily.
* Useful during active development, debugging, or when handling flaky tests.
* Always provide a reason for better traceability.

---

## 98. What is the risk of over-mocking?

### ⚠️ What Is the Risk of Over-Mocking in Unit Testing?

**Over-mocking** refers to the excessive use of mocks in unit tests—mocking everything, including simple or stable components that don't really need to be mocked.

While mocking is powerful for isolating units of code, **over-mocking can be harmful** and reduce the value of your tests.

---

### 🚨 Risks of Over-Mocking

| Problem                                    | Explanation                                                                                               |
| ------------------------------------------ | --------------------------------------------------------------------------------------------------------- |
| ❌ **False Sense of Security**              | Tests pass because mocks behave exactly as defined, not because the real code works.                      |
| 🔁 **Tight Coupling to Implementation**    | Tests rely on method calls and interactions, not behavior, making them fragile to refactoring.            |
| 🧪 **Reduced Test Coverage of Real Logic** | If everything is mocked, nothing real is tested—so no actual behavior is validated.                       |
| 🔍 **Missed Integration Errors**           | You won’t catch issues that arise when real objects interact, especially between layers.                  |
| 💥 **More Complex Tests**                  | Setting up mocks for everything increases boilerplate and reduces clarity.                                |
| 🔄 **Duplicated Logic in Test**            | Over-mocking can cause tests to replicate the logic of the code itself, defeating the purpose of testing. |

---

### 🔧 Example of Over-Mocking

Bad test with over-mocking:

```java
@Test
void testServiceWithMocksEverywhere() {
    User user = mock(User.class);
    when(user.getId()).thenReturn(1);

    UserRepository userRepository = mock(UserRepository.class);
    when(userRepository.findById(1)).thenReturn(Optional.of(user));

    UserService service = new UserService(userRepository);
    User result = service.getUserById(1);

    assertEquals(user, result);
}
```

➡️ This test **only tests mocks** and not the actual logic inside `UserService`.

---

### ✅ Better Approach

Use real objects where possible, and **mock only what you need to isolate**.

```java
@Mock
private UserRepository userRepository;

@InjectMocks
private UserService userService;

@Test
void testGetUserById() {
    User user = new User(1, "Alice");
    when(userRepository.findById(1)).thenReturn(Optional.of(user));

    User result = userService.getUserById(1);

    assertEquals("Alice", result.getName());
}
```

---

### 🧠 Best Practices to Avoid Over-Mocking

* ✅ Mock **external dependencies** (databases, APIs), not your own logic.
* ✅ Prefer **real objects** for value types and simple DTOs.
* ✅ Keep **unit tests focused**, but use **integration tests** to verify real interaction.
* ✅ Don't mock things like `List`, `Map`, or POJOs—use them as-is.
* ✅ Test **behavior**, not implementation (i.e., prefer verifying results over method calls).

---

### ✅ Summary

Over-mocking leads to brittle, misleading, and unhelpful tests. Mock what’s necessary—usually external dependencies—and keep your test logic meaningful and maintainable.

---

## 99. What is a test pyramid and how should you structure your tests?

### ✅ What Is a Test Pyramid and How Should You Structure Your Tests?

The **Test Pyramid** is a concept introduced by Mike Cohn to guide how software tests should be **organized and layered** for maximum effectiveness, efficiency, and maintainability.

---

### 🧱 Test Pyramid: The Layers

```
         UI Tests (Selenium, Cypress, etc.)
              ↑
         Integration Tests (SpringBootTest, @DataJpaTest)
              ↑
         Unit Tests (JUnit, Mockito)
```

---

### 🔍 1. **Unit Tests** (Base of the Pyramid)

* **Fast**, **reliable**, and **cheap** to write and run.
* Test a single class or method in isolation.
* Use **mocks** or **stubs** for dependencies.

**Tools:** JUnit, TestNG, Mockito, AssertJ

✅ **Goal:** Test logic and small components thoroughly.

```java
@Test
void shouldReturnDiscountPrice() {
    double result = calculator.applyDiscount(100, 0.2);
    assertEquals(80.0, result);
}
```

---

### 🔗 2. **Integration Tests** (Middle Layer)

* Test how **multiple components work together** (e.g., service and repository).
* Uses **real Spring context**, DBs, or even external systems in test mode.
* Slower than unit tests but catch more realistic issues.

**Tools:** Spring Boot Test, Testcontainers, H2, @DataJpaTest, @WebMvcTest

✅ **Goal:** Validate wiring/configs and end-to-end paths within your app.

```java
@SpringBootTest
class OrderServiceIntegrationTest {

    @Autowired
    private OrderService orderService;

    @Test
    void shouldPlaceOrderSuccessfully() {
        Order result = orderService.placeOrder(...);
        assertNotNull(result.getId());
    }
}
```

---

### 🖥️ 3. **UI / End-to-End Tests** (Top Layer)

* Simulate user interaction in the **full application**.
* **Slowest** and most **fragile**, but test real-world scenarios.
* Used sparingly—only for **critical paths** like login, checkout, etc.

**Tools:** Selenium, Cypress, Playwright

✅ **Goal:** Ensure user-visible flows work correctly.

---

### ⚖️ Recommended Test Distribution

| Layer          | % of Total Tests | Frequency of Use                 |
| -------------- | ---------------- | -------------------------------- |
| ✅ Unit Tests   | 70%–80%          | Very frequent                    |
| ⚠️ Integration | 15%–25%          | Moderate—focus on critical paths |
| ⚠️ UI/E2E      | 5%–10%           | Minimal—only core features       |

---

### 🚀 Why Use the Test Pyramid?

* **Speed**: Unit tests are fast—build pipelines stay quick.
* **Feedback**: Fast tests = faster feedback = faster delivery.
* **Reliability**: Lower layers are more stable; higher layers are more brittle.
* **Cost**: Writing and maintaining UI tests is expensive. Use wisely.

---

### 🔄 Comparison with Anti-Pattern: The Test Ice Cream Cone 🍦

```
        Unit Tests (least)
       Integration Tests
        UI Tests (most)
```

➡️ This leads to **slow builds**, **brittle pipelines**, and **high maintenance**.

---

### ✅ Summary

| Layer       | Purpose                     | Tools                          |
| ----------- | --------------------------- | ------------------------------ |
| Unit        | Test individual classes     | JUnit, Mockito, AssertJ        |
| Integration | Test component interactions | SpringBootTest, Testcontainers |
| UI/E2E      | Test full app workflows     | Selenium, Cypress              |

**Follow the pyramid** to keep tests:

* Fast ⏱️
* Focused 🎯
* Maintainable 🔧

---

## 100. What are some best practices to follow when writing unit tests?

Here are **some of the most important best practices** to follow when writing **unit tests**, especially in Java (JUnit/Mockito context), to ensure they are **reliable**, **readable**, and **maintainable**:

---

### ✅ 1. **Follow the AAA Pattern** (Arrange-Act-Assert)

Structure your test code clearly:

```java
// Arrange
Calculator calc = new Calculator();

// Act
int result = calc.add(2, 3);

// Assert
assertEquals(5, result);
```

---

### ✅ 2. **Test One Thing Per Test**

Each test should verify one specific behavior. Don’t combine multiple assertions for unrelated things.

```java
@Test
void shouldAddTwoNumbers() {
    assertEquals(5, calculator.add(2, 3));
}
```

---

### ✅ 3. **Use Descriptive Test Names**

Use **meaningful** names that explain **what the test does** and **why** it exists.

**Bad:** `test1()`

**Good:** `shouldReturnZeroWhenListIsEmpty()`

---

### ✅ 4. **Keep Tests Fast**

Unit tests should run in milliseconds. Avoid I/O operations, file access, DB access, or long waits. Use **mocking** to isolate slow dependencies.

---

### ✅ 5. **Use Mocks Only When Necessary**

Mock **external dependencies**, not your own logic.

Use real objects for:

* DTOs
* Value types (e.g., `List`, `Map`)
* Business logic

---

### ✅ 6. **Avoid Static State or Shared Data**

Tests should be **independent** and **repeatable**. Don't rely on:

* Global state
* Order of test execution
* External files or environment state

---

### ✅ 7. **Use `@BeforeEach` for Setup**

Cleanly initialize common test setup.

```java
@BeforeEach
void setUp() {
    calculator = new Calculator();
}
```

---

### ✅ 8. **Test Both Positive and Negative Scenarios**

Don’t just test the happy path—also test:

* Exceptions
* Edge cases
* Invalid inputs

---

### ✅ 9. **Use Assertions Effectively**

Use meaningful assertions, and use libraries like **AssertJ** or **Hamcrest** for fluent assertions.

```java
assertThat(result).isNotNull().isGreaterThan(0);
```

---

### ✅ 10. **Avoid Logic in Tests**

Tests should be **simple** and **declarative**. Avoid:

* `if`/`else`
* Loops
* Complex conditions

If your test is complex, the code it's testing probably needs refactoring.

---

### ✅ 11. **Name and Structure Tests Clearly**

Organize tests to mirror your production code structure. For example:

```
/src/main/java/com/example/service/OrderService.java
/src/test/java/com/example/service/OrderServiceTest.java
```

---

### ✅ 12. **Fail for the Right Reason**

Write tests that fail **only when the behavior changes**, not due to randomness or setup issues.

---

### ✅ 13. **Don’t Test Implementation Details**

Test **behavior**, not private methods or internal logic.

❌ Don't assert method calls unless you're testing a mock interaction
✅ Do assert final outcomes and side effects

---

### ✅ 14. **Use `@DisplayName` for Readability (JUnit 5)**

```java
@DisplayName("Should return correct discount for VIP user")
```

Helps in test reports and builds.

---

### ✅ 15. **Keep Tests in CI and Run Frequently**

Include tests in your build pipelines (CI/CD) and fail builds on test failure. Tests should be part of the development lifecycle.

---

### ✅ Summary: Golden Rules

| Practice                     | Why It Matters                      |
| ---------------------------- | ----------------------------------- |
| Test one thing               | Clarity, maintainability            |
| Fast and independent         | Reliable, quick feedback            |
| Descriptive names            | Understandable failures             |
| Minimal mocking              | More realistic tests                |
| Avoid testing implementation | Refactor safely without test breaks |
| Run tests often              | Detect issues early                 |

---