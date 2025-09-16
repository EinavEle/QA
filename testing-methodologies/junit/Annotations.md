# Common Annotations
Annotations are used to provide additional information about a test method or class. 
This information can be used by the JUnit framework to control how the test is run.

Here are some of the most common annotations in JUnit:

- @Test: This annotation is used to mark a method as a test method. 
- Test methods are run by the JUnit framework.
- @BeforeEach: This annotation is used to mark a method that is run before each test method. 
- This method is typically used to set up the test environment.
- @AfterEach: This annotation is used to mark a method that is run after each test method. 
This method is typically used to tear down the test environment.
- @BeforeAll: This annotation is used to mark a method that is run once before all of the test methods in a class are run. 
This method is typically used to set up shared resources.
- @AfterAll: This annotation is used to mark a method that is run once after all of the test methods in a class have been run. This method is typically used to tear down shared resources.
- @Ignore: This annotation is used to mark a test method that should not be run. Ignored tests are not counted when the JUnit framework reports the number of tests that have passed or failed.
- @Disabled: This annotation is used to mark a test method that is currently disabled. 
- Disabled tests are not run, but they can be re-enabled by removing the annotation.
- @Tag: This annotation is used to tag a test method with a specific tag. 
Tags can be used to filter tests when running the JUnit framework.
