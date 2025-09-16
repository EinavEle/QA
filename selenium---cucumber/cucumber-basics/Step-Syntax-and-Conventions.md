Maintaining proper writing conventions in all steps is crucial. To achieve this, specific rules have been defined for writing each step:
1. The location of the step should be indicated at the beginning of each test, specifying the page where the operation is performed. 
For example:
    ```Cucumber
    On the login page - click on the OK button.
    ```
2. The action being carried out should be clearly stated to make it easy to understand. 
    For example:
    ```Cucumber
    On the home page - click on the user search button.
    ```
    It is incorrect to write: 
    ```Cucumber
    Click search`
    ```
3. Use a hyphen to separate the parts of the sentence.
4. Strings sent to step methods should be marked with ‘’. It is important to specify the string in the annotation as well. 
    For example: 
    ```Cucumber
    On the home page - type in the search bar 'automation is fun'.`
    ```
    In the annotation of the method, it looks like this:
    ```Cucumber
    @When("On the home page - type in the search bar '{string}'").
    ```
    No apostrophe is needed for sending numbers.
5. Each step should have only one action. Do not write more than one action in a step.
    For example: 
    ```Cucumber
    When I send a request to get all the restaurants. 
    And I randomly select a restaurant.
    ```
    It is incorrect to write:
    ```Cucumber
    When I send a request to get all the restaurants and I randomly select one.
    ```
6. Validation steps will always appear under "Then" or in "And" which continues with "Then".
7. Each page will have its corresponding steps class.
8. Use the past tense for "Given", present tense for "When", and present tense for "Then".
9. The names of variables should be clear without abbreviations. For example, use "int numberOfWordInPage'' instead of "int numofWP".
10. Do not enter more than three variables in one step. If necessary, build a table (we will discuss this later).