# Testing Interview Questions & Answers (Deep Dive)

## 1. JUnit Internals
**Test Runner:** JUnit uses a `Runner` internally (e.g., `BlockJUnit4ClassRunner` in JUnit4) to inspect the class using Reflection, find methods annotated with `@Test`, and invoke them.
**Instance Lifecycle:**
- JUnit creates a **NEW instance** of the test class for **EACH** test method. This ensures isolation. Modifying instance variables in `testA()` won't affect `testB()`.

## 2. Mockito Internals (Proxying)
How does `when(mock.method()).thenReturn(value)` work?
1.  **CGLIB/ByteBuddy:** Mockito creates a dynamic proxy (subclass) of your mocked class.
2.  **Stubbing:** When you call `mock.method()`, the proxy intercepts it. It records "User called method X". It returns a default value (null/0).
3.  **Mapping:** `thenReturn(value)` maps the last recorded method call to the return value.
4.  **Runtime:** When actual test runs and calls `mock.method()`, proxy looks up the map and returns the stubbed value.
**Limitation:** Can't mock `final` classes/methods (historically, though `mockito-inline` dependency now allows it). Can't mock `static` methods (requires `Mockito.mockStatic`).

## 3. Test Pyramid
1.  **Unit Tests (70%):** Fast. Isolated. Mock IO/DB. (JUnit).
2.  **Integration Tests (20%):** Test interaction. Real DB (H2/Container). (Spring Boot Test).
3.  **E2E / UI Tests (10%):** Slow. Flaky. Test user flows. (Selenium/Cypress).

## 4. TDD (Test Driven Development)
**Cycle: Red -> Green -> Refactor**
1.  **Red:** Write a failing test for a feature (Feature doesn't exist yet).
2.  **Green:** Write minimal code to pass the test.
3.  **Refactor:** Clean up code while keeping test passing.

## 5. Parameterized Tests (JUnit 5)
Avoids writing multiple test methods for same logic with different data.
```java
@ParameterizedTest
@ValueSource(ints = {1, 3, 5, -15})
void isOdd_ShouldReturnTrueForOddNumbers(int number) {
    assertTrue(Numbers.isOdd(number));
}
```
