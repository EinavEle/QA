# Annotations
Test annotations are used to deal with failures, flakiness, skip, focus, and tag tests. Annotations can be used on a single test or a group of tests, and they can be conditional based on some truthy condition.

There are several annotations available in Playwright, such as:

- `test.skip()`: Marks the test as irrelevant and not run by Playwright Test. It is used when the test is not applicable in some configurations.

- `test.fail()`: Marks the test as failing and ensures it does indeed fail when run by Playwright Test. In our best practice we will not use this annotation, we would prefer to write a correct assertion than to say that we know "that the test will fail".

- `test.fixme()`: Marks the test as failing and not run by Playwright Test. It is used when running the test is slow or crashes.

- `test.slow()`: Marks the test as slow and triples the test timeout.

- `test.only()`: run only that test.

You can group tests using test.describe(), which gives them a logical name and allows you to scope before/after hooks to the group.

Example:
```Playwright
import { test, expect } from '@playwright/test';

test.describe('My Test Suite', () => {
  test('should do something', async ({ page }) => {
    // test code here
  }).slow();

  test('should do something else', async ({ page, browserName }) => {
    test.skip(browserName === 'firefox', 'Still working on it');
    // test code here
  });
  
  test.only('should do something special', async ({ page }) => {
    // test code here
  });
  
  test.describe('My Sub-Suite', () => {
    test('should do something in the sub-suite', async ({ page }) => {
      // test code here
    });
  });
});
```

In this example, the first test is marked as slow, the second test is skipped if the `browserName` is firefox, the third test is focused, and there is a sub-suite with one test.

# Tags
- In Playwright, you can tag your tests with labels like `@fast`, `@slow`,`@bug` or any other label you choose.
- To run only tests with a specific tag, you can use the `--grep` flag followed by the tag name. For example, npx playwright test `--grep @fast will run only tests tagged with @fast`.
- If you want to skip tests with a certain tag, you can use the --grep-invert flag followed by the tag name. For example, npx playwright test `--grep-invert @slow` will skip tests tagged with `@slow`.

Here's an example of how you can tag your Playwright tests in TypeScript:

```TypeScript
import { test, expect } from '@playwright/test';

test('Test login page @fast', async ({ page }) => {
  // This test is tagged as @fast
  // ...
});

test('Test full report @slow', async ({ page }) => {
  // This test is tagged as @slow
  // ...
});
```