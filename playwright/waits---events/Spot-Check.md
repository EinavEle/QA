Write a test that opens a link using the middle button of the mouse, waits for the new tab to load and returns an answer when it is loaded successfully
Use the following link:
https://the-internet.herokuapp.com/
and select one of the options there

  
<details><summary>  
Click here to reveal the answer.  
</summary>

 
```Playwright 
    test('spot check', async () => {
        const context = await browser.newContext()
        const page = await context.newPage()
        await page.goto('https://the-internet.herokuapp.com/')
        const promisePage = context.waitForEvent('page')
        const brokenImagesButton = page.locator("//a[text()='Broken Images']")
        await brokenImagesButton.click({ button: "middle" })
        const test = await promisePage
        const title = await test.locator('//h3').innerText()
        expect(title).toBe('Broken Images')
    })
```
</details>