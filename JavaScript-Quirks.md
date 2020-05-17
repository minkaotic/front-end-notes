# JavaScript Quirks

## Contents
- **[`this` in Javascript](#this-in-javascript)**
  - [Different invocation types](#different-invocation-types)
  - [Bound function](#bound-function)
  - [Arrow function](#arrow-function)
_____________

## `this` in Javascript
Sources: [MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this) | [w3schools](https://www.w3schools.com/js/js_this.asp) | [Gentle Explanation of "this" in JavaScript](https://dmitripavlutin.com/gentle-explanation-of-this-in-javascript/)

**In JS, `this` refers to *the current execution context*.** When used by itself, i.e.:
```js
const x = this;
```
`this` always refers to the *global scope* or *global context*; i.e. the `window` object when run in a browser, or the module context when run in Node. But this use by itself, outside of any function scope, is very rare (and not that useful).

The complexity arises because **where `this` is used within a *function***, the context - and thus the value of `this` - depends on what invocation type the given function is! Moreover, **[`strict` mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode)** (a restricted variant of JavaScript offering better security and stronger error checking) also affects the execution context within function scopes!

### Different invocation types
JS has 4 function invocation types:
- [function invocation](#function-invocation): `alert('Hello World!')`
- [method invocation](#method-invocation): `console.log('Hello World!')`
- [constructor invocation](#constructor-invocation): `new RegExp('\\d')`
- [indirect invocation](#indirect-invocation): `alert.call(undefined, 'Hello World!')`
> :point_right: Each invocation type defines the context in its own way.


#### FUNCTION INVOCATION
*a.k.a. 'a normal function call'*
```js
function foo() {
  console.log(this === window); // => true
  this.myNumber = 20; // add 'myNumber' property to global object
};

foo();
window.myNumber; // => 20
```
- Here, `this` refers to the *global object* (i.e. `window` object in a browser) - same as if `this` was used by itself.
- ...but only if it's not strict mode; in strict mode, `this` is `undefined` instead:

```js
"use strict";
function foo() {
  console.log(this === window); // => false
  console.log(this === undefined); // => true
};

foo();
```
- this is because in non-strict mode, the 'owner' of the function (i.e. global context or `window`) is the default binding for `this`, whereas in strict mode, default bindings are not allowed.


#### METHOD INVOCATION
Refers to functions stored as the property of an object, and therefore called as methods.
- in this case, `this` refers to the object that owns the method, and is usually used to reference its properties
- see [JS Class Syntax](/Javascript-Syntax.md#js-class-syntax) for an example - although the same possibilities apply to object literals:

```js
const calc = {
  num: 0,
  increment() {
    console.log(this === calc); // => true
    this.num += 1;
    return this.num;
  }
};

// method invocation. this is calc
calc.increment(); // => 1
calc.increment(); // => 2
```

##### :warning: Complication 1: nested functions of different invocation types:
If you have a function nested within a function, the inner function's context *only depends on its own invocation type*, not on the outer function's context.

```js
const numbers = {
  numberA: 5,
  numberB: 10,

  sum: function() {
    console.log(this === numbers); // => true

    function calculate() {
      // this is window or undefined in strict mode
      console.log(this === numbers); // => false
      return this.numberA + this.numberB;
    }

    return calculate();
  }
};

numbers.sum(); // => NaN or throws TypeError in strict mode
```
To solve this, you can either:
- modify the inner function’s context with [indirect invocation](#indirect-invocation)
- create a [bound function](#bound-function)
- rewrite the inner function as an [arrow function](#arrow-function)

##### :warning: Complication 2: separating a method from its object:
Methods can be extracted from the object and assigned to a variable, e.g. `const alone = myObj.myMethod;` - **in this case calling `alone()` consitutes a function invocation**, so `this` will be either the global object `window` or `undefined`, rather than the object that the method was originally defined on.

The same is true when a method is passed by reference as an argument to another function, e.g. `setTimeout(myObj.myMethod, 1000);`

- Workaround: a [bound function](#bound-function) `const alone = myObj.myMethod.bind(myObj)` fixes the context by binding `this` to the object that owns the method. Alternatively, defining `myMethod` as an [arrow function](#arrow-function) achieves the same result.


#### CONSTRUCTOR INVOCATION
```js
let City = function(name, state) {
    this.name = name || 'Portland';
    this.state = state || 'Oregon';
};

new City('Boulder', 'Colorado');
```
- Constructor functions are essentially the old syntax for object creation, prior to [JS Class Syntax](#js-class-syntax), but constructor invocation applies equally to constructors defined in class syntax!
- Essentially, constructor invocation happens anytime a function call is preceded by the `new` keyword.
- Here, `this` refers to the newly created object that will be instantiated when `new City()` is called.

##### :warning: Complication: not using `new` keyword:
Oddly enough, it is possible to call a constructor without the `new` keyword. For the above example constructor, calling `City('Boulder', 'Colorado');` would not cause an error - but it would result in the `name` and `state` properties being set *on the global object* (i.e. `window` in the browser), rather than on an instance of `City` - so best avoid this usage and always make sure you use `new` with a constructor call.


#### INDIRECT INVOCATION
A function invoked with `.call`, `.apply` 
 
One solution to the nested function problem discussed in the [Method invocation](#method-invocation) section, is to explicitely change the context of the inner function `calculate()` to the desired one by calling `calculate.call(this)` (an indirect invocation of a function):

```js
const numbers = {
  numberA: 5,
  numberB: 10,
  sum: function() {
    console.log(this === numbers); // => true

    function calculate() {
      console.log(this === numbers); // => true
      return this.numberA + this.numberB;
    }

    // use .call() method to modify the context
    return calculate.call(this);
  }
};
numbers.sum(); // => 15
```
 
### Bound function
`.bind`

### Arrow function

Another solution to our nested function issue:

```js
const numbers = {
  numberA: 5,
  numberB: 10,
  sum: function() {
    console.log(this === numbers); // => true

    const calculate = () => {
      console.log(this === numbers); // => true
      return this.numberA + this.numberB;
    }

    return calculate();
  }
};

numbers.sum(); // => 15
```

The arrow function binds `this` lexically, so `this` has the same value as the containing `sum()` method.
