# Angular Notes

## Contents
- [Overview](#overview) 
  - [History](#history)
  - [AJAX & Angular](#ajax--angular)
  - [Angular vs AngularJS](#angular-vs-angularjs)
- [AngularJS](#angularjs)
  - [Templates, Directives, Controllers, Scope](#templates-directives-controllers-scope)
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
###  Templates, Directives, Controllers, Scope

- ***Templates*** (or *views*) hold most of the HTML, and are what structure our application

- ***Directives*** extend our HTML templages with tags and attributes
  - AngularJS has built-in directives to do anything from evaluating user interactions to easily manipulating data
  - Additionally, we can create our own reusable, custom directives
  
- ***Controllers*** contain the logic that tells our application how to behave, e.g.:
  - What data to display on button click
  - What elements to diplay
  
- ***Scope*** (maybe the hardest part of Angular to understand) is the part of the application that allows you to manipulate data and make changes to the user interface. Every controller, directive and view can have its own scope.

  ![Angular concepts](https://github.com/minkaotic/front-end-notes/blob/master/img/angular-concepts.png)

A controller and directive can also share scope - as in, a place where they can access the same data and variables.

  ![Angular shared scope](https://github.com/minkaotic/front-end-notes/blob/master/img/angular-shared-scope.png)

#### How does Angular work?
Instead of manipulating the DOM “directly,” you annotate your DOM with metadata (directives), and Angular manipulates the DOM for you.


## Sources
- https://www.simplilearn.com/angularjs-vs-angular-2-vs-angular-4-differences-article
- https://www.ng-newsletter.com/posts/beginner2expert-how_to_start.html
- https://teamtreehouse.com/library/angularjs-basics-1x-2

