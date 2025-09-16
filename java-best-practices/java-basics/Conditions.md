For our program to be able to make decisions, we need to provide it with code that chooses the right action for every situation.
For this task, we have our conditions, let's take a look.

### If-else
The `if-else` statement is one of the most common of feature any programming language.
Without it, there will be no algorithms...
In Java, an `if-else` statement looks like this:
```
        if(a<b){
            System.out.println(a);
        }else{
            System.out.println(b);
        }
```
We can also add another branch to the "decision tree" by adding an `else-if` block.
```
        if(a<b){
            System.out.println(a);
        }else if(b<c){
            System.out.println(b);
        }else{
            System.out.println(c);
        }
```

If we have simple conditions and we want to write them in-line, we can use this syntax, known as ternary syntax:
```
a < b ? System.out.println(a) : System.out.println(b);
```
This works with any condition set, but more complex conditions can easily become hard to understand using this type of syntax.

### Switch case
When we have to make a decision between different cases, we can use the `switch` statement.
```
private String getCapital(String country) {
        switch(country){
            case "Israel":
                return "Jerusalem";
            case "England":
                return "London";
            case "Italy":
                return "Rome";
            default:
                throw new IllegalArgumentException("Country not supported");
        }
```
This code would have looked a lot messier if we used `if-else` statements, and even worst if we had many more cases.
Later on, we will see why this code is all wrong from a different angle :)