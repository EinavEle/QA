For a method to function correctly, it needs to make sure the required parameters are provided with the values.
Here are a few ground rules and ideas regarding this topic.

### Early error detection
To make our code easier to debug, we would like to find errors as early as possible.
If our method needs a non-null object and should never get a null object, we should not wait for the inner code to fail. Instead, we should warn about the issue immediately.
```
    //Do not do this!
    public boolean isNameValid(Product product){
        //Do some stuff
        return !product.getName().contains("!");
    }
```
If `product` is null, this code will throw a `NullPointerException`.
The quicker and clearer way to handle this is to validate `product` is not null at the beginning of the method.
```
   public boolean isNameValid(Product product){
        Objects.requireNonNull(product);
        //Do some stuff
        return !product.getName().contains("!");
    }
```
In this case, `NullPointerException` will be thrown before anything else happens. It will save us running code that is doomed to fail and will alert us to fix the problem quicker.
This is especially critical in real-life scenarios where the null value can be passed between many different methods and the exception will be thrown long after the error actually occurred.
Once we take care of this validation, we make sure errors are detected and handled quickly.

### Objects.requireNonNull()
This method is a very comfortable solution to null validation, since it returns the object if it is not null and can be easily integrated in our code.
```
String name = Objects.requireNonNull(product).getName();
```
We can use this method as part of our first interaction with the object or as a standalone at the beginning of the method body.

### Assertions
Assertions are another way to check parameter validity.
```
    public void doSomething(int positiveNumber) {
        assert positiveNumber > 0;
    }
```
This code will throw an `AssertionError` if the number passed is not greater than 0.
Assertions will only throw exceptions when adding the --enableAssertions flag when running your program.
This means it is only used as an internal tool and will not affect your clients.
If we want to make this code throw errors anyway, we could do this:
```
if(positiveNumber > 0) throw new IllegalArgumentException("Number must be positive");
```

### Constructors
Constructors for this matter are just like any other function. They should validate that all given parameters have valid values and enable us to construct a valid and legal instance of this class.

### Don't over restrict
The purpose of parameter validation is to ensure the correct functioning of our code. 
We need to notice that we don't over do it by over restricting parameter values unnecessarily.
We only validate what is necessary for our code to function correctly.

### Don't recheck the method's logic
Take a look at this example:
```
    public boolean isNumberPositive(int number) {
        if(number > 0) throw new IllegalArgumentException("Number is not positive");
        return number > 0;
    }
```
This is obviously a silly example, but I believe you get the idea.
The parameter validation should not check the logic of the method only the validity of a parameter.
