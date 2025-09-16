Write a stock management program with these requirements:

### Item
Item is a class that has:
- Name (can be generated randomly)
- Type - Enum of product types
- Expiration Date
- Weight
- Items should be sorted by expiration date by default.

### Stock
The stock is a list of generated items.
It has the following functionality:
- Generate item and add to list.
- Get a list of expired items.
- Get the item with the closest expiry date.
- Get a list of items sorted alphabetically.
- Get one item by name.
- Get a list of names of items above a certain weight - the list should be of names and not of items.
- Get a hash map of <type, Integer> to sum all the items according to their type.
