Hooks are a testing technique that allows you to run code before or after a test. 
This can be useful for setting up or cleaning up your environment, or for logging or debugging information.

There are two main types of hooks:

Setup hooks: These hooks run before each test. 
They are a good place to set up your environment, such as creating a database or loading test data.

Teardown hooks: These hooks run after each test. They are a good place to clean up your environment, such as deleting test data or closing a database connection.

To use hooks, you need to add them to your test class.
You can do this by using the @Before and @After annotations.

# Common Hooks
**BeforeEach/AfterEach**

These annotations will make a method run before/after every test in the class.

**BeforeAll/AfterAll**

These annotations will make a method run before/after all the tests in the class.

In the following example you can see that we are creating the object that we are going to test in the preliminary phase of the hooks.
```java
public class MyTest {
    private static CalcClass calculate;

    @BeforeEach
    void setup(){
        calculate = new CalcClass();
    }
    @Test
    void calc_sum_test() {
        assertEquals(calculate.calcSum(3,3),6);
    }
```
