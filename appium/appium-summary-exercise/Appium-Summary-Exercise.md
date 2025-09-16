In these exercises we will develop automation infrastructure, and implement all kinds of tests.

We will use best practices of test automation and of the tools we learned.

Develop at least 15 tests of as many different styles as possible

We will be testing the following App:
<a href="https://www.apkfollow.com/download/apks_new_com.claudivan.taskagenda_2023-07-06.apk/" download>Claudivan Taskagenda</a>

**AAA**
- You should adhere to the Arrange, Act, Assert structure

**Test isolation (independence)**
All tests should be independent and not affect or be affected by other tests

**Parallelism**
- Your tests should run in parallel

**Assertions**
- Use the most accurate assertions

**Reporting**
- Test results should be presented using allure report

**Infrastructure**
- Code should be structured in layers (infra, logic, tests)
- Selenium should not be revealed to the tests layer
- Use POM

**GIT**
- Use pull requests and have code reviews
- Use informative commit messages

**Stability**
- Make sure your tests pass consistently, no flaky tests!
- Tests may fail if there are actual bugs in the system
