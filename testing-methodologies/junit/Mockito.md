# What is  a Mock?
A mock is a fake object that simulates the behavior of a real object. It is used in unit testing to isolate the behavior of a single unit of code from its dependencies. This allows the unit of code to be tested in isolation, without having to worry about the behavior of its dependencies.
In our course we use Mockito, Mockito is a mocking framework for Java that allows you to create mock objects.
 Mockito is a popular mocking framework and is used by many Java developers.

# Adding Mockito to a Project
To add Mockito to a project using Maven, you need to add the following dependency to your pom.xml file:
```xml
<dependency>
    <groupId>org.mockito</groupId>
    <artifactId>mockito-core</artifactId>
    <version>4.6.1</version>
    <scope>test</scope>
</dependency>
```
# Using Mockito
```java
import org.junit.jupiter.api.Test;
import org.mockito.Mockito;
import java.util.List;
import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.mockito.Mockito.*;
public class MyServiceTest {
    @Test
    public void testMyService() {
        // Create a mock object
        MyDependency mockDependency = Mockito.mock(MyDependency.class);
        
        // Define the behavior of the mock object
        when(mockDependency.getData()).thenReturn("Mocked data");
        // Create the object under test, injecting the mock dependency
        MyService myService = new MyService(mockDependency);
        // Perform the test
        String result = myService.doSomething();
        // Verify the interaction with the mock object
        verify(mockDependency, times(1)).getData();
        // Perform assertions
        assertEquals("Mocked data processed", result);
    }
}
```
Here's what the different steps in the example do:

1. Create a mock object of the ‘MyDependency’ class using ‘Mockito.mock()’. 
This creates a simulated version of the dependency.

2. Define the behavior of the mock object using ‘when(mockDependency.getData()).thenReturn("Mocked data")’. 
This tells Mockito that when the getData() method is called on the mock object, it should return "Mocked data".

3. Create an instance of ‘MyService’ and inject the mock dependency into it.

4. Perform the test by calling the ‘doSomething()’ method on the ‘MyService’ object. This will internally invoke the getData() method on the mock object.

5. Verify the interaction with the mock object using ‘verify(mockDependency, times(1)).getData()’. 
This ensures that the getData() method was called exactly once during the test.

6. Perform assertions on the result of the test.
