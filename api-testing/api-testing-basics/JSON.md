# *Intro*
JSON is a simple way to exchange data between different software systems. It stands for JavaScript Object Notation, but you don't need to be a JavaScript expert to use it.

It's basically a way of writing data in a structured format that can be easily understood by computers. 
Think of it like a language that machines use to talk to each other.

One of the great things about JSON is that it's really easy to read and write, even for humans. 
It uses a simple syntax of curly braces, square brackets, and key-value pairs.

So, if you need to send data from one system to another, you can just convert it into a JSON format and send it along. 
And when the other system receives it, it can easily convert it back into its own format.

JSON Objects are collections of key-value pairs, enclosed in curly braces {}. 
Each key-value pair is separated by a colon (:), and each pair is separated by a comma (,). Objects are used to represent complex data structures and are often nested within each other.

JSON Arrays are ordered lists of values, enclosed in square brackets []. 
Values are separated by commas (,) and can be of any JSON data type, including strings, numbers, objects, and other arrays. Arrays are used to represent a collection of related items.
```JSON
{
  "name": "John Doe",
  "age": 30,
  "address": {
    "street": "123 Main St",
    "city": "Anytown",
    "state": "CA",
    "zip": "12345"
  },
  "phoneNumbers": [
    {
      "type": "home",
      "number": "555-555-1212"
    },
    {
      "type": "work",
      "number": "555-555-2121"
    }
  ]
}
```
In this example the "name" and "age" properties are simple string and number values, respectively. 
The "address" property is itself an object that contains multiple key-value pairs for the street, city, state, and zip. 
The "phoneNumbers" property is an array that contains two objects, each with its own set of key-value pairs for the type of phone number and the phone number itself.