|||important
Mutability is the ability of a class to be changed, whether from within or by the user.
|||
A mutable class is a class whose data can be modified after it is created:
```
public class Person{
  private String name;
  private int age;

  public void setName(String name){
    this.name = name;
  }

  public void setAge(int age){
    this.age = age;
  }
}
```
This is a simple mutable class.
It is mutable because its data can be modified.
Here is how we can make it immutable (once created, it cannot be modified):
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
Notice that the purpose of the `final` keyword is to hint (to us and the compiler) that this variable cannot be changed once it is set.

### Minimizing mutability
Immutable classes are easier to use, design, implement, and are less prone to errors.
Whenever we don't have to make our classes mutable, we should prefer immutability.
To enforce immutability on a class we need the following:
- The class is final - no subclass can trick the user and make it appear like the class is mutable.
- No setter methods - no one can change the data.
- All fields are final - they are only set once.
- All fields are private - only the enclosing class can access them.

# Immutable objects performance
Since immutable objects never change, we can reuse them without risk.
If we take our previous example, we can provide static factory methods to return specific persons since the `Person` object will never change:
```
public static final Person YOSSI = new Person("Yossi", 34);
public static final Person SHIMON = new Person("Shimon", 56);
```

This way, Yossi and Shimon are initialized once and then reused whenever they are called.

We could improve performance by using <b>lazy initialization</b> (AKA "lazy loading") like so:
```
private static Person shimon;
public static getShimon(){
  if(shimon==null){
    shimon = new Person("Shimon", 56);
  }
  return shimon;
} 
```

In this case, if creating a new `Person` is an expansive action we only do it when we need `shimon` for the first time.
Then we cache the result and reuse it when needed.


### * Classes should be immutable unless there is a very good reason to make them mutable!

When we do write a mutable class, we should make sure we minimize the mutable parts as much as possible. Meaning, we can should use final fields for variables that are never going to change.
For example
```
public class Person {
    private final String name;
    private String address;

    public Person(String name, String address) {
        this.name = name;
        this.address = address;
    }

    public String getName() {
        return name;
    }

    public void setAddress(String address){
      this.address = address; 
    }

    public String getAddress(){
      return address;
    }
}
```

In this case, we are saying that a person's name can never be changed but his address can.

By making the `name` final we help the reader of the code understand the intended behavior of this class and make him less likely to try and change the name by mistake.

Also note there is no setter method for `name`!

### Constructing an instance
When constructing an instance, make sure you build it with its initial state and not return "partially initialized" objects.
```
//This is a partailly initiaized Person
Person moshe = new Person("Moshe", 88);
moshe.setAddress("Rabin 2 Holon");
moshe.setFavoriteFood("Pizza");
//Now moshe is initialized
```
There is no benefit to having partially initialized objects - it just leaves room for errors.
So we should do this:
```
Person moshe = new Person("Moshe", 88, "Rabin 2 Holon", "Pizza");
```
We could also use a **builder** (which we will learn in future classes).
