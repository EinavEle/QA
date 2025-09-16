Let’s look at a few simple functions in Selenium WebDriver to do some basic actions on a browser:

**Launch New Browser:**
To open a browser, create a WebDriver interface instance and specify the browser you want to use. You can use the following code:
```java
WebDriver driver = new ChromeDriver();
```
This will open a new Chrome browser window.

**Navigate:**
To navigate a webpage in a browser, you can use the 'get()' method, which takes a string parameter for the URL you want to visit. 

For instance, if you want to go to the Google homepage, you can use this code:
```java
WebDriver driver = new ChromeDriver();
driver.get("http://www.google.com")
```

**Find Element:**
First, you need to find the element on a web page to interact with it. 
You can do this by using locator strategies like ID, class name, or XPath. 
For instance, if you want to find an element with an ID of "myElement," you can use the following code:
```Java
WebElement element = driver.findElement(By.id("myElement"));
```
WebElement is important in testing and has various options for interacting with elements, such as clicking or getting text. 
It has a lot of options that we will expand on later.

**Switching Between Tabs:**
To move between tabs in your browser, you can use the switchTo() method from the WebDriver interface. 
To go to the first tab, use this code:
```java
driver.switchTo().window(driver.getWindowHandles().toArray()[0]);
```
This will switch the focus to the first tab.

**Set Window Size:**
To resize the browser window, use the manage() method from WebDriver interface and then the window() method to set the size. 
To maximize the window, just use this code:
```java
driver.manage().window().maximize();
```
This will maximize the browser window.

**Close:**
To close the browser window, you can simply use the close() method provided by the WebDriver interface. 
To close the current window, just use this code:
```java
driver.close();
```
This will close the current browser window.