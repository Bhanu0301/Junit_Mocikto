
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
````

---

## How to Write Unit Tests with JUnit

JUnit simplifies writing and running unit tests for Java applications. Follow these steps to create effective unit tests.

---

### Step 1: Set Up JUnit in Your Project

#### Using Maven (JUnit 5)

Add the following dependency to your `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.junit.jupiter</groupId>
        <artifactId>junit-jupiter-api</artifactId>
        <version>5.9.2</version>
        <scope>test</scope>
    </dependency>
</dependencies>
```

#### Using Gradle (JUnit 5)

Add this to your `build.gradle`:

```gradle
dependencies {
    testImplementation 'org.junit.jupiter:junit-jupiter:5.9.2'
}
```

---

### Step 2: Create a Java Class to Test

Example: A simple `Calculator` class.

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

---

### Step 3: Create a JUnit Test Class

JUnit test classes should be placed in the `src/test/java` directory.

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    @Test
    void testAddition() {
        Calculator calculator = new Calculator();
        assertEquals(5, calculator.add(2, 3));
    }
    
    @Test
    void testSubtraction() {
        Calculator calculator = new Calculator();
        assertEquals(2, calculator.subtract(5, 3));
    }
}
```

---

### Step 4: Run the Tests

* **In IntelliJ / Eclipse**: Right-click the test class and select **Run**
* **Using Maven**: Run `mvn test` in the terminal
* **Using Gradle**: Run `gradle test`

---

### Step 5: Use Setup & Cleanup Methods

JUnit provides lifecycle methods for setup and cleanup.

```java
import org.junit.jupiter.api.*;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    private Calculator calculator;

    @BeforeEach
    void setUp() {
        calculator = new Calculator(); // Runs before each test
    }

    @AfterEach
    void tearDown() {
        calculator = null; // Cleanup after each test
    }

    @Test
    void testAddition() {
        assertEquals(5, calculator.add(2, 3));
    }
}
```

---

### Step 6: Test Exception Handling

Ensure methods throw expected exceptions.

```java
@Test
void testDivideByZero() {
    assertThrows(ArithmeticException.class, () -> {
        int result = 10 / 0;
    });
}
```

Learn More: Mockito – Throwing Exceptions in Unit Tests?

---

### Step 7: Run Parameterized Tests (Optional)

JUnit allows testing multiple values using `@ParameterizedTest`.

```java
import org.junit.jupiter.params.ParameterizedTest;
import org.junit.jupiter.params.provider.CsvSource;
import static org.junit.jupiter.api.Assertions.*;

class CalculatorTest {

    @ParameterizedTest
    @CsvSource({ "2,3,5", "4,5,9", "10,20,30" })
    void testAddition(int a, int b, int expected) {
        Calculator calculator = new Calculator();
        assertEquals(expected, calculator.add(a, b));
    }
}
```

---

### Step 8: Integrate with CI/CD (Optional)

JUnit works seamlessly with Jenkins, GitHub Actions, and GitLab CI for automated testing.

#### GitHub Actions Example

Create `.github/workflows/test.yml`:

```yaml
name: Run JUnit Tests

on: [push]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3

      - name: Set up JDK
        uses: actions/setup-java@v3
        with:
          java-version: '17'
          distribution: 'temurin'

      - name: Run Tests
        run: mvn test
```
