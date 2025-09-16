Write the following test by AAA pattern

-> Customer enters the bank's website
-> Enters username and password
-> Enters the bank account page 
-> Makes a deposit of 500 NIS
-> Then makes a bank transfer of 600 NIS 
Expected:  to receive a rejection notice

<details>
  <summary>
     Solution
  </summary>

```java
@Test
public void negative_transfer() {
    // Arrange
    int sumToTransfer = 600;
    int sumToDeposit = 500;
    BankAccountAction bankAccountAction = new BankAccountAction();
    bankAccountAction.depositMoney(sumToDeposit);

    // Act
    boolean result = bankAccountAction.makeTransfer(sumToTransfer);

    // Assert
    assertFalse("Transfer was successful even though there is not enough
                  money in the account", result);
}
```
</details>