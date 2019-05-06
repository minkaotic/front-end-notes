# ASP.NET MVC
## Contents
- [Preamble](#preamble)
    - [MVC pattern recap](#mvc-pattern-recap)
    - [MVC Razor vs. Angular(JS)](#mvc-razor-vs-angularjs)
- [MVC Basics](#mvc-basics)
    - [Controllers & Default Routing](#controllers--default-routing)
    - [Views](#views)
- [Razor & MVC](#razor--mvc)
    - [Basic Syntax](#basic-syntax)
    - [Layout](#layout)
    - [HTML helper methods](#html-helper-methods)
    - [Functions](#functions)
    - [The Request object](#the-request-object)
    - [HttpContext](#httpcontext)
- [Bundling & Minification](#bundling--minification)
    - [Webpack](#webpack)
    - [ASP.NET bundler](#aspnet-bundler)
- [Tag Helpers](#tag-helpers)
    - [Using Tag Helpers](#using-tag-helpers)
    - [Building your own Tag Helpers](#building-your-own-tag-helpers)
- [Areas in ASP.NET](#areas-in-aspnet)
_________________________

## Preamble
ASP.NET is Microsoft's technology for running dynamic web pages on web servers. ASP.NET Razor is a server-side markup language that lets you embed server-based (C#) code into web pages.

### MVC pattern recap
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

_________________________

## MVC Basics

### Controllers & Default Routing
**Controllers** are classes whose names have to end in `...Controller`, and which inherit from the `System.Web.Mvc.Controller` base class.

Controllers have one or more **action methods**, which typically return one of the MVC *action result types*, which derive from the [ActionResult](https://docs.microsoft.com/en-us/dotnet/api/system.web.mvc.actionresult?view=aspnet-mvc-5.2) class; the return type of action methods is therefore usually `ActionResult`.

> Both controllers and action methods need to be public.

By default, the **routing** created by MVC for pages is `~/controllerName/actionName`, for example:

```c#
public class ComicBookController : Controller
{
    public ActionResult Detail()
    {
        return Content("Hello!");
    }
}
```

- this page (resource) will be associated with the path `~/ComicBook/Detail`.
- `Content()` is a handy `Controller` method that returns a new `ContentResult`, which is one of the derived types of `ActionResult`

The **Homepage** (i.e. start page without additional path) is by default associated with `HomeController` -> `Index()`. (NB: For any other `HomeController` action methods, `Home` has to be spelled out in the path.)

Generally, omitting the `actionName` part of any path will associate the request with the controller's `Index()` action method.

### Views
In the MVC paradigm for ASP.NET, the *controller* is combined with the *view* to create a 'page'. MVC provides the [`ViewResult`](https://docs.microsoft.com/en-us/dotnet/api/system.web.mvc.viewresult?view=aspnet-mvc-5.2) action result type for returning views from an action method. The corresponding controller method is `View()`:

```c#
public class ComicBookController : Controller
{
    public ActionResult Detail()
    {
        return View();
    }
}
```
- By default, this will make MVC look in the `~/Views/ComicBook/` and `~/Views/Shared/` directories for a template file called `Detail`.
- By convention, all views are kept in the `Views` folder.
- It is however possible to explicitely request a view that doesn't follow these conventions from the controller action method.

#### Strongly typed views
A *strongly typed view* is an MVC view that is associated with a specific type.

**In the controller:** Create an actual instance of the model and pass this into the call to `View()` (or other result type) in the relevant action method, i.e. `View(modelInstance)`.

> *Constructing and filling the model, and then passing it along to the view, is a classic controller job.*

**In the view:** 
* To define which class to use as a model, add a *model view directive* to the top of the view, using the fully qualified namespace of model:
    ```c#
    @model ProjectName.Models.ModelName
    ```
* A strongly typed view exposes the model instance (i.e. that was passed in from the controller) through the view's `Model` property; so you can access the model's properties via `Model.PropertyName`.


_________________________

## Razor & MVC
Razor is a markup syntax that lets you embed server-based code (Visual Basic and C#) into web pages. It can be seen as an evolution of the old “.aspx” style markup.

ASP.NET MVC has implemented a view engine that allows us to use Razor inside of an MVC application to produce HTML. 

Razor can either be used as part of a classic MVC-structured application, or as part of an *MVVM (Model-View-ViewModel)* setup, whereby the model and controller code is also included within the Razor Page itself. For more on the differences between these, see: https://stackify.com/asp-net-razor-pages-vs-mvc/.


### Basic Syntax
> Super handy reference! => **[C# Razor Syntax Quick Reference](https://haacked.com/archive/2011/01/06/razor-syntax-quick-reference.aspx/)**

1. Add code to a page using the `@` character: it starts inline expressions, single statement blocks, and multi-statement blocks
1. Single or multi statement code blocks are enclosed in braces, each statement ending on a semicolon
1. Expressions don't require braces or semicolons
1. Variables can be used to store values
1. Files have the extension `.cshtml`

```c#
<!-- Single statement block  -->
@{ var myMessage = "Hello World"; }

<!-- Inline expression -->
<p>The value of myMessage is: @myMessage</p>

<!-- Multi-statement block -->
@{
    var greeting = "Welcome to our site!";
    var weekDay = DateTime.Now.DayOfWeek;
    var greetingMessage = greeting + " Today is: " + weekDay;
}
<p>The greeting is: @greetingMessage</p>
```

#### HTML encoding
> For security reasons, content displayed in a page using the `@` character will be HTML-encoded, replacing reserved HTML characters (such as `<` and `>` and `&`) with codes that enable them to be displayed *as characters* in a web page instead of being interpreted as HTML tags or entities.

To output HTML markup that renders tags *as markup*, use `Html.Raw`:

```c#
@{ var description = "<p>Final issue! Even if Spider-Man survives... <strong>will Peter Parker?</strong></p>"; }

<div>@Html.Raw(description)</div>
```

#### Combining control flow & markup
Given the following variables:
```c#
@{
    var seriesTitle = "The Amazing Spider-Man";
    var artists = new string[]
    {
        "Script: Dan Slott",
        "Pencils: Humberto Ramos",
        "Inks: Victor Olazaba",
        "Colors: Edgar Delgado",
        "Letters: Chris Eliopoulos"
    };
}
```
...you can combine conditionals & loops with the markup as follows:
```c#
<div>
    <h1>@seriesTitle</h1>

    @if (artists.Length > 0)
    {
        <h5>Artists:</h5>
        <ul>
            @foreach (string artist in artists)
            {
                <li>@artist</li>
            }
        </ul>
    }
</div>
```

### Layout
The `_Layout.cshtml` file provides the overall look and feel for every page on our website, without having to have the related markup in each view (for example, header and footer markup). 
> *Typically, websites contain just a single layout page, but it is possible to have more than one layout page.*

The `@RenderBody` method is used in the layout file to indicate where the content for the view requested by the user should be included (i.e. the content for each individual page). This method can only be called once from a layout page.

In each view file, the layout to be used with a page is indicated as follows:
```c#
@{
    Layout = "~/Views/Shared/_Layout.cshtml";
}
```

### HTML helper methods
Used in MVC views to generate markup

- e.g. `@Html.ActionLink` - generates a link

Read more:
- https://dzone.com/articles/working-with-built-in-html-helper-classes-in-aspne
- https://www.tutorialsteacher.com/mvc/html-helpers
- https://docs.microsoft.com/en-us/aspnet/mvc/overview/older-versions-1/views/creating-custom-html-helpers-cs


### Functions
The purpose of a `@functions` block is to wrap up reusable code, like methods and properties, and then be able to call those methods or properties from other parts of the page.

###### Declaring functions and properties:
```C#
@functions {
    int userAge = 0;
    string HelloMessage(string user)
    {
        return "Hi " + user + ", how are you?";
    }
    
    int Age
    {
        get { return userAge; }
        set { userAge = value; }
    }
}
```

###### Using declared functions and properties on the page:
```html
<!DOCTYPE html>
<html>
    <head>
        <title></title>
        <meta http-equiv="content-type" content="text/html;charset=utf-8" />
    </head>
    <body>
        @{
            Age = 27; // In a real page, you might retrieve the user's age from a form or database
        }
        <p>The value of the <code>HelloMessage</code> method: @HelloMessage("James")</p>   
        <p>The value of the <code>Age</code> property: @Age.ToString()</p>    
    </body>
</html>
```

### The Request object
You'll often work with the `Request` object, which gives you information like the values of text boxes (form fields) on the page (see [example below](#reading-user-input)), what type of browser made the request, the URL of the page, the user identity, etc. 

The following example shows how to access properties of the `Request` object and how to call the `MapPath()` method of the Request object, which gives you the absolute path of the page on the server:

```html
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

```c#
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

### HttpContext
`HttpContext` can be used to [access the HTTP context](https://docs.microsoft.com/en-us/aspnet/core/fundamentals/http-context?view=aspnetcore-2.2) from Razor pages:

```C#
@{
    var numberOfCatsRequested = Context.Request.Query["cat-quantity"];
}
```

NB: it can also be accessed from [tag helpers](#tag-helpers), controllers, models, or any custom code or middleware.


**Sources:**
- https://docs.microsoft.com/en-us/aspnet/web-pages/overview/getting-started/introducing-razor-syntax-c
- https://www.w3schools.com/asp/razor_intro.asp
- https://blogs.msdn.microsoft.com/timlee/2010/07/30/using-functions-in-an-asp-net-page-with-razor-syntax/
- https://docs.microsoft.com/en-us/aspnet/core/fundamentals/http-context?view=aspnetcore-2.2
_________________________

## Bundling & Minification
Bundling and minification are two techniques used to improve request load time. Bundling and minification improve load time by reducing the number of requests to the server and reducing the size of requested assets (such as CSS and JavaScript.)

Most of the current major browsers limit the number of simultaneous connections per each hostname to six. That means that while six requests are being processed, additional requests for assets on a host will be queued by the browser, so if your website is comprised of a great number of `.html`/`.css`/`.js` files, this will significantly impair page load time.

- **Bundling** allows you to combine (bundle) multiple files into a single file.
    - You can create CSS, JavaScript and other bundles. 
    - Fewer files means fewer HTTP requests and that can improve first page load performance.
- **Minification** performs a variety of different code optimizations to scripts or css, such as removing unnecessary white space and comments and shortening variable names to one character. 


### Webpack
***NB: Most modern day projects tend to use WebPack*** instead of ASP.NET's built in bundler. Webpack essentially does the same thing, but works better with UI frameworks such as Angular, React etc.

For more details, refer to:
- [How to use Webpack in ASP.Net core projects](https://codeburst.io/how-to-use-webpack-in-asp-net-core-projects-a-basic-react-template-sample-25a3681a5fc2)


### ASP.NET bundler
Since ASP.NET 4.5, it comes with its own bundler.

**To enable ASP.NET bundling & minification**, set the value of the `debug` attribute in the `compilation` element in the *Web.config* file to `false`:
```xml
<system.web>
    <compilation debug="false" />
    <!-- Lines removed for clarity. -->
</system.web>
```
Alternatively, you can enable bundling & minification with the `EnableOptimizations` property on the `BundleTable` class - NB this will override the Web.config setting:
```c#
public static void RegisterBundles(BundleCollection bundles)
{
    bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                 "~/Scripts/jquery-{version}.js"));

    // Code removed for clarity.
    BundleTable.EnableOptimizations = true;
}
```

**NB:** Minified files have *.min.* in the file name, e.g.: *FileX.min.js*

A ***BundleConfig.cs*** file will be created in any new ASP.NET MVC project (the default location for this is *App\_Start\BundleConfig.cs*).

Use the `RegisterBundles` method to define any new bundles, and rules for the sources they should be created from, for example:
```c#
public static void RegisterBundles(BundleCollection bundles)
{
     bundles.Add(new ScriptBundle("~/bundles/jquery").Include(
                 "~/Scripts/jquery-{version}.js"));
         // Code removed for clarity.
}
```
- This creates a new JavaScript bundle named "`~/bundles/jquery`" that includes all the appropriate files in the Scripts folder that match the wild card string "~/Scripts/jquery-{version}.js".
- The `Bundle` class' `Include()` method takes an array of strings, where each string is a virtual path to a resource. 
- A range of other methods exist, for example `IncludeDirectory()` to add all the files in a directory (and optionally all subdirectories) which match a search pattern.

**Bundles are referenced in views using the `Render()` method**, (`Styles.Render()` for CSS and `Scripts.Render()` for JavaScript). The following markup from the *Views\Shared\_Layout.cshtml* file shows how the default ASP.NET internet project views reference CSS and JavaScript bundles.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    @* Markup removed for clarity.*@    
    @Styles.Render("~/Content/themes/base/css", "~/Content/css")
    @Scripts.Render("~/bundles/modernizr")
</head>
<body>
    @* Markup removed for clarity.*@
   
    @Scripts.Render("~/bundles/jquery")
    @RenderSection("scripts", required: false)
</body>
</html>
```
 
- The Render methods takes an array of strings, so you can add multiple bundles in one line of code.
- The bundle names need to match the ones created in the *BundleConfig.cs*.


**Sources:**
- https://docs.microsoft.com/en-us/aspnet/mvc/overview/performance/bundling-and-minification

_________________________

## Tag Helpers
Tag Helpers enable server-side code to participate in creating and rendering HTML elements in Razor files.

- Example: The built-in ImageTagHelper can append a version number to the image name. Whenever the image changes, the server generates a new unique version for the image, so clients are guaranteed to get the current image (instead of a stale cached image).
- There are many built-in Tag Helpers for common tasks - such as creating forms, links, loading assets and more - and even more available in public GitHub repositories and as NuGet packages.
    - Most built-in Tag Helpers target standard HTML elements and provide server-side attributes for the element.
- Tag Helpers are authored in C#, and they *target HTML elements* based on element name, attribute name, or parent tag.

For the most part, Razor markup using Tag Helpers looks like standard HTML. A rich IntelliSense environment helps create and navigate HTML and Razor markup.

### Using Tag Helpers

*Add more notes here based on sources below*


### Building your own Tag Helpers
Custom Tag Helpers need to implement [the abstract base class `TagHelper`](https://docs.microsoft.com/en-us/dotnet/api/microsoft.aspnetcore.razor.taghelpers.taghelper?view=aspnetcore-2.2).

*Add notes here based on https://docs.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/authoring?view=aspnetcore-2.2*


**Sources:**
- https://docs.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/intro?view=aspnetcore-2.2
- https://docs.microsoft.com/en-us/aspnet/core/mvc/views/tag-helpers/authoring?view=aspnetcore-2.2

_________________________

## Areas in ASP.NET
The main use of Areas is to physically partition web projects in separate units. 


