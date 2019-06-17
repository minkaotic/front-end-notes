# Frameworks Overview

## Contents
- [MVC pattern recap](#mvc-pattern-recap)
- [Server-side vs client-side rendering](#server-side-vs-client-side-rendering)
________________

## MVC pattern recap
The *Model View Controller* design pattern is commonly used across many frameworks for front end development.

- **Model** = the *data* in your website. The applications data domain is implemented through *model objects*. Model objects often retrieve and store model state in a database. For example, a Product object might retrieve information from a database, operate on it, and then write updated information back to a Products table in a SQL Server database.

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
- MVC and Razor are the ASP.NET server-side technologies used for this.
- Other server-side technologies for this approach include: Express (Javascript), Django (Python) and Rails (Ruby)
- Client-side technologies may include things like jQuery or Dojo.

***Camp 2*** uses server-side technologies to expose REST endpoints. Client-side technologies are used to provide controllers and views.
- WebAPI is the ASP.NET server-side technology used for this.
- Client-side technologies may include things like AngularJS or React.

One consideration for deciding between these two is that for applications with a **large amount of dynamic elements**, you don't want to have to call back to the server every time you want to render some new HTML. Any functionality that requires an **interactive UI without page refreshes** (i.e. a list to which you add items without a page reload, or a form where the fields defined are dependent on each other) would be best served by a client side framework.

On the other hand, server-side rendering more easily achieves important **SEO benefits** - see [this article](https://medium.com/@benjburkholder/javascript-seo-server-side-rendering-vs-client-side-rendering-bc06b8ca2383) for more detail.

