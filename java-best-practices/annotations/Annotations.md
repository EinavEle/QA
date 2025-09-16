Using annotations we can mark methods, fields, and classes so that other classes or tools can handle them in specific ways.

A very common example is the `@Override` annotation.
When we want a subclass method to be invoked instead of a superclass method, we annotate it with `@Override`.

```
class X{
  public void printMe(){
    System.out.print("X");
  }
}

class Y extends X{
  @Override
  public void printMe(){
    System.out.print("Y");
  }
}
```
We will look at an example of a mini testing framework from the book effective java.

```
/**
 * Indicates that the annotated method is a test method.
 * Use only on parameterless static methods.
 */
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Test {
}
```
This is a very basic empty annotation that is designed for methods `@Target(ElementType.METHOD)` meaning you can't annotate a class or field with this annotation and it is retained at run time `@Retention(RetentionPolicy.RUNTIME)`.
`@Target` and `@Retention` are meta annotations which are used to define the annotations themselves.

Since this annotation does nothing but mark a method as a 'test' it is called "marker annotation".

Let's say we want to create a program the receives a class name and runs all the "test" methods in that class.
We can achieve that by annotating the test methods in the class with a "test" marker annotations. Then our program will find and run only these methods.

We can use it to mark test methods:
```
@Test
public static void test1(){}
```

This code will run all static methods marked with our 'test' annotation:
```
public static void main(String[] args) throws Exception {
        int tests = 0;
        int passed = 0;
        Class<?> testClass = Class.forName(args[0]);
        for (Method m : testClass.getDeclaredMethods()) {
            if (m.isAnnotationPresent(Test.class)) {
                tests++;
                try {
                    m.invoke(null);
                    passed++;
                } catch (InvocationTargetException wrappedExc) {
                    Throwable exc = wrappedExc.getCause();
                    System.out.println(m + " failed: " + exc);
                } catch (Exception exc) {
                    System.out.println("Invalid @Test: " + m);
                }
            }
        }
        System.out.printf("Passed: %d, Failed: %d%n",
                passed, tests - passed);
    }
```
This code uses reflection which we will discuss in another class but it simply takes a class name from the arguments and looks for all methods marked with 'test' and runs them.
Then it catches the exceptions of the failed tests.
Notice that this code will only run static methods since we don't have an instance of this class, only the class itself.

If we wanted to add a parameter to our annotation, say to check if a test is throwing a specific exception, we can do that like this:
```
/**
 * Indicates that the annotated method is a test method that
 * must throw the designated exception to succeed.
 */
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface ExceptionTest {
    Class<? extends Throwable> value();
}
```
This `?` wildcard means that this value is a class of a type that extends `Throwable`.
Now we can add an exception type to our annotation and then check if this exception was thrown.

```
@ExceptionTest(IllegalArgumentException.class)
public static void test1(){};
```

This is the updated code for running methods with this annotation:
```
    public static void main(String[] args) throws Exception {
        int tests = 0;
        int passed = 0;
        Class<?> testClass = Class.forName(args[0]);
        for (Method m : testClass.getDeclaredMethods()) {
            if (m.isAnnotationPresent(Test.class)) {
                tests++;
                try {
                    m.invoke(null);
                    passed++;
                } catch (InvocationTargetException wrappedExc) {
                    Throwable exc = wrappedExc.getCause();
                    System.out.println(m + " failed: " + exc);
                } catch (Exception exc) {
                    System.out.println("Invalid @Test: " + m);
                }
            }

            if (m.isAnnotationPresent(ExceptionTest.class)) {
                tests++;
                try {
                    m.invoke(null);
                    System.out.printf("Test %s failed: no exception%n", m);
                } catch (InvocationTargetException wrappedEx) {
                    Throwable exc = wrappedEx.getCause();
                    Class<? extends Throwable> excType =
                            m.getAnnotation(ExceptionTest.class).value();
                    if (excType.isInstance(exc)) {
                        passed++;
                    } else {
                        System.out.printf(
                                "Test %s failed: expected %s, got %s%n",
                                m, excType.getName(), exc);
                    }
                } catch (Exception exc) {
                    System.out.println("Invalid @ExceptionTest: " + m);
                }
            }
        }

        System.out.printf("Passed: %d, Failed: %d%n",
                passed, tests - passed);
    }
```

As you can see the second annotation's behavior is very similar to the first one only this time we are using the `value()` provided in the annotation, to verify the type of exception thrown.

You can also pass array parameters to an annotation but since Java 8 it is easier to use `@Repeatable` which is a meta-annotation that allows an annotation to appear more than once per function.

Our `ExceptionTest` can be used twice on the same function but we need to use a wrapper annotation to contain it.

```
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface ExceptionTestContainer {
    ExceptionTest[] value();
}
```
```
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
@Repeatable(ExceptionTestContainer.class)
public @interface ExceptionTest {
    Class<? extends Throwable> value();
}
```

This is how these annotations are used:
```
    @ExceptionTest(IndexOutOfBoundsException.class)
    @ExceptionTest(NullPointerException.class)
    public static void doublyBad() {
        List<String> list = new ArrayList<>();

        // The spec permits this staticfactory to throw either
        // IndexOutOfBoundsException or NullPointerException
        list.addAll(5, null);
    }
```
And this is the code that executes them:
```
public static void main(String[] args) throws Exception {
        int tests = 0;
        int passed = 0;
        Class testClass = Class.forName(args[0]);
        for (Method m : testClass.getDeclaredMethods()) {
            if (m.isAnnotationPresent(Test.class)) {
                tests++;
                try {
                    m.invoke(null);
                    passed++;
                } catch (InvocationTargetException wrappedExc) {
                    Throwable exc = wrappedExc.getCause();
                    System.out.println(m + " failed: " + exc);
                } catch (Exception exc) {
                    System.out.println("INVALID @Test: " + m);
                }
            }

            // Processing repeatable annotations (Page 187)
            if (m.isAnnotationPresent(ExceptionTest.class)
                    || m.isAnnotationPresent(ExceptionTestContainer.class)) {
                tests++;
                try {
                    m.invoke(null);
                    System.out.printf("Test %s failed: no exception%n", m);
                } catch (Throwable wrappedExc) {
                    Throwable exc = wrappedExc.getCause();
                    int oldPassed = passed;
                    ExceptionTest[] excTests =
                            m.getAnnotationsByType(ExceptionTest.class);
                    for (ExceptionTest excTest : excTests) {
                        if (excTest.value().isInstance(exc)) {
                            passed++;
                            break;
                        }
                    }
                    if (passed == oldPassed)
                        System.out.printf("Test %s failed: %s %n", m, exc);
                }
            }
        }
  ```
  In this code we see that the exceptions thrown are checked one by one to see whether one of them fits our test criteria, if so, the test passes, otherwise it fails.

Annotations have very specific usages but it is important to understand how they work in order to use them correctly.
