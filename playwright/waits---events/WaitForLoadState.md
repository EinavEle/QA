# What is it?
‘WaitForLoadState’ is a method that waits for a page's load state to reach a certain point before proceeding with further actions.

The load state of a page can have one of three values: ‘load’, ‘domcontentloaded’, or ‘networkidle’. 
The ‘WaitForLoadState’ method allows you to specify which load state you want to wait for.
The load state means:
1. ‘load’: This is when the entire page, including all of its resources (images, stylesheets, scripts, etc.), has been loaded.

2. ‘domcontentloaded’: This is when the initial HTML document has been completely parsed and the DOM tree has been constructed, but other resources like images and scripts may still be loading.

3. ‘networkidle’: This refers to a state where there is no more network activity on the page. 
This is useful when you want to ensure that all resources on the page have loaded, and that there are no pending network requests.

# When to use?
If you're dealing with pages that have lots of images and other stuff that takes a long time to load, you can use WaitForLoadState in Playwright. 
It makes sure everything is loaded before you start doing anything. 
So, after refreshing the page, use WaitForLoadState to wait until the page is ready before clicking on anything.

# Example
```Playwright
 test('wait for load', async () => {
        await page.goto('https://example.com');
        // Wait for the page to finish loading
        await page.waitForLoadState('load');
        // Now we can interact with the page
        await page.locator('a').click();
    })
```
In this example we navigate to the ‘example.com’ website, wait for the page to finish loading using ‘WaitForLoadState’, and then click on the first anchor element on the page.
