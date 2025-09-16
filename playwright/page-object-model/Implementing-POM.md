# The Structure of the page class
### Locators
In this part of the POM (Page Object Model) class, we'll set up our locators. 
To avoid any outside interference, we'll declare them as private.
The locators will only be accessible within the class or page where they are defined, and there won't be any external access to them
And in fact this is how the whole issue of "encapsulation" is expressed.

```Playwright
   private userName: Locator
    private password: Locator
    private loginButton: Locator
```

### Constructor
In our case, the constructor's job is to create a webpage that we can use with Playwright and define the locators. 
We can also use the initPage function inside the constructor to make sure that each new page is set up correctly.
The constructor usually takes a WebDriver object to separate test logic from UI logic. This interface controls the web browser from your test script and can be reused across multiple Page Object Model instances. Passing the WebDriver instance to the constructor also ensures proper browser initialization, preventing errors or unexpected behavior.

For example:

```Playwright
 constructor(page: Page) {
        super(page)
        this.userName = page.locator('#user-name')
        this.password = page.locator('#password')
        this.loginButton = page.locator('#login-button')
        this.initPage()
    }
```

### Init Page
The initPage method is usually part of the Page Object class and gets called when we make a new page object. 
It does some setup stuff like waiting for the page to load and page ready to go. 
This method is in charge of getting all the web stuff set up and connected to the right parts of the page object class.

```Playwright
    initPage = async () => {
        await this.page.waitForLoadState()
    }
```
### Methods
In Page Object Model (POM), methods are used to interact with the web elements on a page. 
Methods are defined in a Page Object class and can be called from other classes to perform actions on the web elements.

The methods in a Page Object class should be designed to represent the actions that a user can perform on the corresponding web page. 
For example, if the page is a login page, the Page Object class may contain methods such as fillUserName, fillPassword, and clickOnSubmit.

```Playwright
    fillUserNameInput = async (userName: string) => {
        await this.userName.fill(userName)
    }

    fillPasswordInput = async (password: string) => {
        await this.password.fill(password)
    }

    clickSubmitButton = async () => {
        await this.loginButton.click()
    }
```
In this example, the Page Object class has three methods: `fillUserName`, `fillPassword`, and `clickOnSubmit`. These methods interact with the web elements on the page, entering text into the username and password fields and clicking the login button, respectively.

```Playwright
import { Locator, Page } from '@playwright/test'
import { BasePage } from './base-page'


export class LoginPage extends BasePage {
    private userName: Locator
    private password: Locator
    private loginButton: Locator

    constructor(page: Page) {
        super(page)
        this.userName = page.locator('#user-name')
        this.password = page.locator('#password')
        this.loginButton = page.locator('#login-button')
        this.initPage()
    }

    initPage = async () => {
        await this.page.waitForLoadState()
    }

    fillUserNameInput = async (userName: string) => {
        await this.userName.fill(userName)
    }

    fillPasswordInput = async ([password]: string) => {
        await this.password.fill(password)
    }

    clickSubmitButton = async () => {
        await this.loginButton.click()
    }
}
```

# Compound Actions
If we need to perform complex actions that involve multiple methods we already have, such as filling in data and clicking a button for a login operation, we can create a reusable function for this login action. 
This way, we can call this function from our test code without having to write unnecessary code.

Suppose we have a web application with a login page and we are using Page Object Model for our automated tests. 
In our Page Object class for the login page, we have methods for filling in the username, password, and clicking the login button. 
We could call these methods individually in our test code to perform the login operation:

```Playwright
 fillUserNameInput = async (userName: string) => {
        await this.userName.fill(userName)
    }

    fillPasswordInput = async ([password]: string) => {
        await this.password.fill(password)
    }

    clickSubmitButton = async () => {
        await this.loginButton.click()
    }
```

However, we can create a reusable function for the login operation so that we don't have to write these lines of code every time we want to perform a login. 
We can define a method in the Page Object class for the login page, which calls the individual methods to perform the login operation:

```Playwright
  fullLoginFlow =async (userName:string, password:string) => {
        await this.fillUserNameInput(userName)
        await this.fillPasswordInput(password)
        await this.clickSubmitButton()
    }
```

Now, we can call this login function from our test code with just one line of code:

```Playwright
  test('Full login function',async () => {
        const loginPage = new LoginPage(page)
        await loginPage.fullLoginFlow("standard_user","secret_sauce")
    })
```

This makes our test code more concise and readable, and reduces the potential for errors. Additionally, if we need to update the login process later, we only need to make changes in one place, rather than multiple locations in our test code. Overall, creating reusable functions in our Page Object classes can make our tests more efficient and maintainable.
