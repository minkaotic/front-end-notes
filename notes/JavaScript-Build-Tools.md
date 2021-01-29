# JavaScript Build Tools
**Contents: [Overview](#overview) |  [NPM Basics](#npm-basics) | [Webpack](#webpack)**


-------------

## Overview
When starting a new JavaScript project, one of the first things to do is set up a **build system** to help manage everything needed to build and run the application (incl. tests). Build systems have traditionally included:

> :gift: [Package managers](#package-managers), :books: [Module bundlers](#module-bundlers), :scroll: [Compilers](#compilers) and :ant: [Task runners](#task-runners).

*However!* As both [NPM and Webpack have advanced (see below)](#the-rise-of-webpack--npm), there is an increasing trend to use just those two tools and skip using a dedicated task runner such as Gulp.


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

### Managing dependencies
1. [`npm init`](https://docs.npmjs.com/cli/init) - creates a `package.json` file based on metadata you enter about the current project / repo, allowing you to start tracking the project's dependencies. (Commit this file.)
1. Once your project is thus initialised, `npm install [package_name] --save` - installs a package and saves it as a dependency in the `package.json` file
1. Henceforth, `npm install` will look for the `package.json` file and install all its dependencies

### Dependencies vs. devDependencies
*Dependencies* are modules which are required at runtime / in production
  - e.g. React, Redux, Express, Axios, etc...
  - Install using `npm install --save` (shorthand `npm i -S`)
 
*DevDependencies* are modules which are only required during development
  - e.g. Nodemon, Babel, ESLint, and testing frameworks like Chai, Mocha, Enzyme, etc...
  - To install & save a dependency as a devDependency, use `npm install --save-dev` (shorthand `npm i -D`)

### Installing & uninstalling packages
- `npm install [package_name]` will install a packate *locally* (only for the current project) without saving it as a dependency to be checked in
- `npm install [package_name] -g` will install a package *globally*, i.e. general command line utilities and the such like
  - e.g. to upgrade NPM itself, run: `npm install npm@latest -g`
- `npm install` will install packages listed in `package.json` for a *development* setup (including devDependencies)
- `NODE_ENV=production npm install` will install packages for a *production* setup (ignoring devDependencies), by setting the `NODE_ENV` environment variable (defaults to `development`)

Uninstalling:
- `npm uninstall [package_name]` will uninstall a package, but not remove it from the `package.json` file
- `npm uninstall [package_name] --save` or `--save-dev` will remove it as a dependency
- `npm uninstall [package_name] -g` to uninstall a global package

### Versions & updates
#### Version rules
To instruct NPM to install the latest minor release until the next major version is released, use the `^` character in front of the version number in `package.json`:
```json
{
  "name": "my_nice_app",
  "version": "0.0.1",
  "description": "Celsus is a product data store",
  "main": "",
  "dependencies": {
    "aspnet-prerendering": "^3.0.1",
    "jquery": "^3.4.1",
    ...
  }
}
```
To install the latest *patch* releases until the next minor release, use the `~` character instead.

If a specific version is indicated without `~` or `^`, only that version will ever be used regardless of available updates.

#### Updating
Run `npm outdated` to see a list of outdated packages (`npm outdated -g` for global packages).

Run **`npm update`** to update all packages to the latest allowed version *based on the version rules* set in `package.json`.

> NB: if there was no `package.json` file when running the `npm update` command, it would upgrade all packages in the node modules folder to the latest version.

To update specific packages:
- `npm update [package_name]` for local (project specific) dependencies
- `npm update [package_name] -g` for global packages

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
