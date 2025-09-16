Generic methods are an effective way to generalize your code and make it more flexible and reusable.
Whenever your method's return type may be dependent on the usage, you might want to make it generic.
The "old" way of doing such a thing is this:
Say we have a class that has an internal map of <String, Object>, BTW `Map<K,V>` is a great example of using generics :)

```
    Map<String,Object> items = new HashMap<>();
    
    public Object get(String key){
        return items.get(key);
    }
```
This method is used to return an object by a given key.
What if the user knows the exact type of the object he/she is looking for?
They might do this:
```
Person shmulik = (Person)myMap.get("shmulik");
```
This will work, but it will make us cast the object every time we use the method.
With a small addition we can make this method generic:
```
    public <T> T get(String key){
        return (T)items.get(key);
    }
```
Now, getting our "shmulik" will be a bit prettier:
```
Person shmulik = myMap.get("shmulik");
```
In this particular case, we just moved the cast from the user to inside the function.
This is just a small demonstration of the capabilities of generics.

With generic methods, we can also return subtypes and implementations:
```
public <T extends BaseClass> T something() {
  if(something){
    return new SubClassA();
  }else{
    return new SubClassB();
  }
}
```
This method can return an object of any type that extends `BaseClass`.
This can be very helpful and can make our code very user-friendly.
The expression `<T extends BaseClass>` is called "Bounded type parameter", because the type is bound to another type.

### The ? Wildcards
While using T allows us to return different types, using `?` enables us to get different types as parameters, unrelated to `T`.
```
    public <T> T getAndConvert(List<T> list, int index){
        return (T) list.get(index);
    }
```
This simple code is redundant, it casts an item from a list of `T` to `T`. We could have simply done this:
```
    public <T> T getAndConvert(List<T> list, int index){
        return list.get(index);
    }
```
But, what if we want to use a list of a different type?
```
    public <T> T getAndConvert(List<?> list, int index){
        return (T) list.get(index);
    }
```
In this example, we get an unchecked cast warning. But, if we were to work with a correct hierarchy it could make sense.
You can also use
```
<? super SomeType>
```
If you want the acceptable type to be a parent class of `SomeType`.
