# *Intro*
In testing, setup and teardown are the steps before and after a test case.
Setup prepares everything needed for the test, like setting up objects and data.
Teardown cleans up after the test, restoring the environment to its original state.
These steps ensure tests are independent, consistent, and reliable.

# *Why Setup and Teardown Are Not "In The Test"*
Setup and teardown steps are kept separate from the test itself to distinguish technical setup and cleanup activities from the actual logic being tested. By separating them, it improves the readability and clarity of the test code.

In the test, the focus should be on the specific behavior or functionality being tested, while the setup and teardown handle the technical aspects like initializing objects, setting up test data, or cleaning up resources.

Deciding what goes in the test and what goes in the setup/teardown depends on maintaining a clear separation of concerns. The test should contain the steps that directly validate the expected behavior, while setup and teardown handle the necessary preparations and cleanup that are common to multiple tests.

Teardown is executed regardless of the test outcome to ensure a clean and consistent test environment. Even if the test fails, it is important to clean up any resources acquired during the setup phase to avoid interference with subsequent tests and to maintain the integrity of the testing environment.

# *Examples*
```java
import org.junit.jupiter.api.*;
import java.util.ArrayList;
import java.util.List;

public class ShoppingCartTest {
    private ShoppingCart shoppingCart;
    private List<Item> items;
    @BeforeEach
    public void setup() {
        // Perform setup activities, such as creating a shopping cart
          and adding items
        shoppingCart = new ShoppingCart();
        items = new ArrayList<>();
        // Add test data to the shopping cart
        items.add(new Item("Product A", 10.99));
        items.add(new Item("Product B", 5.99));
        // Add the items to the shopping cart
        for (Item item : items) {
            shoppingCart.addItem(item);
        }
    }
    @AfterEach
    public void teardown() {
        // Clean up resources or reset state, if necessary
        shoppingCart.clear();
    }
    @Test
    public void calculateTotalPrice_ShouldReturnCorrectTotal() {
        // Act
        double totalPrice = shoppingCart.calculateTotalPrice();
        // Assert
        assertEquals(16.98, totalPrice, 0.01);
    }
    @Test
    public void addItem_ShouldIncreaseItemCount() {
        // Arrange
        Item newItem = new Item("Product C", 7.99);
        // Act
        shoppingCart.addItem(newItem);
        int itemCount = shoppingCart.getItemCount();
        // Assert
        assertEquals(items.size() + 1, itemCount);
    }
}
```
In this example, the “setup” method is responsible for creating a “ShoppingCart” instance and adding test data (items) to it. 

The test data is prepared using a list and then added to the shopping cart using a loop.

The ”teardown” method is used to clean up the shopping cart after each test by clearing its contents. 

This ensures that the cart is reset to an initial state for the next test.

The example includes two test methods: “calculateTotalPrice_ShouldReturnCorrectTotal” and “addItem_ShouldIncreaseItemCount”.

Each test focuses on a specific behavior and utilizes the setup resources to perform the necessary actions and assertions.

By using setup to initialize the test data and teardown to reset the state, each test can run independently, avoiding interference between tests and ensuring reliable and consistent results.