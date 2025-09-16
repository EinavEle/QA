Here is a long “flow” test.
Please divide this test into small tests according to the principles we learned:

-> Customer enters the bank's website 
-> enters user information
-> enters the bank account page 
-> makes a deposit of 500 NIS 
-> then makes a bank transfer of 600 NIS 
-> expect to receive a rejection notice

<details>
  <summary>
    Solution
  </summary>

Test 1:
-> Customer enters the bank's website 
Expected: The home page of bank site was show

Test 2:
-> Customer enters the bank's website
-> Enters username and password
- Expected: The full name of user was show

Test 3:
-> Customer enters the bank's website
-> Enters username and password
-> Enters the bank account page 
- Expected: the number account was show and account status

Test 4:
-> Customer enters the bank's website
-> Enters username and password
-> Enters the bank account page 
-> Makes a deposit of 500 NIS
- Expected: The amount in the account is updated to plus 500


Test 5:
-> Customer enters the bank's website
-> Enters username and password
-> Enters the bank account page 
-> Makes a deposit of 500 NIS
-> Then makes a bank transfer of 600 NIS 
- Expected:  to receive a rejection notice


</details>