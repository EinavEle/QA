# Guidelines

### API & UI
- Your tests should include api calls for data preparation.
- Actions under tests should be performed in the UI
- Validations should be done in the UI
- You can add extra validations via API

### AAA
- You should adhere to the Arrange, Act, Assert structure

### Test isolation (independence)
- All tests should be independent and not affect or be affected by other tests

### Parallelism
- Your tests should run in parallel

### Assertions
- Use the most accurate assertions

### Reporting
- Test results should be presented using allure report

### infrastructure
- Code should be structured in layers (infra, logic, tests)
- Selenium should not be revealed to the tests layer
- Use POM

### BDD
- Make sure to use the correct language &wording in your cucumber steps

### GIT
- Use pull requests and have code reviews
- Use informative commit messages
 
### Stability
- Make sure your tests pass consistently, no flaky tests!
- Tests may fail if there are actual bugs in the system