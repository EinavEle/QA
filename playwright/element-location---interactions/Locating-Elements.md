# What is the Locator Class?
The Locator class is a tool that helps developers find elements on a web page.

It provides a simple way to identify and interact with various types of web elements such as buttons, links, inputs, and other user interface elements.

Some key features of the Locator class include:
- It can be used to locate elements by various attributes such as ID, class, name, and text content.
- It can also be used to locate elements using complex selectors such as XPath and CSS selectors.
- It provides a variety of methods to interact with elements such as clicking, typing, and selecting options from drop-down menus.
- It supports waiting for elements to appear or become visible before interacting with them.

Here's an example of using the Locator class in TypeScript to locate a button with the text "Submit":
```Playwright
test('What is the Locator Class?', async () => {
        await page.goto('https://google.com');
        const submitButton = await page.locator(
                                       '//input[@value="I'm Feeling Lucky"]');
        await submitButton.click();
    })
```
We use the page.locator method to find a button element with the text "Submit". 
Finally, we call the click method on the resulting locator object to simulate a click on the button.


# Locator Best Practices
### Locators as class members
It's often useful to declare Locators as class members so that they can be reused across multiple methods. This can help keep your code organized and reduce duplication.

Example:
```Playwrightimport { Locator, Page } from 'playwright';

export class LoginPage {
    private readonly userNameInput: Locator;
    private readonly passwordInput: Locator;
    private readonly loginButton: Locator;

    constructor(page: Page) {
        this.userNameInput =
             page.locator("//input[contains(@data-test,'username')]");
        this.passwordInput =
              page.locator("//input[contains(@data-test,'password')]");
        this.loginButton =
              page.locator("//input[contains(@data-test,'login-button')]");
    }

    async login(userName: string, password: string) {
        await this.userNameInput.type(userName);
        await this.passwordInput.type(password);
        await this.loginButton.click();
    }
}

```
### Chaining Locators
You can combine methods that create a locator, such as page.getByText() or locator.getByRole(), to focus on a specific area of the page.

Here's an example of using Chaining Locators:
```Playwright
  test('Chaining Locators', async () => {
        const browser = await chromium.launch();
        const page = await browser.newPage();
        await page.goto('https://www.example.com');

        // Chaining locators to find the "Sign In" button
        const signInButton = 
                       await page.locator('button').locator('text=Sign In');
        await signInButton.click();
        await browser.close();
    })
```
In this example, we first launch a new Chromium browser and navigate to the example.com webpage. 
After that, we use a "locator" to locate all our buttons on the page, and then we use another “locator” to find the specific button we need.

### Helper Locators - “getBy”
Using the ״getBy״ methods can be really helpful in improving our locators, especially when we're dealing with lots of elements.

#### getByText

Allows locating elements that contain given text.

For example:
```Playwright
<div>Hello <span>world</span></div>
<div>Hello</div>
```

You can locate by text substring, exact string, or a regular expression:
```Playwright
// Matches <span>
page.getByText('world')

// Matches first <div>
page.getByText('Hello world')

// Matches second <div>
page.getByText('Hello', { exact: true })

// Matches both <div>s
page.getByText(/Hello/)

// Matches second <div>
page.getByText(/^hello$/i)
```
#### getByLabel
Allows locating input elements by the text of the associated <label> or aria-labelledby element, or by the aria-label attribute.

```Playwright
<input aria-label="Username">
<label for="password-input">Password:</label>
<input id="password-input">
```
```Playwright
await page.locator('input').getByLabel('Username').fill('john');
await page.locator('input').getByLabel('Password').fill('secret');
```
#### And more…
To learn about other methods for using getBy, you can access the Playwright documentation
https://playwright.dev/docs/api/class-framelocator#methods

### Dynamic Locators
Dynamic locators adapt to changes in web pages, making automated tests easier to maintain. Unlike static locators, they find web elements that may change dynamically. They are a reliable way to identify web elements, based on user interactions or application state.

Here's an example of using dynamic locators :
```Playwright
  test('Dynamic Locators', async () => {
        const MULTI_SELECTOR = (dataTest: string) =>
                              `"//input[contains(@data-test,'${dataTest}')]")`
        await page.goto('https://www.saucedemo.com/');
        await page.locator(MULTI_SELECTOR('username')).fill('standard_user');
        await page.locator(MULTI_SELECTOR('password')).fill('secret_sauce');
        await page.locator(MULTI_SELECTOR('login-button')).click();
        const url = page.url();
        const pageTitle = await page.title();
        expect(url).toContain('inventory.html');
        expect(pageTitle).toEqual('Swag Labs');
    })
```
In this example, we first navigate to a web page and define a dynamic locator for other fields to fill them .
 We then use the click() method to simulate a user clicking on the link.

Next, we define a dynamic locator for a form on the page, using a function that returns a string selector. We then use the fill() method to populate the form fields with some sample data.

Overall, dynamic locators can help make your Playwright tests more flexible and resilient to changes in the web page structure.

### Strictness
The concept of strictness in Playwright means that when you search for an element using a locator, your locator should match one, and only one, element, unless you actually meant to find multiple elements.
. Here's what you need to know:
- If you try to use a locator to do something with a specific element on a webpage, but there are multiple elements that match the locator, it won't work and you'll get an error. 
For example:
```Playwright
Error: page.waitForSelector: Error: strict mode violation: locator('xpath=//input') resolved to 3 elements:
    1) <input value="" type="text" id="user-name" 
                       name="user-n.../> aka locator('[data-test="username"]')
    2) <input value="" id="password" type="password" 
                       name="pas.../> aka locator('[data-test="password"]')
    3) <input type="submit" value="Login" id="login-button" 
                       na.../> aka locator('[data-test="login-button"]')
```

