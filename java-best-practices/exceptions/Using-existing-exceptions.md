`Throwable` same as `Exception` and `RuntimeException` is extensible.
Meaning you can easily write your own exceptions and have them extend one of these main classes.
But usually you don't actually have to (or want to) do this.
Using your own exceptions might seem fancy but more often than not they will just make the learning curve of your code steeper.
Most Java programmers are familiar with the common Java exceptions and you will make their lives a lot easier if you just use them.
This rule is not true only to exceptions BTW...
The most commonly used exceptions in Java are:
- `IllegalArgumentException`
You should throw this exception whenever you get an argument that did not pass the validation for your method.
```
public void printPositiveNumber(int positiveNum){
  if(positiveNum < 0){
    throw new IllegalArgumentException("Number should be positive but was " + positiveNum);
  }else{
    System.out.println(positiveNum);
  }
}
```
- `IllegalStateException`
You should throw this exception when the object being operated on is not in the correct state, for example not fully initialized.
```
public void use() {
        if (!isInitialized) {
            throw new IllegalStateException("Object is not initialized");
        }
        //do stuff
    }
```
- `NullPointerException`
This is thrown when an object that shouldn't be null is null.
```
    public void startCar(){
        if(engine == null){
            throw new NullPointerException();
        }
        //Start car
    }
```
- `IndexOutOfBoundsException`
This exception is thrown when the index provided is outside the boundaries of a collection. This can also be regarded as `IllegalArgumentException` but is more case specific.
- `ConcurrentModificationException`
Thrown when an object is modified by two threads simultaneously.
- `UnsupportedOperationException`
Thrown when method is not supported on a specific object.
In most cases when partially implementing an interface or in skeletal implementations where a method is expected to be overridden by subclass.

In many cases we can use a more specific and appropriate exception but in general, these cover a lot, and if we are using more specific exceptions, it is better to choose them from the Java libraries so that other programmers are more familiar with them.