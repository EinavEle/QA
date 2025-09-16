
Now it's time to learn about one of Node's best features: modules.

  

Modules in node are similar to regular JS modules we've learned about, but now these work as an actual feature of the environment.

  

By that we mean that **in node, every file you write is automatically wrapped in a module for you** - and this is exciting. As such, we can now say "module" and "file" interchangeably: every file in node is a module.

  

This is exciting because node allows us to **export** and **import** modules from one file to another - this means that we no longer have to rely on our index.html to import everything and allow every piece of our code to be accessible on a global level.

# Module systems
There are different types of JavaScript module systems, or in simpler words there are different ways to import and export code from file to file.
The first module system that was supported by NodeJS is called CommonJS and we will learn it first.
Lately, NodeJS also added support for the ES modules system, and we will cover that system as well, as it is common in React and other popular js libraries.  
