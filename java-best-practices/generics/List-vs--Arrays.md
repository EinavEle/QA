`List`s and `Array`s are good examples of why it's good practice to use generics.
Let's take a simple example that shows how arrays work:
```
        Object[] strings = new String[20];
        strings[0] = 1;
```
This code compiles fine but fails at runtime.
Declaring an array of strings as `Object[]` is legal, the problem occurs only on the second line.
When this code runs, we get an `ArrayStoreException` because `int` 1 is not a `String` and our `Object` array is in fact a `String` array.
With `List`, there is no such issue.
```
List<Object> list = new ArrayList<String>();
```
This declaration won't compile, and will give an error saying that these types are not compatible.
Even though we can put a `String` into a list of `Object`, we cannot declare an `ArrayList<String>` as a `List<Object>`.
If we declare the `List` correctly and try to add an `int` to it, we will still get an error:
```
        List<String> list = new ArrayList<>();
        list.add(1)
```
But this time, the code won't compile and we will find the error sooner and not only at runtime.

In short, lists provide a safer and more robust implementation than using "naked" arrays. Just don't forget that behind many list implementation there is an array that stores the actual data.
