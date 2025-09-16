It's very easy and simple to use a lot of strings in your code but there are a lot of cases where it is not efficient and makes your code less maintainable and more error prone.

### Don't use strings when:
1. You should use enum:
```
public void setAlarmTime(String weekday){
  switch(type){
    case "sunday":
      alarm.setTime(null);
    case "monday":
      alarm.setTime("06:00am");
    case "tuesday":
      alarm.setTime("08:00am");
    etc...
  }
}
```
This should be replaced with an enum type which will reduce the potential for errors.
```
public void setAlarmTime(Weekday weekday){
  switch(type){
    case SUNDAY:
      alarm.setTime(null);
    case MONDAY:
      alarm.setTime("06:00am");
    case TUESDAY:
      alarm.setTime("08:00am");
    etc...
  }
}
```

2. When you should use another type:
Sometimes when we get an input from an external source such as file/api response/keyboard input/etc.. we get it as a string but it really represent a number or a date or any other value.
In these cases we should use the appropriate type.
3. When we should use a class
We may sometimes be tempted to concatenate data into one string like this:
```
String shoppingList = "wine, bread, salt";
```
when we should really do this:
```
Collection<String> shopping = Arrays.asList("wine","bread","salt");
```
The first will require any user of this data to do the splitting and arranging of the data and will cause more code to be written and more mistakes to be made.
Another example my be:
```
String key = name+"#"+age;
```
instead of using a class with name and age as our key.
like so:
```
NameAgePair key = new NameAgePair(name, age);
```
This removes the danger of splitting the data incorrectly if for example i have a name with `#` in it.

### Use StringBuilder when building complex strings
We often need to build a string from many other strings.
for example when reading a file.

```
  public static String readFile(String fileName) throws IOException {
        StringBuilder stringBuilder = new StringBuilder();
        try(BufferedReader reader = new BufferedReader(new FileReader(fileName))){
            String line;
            String ls = System.getProperty("line.separator");
            while ((line = reader.readLine()) != null) {
                stringBuilder.append(line);
                stringBuilder.append(ls);
            }
        }
        return stringBuilder.toString();
    }
```