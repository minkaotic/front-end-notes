# Angular Notes

## Contents
- [Overview](#overview) 
  - [History](#history)
  - [AJAX & Angular](#ajax--angular)
  - [Angular vs AngularJS](#angular-vs-angularjs)
- [AngularJS](#angularjs)
  - [Core Concepts](#core-concepts)
  - [Getting Started](#getting-started)
  - [Tools for Debugging AngularJS](#tools-for-debugging-angularjs)
- [Sources](#sources)
_______________

## Overview
Angular is a **client side application framework** built entirely with static files. This means that the entire application is loaded into the browser that the user is using. There are many performance and user experience benefits to client side frameworks, as follow-up requests to the server will only be for small amounts of data, rather than more HTML & CSS files as is the case with traditional web pages.

Some other JavaScript client side frameworks include:
- [Ember](https://www.emberjs.com/)
- [Backbone](http://backbonejs.org/)
- [React](https://reactjs.org/)
- [Vue.js](https://vuejs.org/)

The architecture of Angular(JS) is based on model-view-controller (MVC) design. Angular(JS) lends itself particularly well to building **Single Page Applications (SPAs)**, but can also be used to build 'traditional' multi-page applications.

### History
Google developed AngularJS in 2009 and version 1.0 was released in 2012. Angular has since dominated the world of open-source JavaScript frameworks, with enthusiastic support and widespread adoption among both enterprises and individuals. As a result, Angular has evolved from the AngularJS version 1.0 to Angular version 2.0, Angular 4.0 and now the latest Angular version 6.0, all in just a few years.


### AJAX & Angular
- AJAX is a technology that allows us to get data from a server without the need to refresh a webpage.

- Angular extends this idea. Even though the entire application is loaded into the browser when user requests a URL, in most cases the application will make additional requests for data back to the server via an AJAX call.

- These requests will not re-send the files to the client, but just the pure data - most of the time the response will be in JSON.

- The Angular app can also send data back to the server. This dual capability is known as "two-way data binding".


### Angular vs AngularJS
**AngularJS** is an open-source, JavaScript-based framework for dynamic web app development. It utilizes HTML as a template language. By extending HTML attributes with directives and binding data to HTML with expressions, AngularJS creates an environment that is readable, extraordinarily expressive and quick to develop. 

**Angular** is the blanket term used to refer to Angular 2, Angular 4 and all other versions that come after AngularJS. Both Angular 2 and 4 are open-source, TypeScript-based front-end web application platforms. 

Some key differences include:
- Whilst AngularJS is written in *JavaScript*, Angular uses Microsoft’s *TypeScript* language, which is a superset of ECMAScript 6 (ES6). This has the combined advantages of the TypeScript features, like type declarations, and the benefits of ES6, like iterators and lambdas.

- Unlike Angular, AngularJS was not built with mobile support in mind.

- The later versions, Angular 2 and Angular 4, have been upgraded to provide an overall improvement in performance, especially in page load speed and dependency injection. 

For more differences, see [this infographic from simplilearn.com](https://www.simplilearn.com/ice9/free_resources_article_thumb/angularjs-angular2-angular4-understanding-the-differences.jpg).



## AngularJS
###  Core Concepts

- ***Templates*** (or *views*) hold most of the HTML, and are what structure our application

- ***Directives*** extend our HTML templages with tags and attributes
  - AngularJS has built-in directives to do anything from evaluating user interactions to easily manipulating data
  - Additionally, we can create our own reusable, custom directives
  
- ***Controllers*** contain the logic that tells our application how to behave, they allow you to:
  - Handle data
  - Make changes to the UI (i.e. what data to display on button click)
  - Control the state of the application (for example in an app with functionality to edit and update text: whether or not an item is currently in edit mode)
  
- ***Scope*** (maybe the hardest part of Angular to understand) is the part of the application that allows you to manipulate data and make changes to the user interface. Every controller, directive and view can have its own scope.

  ![Angular concepts](https://github.com/minkaotic/front-end-notes/blob/master/img/angular-concepts.png)

A controller and directive can also share scope - as in, a place where they can access the same data and variables.

  ![Angular shared scope](https://github.com/minkaotic/front-end-notes/blob/master/img/angular-shared-scope.png)

#### How does Angular work?
Instead of manipulating the DOM “directly,” you annotate your DOM with metadata (directives), and Angular manipulates the DOM for you.

### Getting Started
#### in the HTML...
- In order to include AngularJS in your app, either:
  - download the files from the [AngularJS website](https://angularjs.org/) and include them in your project
  - or include a script tag with a link to the Angular file’s CDN version: `<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.5/angular.min.js"></script>`
- Bootstrap AngularJS into the HTML using the `ng-app` directive and the application name:

  ```
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
  ```
  angular.module("todoListApp", []);
  ```

#### Adding a simple directive
In a new JS file, create the directive as below (*NB!* the single parameter version of the `module()` method used in this example will make this directive refer back to the existing `exampleApp`, rather than creating a new one!):
```
angular.module('todoListApp')
.directive('helloWorld', function() {
  return {
    template: "This is the hello world directive!"
  }
});
```

Then add this directive into the HTML file as a tag - note the change from camel case to all lower case with hyphens for the directive name:
```
<body ng-app="todoListApp">
  <hello-world></hello-world>
  ...
</body>
```
Alternatively, directives can also be invoked via attributes of an existing tag:
```
<body ng-app="todoListApp">
  <div hello-world></div>
  ...
</body>
```

Both of these will make "*This is the hello world directive!*" appear in the view (on the page)!

#### Creating & using a controller
Use the `controller()` method of the module (back in the JS file where the app is created):
```
angular.module('todoListApp', [])
.controller('mainCtrl', function($scope) {
  $scope.helloWorld = function() {
    console.log('Hello there! This is the helloWorld controller function in the mainCtrl!');
  };
});
```
- `controller()` takes two parameters: the controller name, and an anonymous function that in turn takes the `$scope` variable as a parameter.
- `$scope` defines an area of operation for your controller: this controller's functions will only work in the parts of the application you allow them to.
- In order to define a function that can be used to alter the application, we attach it to the `$scope` object (in other words: `$scope.helloWorld = function() {...}` creates a function that is attached to the `$scope` object).

**In order to use this controller in our application, we have to inject it into the template**, effectively telling Angular "this is where I want my controller to be used". This is done with the built-in `ng-controller` directive, which has to be set to the name of the controller defined in the JavaScript file:
```
<body ng-app="todoListApp">
  <div ng-controller="mainCtrl">
    <a href="" ng-click="helloWorld()">Log Hello World!</a>
  </div>
</body>
```

- Now `mainCtrl`'s scope is within the `div`.
- This means the controller's functions can be used within it - in this case, by associating its function with the `ng-click` directive (`ng-click="helloWorld()"`) - so when the user clicks this link, the `helloWorld()` function runs.


## Tools For Debugging AngularJS
Chrome Tools:
- [AngularJS Batarang](https://chrome.google.com/webstore/detail/angularjs-batarang/ighdmehidhipcmcojjgiloacoafjmpfk?hl=en)
- [ng-inspector for AngularJS](https://chrome.google.com/webstore/detail/ng-inspector-for-angularj/aadgmnobpdmgmigaicncghmmoeflnamj)

Firefox Tools:
- [AngScope](https://github.com/kosprov/AngScope) - this requires installing [Firebug](https://getfirebug.com/) first


## Sources
- https://www.simplilearn.com/angularjs-vs-angular-2-vs-angular-4-differences-article
- https://www.ng-newsletter.com/posts/beginner2expert-how_to_start.html
- https://teamtreehouse.com/library/angularjs-basics-1x-2

