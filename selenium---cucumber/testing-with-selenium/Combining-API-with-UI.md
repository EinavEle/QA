# *Advantages of combining API and UI*
What is the advantage of combining API and UI tests?
- To make our tests fast and dependable, we need prompt and accurate data.
- APIs are a faster and more reliable approach than other methods.
- APIs bypass browser issues and interact directly with the server, making them highly efficient.
- Using APIs helps us reduce the time taken to retrieve data.
# *How To Do It* 
Let's take logging in to a system that requires creating a new user in the backend as an example. 
We can use an API to create the user data and then fill out the username fields in the UI.
# *Examples*
```java
@Test
public void loginTest(){
    // Arrange
    RestClass restClass = new RestClass();
    User testedUser = new User(“userName”,"Password123");
    restClass.createUserViaApi(testedUser);
    loginPage = new LoginPage(driver);
    // Act loginPage.fullLoginProcess(testedUser.getUserName(),testedUser.getPassword());
    // Assert
    homePage = new HomePage(driver);
    Assert.assertTrue(homePage.headerIsVisible());
}
```
In our example, we use the API to create a user in our system, including their username and password.
Then, we send this data to establish a connection and check if it was successful.