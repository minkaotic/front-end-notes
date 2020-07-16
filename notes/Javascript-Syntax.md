# JavaScript Syntax

## Contents
- **[Language Fundamentals / ES2015](#language-fundamentals--es2015)**
  - [Data Types](#data-types)
  - [`const` & `let` in JavaScript](#const--let-in-javascript)
  - [Template Literals](#template-literals)
  - [String Search Methods](#string-search-methods)
  - [Default Parameters](#default-parameters)
  - [Spread Operator & Rest Parameters](#spread-operator--rest-parameters)
- **[Arrow Functions](#arrow-functions)**
  - [First Class Functions in JS](#first-class-functions-in-js)
  - [Example with Callback](#example-with-callback)
  - [Immediately-invoked function expression](#immediately-invoked-function-expression)
  - [Neater code!](#neater-code)
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
- **[Destructuring](#destructuring)**
_______________

## Language Fundamentals / ES2015
> Whilst many of the syntax features described in this doc were introduced in ES2015, this section focuses on those that are more quickly explained. Other ES2015 features ([arrow functions](#arrow-functions), [destructuring](#destructuring)) have their own dedicated section, or are covered as part of a wider subject (e.g. [`find()`](#the-find-method) in [Loops & Iteration Methods](#loops--iteration-methods)).

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

### `const` & `let` in JavaScript
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

...you can use template literals for **string interpolation** (note the backticks!):
```javascript
alert(`The movie ${movie.title} plays at ${movie.time}`);
```

Template literals are also handy when using **multi-line strings** - compare the two approaches below:
```js
const fruitList = 
  "<ul>" +
    "<li>Kiwi</li>" +
    "<li>Lime</li>" +
    "<li>Pineapple</li>" +
  "</ul>";

const vegetableList = 
  `<ul>
    <li>Potato</li>
    <li>Onion</li>
    <li>Broccoli</li>
  </ul>`;

document.querySelector('.fruits').innerHTML = fruitList;
document.querySelector('.vegetables').innerHTML = vegetableList;
```

### String Search Methods
`startsWith()`, `endsWith()` and `includes()` essentially replace the cumbersome `indexOf()` method.

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


### Default Parameters
[Default parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters) let you set default values for parameters accepted by a function. 

Default values can be strings, booleans, objects, arrays or functions.

```js
function greet(name = 'Guil', timeOfDay = 'Day') {
  console.log(`Good ${timeOfDay}, ${name}!`);
}

greet();                        // Good Day, Guil!
greet('Hermes');                // Good Day, Hermes!
greet('Hermes', 'Morning');     // Good Morning, Hermes!
greet(undefined, 'Afternoon');  // Good Afternoon, Guil!
```

:exclamation: Note the use of `undefined` to use the default value for the first parameter, whilst setting a value for the second. By comparison, when only setting the first parameter (`greet('Hermes')`), this isn't needed.


### Spread Operator & Rest Parameters

[Rest parameters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters) let you specify an unknown number of parameters. The [spread operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Spread_syntax) lets you specify an unknown number of array properties, which allows you to quickly build and manipulate arrays. 

> :bulb: Even though both use the `...` syntax and thus look quite similar, they are pretty different. Whilst a rest parameter *collects* the arguments passed to a function, a spread operator *expands* an array (or any type of expression).

#### Rest parameter example

```js
function myFunction(name, ...params) { 
  console.log(name, params);
}

myFunction('Andrew', 1, 2, 3, 'kittens');  // Andrew [ 1, 2, 3, 'kittens' ]
myFunction('Andrew', 1)                    // Andrew [ 1 ]
```
**Things to note:**
- the rest parameter gathers any number of parameters given to a function into an array
- it must be the *last parameter* defined in the function signature
- can be named anything - doesn't have to be `params`

#### Spread operator examples

1. Spread operator passes ("spreads") all the values of `originalFlavors` and `newFlavors` into the `inventory` array:
```js
const originalFlavors = ['Chocolate', 'Vanilla'];
const newFlavors = ['Strawberry', 'Mint Chocolate Chip'];

const inventory = ['Rocky Road', ...originalFlavors, 'Neapolitan', ...newFlavors];

console.log(inventory);
// [ 'Rocky Road', 'Chocolate', 'Vanilla', 'Neapolitan', 'Strawberry', 'Mint Chocolate Chip' ]
```

2. Spread operator splits array into single values to be passed to a function as separate arguments:

```js
function myFunction (name, iceCreamFlavor) {
  console.log(`${name} really likes ${iceCreamFlavor} ice cream.`)
}

const args = ['Gabe', 'Vanilla'];

myFunction(...args);
```


> :bulb: You can in fact use the spread operator **on *any* [iterables](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)**, not just arrays! This includes: strings, Sets, Maps and even Generator functions!

Spread operator used on a string:
```js
...'abc' // -> 'a', 'b', 'c'
```

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
```js
exec(function (something) {
  console.log(something);
}, 'Hello!');
```

**3. Anonymous function using arrow syntax**
```js
exec((something) => {
  console.log(something);
}, 'Hello!');
```

### Example with Callback
Given an array `const movies = ['Cats', 'Stans last dance', 'Flowers for her birthday', 'Hunger games'];`, you can iterate over the array by using a `forEach()` loop, which takes a callback function:

```js
movies.forEach(function(movie) {
  alert(movie);
});
```

This can be simplified using arrow syntax:

```js
movies.forEach( movie => {
  alert(movie);
});
```

...and since it's only a one line function body, even further to:

```js
movies.forEach( movie => alert(movie) );
```

### Immediately-invoked function expression
An [Immediately-invoked Function Expression (IIFE)](https://flaviocopes.com/javascript-iife/) is a way to execute functions immediately, as soon as they are created. IIFEs are very useful because they don’t pollute the global object, and they are a simple way to isolate variables declarations.

#### Traditional function IIFE
Syntax definition:
```js
(function() {
  /* */
})()
```

Example:
```js
const message = (function(name) {
  return 'Hello ' + name + '!';
})('World');
console.log(message) // => 'Hello World!'
```

#### Arrow function IIFE
Syntax definition:
```js
(() => {
  /* */
})()
```

Example:
```js
const message = (name => {
  return 'Hello ' + name + '!';
})('World');
console.log(message) // => 'Hello World!'
```

:point_right: *We basically have a function defined inside parentheses, and then we append `()` to execute that function.* The wrapping parantheses turn the function declaration into an expression. The invoking parentheses at the end can alternatively be inside the wrapping parentheses too: `(() => {...}())`.

### Neater code!
:bulb: Due to their [lexical context binding](https://github.com/minkaotic/front-end-notes/blob/master/notes/JavaScript-Quirks.md#arrow-function) and simpler syntax, arrow functions have potential to greatly simplify our code - see [the second part of this video](https://teamtreehouse.com/library/arrow-functions) for an extreme example using IIFEs to resolve promises on a class method, where rewriting the following method inside a `classroom` object using arrow syntax:

```js
this.greet = function () {
  this.teacher.greet(this.students.length).then(
    // IIFE wrapping to ensure context is set as classroom object - not needed when using arrow functions!
    (function (classroom) {
      return function (greeting) {
        console.log(`${classroom.teacher.name} says: `, greeting);
      }
    })(this),
    function (err) {
      console.log(err);
    }
  )
}
```
...results in *this*!
```js
this.greet = () => {
  this.teacher.greet(this.students.length).then(
    greeting => console.log(`${classroom.teacher.name} says: `, greeting),
    err => console.log(err));
}
```

_______________

## Loops & Iteration Methods

### Various Loops
#### for
- Used for actions that need to run a particular number of times.
  ```js
  for ( let counter = 1; counter < 10; counter++) {
    console.log( counter );
  } 
  ```

#### forEach
- Can be run on `Array`, `Map` and `Set` objects, and executes a provided callback function once for each element (array) / key/value pair (map) / value (set). 
  ```js
  let movies = ['cats', 'Stans last dance', 'Flowers for her birthday', 'Hunger games'];

  movies.forEach( movie => alert(movie) );
  ```
> :zap: Unlike the older [`for`](#for) and [`while`](#while) loops, **`forEach` does not allow to break out early, it always runs on all members of the array.** ES2015 introduced [`for...of`](#forof) to provide additional capabilities, incl. breaking out early. 

> :bulb: The [`forEach`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach) callback function takes two additional optional parameters: `index` - the index in the array of the current item, and `array`, the whole array.

#### for...of
- Can be run on any iterable objects, including: `String`, `Array`, `NodeList`, `Map`, `Set`, arguments, and user-defined iterables. Invokes a custom iteration hook with statements to be executed for the value of each distinct property of the object.
  ```js
  for (let movie of movies) {
    console.log(movie);
  }
  ```
- Unlike `forEach`, `for...of` allows you to *break out of a loop early* when needed!
  ```js
  let teachers = [
    { name: 'Ken', comments: 'Amazing', rating: 4 },
    { name: 'Nick', comments: 'Automating', rating: 6 },
    { name: 'Sarah', comments: 'Amplifying', rating: 7 },
    { name: 'Alena', comments: 'Appending', rating: 8 }
  ];

  for(let teacher of teachers => {
    if (teacher.name === 'Nick') {
      console.log(teacher.rating);
      break; // skip checking rest of array items as it isn't needed
    }
  });
  ```
- It can also do funky things when used on some types of iterables, such operating on both the `key` and `value` of a `Map` object:
  ```js
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
  ```js
  let counter = 1;
  while (counter < 10 ) {
    console.log( counter );
    counter = counter + 1;
  }
  ```

### The `filter()` method
[`filter()`]() operates on an array and creates a new array with all elements that pass a given condition. Its syntax is `array.filter(currentItem => {return true/false})`. If the callback function returns true for the current item, it is added to the new array.

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

#### Removing duplicates from an array with `filter()`
> :bulb: Like [`forEach()`](#foreach), the other array methods covered here all take two additional optional parameters: the index in the array of the current item, and the array that the method (e.g. `filter()`) was called on.

The `array.indexOf(item)` method returns the index of the first occurrence of an item that is found in an array. We can therefore compare the index of the current element to the index of the current element in the array that `filter()` was called upon to determine if we've already encountered that element value. If the current element is a duplicate, its index will not equal the index of the first occurrence of its value.
```js
const numbers = [1, 1, 2, 3, 4, 3, 5, 5, 6, 7, 3, 8, 9, 10];

const unique = numbers.filter((number, index, array) => {
  return index === array.indexOf(number);
});

console.log(unique); // => [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
```

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
> NB: supplying no inital value can mess things up if the first element in the array (e.g. a string) does not fit your reduce logic (i.e. mathematical addition).
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

### The `find()` method

**Example** - finding the highest scoring player in a players array

```js
const players = [
  {name:"Roger", score:5},
  {name:"Elsie", score:4}
];

const highestScore = Math.max(...players.map(p => p.score))
const highestScoringPlayer = players.find(p => p.score == highestScore)

// highestScoringPlayer has value: {name: "Roger", score: 5}
```
_______________

## Objects & Classes
### Object literals
- *Object literals* are useful when modelling one single, specific thing. E.g.:
  ```js
  const ernie = {
    species: 'dog',
    age: 1,
    breed: 'pug',
    bark: function() {
      console.log('Woof!');
    }
  }
  ```
- To add a property or method to an object literal, simply assign it to the object: `ernie.color = 'black';`
- Since ES2015, a [shorter syntax](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Method_definitions) for method definitions is available: 
  ```js
  const ernie = {
      ...
      bark() {
        console.log('Woof!');
      }
    }
  ```
#### Object property shorthand 
Also since ES2015, [object property shorthand](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Object_initializer#New_notations_in_ECMAScript_2015) provides a shorter syntax for defining property keys in objects: when the interpreter encounters a variable assignment without a property key, *the variable name itself is used as the property key*.

```js
function submit(name, comments, rating = 5) {  
  let data = { name, comments, rating };  // object property shorthand
  
  for (let key in data) {
    console.log(key + ':', data[key]);
  }
}
              
submit('Paul', 'What a lovely man!', 10);
// name: Paul
// comments: What a lovely man!
// rating: 10
```


### Accessing object properties & methods
- Object properties can be accessed through either dot notation or bracket notation:

  | ***dot notation***         | ***bracket notation***        |
  | -------------------------- |-------------------------------|
  | `console.log(ernie.age);`  | `console.log(ernie['age']);`  |
  | `console.log(ernie.breed);`| `console.log(ernie['breed']);`|
  | `ernie.bark();`            | `ernie['bark']();`            |

- *Bracket notation* is useful when there is a need to generate dynamic properties, as the property name can be stored in a variable, and the objects property can then be accessed via that variable (*see example below*). It also allows you to create and access properties that may have spaces in the property key - perfect for handling JSON data.

  ```js
  let prop = 'breed';
  console.log(ernie[prop]);
  ```

### JS Class Syntax
To represent types with the same (or similar) properties, classes are much more robust than object literals. Class syntax was **introduced to Javascript in ES2015**, and comprises syntactic sugar on top of its original prototype syntax.

***A simple example***
```js
class Pet {
  constructor(species, age, breed, sound) {
    this.species = species;
    this.age = age;
    this.breed = breed;
    this.sound = sound;
    this.emoji = this.species === 'dog' ? '🐶' : '❓'
  }
  
  speak() {
    console.log(`${this.emoji}: ${this.sound}`);
  }
}

const ernie = new Pet('dog', 1, 'pug', 'woof!');
ernie.speak();
```

***Things to note***
- In JS, a class *can only have one constructor*. 
- In order to create an instance without any arguments, you can however set defaults, for example:
  ```js
  constructor(species = 'dog', age = 0, breed = 'unknown')
  ```
- **NB:** Declaring methods inside a class *doesn't* use the function keyword!

### Getters & Setters

**Definition & usage of a getter:**
- use `get` keyword to define a getter
- no parentheses when getter is accessed
```js
class Pet {
  get activity() {
    // code to return something
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
```js
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

_______________

### Destructuring
[Destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment) makes it possible to extract values from arrays or object, then assign those values to distinct variables.

#### Destructuring objects:
```js
// given an object
let toybox = { item1: 'car', item2: 'frisbee', item3: 'ball' };

// destructure some of its properties
let {item1, item3} = toybox;

// destructure property to a differently named variable
let {item2: disc} = toybox;

console.log(item1, item3, disc);  // car ball frisbee
```
:point_right: the destructured variables either need to match the property key, or they need to be associated with the key using `{keyName: varName}` syntax.

##### Destructuring nested objects:
```js
let parentObject = {
  title: 'Super Important',
  childObject: {
    title: 'Equally Important'
  }
}

let { title, childObject: { title: childTitle } } = parentObject

console.log(childTitle);  // 'Equally Important'
```

#### Destructuring arrays: 
- Whilst destructuring objects uses curly braces (`let {prop1, prop2, prop3} = myObj`), destructuring arrays ues square brackets (`let [a, b, c] = myArray`).
- Since we're dealing with arrays, we can combine destructuring with the spread operator.

```js
let widgets = ['widget1', 'widget2', 'widget3', 'widget4', 'widget5'];

// use destructuring to assign first 3 items to distinct variables,
// and store remaining items into separate array using spread operator
let [a, b, c, ...d ] = widgets;

console.log(a);  // widget 1
console.log(d);  // [ 'widget4', 'widget5' ]
```

#### Destructuring to set default values for function parameters:
- Objects are commonly passed as parameters to a function
- Sometimes we may want to set default parameters for some of the properties of an object used in function, in case that property isn't set on the object passed
- Destructuring the object in the function's parameter definition allows us to do this!
- in this case, rather than specifying the object parameter (`function getData(myObj) {...}`), we specify all the properties of the object we care about: `function getData({prop1, prop2, prop3 = 'foo'} = {}) {}`

In the following example, for whatever reason we are happy with the passed object's `url` property being null or undefined, but want to set a default of `'post'` for it's `method` property to fall back to:
```js
// destructuring the passed object in the parameter definition
function getData({ url, method = 'post' } = {}, callback) {
  callback(url, method);
}

getData({ url: 'myposturl.com' }, function (url, method) {
  console.log(url, method);
});
// myposturl.com post

getData({ url: 'myputurl.com', method: 'put' }, function (url, method) {
 console.log(url, method);
});
// myputurl.com put
```


