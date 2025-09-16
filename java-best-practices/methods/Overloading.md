Overloading is the practice of having multiple methods with the same name but different parameters, to handle different cases of a similar operation.
For example:
```
  public void println() {
    newLine();
  }

  public void println(int x) {
      if (getClass() == PrintStream.class) {
          writeln(String.valueOf(x));
      } else {
          synchronized (this) {
              print(x);
              newLine();
          }
      }
  }
```
These are two overloads (there are many more) of the `println()` method, one accepts no parameters and the second accepts `int`.
Many times, it's very helpful to provide different options of calling a method. But, there are some things we need to consider when doing so:
### Avoiding confusing overloads
Make sure the user of your methods knows exactly which overload is going to be called when using your methods.
We have two classes:
```
public class Car {
    public void drive() {
        System.out.println("Driving...");
    }
}

```
And
```
public class SportsCar extends Car {
    public void driveFast() {
        System.out.println("Vrrrrrrrooooooooooom");
    }
}

```

And we have a method:
```
    public static void drive(Car car){
        car.drive();
    }
    public static void drive(SportsCar car){
        car.drive();
    }
```
What would happen if we do this:
```
    public static void main(String[] args){
        Car cars[] = new Car[]{new Car(),new SportsCar()};
        for (Car car :
                cars) {
            System.out.println(car.getClass());
            drive(car);
        }
    }
```
And the result is:
```
class methods.Car
Driving...
class methods.SportsCar
Driving...
```
Why???

Didn't the compiler see that the second `Car` is a `SportsCar`?
The answer is no.
At compile time, the second car is first of all a `Car`, even though we are printing the type in runtime and we see that it really is - a `SportsCar`.
**Overloads are selected in compile time**. This is the source of the issue.
To avoid such uncertainties, we can avoid such overloads and determine the type 
```
    public static void drive(Car car){
        if(car instanceof SportsCar){
            ((SportsCar) car).driveFast();
        }else{
            car.drive();
        }
    }
```
The message should be clear: don't confuse the user, make your method's behavior clear.

### Forcing specific overload invocation
Following our first example, if absolutely necessary you can force the invocation of a specific overload by casting your object to the specific type.
```
drive((SportsCar) cars[1]);
```
Please take into account that if you reached a point when you are doing this, you probably have a prettier solution and shouldn't have used this overload in the first place.

### Avoid overloads with the same parameter count
In keeping with the current theme of "don't confuse the user" we should also avoid overloads with the same parameter count.
That's again to help the user understand which overload method is going to be called.
The exception to this is when using very different types that can never be confused with each other.

|||important
## Don't forget! 
You are allowed to call methods by different names and make everything clear.
|||


