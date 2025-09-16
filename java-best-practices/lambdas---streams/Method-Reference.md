Let's take another look at the previous example.
```
List<Student> students = new ArrayList<>();
students.sort((stu1,stu2)->Double.compare(stu1.getHeight(),stu2.getHeight()));
```
The `sort()` method gets a `Comperator<T>`, which is a functional interface, as a parameter.
We supply a lambda that accepts two `Student` objects and compares their height.
We could do the same thing by doing this:
```
students.sort(Comparator.comparingDouble(Student::getHeight));
```
This is called "method reference".
Method references can sometimes replace lambdas and more often than not, they make our code clearer and shorter (like in the example above).
This is the signature of `comparingDouble()`:
```
public static<T> Comparator<T> comparingDouble(ToDoubleFunction<? super T> keyExtractor) {
```
This method gets a `ToDoubleFunction` (also a functional interface) as a parameter.
We can provide it with an anonymous class:
```
        ToDoubleFunction<Student> heightOfStudent = new ToDoubleFunction<>() {
            @Override
            public double applyAsDouble(Student value) {
                return value.getHeight();
            }
        };
        students.sort(Comparator.comparingDouble(heightOfStudent));
```
Which, as we discussed earlier, is long, messy, and unnecessary.
We could provide a lambda:
```
students.sort(Comparator.comparingDouble(student -> student.getHeight()));
```
A lot clearer no?

But, here we also have this `student -> student` statement which we don't actually need.
The best option is this:
```
students.sort(Comparator.comparingDouble(Student::getHeight));
```
The rule of thumb is: use method references when they make your code more readable.
This is not always the case.
For example, When you have long class names or methods that have unclear names, using method reference can make your code less readable which defeats the whole purpose.



|||important
### Readability
Do not forget!
Our main goal is to make our code more readable and understandable.
We don't want to use fancy Java tricks to make ourselves feel better.
We use them when they serve our purpose.
|||
