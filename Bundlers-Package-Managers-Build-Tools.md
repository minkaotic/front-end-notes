# Bundlers, Package Managers and Build Tools

### Contents
- [Overview](#overview)
- [NPM Basics](#npm-basics)
- [Webpack](#webpack)

-------------

## Overview
When starting a new JavaScript project, one of the first things to do is set up a **build system** to help manage everything needed to build and run the application (incl. tests). Build systems usually include:

> :gift: [Package managers](#package-managers), :books: [Module bundlers](#module-bundlers), :scroll: [Compilers](#compilers) and :ant: [Task runners](#task-runners).


### Package managers
Package managers install and keep track of all the dependencies of a project, and simplify the process of upgrading, configuring and removing dependencies.
- [NPM](https://www.npmjs.com/) (node package manager) - the most popular JavaScript package manager
- [Yarn](https://yarnpkg.com/en/) - another popular choice; created by Facebook

### Module bundlers
JavaScript source code is usually split between a number of files or modules. Module bundlers combine all of your source code (and all of its dependencies) into a single, [minified](https://en.wikipedia.org/wiki/Minification_(programming)) JavaScript file before it's served to the browser.
- [Webpack](https://webpack.js.org/)
- [Rollup](https://rollupjs.org/guide/en/)
- [Browserify](http://browserify.org/)
- [Parcel](https://parceljs.org/) - a new open source JavaScript module bundler; recently launched


### Compilers
### Task runners

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

Webpack's main features are **bundling** and **modularisation**

- rather than linking loads of .js files in template, you only need to add the bundle(s), e.g.: `<script src="./dist/bundle.js""></script>` - reducing web calls and speeding up loading times.


..also link to ES modules as one way of handling modularisation


Sources:
- https://medium.com/ag-grid/webpack-tutorial-understanding-how-it-works-f73dfa164f01
