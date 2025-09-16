### What is a try-finally block
A `try-finally` block wraps code that might throw an exception, enabling us to handle exceptions and react to them accordingly.
The `final` part of this block is where we can put functionality we need to invoke once the operation is done, whether an exception was thrown or not.
This is an example from stackoverflow.com
```
FileOutputStream fos;
ObjectOutputStream oos;
try {
    fos = new FileOutputStream(file);
    oos = new ObjectOutputStream(fos);
    ...
    oos.writeObject(shapes);
    ...
} catch (FileNotFoundException ex) {
    // complain to user
} catch (IOException ex) {
    // notify user
} finally {
    if (oos != null) oos.close();
    if (fos != null) fos.close();
}
```

The problem with this example is that `oos.close()` and `fos.close()` can throw exceptions as well.
So to handle these we would need to do this:
```
FileOutputStream fos;
ObjectOutputStream oos;
try {
    fos = new FileOutputStream(file);
    oos = new ObjectOutputStream(fos);
    ...
    oos.writeObject(shapes);
    ...
} catch (FileNotFoundException ex) {
    // complain to user
} catch (IOException ex) {
    // notify user
} finally {
    if (oos != null){
      try{
        oos.close();
      }catch(Exception e){
        //do something
      }
    } 
    if (fos != null){
      try{
        fos.close();
      }catch(Exception e){
        //do something
      }
    } 
}
```
This is obviously very messy...
Ever since Java version 7, the `try-with-resources` is the cleaner and easier way of using and closing resources.

### What is try-with-resources?
`try-with-resources` is pretty similar to try-finally, except the fact that it auto closes all of the used resources without the user implicitly calling `resource.close()`.

||| topic
### Using try-with-resources
* `try-with-resources` closes only auto-closable resources which means classes that implement the `AutoCloseable` interface and implement the `close()` method.

|||

The above example should look like this:
```
 fos;
 oos;
try (FileOutputStream fos = new FileOutputStream(file);
    ObjectOutputStream oos = new ObjectOutputStream(fos)) {
        ...
        oos.writeObject(shapes);
        ...
} catch (FileNotFoundException ex) {
    // complain to user
} catch (IOException ex) {
    // notify user
}
```
Notice that both resources will be closed.
* It's important to understand that in this case, the `close()` method can still throw an exception.
You can handle this thrown exception <b>inside</b> the block.
This way we don't need to wrap what would have been written in the `finally` block with another `try-finally` block.