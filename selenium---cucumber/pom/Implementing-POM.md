# *The Structure of the Page Class*
**Locators**
In this part of the POM (Page Object Model) class, we'll set up our locators. 
To avoid any outside interference, we'll declare them as private and final.
The locators will only be accessible within the class or page where they are defined, and there won't be any external access to them.
And, in fact, this is how the whole issue of "encapsulation" is expressed.
```Java
private final static String  INPUT_USER_NAME = "username";
private final static String  INPUT_PASSWORD = "password";
private final static String  BUTTON_SUBMIT = "btn";
```
**Constructor**
In our case, the constructor's job is to create a webpage that we can use with Selenium to do cool things. 
We can also use the initPage function inside the constructor to make sure that each new page is set up correctly.
The constructor usually takes a WebDriver object to separate test logic from UI logic. This interface controls the web browser from your test script and can be reused across multiple Page Object Model instances. Passing the WebDriver instance to the constructor also ensures proper browser initialization, preventing errors or unexpected behavior.

For example:
```Java
public LoginPage(WebDriver driver){
        this.driver = driver;
        this.initPage();
    }
```
**Init Page**
The initPage method is usually part of the Page Object class and gets called when we make a new page object. 
It does some setup stuff, including waiting for the page to load and getting the elements on the page ready to go. 
This method is in charge of getting all the web stuff set up and connected to the right parts of the page object class.

To do this, the initPage method might use Selenium WebDriver to find and save the web elements on the page as part of the page object.

Once the elements have been initialized, they can be accessed and used by other methods within the same Page Object class.
```Java
public void initPage(){
        user = this.driver.findElement(By.id(INPUT_USER_NAME));
        pass = this.driver.findElement(By.name(INPUT_PASSWORD));
        submit = this.driver.findElement(By.className(BUTTON_SUBMIT));
    }
```
**Methods**
In Page Object Model (POM), methods are used to interact with the web elements on a page. 
Methods are defined in a Page Object class and can be called from other classes to perform actions on the web elements.

The methods in a Page Object class should be designed to represent the actions that a user can perform on the corresponding web page. 
For example, if the page is a login page, the Page Object class may contain methods such as fillUserName, fillPassword, and clickOnSubmit.
```Java
public void fillUserName(String userName){
        this.user.sendKeys(userName);
    }
    public void fillPassword(String password){
        this.pass.sendKeys(password);
    }
    public void clickOnSubmit(){
        this.submit.click();
    }
```
In this example, the Page Object class has three methods: `fillUserName`, `fillPassword`, and `clickOnSubmit`. These methods interact with the web elements on the page, entering text into the username and password fields and clicking the login button, respectively.
```Java
package PageObjectModel;
import org.openqa.selenium.By;
import org.openqa.selenium.WebDriver;
import org.openqa.selenium.WebElement;
import org.testng.Assert;
public class LoginPage extends BasePage{
    private final String  INPUT_USER_NAME = "username";
    private final String  INPUT_PASSWORD = "password";
    private final String  BUTTON_SUBMIT = "btn";
    private final String TITLE = "login_logo";
    private  WebElement user;
    private WebElement pass;
    private WebElement submit;
    private WebElement title;
    public LoginPage(WebDriver driver){
        super(driver);
        this.initPage();
    }
    public void initPage(){
        title = this.driver.findElement(By.className(TITLE));
        user = this.driver.findElement(By.id(INPUT_USER_NAME));
        pass = this.driver.findElement(By.name(INPUT_PASSWORD));
        submit = this.driver.findElement(By.className(BUTTON_SUBMIT));
    }
    public void fillUserName(String userName){
        this.user.sendKeys(userName);
    }
    public void fillPassword(String password){
        this.pass.sendKeys(password);
    }
    public void clickOnSubmit(){
        this.submit.click();
    }
   public void fullLoginProcess(String userName,String password){
        this.fillUserName(userName);
        this.fillPassword(password);
        this.clickOnSubmit();
    }
    public boolean titleIsVisible(){
        return this.title.isDisplayed();
    }
    public void checkTitleInPage(){
        Assert.assertEquals(titleIsVisible(),true);
    }
}
```
# *Compound Actions*
If we need to perform complex actions that involve multiple methods we already have, such as filling in data and clicking a button for a login operation, we can create a reusable function for this login action. 
This way, we can call this function from our test code without having to write unnecessary code.

Suppose we have a web application with a login page and we are using Page Object Model for our automated tests. 
In our Page Object class for the login page, we have methods for filling in the username, password, and clicking the login button. 
We could call these methods individually in our test code to perform the login operation:
```Java
public void fillUserName(String userName){
        this.user.sendKeys(userName);
    }
    public void fillPassword(String password){
        this.pass.sendKeys(password);
    }
    public void clickOnSubmit(){
        this.submit.click();
    }
```
However, we can create a reusable function for the login operation so that we don't have to write these lines of code every time we want to perform a login. 
We can define a method in the Page Object class for the login page, which calls the individual methods to perform the login operation:
```Java
public class LoginPage {

    // ...
    public void fullLoginProcess(String userName,String password){
        this.fillUserName(userName);
        this.fillPassword(password);
        this.clickOnSubmit();
    }
    // ...
}
```
Now, we can call this login function from our test code with just one line of code:
```Java
LoginPage loginPage = new LoginPage(driver);
loginPage.fullLoginProcess("student","Password123");
```
This makes our test code more concise and readable, and reduces the potential for errors. Additionally, if we need to update the login process later, we only need to make changes in one place, rather than multiple locations in our test code. Overall, creating reusable functions in our Page Object classes can make our tests more efficient and maintainable.