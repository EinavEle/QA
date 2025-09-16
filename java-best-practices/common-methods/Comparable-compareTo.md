While `compareTo()` is not a common `Object` method, it does belong to the `Comparable` interface.
We are discussing it in this class because it is very similar in usage and function to the rest of the common methods, especially `equals()`.

### The `Comparable` interface
The `Comparable` interface is a very simple one and has only one method in it.
```
public interface Comparable<T> {
     public int compareTo(T o);
}
```
Implementing this interface means that your class has a natural order and can be easily sorted by `Arrays.sort()` or any other generic sorting method.
Since the implementation of `Comparable` is pretty quick and requires little effort, it is recommended to use it most of the time.

The contract of `compareTo()` may look a bit intimidating, so let's just say that it should behave like `equals()`: return -1, 0, 1 to indicate if x is less than, equal to, or greater than y.

This is an example of a `compareTo()` method that sorts our `Person` by age:
```
    @Override
    public int compareTo(Person o) {
        if (this.age < o.age) return -1;
        if (this.age == o.age) return 0;
        return 1;
    }
```
Since `age` is an `int` we could have just used the `Integer.compare()` method that does exactly the same thing.
```
    @Override
    public int compareTo(Person o) {
        return Integer.compare(age, o.age);
    }
```
This is `Integer.compare()`:
```
    public static int compare(int x, int y) {
        return (x < y) ? -1 : ((x == y) ? 0 : 1);
    }
```
If we wanted to sort our `Person` by name and then age, it would look like this:
```
    @Override
    public int compareTo(Person o) {
        int result = name.compareTo(o.name);
        if(result == 0){
            return Integer.compare(age, o.age);
        }else{
            return result;
        }
    }
```
This methods compares the `name` and if the names are equal it then compares by `age`.

To summarize, when writing your own classes, you should consider implementing `Comparable` if there is a natural ordering relevant to your class.
