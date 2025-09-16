Write a test using Gherkin Cucumber that explains how you withdraw money from a bank account.
Divide the steps as we learned in class, remember it should be simple and readable for anyone regardless of their understanding of the world of automation.
<details>
  <summary>
    Solution
  </summary>

```Cucumber
Given I have $100 in my checking account
When I withdraw $20 from my checking account
Then I have $80 in my checking account 
```

</details>