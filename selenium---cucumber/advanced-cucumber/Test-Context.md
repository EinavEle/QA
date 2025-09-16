# *What is the test context?*
The test context is a dictionary containing the state of the test.
It is usually implemented as a class wrapping a hash map.
We use it to pass information between steps such as user details, randomly selected items, API requests/responses, or anything else that is created at one point and can be used later on.
Since the test context is bound to one specific test, it should be disposed of when the test is finished.
# *Context Injection*
Context injection is the way we pass the same context object between all of our step classes.
Remember, our steps exist in different classes but they should all access the same data at different times.
We are using dependency injection to initialize every step class with the same test context.
In Cucumber, we usually use a simple DI library called pico-container which handles injection in Cucumber seamlessly.
We do not need to take care of all the dependency injection configurations, we just need to add this dependency and add the required object to the step class constructor.

The maven dependency for Cucumber pico-container:
```Cucumber
<dependency>
    <groupId>io.cucumber</groupId>
    <artifactId>cucumber-picocontainer</artifactId>
    <version>7.11.2</version>
    <scope>test</scope>
</dependency>
```
In order to inject the test context into a step class, add it to the constructor and Cucumber will use pico-container to do the rest.
```Cucumber
private TestContext context;

    public Steps2(TestContext context) {
        this.context = context;
    }
```
This will inject the TestContext object into our class.
Now we can use it in our steps and put/get data from it.
# *Storing and Reading From the Context*
**How to use it?**

To use the context, we'll create a class that'll act as the "global" object and store all the data we need for the test, like in this example:
```Cucumber
public class TestContext {
    private HashMap<String, Object> context = new HashMap<>();
}
```
Once that's done, we can add methods to the object for inserting and retrieving data from the context. Then we can use these methods throughout the test, like in this example:
```Cucumber
public void put(String key, Object obj){
        context.put(key,obj);
    }

public <T> T get(String key){
        Object o = context.get(key);
        if(o==null){
            return null;
        }else{
            return (T)o;
        }
    }
```
Every time a run starts, Cucumber and Pico will include the context as part of the starting process, as we mentioned in the previous section.

**Usage Example** 

Here is an example for using TestContext to calculate two numbers:
```Cucumber
@Given("i will insert number {int} and number {int} to context")
public void iWillInsertNumberAndNumberToContext(int num1, int num2) {
    context.put("num1",num1);
    context.put("num2",num2);
}
@When("i calc the sum of them")
public void iCalcTheSumOfThem() {
    int num1 = context.get("num1");
    int num2 = context.get("num2");
    int sum = num1+num2
    context.put("sum",sum);
}
@Then("validate the sum is equal to {int}")
public void validateTheSumIsEqualTo(int sum) {
    int calcSum = context.get("sum");
    Assert.assertEquals(calcSum,sum);
}
```
**Naming Conventions**

If you want your code to be easy to understand and maintain, it's crucial to use proper naming conventions when setting up a test context. Below are some naming conventions that can help you achieve that. 

Also, when it comes to context keys, there are some best practices that can make your code less formal and easier to maintain. Here are a few examples:

1. Avoid using strings: Strings can be error-prone and hard to maintain. Instead, use constants or enums to define context keys. This way, if you mistype a context key, the compiler will catch the error.
    ```Cucumber
    LoginContext loginContext = new LoginContext("testuser", "testpassword");
    testContext.put(LoginContext.USERNAME_KEY, loginContext.getUsername());
    testContext.put(LoginContext.PASSWORD_KEY, loginContext.getPassword());
    ```
2. Use types: Instead of using generic objects, use strongly typed objects to define your context keys. This will provide additional type safety and make your code more self-documenting.
    ```Cucumber 
    testContext.put(LoginRequest.class.toString(),loginRequest);
    testContext.put(LoginRequest.class + usedId, loginRequest);
    ```
3. Be consistent: Make sure that you are consistent in your naming conventions and use the same approach throughout your codebase. This will make it easier for others to read and understand your code.