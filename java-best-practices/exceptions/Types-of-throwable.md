`Throwable` is the base class of all types of thrown errors in Java.
The throwables are generally divided into 3 groups:
- **Checked exceptions**
Checked exceptions are errors that get thrown when the state can possibly still be fixed.
Meaning, you throw this exception so the user can handle it and react accordingly.
For example `FileNotFoundException` is a checked exception indicating we are trying to read/write a file that doesn't exist.
If we reached this exception it doesn't necessarily mean that we have to shut everything down, maybe we have a default behavior or a fallback to provide when this happens.
We can ask the user to provide another file name or we can ask the user if he wants to create a new file.
- **Runtime Exceptions**
Runtime (or unchecked) exceptions are generally non recoverable.
For example `NullPointerException` means some object we are trying to operate on was null and the code just cannot continue running.
Runtime exceptions will cause your program to exit immediately.
- **Errors**
Errors are reserved for internal JVM errors and we should not use them in our code.
One common error you may be familiar with is `StackOverflowError` which is thrown when we have exhausted the memory stack.
Excluding `AssertionError` which we have discussed in an earlier class.