# *Scenario Structure*
**Given/When/Then**

"Given/When/Then" is a scenario structure used in the BDD (Behavior-Driven Development) methodology to describe the behavior of a software system.

The terms "Given/When/Then" can be considered as equivalent to "Arrange/Act/Assert".
- The "Given" step is where you set the stage for what you're testing. You describe what the system looks like when the test starts and what data it has to work with. 
It's important to make this step easy to understand for everyone on the team, including the non-technical folks.
    ```Cucumber
    Given that the user is logged in
    ```
- The "When" step shows what the user does that causes the system to respond in a particular way. It can be anything from clicking a button to entering some data. It's written in a way that's easy to understand and from the user's point of view.
    ```Cucumber
    When the user clicks the "Add to cart" button on the product page.
    ```
- The "Then" step tells you what to expect after you take an action. It could be a message that pops up, a change in the system's status, or any other kind of output. It's written in a user-friendly way, so that everyone involved in the project can understand it.
    ```Cucumber
    Then Validate user is on dashboard page
    ```
- Multiple "Given" and "Then" steps may be needed to describe a behavior completely. 
"Given" steps describe the setup, while "Then" steps describe the expected outcomes.
 You can use "And" to combine conditions or actions in a single step for better readability and brevity.
    ```Cucumber
    Given the user has entered valid login credentials
    And the user is on the homepage
    When the user clicks on the "Profile" button
    And selects "Edit Profile"
    And changes the email address to a valid email address
    Then the system should display a success message
    And the user's email address is updated in the system.
    ```
**Don’t combine two actions in one step** and don't combine both an action and a verification in the same step. 

In order to enable the construction of different and varied tests and ensure that anyone can come and assemble the tests, we would like to separate and make the actions as unique as possible. 

With the help of the separation of steps, we can compile a wider variety of tests without adding redundant and duplicate steps

For example, if you have a test that would get a list of restaurants from an API request and then randomly select one, you should define two separate steps, one to get the list of restaurants and store it , and the second to read the list  and randomly select one.

The correct way to do it:
```Cucumber
When I send a request to get all the restaurants.   
And I randomly select a restaurant    
```
The incorrect way to do it:
```Cucumber
When I send a request to get all the restaurants and I randomly select one
```
**Scenario Background**

The scenario background is used to define preconditions or steps that are common to multiple scenarios in a feature file. For example, if all scenarios in a feature file require a user to be logged in, the login step can be defined in the scenario background to avoid repeating the same steps in each scenario.

The scenario background can be defined using the Cucumber annotations. To define a scenario background, you can use the "@Given" annotation followed by the steps that need to be executed. For example:
```Cucumber
@Given("I am logged in as a registered user")
public void login() {
    // code to log in as a registered user
}
```
This annotation and method define a scenario background that logs in a user before each scenario. To use this scenario background in a feature file, you can simply reference the annotation in the feature file:
```Cucumber
Feature: My Feature
  Background: 
    Given I am logged in as a registered user


  Scenario: My First Scenario is using the given from Background
    And I do something
    When I do something else
    Then something happens

  Scenario: My Second Scenario is also using the given from Background
    And I do something Else
    When I do other thing
    Then something happens 
```
This feature file will execute the scenario background before executing the steps in each scenario, ensuring that the user is logged in before performing any actions.