# *What are waits and when to use them?*
- A wait is used to pause the test script until a specific condition is met, like an element being available, visible, or interactable, or a particular text appearing on the webpage.
- Waits are important for reliable and error-free test automation with Selenium, as web pages can load and render at different speeds, causing timing issues.
- Selenium has two types of waits: implicit waits and explicit waits.

# *Implicit vs. Explicit*
With implicit wait, you set a general waiting time for the whole script, and if an element is not found within that time, the script will throw an error. It's like setting a timer for the whole process.

On the other hand, explicit wait is more like a targeted wait. You can wait for a specific element to appear or become clickable, and the script will wait until that condition is met before continuing. It's like waiting for a specific thing to happen before moving on to the next step.

Now let's expand on that…

# *Implicit Wait*
Implicit wait is a feature in WebDriver that helps it to wait for a certain period while looking for an element on a webpage. 
This comes in handy when some elements take longer to load.

Normally, implicit waiting for elements is turned off by default and you have to switch it on manually for each session. 
But be careful not to mix implicit and explicit waits, as it may lead to unexpected results, like waiting for the maximum time even if the element is already available or the condition is true.

To use implicit wait, simply use the "implicitlyWait" method of the "WebDriver.Options" interface. Once you set it, it will be in place for the whole session.

Here's an example of setting an implicit wait in Java:
```Java
public static void implicitWait() {
      // create a new ChromeDriver instance
      WebDriver driver = new ChromeDriver();
      //Create a implicitly Wait
      driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
      // navigate to a webpage
      driver.get("https://www.google.com");
      WebElement searchBox = driver.findElement(By.name("q"));
      searchBox.sendKeys("Selenium");
      WebElement luckyButton = driver.findElement(By.name("btnI"));
      luckyButton.click();
      driver.close();
}
```
In this example, WebDriver waits for a maximum of 10 seconds while trying to find an element, before throwing a "NoSuchElementException" if it is not found.

The implicit wait is set for the duration of the session or until it is changed again.

# *Explicit Wait*
Explicit waits are a way to pause program execution until a condition is met in imperative, procedural languages. 
They're useful for synchronizing the state between the browser and its DOM with your WebDriver script, like waiting for a dynamically added element to be added to the DOM before using the findElement call.

To use an explicit wait, you pass a function reference as the condition, which will run repeatedly until it returns a truth value. 
You can customize the wait condition by passing an argument to override the default timeout. 
Predefined expected conditions are also available in most clients, like element existence, visibility, and text.


For example:
```Java
public static void explicitWait() {
      // create a new ChromeDriver instance
      WebDriver driver = new ChromeDriver();
      // navigate to a webpage
      driver.get("https://www.google.com");
      // find the search box element and enter a query
      WebElement searchBox = driver.findElement(By.name("q"));
      searchBox.sendKeys("Selenium");
      // wait until the "I'm Feeling Lucky" button is clickable, or time out after 10 seconds
      WebElement luckyButton = new WebDriverWait(driver, 10)
                                    .until(ExpectedConditions
                                    .elementToBeClickable(By.name("btnI")));
      luckyButton.click();
      // close the browser window
      driver.quit();
}
```