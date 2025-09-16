# *Static Content vs. Dynamic Content*
- Static content refers to elements on a webpage that do not change frequently, like headings, paragraphs, and images.
These elements can be easily identified using standard locator strategies such as ID, name, class name, or CSS selector when writing a scripts.
For example, a website logo: 
![.guides/img/image5](./image5.png)
- Dynamic content refers to elements on a webpage that can change frequently based on user interactions or external factors.
Examples of dynamic content include pop-ups, dropdown menus, and other elements that can change based on user actions or server-side updates.
For example, a user profile name or image:
![.guides/img/image4](./image4.png)
- Handling dynamic content can be challenging as the location and properties of these elements can change dynamically.
- Additional techniques, such as waiting for content to load, using specialized locator strategies like XPath, or using tools like WebDriverWait, can be used to handle dynamic content effectively.
- It is important to consider both static and dynamic content when automating tests, and to use appropriate techniques and strategies to handle each type of content effectively.
# *Interacting with Dynamic Content*
1. Use Explicit Waits: With explicit waits, you can wait for a certain condition to happen before moving on to the next step in your test. 
This comes in handy when you're waiting for content that changes all the time. 
To use it, you can rely on the WebDriverWait class to either wait for a specific amount of time or until a particular condition is fulfilled.
Here's an example: the code below waits for a maximum of 10 seconds to find an element with an ID:
    ```Java
    import org.openqa.selenium.support.ui.WebDriverWait;
    import org.openqa.selenium.support.ui.ExpectedConditions;

    // wait up to 10 seconds for element to be visible
    WebElement element = new WebDriverWait(driver, 10).until(
        ExpectedConditions.visibilityOfElementLocated(By.id("dynamic-element"))
    );
    ```
2. Try Dynamic Locators: If you think an element's attributes might change dynamically, you can use more flexible locator strategies, such as XPath or regex. These can help you find the element even if it changes.
Here's an example: the following XPath finds an element with an ID that has the word "dynamic" anywhere in the string:
    ```Java
    WebElement element = driver.findElement(By.xpath(String.format("//div[contains(@id,'%s')]",dynamicId)));
    ```
3. Try Actions Class: With the Actions class, you can do more advanced user interactions, like clicking on an element or dragging and dropping.
It's great for dealing with content that changes all the time and needs user input.
For example, the code below clicks on an element with an ID of "dynamic-element":
    ```Java
    import org.openqa.selenium.interactions.Actions;

    // locate the element
    WebElement element = driver.findElement(By.id("dynamic-element"));

    // create an actions object and click on the element
    Actions actions = new Actions(driver);
    actions.click(element).perform();
    ```
Locating and interacting with dynamic content can be tricky and might need some specialized techniques like explicit waits, dynamic locators, and the Actions class. These methods can help you better deal with content that changes frequently.