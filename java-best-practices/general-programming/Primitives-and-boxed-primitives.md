It's important to understand the difference between primitive types and boxed primitives.

|||info
primitives (int, long, double...) are not objects and they represent raw values.
Boxed primitives (Integer, Long, Double...) are objects which means they can have null values and they behave differently in some situations.
|||
Another important factor is that boxed primitives take more space in the stack.
Generally, we will always want to use primitives unless we actually need the variable to be nullable.

### Defaults
```
int x;
public void printx(){
  System.out.println(x);
}

```
It should be obvious that this code will print `0`

but what about this?
```
Integer x;
public void printx(){
  System.out.println(x);
}
```
This code will print `null` since Integer is an object and `null` is the default value of objects.

