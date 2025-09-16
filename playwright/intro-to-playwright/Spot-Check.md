Write a simple test that makes a login to the website:
https://www.saucedemo.com/
  
<details><summary>  
Click here to reveal the answer.  
</summary>

 
```Playwright 
test('should login with valid credentials', async () => {
        await
        page.goto('https://practicetestautomation.com/practice-test-login/');
        const userName = page.locator('//input[@id="username"]');
        const password = page.locator('//input[@id="password"]');
        const loginButton = page.locator('//button[@id="submit"]')
        await userName.fill('student');
        await password.fill('Password123');
        await loginButton.click();
        const url = page.url();
        const pageTitle = await page.title();
        const header = page
                  .locator('//h1[contains(text(),"Logged In Successfully")]');
        expect(url).toContain('logged-in-successfully');
        expect(pageTitle)
                .toEqual('Logged In Successfully | Practice Test Automation');
        expect(await header.isVisible()).toBeTruthy();
    });
```
</details>