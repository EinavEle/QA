# What are waits and when to use them?
- Waits in Appium handle timing issues during test automation.
- They ensure that the test script waits for specific conditions before proceeding.
- Waits are used when there are timing differences between the test script and the application's response.
- Examples of timing differences include network delays, UI rendering, and server processing.
- Waits are helpful for element visibility, availability, clickability, and complete page load scenarios.
- They enhance the stability and reliability of tests by synchronizing with the application's timing.

# Implicit vs Explicit
With implicit wait, you set a general waiting time for the whole script, and if an element is not found within that time, the script will throw an error. It's like setting a timer for the whole process.

On the other hand, explicit wait is more like a targeted wait. You can wait for a specific element to appear or become clickable, and the script will wait until that condition is met before continuing. It's like waiting for a specific thing to happen before moving on to the next step.

Now let's expand on that…

# Implicit wait
Implicit waits define a global timeout that applies to all subsequent commands in the test script. It tells the Appium server to wait for a certain period of time for an element to appear before throwing an exception. 
This wait is applicable for the entire duration of the session unless overridden.


Here example for Implicit wait:
```Java
 @Test
    public void implicitlyWaitTest() throws MalformedURLException{
        // Create Appium driver instance
        driver = new AndroidDriver<>(
                               new URL("http://localhost:4723/wd/hub"), caps);
        // Set implicit wait for 10 seconds
        driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS);
        MobileElement womenButton = driver
               .findElementById("com.asos.app:id/splash_floor_women");
        womenButton.click();
        MobileElement okThanksButton = driver
               .findElementById("com.asos.app:id/dismiss_on_boarding_button");
        okThanksButton.click();
        MobileElement okThanksButton2 = driver
                .findElementById("android:id/button2");
        okThanksButton2.click();
        MobileElement womenCategorySelection = driver
                 .findElementById("com.asos.app:id/spinner_item_text");
        Assert.assertEquals("WOMEN",womenCategorySelection.getText());
    }
```
In this example, an implicit wait of 10 seconds is set using `driver.manage().timeouts().implicitlyWait(10, TimeUnit.SECONDS).`
This means that if any element is not immediately found, the driver will wait for up to 10 seconds for it to appear before throwing an exception.

# Explicit wait
Explicit waits allow for more fine-grained control over synchronization. 
With explicit waits, you can instruct the Appium driver to wait for a specific condition to be met before proceeding to the next step in the test script. 
This condition could be the presence of a specific element, its visibility, or any other desired state.

For example:

```Java
    @Test
    public void explicitWaitTest()throws MalformedURLException{
        // Create Appium driver instance
        driver = 
          new AndroidDriver<>(new URL("http://localhost:4723/wd/hub"), caps);
        //Explicit wait
        WebDriverWait wait = new WebDriverWait(driver, 10);
        wait.until(ExpectedConditions.visibilityOfElementLocated
                (By.id("com.asos.app:id/splash_floor_women")));
        MobileElement womenButton = driver
                      .findElementById("com.asos.app:id/splash_floor_women");
        womenButton.click();
        wait.until(ExpectedConditions.visibilityOfElementLocated
                (By.id("com.asos.app:id/dismiss_on_boarding_button")));
        MobileElement okThanksButton = driver
               .findElementById("com.asos.app:id/dismiss_on_boarding_button");
        okThanksButton.click();
        wait.until(ExpectedConditions.visibilityOfElementLocated
                (By.id("android:id/button2")));
        MobileElement okThanksButton2 = driver
                     .findElementById("android:id/button2");
        okThanksButton2.click();
        wait.until(ExpectedConditions.visibilityOfElementLocated
                (By.id("com.asos.app:id/spinner_item_text")));
        MobileElement womenCategorySelection = driver
                 .findElementById("com.asos.app:id/spinner_item_text");
        Assert.assertEquals("WOMEN",womenCategorySelection.getText());
    }
```
In this example, an explicit wait of 10 seconds is set using “WebDriverWait” to wait for the visibility of an elements with the ID 
`com.asos.app:id/splash_floor_women`,
`com.asos.app:id/dismiss_on_boarding_button
android:id/button2`,
`com.asos.app:id/spinner_item_text`.

The test verifies that the element is displayed on the screen using `Assert.assertEquals("WOMEN",womenCategorySelection.getText());.`


