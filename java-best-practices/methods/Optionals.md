`Optional` was presented in Java 8. It allows us to return an object which is possibly empty.
```
    public Optional<Car> findCarByLicense(int license) {
        for (Car car : cars) {
            if (car.getLicense() == license) {
                return Optional.of(car);
            }
        }
        return Optional.empty();
    }
```
This methods returns an `Optional` which is a wrapper generic type that may include one `Car` or be empty.
The `Optional` object enables us to handle objects that may be empty more fluidly.
```
    public void driveCar(int license){
        Car foundCar = findMyCar(license).orElse(DEFAULT_CAR);
        foundCar.drive();
    }
```
Or
```
Car foundCar = findMyCar(license).orElseThrow(() -> new RuntimeException("Car not found"));
```
Or many other possibilities.
The most basic thing we can do is to simply check if a `Car` is present in this optional.
```
boolean haveACar = findMyCar(license).isPresent();
```
If we know that the item is definitely present in the `Optional`,
we can simply get it.
```
Car car = findMyCar(license).get();
```
We should be careful when using `get()` without checking that there is a `Car` there. Otherwise, `NoSuchElementException` will be thrown.


### When *not* to use optionals
- When returning boxed primitives.
A boxed primitive is already a wrapper of a primitive type. No reason to use another wrapper to wrap the wrapper.
There are helper objects: `OptionalInt`, `OptionalDouble` etc.. that provide almost the same functionality without the double wrapping.
- Performance sensitive programs may suffer from using too many optionals, since `Optional` is an object that needs to be allocated. If you need a very fast response time, it may be better to return `null`s instead of empty `Optional`s.
- As keys/values in `Map`s.
Using `Optional` as a map key will cause your code to be more complicated and makes the `containsKey()` functionality of `Map` useless.
