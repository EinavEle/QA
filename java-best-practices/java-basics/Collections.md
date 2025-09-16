Collections provide a way to store and manipulate groups of objects.
There are many types of collections in Java.
Some are very straightforward and some fit very specific use cases.
We will go over the commonly used collections of the language.

### Array
The array is the most basic of collections.
It is also the basis for many other collections, like `ArrayList`, `Stack`, and others.

|||important
In Java, An array is an object containing a fixed number of values of the same type.
|||
The array is indexed which means we can access elements by their index.
Initializing an array looks like this:
```
int[] numbers = new int[20];
```
Since the array has a fixed size we must declare its size on initialization.
We can assign items to the array like this:
```
numbers[4] = 8;
```
We can get items from the array in the same way:
```
int firstNumber = numbers[0];
```

### List (ArrayList)
A `list` is a very common and useful collection.
List is an interface and it has different implementations.
The most used implementation of `List` is `ArrayList`.
Creating an array list:
```
List<String> strings = new ArrayList<>();
```
We can add to the list by:
```
strings.add("Shalom");
```
We can get items by their index (like an array):
```
strings.get(13);
```
We can remove items by index or by providing the item:
```
strings.remove(0);
strings.remove("shalom");
```
Iteration over lists can be done with `for-each`, loops or using an iterator:
```
Iterator<String> it = strings.iterator();
while(it.hasNext()){
  it.next();
}
```

### List (LinkedList)
A `LinkedList` is used just like an ArrayList, since they both implement the `List` interface.
It is important to know the difference between the two, because they behave very differently.
A `LinkedList`` is a list of nodes that have references to the next and previous items, thus creating the list structure.
It is not based on arrays which means every time you access an item you go through all the nodes leading to this index.
Since `LinkedList` also implements `Deque` (a sub interface of `Queue`) you can use it as a queue as well.
We will see more about it below.

### Queue (LinkedList)
A queue is another type of collection, which is also an interface.
The most common implementation used for it is `LinkedList`.
A queue, as you might have guessed, is used when we want to use objects in a certain order, specifically, FIFO - first in, first out.
With a `Queue` we can add/offer items into the queue:
```
Queue<String> queue = new LinkedList<>();
queue.add("first");
queue.offer("second");
```
The difference between `add()` and `offer()` is that with `add()` you might get an exception if the queue is size-limited. 
`offer()`, on the other hand, will not throw an exception, but the operation will fail and return false.
We can `peek()` at the queue to get the next item:
```
String str = queue.peek();
```
The `peek()` method does not change the queue, it only returns the item and leaves it in its original position.
The `poll()` method is a different story:
```
String str = queue.poll();
```
`poll()` will return the next item in the queue and it will also remove it from the queue.
Here is a more complete example:
```
        Queue<String> queue = new LinkedList<>();
        queue.add("first");
        queue.offer("second");
        queue.addAll(Arrays.asList("third","forth"));
        System.out.println(queue.poll());
        System.out.println(queue.peek());
        System.out.println(queue.peek());
        System.out.println(queue.poll());
```
What will this code print?
```
first
second
second
second
```
The `poll()` invocation prints the "first" and removes it.
The two `peek()` invocations print the "second" and leave it in the queue.
The last `poll()` still prints "second" because it never left the queue.

### Stack
Stack is very similar to queue only in reverse.
Stack is FILO - first in, last out.
The syntax of `Stack` is also a bit different than `Queue`.
We can add by using:
```
Stack<String> stack = new Stack<>();
        stack.push("first");
        stack.add("second");
```
Both will add elements the same way (`add()` belongs to the `List` implementation).
`add()` will return boolean and `push()` will return the element itself.
We can `Peek()` the same way as we can with `Queue` (without removing from the stack):
```
String str = stack.peek();
```
Taking an item from the stack (and removing it) is done with `pop()`:
```
String str = stack.pop();
```
### Queue/Stack summary
Here is a summarizing example that does the same thing twice ,first using queue and then using stack.
```
public static void queueEx() {
        Queue<User> users = new LinkedList<>();
        System.out.println("Inserting");
        for (int i = 0; i < 5; i++) {
            User newUser = User.newRandomUser();
            System.out.println(newUser);
            users.offer(newUser);
        }
        System.out.println("Polling");
        for (int i = 0; i < 5; i++) {
            System.out.println(users.poll());
        }
    }

    public static void stackEx() {
        Stack<User> users = new Stack<>();
        System.out.println("Inserting");
        for (int i = 0; i < 5; i++) {
            User newUser = User.newRandomUser();
            System.out.println(newUser);
            users.push(newUser);
        }
        System.out.println("Polling");
        for (int i = 0; i < 5; i++) {
            System.out.println(users.pop());

        }
    }
```
You can see that the implementation is almost the same.
And here is the output:
```
Inserting
User{name='Annabella', email='Annabella@Annabella.com', country=Dominican Republic}
User{name='Kaitlyn', email='Kaitlyn@Kaitlyn.com', country=Haiti}
User{name='Audrie', email='Audrie@Audrie.com', country=Marshall Islands}
User{name='Modestia', email='Modestia@Modestia.com', country=Kyrgyzstan}
User{name='Siobhan', email='Siobhan@Siobhan.com', country=Democratic Republic of the Congo}
Polling
User{name='Annabella', email='Annabella@Annabella.com', country=Dominican Republic}
User{name='Kaitlyn', email='Kaitlyn@Kaitlyn.com', country=Haiti}
User{name='Audrie', email='Audrie@Audrie.com', country=Marshall Islands}
User{name='Modestia', email='Modestia@Modestia.com', country=Kyrgyzstan}
User{name='Siobhan', email='Siobhan@Siobhan.com', country=Democratic Republic of the Congo}
Inserting
User{name='Ethelda', email='Ethelda@Ethelda.com', country=Tonga}
User{name='Gerladina', email='Gerladina@Gerladina.com', country=Libya}
User{name='Georgetta', email='Georgetta@Georgetta.com', country=Tanzania}
User{name='Moria', email='Moria@Moria.com', country=Marshall Islands}
User{name='Lea', email='Lea@Lea.com', country=Uzbekistan}
Polling
User{name='Lea', email='Lea@Lea.com', country=Uzbekistan}
User{name='Moria', email='Moria@Moria.com', country=Marshall Islands}
User{name='Georgetta', email='Georgetta@Georgetta.com', country=Tanzania}
User{name='Gerladina', email='Gerladina@Gerladina.com', country=Libya}
User{name='Ethelda', email='Ethelda@Ethelda.com', country=Tonga}
```

### Map (HashMap)
The `Map` is a very useful collection that stores elements by keys.
Its most common implementation is the `HashMap`.
A simple example would be using a map as a dictionary of students, organized by their "id".
So the key is `Integer` and the value is `Student`.
```
Map<Integer, Student> studentsById = new HashMap<>();
```
To insert a student to the map, we use the `put()` method.
```
studentsById.put(student.getId(),student);
```

|||important
The `put()` method will override an existing value if the key is already present in the map.
|||
You can use `putIfAbsent()` if you want to avoid overriding existing values.

To get a value from the map using its key, do this:
```
Student student = studentsById.get(12345);
```
`get()` will return `null` if the key is not present in the map.

We can also check whether a key is present or not:
```
boolean present = studentsById.containsKey(12345);
```
To iterate over a map, you can either:
- Create a collection out of its values by calling `map.values()` and iterating over it.- Or, you can iterate over the keys using `map.keySet()`.