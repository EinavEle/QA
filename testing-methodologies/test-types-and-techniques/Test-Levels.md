# Unit Tests

In software testing levels, Unit Testing is the process of testing individual units or components of software code. 
It is usually performed by developers during the coding phase of software development. Unit Testing involves testing each unit or module of code in isolation from the rest of the system, to ensure that it behaves as expected and meets its design specifications. 
The primary goal of Unit Testing is to identify defects early in the development cycle and ensure that each unit of code is working correctly before it's integrated with other modules or components of the system.
Here a example for function named ‘calculateSum’ that takes in an array of integers and returns their sum:
```java
@Test
    public void testCalculateSum() {
        int[] numbers = {1, 2, 3, 4, 5};
        int expectedSum = 15;
        int actualSum = CalculateSum.calculateSum(numbers);
        assertEquals(expectedSum, actualSum);
    }
```
In this example, we import the Assert class from the JUnit framework and define a test case method named testCalculateSum. 
We define an array of integers and an expected sum, and then call the calculateSum function with the array as an argument. 
We use the assertEquals method to compare the expected sum with the actual sum returned by the calculateSum function. 
If the two values match, the test case passes; if they don't, the test case fails. 
This unit test helps ensure that the calculateSum function works correctly for a given input and meets its design specifications.
# Integration Tests (AKA Component Tests)
Integration Testing, also known as Component Testing, is a software testing level where individual software components are tested together as a group. 
The purpose of Integration Testing is to verify that the components interact with each other as expected and that the system works as a whole. 
It involves testing the interfaces between the components and the data flow between them. 
Integration Testing is performed after Unit Testing and before System Testing. 
It helps detect defects that may arise from the interaction between components and ensures that the software meets the design specifications.

Consider an e-commerce application with the following components:
1. User Interface (UI)
2. Shopping Cart
3. Inventory Management
4. Payment Gateway

An integration test for this system could involve:

1. Simulating a user adding a product to the shopping cart through the UI.
1.  Verifying the UI communicates with the shopping cart correctly.
1.  Checking if the shopping cart adds the product to the cart.
1.  Simulating the user proceeding to checkout.
1.  Verifying the shopping cart communicates with the inventory management to check product availability.
1.  Checking if the inventory management responds with the appropriate stock status.
1.  Simulating the user completing the payment process.
1.  Verifying the shopping cart communicates with the payment gateway and sends payment details.
1.  Checking if the payment gateway processes the payment successfully.
1.  Validating the UI displays the appropriate response.
This example demonstrates how integration tests verify the interactions and data flow between components to ensure the overall functionality of the system.
# System Testing
​​System Testing tests the entire software system to ensure it meets the requirements and works in a real-world environment. 
It verifies the user interface, functionality, performance, reliability, security, and compatibility. 
Test cases cover different scenarios to identify defects and ensure the system works when all components are integrated. 
Examples include testing a web application across different browsers or a mobile app for performance and security. 
System Testing is important to meet customer requirements and work as expected.

For example, we can make all the preparations for our tests using the api service and check that the products are shown in the ui interface, on an ecommerce site we would like to add a product to the cart using an api call and we can check on the site itself if the product is in the cart, another example is testing the same cart in different browsers, we will expect to see the The same result in any type of browser defined by the customer.
