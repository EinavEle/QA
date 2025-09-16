For the purpose of better performance and readability, we should always avoid creating objects if we don't really need them.

Here are some examples of how we can avoid creating unnecessary objects:
1. **Static factories:**
As we saw earlier this lesson, we can use static factory methods to build an object once and use it many times afterwards.
2. **Caching:**
Caching can be tricky, but the general idea is that if you use a resource often, you can save it "in memory" so it can be easily used again.
For example, if you have a regex pattern that gets reused again and again on different strings, there is no need to compile this pattern more than once.
```
    private static final Pattern pat = Pattern.compile("http://(.*)\"");
    public boolean containsLink(String str){
        return pat.matcher(str).matches();
    }
```

instead of:
```
    public boolean containsLink(String str){
        Pattern pat = Pattern.compile("http://(.*)\"");
        return pat.matcher(str).matches();
    }
```

3. **Avoid object pools unless totally necessary:**
Object pools are collections of pre-made objects ready to use on demand.
Whenever we consider using an object pool, we should make sure we actually need it and it doesn't make us create unnecessary objects and waste more time and effort than it saves.
The perfect example of an object pool is a database connection pool.
In a database connection pool, we have a number of connections ready for use, and the user can very quickly perform queries using them.
The reason why a database connection pool makes sense is the fact the creating a connection to the DB is an expensive action and we do not want to make the user wait for a new connection whenever they want to query the DB.

4. **Beware of autoboxing:**
Autoboxing is the automatic creation of an object out of a primitive type.
In some cases, when we use boxed primitives, along with primitives we can make Java turn our primitives into boxed primitives, which creates objects that we did not intend to create.
```
    private static long sum(){
        Long sum = 0L;
        for (long i = 0; i < Integer.MAX_VALUE; i++) {
            sum += i;
        }
        return sum;
    }
```
This method creates a `Long` object out of the primitive `i` every time it adds `i` to `sum`.
This could be avoided by declaring `sum` as `long` instead of `Long`.
This small change between `Long` and `long` could have a high price in performance.
In testing, the `Long` version took approx. 5 times longer.