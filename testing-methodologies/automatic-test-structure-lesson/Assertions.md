# *Intro*
Assertions are statements in tests that verify expected behavior and help ensure that the code being tested functions correctly. 
They are used to compare the actual results of the code being tested against the expected outcomes.
Assertions are typically placed in the "Assert" phase of the Arrange-Act-Assert (AAA) pattern in testing. 
They evaluate a condition and throw an exception if the condition is false, indicating a test failure.
Assertions play a crucial role in validating the behavior of the code and providing feedback on whether the code is functioning as expected.
When an assertion fails, it indicates a deviation from the expected behavior, enabling developers to identify and fix issues.

We want the assertions to be as precise as possible for several reasons:
- Readability and expressiveness: Using matchers like arrayContains, greaterThan, and so on provides higher readability and expressiveness to the code. When we read arrayContains(expectedItem, actualArray), it is much more clear than assertTrue(Arrays.asList(actualArray).contains(expectedItem)). Matchers directly refer to the type of the check we are performing and present the result in a more understandable manner.
- Readable and maintainable code: Using matchers reduces the need to construct expressions inside assertTrue. Matchers offer a higher capability to perform the check and determine whether the assertion described in the check is true or not.
- Concise information: Matchers provide more informative and detailed error messages. Instead of seeing a generic assertion failure message like "assertion failed", matchers offer customized and specific error messages that assist in immediately identifying the cause of the failure.

We will expand on types of assertions in the “JUnit” unit.

For example:
```java
public class ExampleTest {

    @Test
    public void testAddition() {
        int result = 2 + 2;
        assertEquals(4, result, "Addition result should be 4");
    }

    @Test
    public void testDivision() {
        int numerator = 10;
        int denominator = 2;
        int result = numerator / denominator;
        assertTrue(result, greaterThan(0));
    }

    @Test
    public void testArrayLength() {
        String[] fruits = {"Apple", "Banana", "Orange"};
        assertEquals(3, fruits.length, "Array length should be 3");
    }
}
```
In this example, we have three test methods, each demonstrating different types of assertions:
- In the `testAddition` method, we perform an addition operation and assert that the result is equal to 4 using the `assertEquals` method.
- In the `testDivision` method, we divide two numbers and assert that the result is greaterThan 0 using the `assertTrue` method. By targeting our Assert (in our case, a greaterThan) it will be easier for us to understand what the fail is about than to write a general Assertion.
- In the `testArrayLength` method, we check the length of an array and assert that it is equal to 3 using the `assertEquals` method.

If any of these assertions fail during the test execution, an assertion error will be thrown, indicating that the expected condition was not met.
These assertions provide a way to validate specific conditions or expected outcomes in tests, helping to ensure that the code behaves as intended.