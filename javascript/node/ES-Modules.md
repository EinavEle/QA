Now let's look at another modules system called ES modules.

## Configuration
In order for us to work with the ES module system in NodeJS we need to add a small configuration.

First create a new folder. In it create a configuration file called `package.json`.
Copy the following json into the `package.json` file:
```
{
  "name": "test",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "type": "module",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```
Specifically notice this line:
```js
  "type": "module"
```

This is the setup that will make the ES modules system work in node.

We will talk later about the `package.json` file and understand more what it is used for.

Now we are all set!

## Named Exports

Let's go back to our example, create a circleUtils.js file, and add the following code inside:
```JavaScript
const title = "Circle Utility";
const pi = 3.14159;

const calcCircleArea = function (radius) {
  return pi * radius * radius;
};

export { title, pi, calcCircleArea };
```

Now the export part looks a bit different:
```JavaScript
export { title, pi, calcCircleArea };
```

Here we export an Object with 3 properties: 
- title
- pi
- calcCircleArea

This is called a **named export**. Later we will see another type of export, called a **default export**.
  
To see how the import works, go ahead and create another file called shapesApp.js, and add the following code there:
```
import { title, pi, calcCircleArea } from './circleUtils.js';
console.log("pi", pi);
```
 

In this separate file, we can **import** the keys that we exported using the export keyword.  

In this case, the file (i.e. module) in which we're interested is in the same directory, so we preface its filename with ./ - notice also that in this case we **do write out the** **.js** **extension**.

  

If you run the above code (of course, using the node shapesApp.js command in your terminal, or by pressing F5 in VS Code), you'll see the following object in the console:

  
```
pi 3.14159
```
  
Note that this is a modular syntax.
Here we import all the variables that we have defined in circleUtils. But we can import just one or two, exactly the ones we need

```
import { title } from './circleUtils.js';
```

or

```
import { title, pi } from './circleUtils.js';
```

## Default Export

Another way to export is to export a single object like this:

```js
const title = "Circle Utility";
const pi = 3.14159;

const calcCircleArea = function (radius) {
  return pi * radius * radius;
};

const calcUtils = { title, pi, calcCircleArea }

export default calcUtils;
```

Here we are exporting an object with 3 properties: title, pi, calcCircleArea.
Note the `default` keyword!

They way to import this object in our `shape.js` file is:

```js
import calcUtils  from './circleUtils.js';


console.log(calcUtils.calcCircleArea(5));
```

Note that here we import without `{}`.