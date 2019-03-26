# JavaScript Syntax

## Contents
- **[Language fundamentals](#language-fundamentals)**
  - [Data types](#data-types)
  - [`const` & `let` in JavaScript](#const--let-in-javascript)
  - [Template Literals](#template-literals)
- **[Loops & Iteration Methods](#loops--iteration-methods)**
  - [Various Loops](#various-loops)
  - [Iteration Methods](#iteration-methods)
- **[Callbacks & Arrow Functions](#callbacks--arrow-functions)**
- **[Objects & Classes](#objects--classes)**
  - [Object literals](#object-literals)
  - [Accessing object properties & methods](#accessing-object-properties--methods)
  - [JS Class Syntax](#js-class-syntax)
  - [Getters & Setters](#getters--setters)
  - ['this' in Javascript](#this-in-javascript)

_______________

## Language fundamentals

### Data types
The latest ECMAScript standard defines seven data types for JavaScript - **six [primitive](https://developer.mozilla.org/en-US/docs/Glossary/Primitive) data types:**

- **`Boolean`**
- **`Null`** - a special value that explicitly represents "nothing" or something that does not exist. For example, this code states that age is unknown or empty:
    ```javascript
    let age = null;
    ```
- **`Undefined`** - means “value is not assigned”, i.e. a variable that's declared but not assigned any value.
- **`Number`** - with our without decimal point
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
- Can be run on `Array`, `Map` and `Set` objects, and executes a provided callback function once for each element (array) / key/value pair (Map) / value (Set). 
  ```javascript
  var movies = ['cats', 'Stans last dance', 'Flowers for her birthday', 'Hunger games'];

  movies.forEach( movie => alert(movie) );
  ```

#### for...of
- Can be run on iterable objects, including: `String`, `Array`-like objects (incl. Array, TypedArray, arguments or NodeList), `Map`, `Set`, and user-defined iterables. Invokes a custom iteration hook with statements to be executed for the value of each distinct property of the object.
  ```javascript
  for (var movie of movies) {
    console.log(movie);
  }
  ```
#### while
- Repeats a block of code until a particular condition is no longer true. Similar to `[do...while](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Statements/do...while)` loop.
  ```javascript
  var counter = 1;
  while (counter < 10 ) {
    console.log( counter );
    counter = counter + 1;
  }
  ```

### Iteration methods
#### map()
- Used on arrays; creates a new array with the results of calling a provided function on every element in the original array.
  ```javascript
  const fruits = ['apple', 'pear', 'cherry'];
  const capitalizedFruits = fruits.map( fruit => fruit.toUpperCase() );
  ```

_______________

## Callbacks & Arrow Functions
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
  var prop = 'breed';
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


