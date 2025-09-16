# What is it?
waitForEvent is a method that waits for a specific event to happen and then passes its value into a function. Once the function returns a truthy value, waitForEvent resolves and returns the event data value.

If the page is closed before the event is fired, waitForEvent will throw an error. Therefore, you should handle this situation in your code to prevent unexpected errors.

Overall, waitForEvent is a useful method in Playwright that allows you to wait for specific events to happen and then perform actions based on the data returned from those events.

# When to use
We will usually use this when there are continuous events for example wait for loading page, downloading a file as in the example we will see right away

# Example
```Playwright
 test('wait for event', async () => {
        await page.goto('https://the-internet.herokuapp.com/download')
        const downloadPromise = page.waitForEvent('download')
        await page.getByText('qa.png').click()
        const download = await downloadPromise;
        expect(await download.failure()).toBeNull()
    })
```
In our example, we will load a page and then set the waiting function without waiting for it to complete, then we click on the download button, finally we will wait for the "download" event to complete.

In other example we use it with ‘page’ event:
```Playwright
 test(' wait for event `page`', async () => {
        const context = await browser.newContext()
        const page = await context.newPage()
        // Navigate to a page that opens a new tab
        await page.goto('https://www.nba.com/stats')
        const playerButton = page.locator('//a//span[text()="Players"]')
        const pagePromise = context.waitForEvent('page')
        await playerButton.click({ button: 'middle' })
        // Wait for a new page to be opened
        const newPage = await pagePromise
   await expect(newPage.locator('//h1[text()="League Roster"]')).toBeVisible()
    })
```
In this example, we create a new context and use waitForEvent() to listen for the 'page' event. 
Once the event is emitted (i.e. a new page is created), we store a reference to the new page in the newPage variable and perform some action on it (in this case, navigating to a URL).
https://playwright.dev/docs/events#waiting-for-event