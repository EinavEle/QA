### The setup:
- Class Warehouse has items in it.
- Class Headquarters can use the warehouse’s API, but can also modify the items directly.
- Class Client exists in a different package, and can get items only through the Headquarters.

### Questions
What are the access levels of: `Warehouse`, `Headquarters`, `Item` and why?
What is the access level the method `modifyItem()` inside `Item` should have?

<details>
<summary>Answer</summary>
Warehouse is package private because no one needs to use it from out side the package.
Headquarters is public because it is being used by Client.
Item is public because it is also being used by Client

modifyItems() should be package private because all classes in the package should be able to call it.
</details>