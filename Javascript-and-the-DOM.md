# JavaScript and the DOM

## Contents:
- [Intro](#intro)
  - [Adding JS code to a page](#adding-js-code-to-a-page)
- [The DOM](#the-dom)
  - [Example Interactions](#example-interactions)
  - [Different Selectors](#different-selectors)
  - [Various DOM Manipulation Methods](#various-dom-manipulation-methods)
  - [Traversing the DOM](#traversing-the-dom)
- [Events](#Events)
  - [First Class Functions in JS](#first-class-functions-in-js)
  - [Listening for Events](#listening-for-events)
  - [Event bubbling & delegation](#event-bubbling--delegation)
 
__________

## Intro

*JS allows to make pages interactive, through:*
- selecting elements on the page
- manipulating elements
- listening for user actions

This is based on the **[DOM (Document Object Model)](#the-dom)**.

### Adding JS code to a page
- link any JS files in the html file to execute them when the page loads, like so: `<script src="file-name.js"></script>`
- link at bottom of `<head>` to run script before the content of the page loads, or at bottom of `<body>` to run script once page has loaded
- **Fun fact:** variables declared in the JS script will be accessible in the browser's JS console too!

__________

## The DOM

The browser has a **global environment** (global scope) which contains a great number of global variables, such as `location.href`, `alert()` and loads more. All of these are properties of a single global object called **window**. (It can be explored by typing `window` in the browser's JS console.) The **`document` object** is another key property of the browser's `window`:

- it is a representation of a webpage which JS can use
- changes that JavaScript makes to the DOM alter the web page
- this is done by selecting and controlling elements of the currently loaded web page
- i.e. `document.getElementById('myHeading').style.color = 'red'`

#### Nodes vs. Elements
- Nodes belong to the DOM
- Elements are plain HTML
- ...but both are conceptually often interchangeable

__________

### Example Interactions

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
  myTextInput.value = '';         // to clear input field after submission
});
```
__________

### Different Selectors
#### Specific element selectors
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
  - element attribute value - `querySelector('[title="fun"]')`
  - elements with a certain attribute - `querySelectorAll('a[title]')`
  - elements of a particular nesting rule - `querySelectorAll('nav ul li a')` (= all links in the nav bar)
  - CSS pseudo class queries - `querySelector('li:nth-child(odd)')` or `querySelector('li:last-child')`

It's often possible to use different selectors to achieve the same thing. To decide which one is the best option, consider browser compatibility as well as other details in a given selector's spec.

Resources for this include:
- [MSDN](https://developer.mozilla.org/en-US/)
- [Can I Use...](https://caniuse.com/#)
- [Babel](https://babeljs.io/)

__________

### Various DOM Manipulation Methods
#### Getting & setting text
- Get & set an element's text using the `element.textContent` property:
```
let myHeading = document.querySelector('h1');
console.log(myHeading.textContent);                     //retrieve and use element's text
myHeading.textContent = 'This is the new headline';     //change element's text
```

- `element.innerHTML` can be (mis)used for this too, but is more commonly used to alter the actual HTML of parts of the page

#### Changing element attributes
Attributes, like the href attribute on a link, or the action attribute on a form, exist as properties of an element object. These can be manipulated with `Element.attribute`, for example:

**HTML**
```
...
<input type="text" class="description">
...
```

**Javascript**
```
const input = document.querySelector('input');
console.log(input.type);          //returns "text"
input.type = 'checkbox'           // changes input type
```

***NB:*** class attributes are a special case and are accessed via the `element.className` property.

#### Changing element styles
The `element.style` property and its sub-properties are usually used to **set** styles only, not to retrieve them. This is because it will *only* retrieve active *in-line* styles for a given element, and won't show e.g. styles applied from a separate CSS stylesheet!

Examples:
- Change background colour: `element.style.backgroundcolor = 'blue'`
- Hide (and unhide) elements from the page: `element.style.display = 'none'`

#### Adding and removing new DOM elements
- Create a new element with `document.createElement()`, then insert it with `Node.appendChild(childElement)` for example:
```
const addItemInput = document.querySelector('button.addItemButton');
let ul = document.getElementsByTagName('ul')[0];
let li = document.createElement('li');
li.textContent = addItemInput.value;
ul.appendChild(li);
```

- Remove an element with `Node.removeChild(childElement`).

__________

### Traversing the DOM
DOM traversal refers to the selection of elements based on their relationship to another element within the DOM.

- To get a reference to an element's **parent** node, use its `parentNode` property.
- To get the **sibling** immediately prior to the element in its sibling list, use its `previousElementSibling` property.
- To get the **sibling** immediately after the element in its sibling list, use its `nextElementSibling` property.
- To insert a node before a given reference node in a list of children of a parent node, use `parentNode.insertBefore(newNode, referenceNode)`.
- To get children of an element:
  - `children` to get a HTML collection of all the children of an element
  - `firstElementChild` to get its first child
  - `lastElementChild` to get its last child

__________

## Events
Any time users interact with a webpage, they generate all kinds of events: moving the mouse around, scrolling, or clicking a link. Browsers "listen" for events and, with JavaScript, we can do something in response to an event.

- See also: [Thorough list of DOM events on MDN](https://developer.mozilla.org/en-US/docs/Web/Events)

__________

### First Class Functions in JS
Given a function that takes another function as an argument, such as:
```
function exec(func, arg) {
  func(arg);
}
```
...then the following three ways of calling it are equivalent:

**Option 1:**
```
function say(something) {
  console.log(something);
}

exec(say, 'Hello!');
```

**Option 2:**
```
exec(function say(something) {
  console.log(something);
}, 'Hello!');
```

**Option 3:**
```
exec((something) => {
  console.log(something);
}, 'Hello!');
```

_______________

### Listening for Events
`EventTarget.addEventListener(eventType, function)` allows to pass a function for callback any time the event takes place. See [MDN docs](https://developer.mozilla.org/en-US/docs/Web/API/EventTarget/addEventListener) for more details.

The callback function that is passed to `addEventListener` is often called an *event handler*.

_______________

### Event bubbling & delegation

An event received by an element doesn't stop with that one element. That event moves to other elements like the parent, and other ancestors of the element. This is called "event bubbling".

![DOM tree](https://github.com/minkaotic/front-end-notes/blob/master/img/dom_tree.png)

This is useful because it allows us to add an event listener to a parent element and let it handle events on its children:
- without the need for *for loops* for each child that we want the event to be handled for
- makes the code resilient to changes to the DOM that add or remove children
- ***But: How does the parent know which child triggered the event?***

...by passing the `event` object as an argument to the `eventListener`! This allows us to call the **event target**. E.g.:
```
document.addEventListener('click', (event) => {
  console.log(event.target);
});
```

- You can even access the *properties* of the element that triggered the event directly via the `target`, for example: `event.target.tagName`. This is useful if you need to make decisions based on these properties.

- `event.currentTarget` is the node on which the running listener was registered on. This is the same value of the listener invocation context, i.e, the value referenced by the `this` keyword.

***Some more notes on event propagation...***
- *Event Propagation* is the blanket term for both event bubbling and event capturing
- Technically, propagation doesn't only bubble up, but flows down from the Window during the capture phase first. This is explained well in the article ["What Is Event Bubbling in JavaScript? Event Propagation Explained"](https://www.sitepoint.com/event-bubbling-javascript/)
- The event propagation can be stopped in any listener by invoking the `stopPropagation()` method of the event object. (Any other remaining listeners attached on the current target will still receive the event, but it won't be bubbled up further from there.)
- *Event Cancellation:* Some events are associated with a default action that the browser executes at the end of the propagation. For instance, the click on a link element or the click on a form submit button causes the browser to navigate to a new page, or submit the form respectively. It is possible to avoid the execution of such default actions by calling the event object's `event.preventDefault()`, in a listener.
