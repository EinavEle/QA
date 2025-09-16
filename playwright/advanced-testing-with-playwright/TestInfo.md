# Using test info
In Playwright, testInfo is an object that provides information about the currently running test. 
It is available as a property of the PlaywrightTestParameters object that is passed to each test function.

The testInfo object provides the following information:

- `title`: the title of the test.
- `file`: the file path of the test.
- `repeatEachIndex`: the index of the current iteration of a repeated test.
- `skip`: a boolean indicating whether the test is marked as skipped.
- `expectedStatus`: the expected status of the test (if provided).
- `annotations`: an array of annotations (tags) applied to the test.

Here's an example of how you can access the testInfo object in a Playwright test:

```Playwright
import { test, expect } from '@playwright/test';

test('Test example', async ({ page}, testInfo) => {
  console.log(`Runing test "${testInfo.title}" from file" ${testInfo.file}"`);
  console.log(`Test annotations: ${testInfo.annotations}`);
  console.log(`Expected status: ${testInfo.expectedStatus}`);
  console.log(`Is test skipped? ${testInfo.skip}`);
  console.log(`Current repeat index: ${testInfo.repeatEachIndex}`);
  
  // Test code here...
});
```

In this example, we are logging various properties of the testInfo object to the console for debugging purposes. 
You can use these properties to customize the behavior of your test based on its metadata.