Assertions are statements that check the outcome of a test. If the outcome is not as expected, the assertion will fail and the test will be marked as a failure.

# Using JUnit Assertions
There are many different types of assertions available in JUnit. Some of the most common assertions are:
- assertEquals(): This assertion checks if two objects are equal.
- assertNotEquals(): This assertion checks if two objects are not equal.
- assertTrue(): This assertion checks if a boolean expression is true.
- assertFalse(): This assertion checks if a boolean expression is false.
- assertNull(): This assertion checks if a reference is null.
- assertNotNull(): This assertion checks if a reference is not null.

To use assertions in JUnit, you need to import the org.junit.Assert class. You can then use the methods in this class to check the outcome of your tests.
For example:
```java
void calc_sum_test() {
        assertEquals(calculate.calcSum(3,3),6);
    }
```
# Hamcrest Assertion Library
Hamcrest provides a rich set of matchers that are not available in JUnit. 
We usually prefer to use the most exact assertion possible so the error we get if the test fails will be clear and help us investigate the failure.

Here are some examples of assertions provided by Hamcrest that are not available in JUnit:

Here are some of the most common Hamcrest matchers:

1. Collection Matchers:
a) hasItem: Checks if a collection contains a specific item.
b) hasItems: Checks if a collection contains all specified items.
c) contains: Checks if a collection contains elements in a specific order.
d) containsInAnyOrder: Checks if a collection contains elements in any order.
2. String Matchers:
a) startsWith: Checks if a string starts with a specific substring.
b) endsWith: Checks if a string ends with a specific substring.
c) containsString: Checks if a string contains a specific substring.
d) matchesPattern: Checks if a string matches a regular expression pattern.
3. Number Matchers:
a) greaterThan: Checks if a number is greater than a specified value.
b) lessThan: Checks if a number is less than a specified value.
c) closeTo: Checks if a floating-point number is close to a specified value with a given delta.
4. Object Matchers:
a) equalTo: Checks if an object is equal to another object using the equals method.
b) sameInstance: Checks if two references point to the same instance.
c) hasProperty: Checks if an object has a specific property with a given value.
5. Custom Matchers:
Hamcrest allows you to create your custom matchers by implementing the Matcher interface. This gives you the ability to define custom assertions specific to your domain or application.

These are just a few examples of the matchers available in Hamcrest. The library provides a wide range of matchers for different types of assertions, making it highly flexible and expressive for writing test assertions.
