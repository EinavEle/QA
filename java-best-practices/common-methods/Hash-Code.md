The `hashCode()` function is used to return a unique int value for an object and improve the performance of `HashSet`, `HashMap` or any other hash-based collection.

This is the contract of `hashCode()` as described in the Object class of Java:
The general contract of hashCode is:
- Whenever it is invoked on the same object more than once during an execution of a Java application, the hashCode method must consistently return the same integer, provided no information used in equals comparisons on the object is modified. This integer need not remain consistent from one execution of an application to another execution of the same application.
- If two objects are equal according to the equals method, then calling the hashCode method on each of the two objects must produce the same integer result.
- It is not required that if two objects are unequal according to the equals method, then calling the hashCode method on each of the two objects must produce distinct integer results. However, the programmer should be aware that producing distinct integer results for unequal objects may improve the performance of hash tables.

As a general rule, you don't need to override `hashCode()` but <b>if you override `equals()` you must override `hashCode()`</b>.
Otherwise, you will encounter unpredictable behavior when using `HashMap` or other hash tables.

Equal objects must have equal hash codes.
Take for example the case of our `Person` class:
```
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

    @Override
    public boolean equals(Object o) {
        if (this == o) return true;
        if (!(o instanceof Person)) return false;
        Person person = (Person) o;
        return age == person.age && Objects.equals(name, person.name);
    }
  }
```
In this example our class does not override `hashCode()` and for this reason look what happens when we use it in a `HashMap`:
```
    public static void main(String[] args ){
        Person shlomy = new Person("Shlomy", 45);
        HashMap<Person, String> addressBook = new HashMap<>();
        addressBook.put(shlomy,"Pinhasi 88 Netanya");
        //...
        Person shlomy1 = new Person("Shlomy", 45);
        addressBook.put(shlomy1,"Pinsker 2 Tel Aviv");
        for (Iterator<Map.Entry<Person, String>> i = addressBook.entrySet().iterator(); i.hasNext();) {
            System.out.println(i.next());
        }
    }
```
If `shlomy` and `shlomy1` are equal, and we use them as a key in our `HashMap` you would expect the second `put()` to replace shlomy's address in the address book.
But the result of this function is this:
```
Person{name='Shlomy', age=45}=Pinhasi 88 Netanya
Person{name='Shlomy', age=45}=Pinsker 2 Tel Aviv
```
Why?
That's right, because in our `Person` class we did not override `hashCode()`. This means that when the `HashMap` calls `hashCode()` for these two instances of `Person` it gets a different result, which then means it is considered a different object.

So... how do we fix it?
We override the `hashCode()` function to match our `equals()` implementation.
```
    @Override
    public int hashCode() {
        int result = 1;
        result = 31 * result + name.hashCode();
        result = 31 * result + age;
        return result;
    }
```
This calculation of `hashCode()` is a Java standard and does a good, performant job.
When we override `hashCode()`, this is the new output of the previous method:
```
Person{name='Shlomy', age=45}=Pinsker 2 Tel Aviv
```
The `HashMap` now considers the two shlomys to be the same object, just as we did when we decided that having the same `name` and `age` makes `Person`s equal.

### Objects.hash()
The `Objects.hash()` method allows us to calculate the hash code of an array of objects without doing so manually.
These two examples would yield the same result:
```
    @Override
    public int hashCode() {
        int result = 1;
        result = 31 * result + name.hashCode();
        result = 31 * result + age;
        return result;
    }
```

```
    @Override
    public int hashCode() {
        return Objects.hash(name, age);
    }
```
While the top example shows the exact calculation, using the bottom example is much simpler and will give the same hash code.
If performance is critical to your application, you must take into account the fact that `Objects.hash()` creates an array out of your objects and autoboxes any primitive type.
This is surely not a huge deal in most cases but it can affect performance in performance-sensitive situations.