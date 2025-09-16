Create a `Farm` class that can generate different type of animals
### The `Animal` has this functionality:
- It can `move()`.
- It has a `gender`.
- It has an `id`.
- It has `weight`.
- It can `mate(Animal partner)` and create a new animal of its type (only with the opposite gender).


### The `Farm` has the following capabilities:
- It has a list of `Animals`
- When the `Farm` is initialized it should be randomly filled with some `Animal`s
- It can create new `Animal`s by the `mate()` function of existing `Animal`s
- It can `acquire()` new `Animal`s - meaning generating new animals and adding them to the list
When trying to `acquire()` a new animal the farm should check the possibility of mating existing animals of the requested type
- It can provide `Animal`s to outside users (and remove them from the list)
- when a framer requests an animal type that does not exist in the list, the farm should `acquire()` a new one.

### The `Farmer` can do the following:
- He can make an animal move.
- He can request an animal from the `Farm`.
- He has it's own animal list (separated from the farm)
- He can provide the client with a list of animals by type and id
Example:
1 - Dog
2 - Cow
3 - Dog
4 - Horse

### Tasks:
- Create 3 different types of `Animal` in the farm. `Animal` should be an interface.
- Create a skeletal implementation abstract class for `Animal`.


### Additional information:
- The client code can only interact with the `Farmer` so other classes should not be accessible
- The client code does not know the `Animal` types so you can use an enum to tell the farmer what type of animal to use

<b> * Consider immutability carefully

