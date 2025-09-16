# Intro
While the purpose of our tests is to ensure the quality of the product and they should most of the time pass, the real value of automated tests comes when they fail!
When a test fails we get a signal that something is wrong with our program.
Then we can investigate and fix it.
# There are two main types of failures
**Validation failure - Assertion Exception**
Validation failure, also known as an assertion exception, happens in automated tests when a specific condition or expected outcome does not match the actual result, highlighting a test failure that requires investigation and resolution.

**Setup failure - any other error**
Setup failure in automated tests happens when the required setup steps encounter errors or are not executed correctly, while any other error refers to unexpected issues or runtime errors that occur during the testing process, requiring investigation and resolution.
# Reporting different types of errors and why it matters



When investigating failed tests, assertion errors tell us that the test result was not as expected. This means that the test was executed fully but failed.
On the other hand, if a setup error was thrown, the test wasn’t really executed so we can’t determine the result.
In a report, these two errors should be displayed differently, since one is probably a bug, and the other is either a test error or a temporary environment issue.
