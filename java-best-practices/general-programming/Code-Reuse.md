### Code Reuse
Code reuse is the principle of using existing code instead of righting duplicate code.
It is also know as "Don't repeat yourself".

Take this use case for example:
```
        for (String item: list1) {
            System.out.println(item);
        }

        for (String item: list2) {
            System.out.println(item);
        }
```
Here we have two very simple for loops that print every item in a list of strings.

The correct usage of such code will be to extract it to a method that looks like this:
```
    private void printList(List<String> list){
        for (String item: list) {
            System.out.println(item);
        }
    }
  ```
  And then calling it with our two lists:
  ```
        printList(list1);
        printList(list2);
  ```
  This way we are ensuring a consistent behavior and saving duplicated code.
  Moreover, if we need to extend the functionality of this method we only need to do it in one place.
  
  For example:

```
    private void printList(List<String> list){
        if (list.size()<10){
            for (String item: list) {
                System.out.println(item);
            }
        }else{
            System.out.println("List has more than 10 items");
        }
    }
```
Now think of how much duplicated code we could have written if we didn't have a single function to handle this.
And of course, the more complex your code is, the more important the concept of code reuse becomes.