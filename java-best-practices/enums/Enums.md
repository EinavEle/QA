Enums are very useful and can help us maintain a certain order and clarity in our code.
Enums are special data type that can hold predefined constant values.
we should use them whenever we have types of constant values that are all known in advance, or if we wish to give those constant a clearer and unified meaning.
when we define a new enum variable, it must be equal to one of the values that have been predefined for it, so you might also think of Enum as Object, that can hold only set of predefine values.
For example the seasons of the year:
```
public enum Season {
    SUMMER,
    AUTUMN,
    WINTER,
    SPRING
}
```

There is no reason to use `String` as we know they can be a source of many mistakes.
Using enums makes sure that everybody will use the exact same constant when choosing a season.

### Extra values of enums
Sometimes we want to add some attributes to our enums which can be another constant related to our `Season`.
For example we want to add the temperature range of each season, we can do this like that:
```
public enum Season {
    SUMMER(24,44),
    AUTUMN(14,30),
    WINTER(0,22),
    SPRING(16,25);

    Season(int lowTemp, int highTemp) {
        this.lowTemp = lowTemp;
        this.highTemp = highTemp;
    }
    
    public final int lowTemp;
    public final int highTemp;
}
```
We have added the fields `lowTemp` and `highTemp` and we also added them to the constructor of our enum.
Now every season has it's temperature range and it is a part of our constant data.
We can use it like this:
```
System.out.println(Season.SPRING.highTemp);
```

### Enum methods
Let's say we need to invoke some function depending on the season.
How would we do this?
```
    private void temperatureControl(Season season){
        switch (season) {
            case SUMMER:
                System.out.println("Turn on AC");
                break;
            case AUTUMN:
                System.out.println("Open windows");
                break;
            case WINTER:
                System.out.println("Turn on heater");
            case SPRING:
                System.out.println("Do nothing");
                break;
            default:
                throw new IllegalArgumentException("No such season");
        }
    }
```
While this method will work, it is not the perfect solution.
Why?
First of all, it leaves a place for human error, for example what will happen if sometime in the future we will add the `MONSOON` season?
We will need to make sure that every `switch` we have in our program is updated to handle this new `Season` case.
So what is the better solution?
We can implement this `temperatureControl()` function inside our enum.
```
public enum Season {
    SUMMER(24,44){
        @Override
        public void temperatureControl() {
            System.out.println("Turn on AC");
        }
    },
    AUTUMN(14,30) {
        @Override
        public void temperatureControl() {
            System.out.println("Open windows");
        }
    },
    WINTER(0,22) {
        @Override
        public void temperatureControl() {
            System.out.println("Turn on heater");
        }
    },
    SPRING(16,25) {
        @Override
        public void temperatureControl() {
            System.out.println("Do nothing");
        }
    };

    Season(int lowTemp, int highTemp) {
        this.lowTemp = lowTemp;
        this.highTemp = highTemp;
    }

    public final int lowTemp;

    public final int highTemp;

    public abstract void temperatureControl();
}
```
By adding an abstract method to our enum, we enforce every constant instance of `Season` to implement `temperatureControl()` then we can use it safely.
```
season.temperatureControl();
```
And, whenever we decide to add a new `Season` the compiler will force us to add a `temperatureControl()` method to it so there is no way we forget to implement it.

To summarize, enums are powerful and we should use them whenever we have known constants even if the list of constants may change in the future.
Correct use of enums can save a lot of time and code.