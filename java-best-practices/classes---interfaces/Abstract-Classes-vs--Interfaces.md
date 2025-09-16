|||important
### Interface
An Interface in Java programming language is defined as an abstract type used to specify the behavior of a class. An interface in Java is a blueprint of a class. A Java interface contains static constants and abstract methods.
|||
|||important
### Abstract Classe
An abstract class, in the context of Java, is a superclass that cannot be instantiated and is used to state or define general characteristics. An object cannot be formed from a Java abstract class
|||

In many cases in Java, we seem to have a the dilemma whether to use interfaces or abstract classes.
In most cases, interfaces are more flexible and provide more options while abstract classes are more rigid and demand specific type hierarchy.
### Advantages of interfaces:
- Retrofitting
You can easily retrofit a class to implement an interface after its written, it's not that easy with an abstract class.
- Mixins
You can implement interfaces that do not interfere with the main function of the class like: Comparable, Serializable, etc..
- Multiple Interfaces
You can make a class implement more than one interface and you can also make a third interface that extends two other interfaces.

### Skeletal implementation
A skeletal implementation is a way to give the user of an interface an easy start by providing an abstract class that implements the "primitive" part of an interface.
Instead of leaving it all to the implementing class, the skeletal abstract class can provide a shortcut.

This class implements `equals()`, `hashCode()`, and `toString()` and also throws an exception when calling `setValue()` since the implementation isn't necessarily of a modifiable map.
Using this skeletal implementation, we can easily implement this interface.

Here is an example from Effective Java:
```
public abstract class AbstractMapEntry<K,V>
        implements Map.Entry<K,V> {
    // Entries in a modifiable map must override this method
    @Override public V setValue(V value) {
        throw new UnsupportedOperationException();
    }

    // Implements the general contract of Map.Entry.equals
    @Override public boolean equals(Object o) {
        if (o == this)
            return true;
        if (!(o instanceof Map.Entry))
            return false;
        Map.Entry<?,?> e = (Map.Entry) o;
        return Objects.equals(e.getKey(),   getKey())
                && Objects.equals(e.getValue(), getValue());
    }

    // Implements the general contract of Map.Entry.hashCode
    @Override public int hashCode() {
        return Objects.hashCode(getKey())
                ^ Objects.hashCode(getValue());
    }

    @Override public String toString() {
        return getKey() + "=" + getValue();
    }
}
```

