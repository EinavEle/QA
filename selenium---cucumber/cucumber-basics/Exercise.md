In this exercise you will write a few simple tests using Cucumber and Selenium.

We will be testing this site:
https://www.selenium.dev/documentation/
1. Write a few tests for the Selenium documentation site.
2. Use POM to model the pages and components you are going to test.
3. Ideas for tests:
a) Side menu navigation and sub items
b) Navigating via breadcrumbs
4. Test example:
```Cucumber
Given I’m on the Selenium documentation site
When On the sidebar - I click ‘WebDriver’
Then On the sidebar - ‘WebDriver’ submenu appears
And I’m on the ‘WebDriver’ documentation page
```
5. Write at least 5 tests