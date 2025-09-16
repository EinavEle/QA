# What is Authentication?
Authentication is verifying someone's identity to access something. 
It's like showing an ID. You provide a username and password to prove authorization. 
Tests can use pre-authenticated states, avoiding authentication in each test and speeding up execution. 

# When to use?
Imagine that all your tests are running simultaneously using the same account, but none of them interfere with each other, This is an excellent invitation to come and create Authentication once in a way that we will learn later.

# When not to use?
Your tests mess with the stuff on the server-side. 
For example, one test checks how the settings page looks, while the other one is tweaking some settings, and you're running all tests at the same time. 
In this kind of situation, tests gotta use different accounts.
Also, your login stuff is tied to the browser you're using.

# How to? 
The next part is copied in Playwright's documentation, you can see the full process there:
https://playwright.dev/docs/auth

Details

Create auth.setup.ts that will prepare authenticated browser state for all other tests.
```Playwright
// auth.setup.ts
import { expect, test as setup } from '@playwright/test';

const authFile = 'playwright/.auth/user.json';

setup('authenticate', async ({ page }) => {
    // Perform authentication steps. Replace these actions with your own.
    await page.goto('https://practicetestautomation.com/practice-test-login/');
    await page.locator('//input[@name="username"]').fill('student');
    await page.locator('//input[@name="password"]').fill('Password123');
    await page.locator('//button[@id="submit"]').click();
    // Wait until the page receives the cookies.
    //
    // Sometimes login flow sets cookies in the process of several redirects.
    // Wait for the final URL to ensure that the cookies are actually set.
    await page.waitForURL('https://github.com/');
    // Alternatively, you can wait until the page reaches a state where all cookies are set.
    await expect(page.locator('//h1[@class="post-title"]')).toBeVisible();

    // End of authentication steps.

    await page.context().storageState({ path: authFile });
});
```

Create a new setup project in the config and declare it as a dependency for all your testing projects. This project will always run and authenticate before all the tests. 
All testing projects should use the authenticated state as storageState.

```Playwright
// playwright.config.ts
import { defineConfig, devices } from '@playwright/test';

export default defineConfig({
  projects: [
    // Setup project
    { name: 'setup', testMatch: /.*\.setup\.ts/ },

    {
      name: 'chromium',
      use: {
        ...devices['Desktop Chrome'],
        // Use prepared auth state.
        storageState: 'playwright/.auth/user.json',
      },
      dependencies: ['setup'],
    },

    {
      name: 'firefox',
      use: {
        ...devices['Desktop Firefox'],
        // Use prepared auth state.
        storageState: 'playwright/.auth/user.json',
      },
      dependencies: ['setup'],
    },
  ],
});
```

Tests start already authenticated because we specified storageState in the config.

```Playwright
// tests/example.spec.ts
import { test } from '@playwright/test';

test('test', async ({ page }) => {
  // page is authenticated
});
```
