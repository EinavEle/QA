Making defensive copies is the practice of copying objects in order to not allow direct access to them.
In **immutable** classes, when we give the user a pointer to an inner **mutable** object, he can modify it and **make our class mutable** de facto.
This is an immutable class:
```
public final class LibraryCard {
    private final Date issueDate;
    private final String nameOnCard;

    public LibraryCard(Date issueDate, String nameOnCard) {
        this.issueDate = issueDate;
        this.nameOnCard = nameOnCard;
    }

    public Date getIssueDate() {
        return issueDate;
    }

    public String getNameOnCard() {
        return nameOnCard;
    }
}
```
Theoretically, there should be no way to update the data of this "immutable" class, all of its members are final and are set only at the contstuctor.
But...
```
    public static void main(String[] args) {
        LibraryCard assaf = new LibraryCard(new Date(), "Assaf");
        Date issueDate = assaf.getIssueDate();
        System.out.println(issueDate);
        issueDate.setTime(473427212000L);
        System.out.println(assaf.getIssueDate());
    }
```
When running this code we get:
```
Sat Jan 01 13:33:32 EET 2022
Tue Jan 01 13:33:32 EET 1985
```
Well, look at the method `getIssueDate()`, it returns the `issueDate` which is a `Date` and is mutable.
When the user has access to this `issueDate` he can simply modify it (because `Date` is mutable), which changes the inner workings of our supposedly immutable object.
So how do we fix this?
```
    public Date getIssueDate() {
        return new Date(issueDate.getTime());
    }
```
Now, this is the result:
```
Sat Jan 01 13:33:32 EET 2022
Sat Jan 01 13:33:32 EET 2022
```
In this version, we simply return a copy of the inner `issueDate` and then any changes to it will not affect our object. This is called a defensive copy.

This issue can also occur at the constructor level:
```
    public static void main(String[] args) {
        Date myDate = new Date(1641036812000L);
        LibraryCard assaf = new LibraryCard(myDate, "Assaf");
        System.out.println(assaf.getIssueDate());
        myDate.setTime(473427212000L);
        System.out.println(assaf.getIssueDate());
    }
```
In this case I construct the object with one value and I change it later.
The inner object and `myDate` are the same. So, as long as I have access to `myDate` I can change the `LibraryCard`'s internals, even though the class does not allow it.
The solution here is very similar to the previous one:
```
    public LibraryCard(Date issueDate, String nameOnCard) {
        this.issueDate = new Date(issueDate.getTime());
        this.nameOnCard = nameOnCard;
    }
```
When I get to the object in the constructor, I make an internal copy of it so it won't be modifiable.
If I have any validations relevant to this parameter, I should perform them on the copied object in order to avoid the possibility of the object being changed between validation and copying.

```
    public LibraryCard(Date issueDate, String nameOnCard) {
        Date copyDate = new Date(issueDate.getTime());
        //Date must be this year
        if(!copyDate.after(START_DATE)){
            throw new IllegalArgumentException("Date must be later than " + START_DATE);
        }else{
            this.issueDate = copyDate;
        }
        this.nameOnCard = nameOnCard;
    }
```

In summary, make sure you defensively copy internal mutable objects of any immutable class.