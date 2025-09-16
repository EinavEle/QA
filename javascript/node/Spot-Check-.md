Here is the content of a `main.js` file:

```js
import { foo, boo } from './utils.js';
import Person from './Person.js';

foo(); //should print foo
boo(); //should print boo

const p1 = new Person('John', 'Doe', 30, 'Tel Aviv');
console.log(p1.firstName);
```

Add the relevant files:
- utils.js
- Person.js

and make the code work!

<details><summary>
  Click here to reveal the answer.
</summary>

utils.js
```js
const foo = function () {
  console.log('foo');
};

const boo = function () {
  console.log('boo');
};

export { foo, boo };
```

Person.js
```js
class Person {
  constructor(fname, lname, age, city) {
    this.firstName = fname;
    this.lastName = lname;
    this.age = age;
    this.city = city;
  }
}

export default Person;
```
</details>

