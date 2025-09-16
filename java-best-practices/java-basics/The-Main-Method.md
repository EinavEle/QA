In order to run a Java program, we have to implement at least one `main()` method.
The `main()` method is our starting point.
The signature of the `main()` method looks like this:
```
public static void main(String[] args) { }
```
Java will accept other variants of this signature, like:
```
public static void main(String... args) { }
public static void main(String args[]) { }
```
And a few more, but the first example above is the most commonly used.


|||info
The method signature is the combination of the method name and the parameter list.
|||

You can implement more than one `main()` method in your program.
For example, you could run a class or a module separately from the rest of the code  while developing, so you can debug or test it.
Eventually, an executable jar or any other configuration that will run your program will have a single entry point with a single `main()` method.