The `break` and `continue` are keywords that allow us to change the behavior of loops.

### Break
```
        Student giora = null;
        for (Student student : students) {
            if(student.getName().equals("Giora")){
                giora = student;
            }
        }
```
Say we are looking for "Giora" in our students list, and we know that there is only one Giora.
There is no reason for us to continue the loop once we found our Giora.
```
        Student giora = null;
        for (Student student : students) {
            if(student.getName().equals("Giora")){
                giora = student;
                break;
            }
        }
```
This is where we use the `break` keyword.
This will stop the loop immediately, regardless of the stop condition.
If this logic was a part of a method, we could use the `return` keyword.
It will also stop the loop immediately.
```
    private Student getStudentByName(List<Student> students, String name) {
        for (Student student : students) {
            if (student.getName().equals(name)) {
                return student;
            }
        }
        throw new IllegalArgumentException(String.format("%s was not found in student list", name));
    }
```

### Continue
The continue keyword tells the loop to start the next iteration without executing any code beyond this point.
```
    public static void main(String[] args) {
        for (int i = 0; i < 20; i++) {
            if(i%2==0){
                continue;
            }
            System.out.println(i);
        }
    }
```
This code will print every odd number between 0 to 19.
When an even number enters the `if` block, the loop will immediately go to the next iteration (not getting to the println).
