Whenever an exception is thrown, we have a problem, it may be in our data, in the code, maybe just a runtime problem with our system.
In any case, we will want to know what happened and have as much data as we can.
Failure capture is the concept of providing this data with our exceptions so that it will be easier to investigate later.

```
throw new IllegalStateException();
```
This code does provide some information by telling us that the error is related to the object's state (which was illegal when this was thrown).
It is definitely more helpful than:

```
throw new Exception();
```
Which should never be used because it provides almost no information at all.

But there is a lot more we can do:
```
throw new IllegalStateException("The object is not fully initialized");
```
First of all we can add a message to describe the error to the user.
We can also print the objects state.
```
throw new IllegalStateException( String.format("The object is not fully initialized. Current state: %s", this));
```
If the error is a result of a different error we can use `initCause()` to include the internal error in our new thrown exception or use a constructor that receives the cause as a parameter.
```
    try{
        doSomething();
    } catch (FileNotFoundException e) {
        throw new IllegalStateException(e);
    }
```

The bottom line is, we should do our best to provide as much information as we can so errors can be investigated thoroughly.