# *When to use scenario outline?*
Scenario Outline is used when you need to run the same scenario with multiple sets of data. It is a way to reduce code duplication and increase the efficiency of your testing. 
You can use Scenario Outline when you have a scenario that requires the same steps to be executed with different inputs or data sets.
# *Implementation and examples*
Here's an example of using Scenario Outline in Cucumber:
```Cucumber
Scenario Outline: Login with different credentials
  Given I am on the login page
  When I enter ‘<username>’ and ‘<password>’
  And I click the login button
  Then I should be logged in

  Examples:
    | username    | password |
    | user1       | pass1    |
    | user2       | pass2    |
    | user3       | pass3    |
```
In this example, the Scenario Outline is used to test the login feature with different sets of usernames and passwords. 
The placeholders <username> and <password> are used to represent the actual values that will be used during testing.

The Examples section below the Scenario Outline defines the data sets to be used for testing. In this case, we have defined three data sets with different values for the input credentials.

When Cucumber runs this scenario, it will execute the steps for each data set defined in the Examples section. 
This allows you to test the same scenario with multiple variations of data, without having to write separate scenarios for each data set.