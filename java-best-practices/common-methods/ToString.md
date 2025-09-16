The `toString()` function represents an object as text.
It is automatically called when calling `println()`, in logging, and more.
The default `toString()` implementation is kind of useless and will give our `Person` class this result when printed:
Code:
```
Person shlomy = new Person("Shlomy", 45);
System.out.println(shlomy);
```
Result:
```
Person@de43420a
```

This is why it's important to always override `toString()` with the real data the class represents:
```
    @Override
    public String toString() {
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                '}';
    }
```
Then running our code will print:
```
Person{name='Shlomy', age=45}
```

### Things to consider
- In bigger classes with a lot of fields, you may consider printing only the most important data and not all of it.
- Do not use `toString()` as an API!
If you expose in your `toString()` function data that would otherwise be hidden from the user, like a private field, you break encapsulation and give the user a 'back door' to the class's inner workings.
- Take into account the usage and backwards support of your `toString()` function.
If your classes are widely used, their `toString()` function may be used and parsed in many ways by its users.
So, make sure you commit to your `toString()` method or declare explicitly that it is prone to changes.