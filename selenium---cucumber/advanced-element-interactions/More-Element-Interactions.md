# *Select*
You know those little dropdown menus on web pages?
Well, the Select class is what you use to control them! 
Its got all kinds of handy methods for selecting and deselecting options, getting the currently selected option, and grabbing all the options available. 
It's a super helpful tool for working with dropdowns, list boxes, and other similar elements.
```Java
public static  void selectTest(){
      // Initialize the WebDriver
      WebDriver driver = new ChromeDriver();
      // Navigate to the page with the drop-down list
      driver.get("https://www.amazon.com/");
      // Find the drop-down list element by ID
      WebElement dropdown = driver.findElement(By.id("searchDropdownBox"));
      // Create a Select object
      Select select = new Select(dropdown);
      // Select the "Books" option
      select.selectByValue("search-alias=stripbooks-intl-ship");
}
```
# *Check*
Have you ever seen those small check boxes on websites that you can select?
Those are checkboxes! 
They're pretty handy for selecting one or more options from a list.
And, when you check a box, that value gets sent along with the rest of the form data.

If you're working with checkboxes in Selenium, you'll want to use the click method to check or uncheck them.

Here's an example:
First, we'll check if the box is already selected. 
If it is, we'll click it again to deselect it. 
```Java
public static void checkBox(){
      // Initialize the WebDriver
      WebDriver driver = new ChromeDriver();
      // Navigate to the page with the drop-down list
      driver.get("https://www.zap.co.il/models.aspx?sog=e-tv&db4004=4839");
      // Find the drop-down list element by ID
      WebElement multiChoice =
                      driver.findElement(By.className("MultiSelectionBtn"));
      multiChoice.click();
      WebElement lgCheckBox = 
          new WebDriverWait(driver, 10).until(ExpectedConditions
                                .elementToBeClickable(By.id("db189989_2")));
      lgCheckBox.click();
      if (lgCheckBox.isSelected()) {
          lgCheckBox.click();
      }
      driver.quit();
}
```
In our example we use explicit wait for the pop-up.

In this example , we check if it is unselected, and if the result is false, we click to select the checkbox:
```Java
public static void checkBoxUnSelected() {
      // Initialize the WebDriver
      WebDriver driver = new ChromeDriver();
      // Navigate to the page with the drop-down list
      driver.get("https://www.zap.co.il/models.aspx?sog=e-tv&db4004=4839");
      // Find the drop-down list element by ID
      WebElement multiChoice =
                      driver.findElement(By.className("MultiSelectionBtn"));
      multiChoice.click();
      WebElement lgCheckBox = new WebDriverWait(driver,10)
                                .until(ExpectedConditions
                                .elementToBeClickable(By.id("db189989_2")));
      if (!lgCheckBox.isSelected()) {
          lgCheckBox.click();
      }
      driver.quit();
}
```
You can see the only alteration made was to the if statement.
# *IsDisplayed*
Are you looking to verify if a specific element appears on a webpage?
Then you'll definitely want to use isDisplayed! It's a handy-dandy method in Selenium that tells you whether or not an element is visible on the page.

Basically, isDisplayed returns either true or false, depending on whether the element is present and visible on the page. 
It's super useful for making sure certain things are showing up before you try to interact with them in your test automation scenarios.

For example, let's say you want to check if the Amazon logo is displayed. 
Just use isDisplayed to find out if it's showing up on the page!
```Java
public static void isDisplayed(){
        // Create a new instance of the ChromeDriver
        WebDriver driver = new ChromeDriver();
        // Navigate to the page with the element
        driver.get("https://www.amazon.com/");
        // Find the element by its ID
        WebElement amazonLogo = driver.findElement(By.id("nav-logo-sprites"));
        // Check if the element is displayed
        if (amazonLogo.isDisplayed()) {
            System.out.println("The logo is displayed.");
        } else {
            System.out.println("The logo is hidden or not present.");
        }
        // Close the browser
        driver.quit();
}
```
# *IsEnabled*
Interested in finding out whether a particular element on a webpage is enabled or not?
Then you'll definitely want to use isEnabled! It's another method in Selenium that can tell you whether or not an element can be interacted with.

If isEnabled returns true, that means the element is enabled and ready to be clicked, typed into, or whatever else you need to do with it. 
But if it returns false, that means the element is disabled or not even present in the DOM.

You can use isEnabled in all sorts of test automation scenarios where you need to make sure certain elements are good to go before performing actions on them.

For example, maybe you want to check if a "Submit" button is enabled after filling out a form. 
Just use isEnabled to make sure it's ready to be clicked!
```Java
public static void isEnabled(){
      // Create a new instance of the ChromeDriver
      WebDriver driver = new ChromeDriver();
      // Navigate to the page with the element
      driver.get("https://example.com");
      // Find the element by its ID
      WebElement element = driver.findElement(By.id("Submit"));
      // Check if the element is enabled
      if (element.isEnabled()) {
          System.out.println("The element is enabled.");
      } else {
          System.out.println("The element is disabled or not present.");
      }
      // Close the browser
      driver.quit();
}
```
# *Hover*
Ever heard of "hovering" or "mouseover" actions in Selenium? It's when you move your mouse cursor over an element on a web page without clicking it.

