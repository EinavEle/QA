# *The Scenario Class*
The ‘Scenario’ class in Cucumber is a representation of a single scenario in a feature file. 
It provides methods to interact with the scenario and retrieve various pieces of information about it during runtime.

Some of the data that can be obtained from the Scenario class include:

- Scenario name: The name of the scenario as specified in the feature file.
- Scenario status: The status of the scenario (passed, failed, skipped, etc.).
- Scenario source tag names: The tags associated with the scenario.
- Scenario source location: The file path and line number where the scenario is defined.
- Scenario result: The result of the scenario (pass or fail).
- Scenario duration: The time taken to execute the scenario.

In addition, the ‘Scenario’ class also provides methods for interacting with the scenario during runtime, such as adding tags, attaching screenshots, logging messages, and retrieving scenario context information.
These methods can be used to customize the behavior of the scenario and capture additional information during runtime.

Example for using ‘Scenario’ class:
```java
public class StepDefinitions{
    private Scenario scenario;
        @Before
        public void before(Scenario scenario){
            this.scenario = scenario;
        }
        @Given("I have apples {}")
        public void iHaveApples(int numApples){
            scenario.log("I have " + numApples + " apples");
            // Perform logic to simulate having a certain number of apples
        }
        @Then("I eat {} apples")
        public void iEatApples(int numApples){
            scenario.log("I eat " + numApples + " apples");
            // Perform logic to simulate eating a certain number of apples
        }
        @After
        public void after(Scenario scenario){
            if (scenario.isFailed()) {
                takeScreenshot(testName);
            }
        }
}
```
In this example, the ‘Scenario’ class is used to log messages during the execution of each step using the ‘log()’ method.
Additionally, the ‘Before’ and ‘After’ hooks are used to set up and tear down the scenario object and perform custom logic before and after the scenario is executed.

The ‘After’ hook also checks if the scenario failed using the ‘isFailed()’ method and takes a screenshot and attaches it to the scenario if it did. 
This is an example of how the ‘Scenario’ class can be used to customize the behavior of the test suite and capture additional information during runtime.