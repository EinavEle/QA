Using dependency injection (DI) helps us decouple services from their resources.

This is an example of a utility class with a hard-wired resource:
```
public class WordUtility {
    private final Set<String> wordList = ...
    public WordUtility(){};
}
```

The `wordList` set is hard-wired, which means this class will always instantiate with the same set of words.
The correct implementation should be:
```
public class WordUtility {
    private final Set<String> wordList;
    public WordUtility(Set<String> wordList){
        this.wordList=wordList;
    };
}
```
This way we can provide different word lists whenever we instantiate this class.
This not only allows us to use different sets of words, but also removes the permanent link ("coupling") between the class `WordUtility` and a specific word list.

Dependency injection in more complex situations, where there are many inter-dependent components, is best done by a dependency injection framework such as for example Spring:

```
@RestController
public class SpringExample {
    
    @Autowired
    private AuthService authService;
    @Autowired
    private DataService dataService;
    @Autowired
    private UserService userService;
    ... 
```

In this snippet, we can see the `@Autowired` annotation which "injects" the dependencies automatically and allows us to use these services without providing them directly.

DI is should always be preferred to hard-wiring since it makes our components more flexible and easier to use.