
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

## Why Use Mockito for Unit Testing?

Mockito is useful in the following cases when it comes to unit testing:

- Isolates the component under test by replacing actual dependencies with mock dependencies/objects.
- Avoids database, network, or file dependencies, making tests faster and more reliable.
- Allows behavior verification (e.g., checking if a method was called), supports stubbing, and enables controlled responses for mocked methods.

---

## Features of Mockito

Mockito provides powerful mocking capabilities for unit testing in Java. It helps isolate dependencies, control method responses, and verify interactions.

Below are its key features:

---

### 1. Mocking Dependencies

Mockito allows mocking objects to replace real dependencies in a test environment, preventing tests from depending on databases, APIs, or external systems. This ensures tests run in isolation, making them faster and more reliable.

**Example:**
```java
UserRepository repoMock = mock(UserRepository.class);
````

---

### 2. Stubbing Method Behavior

Stubbing lets you define method responses for mock objects, ensuring predictable behavior in tests regardless of external factors. This allows precise control over test conditions and expected outcomes.

**Example:**

```java
when(repoMock.findById(1)).thenReturn(new User(1, "Alice"));
```

---

### 3. Behavior Verification

Mockito allows checking whether a method was called, how many times, and with which arguments, ensuring correct interactions between components.

**Example:**

```java
verify(repoMock, times(1)).findById(1);
```

---

### 4. Assertion Support

Mockito works with JUnit assertions to validate test outputs, confirming if the system produces expected values.

**Example:**

```java
assertEquals("Alice", user.getName());
assertNotNull(user);
```

---

### 5. Mockito Annotations

Mockito provides `@Mock`, `@InjectMocks`, and `@Spy` annotations to simplify mock object setup, reduce boilerplate code, and improve readability.

**Example:**

```java
@Mock
UserRepository repoMock;

@InjectMocks
UserService service;
```

---

### 6. Spies (Partial Mocking)

A spy allows real method calls but enables selective method overriding. This is useful for testing specific behaviors while preserving original functionality.

**Example:**

```java
List<String> spyList = spy(new ArrayList<>());
spyList.add("Hello");
verify(spyList).add("Hello");
```

---

### 7. Exception Handling

Mockito allows forcing a method to throw an exception, which helps test error-handling logic and system robustness.

**Example:**

```java
when(repoMock.findById(1))
    .thenThrow(new RuntimeException("Database error"));
```

---

### 8. Argument Matchers

Mockito provides argument matchers such as `anyInt()`, `anyString()`, and `eq(value)` to handle dynamic inputs during stubbing and verification.

**Example:**

```java
when(repoMock.findById(anyInt()))
    .thenReturn(new User(1, "Alice"));
```

---

## How to Write Unit Tests with Mockito

Mockito makes unit testing easier by allowing developers to mock dependencies, control method behavior, and verify interactions.

---

### Step 1: Add Mockito Dependency

#### Maven (`pom.xml`)

```xml
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>5.2.0</version>
    <scope>test</scope>
</dependency>
```

#### Gradle (`build.gradle`)

```gradle
testImplementation 'org.mockito:mockito-core:5.2.0'
```

---

### Step 2: Create a Sample Class to Test

Suppose a `UserService` class depends on `UserRepository` to fetch user data.

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

---

### Step 3: Write a Mockito Test Class

Create a test class and mock dependencies.

```java
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.BeforeEach;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.MockitoAnnotations;

import static org.mockito.Mockito.*;
import static org.junit.jupiter.api.Assertions.*;

class UserServiceTest {

    @Mock
    private UserRepository userRepository;

    @InjectMocks
    private UserService userService;

    @BeforeEach
    void setUp() {
        MockitoAnnotations.openMocks(this);
    }

    @Test
    void testGetUserById() {
        // Arrange
        User mockUser = new User(1, "Alice");
        when(userRepository.findById(1)).thenReturn(mockUser);

        // Act
        User result = userService.getUserById(1);

        // Assert
        assertNotNull(result);
        assertEquals("Alice", result.getName());
        verify(userRepository, times(1)).findById(1);
    }
}
```

---

### Step 4: Explanation of the Test

* **Mock Creation**: `@Mock` creates a fake `UserRepository`.
* **Dependency Injection**: `@InjectMocks` injects mocks into `UserService`.
* **Setup Method**: `MockitoAnnotations.openMocks(this)` initializes mocks.
* **Stubbing**: Defines expected behavior using `when().thenReturn()`.
* **Assertions**: Validates output using JUnit assertions.
* **Verification**: Ensures interactions occurred as expected.

```
