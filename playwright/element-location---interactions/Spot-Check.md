Create a test for this web page: https://www.globalsqa.com/demo-site/draganddrop/
Using drag and drop function
The test need to check if the element was moved to the trash
  
<details><summary>  
Click here to reveal the answer.  
</summary>

 
```Playwright 
          test('Spot Check', async () => {
        const browser = await chromium.launch();
        const page = await browser.newPage();
        await page.goto('https://www.globalsqa.com/demo-site/draganddrop/');
        const source = page.locator("//h5[text()='High Tatras']");
        const target = page.locator("//div[@id='trash']");
        await source.dragTo(target);
        const itemOnTrash = page
                            .locator("//ul[@class='gallery ui-helper-reset']")
        expect(await itemOnTrash.isVisible()).toBeTruthy();
    })
```
</details>