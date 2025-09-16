The equals method normally tells us whether two instances of an object are the same.
For most objects, unless we use equals on the same instance, it will return false.
Since no matter the data inside the object, the instances of two objects are inherently different.
This will obviously return `true`:
```
Object obj = new Object();
return obj.equals(obj);
```

But this will return false, even though there is no difference in the value of these two objects:
```
Object o = new Object();
Object o1 = new Object();
return o.equals(o1);
```

This example is better understood with a real "value class".
Let's take our `Person`:
```
public class Person {
    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }
}
```

What do you think this will return?
```
    public static void main(String[] args ){
        Person shlomy = new Person("Shlomy", 45);
        Person shlomy1 = new Person("Shlomy", 45);
        System.out.println(shlomy.equals(shlomy1));
    }
```
I'm sure you got it, it returns false.                                                                                    
But should it return false?
When comparing "value objects" we most likely want them to return true if all their inner data is actually the same.
So what do we do?
We override `equals()` like so:
```
    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Person)) return false;
        Person person = (Person) o;
        return age == person.age && Objects.equals(name, person.name);
    }
```
This implementation of `equals()` will return `true` for the above example.

### When shouldn't we override `equals()`?
- When each instance of the class is unique even when the data is equal.
- When there is no need for a "logical equality" that compares data.
- When a superclass already overrides `equals()` and the subclasses can safely use it.
- When we are absolutely sure that `equals()` is not going to be called on an object.

### The `equals()` contract
There are a few rules we need to enforce in order for our `equals()` implementation to follow the general contract of `equals()` in Java.
The following is the contract as described in the `Object` class of Java:

The equals method implements an equivalence relation on non-null object references:
- It is **reflexive**: for any non-null reference value x, x.equals(x) should return true.
- It is **symmetric**: for any non-null reference values x and y, x.equals(y) should return true if and only if y.equals(x) returns true.
- It is **transitive**: for any non-null reference values x, y, and z, if x.equals(y) returns true and y.equals(z) returns true, then x.equals(z) should return true.
- It is **consistent**: for any non-null reference values x and y, multiple invocations of x.equals(y) consistently return true or consistently return false, provided no information used in equals comparisons on the objects is modified.
For any non-null reference value x, x.equals(null) should return false.
