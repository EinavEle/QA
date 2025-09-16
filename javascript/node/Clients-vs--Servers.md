
#### **HISTORY, BROWSER VS NODE, AND SPECS**

  

Node.js, created by Ryan Dahl, was introduced in 2009 and has continued to evolve since then. It’s a popular open source and cross platform project on [GitHub](https://github.com/nodejs/node). Node's JavaScript engine is based on the V8 JavaScript engine. This is Google’s JavaScript engine and is used in Google’s Chrome browser. This engine is written in C, not JavaScript, and it is very fast.

  

![](http://roa.h-cdn.co/assets/15/34/980x652/gallery-1440085966-jprice-roadandtrack-4471.jpg)

(above is another very fast V8, don't get confused)

  

For the most part, **running JS in node or in the browser is the same** - that is, same syntax, same built-in methods, same objects available to us - **but browser-specific operations are different**. More specifically:

-   Working with the DOM
-   There is no document object in Node, as there is no browser
-   As such, most of jQuery functionalities (interactions with the DOM) will not work in node - it makes no sense
-   The _value_ of this in the global scope
-   In the browser, the global this is the window object, in Node there is no window
-   We can make HTTP requests more liberally via node than through the browser, as we avoid [CORS issues](https://medium.com/@baphemot/understanding-cors-18ad6b478e2b)

  

There are other differences, but they will become clear as we go on.

  

----------

  

On a more technical note, node uses an event-driven, single threaded, server architecture and non-blocking I/O (input/output) model.

  

We'll learn what that means over the course of... this course, but the gist is that the interpreter* doesn’t pause or sleep while waiting for results. The interpreter is available for serving other requests. When one of the results is ready, a callback is invoked.

###### Remember, the **interpreter** is the part that actually reads our JS code and translates it to computer commands

  

Again - no need to worry about all these tech details right now, we'll explore them over time.