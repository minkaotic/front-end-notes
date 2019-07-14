# JavaScript Syntax

## Contents
- **[Language Fundamentals / ES2015](#language-fundamentals--es2015)**
  - [Data Types](#data-types)
  - [`const` & `let` in JavaScript](#const--let-in-javascript)
  - [Template Literals](#template-literals)
  - [String Search Methods](#string-search-methods)
- **[Arrow Functions](#arrow-functions)**
  - [First Class Functions in JS](#first-class-functions-in-js)
  - [Example with Callback](#example-with-callback)
- **[Loops & Iteration Methods](#loops--iteration-methods)**
  - [Various Loops](#various-loops)
  - [`filter()`](#the-filter-method)
  - [`map()`](#the-map-method)
  - [`reduce()`](#the-reduce-method)
  - [`find()`](#the-find-method)
- **[Objects & Classes](#objects--classes)**
  - [Object literals](#object-literals)
  - [Accessing object properties & methods](#accessing-object-properties--methods)
  - [JS Class Syntax](#js-class-syntax)
  - [Getters & Setters](#getters--setters)
  - ['this' in Javascript](#this-in-javascript)
- **[JS Concurrency Model & Event Loop](#js-concurrency-model--event-loop)**
_______________

## Language Fundamentals / ES2015

### Data Types
The latest ECMAScript standard defines seven data types for JavaScript - **six [primitive](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) data types:**

- **`Boolean`**
- **`Null`** - a special value that explicitly represents "nothing" or something that does not exist. For example, this code states that age is unknown or empty:
    ```javascript
    let age = null;
    ```
- **`Undefined`** - means “value is not assigned”, i.e. a variable that's declared but not assigned any value.
- **`Number`** - with or without decimal point
- **`String`**
- **`Symbol`** - a new data type in ES2015 that represents a unique identifier. See [MDN docs](https://developer.mozilla.org/en-US/docs/Glossary/Symbol) for more detail.

The **7th data type is `Object`**.
 
Use the `typeof` operator to see which data type is stored in a variable. For example:

```javascript
let name = "Alena Holligan";
alert(typeof name); // returns "string"

let score = 150;
alert(typeof score); // returns "number"

let x;
alert(typeof x); // returns "undefined"
```

### const & let in JavaScript
**Best practice:**
> `const` is your first / best option when declaring variables in JavaScript, as it avoids re-assignment bugs. Use `let` only if you have an explicit need to re-assign a given variable. However, you may need to use `var` if there is a need to support older browsers - check *[Can I Use](https://caniuse.com/#search=let)*.

Note some quirks of `const`, `let` and `var`:

Whilst **`const`** prevents a variable from being *re-assigned*, it does not prevent complex data types like arrays and objects from being *modified*. The following code will not error:
```javascript
const days = ['Monday'];
days.push('Tuesday');   // add a new value
days[0] = 'Friday';     // overwrite existing value

const person = { first_name: 'Imogen'};
person.last_name = 'Heap';      // add a new value
person.first_name = 'Andrew';   // overwrite existing value
```

Whilst **`let`** is similar to `var` in that it declares a variable that can be re-assigned, *scoping works differently* between the two:

- `var` has **function level scoping**: Even if a variable is declared within a block (i.e. loop or conditional), the JavaScript interpreter will 'hoist' the declaration to the top of the function! This can be very confusing, and it's therefore considered best practice to declare all the variables used in a function at the beginning of the function. Even then, awkward pitfalls with things like counter variables in a loop remain - see [this video](https://teamtreehouse.com/library/using-let-with-for-loops) for an example.

- `let` (and `const`) have **block level scoping**, so variables declared with them are limited to the scope of their containing block, and won't be hoisted.

- [Great article with more detail on the above](https://love2dev.com/blog/javaScript-var-let-const/)


### Template Literals
Instead of concatenating strings like this:
```javascript
alert("The movie " + movie.title + " plays at " + movie.time);
```

...you can use template literals (note the backticks!):
```javascript
alert(`The movie ${movie.title} plays at ${movie.time}`);
```

### String Search Methods
`startsWith`, `endsWith` and `includes` essentially replace the cumbersome `indexOf` method.

Given:
```javascript
const stringToSearch = 'Hi, I am a nice string!';
```
...confirm match at start of string
```javascript
// old
if (stringToSearch.indexOf('Hi,') === 0) {...}
// new
if (stringToSearch.startsWith('Hi,')) {...}
```
...confirm match at end of string
```javascript
// old
if (stringToSearch.indexOf('string!') === stringToSearch.length - 'string!'.length) {...}
// new
if (stringToSearch.endsWith('string!')) {...}
```
...check string includes
```javascript
// old
if (stringToSearch.indexOf('nice') > -1) {...}
// new
if (stringToSearch.includes('nice')) {...}
```

- `startsWith` and `includes` take an optional second parameter to specify the index at which to start searching
- `endsWith` takes an optional second parameter to specify the index at which to end the search

_______________

## Arrow Functions
A new syntax for writing JS functions as of ES2015; akin to 'lambda functions' in other programming languages. Arrow functions provide a short syntax for defining functions, and also simplify function scope.

Traditional syntax:
```javascript
// function declaration
function square(x) {
    return x * x;
}

// function expression
let square = function(x) {
    return x * x;
}
```

Arrow syntax:
```javascript
const square = (x) => {
    return x * x;
}
```
- Additionally, if your function takes *exactly one parameter*, you can remove the paranthesis.
- If the function body is *only one line of code*, you can further remove the `return` key word as well as the curly braces.

Super concise arrow syntax:
```javascript
const square = x => x * x;
```

### First Class Functions in JS
Given a function that takes another function as an argument, such as:
```javascript
function exec(func, arg) {
  func(arg);
}
```
...then the following three ways of calling it are equivalent:

**1. Traditional function declaration**
```javascript
function say(something) {
  console.log(something);
}

exec(say, 'Hello!');
```

**2. Passing an anonymous function**
```javascript
exec(function (something) {
  console.log(something);
}, 'Hello!');
```

**3. Anonymous function using arrow syntax**
```javascript
exec((something) => {
  console.log(something);
}, 'Hello!');
```

### Example with Callback
Given an array `const movies = ['Cats', 'Stans last dance', 'Flowers for her birthday', 'Hunger games'];`, you can iterate over the array by using a `forEach()` loop, which takes a callback function:

```javascript
movies.forEach(function(movie) {
  alert(movie);
});
```

This can be simplified using arrow syntax:

```javascript
movies.forEach( movie => {
  alert(movie);
});
```

...and since it's only a one line function body, even further to:

```javascript
movies.forEach( movie => alert(movie) );
```

_______________

## Loops & Iteration Methods

### Various Loops
#### for
- Used for actions that need to run a particular number of times.
  ```javascript
  for ( let counter = 1; counter < 10; counter++) {
    console.log( counter );
  } 
  ```

#### forEach
- Can be run on `Array`, `Map` and `Set` objects, and executes a provided callback function once for each element (array) / key/value pair (map) / value (set). 
  ```javascript
  let movies = ['cats', 'Stans last dance', 'Flowers for her birthday', 'Hunger games'];

  movies.forEach( movie => alert(movie) );
  ```
> :zap: Unlike the older [`for`](#for) and [`while`](#while) loops, you cannot break out of `forEach` early, it always runs on all members of the array.

> :bulb: The [`forEach`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) callback function takes two additional optional parameters: `index` - the index in the array of the current item, and `array`, the whole array.

#### for...of
- Can be run on any iterable objects, including: `String`, `Array`, `NodeList`, `Map`, `Set`, arguments, and user-defined iterables. Invokes a custom iteration hook with statements to be executed for the value of each distinct property of the object.
  ```javascript
  for (let movie of movies) {
    console.log(movie);
  }
  ```
- It can also do funky things when used on some types of iterables, such operating on both the `key` and `value` of a `Map` object:
  ```javascript
  let iterable = new Map([['a', 1], ['b', 2], ['c', 3]]);
  for (let entry of iterable) {
    console.log(entry);
  }
  for (let [key, value] of iterable) {
    console.log(value);
    console.log(key);
  }
  ```

#### while
- Repeats a block of code until a particular condition is no longer true. Similar to [`do...while`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/do...while) loop, which will always execute the code block at least once as condition is checked at the end of the loop.
  ```javascript
  let counter = 1;
  while (counter < 10 ) {
    console.log( counter );
    counter = counter + 1;
  }
  ```

### The `filter()` method
[`filter()`]() operates on an array and creates a new array with all elements that pass a given condition. Its syntax is `array.filter(currentItem => {return true/false})`. Iff the callback function returns true for the current item, it is added to the new array.

**Example: Given an array...**
```js
const names = ['Selma', 'Ted', 'Mike', 'Sam', 'Sharon', 'Marvin'];
```
**...create new array with filtered results**
```js
const sNames = names.filter(name => {
  return name.charAt(0) === 'S';
});
```
...or equivalent using concise arrow syntax:
```js
const sNames = names.filter(name => name.charAt(0) === 'S');
```
...or equivalent using nice readable function being extracted:
```js
const startsWithS = name => name.charAt(0) === 'S';
const sNames = names.filter(startsWithS);
```
**Result:** `sNames` will be `[ 'Selma', 'Sam', 'Sharon' ]`.


### The `map()` method
[`map()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/map) is used on arrays and creates a new array with the results of calling a provided function on every element in the original array. *The new array will therefore always have the same number of items as the original array.*

**Example 1**
```js
const fruits = ['apple', 'pear', 'cherry'];
const capitalizedFruits = fruits.map( fruit => fruit.toUpperCase() );
```
**Example 2**
```js
const prices = [5, 4.23, 6.4, 8.09, 3.20];
const toDisplayPrices = price => `£${price.toFixed(2)}`;
const result = prices.map(toDisplayPrices);
// result: [ '£5.00', '£4.23', '£6.40', '£8.09', '£3.20' ]
```

### The `reduce()` method
[`reduce()`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/reduce) executes a given reducer function on each element of the array, resulting in a single output value. 
- `reduce()` takes two arguments: a callback function (the reducer function) and an initial value.
- The initial value argument is optional; it represents the value to use as the first argument to the first call of the callback. If no initial value is supplied, the first element in the array will be used and skipped.
> NB:
- The reducer function takes at least two arguments: an accumulator, which tracks the result of operations thus far, and the current value from the input array.
- Once `reduce()` has iterated over the whole array, it returns the value of the accumulator.
- Additionally, the reducer function can take two optional parameters to represent the current index and the source array.

**Example 1** - with or without initial value
```js
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15
```
**Example 2** - simple logic
```js
const prices = [6.75, 3.10, 4.00, 8.12];

const total = prices.reduce((sum, price) => sum + price);
// resulting total: 21.97
```
**Example 3** - more complex logic, making `return` explicit
```js
const names = ['Gary', 'Pasan', 'Gabe', 'Treasure', 'Gengis', 'Gladys', 'Tony'];

const startsWithG = names.reduce((sum, name) => {
  if (name[0] === 'G') {
    return sum + 1;
  }
  return sum;
}, 0);

// Resulting value of startsWithG: 4
```

### `find()`

_______________

## Objects & Classes
### Object literals
- *Object literals* are useful when modelling one single, specific thing. E.g.:
  ```
  const ernie = {
    species: 'dog',
    age: 1,
    breed: 'pug',
    bark: function(){
      console.log('Woof!');
    }
  }
  ```
- To add a property or method to an object literal, simply assign it to the object: `ernie.color = 'black';`

### Accessing object properties & methods
- Object properties can be accessed through either dot notation or bracket notation:

  | ***dot notation***         | ***bracket notation***        |
  | -------------------------- |-------------------------------|
  | `console.log(ernie.age);`  | `console.log(ernie['age']);`  |
  | `console.log(ernie.breed);`| `console.log(ernie['breed']);`|
  | `ernie.bark();`            | `ernie['bark']();`            |

- *Bracket notation* is useful when there is a need to generate dynamic properties, as the property name can be stored in a variable, and the objects property can then be accessed via that variable (*see example below*). It also allows you to create and access properties that may have spaces in the property key - perfect for handling JSON data.

  ```
  let prop = 'breed';
  console.log(ernie[prop]);
  ```

### JS Class Syntax
To represent types with the same (or similar) properties, classes are much more robust than object literals. Class syntax was **introduced to Javascript in ES2015**, and comprises syntactic sugar on top of its original prototype syntax.

***A simple example***
```
class Pet {
  constructor(species, age, breed, sound) {
    this.species = animal;
    this.age = age;
    this.breed = breed;
    this.sound = sound;
  }
  
  speak() {
    console.log(this.sound);
  }
}

const ernie = new Pet('dog', 1, 'pug', 'woof!');
ernie.speak();
```

***Things to note***
- In JS, a class *can only have one constructor*. 
- In order to create an instance without any arguments, you can however set defaults, for example:
  ```
  constructor(species = 'dog', age = 0, breed = 'unknown')
  ```
- **NB:** Declaring methods inside a class *doesn't* use the function keyword!

### Getters & Setters

**Definition & usage of a getter:**
- use `get` keyword to define a getter
- no parentheses when getter is accessed
```
class Pet {
  get activity() {
    ///code to return something
  }
}

const elsie = new Pet();
console.log(elsie.activity);
```

**Definition & usage of a setter:**
- Use `set` keyword to define a setter.
- Setters always receive exactly 1 parameter, which is the value that is assigned to the setter when called (i.e. `elsie.owner = 'Mia';`). As with getters, no parentheses are used when calling setters.
- Setters can receive a value, perform some optional logic on it, then assign it to *either a new or existing property of the object*.
- The name of a property can never be the same as the name of a getter or setter method, so by convention, the backing property of a setter uses an underscore in front of it.
- Typically, a matching getter method will be defined that returns the value of the backing property.
```
class Pet {
  set owner(owner) {
    this._owner = owner;
  }
  
  get owner() {
    return this._owner;
  }
}

const elsie = new Pet();
elsie.owner = 'Mia';
console.log(elsie.owner);
```
____________________

## 'this' in Javascript
There are 4 ways in which `this` takes a value in JS:

***1. In normal function calls***
```
function tryingThis() {
  console.log(this);
};
```
- Here, `this` refers to the *global scope* or *global context* when run in a browser, i.e. the `Window` object, or it refers to the module context if run in Node.

***2. Within methods on objects***
- see [JS Class Syntax](#js-class-syntax) for an example - although the same possibilities apply to object literals
- in this case, `this` refers to the object itself, and is usually used to reference its properties

***3. In a constructor function***
```
let City = function(name, state) {
    this.name = name || 'Portland';
    this.state = state || 'Oregon';
};
```
- Constructor functions are essentially the old syntax for object creation, prior to [JS Class Syntax](#js-class-syntax).
- Here, `this` refers to the instance that will be instantiated when `new City()` is called.

4. A function invoked with `.call`, `.apply` or `.bind` (advanced use; not explained here)

____________________

## JS Concurrency Model & Event Loop
JavaScript is a single-threaded language and has a concurrency model based on an "event loop". This model is quite different from models in other languages like C and Java.
* The *event loop* is a constantly running process that checks i fthe call stack is empty
* A JavaScript runtime uses a *message queue*, which is a list of messages to be processed
* Each message has an associated *function*, which gets called in order to handle the message.
* At some point during the *event loop*, the runtime starts handling the messages on the queue, starting with the oldest one.

**Examples:**
* In web browsers, messages are added to the event loop anytime an event occurs and there is an event listener attached to it. If there is no listener, the event is lost.

*[to be continued...]*

For more detail, refer to [this article on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop) or [this article on HackerNoon](https://hackernoon.com/understanding-js-the-event-loop-959beae3ac40).
