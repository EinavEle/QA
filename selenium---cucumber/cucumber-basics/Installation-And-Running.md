# *How to Install Cucumber in our Project*
To add Cucumber to a Maven project in Selenium Java, you can follow these steps:
1. Create a new Maven project in IntelliJ IDEA.
2. Add the following dependency to your pom.xml file:
    ```html
    <dependency>
      <groupId>io.cucumber</groupId>
      <artifactId>cucumber-java</artifactId>
      <version>7.0.0</version>
    </dependency>
    ```
This will add the Cucumber Java library to your project.
3. Create a new directory called "features" in the src/test/resources directory of your project. 
This directory will contain the feature files for your Cucumber tests.

4. Create a new directory called "steps" in the src/test/java directory of your project. This directory will contain the Java classes that define the step definitions for your Cucumber tests.

5. Create a new feature file in the "features" directory. This file should have the ".feature" extension and should contain the scenarios that you want to test.

6. Create a new Java class in the "stepds" directory. This class should contain the step definitions for the scenarios in your feature file.

7. Run your Cucumber tests by executing the following Maven command from the command line:
    ```Maven
    mvn test
    ```
This will execute all of the tests in your Maven project, including the Cucumber tests.
# *First Simple Test* 
1. First, create a feature file with the scenarios that you want to test. In this example, we'll create a file called "test.feature" in the "features" directory, with the following content:
    ```Cucumber
    Feature: Search Feature
      Scenario: Search for a product
        Given I am on the homepage
        When I search for "iPhone"
        Then Validate i'm on the iphone search results page
    ```
2. Next, create a Java class that defines the step definitions for the scenarios in the feature file. 
In this example, we'll create a file called "Steps.java" in the "steps" directory, with the following content:
    ```java
    import io.cucumber.java.en.Given;
    import io.cucumber.java.en.When;
    import io.cucumber.java.en.Then;
    import org.openqa.selenium.By;
    import org.openqa.selenium.WebDriver;
    import org.openqa.selenium.chrome.ChromeDriver;
    import org.testng.Assert;
    public class Steps {
            private WebDriver driver;
            private final String webDriverPath = "path/to/chromedriver";
            @Given("I am on the homepage")
            public void iAmOnTheHomepage() {
                    // Code to set up the web driver and navigate to the homepage
                    System.setProperty("webdriver.chrome.driver", webDriverPath);
                    driver = new ChromeDriver();
                    driver.get("https://www.google.com/");
            }
            @When("I search for {string}")
            public void iSearchFor(String searchTerm) {
                driver.findElement(By.xpath("//input[@title='Search']"))
                      .sendKeys(searchTerm);
                driver.findElement(
                      By.xpath("//center//input[contains(@value,'Feeling
                                Lucky')]")).click();
            }
            @Then("Validate i'm on the iphone search results page")
            public void iShouldSeeAListOfSearchResults() {
                    String currentUrl = driver.getCurrentUrl();                 
                    Assert.assertEquals(currentUrl,
                                        "https://www.apple.com/il/iphone/");
                    driver.quit();
            }
    }
    ```
3. Finally, run the Cucumber test by executing the "mvn test" command from the command line. 

This will run all the tests in your Maven project, including the Cucumber tests with Selenium.