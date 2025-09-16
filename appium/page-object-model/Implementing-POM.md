# The Structure of the page class
### Locators
In this part of the POM (Page Object Model) class, we'll set up our locators. 
To avoid any outside interference, we'll declare them as private and final.
The locators will only be accessible within the class or page where they are defined, and there won't be any external access to them
And in fact this is how the whole issue of "encapsulation" is expressed.
```Java
 private final MobileElement emailInput;
    private final MobileElement passwordInput;
    private final MobileElement signInWebButton;
    private final MobileElement loginErrorMessage;
```

### Constructor
In our case, the constructor's job is to create an app that we can use with Appium.

The constructor usually takes a Driver object to separate test logic from UI logic. This interface controls the web browser from your test script and can be reused across multiple Page Object Model instances. Passing the WebDriver instance to the constructor also ensures proper browser initialization, preventing errors or unexpected behavior.
In addition, in the constructor we will define all the paths of our locators that we defined earlier

For example:
```Java
public LoginPage(AndroidDriver<MobileElement> driver) {
        super(driver);
        this.emailInput = this.driver.findElementById("UsernameValidator");
        this.passwordInput = this.driver.findElementById("Password");
        this.signInWebButton = this.driver.findElementById("signin");
        this.loginErrorMessage = this.driver
                                     .findElementById("loginErrorMessage");
    }
```

### Methods
In Page Object Model (POM), methods are used to interact with the elements on a page. 
Methods are defined in a Page Object class and can be called from other classes to perform actions on the web elements.

The methods in a Page Object class should be designed to represent the actions that a user can perform on the corresponding web page. 
For example, if the page is a login page, the Page Object class may contain methods such as fillUserName, fillPassword, and clickOnSubmit.
```Java
   public void fillEmailInput(String email) {
        this.emailInput.setValue(email);
    }
    public void fillPasswordInput(String password) {
        this.passwordInput.setValue(password);
    }
    public void clickSignInButton() {
        this.signInWebButton.click();
    }
    public String getLoginErrorMessage() {
        return this.loginErrorMessage.getText();
    }
```

In this example, the Page Object class has three methods: `fillEmailInput`, `fillPasswordInput,clickSignInButton`, and `getLoginErrorMessage`. 
These methods interact with the web elements on the page, entering text into the email and password fields and clicking the login button, respectively.

# Compound Actions
If we need to perform complex actions that involve multiple methods we already have, such as filling in data and clicking a button for a login operation, we can create a reusable function for this login action. 
This way, we can call this function from our test code without having to write unnecessary code.

Suppose we have an application with a login page and we are using Page Object Model for our automated tests. 
In our Page Object class for the login page, we have methods for filling in the email, password, and clicking the login button. 
We could call these methods individually in our test code to perform the login operation:

```Java
  public void fillEmailInput(String email) {
        this.emailInput.setValue(email);
    }
    public void fillPasswordInput(String password) {
        this.passwordInput.setValue(password);
    }
    public void clickSignInButton() {
        this.signInWebButton.click();
    }
```

However, we can create a reusable function for the login operation so that we don't have to write these lines of code every time we want to perform a login. 
We can define a method in the Page Object class for the login page, which calls the individual methods to perform the login operation:
```Java
public class LoginPage extends BasePage {
    //...
    public void fullSignInFlow(String email, String password) {
        this.fillEmailInput(email);
        this.fillPasswordInput(password);
        this.clickSignInButton();
    }
    //...
}
```

Now, we can call this login function from our test code with just one line of code:
```Java
 LoginPage loginPage = new LoginPage(driver);
        loginPage.fullSignInFlow("test@email.com","123");
```
This makes our test code more concise and readable, and reduces the potential for errors. Additionally, if we need to update the login process later, we only need to make changes in one place, rather than multiple locations in our test code. 
Overall, creating reusable functions in our Page Object classes can make our tests more efficient and maintainable.




