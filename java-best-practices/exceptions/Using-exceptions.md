Exceptions, as their name suggests, are designed for exceptional cases.
They should not be used as part of the "happy path" of your code.
You should never consider throwing an exception when things go according to plan.
Exceptions are thrown when something went wrong and should provide us with the information regarding what went wrong and where.

### Never ignore exceptions!
When exceptions are caught, they need to be handled!
having code like this:
```
try{
  doSomething();
}catch(Exception e){

}
```
Means you have an error somewhere, you created a piece of code that can handle it or at least log it somewhere, and you are completely ignoring it.
Debugging such code could take a very very long time and leave you and your team highly frustrated.
The minimal thing that must be done in a catch block is to log the exception somewhere so it can be investigated if necessary.
Whenever possible, react to the exception and try to recover from the error, or at least notify the client in a constructive way.