Before we close this class there are a few things you should never do with classes and interfaces:
1. Do not use interfaces for anything but defining types.
An interface should define the behavior of a class and not anything else.
2. Do not define more than one top-level (not nested) class in a file.
This can cause many errors and makes the code a lot less readable.
3. Do not use tagged classes (or catch-all classes).
Tagged classes are classes that represent more than one type of object by constructing different objects according to a received tag.
Example from Effective Java:
```
// Tagged class - vastly inferior to a class hierarchy! (Page 109)
class Figure {
    enum Shape { RECTANGLE, CIRCLE };

    // Tag field - the shape of this figure
    final Shape shape;

    // These fields are used only if shape is RECTANGLE
    double length;
    double width;

    // This field is used only if shape is CIRCLE
    double radius;

    // Constructor for circle
    Figure(double radius) {
        shape = Shape.CIRCLE;
        this.radius = radius;
    }

    // Constructor for rectangle
    Figure(double length, double width) {
        shape = Shape.RECTANGLE;
        this.length = length;
        this.width = width;
    }

    double area() {
        switch(shape) {
            case RECTANGLE:
                return length * width;
            case CIRCLE:
                return Math.PI * (radius * radius);
            default:
                throw new AssertionError(shape);
        }
    }
}
```
This kind of implementation is ineffective, unreadable, and very much error prone.
This class should have been split into a few classes where the common logic should be in a base class.
