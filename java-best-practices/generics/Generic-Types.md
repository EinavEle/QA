Two great features of generics:
1. Types are checked at compile time.
2. Casting is done automatically for you.


This is why we should prefer using generic types when possible.
Let's take the Java `Stack` example:
```
public class Stack<E> extends Vector<E>
```
The `E` in Stack<E> is a type parameter that tells us what elements are going to be used with this `Stack`. In other words, it tells us a stack of which element.
For example, `Stack<String>` means a stack of strings, `List<Integer>` is a list of integers and so on..

### Do not use raw types
Whenever a class has a generic implementation, we should use it and not ignore it.
However, we should never use raw types.

|||important
Raw type means using a generic type without its type parameter.
|||

Here is an example of what not to do:
```
//Don't do this!
List list = new ArrayList();
list.add(new Object());
list.add("Shalom");
```
This code compiles and runs just fine, but it is written very poorly and generates warnings that tell us we should not use a raw type.

This usage robs us of all the good that generic types provide.
First of all, I cannot know for sure which type of objects this list contains but if we do it like this, it will be a lot clearer:
```
        // using a generic to specify a list of strings
        List<String> list = new ArrayList<>();
        list.add(new Object());
        list.add("Shalom");
```
However, the second line above gives me an error saying you can't put an `Object` into a list of `String`. This would allow me later on to use any element of this list as a `String`, without needing to cast it to a `String` explicitly.
```
        
        List list = new ArrayList<>();
        list.add(new Object());
        list.add("Shalom");
        //Casting to string is a must, since this is a raw list
        String s = (String)list.get(1);
```
In this case I know it's a `String` but it's not always the case.

To summarize, When we use the generic types correctly we do not need casting and we get appropriate errors at compile time whenever we are doing something wrong.