# Select
The Select class is used to handle dropdowns or selection elements in mobile applications. It provides methods to select options from a dropdown list based on different criteria such as index, value, or visible text.

Example of using Select in Appium:

Suppose we have a dropdown element with the ID "dropdown" in a mobile application, and we want to select an option by its visible text:
```Java
    @Test
    public void selectTest(){
        MobileElement womenButton = driver
                       .findElementById("com.asos.app:id/splash_floor_women");
        womenButton.click();
        MobileElement okThanksButton = driver
               .findElementById("com.asos.app:id/dismiss_on_boarding_button");
        okThanksButton.click();
        MobileElement okThanksButton2 = driver
                      .findElementById("android:id/button2");
        okThanksButton2.click();
        MobileElement dropdownElement = driver
                      .findElementByClassName("android.widget.ListView");
        Select dropdown = new Select(dropdownElement);
        dropdown.selectByVisibleText("Men");
        MobileElement womenCategorySelection = driver
                       .findElementById("com.asos.app:id/spinner_item_text");
        Assert.assertEquals("Men",womenCategorySelection.getText());
    }
```

# IsDisplayed
The "isDisplayed" method is all about checking if an element is visible on the mobile app screen. It simply gives you a true or false, telling you if the element is currently shown or not.

Example of using "isDisplayed":

Suppose we have a button element with the ID "button" in a mobile application, and we want to check if it is currently displayed:
```Java
   @Test
    public void isDisplayedTest(){
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
        Assert.assertTrue(womenCategorySelection.isDisplayed());
    }
```
In this example, we first find an element using its ID. 
Then, we use the ‘isDisplayed()’ method on the button element to check if it is currently displayed. 
The method returns a boolean value, which is checked in assertTrue assertion.

# IsEnabled
The "isEnabled" method is used to check the enabled status of an element on the mobile application screen. 
It returns a boolean value indicating whether the element is currently enabled for interaction or not.

Example for "isEnabled"

```Java
  @Test
    public void isEnabledTest(){
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
        Assert.assertTrue(womenCategorySelection.isEnabled());
    }
```
In this example, first, we find an element using its ID. Then, we use the 'isEnabled()' method on the element to see if it's currently enabled. The method gives us a true or false, and we check it using assertTrue assertion.

# DragAndDrop
"DragAndDrop" refers to the action of dragging an element from one location and dropping it onto another location in a mobile application. 
It is used to simulate user interactions such as rearranging elements or performing drag-and-drop operations.
Example of using "DragAndDrop":
Suppose we have two elements, sourceElement and targetElement, in a mobile application, and we want to perform a drag-and-drop operation:
```Java
       @Test    
       public void dragAndDropTest() {
        // Find the source and target elements
        MobileElement sourceElement = driver.findElement(By.id("source"));
        MobileElement targetElement = driver.findElement(By.id("target"));
        // Perform the drag and drop operation
        TouchAction action = new TouchAction(driver);
        action.longPress(ElementOption.element(sourceElement))
              .moveTo(ElementOption.element(targetElement))
              .release()
              .perform();
         Assert.assertTrue(targetElement.isEnabled());
    }
}
```
In this example, we first find the sourceElement and targetElement using their respective IDs. Then, we create a TouchAction object, which allows us to perform touch-related actions.
The drag and drop operation is performed using the “longPress()” method to press and hold the sourceElement, “moveTo()” method to move the element to the targetElement, and release() method to release the element.

# Clear
 The "clear" method is used to clear the text or input of an editable element in a mobile application. It is commonly used to remove any existing text or input from a text field or input box.

Example for "clear":

```Java
  @Test
    public void clearTest(){
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
        MobileElement searchButton = driver
               .findElementById("com.asos.app:id/action_search_for_products");
        searchButton.click();
        MobileElement searchInput = driver
                         .findElementById("com.asos.app:id/search_edit_text");
        searchInput.click();
        searchInput.setValue("test");
        searchInput.clear();
        Assert
           .assertEquals("Search for items and brands",searchInput.getText());
    }
```
In this example, we first find the input element using its ID. 
Then, we use the “clear()” method on the input element to clear any existing text or input in the field.

