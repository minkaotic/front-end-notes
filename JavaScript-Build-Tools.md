# JavaScript Build Tools

### Contents
- [Overview](#overview)
- [NPM Basics](#npm-basics)
- [Webpack](#webpack)

-------------

## Overview
When starting a new JavaScript project, one of the first things to do is set up a **build system** to help manage everything needed to build and run the application (incl. tests). Build systems have traditionally included:

> :gift: [Package managers](#package-managers), :books: [Module bundlers](#module-bundlers), :scroll: [Compilers](#compilers) and :ant: [Task runners](#task-runners).

*However!* As both [NPM and Webpack have advanced (see below)](#webpack), there is an increasing trend to use just those two tools and skip using a dedicated task runner such as Gulp.


### Package managers
Package managers install and keep track of all the dependencies of a project, and simplify the process of upgrading, configuring and removing dependencies.
- [NPM](https://www.npmjs.com/) (node package manager) - the most popular JavaScript package manager
- [Yarn](https://yarnpkg.com/en/) - another popular choice; created by Facebook


### Module bundlers
JavaScript source code is usually split between a number of files or modules. Module bundlers combine all of your source code (and all of its dependencies) into a single, [minified](https://en.wikipedia.org/wiki/Minification_(programming)) JavaScript file before it's served to the browser.

This way, rather than linking loads of .js files in your template, you only need to add the bundle(s), e.g.: `<script src="./dist/bundle.js""></script>` - reducing web calls and speeding up loading times.

Popular bundlers:
- [Webpack](https://webpack.js.org/)
- [Rollup](https://rollupjs.org/guide/en/)
- [Browserify](http://browserify.org/)
- [Parcel](https://parceljs.org/) - a new open source JavaScript module bundler; recently launched


### Compilers
Javascript runtime environments (like the browser) only understand standard JavaScript. Modern, complex JavaScript applications often require more than pure JavaScript. To support any of the following, you need to transform to standard JavaScript using a compiler:

- Using new, cutting-edge JavaScript features that are not yet supported by all browsers
- Using a library or framework
- Using different "flavors" of JavaScript, such as [TypeScript](https://www.typescriptlang.org/) or [CoffeeScript](http://coffeescript.org/)

Popular compilers:
- Typescript has a built-in compiler that converts a TypeScript file to plain JavaScript.
- [Babel](https://babeljs.io/) is the most popular JavaScript compiler, and the most reliable way to use features from ES2015 and beyond while supporting older browsers


### Task runners
Task runners define and run common tasks in your project, for example:

- Minifying your JavaScript so it can be loaded quickly and efficiently into the browser
- Linting to ensure consistent coding style free of errors
- Running tests on your code
- Compiling source code from one type of syntax to another (both JS-wise and SASS to CSS)
- Starting up a development server on your computer to run your app
- Automatically reloading the browser whenever a JavaScript/SASS file is saved

Popular task runners:
- [Gulp](https://gulpjs.com/) is a common task runner
- [NPM](https://www.npmjs.com/) can also run automated tasks and is now the preferred task runner of many developers


:bulb: **JavaScript tools change all the time! Check the [State of JS Tools](https://2019.stateofjs.com/other-tools/) for a current overview.**


-------------

## NPM Basics
[NPM](https://www.npmjs.com/) offers both a public registry and a CLI to manage software packages (modules) for JavaScript. It is also often used as a task runner to automate common steps forming part of the build chain.
In the CLI, get an overview of options with `npm`, or use the help flag for more details on each command, e.g. `npm install -h`.

### Installing packages
- Installing a package locally (only to a given project): `npm install [package_name]`
- Installing a package *globally*, i.e. general command line utilities and the such like: `npm install [package_name] -g`
- To upgrade NPM itself, run: `npm install npm@latest -g`

### Managing dependencies
1. `npm init`

-------------

## Webpack

### The rise of `Webpack + NPM`
[Webpack](https://webpack.js.org/)'s main features are **bundling** and **modularisation**. However, Webpack is such a powerful tool that it can already perform the vast majority of the tasks previously done through a task runner:
- Provides options for minification and sourcemaps for your bundle
- Can be run as middleware through a custom server called `webpack-dev-server`, which supports both live reloading and hot reloading
- By using loaders, you can also add ES6 to ES5 transpilation, and CSS pre- and post-processors

This significantly cuts down on tasks that would have previously been handled by a dedicated [task runner](#task-runners) such as Gulp, leaving only unit tests & linting as major tasks that Webpack can’t handle independently - and for these, many devs opt to just use NPM scripts directly.


### Webpack basics

..also link to ES modules as one way of handling modularisation


Sources:
- https://medium.com/ag-grid/webpack-tutorial-understanding-how-it-works-f73dfa164f01
- https://www.toptal.com/front-end/webpack-browserify-gulp-which-is-better
