In Selenium, there are several basic element interactions that can be used to interact with web elements on a page. For example:

**Click**
This method is used to simulate a mouse click on a web element, such as a button or a link. It can be used to trigger events or navigate to a new page.
```java
WebElement button = driver.findElement(By.id("myButton"));
button.click();
```

**SendKeys**
This method is used to simulate typing into a text input field. It can be used to enter text, passwords, or other input values into a form field.
```java
WebElement inputField = driver.findElement(By.name("username"));
inputField.sendKeys("myusername");
```
You can also send actual keys like "return", "esc", "leftarrow", etc..
For example:
```java
WebElement textBox = driver.findElement(By.id("idOfElement"));
textBox.sendKeys(Keys.ENTER);
```
Within the Selenium library, "Keys" is an enum that includes numerous keys.

**GetText**
This method is used to retrieve the text value of a web element. It can be used to verify that the expected text is displayed on the page, or to capture the value for later use in a script.
```java
// Find a web element and get its text value
WebElement element = driver.findElement(By.id("myHeader"));
String text = element.getText();
```