For example, this code will throw an error if there are multiple buttons on the page:
**Throws an error if more than one**
```await page.getByRole('button').click();```
- However, Playwright is smarter than that. If you need to do something with multiple elements that match a locator, it can handle it just fine. 

For example, this code will work even if there are multiple buttons on the page:
**Works fine with multiple elements**
```await page.getByRole('button').count();```

If you really need to use a locator that might match multiple elements, you can tell Playwright which element to use with locator.first(), locator.last(), and locator.nth()(We will talk about them right away). 

But be careful, because if the page changes, Playwright might end up clicking on the wrong thing. It's usually better to follow best practices and create a locator that uniquely identifies the element you want to work with.

# Locator Functionality
### Nth
The nth function allows you to select an element based on its position in a set of matched elements, using a zero-based index.
- You can use the nth function with the first, last, or a specific index value.
- The nth function is particularly useful when you need to select a specific element from a list or table that has no unique identifier.
- You can use the nth-child() or nth-of-type() CSS selector functions with the page.locator() or element.locator() methods to create a dynamic locator that targets a specific element based on its position.

Here's an example of using the nth functionality:

```Playwright
   test('Nth', async () => {
        const page = await browser.newPage();
        await page.goto('https://www.nba.com/stats');
        // Find all links on the page
        const links = page.locator('a');
        // Click the second link
        await links.nth(1).click();
    })  
```
In this example, we select the second  link on the page using the nth.
 We then click on the resulting element using the click() method.

Overall, the nth functionality in Playwright locators allows you to select elements based on their position in a set of matched elements, making it easier to target specific elements in lists, tables, and other types of content.

### Count
The count functionality in Playwright locators allows you to find the number of matched elements for a given selector.
- You can use the count functionality with the page.locator() or element.locator() methods to create a dynamic locator that returns the number of matched elements.
- The count functionality is particularly useful when you need to verify the number of elements that match a certain selector, such as checking that a list or table has a certain number of rows or columns.

Here's an example of using the count functionality:

```Playwright
  test('Count', async () => {
        const browser = await chromium.launch();
        const page = await browser.newPage();
        await page.goto('https://www.nba.com/stats');
        // Count the number of links on the page
        const linkCount = await page.locator('a').count();
        // Count the number of rows in a table
        const rowCount = await page.locator('table tr').count();
        console.log(
        `There are ${linkCount} links and ${rowCount} rows on the page.`);
        await browser.close();
    })
```

In this example, we use the count() method with the page.locator() method to count the number of links and rows on the page. 
We can then log this information to the console.

Overall, the count functionality in Playwright locators allows you to quickly and easily get the number of matched elements for a given selector, making it easier to verify the number of elements in lists, tables, and other types of content.

### Filter
The filter functionality in Playwright locators allows you to refine the selection of elements based on additional criteria.
- You can use the filter functionality with the page.locator() or element.locator() methods to create a dynamic locator that selects elements based on a specified condition.
- The filter functionality is particularly useful when you need to select only certain elements that match a specific criteria, such as selecting only the elements that have a certain class name, or only the elements that contain certain text.

Here's an example of using the filter functionality:

```Playwright
  test('Filter', async () => {
        const browser = await chromium.launch();
        const page = await browser.newPage();
        await page.goto('https://www.nba.com/stats');
        // Find all locators with text "Game" in "ul"
        const gameSpan = await page.locator("//ul[@id='nav-ul']")
                                    .filter({ hasText: 'Games' }).count();
        console.log(`Num of Game Span : ${gameSpan}.`);
        await browser.close();
    })
```
In this example, we use the filter() method with the page.locator() method to refine the selection of tags with text  on the page. 

Overall, the filter functionality in Playwright locators allows you to refine the selection of elements based on additional criteria, making it easier to select only the elements that you need in your tests.

# Element Handles
Element Handles are a mechanism that allows developers to interact with web elements. 

Here's what you need to know about them:

- Element Handles are objects that represent web elements on a page. They are returned by Playwright methods such as page.$, page.$$, element.$, and element.$$.
- The benefit of using Element Handles is that they provide a way to interact with web elements without needing to re-query the page each time an action is performed. This can lead to faster and more stable automation scripts.

Here's an example:
```Playwright
  test('Element Handles', async () => {
        const browser = await chromium.launch();
        const page = await browser.newPage();
        await page.goto('https://www.nba.com/stats');
        // Use an Element Handle to click a link
        const linkHandle = await page.$('a');
        await linkHandle!.click();
        // Use an Element Handle to type into an input
        const inputHandle = await page.$('input');
        await inputHandle!.type('Hello, world!');
        await browser.close();
    })
```
In the example above, linkHandle and inputHandle are both Element Handles. They are used to interact with the first link and first input on the page, respectively.

### Why not use them?
ElementHandles are bound to elements on the page. Which means that the moment the element is changed in the DOM, for any reason, it is no longer bound to the element handle object in our code.
Any action using this element will result in an ElementDoesNotExist error.
So, while using ElementHandles can supposedly save you time by not querying the page more than once, it will definitely cost you with volatile and unstable tests.

The bottom line is **don’t use it unless absolutely necessary.**