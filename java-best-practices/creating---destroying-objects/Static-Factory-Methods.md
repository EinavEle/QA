Static factory methods are a way to create a new object without calling its constructor directly.
Like so:
```
    public static Student createNewStudent(String name, int age, double grade){
        Student student = new Student();
        student.setName(name);
        student.setAge(age);
        student.setGrade(grade);
        return student;
    }
```

In this example we are returning a new student with the necessary parameters, just like we can do with a public constructor:

```
    public Student(String name, int age, double grade) {
        this.name = name;
        this.age = age;
        this.grade = grade;
    }
```

So.. why do we need this static factory method after all?
1. It gives us <b>better readability</b> than overloading constructors.
We can do this:
```
    public Student(String name, int age, double grade) {
        this.name = name;
        this.age = age;
        this.grade = grade;
    }

    public Student(String name, int age) {
        this(name,age,0.0);
    }
```
Instead of this, which is much less readable:
```
    public static Student createNewStudentWithNoGrade(String name, int age){
        Student student = new Student();
        student.setName(name);
        student.setAge(age);
        student.setGrade(0.0);
        return student;
    }
```
Obviously this difference becomes greater when the classes are more complex.

2. **Reusable objects**
Say we have an object that we only want to initialize once then return that same object whenever its called.
For example a singleton or any other lazy-loaded resource.
We can instantiate the object once, save it locally and return it when needed:
```
    public static getConfig(){
      if(config==null){
        config = loadConfigurationFile();
      }
      return config;
    }
```
3. **Returning subtypes or other implementations**
Static factory methods allow us to return more than the specific type unlike constructors.
```
    public static Student createNewStudent(String name, int age, double grade){
        if(grade>90){
            return new SpecialStudent(name,age,grade,"Engineering");            
        }else if(grade>80) {
            return new SpecialStudent(name,age,grade,"Psychology");
        }else{
            return new Student(name,age,grade);
        }
    }
```

4. **Performing common operations:**
Static factory methods are useful when performing common operations like conversions..

```
    public static Student fromPerson(Person person) {
        return new Student(person.getFirstName() + " " + person.getLastName(), person.getAge());
    }
```




  