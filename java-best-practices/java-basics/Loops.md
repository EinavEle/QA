In Java, when we need to perform iterative actions, we have a few loops to choose from:
- For
- For-each
- While
- Do-while

Let's briefly go over them.

### For
A simple and classic for loop might look like this:
```
        for (int i = 0; i < 10; i++) {
            System.out.println(i);
        }
```
We have our index `i`, we have our limit `10`, and we have the operation `i++` which increments `i` by 1 every iteration of the loop.
We could do the same thing backwards:
```
        for (int i = 9; i >= 0; i--) {
            System.out.println(i);
        }
```

### For-each
The foreach statement is more suitable for iteration over a collection.
While you can use for and provide the index it is less suitable and will force you to use an extra variable.
A simple for each loop might look like this:
```
        for (Student student : students) {
            System.out.println(student.getName());
        }
```
Using the `for-each` loop, we get direct access to every item in the collection.
We could have done the same with a for loop:
```
        for (int i = 0; i < students.size(); i++) {
            Student student = students.get(i);
            System.out.println(student.getName());
        }
```
As you can see, this is less efficient and less clear.

### While
The while loop will go on as long as its stop condition is not met.
```
        Student yossi = null;
        Iterator<Student> it = students.iterator();
        while (yossi == null) {
            Student next = it.next();
            if (next.getName().equals("Yossi")) {
                yossi = next;
            }
        }
```
The while loop can be a bit dangerous!
Pay close attention to your stop condition.
In this case, for example, if there is no "Yossi" in the student list.
We will get an exception because `it.next()` will fail at the last item of the list.
This kind of logic is better done with other loops.
This is a more common use of while:
```
        boolean done = false;
        while(!done){
            //do something
        }
```
This example is also problematic because there is no guarantee that `done` will ever be `true`, meaning this `while` loop could go on forever.
In such cases, we should provide another stop condition to act as a safety net.
```
        boolean done = false;
        int retries = 0;
        while (!done && retries < 20) {
            //do something
            retries++;
        }
```
Now we have provided a safe stop condition that will definitely make our while loop exit, eventually.

### Do-while
The `do-while` loop is very similar to the while loop.
The only difference is in where the condition is tested.
```
        boolean done = false;
        int retries = 0;
        do {
            //do something
            retries++;
        } while (!done && retries < 20);
```
In the example above, we are telling the code:
1. Do one iteration of the loop,
2. Test the condition to see whether another iteration should be executed.
This can be very useful at times, like when we know that one iteration must run in any case, allowing us to skip the first condition test.
It may seem meaningless in such simple examples but conditions can sometimes be costly actions that will waste compute-time unnecessarily.