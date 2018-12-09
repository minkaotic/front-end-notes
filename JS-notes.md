# JS notes

## Contents:
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

The browser has a **global environment** (global scope) which contains a great number of global variables, such as `location.href`, `alert()` and loads more. All of these are properties of a single global object called **window**. (It can be explored by typing `window` in the browser's JS console.) The **`document` object** is another key property of the browser's `window`:

- it is a representation of a webpage which JS can use
- changes that JavaScript makes to the DOM alter the web page
- this is done by selecting and controlling elements of the currently loaded web page
- i.e. `document.getElementById('myHeading').style.color = 'red'`

### Basic interactions

*To add lines of content to a page:*
```
document.write("<h2>Sudden new headline</h2>");
document.write("<p>I'm practicing interacting with the DOM.</p>");
```

*To listen for a user interaction and make a change in response:*
```
const myHeading = document.getElementById('myHeading');

myHeading.addEventListener('click', () => {
  myHeading.style.color = 'red';
});
```

*More involved version incl. an input field for the color & button to apply:*
```
const myHeading = document.getElementById('myHeading');
const myButton = document.getElementById('myButton');
const myTextInput = document.getElementById('myTextInput');

myButton.addEventListener('click', () => {
  myHeading.style.color = myTextInput.value;
  });
```

### Different Selectors
- Element selectors like `getElementById()` return a **HTML element**.
- Element selectors like `getElementsByClassName()` or `getElementsByTagName()` return a **HTML collection**.

Elements in a collection can be accesses by index, e.g.:
```
const body = document.getElementsByTagName('body')[0];
```

#### CSS query selectors
- `querySelector()` and `querySelectorAll()` return an HTML element and a [Node List](https://developer.mozilla.org/en-US/docs/Web/API/NodeList) of HTML elements, respectively.
- They take queries such as:
  - tag name - `querySelector('li')`
  - element id - `querySelector('#myId')`
  - element class - `querySelector('.myClass')`
  - element atrribute - `querySelector('[title="fun"]')`
  - CSS pseudo class queries - `querySelector('li:nth-child(odd)')`

It's often possible to use different selectors to achieve the same thing. To decide which one is the best option, consider browser compatibility as well as other details in a given selector's spec.

Resources:
- [MSDN](https://developer.mozilla.org/en-US/)
- [Can I Use...](https://caniuse.com/#)
- [Babel](https://babeljs.io/)
