# Junit_Mocikto

Learning JUnit and Mockito

*JUnit* provides a structured framework for writing and running tests.  
*Mockito* helps mock dependencies for effective isolation and verification.

---

## What is JUnit?

JUnit is a popular Java testing framework that helps developers write and run unit tests.

---

## Key Features

### Annotations
`@Test`, `@BeforeEach`, `@AfterEach`, etc., are used to organize test cases.

*JUnit employs annotations to specify and maintain test cases:*

- `@Test`: Indicates that a method is a test case.
- `@BeforeEach`: Executes before each test (for example, setup code).
- `@AfterEach`: Executes after each test (for example, cleanup code).
- `@BeforeAll`: Executes once before all tests in a class.
- `@AfterAll`: Executes once after all the tests.
- `@Disabled`: Disables a test case.

---

### Assertion Statements
`assertEquals`, `assertNotNull`, `assertTrue`, etc., are used to confirm expected outputs.

*Assertions check expected outputs and help identify problems early. Some common assertions are:*

- `assertEquals(expected, actual)`: Tests whether two values are equal.
- `assertTrue(condition)`: Checks if a condition is true.
- `assertFalse(condition)`: Checks if a condition is false.
- `assertThrows(Exception.class, () -> { })`: Checks that an exception is thrown.

---

### Build and CI/CD Integration
Easy integration with build tools (Maven, Gradle) and CI/CD pipelines  
(Jenkins, GitHub Actions, etc.) to automate testing.

---

### Test Driven Development (TDD)
Supports Test Driven Development (TDD).

---

### Parameterized Tests
JUnit allows running the same test with different inputs using `@ParameterizedTest`:

- `@ValueSource(ints = {1, 2, 3})`: Provides multiple values for testing.
- `@CsvSource({ "1, One", "2, Two" })`: Supplies multiple test cases in CSV format.
- `@MethodSource`: Supplies test data from a static method.

---

### Exception Handling
JUnit can test if a method correctly throws an expected exception.

```java
@Test
void testException() {
    assertThrows(ArithmeticException.class, () -> {
        int result = 10 / 0;
    });
}
