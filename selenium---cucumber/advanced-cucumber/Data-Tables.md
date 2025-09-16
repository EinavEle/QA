# *What are data tables?*
Data tables let you give a bunch of related information to a feature file step all at once. 
They make scenarios easier to read and write by letting you do the same thing with different sets of data without repeating yourself.

In Cucumber, a data table looks like a table with columns and rows. 
Each column is a different thing you want to check, and each row is a different set of values for those things. 
For example, if you're testing a login feature, you could use a data table to try out a bunch of different usernames and passwords at once.

Here is an example of a data table in Cucumber:

```Cucumber
Then Verify user exists
| Name     | User Name           |
| Arbel    | arbel2021           |
| Gaya     | gaya2018            | 
| Elinor   | elinor1990          |
```
In this example, the Then step takes a data table that defines three users with their names. The step implementation can then use this data to verify the users in the system.

Data tables can be used with any step in a Cucumber scenario that takes parameters. 
The data in the table can be accessed in the step implementation using Cucumber's built-in data table API.
# *Data Table Usage*
1. Testing forms: Data tables can be used to test forms with multiple input fields, where each row of the table represents a different set of input values.
2. Testing search functionality: Data tables can be used to test search functionality with different search queries and expected search results.
3. Testing CRUD operations: Data tables can be used to test create, read, update, and delete (CRUD) operations on different types of data.
4. Testing user authentication: Data tables can be used to test user authentication with different usernames and passwords.
# *Data Table Standards*
Data table standards refer to the conventions and practices followed while writing and using data tables in feature files.
Here are some commonly followed data table standards in Cucumber:
1. Names: Column names should be written in lowercase and separated by vertical bars (|). 
Column names should be descriptive and meaningful.
Example:
    ```Cucumber
    | name  | age | email          |
    | Alice | 28  | alice@mail.com |
    | Bob   | 30  | bob@mail.com   |
    ```
2. Values: Data should be separated by vertical bars (|) and aligned with their respective column names.
Example:
    ```Cucumber
    | name  | age | email          |
    | Alice | 28  | alice@mail.com |
    | Bob   | 30  | bob@mail.com   |
    ```
3. Alignment: The values in each column should be aligned with each other to make the table easy to read.
Example:
    ```Cucumber
    | name  | age | email          |
    | Alice | 28  | alice@mail.com |
    | Bob   | 30  | bob@mail.com   |
    ```
4. Headers: The first row of the table should contain the column headers. If a header contains multiple words, they should be separated by underscores (_).
Example:
    ```Cucumber
    | first_name | last_name | age | email          |
    | Alice      | Smith     | 28  | alice@mail.com |
    | Bob        | Johnson   | 30  | bob@mail.com   |
    ```
5. Empty Cells: Empty cells should be represented by an empty space between vertical bars (| |).
Example:
    ```Cucumber
    | name  | age | email          |
    | Alice | 28  |                |
    | Bob   | 30  | bob@mail.com   |
    ```
# *Implementation* 
To implement data tables in Cucumber, follow these steps:
1. Create a scenario with a table in Cucumber.
    ```Cucumber
    When User enter credentials
      | Username   | Password |
      | testuser_1 | Test@123 |
      | testuser_2 | Test@456 |
    ```
2. Define an object that corresponds to the fields in the table.
    ```Cucumber
    public class Credentials
        {
            public string Username { get; set; }
            public string Password { get; set; }
        }
    ```
3. In the steps object, define the step that uses the table and receives a table type as a variable format.
    ```Cucumber
    @When("User enter credentials")
          public void WhenUserEnterCredentials(Table table)
          {

          }
    ```
4. To use the table, call the CreateSet() function and send the corresponding object as a parameter.
5. If the table has more than one row of data, use a foreach loop to iterate over all the rows.
    ```Cucumber
    @When("User enter credentials")
            public void WhenUserEnterCredentials(Table table)
            {
                var credentials = table.CreateSet<Credentials>();      
                foreach (var userData in credentials)
                {
                    driver.FindElement(By.Id("log")).SendKeys(userData.Username);
                    driver.FindElement(By.Id("pwd")).SendKeys(userData.Password);
                    driver.FindElement(By.Id("login")).Click();
                }
            }
    ```