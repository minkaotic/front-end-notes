## ES Modules

EcmaScript modules (ESM) bring an official, standardized module system to JavaScript, allowing programmers to write independent units of code that other programmers can explicitly include (or mark as “required”) in their Javascript code.

### Contents
- [What problems do Modules solve?](#what-problems-do-modules-solve)
- [How do Modules help?](#how-do-modules-help?)
- [How ES Modules work](#how-es-modules-work)
- [How to use Modules](#how-to-use-modules)
- [History of Modules in JavaScript](#history-of-modules-in-javascript)

## What problems do Modules solve?
All revolves around how variables are managed in ES:

- JavaScript has **scope**, which means that variables defined in a given function can't be accessed by another function.

- Whilst this is mostly desirable, *one downside is that it makes sharing variables between different functions hard*.

- Prior to modules, a common workaround was to put variables that need sharing on the *global scope* (or another scope above the current scope). Downsides of *that* are:
  - All your script tags need to be in the right order. Inadvertent changes to the order that mean a given variable isn't there, will cause the app to throw an error and stop running.
  - Maintenance is tricky, as you don't know which scripts depend on another script having put a variable in the global scope first.
  - Malicious code can manipulate variables in the global scope to make your code do something evil, or non-malicious code could just accidentally clobber your variable.


## How do Modules help?
Modules make it possible to group the variables and functions that are related to one another, and make them available in a module scope. This can be used to share variables between the functions in the module -

- But unlike function scopes, module scopes can make their variables available to *other modules* as well. 
- This is done through explicitely exporting the variables, classes or functions from the module that should be available to others.
- Other modules can explicitely state that they depend on an exported variable, class or function.

![JS scope with and without modules](https://github.com/minkaotic/front-end-notes/blob/master/img/js-scope.PNG)
*Source: [Lin Clark - ES Modules: A Cartoon Deep Dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)*

As an additional benefit on top of avoiding the problems above, the the ability to export and import variables between modules also makes it a lot easier to (re)organise code into small chunks that can work independently of each other, and can be combined and re-combined.


## How ES Modules work
Modules build up a graph of dependencies, which starts from a specified entry point. From there, the dependencies are pulled in via `import` statements.

The browser (or a transpiler like Webpack!) uses these `import` statements to find the rest of the code needed to run.


## How to use Modules
ES6 modules are stored in files. There is exactly one module per file and one file per module.

### Basic imports & exports
To **export** a variable in the file **lib.js**:
```javascript
export const myVariable = 'some important text';
export function square(x) {
  return x * x;
}
```

To **import variables**:
```javascript
import {myVariable, square} from 'lib';
```

To **import the whole module**:
```javascript
import * as lib from 'lib';
```

Import if file is in a different directory:
```javascript
import * as lib from '../stuff/lib';
```

### Default exports
There can be a single *default export* in a module.

For example, in file **lib.js**:
```javascript
export default function () { ··· } // no semicolon!
```
Import & usage:
```javascript
import myFunc from 'lib';
myFunc();
```

Another example, this time using a class - in **lib.js**:
```javascript
export default class { ··· } // no semicolon!
```
Import & usage:
```javascript
import MyClass from 'MyClass';
const inst = new MyClass();
```

***NB:*** There is no semicolon at the end if you default-export a function or a class (which are anonymous declarations)!

### Use of modules in browsers
Note that the use & syntax of modules in browsers is a bit different, see "[ECMAScript modules in browsers](https://jakearchibald.com/2017/es-modules-in-browsers/)" for more details on that.


## History of Modules in JavaScript

https://flaviocopes.com/es-modules/
https://nodejs.org/api/esm.html#esm_notable_differences_between_import_and_require
https://stackoverflow.com/questions/16521471/relation-between-commonjs-amd-and-requirejs


**Sources:**
- https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/
- http://exploringjs.com/es6/ch_modules.html
