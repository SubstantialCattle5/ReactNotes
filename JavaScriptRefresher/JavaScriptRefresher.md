# JS Refresher

## [let](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/let) , [const](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/const)

You use `let` instead of `var` as a variable.

`const` instead of `var` if you plan on
never re-assigning this "variable" (effectively turning it into a
constant therefore).

## [ES6 Arrow Function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Arrow_functions)

Arrow functions are a different way of creating functions in JavaScript. Besides a shorter syntax, they offer advantages
when it comes to keeping the scope of the `this` keyword.

#### Standard Function

```js
function callMe(name) {
  console.log(name);
}
```

**becomes**

```js
const callMe = function (name) {
  cosole.log(name);
};
```

#### Important:

1. **no arguments**

```js
const callMe = () => {
  console.log("nilay");
};
```

2. **exactly one argument**

```js
const callMe = () => {
  console.log("nilay");
};
```

3. **when just returning a value**

```js
const returnMe = (name) => name;
```

## Exports & Imports

In react projects , you split your code across mulitple JavaScript files - so called Modules to keep each file/module focused and manageable.

To access functionality in another file, you need to add `export` (to make it available) and `import` (to get access) statements.

There are two different types of Exports:

**default**

```js
 export default ... ;
```

**named**

```js
export const someData = ...;
```

Import **default exports** like :

```js
import someNameOfYourChoice from "./path/to/file.js";
```

**Named exports** have to be imported by their name :

```js
import { someData } from "./path/to/file.js";
```

_A file can contain only one default and an unlimited amount of named exports.You can also mix the one default with any amount of and exports in one and the same file._

When importing **named exports** , you can also import all the named exports at once with the following syntax -

```js
import * as upToYou from "./path/to/file.js";
```

## Classes

Classes are a feature which basically replace constructor functions and prototypes. You can define blueprints for JavaScript objects with them.

```js
class Person {
  name = "nilay";
}

const person = new Person();
console.log(person.name);
```

Using inheritance when using Classes :

```js
class Humans {
  species = "human";
}

class Person extends Human {
  name = "Nilay";
  printMyName = () => {
    console.log(this.name);
  };
}

const person = new Person();
person.printMyName();
console.log(person.species);
```

## Spread & Rest Operators

The spread and rest operators actually use the same
syntax: `...`

It's usage determines whether you're using it as the spread or rest operator.

#### Using the Spread Operator

The spread operator allows you to pull elements out of an
array (=> split the array into a list of its elements) or pull the properties out of an object.

```js
const oldArray = [1, 2, 3];
const newArray = [...oldArray, 4, 5]; // this is now [1,2,3,4,5]
```

Spread Operator used on Object

```js
const oldObject = { name: "nilay" };
const newObject = { ...oldObject, age: 19 }; // new object would be then {name:'nilay' , age:19}
```

## Destructing

Destructuring allows you to easily access the values of
`arrays` or `objects` and assign them to variables.

#### Arrays -

```js
const array = [1, 2, 3];
const [a, b] = array;
console.log(a); // prints out value of a
console.log(b); // prints out value of b
console.log(array); // prints out the array
```

#### Objects -

```js
const myObj = {
  name: "Nilay",
  age: 19,
};
const { name } = myObj;
console.log(name); // spits out nilay 
console.log(age); // spits out undefined 
console.log(myObj); // spits out {name:'nilay' , age:19}
```