To perform a hover action like this in Selenium, you'll want to use the "Actions" class (don't worry, we'll cover this in-depth later!). This class gives you a bunch of different methods to perform all sorts of user interactions.

If you want to see an example of how to perform a hover action, check out this code snippet:
```Java
public static void hover(){
      // create a new instance of ChromeDriver
      WebDriver driver = new ChromeDriver();
      // navigate to the webpage
      driver.get("https://www.zap.co.il/");
      // locate the element to hover over
      WebElement LangFlag = driver.findElement(By.className("SubMenuItem"));
      // create an Actions object and move to the element
      Actions action = new Actions(driver);
      action.moveToElement(LangFlag).build().perform();
      // close the browser
      driver.quit();
}
```
With this code, you'll be able to hover over any element you want with ease!
# *GetAttribute*
To retrieve the value of a specific attribute of a web element, you can use the "getAttribute()" method in Selenium. 
For instance, you can get the value of the "class", "value", or "data-test-id" attribute of an element. Here's an example code snippet that demonstrates how to use the "getAttribute()" method:
```Java
public static void getAttribute(){
      // create a new instance of ChromeDriver
      WebDriver driver = new ChromeDriver();
      // navigate to the webpage
      driver.get("https://www.example.com");
      // locate the element and get the value of the "href" attribute
      WebElement link = driver.findElement(By.id("nav_a"));
      String attributeValue = link.getAttribute("href");
      // print the value of the "href" attribute
      System.out.println
                      ("The value of the 'href' attribute is: " + hrefValue);
      // close the browser
      driver.quit();
}
```
So, basically this code finds an element with a specific ID and saves it in a variable called "element". 
Then, it uses a method called "getAttribute()" to get the value of the "class" attribute of that element and stores it in a variable called "attributeValue".
Finally, it prints the value of the "class" attribute to the console.
This is important because it helps us do different things with web elements, like checking if they exist or clicking on them while doing Selenium test automation.

You can use the "getAttribute()" method to get the value of any attribute of a web element, such as "class", "id", "name", "value", etc.
# *DragAndDrop*
"Drag and drop" refers to the action of clicking and holding a graphical element, moving it to a new location, and then releasing it. 
This is often used in user interfaces to allow users to move items around or interact with visual elements.

Here's an example code snippet that shows you how to perform drag and drop:
```Java
public static void dragAndDrop(){
      // create a new instance of ChromeDriver
      WebDriver driver = new ChromeDriver();
      // navigate to the webpage
      driver.get("https://www.globalsqa.com/demo-site/draganddrop/");
      // locate the source and target elements
      WebElement sourceElement =
                                driver.findElement(By.xpath
                                ("//div[@id='gallery']/img[@alt='The peaks
                                    of High Tatras']"));
      WebElement targetElement = driver.findElement(By.id("trash"));
      // create an Actions object and perform drag and drop
      Actions actions = new Actions(driver);
      actions.dragAndDrop(sourceElement, targetElement).build().perform();
      // close the browser
      driver.quit();
}
```
This code finds the elements you want to move and puts them into the "sourceElement" and "targetElement" variables. 
Then, it uses an "Actions" object to drag and drop the elements using the "dragAndDrop()" method. 
Finally, it closes the browser with the "quit()" method.

Just a heads up - "dragAndDrop()" might not work on all websites. If that's the case, you can use the "clickAndHold()" method to pretend like you're holding down the mouse button, then use "moveToElement()" to move the element where you want it to go, and finally use "release()" to let go of the mouse button.

Here's an example:
```Java
public static void alternativeDragAndDrop() {
      // create a new instance of ChromeDriver
      WebDriver driver = new ChromeDriver();
      // navigate to the webpage
      driver.get("https://www.globalsqa.com/demo-site/draganddrop/");
      // locate the source and target elements
      WebElement sourceElement = driver.findElement(By.xpath("//div[@id='gallery']/img[@alt='The peaks of High Tatras']"));
      WebElement targetElement = driver.findElement(By.id("trash"));
      // create an Actions object and perform drag and drop
      Actions actions = new Actions(driver);
      actions.clickAndHold(sourceElement)
              .moveToElement(targetElement)
              .release()
              .build()
              .perform();
      // close the browser
      driver.quit();
}
```
# *Clear*
If you want to delete the contents of a text field or text area, you can use the "clear()" method. 
This method is called on the element that represents the input field.
It's useful when you want to start fresh with a blank input field. 

Here's an example:
```Java
public static void clearMethod() {
      // create a new instance of ChromeDriver
      WebDriver driver = new ChromeDriver();
      // navigate to the webpage
      driver.get("https://practicetestautomation.com/practice-test-login/");
      WebElement user = driver.findElement(By.id("username"));
      user.sendKeys("student");
      // clear the contents of the input field
      user.clear();
      // close the browser
      driver.quit();
}
```
In this example, we first enter data into the input field using the "sendKeys()" method, and then we use the "clear()" method to remove the data from the same input field.