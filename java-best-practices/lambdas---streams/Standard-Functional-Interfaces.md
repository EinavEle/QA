The `java.util.function` package contains 43 functional interfaces.
There are even more functional interfaces running around the Java libraries.
You are not expected to remember, or even know, all of them. Nor is it necessary.
Most interfaces are very similar to each other and they all stem from a few "root" interfaces which you do need to understand and use.
### Consumer
Gets an argument and returns nothing.
You use it when you want to perform an action using an object, but you have nothing to return.
Example:
```
Consumer<String> cons = text -> System.out.println(text);
```

### Supplier
Gets no argument but returns something.
The most common use is factories.
Example:
```
Supplier<Student> studentMaker = () -> new Student();
```

### Predicate
A function that gets an object and returns a boolean.
Example:
```
Predicate<Student> isHigh = student -> student.getHeight() > 1.80;
```

### Function
Gets an object of type T and returns an object of type R.
Example:
```
Function<Student, Long> studentAge = student -> ChronoUnit.YEARS.between(LocalDateTime.now(),student.getBirthDate());
```
<B>*Most other functional interfaces are extensions of these four.</b>

### Operators
There are two very useful functional interfaces that extend `Function`.
They both accept and return the same type, so they can become very handy.
#### UnaryOperator
Accepts one object and returns an object of the same type.
```
UnaryOperator<String> doubleString = str -> str.repeat(2);
```
#### BinaryOperator
Accepts two objects of the same type and returns one.
```
BinaryOperator<String> connectStrings = (str1, str2) ->  str1 + str2;
```



### Primitives support
`java.util.function` also has functional interfaces that support primitives, so we don't have to autobox them into boxed primitives.
For example, if we use a predicate that accepts `int` we would have to use `Integer` because all functional interfaces use generics and thus do not support primitives.
```
Predicate<Integer> higherThanTen = i -> i>10;
```        
This will autobox any `int` we use into an `Integer`.
And this is the `IntPredicate` which can execute the same logic without the autoboxing.
```
IntPredicate primitiveHigherThanTen = i -> i>10;
```
Like the `IntPredicate`, we have the `LongFunction<R>`, `DoubleUnaryOperator` and so on.
So if you are using primitives, it's better to use these functional interfaces.

### Using your own functional interfaces
While not impossible, it is most of the time not recommended to write your own functional interfaces.
As stated a lot of times in the past, we always want to make our code usable and easy to understand. Using the standard functional interfaces accomplishes this task perfectly.
And besides, the existing interfaces cover so many options that you will probably find something that suits your needs.