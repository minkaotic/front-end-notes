# ASP.NET MVC & Razor 
## Contents
- [Preamble](#preamble)
    - [MVC pattern recap](#mvc-pattern-recap)
    - [MVC Razor vs. Angular(JS)](#mvc-razor-vs-angularjs)
- [ASP.NET MVC](#aspnet-mvc)
    - [Razor & MVC](#razor--mvc)
    - [Razor syntax](#razor-syntax)
    - [Razor Helpers](#razor-helpers)


## Preamble
ASP.NET is Microsoft's technology for running dynamic web pages on web servers. ASP.NET Razor is a server-side markup language that lets you embed server-based (C#) code into web pages.

### MVC pattern recap
The *Model View Controller* design pattern is commonly used across many frameworks for front end development.

- **Model** = the *data* in your website. The applications data domain is implemented through *model objects*. Model objects often retrieve and store model state in a database. For example, a Product object might retrieve information from a database, operate on it, and then write updated information back to a Products table in a SQL Server database.

- **View** = the components that display the application's *user interface (UI)*. Typically, this UI is created from the model data. (An example would be an edit view of a Products table that displays text boxes, drop-down lists, and check boxes based on the current state of a Product object.)

- **Controller** = the *coordinator* responsible for directing what specific actions need to be performed when a user navigates to our website, in order to send a response to that user. Controllers are the components that handle user interaction, work with the model, and ultimately select a view to render that displays UI. 

In an MVC application, the view only displays information; the controller handles and responds to user input and interaction. For example, the controller handles query-string values, and passes these values to the model, which in turn might use these values to query the database.

![MVC diagram](https://github.com/minkaotic/front-end-notes/blob/master/img/mvc.png)
*Source: [this article](https://medium.freecodecamp.org/model-view-controller-mvc-explained-through-ordering-drinks-at-the-bar-efcba6255053)*

The MVC pattern helps create applications that separate the different aspects of the application: input logic (controller), business logic (model), and UI logic (view), while providing a loose coupling between these elements. 


**Sources:**
- https://docs.microsoft.com/en-us/previous-versions/aspnet/dd381412(v=vs.108)
- https://teamtreehouse.com/library/the-anatomy-of-an-mvc-project
- Also see [this great analogy comparing MVC to a bar](https://medium.freecodecamp.org/model-view-controller-mvc-explained-through-ordering-drinks-at-the-bar-efcba6255053)


### MVC Razor vs. Angular(JS)
Razor renders the HTML on the server, whereas Angular(JS) renders it on the client.
There's a whole debate about which of these are better, and modern web development is split into two camps:

***Camp 1*** uses server-side technologies for its controllers and views and has JavaScript in its views for dynamic things.
- MVC and Razor are the ASP.NET server-side technologies used for this.
- Other server-side technologies for this approach include: Express (Javascript), Django (Python) and Rails (Ruby)
- Client-side technologies may include things like jQuery or Dojo.

***Camp 2*** uses server-side technologies to expose REST endpoints. Client-side technologies are used to provide controllers and views.
- WebAPI is the ASP.NET server-side technology used for this.
- Client-side technologies may include things like AngularJS or React.

One consideration for deciding between these two is that for applications with a large amount of dynamic elements, you don't want to have to call back to the server every time you want to render some new HTML. Also, any functionality that requires an interactive UI without page refreshes (i.e. a list to which you add items without a page reload, or a form where the fields defined are dependent on each other) would be best served by a client side framework.


## ASP.NET MVC

### Razor & MVC
Razor is a markup syntax that lets you embed server-based code (Visual Basic and C#) into web pages. It can be seen as an evolution of the old “.aspx” style markup.

ASP.NET MVC has implemented a view engine that allows us to use Razor inside of an MVC application to produce HTML. 

Razor can either be used as part of a classic MVC-structured application, or as part of an *MVVM (Model-View-ViewModel)* setup, whereby the model and controller code is also included within the Razor Page itself. For more on the differences between these, see: https://stackify.com/asp-net-razor-pages-vs-mvc/.

### Razor syntax
#### Basics
1. Add code to a page using the `@` character: it starts inline expressions, single statement blocks, and multi-statement blocks
1. Single or multi statement code blocks are enclosed in braces, each statement ending on a semicolon
1. Expressions don't require braces or semicolons
1. Variables can be used to store values
1. Files have the extension `.cshtml`

```
<!-- Single statement blocks  -->
@{ var total = 7; }
@{ var myMessage = "Hello World"; }

<!-- Inline expressions -->
<p>The value of your account is: @total </p>
<p>The value of myMessage is: @myMessage</p>

<!-- Multi-statement block -->
@{
    var greeting = "Welcome to our site!";
    var weekDay = DateTime.Now.DayOfWeek;
    var greetingMessage = greeting + " Today is: " + weekDay;
}
<p>The greeting is: @greetingMessage</p>
```

#### The Request object
You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page (see [example in the next section](#reading-user-input)), what type of browser made the request, the URL of the page, the user identity, etc. 

The following example shows how to access properties of the `Request` object and how to call the `MapPath()` method of the Request object, which gives you the absolute path of the page on the server:

```
<table border="1">
<tr>
    <td>Requested URL</td>
    <td>Relative Path</td>
    <td>Full Path</td>
    <td>HTTP Request Type</td>
</tr>
<tr>
    <td>@Request.Url</td>
    <td>@Request.FilePath</td>
    <td>@Request.MapPath(Request.FilePath)</td>
    <td>@Request.RequestType</td>
</tr>
</table>
```

The result displayed in a browser:

![Request object props](https://github.com/minkaotic/front-end-notes/blob/master/img/request-object-properties.PNG)


#### Reading user input
An important feature of dynamic web pages is that you can read user input. In Razor, input is read via `Request["input-name"]`, and posting input is tested by the `IsPost` condition:

```
@{
    var totalMessage = "";
    if (IsPost)
    {
        var num1 = Request["text1"];
        var num2 = Request["text2"];
        var total = num1.AsInt() + num2.AsInt();
        totalMessage = "Total = " + total;
    }
}
<form action="" method="post">
    <p>
        <label for="text1">First Number:</label><br>
        <input type="text" name="text1" />
    </p>
    <p>
        <label for="text2">Second Number:</label><br>
        <input type="text" name="text2" />
    </p>
    <p><input type="submit" value=" Add " /></p>
</form>
<p>@totalMessage</p>
```

### Razor Helpers
ASP.NET helpers are components that can be accessed by single lines of Razor code. You can build your own helpers using Razor syntax, or use built-in ASP.NET helpers.

Some useful built-in Razor helpers include:

- Web Grid
- Web Graphics
- Google Analytics
- Facebook Integration
- Twitter Integration
- Sending Email
- Validation


**Sources:**
- https://docs.microsoft.com/en-us/aspnet/web-pages/overview/getting-started/introducing-razor-syntax-c
- https://www.w3schools.com/asp/razor_intro.asp
