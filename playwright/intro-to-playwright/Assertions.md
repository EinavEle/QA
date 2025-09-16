# Expect
Expect in Playwright:
- Expect is a method used to define assertions in Playwright tests.
- Expect provides a more readable syntax for writing assertions, using natural language phrases to describe the expected behavior.     

Example:

```Playwright
// Verify that an element with the id 'myElement' exists
const myElement = await page.locator('#myElement');
expect(myElement).toBeTruthy();
// Verify that an element with the class 'myClass' has text 'Hello World'
const myClassElement = await page.locator('.myClass');
const text = await myClassElement.textContent();
expect(text).toBe('Hello World');
// Verify that a button with the text 'Click Me' can be clicked
const clickMeButton = await page.locator('button:text("Click Me")');
await clickMeButton.click();
expect(await page.url()).toBe('https://example.com/success');

```
Some different options for using Expect:

- expect.toBeTruthy(): verifies that a value is truthy
```Playwright

// This test passes because the value is truthy
const value = "hello";
expect(value).toBeTruthy();

// This test fails because the value is falsy
const otherValue = null;
expect(otherValue).toBeTruthy(); // Throws an error

```
- expect.toBeFalsy(): verifies that a value is falsy
```Playwright
// This test passes because the value is falsy
const value = null;
expect(value).toBeFalsy();

// This test fails because the value is truthy
const otherValue = "hello";
expect(otherValue).toBeFalsy(); // Throws an error
```
- expect.toBeNull(): verifies that a value is null
```Playwright
// This test passes because the value is null
const value = null;
expect(value).toBeNull();

// This test fails because the value is not null
const otherValue = "hello";
expect(otherValue).toBeNull(); // Throws an error
```
- expect.toContain(): verifies that a string contains a specific substring
```Playwright
// This test passes because the array contains the specified element
const arr = [1, 2, 3];
expect(arr).toContain(2);

// This test fails because the array does not contain the specified element
const otherArr = [4, 5, 6];
expect(otherArr).toContain(2); // Throws an error
```
- expect.toMatch(): verifies that a string matches a specific regular expression
```Playwright
// This test passes because the string matches the regular expression
const str = "Hello, world!";
expect(str).toMatch(/world/);

// This test fails because the string does not match the regular expression
const otherStr = "Goodbye, world!";
expect(otherStr).toMatch(/hello/); // Throws an error
```
Beyond what we have presented to you, there are many more options "toBe...".
You can read about them in the following link:
https://playwright.dev/docs/api/class-genericassertions#generic-assertions-to-be

# Web-first assertions
Assertions are a way to check if the expected and actual results match in testing. When using Playwright, it's recommended to use web first assertions. 
This means that Playwright will wait until the expected condition is met before checking the result. 

For example, if you want to check if an alert message appears after clicking a button, you can use the toBeVisible() assertion. 
This assertion will wait until the message is visible before checking it.

It's important not to use manual assertions that don't include the await expect() syntax. This means that the test won't wait for the result and will just return immediately. Here's an example of what not to do:
```Playwright
expect(await page.getByText('welcome').isVisible()).toBe(true);
```
Instead, you should use web first assertions like toBeVisible() with the await expect() syntax, like this:

```Playwright
 await expect(page.getByText('welcome')).toBeVisible();
```

# Assertion timeout & retries
- Assertion timeout refers to the maximum time that Playwright will wait for an assertion to pass before failing the test.
- Assertion timeouts are important to ensure that tests don't get stuck waiting indefinitely for an assertion that will never pass.
- In Playwright, the default assertion timeout is 30 seconds, but this can be customized using the timeout option when defining assertions.

Example:
```Playwright
// Set a custom assertion timeout of 10 seconds
await expect(page).toHaveSelector('#myElement', { timeout: 10000 });
```
Assertion retries in Playwright:
- Assertion retries refer to the number of times Playwright will attempt to re-run a failing assertion before failing the test.
- Assertion retries can be useful in cases where a test failure is due to a flaky network connection or timing issues.
- In Playwright, the default number of assertion retries is 0, meaning that the assertion will only be run once.

Example:
```Playwright
// Set a custom number of assertion retries to 3
await expect(page).toHaveSelector('#myElement', { retry: 3 });
```

Combining assertion timeout and retries in Playwright:

Assertion timeout and retries can be combined to provide a more robust and reliable test suite.
For example, setting a longer timeout and a higher number of retries can help ensure that tests pass even in flaky network conditions.

Example:
```Playwright
// Set a custom assertion timeout of 30 seconds and 3 retries
await expect(page).toHaveSelector('#myElement', { timeout: 30000, retry: 3 });
```

Note: it's important to use assertion timeout and retries judiciously, as setting them too high can lead to slow and unreliable test runs. 
It's usually best to start with the default settings and adjust as needed based on the specific requirements of your tests.

# Soft assertions
- Soft assertions are a type of assertion in automated testing that allow the test to continue running even if an assertion fails.
- Unlike regular (or "hard") assertions, which cause the test to immediately fail and stop running, soft assertions only log the failure and continue running the test.
- Soft assertions can be useful in cases where a test failure doesn't necessarily mean that the test has failed completely, and where it's important to collect multiple pieces of information about the test's behavior.

Example:
```Playwright
// Make a few checks that will not stop the test when failed...
await expect.soft(page.getByTestId('status')).toHaveText('Success');
await expect.soft(page.getByTestId('eta')).toHaveText('1 day');

// Avoid running further if there were soft assertion failures.
expect(test.info().errors).toHaveLength(0);
```

In the example above, we're using soft assertions to check the state of multiple elements on the page. 
If any of the assertions fail, we set a hasError flag to true, but we continue running the test regardless.
After all of the assertions have been run, we log the final result of the test based on the hasError flag. 
This allows us to collect multiple pieces of information about the test's behavior, without immediately failing the test if any of the assertions fail.

# Custom messages
 The custom-message is an optional parameter that you can use with assertions to provide a custom error message when the assertion fails. 

The custom message will be included in the error output to help you diagnose the cause of the failure.

Here's an example of how you can use custom-message with an assertion:

```Playwright
test('custom message example', async ({ page }) => {
  const title = await page.title();
  const expectedTitle = 'Example Title';
  expect(title, `Title should be "${expectedTitle}"`).toBe(expectedTitle);
});
```
In this example, we are using the expect assertion to check that the page title is equal to the expected title. 

We are also providing a custom message as the second argument to expect using the custom-message syntax. 

If the assertion fails, the custom message will be included in the error output to help us diagnose the cause of the failure.

Custom messages can be particularly useful when you are testing complex scenarios and need to provide additional context to help you debug failing tests. 

By providing a clear and concise message, you can make it easier to understand what went wrong and how to fix it.