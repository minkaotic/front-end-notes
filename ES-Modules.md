## ES Modules

EcmaScript modules (ESM) bring an official, standardized module system to JavaScript, allowing programmers to write independent units of code that other programmers can explicitly include (or mark as “required”) in their Javascript code.


### What problems do Modules solve?
All revolves around how variables are managed in ES:

- JavaScript has **scope**, which means that variables defined in a given function can't be accessed by another function.

- Whilst this is mostly desirable, *one downside is that it makes sharing variables between different functions hard*.

- Prior to modules, a common workaround was to put variables that need sharing on the *global scope* (or another scope above the current scope). Downsides of *that* are:
  - All your script tags need to be in the right order. Inadvertent changes to the order that mean a given variable isn't there, will cause the app to throw an error and stop running.
  - Maintenance is tricky, as you don't know which scripts depend on another script having put a variable in the global scope first.
  - Malicious code can manipulate variables in the global scope to make your code do something evil, or non-malicious code could just accidentally clobber your variable.


### How do Modules help?
Modules make it possible to group the variables and functions that are related to one another, and make them available in a module scope. This can be used to share variables between the functions in the module -

- But unlike function scopes, module scopes can make their variables available to *other modules* as well. 
- This is done through explicitely exporting the variables, classes or functions from the module that should be available to others.
- Other modules can explicitely state that they depend on an exported variable, class or function.

![JS scope with and without modules](https://github.com/minkaotic/front-end-notes/blob/master/img/js-scope.PNG)
*Source: [Lin Clark - ES Modules: A Cartoon Deep Dive](https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/)*

As an additional benefit on top of avoiding the problems above, the the ability to export and import variables between modules also makes it a lot easier to (re)organise code into small chunks that can work independently of each other, and can be combined and re-combined.


## How ES Modules work
Modules build up a graph of dependencies, which starts from a specified entry point. From there, the dependencies are pulled in via `import` statements.

The browser uses these `import` statements to find the rest of the code needed to run. As the browser can't work with the files themselves, it parses all of code in these files to turn them into data structures called **module records**. From there, it turns the module record into a **module instance**, which combines *the code* and *the state*.


## How to use Modules

Add the `type=module` attribute to the script element:
```
<script type="module">
  import {addTextToBody} from './utils.mjs';

  addTextToBody('Modules are pretty cool.');
</script>
```


**Sources:**
- https://hacks.mozilla.org/2018/03/es-modules-a-cartoon-deep-dive/
- https://jakearchibald.com/2017/es-modules-in-browsers/
