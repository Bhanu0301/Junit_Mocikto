# Junit_Mocikto
Learning JUnit and Mockito

*JUnit* provides a structured framework for writing and running tests.
*Mockito* helps mock dependencies for effective isolation and verification.

What is JUnit?
JUnit is a popular Java testing framework that helps developers write and run unit tests. 

Key Features

Annotations - @Test, @BeforeEach, @AfterEach...etc - to organize test cases.

*JUnit employs annotations to specify and maintain test cases:*
*@Test: Indicates that a method is a test case.*
*@BeforeEach: Executes before each test (for example, setup code).*
*@AfterEach: Executes after each test (for example, cleanup code).*
*@BeforeAll: Executes once before all tests in a class.*
*@AfterAll: Executes once after all the tests.*
*@Disabled: Disables a test case.*


Assertion Statements - assertEquals, assertNotNull, assertTrue...etc - to confirm expected outputs.

*Assertions check expected outputs and help identify problems early. Some common assertions are:*
*assertEquals(expected, actual): Tests whether two values are equal.*
*assertTrue(condition): Checks if a condition is true.*
*assertFalse(condition): Checks if a condition is false.*
*assertThrows(Exception.class, () -> { }): Checks that an exception is thrown.*

Easy integration with build tools(Maven, Gradle) and CI/CD pipelines (Jenkins, Github actions..etc) to automate testing.

Supports TDD (Test Driven Development)

Parameterized Tests: JUnit allows running the same test with different inputs using @ParameterizedTest:

*@ValueSource(ints = {1, 2, 3}): Provides multiple values for testing.*
*@CsvSource({ “1, One”, “2, Two” }): Supplies multiple test cases in CSV format.*
*@MethodSource: Supplies test data from a static method.*

 Exception Handling: JUnit can test if a method correctly throws an expected exception.
 
    @Test
    void testException() {
        assertThrows(ArithmeticException.class, () -> {
            int result = 10 / 0;
        });
    }
    
 Timeout Handling: JUnit allows setting a time limit for test execution:
 
    @Test
    @Timeout(2) // Fails if execution takes more than 2 seconds
    void testTimeout() {
        Thread.sleep(1000);
    }
 Test Suites: JUnit enables grouping multiple test classes into a suite using @Suite and @SelectClasses.

 Mocking Support: JUnit integrates with Mockito for mocking dependencies, enabling isolated testing of components.
