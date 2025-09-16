Implement the auth setup for a site of your choice and write 3 tests that use this authenticated state

<details><summary>  
Click here to reveal the answer.  
</summary>

playwright.config

```Playwright 
{ defineConfig, devices } from '@playwright/test';
export default defineConfig({
  testDir: './tests',
  fullyParallel: false,
  retries: process.env.CI ? 2 : 0,
  workers: process.env.CI ? 1 : 1,
  reporter: 'allure-playwright',
  use: {
    viewport: { width: 1280, height: 1024 },
    trace: 'on',
    screenshot: 'only-on-failure',
    headless: false,
    video: 'on'
  },
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
  ],
});
```

auth.setup.ts

```Playwright
import { expect, test as setup } from '@playwright/test';
const authFile = 'playwright/.auth/user.json';
setup('authenticate', async ({ page }) => {
    // Perform authentication steps. Replace these actions with your own.
    await page.goto('https://www.saucedemo.com/');
    await
        page.locator('//input[@data-test="username"]').fill('standard_user');
    await page.locator('//input[@data-test="password"]').fill('secret_sauce');
    await page.locator('//input[@data-test="login-button"]').click();
    // Wait until the page receives the cookies.
    // Sometimes login flow sets cookies in the process of several redirects.
    // Wait for the final URL to ensure that the cookies are actually set.
    await page.waitForURL('https://www.saucedemo.com/inventory.html');
    // Alternatively, you can wait until the page reaches a state where all
       cookies are set.
    await expect(page.locator('//div[@class="app_logo"]')).toBeVisible();
    // End of authentication steps.
    await page.context().storageState({ path: authFile });
});
```

auth.spec.ts

```Playwright
import { expect, test } from '@playwright/test';
test.only('test', async ({ page }) => {
    // page is authenticated
    const url = page.url();
    const pageTitle = await page.title();
    expect(url).toContain('inventory.html');
    expect(pageTitle).toEqual('Swag Labs');
});
```

</details>