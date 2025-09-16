Reflections are Java's way to give us access to class data at runtime.
Notice that I wrote "class" data and not "object" data.
Since a class is the blueprint of an object, we sometimes need to access this blueprint and not a specific object.
We can get access to the class data by using the `getClass()` method.
```
Class<?> clz = yossi.getClass();
```
In this case, `yossi` is an object of the type `Student`, but this piece of code doesn't have to know that.
Once we have the `Class` object we can use it to get info about the class itself.
This for example gets the class name:
```
System.out.println(clz.getName());
```
We can also extract methods and constructors out of this `Class` object.
Let's say we want to create another instance of the same type of `yossi`, we could look for a parameterless constructor in the class.
```
Constructor<?> constructor = clz.getConstructor();
```
Now we have an `Constructor` object that we can invoke, assuming there is a parameterless constructor for this class.
If there is no fitting constructor this code will throw `NoSuchMethodException`.
In case we did find a relevant constructor, we can then invoke it:
```
Object o = constructor.newInstance(null);
```

### Drawbacks of reflections
Before we see some more examples, we need to take into account the fact that using reflections usually means writing a lot of code, risking many errors, and losing a lot of the compiler's assistance.
Since we don't know a lot about the class at compile time, we have to make assumptions and write bulky code to handle errors and cast our objects.
Reflections are also very bad for performance and should be avoided for this reason.

### When to use
One very common example of using reflections can be found in our annotations class.
Since annotations provide data about classes, fields, and methods, some processes can access this data using reflections.
```
        Method[] methods = clz.getMethods();
        for (Method method : methods) {
            if(method.isAnnotationPresent(Override.class)){
                System.out.println(method.getName());
            }
        }
```
This code will print all the methods annotated with `@Override` for a specific class.
