# JS notes

List of contents:
- [Intro](#intro)
- [The DOM](#the-dom)

## Intro
- link any JS files in the html file to execute them when the page loads, like so: `<script src="file-name.js"></script>`
- link at bottom of `<head>` to run script before the content of the page loads, or at bottom of `<body>` to run script once page has loaded

*JS also allows to make pages interactive, through:*
- selecting elements on the page
- manipulating elements
- listening for user actions

This is based on the **DOM (Document Object Model)**

## The DOM

The browser has a **global environment** which contains a great number of global variables, such as `location.href`, `alert()` and loads more. All of these are properties of a single global object called **window**. (It can be explored by typing `window` in the browser's JS console.) The **`document` object** is another key property of the browser's `window`:
- can be used to select and control elements of the currently loaded web page
- i.e. `document.getElementById('myHeading').style.color = 'red'`


*To add lines of content to a page:*
```
document.write("<h2>My first JavaScript program</h2>");
document.write("<p>I'm practicing 'debugging'.</p>");
```
