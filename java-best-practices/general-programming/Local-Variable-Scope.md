The scope of a variable is the space where a variable is living and is available before being disposed and garbage collected.
The simplest and easiest way to visually see the scope is to look at the next `}` after the variable's declaration.

In this example the `text` string is available in the `main` function and is disposed afterwards:
```
private void main(){
  String text = "Hello";
  System.out.println(text);
}
```

Generally, we want to minimize the scope of a variable and dispose of it as soon as it's no longer used.
This helps the reader understand our code and makes it more maintainable.

One of the ways to help this scope reduction is to only declare a variable when we first need it.

### Wrong way:
```
    private void varScope(){
        int sum;
        int x = doStuff();
        int y = doOtherStuff();
        sum = x+y;
    }
``` 

### Right way:
```
    private void varScope(){
        int x = doStuff();
        int y = doOtherStuff();
        int sum = x+y;
    }
```
* Notice that we also initialize the variable on decleration and not later in the code.
This also helps making the code more understandable and clean.

There are some use cases where we must declare the variable and assign it separately:
```
    private int varScope(){
        int x;
        try{
            x = doStuff();
        }catch(Exception e){
            // handle exception
            x = doOtherStuff();
        }
        return x;
    }
```
In this case we have no choice and must separate variable declaration from assignment.

# For loop scopes
When declaring a variable in a loop scope, this variable is available only inside the loop function.

```
    for(int i=0; i<10; i++){
      System.out.println("This is the value of i " + i);
    }
```
This is an example of the same thing done with a while loop:
```
  private void loop(){
    int i=0;
    while(i<10){
        System.out.println("This is the value of i " + i);
        i++;
    }
    //i is still available here
  }
```

In this case the scope of int `i` is bigger and it will be disposed only when the outer function will end.
This can cause human errors and bugs but more importantly, it's just keeping an unneeded variable 'alive' for no reason.

For this reason we will prefer using for loops instead of while loops when possible.

Another important thing about for loops is the fact that we can use more than one variable in it:
```
    private static void loop() {
        for (int x = 0, y = 0; x < 10; x++, y++) {
            System.out.println(x * y);
        }
    }
```