After we locate the elements and we know  a basic interactions we can run this simple test to check if we get the correct elements:
```Java
@Test
    public void calcSumTest() throws MalformedURLException {
        DesiredCapabilities caps = new DesiredCapabilities();
        caps.setCapability("platformName", "Android");
        caps.setCapability("platformVersion", "13");
        caps.setCapability("deviceName", "RF8R51CN95V");
        caps.setCapability("appPackage",
                           "com.sec.android.app.popupcalculator");
        caps.setCapability("appActivity", ".Calculator");

        AndroidDriver<MobileElement> driver = 
        new AndroidDriver<>(new URL("http://localhost:4723/wd/hub"), caps);
        MobileElement number8 = driver.findElementById(
              "com.sec.android.app.popupcalculator:id/calc_keypad_btn_08");
        MobileElement number9 = driver.findElementById(
              "com.sec.android.app.popupcalculator:id/calc_keypad_btn_09");
        MobileElement plus = driver.findElementById(
               "com.sec.android.app.popupcalculator:id/calc_keypad_btn_add");
        MobileElement result = driver.findElementById(
               "com.sec.android.app.popupcalculator:id/calc_tv_result");
        number8.click();
        plus.click();
        number9.click();
        Assert.assertEquals(result.getText(),"17");
        //this should be in 'after' hook
        driver.quit();
    }
```
In this example we click on 8, 9 and ‘+ ‘ button and expected to get 17 in result view text.