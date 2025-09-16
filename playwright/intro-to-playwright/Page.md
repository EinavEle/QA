- The Page class in Playwright represents a single web page in a browser.
- It provides methods to interact with the page's HTML elements, such as filling out forms, clicking buttons, and navigating to other pages.
- You can also use the Page class to interact with the browser itself, such as taking screenshots, emulating devices, and intercepting network requests.

Here's an example of how to create a Page instance and use some of its basic functionality :

```Playwright
import { chromium } from 'playwright';
(async () => {
  // Launch a new browser instance
  const browser = await chromium.launch();
  // Create a new browser context and page
  const context = await browser.newContext();
  const page = await context.newPage();
  // Navigate to a website
  await page.goto('https://the-internet.herokuapp.com/add_remove_elements/');
  // Get the page title
  const title = await page.title();
  console.log(`The page title is: ${title}`);
  // Get the page URL
  const url = await page.url();
  console.log(`The page URL is: ${url}`);
  // declare element and click it
  const button = await page.locator('button');
  await button.click();
  // Take a screenshot of the page
  await page.screenshot({ path: 'example.png' });
  // Close the browser
  await browser.close();
})();
```
In this example, we launch a new instance of Chromium using chromium.launch(). 
We then create a new Browser Context and Page instance using browser.newContext() and context.newPage(), respectively.
We navigate to a website using page.goto('https://www.example.com') and retrieve the page's title and URL using page.title() and page.url(), respectively.

We then wait for an element to appear using page.waitForSelector('button') and click it using button.click().
Finally, we take a screenshot of the page using page.screenshot() and close the browser using browser.close().

# Locator
- The Locator class in Playwright is used to find and interact with elements on a web page.
- Locator provides methods to interact with the element, such as clicking it, filling in form fields, and retrieving its text content.
Here's an example of how to use Locator to interact with a button element:
```Playwright
import { chromium } from 'playwright';
(async () => {
  // Launch a new browser instance
  const browser = await chromium.launch();
  // Create a new browser context and page
  const context = await browser.newContext();
  const page = await context.newPage();
  // Navigate to a website
  await page.goto('https://www.example.com');
  // Find and click a button using a CSS selector
  const button = await page.locator('button');
  await button.click();
  // Find a form field and fill it in
  const input = await page.locator('#search-box');
  await input.fill('test search');
  // Get the text content of an element
  const header = await page.locator('h1');
  const textContent = await header.textContent();
  console.log(`The header text is: ${textContent}`);
  // Close the browser
  await browser.close();
})();

```
In this example, we launch a new instance of Chromium using chromium.launch().
- We then create a new Browser Context and Page instance using browser.newContext() and context.newPage(), respectively.
- We navigate to a website using page.goto('https://www.example.com') and find a button element using page.locator('button'). 
- We then click the button using button.click().
- We find a form field element using page.locator('#search-box') and fill it in using input.fill('test search').
- Finally, we find a header element using page.locator('h1') and retrieve its text content using header.textContent(). We log the text content to the console.
- We close the browser using browser.close().