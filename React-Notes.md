# React Notes ⚛️
[React](https://reactjs.org/) is a JavaScript library for building user interfaces.
- Simplifies building and maintaining the UI of your application by breaking it up into smaller, reusable *components*.
- Reduces the complexity of updating your DOM elements when users interact with your application, thanks to the *virtual DOM*: when your application's data changes, React figures out which parts of your document need to be changed, and immediately updates only those parts.

## Contents
- [Setup](#setup)
- [React Basics](#react-basics)
  - [Creating & rendering React elements](#paw_prints-creating--rendering-react-elements)
  - [JSX: declarative syntax for UI elements](#paw_prints-jsx-declarative-syntax-for-ui-elements)
  - [Components](#paw_prints-components)
  - [Props](#paw_prints-props)

_______________
## To Do
- [ ] Read the "Main Concepts" in docs, including [Thinking in React](https://reactjs.org/docs/thinking-in-react.html)
- [ ] Finish [Learn React](https://teamtreehouse.com/tracks/learn-react) track on Treehouse
- [ ] Look into testing
- [ ] [Set up](https://teamtreehouse.com/library/add-react-to-a-project) a practice project locally (also see [this article](https://www.twilio.com/blog/2015/08/setting-up-react-for-es6-with-webpack-and-babel-2.html) for more setup bantz)
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
### :paw_prints: Creating & rendering React elements
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
</br>

### :paw_prints: JSX: declarative syntax for UI elements
**Docs:** [Introduction](https://reactjs.org/docs/introducing-jsx.html) | [In Depth](https://reactjs.org/docs/jsx-in-depth.html)

JSX is a syntax extension to JavaScript that is used with React to describe elements in the UI. It uses a markup-like syntax to create React elements, and is used by most React developers as it resembles writing HTML.

JSX essentially provides syntactic sugar / an abstraction on top of `React.createElement()`, and needs to be transpiled (using e.g. Babel) into valid JS in order to work in the browser.

#### Rendering an element with children, rewritten in JSX:
```js
const desc = 'A nice page written in React';
const titleId = 'main-title';

const header = (
  <header>
    <h1 id={titleId}>A nice main title</h1>
    <p className="main-desc">{ desc }</p>
  </header>
);

ReactDOM.render(
  header,
  document.getElementById('root')
);
```
> :bulb: **Things to note:**

- Use parentheses to surround multi-line JSX - this is not required, but good practice

- JSX allows embedding JavaScript expressions within it, written inside curly braces. This allows making your JSX dynamic.

- No `"..."` needed in the `<h1>`'s attribute when using a JSX expression

- JSX attributes aren't always like for like; e.g. to set classes, use JSX attribute `className` (this is due to `class` being reserved word in JS)

- JSX comments are in curly braces too, combined with `/*...*/` - this applies to both inline and multi-line comments. `{/* this is a comment */}`

</br>

### :paw_prints: Components
A [component](https://reactjs.org/docs/components-and-props.html) is a piece of UI that you can reuse. Being able to split your UI code into independent, reusable pieces, and think about each piece in isolation is one of the most embraced features of React.

React components are written in plain JavaScript, with the help of JSX, and they contain the logic required to display a small part of your UI. Components accept arbitrary inputs (called ["props" - see next section](#paw_prints-props)) and return React elements describing what should appear on the screen.

To create a React component:
1. define the component as [either a function or class](https://reactjs.org/docs/components-and-props.html#function-and-class-components)
2. display the component with a JSX tag: JSX lets you define your own tags. A JSX tag can not only represent an HTML element (like `<h1>`, `<span>`, and `<header>`), it can also represent a user-defined component (e.g. `<App />`, `<Header />`, `<Player />`, `<Counter />` below).

#### Example - App using components (defined as functions) & JSX
```js
const Header = () => {
  return (
    <header>
      <h1>Scoreboard</h1>
      <span className="stats">Players: { playerCount }</span>
    </header>
  );
}

const Player = () => {
  return (
    <div className="player">
      <span className="player-name">{ currentPlayerName }</span>
      <Counter />
    </div>
  );
}

const Counter = () => {
  return (
    <div className="counter">
      <button className="counter-action decrement"> - </button>
      <span className="counter-score">{ currentPlayerScore }</span>
      <button className="counter-action increment"> + </button>
    </div>
  );
}

const App = () => {
  return(
    <div className="scoreboard">
      <Header />
      <Player />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

> :bulb: **Things to note:**

- **Capitalised component names:** React components are required to start with an uppercase letter both in the function definition and when using it in JSX - the latter is to differentiate custom components from native DOM elements

- The **self-closing form of the tag** (e.g. `<Header />`) can be used if the component has no children

- Usually only pass the **top-level component** to the `ReactDOM.render()` method

> :bulb: **When a component contains another component, it's called [COMPOSITION](https://reactjs.org/docs/components-and-props.html#composing-components).** Composing components is a core principle in React, and you typically have parent components with one or many child components. This gives the parent component the ability to control how its child components are rendered.

</br>

### :paw_prints: Props
Every React component and element can receive a list of attributes called properties (or props). Props are a core concept in React as it's how you get data into a component: most of the components in your UI will be configured with props. For example, you'll add functionality to a component, have it behave a certain way, and display its contents with props.

>*Props look like custom HTML attributes.*

Using props:
1. Define the props in a component's JSX tag, using attribute syntax (`<MyComponent propName={ someValue } />`)
2. Enable the use of props in a component - when defined as a function, React provides one default argument: a props object (customarily called `props`) containing a list of props given to the component (`const MyComponent = (props) => {...}`)

#### Previous example, updated with props:
```js
const Player = (props) => {
  return (
    <div className="player">
      <span className="player-name">{ props.name }</span>
      <Counter score={ props.score } />
    </div>
  );
}

const Counter = (props) => {
  return (
    <div className="counter">
      ...
      <span className="counter-score">{ props.score }</span>
      ...
    </div>
  );
}

const App = () => {
  return(
    <div className="scoreboard">
      ...
      <Player name="Guil" score={ 50 } />
      <Player name="Treasure" score={ 90 } />
      <Player name="Ashley" score={ 85 } />
      <Player name="James" score={ 80 } />
    </div>
  );
}

```

> :bulb: **Things to note:**

- Prop names in JSX (like all [JSX attributes](https://reactjs.org/docs/introducing-jsx.html#specifying-attributes-with-jsx)) use **`camelCasing`**

- Whenever passing a prop a value other than a string, place it within curly braces, i.e. `totalPlayers={1}`, so it gets evaluated as a JSX expression

- All props are **immutable**, so a component can read the props given to it, but never change them (attempting to assign to a prop will throw an error). The (parent) component higher in the tree owns and controls the property values.

_______________


