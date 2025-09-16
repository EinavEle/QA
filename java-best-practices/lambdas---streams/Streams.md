Streams are another great addition to Java 8. They go hand in hand with lambdas.
A stream is an interface used to process data in a pipeline.
The introduction of streams into the language is a big step towards a more functional programming style that was non-existent in Java before.

### Creating a stream
Creating a stream is very simple.
We just need to call `stream()` on a collection.
```
List<Student> students = new ArrayList<>();
Stream<Student> stream = students.stream();
```

### Types of operations
#### Intermediate operations
Intermediate operations are processes on the stream that return another stream.
Actions like filter, map, etc.. are intermediate.
`filter()` for example, takes a `Predicate` that will determine whether an element passes the filter or not.
This code will return a stream of students higher than 1.60:
```
Stream<Student> stream = students.stream().filter(student -> student.getHeight()>1.60);
```
As you can see, this returns a stream of `Student` but this stream will only include students that pass the filtration.
Another important example is `map()`.
Say we want to get a stream of only the dates of birth of our students:
```
stream.map(Student::getBirthDate);
```
The `map()` method accepts a `Function` and returns the result of this function for every element in the stream.
In this case, we used a method reference but we could have reached the same result with this code:
```
stream.map(student -> student.getBirthDate());
```

#### Terminal operations
Terminal operations are actions that return a result (not a stream).
`count()`, `collect()`, `anyMatch()` and many others are terminal operations.
If we wanted to count the items in our stream after we filtered them, we would do this:
```
long count = students.stream().filter(student -> student.getHeight() > 1.60).count();
```
The result of this code is not a stream but a number representing the count of our filtered students.
If we would like to know if any of our students has a birthday today, we would do this:
```
boolean isBirthday = students.stream().anyMatch(student -> student.getBirthDate().getMonth().equals(LocalDateTime.now().getMonth()) && student.getBirthDate().getDayOfMonth() == LocalDateTime.now().getDayOfMonth());
```
This will not return the student, Rather, it will only return `true` if there is at least one student who has a birthday.

Learning the different operations of streams can be very helpful since there are many ways to achieve the same result, but some are a lot more efficient than others.
Our birthday example could have been done this way:
* I added the isBirthday method to make the code more readable.
```
boolean isBirthday = students.stream().anyMatch(Student::isBirthday);
```
Or like this:
```
boolean isBirthday = students.stream().filter(Student::isBirthday).count()>0;
```
Or like this:
```
boolean isBirthday = students.stream().filter(Student::isBirthday).findFirst().isPresent();
```
All will produce the same result but the first one will run the fastest (if the result is `true`).
`anyMatch()` will return true when it will find the first item that returns true. meaning if this item is number 7 on a list of 200, the program will only iterate over 7 items.
Both other options will iterate over the entire collection to get the same result.
This is a simple example of how knowing the specifics of how things work can significantly improve the quality of our code.

#### Collecting
Collecting is a terminal operation, but it deserves its own section.
Collecting is the action of returning a collection out of a stream.
For example if we wanted to get a list of filtered students it would look like this:
```
List<Student> studentsWithA = students.stream().filter(student -> student.getName().contains("a")).collect(Collectors.toList());
```
We can also collect the streams into `Set` or `Map`.
This is an example of turning our list of students into a map of students, where the `Student` object is the value and the students `id` is the key:
```
Map<Integer, Student> studentMap = students.stream().collect(Collectors.toMap(Student::getId, student -> student));
```
The `toMap()` collector gets two `Function` arguments. In our case, one is a method reference and one is a lambda. The first is the function to provide the key, and the second for providing the value.

### Lazy evaluation
Another very important fact about streams is the fact that streams are lazily evaluated.
This means that until the invocation of a terminal operation, no computation is performed.
This differs greatly from the old "for each" iteration that most of us are used to.
```
Stream<Student> birthdayStudents = students.stream().filter(Student::isBirthday);
```
This code returns a stream of students that have a birthday today.
But, unless we perform a terminal operation on this stream, this code actually does nothing.
It only filters the list once we do something like this:
```
List<Student> birthdayList = birthdayStudents.collect(Collectors.toList());
```
This has big implications on how we design our code, since it can affect performance.


### Overusing streams
Streams are a fun way of programming, and they are very effective.
Still, we need to make sure we do not overuse them.
Most of the time, stream pipelines that take more the 2-3 lines become unreadable. As with lambdas, our goal is to make our code readable and usable.
So, if you find yourself forcing a stream where it doesn't belong, don't be ashamed to use the good old "for each" to do your iterating with.