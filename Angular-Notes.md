# Angular(JS) Notes

## Contents
- [Overview](#overview) 
  - [History](#history)
  - [Angular vs AngularJS](#angular-vs-angularjs)
  - [Data Binding](#data-binding)
- [AngularJS](#angularjs)
  - [Core Concepts](#core-concepts)
  - [Getting Started](#getting-started)
  - [Useful Directives](#useful-directives)
  - [Tools for Debugging AngularJS](#tools-for-debugging-angularjs)
  - [AngularJS Components](#angularjs-components)
- [Sources](#sources)
_______________

# Overview
Angular is a [client side application framework](https://github.com/minkaotic/front-end-notes/blob/master/Frameworks-Overview.md#server-side-vs-client-side-rendering) built entirely with static files. 

The architecture of Angular(JS) is based on [model-view-controller (MVC)](https://github.com/minkaotic/front-end-notes/blob/master/Frameworks-Overview.md#mvc-pattern-recap) design. Angular(JS) lends itself particularly well to building **Single Page Applications (SPAs)**, but can also be used to build 'traditional' multi-page applications.

> **Instead of manipulating the DOM “directly,” you annotate your DOM with metadata (directives), and Angular manipulates the DOM for you.**

## History
Google developed AngularJS in 2009 and version 1.0 was released in 2012. Angular has since dominated the world of open-source JavaScript frameworks, with enthusiastic support and widespread adoption among both enterprises and individuals. As a result, Angular has evolved from the AngularJS version 1.0 to Angular version 2.0, Angular 4.0 and now the latest Angular version 6.0, all in just a few years.

## Angular vs AngularJS
**AngularJS** is an open-source, JavaScript-based framework for dynamic web app development. It utilizes HTML as a template language. By extending HTML attributes with directives and binding data to HTML with expressions, AngularJS creates an environment that is readable, extraordinarily expressive and quick to develop. 

**Angular** is the blanket term used to refer to Angular 2, Angular 4 and all other versions that come after AngularJS. Both Angular 2 and 4 are open-source, TypeScript-based front-end web application platforms. 

Some key differences include:
- Whilst AngularJS is written in *JavaScript*, Angular uses Microsoft’s *TypeScript* language, which is a superset of ECMAScript 6 (ES6). This has the combined advantages of the TypeScript features, like type declarations, and the benefits of ES6, like iterators and lambdas.

- Unlike Angular, AngularJS was not built with mobile support in mind.

- The later versions, Angular 2 and Angular 4, have been upgraded to provide an overall improvement in performance, especially in page load speed and dependency injection. 

For more differences, see [this infographic from simplilearn.com](https://www.simplilearn.com/ice9/free_resources_article_thumb/angularjs-angular2-angular4-understanding-the-differences.jpg).

## Data Binding
One of the most powerful features of Angular is called “data binding.” At a high level, data binding is how an application mixes together it’s data and its logic to create what the user sees.

In most frameworks data binding takes place once, and then it is up to the developer to write code that keeps all data in sync with the user’s interactions. *=> This is called **one-way data binding**, and can be tedious if you have a lot of data and a lot of user interactions to manage.*

In Angular, when data is bound to the scope, this data is kept in sync with the application's underlying data store with little help from the developer. This means that anytime a user interacts with the app, Angular updates the data in the scope of your application. *=> This is called **two-way data binding.***

The [`ng-model`](#adding-data-to-your-app-using-ng-model) directive is a great example of how this works.


# AngularJS
## Core Concepts

- ***Templates*** (or *views*) hold most of the HTML, and are what structures our application

- ***Directives*** extend our HTML templates. Directives are either tags, or and attributes of tags
  - AngularJS has built-in directives to do anything from evaluating user interactions to easily manipulating data
  - Additionally, we can create our own reusable, custom directives
  
- ***Controllers*** are they glue of our application - they contain the logic that tells the application how to behave; specifically, they:
  - Handle data
  - Make changes to the UI (i.e. what data to display on button click)
  - Control the state of the application (for example in an app with functionality to edit and update text: whether or not an item is currently in edit mode)
  
- ***Scope*** is the part of the application that allows you to manipulate data and make changes to the user interface. Every controller, directive and view can have its own scope.

  ![Angular concepts](https://github.com/minkaotic/front-end-notes/blob/master/img/angular-concepts.png)

- A controller and directive can also share scope - as in, a place where they can access the same data and variables.

  ![Angular shared scope](https://github.com/minkaotic/front-end-notes/blob/master/img/angular-shared-scope.png)

- Each controller's scope inherits from the `$rootScope`, of which there is one per application. It is best practice to not use `$rootScope` directly, as any variables created here are available anywhere in the application (defying the idea of sensible scoping).
- Controllers can be nested within one another in the template, in which case the child controller's scope will inherit the functions and values of the parent controller's scope. In other words, anything on the parent controller's scope will be accessible to both the parent and the child controller.
- Any functions and values inherited from a parent scope can be overwritten within the context of the child scope.
- For a recap on scope, see [this video](https://teamtreehouse.com/library/understanding-scope-in-angular)


## Getting Started
- [Hooking up an AngularJS app](#hooking-up-an-angularjs-app)
- [Adding a simple directive](#adding-a-simple-directive)
- [Creating & using a controller](#creating--using-a-controller)

### Hooking up an AngularJS app
#### in the HTML...
- In order to include AngularJS in your app, either:
  - download the files from the [AngularJS website](https://angularjs.org/) and include them in your project
  - or include a script tag with a link to the Angular file’s CDN version: `<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.5/angular.min.js"></script>`
- Bootstrap AngularJS into the HTML using the `ng-app` directive and the application name:

  ```html
  <!doctype html>
  <html lang="en">
    <head>
      <title>...</title>
    </head>
    <body ng-app="todoListApp">
      <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.5/angular.min.js"></script>
      <script src="scripts/app.js" type="text/javascript"></script>
    </body>
  </html>
  ```

#### in the JavaScript file...
- Create the application with Angular's `module()` method, providing the name of the application (matching the name used in the `ng-app` directive), and an array of its dependencies (in this case, none):
  ```javascript
  angular.module("todoListApp", []);
  ```

### Adding a simple directive
In a new JS file, create the custom directive using the `module()`'s `directive()` method (*NB!* the single parameter version of the `module()` method used here will make this directive refer back to the existing `todoListApp`, rather than creating a new one!):
```javascript
angular.module('todoListApp')
.directive('helloWorld', () => {
  return {
    template: "This is the hello world directive!"
  }
});
```
- `directive()` takes two parameters: the directive name, and a callback function that returns an object to be used in the directive - in the example above, it provides a `template` (typically a small snippet of HTML).

Then add this directive into the HTML file as a tag - note the change from camel case to all lower case with hyphens for the directive name:
```html
<body ng-app="todoListApp">
  <hello-world></hello-world>
  ...
</body>
```
Alternatively, directives can also be invoked via attributes of an existing tag:
```html
<body ng-app="todoListApp">
  <div hello-world></div>
  ...
</body>
```

Both of these will make "*This is the hello world directive!*" appear in the view (on the page)!

### Creating & using a controller
Use the `controller()` method of the module (back in the JS file where the app is created):
```javascript
angular.module('todoListApp', [])
.controller('mainCtrl', function($scope) {
  $scope.helloWorld = () => {
    console.log('Hello there! This is the helloWorld controller function in the mainCtrl!');
  };
});
```
- `controller()` takes two parameters: the controller name, and a callback function that in turn takes the `$scope` variable as a parameter.
- By convention, controller names end in `Ctrl`.
- `$scope` defines an area of operation for your controller: this controller's functions will only work in the parts of the application you allow them to.
- In order to define a function that can be used to alter the application, we attach it to the `$scope` object - `$scope.helloWorld = () => {...}`.

**In order to use this controller in our application, we have to inject it into the template**, effectively telling Angular "this is where I want my controller to be used". This is done with the built-in `ng-controller` directive, which has to be set to the name of the controller defined in the JavaScript file:
```html
<body ng-app="todoListApp">
  <div ng-controller="mainCtrl">
    <a href="" ng-click="helloWorld()">Log Hello World!</a>
  </div>
</body>
```

- Now `mainCtrl`'s scope is within the `div`.
- This means the controller's functions can be used within it - in this case, by associating its function with the `ng-click` directive (`ng-click="helloWorld()"`) - so when the user clicks this link, the `helloWorld()` function runs.
- NB: Using `ng-click="helloWorld()"` anywhere in the template that is outside the controller's scope, won't have any effect.


## Useful Directives
AngularJS has many time-saving directives built in!

- [Adding data to an app using `ng-model`](#adding-data-to-an-app-using-ng-model)
- [`ng-click`](#ng-click)
- [`ng-show` and `ng-hide`](#ng-show-and-ng-hide)
- [By comparison: `ng-if`](#by-comparison-ng-if)

### Adding data to an app using `ng-model`
The [`ng-model`](https://docs.angularjs.org/api/ng/directive/ngModel) directive binds an `input`, `select`, `textarea` (or custom form control) to a property on the application's scope, for example:

```html
<div ng-controller="mainCtrl">
  <h1>My TODOs</h1>
  <input ng-model="todo.completed" type="checkbox"/>
  <input ng-model="todo.name" type="text"/>
</div>
```
- Using the `ng-model` directive binds the value in either input to the respective properties of an object called `todo` in the `$scope` of `mainCtrl`.
- Thanks to Angular's [two-way data binding](#data-binding), anytime a user changes the input the variable in the scope updates too.

Then we can reference the value of either variable in our template, using the [AngularJS expression](https://docs.angularjs.org/guide/expression) in interpolation syntax ("mustache syntax"). For example, to use `todo.name` as the label text:

```html
<div ng-controller="mainCtrl">
  <h1>My TODOs</h1>
  <input ng-model="todo.completed" type="checkbox"/>
  <label>{{ todo.name }}</label>
  <input ng-model="todo.name" type="text"/>
</div>
```

#### It can do more!
As well as binding the view into the model for form elements, the `ng-model` directive is also responsible for:
- Providing validation behavior (i.e. required, number, email, url).
- Keeping the state of the control (`valid`/`invalid`, `dirty`/`pristine`, `touched`/`untouched`, validation errors).
- Setting [CSS classes related to these states](https://docs.angularjs.org/api/ng/directive/ngModel#css-classes) on the element to allow state-based styling.


### `ng-click`
The [`ng-click`](https://docs.angularjs.org/api/ng/directive/ngClick) directive allows you to specify custom behavior when an element is clicked. It's a really common directive that greatly simplifies the amount of code needed to create click interactions for the user.

##### Example 1 - incrementing counter
```html
<button ng-click="count = count + 1" ng-init="count=0">
  Increment
</button>
<span>
  count: {{count}}
</span>
```

##### Example 2 - toggling edit mode on and off
i.e. to switch the application state from “editing” to “not editing.”
```html
<a href="" ng-click="editing = !editing">Edit</a>
```

### `ng-show` and `ng-hide`
The [`ng-show`](https://docs.angularjs.org/api/ng/directive/ngShow) and [`ng-hide`](https://docs.angularjs.org/api/ng/directive/ngHide) directive show or hide the given HTML element based on the expression provided.

> :bulb: This is implemented by the directives adding (or removing) the `.ng-hide` class to the element, which will style the element with `display: none !important`.

##### Example - switching element visibility depending on edit mode
Here both directives are used to build fluid toggling of label vs. input view of or to do list item depending on whether edit mode is on in our app - see this example in action in [CodePen](https://codepen.io/minkaotic/pen/WqJzQO)!:

```html
<div ng-controller="mainCtrl" class="list">
  <h1>My TODOs</h1>
  <input ng-model="todo.completed" type="checkbox"/>
  <label ng-hide="editing">{{ todo.name }}</label>
  <input ng-show="editing" ng-model="todo.name" type="text"/>
  <div class="actions">
    <a href="" ng-click="editing = !editing">Edit</a>
  </div>
</div>
```

### By comparison: `ng-if`
https://docs.angularjs.org/api/ng/directive/ngIf
https://www.codelord.net/2015/07/28/angular-performance-ng-show-vs-ng-if/
https://stackoverflow.com/questions/21869283/when-to-favor-ng-if-vs-ng-show-ng-hide



## Tools For Debugging AngularJS
Chrome Tools:
- [AngularJS Batarang](https://chrome.google.com/webstore/detail/angularjs-batarang/ighdmehidhipcmcojjgiloacoafjmpfk?hl=en)
- [ng-inspector for AngularJS](https://chrome.google.com/webstore/detail/ng-inspector-for-angularj/aadgmnobpdmgmigaicncghmmoeflnamj)

Firefox Tools:
- [AngScope](https://github.com/kosprov/AngScope) - this requires installing [Firebug](https://getfirebug.com/) first


## AngularJS Components

In AngularJS, a [Component](https://docs.angularjs.org/guide/component) is a special kind of directive that uses a simpler configuration which is suitable for a component-based application structure.

Advantages of Components:
- simpler configuration than plain directives
- promote sane defaults and best practices
- optimized for component-based architecture
- writing component directives will make it easier to upgrade to Angular

### Creating and configuring a Component
Components can be registered using the `.component()` method of an AngularJS module (returned by `angular.module()`). The method takes two arguments:
- The name of the Component (as string).
- The Component config object. (Note that, unlike the .directive() method, this method does not take a factory function.)

```javascript
const component: ng.IComponentOptions = {
    controller: SomeController,
    template: require("./landingPage.template.html")
};

module.component('landingPage', component);
```

### Component-based Application Architecture
(More on this is covered in the [docs](https://docs.angularjs.org/guide/component#component-based-application-architecture)!)
- **Components only control their own View and Data.** Components should never modify any data or DOM that is out of their own scope.  Component directives use an isolated scope, so a whole class of scope manipulation is not possible.
- **Components have a well-defined public API - Inputs and Outputs.**
- **Components have a well-defined lifecycle.** Each component can implement "lifecycle hooks". These are methods that will be called at certain points in the life of the component. See [docs](https://docs.angularjs.org/guide/component#component-based-application-architecture) for a full list of these.


## Sources
- https://www.simplilearn.com/angularjs-vs-angular-2-vs-angular-4-differences-article
- https://www.ng-newsletter.com/posts/beginner2expert-how_to_start.html
- https://teamtreehouse.com/library/angularjs-basics-1x-2
- https://docs.angularjs.org/guide/component
