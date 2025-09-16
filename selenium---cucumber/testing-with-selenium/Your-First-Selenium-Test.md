The automation testing framework follows a clear process.
First, we gather the necessary information, and then we create and set up test data.
If the test involves the user interface, we use tools like Selenium WebDriver to perform the required actions and produce the expected results. 
Finally, we verify the test results through assertions and end the test, whether it was successful or not. 
To explain this process further, let's take an example test.
```java
@BeforeTest
public void beforeAll(){
    System.setProperty("webdriver.chrome.driver", webDriverPath);
    driver = new ChromeDriver();
    driver.get(URL);
}
@AfterTest
public void afterAll(){
    driver.close();
}

@Test
public void loginTest(){
    // Arrange
    String testedUsername = "student";
    String testedPassword = "Password123";
    loginPage = new LoginPage(driver);
    // Act
    loginPage.fullLoginProcess(testedUsername,testedPassword);
    // Assert
    homePage = new HomePage(driver);
    Assert.assertTrue(homePage.headerIsVisible());
}
```
The test has three parts:
- First, we sort the data
- Second, we perform the test actions
- Third, we conduct the actual test

Before starting the test, we need to do some general actions like bending and patterning materials. 
These actions are not part of the test and will only be done once before all the tests start.