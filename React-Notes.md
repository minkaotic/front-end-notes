# React Notes
[React](https://reactjs.org/) is a JavaScript library for building user interfaces.
- Simplifies building and maintaining the UI of your application by breaking it up into smaller, reusable *components*.
- Reduces the complexity of updating your DOM elements when users interact with your application, thanks to the *virtual DOM*: when your application's data changes, React figures out which parts of your document need to be changed, and immediately updates only those parts.

## Contents
- [Setup](#setup)
- [React Basics](#react-basics)
  - [Creating & rendering React elements](#creating--rendering-react-elements)

_______________
## To Do
- [ ] Finish React Track on Treehouse
- [ ] Look into testing
- [ ] [Set up](https://teamtreehouse.com/library/add-react-to-a-project) a practice project locally
_______________

## Setup
There are 2 common ways to add React to a new project:
1. Using [React toolchains](https://reactjs.org/docs/create-a-new-react-app.html), for example [Create React App](https://reactjs.org/docs/create-a-new-react-app.html#create-react-app)
2. with [React's CDN links](https://reactjs.org/docs/cdn-links.html)

#### Why 2 separate libraries?
:bulb: When building web applications in React, you use two libraries: `React` and `ReactDom`:
- React started out as a library for building interfaces in the browser, but the patterns and tools it provided proved so useful that it has since been extended to native application development.
- When React Native came along, `React` (as the core library), and `ReactDom` (for web app development) were split into two libraries.

_______________

## React Basics
### Creating & rendering React elements
> :bulb: *React elements are the smallest building blocks of React apps.*

You can call [**`createElement()`**](https://reactjs.org/docs/react-api.html#createelement), using the React API to create and return React elements. This takes three arguments:

1. the element *type* - usually a string representing a HTML type
2. an object containing any *attributes* and values to give the element (pass an empty object `{}` or `null` to skip)
3. params comprising the *content or children* of the element

```js
const title = React.createElement(
  'h1',
  { id: 'title' },
  'A nice main title'
);
```

> **NB:** `createElement()` does not create actual DOM elements; instead `title` is an object that describes a DOM node (an *object representation of a DOM node*).

To render React elements to the DOM, call [**`ReactDOM.render()`**](https://reactjs.org/docs/react-dom.html#render) - which takes two arguments:

1. the element you'd like to render
2. the actual HTML element you would like to update / render to (typically **where the React application will be *mounted***)

```html
<body>
  <div id="root"></div>
</body>
```
```js
ReactDOM.render(
  title,
  document.getElementById('root')
);
```
> :bulb: **In other words:** React doesn't manipulate the DOM directly; instead it manages object representations of DOM nodes, and then it is up to `render()` to interpret these element objects and create DOM nodes out of them.

#### Rendering an element with child elements:

```js
const title = React.createElement('h1', ...);
const desc = React.createElement('p', ...);

const header = React.createElement(
  'header',
  null,
  title,
  desc
);

ReactDOM.render(
  header,
  document.getElementById('root')
);
```
