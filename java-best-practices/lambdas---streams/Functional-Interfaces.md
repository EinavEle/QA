### Then: Function Objects, Now: Lambdas

In the old days, when we wanted to pass an anonymous function, we would have had to instantiate a function object:
```
        Runnable run = new Runnable() {
            @Override
            public void run() {
                System.out.println("Hello");
            }
        };
``` 
This `Runnable` is an anonymous class, we can pass it anywhere and use its `run()` function.
To be clear, this `Runnable` is an anonymous class because `Runnable` is a functional interface which we implemented without using a class.
As you can see, there is a lot of boilerplate code around the actual functionality of this runnable.
The new lambda interface allows us to pass the same functionality with much less code.
```
() -> System.out.println("Hello");
```
This lambda is doing the exact same thing as the anonymous class above, only with a lot less code.
This is what functional interfaces are all about.
Java understands that when you are writing this you mean to implement the `run()` method of the `Runnable` functional interface.

|||info
## Definition

A functional interface is an interface with exactly one abstract method that can be instantiated by using a lambda/method reference/constructor that implements this one method.
|||

Later in this class we will look at the most common functional interfaces and see how to use them.

We can also pass parameters to our lambda like this:
```
(x)-> x+" and more";
```
This simple lambda will add " and more" to a given string.

But wait, where are the types in this lambda?

### Type inference
This lambda `(x)-> x+" and more";` has two parameters in it, `x` and the returned value.
What are their types?
I already told you it's `String` but it is not written anywhere...
In fact we could have written it like this:
```
Function<String, String> test = (String x) -> x + " and more";
```
Here we explicitly stated that `x` is of type `String` and the return type of this function is also a `String`. In most cases it is not necessary because Java uses what's called type inference, which means it figures out the types based on the context of your code.
For example, if you are using the `Comperator` functional interface, it is obvious that you are comparing objects of a specific type.
```
List<Student> students = new ArrayList<>();
students.sort((stu1,stu2)->Double.compare(stu1.getHeight(),stu2.getHeight()));
```
Here, we are not stating that `stu1` and `stu2` are of type `Student` but Java understands it through type inference.

|||info
Though Java can most of the time infer the types of the parameters in your lambdas, it is sometimes good to declare these types explicitly, especially if it is not obvious to the user.
|||
There is an even prettier and shorter way to sort the students by height.
We'll take a look in the next section.