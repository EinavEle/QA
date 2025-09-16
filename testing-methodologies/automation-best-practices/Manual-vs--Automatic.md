# Manual test structure
The structure of a manual test typically includes:
- Test Case Identifier: A unique number or identifier for easy reference.
- Test Case Title: A concise and descriptive title summarizing the test's purpose.
- Test Case Description: Detailed steps and any necessary preconditions.
- Test Steps: Clear, step-by-step instructions for the tester.
- Expected Results: The desired outcome after each step.
- Test Data: Specific data or inputs required for the test.
- Test Execution Notes: Additional observations or comments during execution.
- Test Results: Actual outcome or result observed.
- Test Case Status: Overall disposition of the test case (pass, fail, etc.).

In a manual test there is the personal touch which also allowed to see things like small changes in the app layout

Example:
[Blank template testCase](https://docs.google.com/spreadsheets/d/1HISIeCP3Q_8IvqSgEV-UwMv7fqG12tUMKd_CnZvu35I/edit?usp=sharing)

# Automatic test structure
In automatic tests we will work with a pattern also called AAA.
The AAA (Arrange-Act-Assert) pattern is a common structure for automated tests. It involves three steps:
- Arrange: Set up the test by initializing objects, configuring the system, and preparing necessary data.
- Act: Perform the action or operation being tested, such as calling methods or interacting with interfaces.
- Assert: Verify the expected outcome or behavior by comparing actual results against expected values.

Using the AAA pattern helps organize tests, improve readability, and ensure consistent testing practices.
```java
test('Create restaurants via api and check it in ui', async () => {
    //Arrange
    const myNewRest = { address: "Abc", id: 100, name: "Def", score: 5 }
    await restaurantsAPI.createRestaurant(myNewRest);
    //Act
    let resturantPage = await browser.newPage(ResturantPage,
                                              configJson.resturantUrl)
    //Assert
    await expect(resturantPage.retsurantIsVisible(100)).toBeVisible
  })
```
In our example you can see that in the part of the ‘Arrange’ we prepare the data and create a restaurant, then in the part of the ‘Act’  itself we enter the page in the ui and at the end in the comparison we actually ‘Assert’  that the restaurant was created in the ui.
# Properties of a manual test 
**Can be specific or general**
Manual tests can be tailored to specific areas or cover a wider range of functionalities, offering flexibility in their approach.
A tester can do a general test and enter general data and check the result and compare it to the desired result and can be specific and enter precise data and check the resulting result

**Can be exploratory**
Manual tests have the freedom to be exploratory, enabling testers to investigate the software dynamically and find unforeseen issues that may not have been anticipated.

**Takes into account the common sense of the tester**
Manual tests utilize the tester's common sense and intuition, enabling them to use their own knowledge and judgment during the evaluation of the software.
For example, if there is any change in the behavior of the application, a manual tester will be able to notice it and behave accordingly in the test

**Done by a real person**
Manual tests are carried out by actual individuals, bringing a human element to the testing process and allowing for subjective assessment and flexibility.
For example, a human tester can see if there are changes in the movements of elements in the application

**Mostly has some variance when executed**
Manual tests can vary in their execution due to the human factor, providing room for adaptability and the ability to explore different scenarios.
# Properties of an automatic test
**Very specific**
Automatic tests are designed to be highly specific, allowing for precise evaluation of particular functionalities or specific aspects of the software.

For example, if we have an e-commerce system and we have a procedure for purchasing a product, we will perform a test for each step in the process and not one test that checks all the processes

**What’s not written is not tested **
Automatic tests follow a "what's not written is not tested" principle, ensuring comprehensive coverage of predefined scenarios, such as an automated test for adding items to a cart and verifying that the correct quantity is added rather than an unintended quantity, From this you can understand that what we will check in our example is the amount of items in the cart and not the sum of the products for that matter.

**Code mistakes = broken test**
In automatic tests, code mistakes directly result in broken tests, as any errors or issues in the underlying test code can cause failures in the automated testing process.

For example, if we have a loop that ran a number of times on a certain process and inside the loop there is a variable that extracts data, if we do not reset it at the beginning of each iteration, that variable will receive the data from the previous iteration and thus we will actually get a code error that breaks our test

**Has no variance**
Automatic tests are consistent and reliable since they have little to no variance, allowing for dependable and reproducible execution that helps detect any deviations or unexpected behaviors in the software.
