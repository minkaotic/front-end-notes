# Frameworks Overview

## Contents
- [MVC pattern recap](#mvc-pattern-recap)
- [Server-side vs client-side rendering](#server-side-vs-client-side-rendering)
- [The role of AJAX](#the-role-of-ajax)

## To do
- [ ] Add notes about SPAs
- [ ] Add notes about PWAs
- [ ] Add notes about modern preference for component approach

________________

## MVC pattern recap
The *Model View Controller* design pattern is commonly used across many frameworks for front end development.

- **Model** = the *data* in your website. The application's data domain is implemented through *model objects*. Model objects often retrieve and store model state in a database. For example, a Product object might retrieve information from a database, operate on it, and then write updated information back to a Products table in a SQL Server database.

- **View** = the components that display the application's *user interface (UI)*. Typically, this UI is created from the model data. (An example would be an edit view of a Products table that displays text boxes, drop-down lists, and check boxes based on the current state of a Product object.)

- **Controller** = the *coordinator* responsible for directing what specific actions need to be performed when a user navigates to the website, in order to send a response to that user. Controllers are the components that handle user interaction, select a view to render in the UI and work with the model to decide what data should be sent to the view. 

In an MVC application, the view only displays information; the controller handles and responds to user input and interaction. For example, the controller handles query-string values, and passes these values to the model, which in turn might use these values to query the database.

![MVC diagram](https://github.com/minkaotic/front-end-notes/blob/master/img/mvc.png)
*Source: [this article](https://medium.freecodecamp.org/model-view-controller-mvc-explained-through-ordering-drinks-at-the-bar-efcba6255053)*

The MVC pattern helps create applications that separate the different aspects of the application: input logic (controller), business logic (model), and UI logic (view), while providing a loose coupling between these elements. 

**Sources:**
- https://docs.microsoft.com/en-us/previous-versions/aspnet/dd381412(v=vs.108)
- https://teamtreehouse.com/library/the-anatomy-of-an-mvc-project
- Also see [this great analogy comparing MVC to a bar](https://medium.freecodecamp.org/model-view-controller-mvc-explained-through-ordering-drinks-at-the-bar-efcba6255053)


## Server-side vs client-side rendering
[Razor](https://github.com/minkaotic/front-end-notes/blob/master/MVC-and-Razor.md#razor--mvc) renders the HTML on the server, whereas [Angular(JS)](https://github.com/minkaotic/front-end-notes/blob/master/Angular-Notes.md) renders it on the client.
There's a whole debate about which of these are better, and modern web development is split into two camps:

***Camp 1*** uses server-side technologies for its controllers and views and has JavaScript in its views for dynamic things.
- [MVC and Razor](https://github.com/minkaotic/front-end-notes/blob/master/MVC-and-Razor.md) are the ASP.NET server-side technologies used for this.
- Other server-side technologies for this approach include: Express (Javascript), Django (Python) and Rails (Ruby)
- Client-side technologies may include things like jQuery or Dojo.

***Camp 2*** uses server-side technologies to expose REST endpoints. Client-side technologies are used to provide controllers and views.
- WebAPI is one ASP.NET server-side technology used for this.
- Some examples of client-side JS frameworkds include [Angular](https://angular.io/)/[AngularJS](https://github.com/minkaotic/front-end-notes/blob/master/Angular-Notes.md), [Ember](https://www.emberjs.com/), [Backbone](http://backbonejs.org/), [React](https://reactjs.org/) and [Vue.js](https://github.com/minkaotic/front-end-notes/blob/master/Vue-JS-Notes.md).

### How to choose?
*Client-side rendering* essentially means that the entire application is loaded into the browser that the user is using. There are many performance and user experience benefits to client-side frameworks, as follow-up requests to the server will only be for small amounts of data, rather than more HTML & CSS files as is the case with traditional web pages.

One consideration for deciding between a client- or server-side framework is that for applications with a **large amount of dynamic elements**, you don't want to have to call back to the server every time you want to render some new HTML. Any functionality that requires an **interactive UI without page refreshes** (i.e. a list to which you add items without a page reload, or a form where the fields defined are dependent on each other) would be best served by a client side framework.

On the other hand, server-side rendering more easily achieves important **SEO benefits** - see [this article](https://medium.com/@benjburkholder/javascript-seo-server-side-rendering-vs-client-side-rendering-bc06b8ca2383) for more detail.


## The role of AJAX
- AJAX (Asynchronous JavaScript And XML) is a technology that allows us to get data from a server without the need to refresh a webpage.
  - It does so by using the [XMLHttpRequest](https://developer.mozilla.org/en-US/docs/Web/API/XMLHttpRequest) (XHR) object to communicate with servers.
  - It can send and receive information in various formats, including JSON, XML, HTML, and text files.
  - [More about AJAX](https://developer.mozilla.org/en-US/docs/Web/Guide/AJAX/Getting_Started)

- CLient-side frameworks like Angular extend this idea. Even though the entire application is loaded into the browser when a user requests a URL, in most cases the application will make additional requests for data back to the server via an AJAX call.

- These requests will not re-send the files to the client, but just the pure data - most of the time the response will be in JSON.

- The client-side app can also send data back to the server. This dual capability is known as **"[two-way data binding](https://github.com/minkaotic/front-end-notes/blob/master/Angular-Notes.md#data-binding)"**.

