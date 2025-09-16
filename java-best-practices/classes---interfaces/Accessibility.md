How accessible do our are classes, methods, and fields need to be?
Well, the less accessible the better.
Minimizing accessibility helps us with decoupling and with hiding the inner workings of our components.
This is called encapsulation.
Whether we look at a small class or a huge module, we always want to expose only what absolutely necessary, because whatever is public and used by others must be supported at all times.

# Accessibility modifiers
There are three types of accessibility modifiers available for classes:
1. **Package private:**
This class will be accessible from everywhere within the package, but not outside the package.
2. **Public:**
This class will be accessible from everywhere.
3. **Private:**
Only for inner classes - this class will only be accessible by it's outer class

Let's take a look at an example - the PackageSize class is only available inside ShopItem:
```
class ShopItem {
    private int id;
    private String name;
    private double price;
    private PackageSize packageSize;

    private class PackageSize{
        private int width;
        private int height;
    }
}
```

### For methods and fields
1.** Private:**
Only accessible from within the class.
2. **Package private:**
Accessible from classes within the package.
3. **Protected:**
Accessible from within the class and from subclasses.
4. **Public:**
Accessible everywhere.

As a general rule, we want to minimize accessibility so that only what must be executed by the user of the class will be exposed.
The public part of a class is its API.
Here is an example:
```
public class Shop {
    private List<ShopItem> inventory;

    Shop(List<ShopItem> inventory) {
        this.inventory = inventory;
    }

    public boolean isItemAvailable(String itemName) {
        for (ShopItem item :
                inventory) {
            if (item.getName().equals(itemName)) {
                return true;
            }
        }
        return false;
    }
}
```
In this very simple example, you can see that the shop's inventory is private and a user cannot access it from outside the class itself.
However, in order to be usable the shop provides a method `isItemAvailable()` that tells the user if the item exists or not.
By design, the user shouldn't care how the answer is given.
It is an API that the shop provides and that's it.
In the future, a lot of complex checks and calculations could affect the question of whether the item is available, but the shop's user would never know about it.
For all the user cares, it could be something like this:
```
public boolean isItemAvailable(String itemName) {
  internalIsItemAvailable(itemName);
}
```
Where `internalIsItemAvailable()` could be anything...

The `isItemAvailable()` method is the shop's API and all other non public members are the implementation.


|||important
We should always consider which part of our code is implementing the API and which *is* the API
|||

# Accessor methods
Accessor methods are the way we access the public class's data from outside.
Let's look at our `ShopItem` example:
```
class ShopItem {
    private int id;
    private String name;
    private double price;
    private PackageSize packageSize;
...
    //Accessor method
    public double getPrice() {
        return price;
    }
    public void setPrice(double price) {
        this.price = price;
    }
}
```

In this case, you may think it's simpler to just make `price` public.
But...
The whole point of a class is to provide an API that would stay consistent, even when the implementation may change.
So in the future we can do this:
```

    public double getPrice() {
        return checkSalesAndCoupons(this.price);
    }

    public void setPrice(double price) {
        if(price < 10){
            this.price = 10;
        }else{
            this.price = price;    
        }
    }
```
Now, the user uses the API just the same but no longer gets the same response.
We just added some layers of implementation that change the behavior of our item.
This way, the class controls the behavior and logic of getting and setting data inside the class.
The user can only use these methods.