|||important
Inheritance is a very useful tool to extend existing classes and reuse their code and functionality.
|||
Even though it may sometimes be tempting to extend core classes like `java.util.ArrayList` or others, **we should use inheritance only for classes we control directly and are written by us.**
Since the implementation of `java.util.ArrayList` is outside our control and can be changed with different versions of Java, extending it will be unsafe.

Let's take an example from Effective Java:
```
// Broken - Inappropriate use of inheritance! (Page 87)
public class InstrumentedHashSet<E> extends HashSet<E> {
    // The number of attempted element insertions
    private int addCount = 0;

    public InstrumentedHashSet() {
    }

    public InstrumentedHashSet(int initCap, float loadFactor) {
        super(initCap, loadFactor);
    }

    @Override public boolean add(E e) {
        addCount++;
        return super.add(e);
    }

    @Override public boolean addAll(Collection<? extends E> c) {
        addCount += c.size();
        return super.addAll(c);
    }

    public int getAddCount() {
        return addCount;
    }

    public static void main(String[] args) {
        InstrumentedHashSet<String> s = new InstrumentedHashSet<>();
        s.addAll(List.of("Snap", "Crackle", "Pop"));
        System.out.println(s.getAddCount());
    }
}
```

This is a class extending `HashSet`, its main purpose is to count every added item.
It does not work properly because of the underlying implementation of `HashSet` which actually calls `add()` when we call `addAll()`.
That shows us why this kind of extension is less predictable and unsafe.

It's important to understand that inheritance breaks encapsulation and when extending a class we become affected by its inner implementation.
To mitigate this risk we can use composition instead of inheritance.

### Composition
The preferred solution to this situation is to use composition and have a class that has `HashSet` as a private field.

|||important
Composition means we can use the functionality of `HashSet` without being involved in its implementation and still add our functionality on top of it.
|||

First, we create a forwarding class:
```
// Reusable forwarding class (Page 90)
public class ForwardingSet<E> implements Set<E> {
    private final Set<E> s;
    public ForwardingSet(Set<E> s) { this.s = s; }

    public void clear()               { s.clear();            }
    public boolean contains(Object o) { return s.contains(o); }
    public boolean isEmpty()          { return s.isEmpty();   }
    public int size()                 { return s.size();      }
    public Iterator<E> iterator()     { return s.iterator();  }
    public boolean add(E e)           { return s.add(e);      }
    public boolean remove(Object o)   { return s.remove(o);   }
    public boolean containsAll(Collection<?> c)
                                   { return s.containsAll(c); }
    public boolean addAll(Collection<? extends E> c)
                                   { return s.addAll(c);      }
    public boolean removeAll(Collection<?> c)
                                   { return s.removeAll(c);   }
    public boolean retainAll(Collection<?> c)
                                   { return s.retainAll(c);   }
    public Object[] toArray()          { return s.toArray();  }
    public <T> T[] toArray(T[] a)      { return s.toArray(a); }
    @Override public boolean equals(Object o)
                                       { return s.equals(o);  }
    @Override public int hashCode()    { return s.hashCode(); }
    @Override public String toString() { return s.toString(); }
}
```
This class implements `Set` and actually uses its inner `Set`.
Now we can create our wrapper class:
```
// Wrapper class - uses composition in place of inheritance  (Page 90)
public class InstrumentedSet<E> extends ForwardingSet<E> {
    private int addCount = 0;

    public InstrumentedSet(Set<E> s) {
        super(s);
    }

    @Override public boolean add(E e) {
        addCount++;
        return super.add(e);
    }
    @Override public boolean addAll(Collection<? extends E> c) {
        addCount += c.size();
        return super.addAll(c);
    }
    public int getAddCount() {
        return addCount;
    }

    public static void main(String[] args) {
        InstrumentedSet<String> s = new InstrumentedSet<>(new HashSet<>());
        s.addAll(List.of("Snap", "Crackle", "Pop"));
        System.out.println(s.getAddCount());
    }
}
```
The main difference is that when the inner `addAll()` in the private `Set` is called, it is calling it own `add()` since our wrapper class is not overriding it but it overrides the forwarding class.

Let's take a simpler example.
This is a `Dog` class:
```
public class Dog {
    public void bark(){
        System.out.println("Wuff wuff!!!");
    }
    
    public void run(){
        System.out.println("Running!!!");
    }
    public void issueWarning(){
        run();
        bark();
    }
}
```
It can run and bark, and when it wants to warn us that something bad is happening he is does both.

Now, if I were to extend this dog to an attack dog (add a "rrr" to the bark and make this bite) it would look something like this:
```
public class AttackDog extends Dog {
    @Override
    public void bark(){
        super.bark();
        System.out.println("rrrrrrrrrrrrr");
    }

    public void bite(){
        System.out.println("Biting!");
    }
    public void attack(){
        super.issueWarning();
        bite();
    }
}
```
But when we run this `AttackDog` `attack()` function, this is what happens:
```
Running!!!
Wuff wuff!!!
rrrrrrrrrrrrr
Biting!
```
The superclass `Dog` called the `AttackDog` `bark()` and not its own `bark()` since we overridden it.
When both these classes are written by us this can be fixed easily, but when it's not the case things can get unpredictable and unstable.


