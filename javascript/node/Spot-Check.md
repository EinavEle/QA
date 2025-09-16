Replace the content of the previous `package.json`
with this content:

```
{
  "name": "imports",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "",
  "license": "ISC"
}
```
and run the `shape.js` file.

What is the result? Why is this the result?


<details>
  <summary>
     Solution
  </summary>
    We get a warning:

```console
Warning: To load an ES module, set "type": "module" in the package.json or use the .mjs extension.

```
and an Error:

```console
SyntaxError: Cannot use import statement outside a module
```  

This is because the package.json file does not contain the 
`type: module`
line

To fix the Error add this line.
</details>