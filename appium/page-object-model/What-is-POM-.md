
# Intro to POM(Page Object model):

POM stands for "Page Object Model," which is a design pattern used in software development for creating more organized and maintainable code. 
It's like having a blueprint for your application, where each page or component is defined as a separate class with its own methods and properties. 
This makes it easier to make changes or updates to your code without affecting the rest of the application.
Each pom is basically a class that represents a page in the app being tested.

This Class (this page) applies several rules:

1. Encapsulation: The principle of encapsulation refers to the concept of bundling data and behavior (methods) within a single unit (class). 
This helps to hide the complexity of the internal workings of the class and provides a well-defined interface for interacting with it.

    As an example, we have encapsulated all the locators on our page by defining them as private, ensuring that they are only accessible within the relevant code or class and not from outside.

```Java
private final MobileElement womenButton;
```
2. Abstraction: Abstraction is the process of selecting only relevant information about an object to be used in the program. 
It allows for creating simpler models of complex systems and enables you to focus on what an object does, rather than how it does it.

    For example let's say you have a login page with the following elements:
    - Username field
    - Password field
    - Login button

    Instead of directly interacting with these elements in your test case, you can create a separate Java class for this login page and define methods that represent the actions that a user can perform on this page. 
    This is called abstraction, where you hide the implementation details of the login page and only expose the necessary functionality.
    Here's an example of how you can implement this using Page Object Model

```Java
import io.appium.java_client.MobileElement;
import io.appium.java_client.android.AndroidDriver;

public class LoginPage extends BasePage{
    private final MobileElement emailInput;
    private final MobileElement passwordInput;
    private final MobileElement signInWebButton;
    private final MobileElement loginErrorMessage;
    public LoginPage(AndroidDriver<MobileElement> driver) {
        super(driver);
        this.emailInput =  this.driver.findElementById("UsernameValidator");
        this.passwordInput  = this.driver.findElementById("Password");
        this.signInWebButton  = this.driver.findElementById("signin");
        this.loginErrorMessage =this.driver.findElementById("loginErrorMessage");
    }

    public void fillEmailInput(String email){
        this.emailInput.setValue(email);
    }
    public void fillPasswordInput(String password){
        this.passwordInput.setValue(password);
    }
    public void clickSignInButton(){
        this.signInWebButton.click();
    }
    public String getLoginErrorMessage(){
        return this.loginErrorMessage.getText();
    }
}
```

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;In your test case, you can then create an instance of the LoginPage class and 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;call the methods defined in it, like this:

```Java
 @Test
    public void POMTest(){
        driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
        WelcomePage welcomePage = new WelcomePage(driver);
        welcomePage.clickWomenButton();
        AppUpdatePage updatePage=new AppUpdatePage(driver);
        updatePage.clickOnOkButton();
        HomePage homePage = new HomePage(driver);
        homePage.goToSignInPage();
        LoginPage loginPage = new LoginPage(driver);
        loginPage.fullSignInFlow("test@email.com","123");
        Assert.assertTrue(loginPage.getLoginErrorMessage().contains("Looks like either your email"));
    }
```
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;By using abstraction in this way, your test case becomes more readable and 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;maintainable. If the implementation of the login page changes in the future, 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;you only need to update the LoginPage class, and your test cases will still 
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;work without any modifications.

3. Inheritance: Inheritance is a mechanism that allows a class to inherit the properties and methods of another class. 
This helps to create a hierarchy of classes and makes it easier to create new classes based on existing ones.
For example, all pages have the refresh() ability so this functionality will be implemented in a base class and all inheriting classes will be able to use it.

4. Polymorphism: Polymorphism allows objects of different classes to be treated as if they were of the same class. It enables you to write code that can work with objects of different types in a generic way, without knowing the specific type of the object.

    Let's say we have a base class called Page that defines a common method for all pages in our application, called getTitle(), which returns the title of the page as a string:

```Java
public class Page {
    public String getTitle() {
        // Implementation to get the title of the page
        return "Page Title";
    }
}
```

Now, we have two page classes, HomePage and LoginPage, which inherit from the Page class:

```Java
public class HomePage extends Page {
    // HomePage specific methods and locators
}

public class LoginPage extends Page {
    // LoginPage specific methods and locators
}
```

Both HomePage and LoginPage classes inherit the getTitle() method from the Page class, so we can call the getTitle() method on objects of these classes without knowing the specific type of the object.

For example, in our test script, we can create a Page object and call the getTitle() method, and it will work for any page:

```Java
public class MyTest {
    @Test
    public void getPageTitle() {
        List<Page> pages = new ArrayList<>();
        pages.add(new HomePage());
        pages.add(new LoginPage());
        for(Page page:pages){
          System.out.println(page.getTitle());
        }
    }
}
```

In this example, we create a list of pages that are made up of various sub-pages. We then attempt to print the title of each page using a method that belongs to the base class.