In the Java language, we have two types of variables: primitives and reference types (or objects).
### Primitives
The primitive types are `int`, `byte`, `short`, `long`, `float`, `double`, `boolean` and `char` and they represent raw values.
Primitives have a smaller memory footprint since they have nothing but the raw value itself.

Example of using a primitive type:
```
int x = 1;
System.out.println(x+1);

char c = 'c';
System.out.println(c);
```
### Objects
Objects, on the other hand, are much more complex. 
They are initialized with a constructor and they can have unlimited functionality added to them.
In fact, most of what happens in our code are interactions between objects.
Example of initializing an object:
```
Student yossi = new Student("Yossi", 1231, 1.68, LocalDateTime.of(2000, 1, 1, 0, 0));
```

### Boxed primitives
All primitives have a corresponding Java class that provides extra functionality and also enables us to use these types where an object is required (in generics, for example).
These are called boxed primitives.
For example:
```
Integer x = 1;
```
Value wise, it is equal to:
```
int x = 1;
```
However, `Integer` can be null, and it has other capabilities that `int` doesn't.
When creating an `Integer` (or any other boxed primitive) we do not have to use the `new` keyword. 
Java creates the object with the given value automatically.
These two statements will yield the same result:
```
        Integer y = 1;
        Integer z = Integer.valueOf(1);
```
We will cover more about boxing and autoboxing in future lessons.