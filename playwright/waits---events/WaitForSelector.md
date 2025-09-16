# What is it?
The ‘waitForSelector’ function waits until a particular element, identified by the selector you provide, does what you want it to do. 
You can specify that you want it to show up, disappear from the page, or become visible or hidden. 
If the element is already doing what you want when you call the function, it'll finish right away. But if it takes too long to meet the condition, the function will throw an error.

# When to use?
You would use the ‘waitForSelector’ function when you need to ensure that a specific element is in a certain state before proceeding with the next step in your code. 
For example, you may need to wait for an element to become visible or hidden before you can interact with it, or you may need to wait for an element to appear or disappear from the page before you can proceed with the rest of your code. 
‘waitForSelector’ is particularly useful when working with dynamic web pages where elements may be added or removed from the DOM based on user interaction or other events.

# Examples
In the next example, ‘page.locator’ is used to find the ‘h1’ element on the page, and then innerText() is called on the element to extract its text content. 

```Playwright
 test('wait for selector', async () => {
        await page.goto('https://example.com')
        // Wait for the selector to be available
        await page.locator('//h1').waitFor()
        let header = await page.locator('//h1')
        // Get the text content of the element
        const title = await header.innerText()
        console.log(title) // Output: "Example Domain"
    })
```