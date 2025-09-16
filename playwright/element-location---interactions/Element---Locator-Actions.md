# Element Actions
### selectOption
 The "Select Option" is used to interact with dropdown menus or other elements that require selecting an option from a list.

Here is an example of using the select function:
```Playwright
test('Select Action', async () => {
        await page.goto('https://www.saucedemo.com/');
        loginPage = new LoginPage(page);
        await loginPage.login('standard_user', 'secret_sauce');
        // Select the first option from a dropdown element with data-test "product_sort_container"
        await page.locator("//select[@data-test='product_sort_container']")
                  .selectOption('Name (A to Z)');
    })
```
In this example, we first navigate to a web page and make a login action.
Then use the select function to select the first option from a dropdown element with a data-test of "product_sort_container". 

### Check
The Check Action in Playwright is used to select a checkbox or radio button element in a web page. 
It is a function that can be called on a Page or ElementHandle object to interact with the element.

Here is an example of using the check function:
```Playwright
 test('Check Action',async () => {
        const browser = await chromium.launch();
        const page = await browser.newPage();
        await page.goto('https://www.example.com');
        // Check a checkbox with the id "my-checkbox"
        await page.locator('#my-checkbox').check();
        await browser.close();
    })
```
In this example, we first launch a Chromium browser instance and navigate to a web page. We then use the Check Action to select a checkbox element with an ID of "my-checkbox". Finally, we close the browser.

### SetInputFiles
The SetInputFiles Action is used to Upload file or multiple files into `<input type=file>`.

Here is an example of using the check function:
```Playwright
test('setInputFiles Action', async () => {
        // Select one file
        await page.locator("//input[@id='Upload file']")
                  .setInputFiles('myfile.pdf');

        // Select multiple files
        await page.locator("//input[@id='Upload file']")
                  .setInputFiles(['file1.txt', 'file2.txt']);

        // Remove all the selected files
        await page.locator("//input[@id='Upload file']").setInputFiles([]);

        // Upload buffer from memory
        await page.locator("//input[@id='Upload file']").setInputFiles({
            name: 'file.txt',
            mimeType: 'text/plain',
            buffer: Buffer.from('this is test')
        });
```

### DragTo
The DragTo Action in Playwright is used to simulate a drag-and-drop action between two elements in a web page.

Here is an example of using the dragTo function:
```Playwright
    test('DragTo Action', async () => {
            const source = page.locator('#source');
            const target = page.locator('#target');
            await source.dragTo(target);
            // or specify exact positions relative to the top-left corners of the elements:
            await source.dragTo(target, {
                sourcePosition: { x: 34, y: 7 },
                targetPosition: { x: 10, y: 20 },
            });
```
# Multi-Element Actions
### Strictness
Multi-Element Actions let you handle locators with multiple elements in Playwright. 
Use methods like locator.first(), locator.last(), and locator.nth() to select a specific element. However, these methods are risky when the page changes. It's best to use locators that identify the target element uniquely.

For example: 

```Playwright
   test('Strictness in multi element', async () => {
        const browser = await chromium.launch();
        const page = await browser.newPage();
        await page.goto('https://www.nba.com/stats');
        // Find all links on the page
        const links = page.locator('a');
        // Click the first link
        await links.first().click();
        // Click the last link
        await links.last().click();
        // Click the second link
        await links.nth(1).click();
    })
```
# Element Info
### InputValue
The InputValue function in Playwright is used to get the value from an input or textarea or select element in a web page. 

Here is an example of using the inputValue function:
```Playwright
  test('InputValue', async () => {
            const value = await page.locator('textbox').inputValue();
        })
```

### GetAttribute
The getAttribute function in Playwright is used to retrieve the value of a specific attribute of a web page element. 

Here is an example of using the getAttribute function:
```Playwright
        test('GetAttribute',async () => {
            const browser = await chromium.launch();
            const page = await browser.newPage();
            await page.goto('https://www.example.com');
            
            // Retrieve the value of the "href" attribute of 
               an anchor element with a class of "my-link"
            const myLinkLocator = page.locator("my-link");
            const hrefValue = await myLinkLocator.getAttribute('href');
           // Output: the value of the "href" attribute
            console.log(hrefValue);
            await browser.close();
        })
```
### “Is…”
The isVisible, isEnabled, isHidden, and isEditable functions in Playwright are used to check the state of a web page element.

- The isVisible function checks whether an element is visible on the web page.
- The isEnabled function checks whether an element is enabled and can be interacted with.
- The isHidden function checks whether an element is hidden on the web page.
- The isEditable function checks whether an element can be edited by the user.
- They return a boolean value indicating the state of the element.

Here is an example of using the all Is.. functions:

```Playwright
   test('Is... Example', async () => {
            const browser = await chromium.launch();
            const page = await browser.newPage();
            await page.goto('https://www.saucedemo.com/');

            // Check whether an input field with the name "username" is
                                      visible, enabled, hidden, and editable”
            const usernameInput = await
                                   page.locator(“//input[@name=’user-name’]”);
            const isUsernameInputVisible = await usernameInput.isVisible();
            const isUsernameInputEnabled = await usernameInput.isEnabled();
            const isUsernameInputHidden = await usernameInput.isHidden();
            const isUsernameInputEditable = await usernameInput.isEditable();
            console.log('Is the username input visible?',
                                                     isUsernameInputVisible);
            console.log('Is the username input enabled?',
                                                     isUsernameInputEnabled);
            console.log('Is the username input hidden?', 
                                                     isUsernameInputHidden);
            console.log('Is the username input editable?', 
                                                     isUsernameInputEditable);
            await browser.close();
        })
```

### BoundingBox
A BoundingBox in Playwright is a rectangular region on a web page that is defined by its coordinates (x, y) and its dimensions (width and height).

This can come in handy if you wanna check out visual stuff on a page like how far apart different elements are or if one element is on top of another.

Here is an example of using the all BoundingBox functions:

```Playwright
  test('boundingBox', async () => {
        const browser = await chromium.launch();
        const page = await browser.newPage();
        await page.goto('https://www.google.com');

        const searchBox = await page.locator("//input[@title='Search']");
        const searchBoxBoundingBox = await searchBox.boundingBox();

        // Click the center of the search box
        await page.mouse.click(
            searchBoxBoundingBox!.x + searchBoxBoundingBox!.width / 2,
            searchBoxBoundingBox!.y + searchBoxBoundingBox!.height / 2,
        );

        // Type text into the search box
        await page.keyboard.type('example search query');

        await browser.close();
    })
```
