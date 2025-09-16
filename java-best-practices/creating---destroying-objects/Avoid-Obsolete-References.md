Garbage collection (GC) is the process of freeing up the memory used by objects after they are no longer needed.
In C or C++, when you want to free used memory and dispose of an object, you need to do it yourself.
Most of the time in Java, we do not need to think about garbage collection and disposal of objects because the language takes care of it automatically for us.
But sometimes, it is our job to take care of disposal and make sure we don't leave anything behind.

1. The first thing we should always do is to make sure we keep the scope of variables as small as possible so that the GC will take care of disposal as it should.

2. Beware of caching - whenever you use caching to improve performance you should be aware of the fact that you just created an object that is not going to be disposed when you are done with it.
You can schedule cached items for deletion after some time of being unused.
```
ScheduledExecutorService ses = Executors.newScheduledThreadPool(1);
ses.scheduleAtFixedRate(() -> checkCachedUse(), 5,10, TimeUnit.SECONDS);
```
This cleaner scheduler will run in a different thread, and clean the object according to the `checkCachedUse()` function.

3. Clean and deregister anything you are not using.
If you registered a callback for handling an event or you have an open connection that you don't need - close it!
A scheduler like the one in the example above will continue running until told otherwise so if you don't need it to run anymore - make sure you stop it!

4. Nulling out references
In some cases, we might have a reference to an object which is not used, but also not disposed of.
For example, let's say we want to implement a stack, like this:
```
public class MyStack {
    private Object[] objects;
    private final int DEFAULT_SIZE = 8;
    private int size = 0;
    public MyStack(){
        objects = new Object[DEFAULT_SIZE];
    }

    public void push(Object obj){
        if(size==objects.length){
            objects = Arrays.copyOf(objects,objects.length+DEFAULT_SIZE);
        }
        objects[size++] = obj;
    }
    
    public Object pop(){
        Object object = objects[--size];
        return object;
    }
    
    public Object peek(){
        Object object = objects[size];
        return object;
    }
}

```

The underlying array of this stack implementation (which is a very simplified, and flawed, version of the actual Java implementation) needs to grow whenever the data fills the array and we want to push another object.
But what happens when the array grows and we pop out objects?
In the underlying array, the object still exists.
This can cause memory leaks in larger scale. The solution to  manually null out the reference, like this:
```
    public Object pop(){
        Object object = objects[--size];
        objects[size] = null;
        return object;
    }
```

Manually nulling the object tells the GC to dispose it and will prevent this obsolete reference.
In the actual Java implementation of stack this is exactly what's being done:
```
    public synchronized void removeElementAt(int index) {
        if (index >= elementCount) {
            throw new ArrayIndexOutOfBoundsException(index + " >= " +
                                                     elementCount);
        }
        else if (index < 0) {
            throw new ArrayIndexOutOfBoundsException(index);
        }
        int j = elementCount - index - 1;
        if (j > 0) {
            System.arraycopy(elementData, index + 1, elementData, index, j);
        }
        modCount++;
        elementCount--;
        elementData[elementCount] = null; /* to let gc do its work */
    }
```

Notice that most of the time, GC happens without our involvement and we don't need to null out variables.