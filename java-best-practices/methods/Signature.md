The signature of a method includes the name and parameters of a method.
It is very important to make the signature clear so that the method's users will know how to properly use it.

### Name
We should always provide clear and understandable names for our functions.
We should follow both Java naming conventions and your team's naming conventions.
Names should help the reader easily understand what the method does.

### Parameter count
As a general rule, we do not want too many parameters in the signature. It is not likely that a developer will remember the order and meaning of 10 or more parameters of a method.
Keep the parameter count to no more than 4 parameters and use inner classes/builders if more parameters are really necessary.
For example:
```
    public void publishPost(int id, String description, Date date, 
    String title, boolean visible, double grade){
        //publish a blog post
    }
```
Could simply be:
```
    public void publishPost(BlogPost post, boolean visible, double grade){
        //publish a blog post
    }
```
The purpose is to make everything clearer and easier to use.
The constructor of `BlogPost` will take the relevant parameters and be easy to understand. Now, our method will take only 3 parameters.

### Enums and booleans
You should only use booleans if the parameters are clearly a true/false value.
```
public void shouldLockDoor(boolean lock)
```
But not for substituting an option selection like:
```
public void dance(boolean isBoogie){
  if(isBoogie){
    //Dance the boogie
  }else{
    //Dance the tango
  }
}
```
In this case, we can and should use an enum.
```
public void dance(Dance dance){
  switch(dance){
    case BOOGIE:
      //dance the boogie
      break;
    case TANGO:
      //dance the tango
      break;
    default:
      throw new IllegalArgumentException("Dance not supported: " + dance)
  }
}
```
Enums not only make our code clearer to the user, it also allows for additional options to be easily added in the future.

### Favor interfaces over classes
If your method can accept `Map` and does not depend on the specific implementation `HashMap` it should have a `Map` parameter.
This way, your code is more usable and won't require casting or other manipulations, and will also allow users to use different map implementations.
