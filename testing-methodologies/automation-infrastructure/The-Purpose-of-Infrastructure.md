# How tests look without infrastructure
Examples of Tests Without Infrastructure:

- Unreliable Execution: Tests may fail due to inconsistent or unstable testing environments, leading to unreliable results.
- Limited Test Coverage: Without infrastructure, tests may be restricted to specific platforms or configurations, resulting in limited coverage.
- Inefficient Test Data Handling: Lack of infrastructure support makes managing test data challenging, leading to inconsistencies or inadequate coverage.
- Inconsistent Tool Integration: Testing tools may not integrate seamlessly, causing compatibility issues or limitations in functionality.
- Non-Scalable Testing: Without proper infrastructure, it becomes difficult to scale automation testing for large-scale projects or applications.
```java
test('should search for Playwright', async () => {
    await page.goto('https://google.com');
    const input = page.locator('input[name="q"]');
    await input.fill('Playwright');
    await input.press('Enter');
    expect(await page.title()).toContain('Playwright');
  })
```
# What’s wrong with script tests
**No code reuse**
Script tests often lack modularity, leading to duplicate code and an inefficient testing process. 
This makes it difficult to maintain and update the tests.
**Complex code everywhere**
 Script tests tend to have complex and lengthy code, making them hard to understand and maintain. 
This complexity can lead to errors and make it challenging to debug issues.
**Lots of code**
Script tests often involve writing a significant amount of code to cover different test scenarios. 
This can result in a large codebase, making it difficult to manage and navigate through the tests.
**Not resistant to changes**
Script tests are typically tightly coupled with the application's implementation details. 
As a result, any changes in the application's code or user interface can break the tests, requiring significant rework.
**Hard to maintain**
Due to their complex and lengthy nature, script tests can be difficult to maintain. 
As the application evolves, the tests need to be updated to reflect the changes, which can be time-consuming and error-prone.
**Reveals infrastructure** 
Script tests often expose the underlying infrastructure details, such as the automation tools (e.g., Selenium, Playwright) or the database. 
This can create dependencies and make the tests more fragile to changes in the infrastructure.
# What do we get with a good infra
A good infrastructure in automation testing offers several benefits:
**Readability**
The code is well-structured and organized, making it easy to read and understand.
**Division of responsibilities**
Each layer of the infrastructure has clear responsibilities, leading to better separation of concerns and maintainability.
**Each layer is easy to use**
The infrastructure provides user-friendly interfaces and tools, making it easy for testers to work with.
**Change resistance**
The infrastructure is designed to handle changes in the application smoothly, reducing the need for extensive modifications.
**Maintainable**
The infrastructure is built with maintainability in mind, allowing for easy updates, enhancements, and bug fixes.
**Code reuse**
The infrastructure promotes code reuse, allowing testers to leverage existing components and libraries for efficient test development.
**Stable**
The infrastructure ensures stability in test execution, minimizing flakiness and false positives.

**Easy to debug**
The infrastructure provides robust debugging capabilities, enabling testers to identify and resolve issues quickly.
**Enables easy infra switches**
The infrastructure is designed to support easy switching between different tools or technologies, providing flexibility and adaptability.
**Readable and easy to learn**
The infrastructure is designed with simplicity and clarity, making it accessible for new team members to understand and learn.
**Scalability**
The infrastructure can handle a growing number of tests and accommodate the needs of larger projects or applications.
