# Intro
Most of the time we expect our tests to simply pass and cause no problems.
But alas, tests fail sometimes.
We always try to make our test  failures meaningful and informative but what if the test's status, pass or fail, is wrong?
Well, this is a very bad thing for our tests.
Remember, the goal of automation is to provide certainty and quality, if you cannot trust the results of our tests, we are in a huge problem.

There are two types of wrong test results:
# False positive
A false positive occurs when a test case incorrectly reports a failure or identifies an issue that does not actually exist in the system under test. 
It indicates a situation where the automation test incorrectly indicates a problem or failure when, in fact, the functionality being tested is working correctly. 
False positives can occur due to factors such as flawed test scripts, unreliable test data, or issues with the test environment. 
It is important to minimize false positives in automation testing to ensure accurate and reliable test results.

For example, a test might say a button on a website is broken when it's actually working correctly. This can happen because of mistakes in the test or using the wrong data. To make sure our tests are reliable, we need to minimize false positives.

What is the solution?
**See your tests fail!**
When developing a new test, change the final validation to an unexpected result, and see the error you get.
This way, you know that the test actually checks what you intended to check.
# False negative
 A false negative refers to a scenario where a test case incorrectly indicates a pass or success when, in reality, there is an issue or failure in the system being tested. It means that the automation test fails to detect an actual problem or issue that exists. False negatives can occur due to factors such as incomplete test coverage, inadequate assertions, or errors in the test implementation. Minimizing false negatives is important to ensure comprehensive and accurate testing, as they can lead to undetected defects and compromise the overall quality of the software.
For example, a test might pass and say a feature is working correctly, even though there's a bug. This can happen if the test doesn't check all the necessary things or if there are mistakes in the test setup

What is the solution?
**Fight for stability!**
What is stability?
Stability refers to the ability of automated tests to consistently produce reliable and accurate results over multiple test runs, We will expand on this later.


