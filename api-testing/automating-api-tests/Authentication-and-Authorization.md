# Authentication
Authentication is verifying the identity of a user or application trying to access an API. Authorization is determining if they have the necessary permissions to perform actions. Using a token is a common way of authentication in API automation testing . 
It involves generating a token and including it in API requests to verify the user's authorization. 

This helps prevent unauthorized access and ensures only authorized users can perform actions.

Things we would like to test:
1. Check if the login credentials work and invalid ones are rejected.
1. Test if the account is locked after a certain number of failed login attempts.
1. Check if the session remains secure after logging in and that the user is logged out after inactivity.
1. Test password reset functionality to make sure it's secure and effective.
1. Verify that different user roles have the appropriate level of access.
1. Test multi-factor authentication to ensure it's secure and prompts users for the second factor of authentication.

For example:
```Java
@Test
public void simpleAuthentication(){
    Map<String,String > body = new HashMap<>();
    //here we get the token for our user
    body.put("username","tzahi");
    body.put("password","123abc");
    AutomatingAPITests.HttpResponse<AuthResponse> auth =
                  HttpUtil.get("https://example.com/authenticate",body);
    //now we get the user details
    AutomatingAPITests.HttpResponse<UserDetailsResponse> 
                                                        userDetails =null;
    body.put("token",auth.getToken().toString());
    userDetails = HttpUtil.get("https://example.com/user",body);
}
```
In our example, we grab the token using the user's login info and then use it to fetch their details.

# Authorization
Authorization testing is about checking who has permission to do what in an application. 
It involves verifying whether users or entities can access specific resources or perform certain actions. 
For example, in a web app, you might test if regular users and admins can access different pages. 
This testing is important for ensuring the application is secure and that users can only access the resources and actions they're authorized to.

For example:
```Java
@Test
public void testProtectedPageAccess() {
    // Create a regular user account
    User regularUser = new User("username", "password", Role.USER);

    // Create an admin user account
    User adminUser = new User("admin", "password", Role.ADMIN);

    // Try to access a protected page with the regular user account
    String regularUserPage = getPage("/protected-page", regularUser);
    assertEquals("Access Denied", regularUserPage);

    // Try to access a protected page with the admin user account
    String adminUserPage = getPage("/protected-page", adminUser);
    assertEquals("Protected Page Content", adminUserPage);
}

// Helper method to simulate getting a protected page with a user's credentials
private String getPage(String pageUrl, User user) {
    // Set up a HTTP connection using the user's credentials
    HttpURLConnection connection = (HttpURLConnection) 
                                          new URL(pageUrl).openConnection();
    connection.setRequestMethod("GET");
    connection.setRequestProperty
                             ("Authorization", "Bearer " + user.getToken());

    // Try to get the content of the page
    try (BufferedReader reader = new BufferedReader
                        (new InputStreamReader(connection.getInputStream())))
       {
        StringBuilder content = new StringBuilder();
        String line;
        while ((line = reader.readLine()) != null) {
            content.append(line);
        }
        return content.toString();
    } catch (IOException e) {
        return "Access Denied";
    }
}
```
So, we made two users: an admin and a regular person.
Then we tried to look at a page and see if the visitors who weren't supposed to be there got blocked.