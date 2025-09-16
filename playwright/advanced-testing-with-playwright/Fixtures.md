# What are fixtures?
Fixtures in Playwright are like pre-made setups that you can use to get your tests ready. Think of them like a recipe for baking a cake - you have a list of ingredients and steps that you follow to get the cake ready to go into the oven.
In the same way, you can use a fixture to prepare the setup for your tests.

The primary benefit of fixtures is the ability to share resources among tests. This is particularly important to us because it allows us to avoid duplicating setup code and promotes resource sharing. Fixtures are especially valuable when multiple tests require the same setup, such as logging into a website or navigating to a specific page. Rather than rewriting the setup code for each individual test, we can define a fixture to handle it once and then reuse that fixture across all the tests. This approach significantly reduces code repetition and improves test efficiency.

Using fixtures makes your test code easier to read and less cluttered, because you don't have to repeat the same setup steps over and over. 
It also makes it easier to change your setup steps, because you only have to change the fixture code in one place, instead of changing every single test.

In Playwright, there are different types of fixtures available for setting up and managing resources in tests:

1. page: Represents an isolated page for each test run.
2. context: Provides an isolated browser context for each test run. The page fixture belongs to this context.
3. browser: Represents a shared browser instance across multiple tests, optimizing resource usage.
4. browserName: Gives the name of the browser currently running the test (chromium, firefox, or webkit).
5. request: Offers an isolated instance for making API requests and testing network-related functionalities.

These fixtures help streamline resource setup, isolation, and reuse in tests. Depending on your testing needs, you can select the appropriate fixtures to ensure efficient and reliable test execution.

For example:
```Playwright
import { chromium } from 'playwright';
import { test, expect, Browser, Page } from '@playwright/test'
// Define a fixture that launches a browser and navigates to a page
const launchBrowser = async (): Promise<{ browser: Browser, page: Page }> => {
    const browser = await chromium.launch();
    const page = await browser.newPage();
    await page.goto('https://the-internet.herokuapp.com/');
    return { browser, page };
};
// Use the fixture in a test
test.describe('My test suite', () => {
    let browser: Browser;
    let page: Page;

    test.beforeEach(async () => {
        ({ browser, page } = await launchBrowser());
    });

    test.afterEach(async () => {
        await browser.close();
    });

    test('My test', async () => {
        // Use the `page` object to interact with the page
        await page.locator('//a[text()="A/B Testing"]').click()
        const title = await page.locator
                           ('//h3[text()="A/B Test Variation 1"]').innerText()
        expect(title).toBe('A/B Test Variation 1');
    });
});
```
In the following code we can see how the fixture is defined as an object called launchBrowser and then in the tests it is used in order to enter any page that appears and do a title check test on it

# Dangers of Passing State
As we discussed before, some of the principles of automation are self-tests, so that information will not pass between tests and therefore passing state in fixtures can cause problems in your tests. 
Fixtures are supposed to be independent and not rely on any outside data, so when you pass in state, it can get confusing and make your tests act in unexpected ways.

For example, imagine you pass a user ID into a fixture that multiple tests use. If one of those tests changes something about the user data, it could mess up the other tests that use that same ID. 
This could lead to weird results, false positives, or false negatives, which can be frustrating and time-consuming to debug.

Also, if you change something about the state in one fixture, it might mean you have to change all the tests that use that fixture, which could be a lot of work and cause even more confusion.

So, it's best to try to keep your fixtures separate from any external data, and only use them to set up and tear down things specific to each test. 
If you need to share data between tests, it's better to use a shared resource like a database or API that can be accessed by each test on its own.
