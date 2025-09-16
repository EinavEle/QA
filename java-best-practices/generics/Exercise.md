Write a generic method that gets a `Callable<T>` and runs it until an expected result is returned or a given retry count is reached.
The method should return the final result it got even if it is not the expected one.
The method should be provided with number of retries and sleep between retries.
The method should have overloads that have default sleeps and retry limits.