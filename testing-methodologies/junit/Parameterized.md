# What is a Parameterized Test
A parameterized test is a test that can be run multiple times with different data. 
This can be useful for testing code that is expected to work with a variety of inputs.

To create a parameterized test, you need to use the @ParameterizedTest annotation. This annotation takes two arguments: the data provider and the test method.

The data provider is a method that returns a collection of data. 
The test method is the method that will be run with each piece of data.
# Example 
```java
@ParameterizedTest
    @MethodSource("getIntegers")
    public void testAdd(int a, int b, int expected) {
        Assertions.assertEquals(expected, a + b);
    }

    private static Stream<Arguments> getIntegers() {
        return Stream.of(
            Arguments.of(1, 2, 3),
            Arguments.of(5, 6, 11),
            Arguments.of(10, 10, 20)
        );
    }
```
The getIntegers() method returns a Stream of Arguments objects. Each Arguments object contains the three values that will be used to run the testAdd() method.

The testAdd() method takes three arguments: the first and second numbers to add, and the expected result. The method then asserts that the result of adding the first and second numbers is equal to the expected result.

When the ParameterizedTest annotation is used, JUnit will run the testAdd() method once for each piece of data in the data provider. This means that the testAdd() method will be run three times in this example.

Parameterized tests can be a powerful tool for testing code that is expected to work with a variety of inputs. By using parameterized tests, you can save time and effort by running the same test multiple times with different data.
