# Intro to POM(Page Object model):

POM stands for "Page Object Model," which is a design pattern used in software development for creating more organized and maintainable code. 
It's like having a blueprint for your website or application, where each page or component is defined as a separate class with its own methods and properties. 
This makes it easier to make changes or updates to your code without affecting the rest of the application.
Each pom is basically a class that represents a page in the app being tested.

This Class (this page) applies several rules:

1. Encapsulation: The principle of encapsulation refers to the concept of bundling data and behavior (methods) within a single unit (class). 
This helps to hide the complexity of the internal workings of the class and provides a well-defined interface for interacting with it.

     As an example, we have encapsulated all the locators on our page by declaring them in class and defining them in the constructor , ensuring that they are only accessible within the relevant code or class and not from outside.

      For example:
```Playwright
export class MyPage {
    private userName: Locator

    constructor(page: Page) {
        this.userName = page.locator('#user-name')
    }
}
```
2. Abstraction: Abstraction is the process of selecting only relevant information about an object to be used in the program. 

      It allows for creating simpler models of complex systems and enables you to focus on what an object does, rather than how it does it.

    For example let's say you have a login page with the following elements:
    - Username field
    - Password field
    - Login button

      Instead of directly interacting with these elements in your test case, you can create a separate class for this login page and define methods that represent the actions that a user can perform on this page. 
      This is called abstraction, where you hide the implementation details of the login page and only expose the necessary functionality.
Here's an example of how you can implement this using Page Object Model:
```Playwright
import { Locator, Page } from '@playwright/test'

export class LoginPage {
    protected page: Page
    private userName: Locator
    private password: Locator
    private loginButton: Locator

    constructor(page: Page) {
        this.page = page
        this.userName = page.locator('#user-name')
        this.password = page.locator('#password')
        this.loginButton = page.locator('#login-button')
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
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In your test case, you can then create an instance of the LoginPage class and 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;call the methods defined in it, like this:

```Playwright
 test('simple page', async ({page}) => {
        const loginPage = new LoginPage(page)
        await loginPage.fillUserNameInput("standard_user")
        await loginPage.fillPasswordInput("secret_sauce")
        await loginPage.clickSubmitButton()
        // Add assertions to verify that the login was successful
    })
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;By using abstraction in this way, your test case becomes more readable and 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;maintainable. 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;If the implementation of the login page changes in the future, you only need to 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;update the LoginPage class, and your test cases will still work without any 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;modifications.

3. Inheritance: Inheritance is a mechanism that allows a class to inherit the properties and methods of another class. 
This helps to create a hierarchy of classes and makes it easier to create new classes based on existing ones.
For example, all pages have the refresh() ability so this functionality will be implemented in a base class and all inheriting classes will be able to use it.
