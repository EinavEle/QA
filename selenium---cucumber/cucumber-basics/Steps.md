**Steps Method:**

Step method should be defined with the "@Given", "@When", or "@Then" annotations depending on the type of step. 
The step method should contain the code that performs the action or checks the condition specified in the step.

Here's an example of how a step method should look like in Selenium Java:
```java
@When("I enter username as '{string}' and password as '{string}'")
public void enterCredentials(String username, String password) {
    simplePage.fillUserNameField(username);
    simplePage.fillPasswordField(password);
}
@When("I click on the login button")
public void clickLoginButton() {
    simplePage.clickLoginButton();
}
@Then("Validate i see the dashboard page")
public void verifyDashboardPage() {
    simplePage.verifyDashboardPage();
}
```
In this example, there are four steps: "goToLoginPage", "enterCredentials", "clickLoginButton", and "verifyDashboardPage". 
Each step does something specific like going to a page, entering text, clicking buttons, or checking the URL.
We use annotations to specify what type of step it is.
# Steps class:
Steps class is a Java class that defines the step methods that are used in the Cucumber feature files.

Here's an example of how a Steps class should look like:
```Cucumber
public class LoginSteps {
    private WebDriver driver;

    @Given("I am on the login page")
    public void goToLoginPage() {
        driver = new ChromeDriver();
        driver.get("https://www.example.com/login");
    }

    @When("I enter username as ‘{string}’ and password as ‘{string}’")
    public void enterCredentials(String username, String password) {
        WebElement usernameField = driver.findElement(By.id("username"));
        WebElement passwordField = driver.findElement(By.id("password"));
        usernameField.sendKeys(username);
        passwordField.sendKeys(password);
    }

    @When("I click on the login button")
    public void clickLoginButton() {
        WebElement loginButton = driver.findElement(By.id("loginButton"));
        loginButton.click();
    }

    @Then("I see the dashboard page")
    public void verifyDashboardPage() {
        String expectedUrl = "https://www.example.com/dashboard";
        String actualUrl = driver.getCurrentUrl();
        assertEquals(expectedUrl, actualUrl);
        driver.quit();
    }
}
```
In this example, the Steps class is named "LoginSteps". The class contains the step methods that correspond to the steps in the feature file. The "@Given", "@When", and "@Then" annotations are used to indicate the type of step.

The class also includes a WebDriver instance, which is used to interact with the web page in the step methods. 
The WebDriver instance is typically created in the "@Before" method of the test class and initialized in the first step method.

Once the Steps class is defined, it can be used in the Cucumber runner class to run the tests. The Cucumber runner class should be configured to use the Steps class and the feature file, and the tests can be run by executing the runner class.