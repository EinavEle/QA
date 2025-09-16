If you look closely at the `Object` class, you will find the `clone()` method. Since every class extends `Object`, every class has its own `clone()` method.
Yet, if you don't override it, you can't use it! it's a `protected` method of `Object`.

### Using `clone()`
In order to use clone, we first need to make our class implement `Cloneable`- a very non-traditional way of using interfaces.
The `Cloneable` interface does not include any methods or behaviors but it does this (copied from Java `Cloneable` interface):

> A class implements the Cloneable interface to indicate to the Object.clone() method that it is legal for that method to make a field-for-field copy of instances of that class.

This means, when you "implement" `Cloneable` you allow the `Object.clone()` method to be called and make a copy of your object.
But this copy is a very non-intelligent one...
Take a `Song` class for example:
```
public class Song implements Cloneable {
    private List<String> notes;
    private String lyrics;

    public Song(List<String> notes, String lyrics) {
        this.notes = new ArrayList<>(notes);
        this.lyrics = lyrics;
    }
    public void addNotes(String... notes){
        this.notes.addAll(Arrays.asList(notes));
    }

    @Override
    protected Song clone() {
        try {
            return (Song) super.clone();
        } catch (CloneNotSupportedException e) {
            throw new RuntimeException(e);
        }
    }

    @Override
    public String toString() {
        return "Song{" +
                "notes=" + notes +
                ", lyrics='" + lyrics + '\'' +
                '}';
    }
}
```
What would happen when we run this?
```
    public static void main(String... args){
        Song song = new Song(Arrays.asList("sol", "mi", "mi", "fa", "re", "re"), "Jonathan the little one");
        Song song2 = song.clone();
        song2.addNotes("do","re","mi","fa","sol","sol","sol");
        System.out.println(song);
        System.out.println(song2);
    }
```
The result is that both songs now contain the same notes:
```
Song{notes=[sol, mi, mi, fa, re, re, do, re, mi, fa, sol, sol, sol], lyrics='Jonathan the little one'}
Song{notes=[sol, mi, mi, fa, re, re, do, re, mi, fa, sol, sol, sol], lyrics='Jonathan the little one'}
```
The simple `Object.clone()` when copying field-for-field does not take care of cloning lists, or any other inner object for that matter.
It means that even though we cloned `Song` and expected to get a <b>separate and independent</b> copy of it, we got two instances pointing at the same list of notes.
To fix this, we need to alter the `clone()` method to take care of any inner objects.
The new implementation looks like this:
```
    @Override
    protected Song clone() {
        try {
            Song clone = (Song) super.clone();
            clone.notes = new ArrayList<>(notes);
            return clone;
        } catch (CloneNotSupportedException e) {
            throw new RuntimeException(e);
        }
    }
```
In this specific case the solution was not too difficult, but imagine how complex it can get in larger classes...

### Copy constructors
A copy `constructor` or copy `factory` can give us the same results as `clone()` with less complexity and more flexibility.
```
    public Song(Song song){
        notes = new ArrayList<>(song.notes);
        lyrics = song.lyrics;
    }
```
Using this constructor instead of `clone()` will yield the same result and does not require try-catch or implementing an interface.
This is our updated code:
```
    public static void main(String... args){
        Song song = new Song(Arrays.asList("sol", "mi", "mi", "fa", "re", "re"), "Jonathan the little one");
        Song song2 = new Song(song);
        song2.addNotes("do","re","mi","fa","sol","sol","sol");
        System.out.println(song);
        System.out.println(song2);
    }
```
And we can do the same with a static factory:
```
    public static Song copyOf(Song song){
        return new Song(song.notes, song.lyrics);
    }
```
Which will be used like so:
```
        Song song2 = Song.copyOf(song);
```