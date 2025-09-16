# Different timeouts in Playwright 
Playwright Test has various configurable timeouts, including test timeouts, expect timeouts, action timeouts, navigation timeouts, global timeouts, and timeouts for hooks and fixtures. 

Here's a summary:
- Test timeout: The timeout for each test, including test hooks and fixtures.
 The default is 30 seconds. 
You can set it in the configuration 
```config = { timeout: 60000 }```
 or override it for a single test using 
```test.setTimeout(120000)```.

- Expect timeout: The timeout for each assertion. 
The default is 5 seconds. 
You can set it in the configuration
 ```config = { expect: { timeout: 10000 } }```
or override it for a single assertion using 
```expect(locator).toHaveText({ timeout: 10000 })```.

- Action timeout: The timeout for each action. 
There is no default timeout.
You can set it in the configuration 
```config = { use:{actionTimeout: 10000 }}```
 or override it for a single action using 
```locator.click({ timeout: 10000 })```.

- Navigation timeout: The timeout for each navigation action.
There is no default timeout. 
You can set it in the configuration
 ```config = { use: { navigationTimeout: 30000 } }```
 or override it for a single action
 ```using page.goto('/', { timeout: 30000 })```.

- Global timeout: The timeout for the entire test run.
There is no default timeout.
You can set it in the configuration using
 ```config = { globalTimeout: 60*60*1000 }```.

- Hook and fixture timeout: The timeout for hooks and fixtures. 
The default is 30 seconds. 
You can set it in the configuration or override it for a single hook or fixture using test.setTimeout or scope: 'test', timeout: 30000.

For example:
```Playwright
import { defineConfig } from '@playwright/test';
export default defineConfig({
  timeout: 60000,
  expect: {
    timeout: 10000
  },
  use: {
    actionTimeout: 10000,
    navigationTimeout: 30000
  },
  globalTimeout: 60*60*1000
});

test('example', async ({ page }) => {
  test.setTimeout(120000);
  expect(locator).toBeVisible({ timeout: 10000 });
  locator.click({ timeout: 10000 });
  page.goto('/', { timeout: 30000 });
  testInfo.setTimeout(testInfo.timeout + 30000);
  await expect(page.getByRole('button')).toHaveText('Sign in', { timeout: 10000 });
  await page.goto('https://playwright.dev', { timeout: 30000 });
});
```
