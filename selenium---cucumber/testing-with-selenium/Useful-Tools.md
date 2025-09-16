# *Screenshots*
Taking a screenshot is like taking a picture of what's going on in your web browser at a particular moment. It's a handy way to figure out what went wrong during testing, because you can see exactly what the user saw when things went south.

If you're using Selenium, you can use something called the TakesScreenshot interface to take a screenshot of the page.

To capture a screenshot when a test fails, we can create a function that takes a screenshot and call it at the end of the test using the @AfterMethod annotation.
```java
public void takeScreenshot(String testName) {
    // Take a screenshot of the page
    File screenshot = 
              ((TakesScreenshot) driver).getScreenshotAs(OutputType.FILE);
    try {
        // Save the screenshot to a file
        FileUtils.copyFile(screenshot, 
                            new File("screenshots/" + testName + ".png"));
        System.out.println("Screenshot saved to: " 
                              + "screenshots/" 
                              + testName + ".png");
    } catch (IOException e) {
        e.printStackTrace();
    }
}
```
# *Browser Console Logs*
- Use driver.get_log('browser') to retrieve browser logs in Selenium WebDriver.
- Other log types that can be retrieved include 'client', 'driver', and 'server'.
- Browser logs can provide information on network requests, JavaScript console messages, warnings, and errors, which is helpful for debugging and troubleshooting.
- Some browsers may not support get_log() or only support specific log types, so check browser-specific documentation for compatibility.
For example:
```java
List<LogEntry> browseLog =  
driver.manage().logs().get("browser").getAll();
System.out.println(browseLog);
```
Sample from browser log:
```java
POST request failed with response code: 404
[]
```