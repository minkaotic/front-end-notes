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
  - [State](#paw_prints-state)
  - [Handling events](#paw_prints-handling-events)
- [React Context API](#react-context-api)

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
1. define the component as [either a function or class](https://reactjs.org/docs/components-and-props.html#function-and-class-components) (see [Example 2](#example-2---function-vs-class-component) below for side-by-side comparison!)
2. display the component with a JSX tag: JSX lets you define your own tags. A JSX tag can not only represent an HTML element (like `<h1>`, `<span>`, and `<header>`), it can also represent a user-defined component (e.g. `<App />`, `<Header />`, `<Player />`, `<Counter />` below).

#### Example 1 - App using components (defined as functions) & JSX
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

#### Example 2 - function vs class component
| Function component  | Class component |
| ------------- | ------------- |
| ![test](/img/function-component.png)  | ![test](/img/class-component.png)   |

</br>

### :paw_prints: Props
Every React component and element can receive a list of attributes called properties (or props). Props are a core concept in React as it's how you get data into a component: most of the components in your UI will be configured with props. For example, you'll add functionality to a component, have it behave a certain way, and display its contents with props.

>*Props look like custom HTML attributes.*

Using props:
1. Define the props in a component's JSX tag, using attribute syntax (`<MyComponent propName={ someValue } />`)
2. Enable the use of props in a component - when defined as a function, React provides one default argument: a props object (customarily called `props`) containing a list of props given to the component (`const MyComponent = (props) => {...}`)

#### Previous example, updated with props, making player data dynamic:
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

const App = (props) => {
  return(
    <div className="scoreboard">
      <Header title="Scoreboard" totalPlayers={props.initialPlayers.length} />
      {props.initialPlayers.map( player => 
        <Player name={player.name} score={player.score} />
      )}
    </div>
  );
}

// players is an array of objects with the data needed by the app
ReactDOM.render(
  <App initialPlayers={ players } />,
  document.getElementById('root')
);
```

> :bulb: **Things to note:**

- Prop names in JSX (like all [JSX attributes](https://reactjs.org/docs/introducing-jsx.html#specifying-attributes-with-jsx)) use **`camelCasing`**

- Whenever passing a prop a value other than a string, place it within curly braces, i.e. `totalPlayers={1}`, so it gets evaluated as a JSX expression

- All props are **immutable**, so a component can read the props given to it, but never change them (attempting to assign to a prop will throw an error). The (parent) component higher in the tree owns and controls the property values.

- :warning: The above example would create a React console error, as the `<Player />` elements created with an iteration method haven't been given a unique key - see below for more details.

#### A note about React keys
> :bulb: **Pass a key prop to a component any time you are creating elements by iterating over an array of items!**

React manages what gets rendered to the DOM. In order for this process to be fast and efficient, React needs a way to quickly know which items were changed, added, or removed. For this, React gives elements a special built-in prop named `key` - a unique identifier for an element in a list. [The React docs on keys](https://reactjs.org/docs/lists-and-keys.html#keys) recommend this should be a string.

> React does not recommend using `index` for unique keys, because the `index` might not always uniquely identify elements. It's usually best to use a unique id.

##### Updated example using keys for each player
```js
const App = (props) => {
  return(
    <div className="scoreboard">
      <Header title="Scoreboard" totalPlayers={props.initialPlayers.length} />
      {props.initialPlayers.map( player => 
        <Player name={player.name} score={player.score} key={ player.id.toString() } />
      )}
    </div>
  );
}

```

</br>

### :paw_prints: State
#### Props vs State
There are 2 ways data gets handled in React components: props & state. Both props and state changes trigger a *render update*. However:
- Since props are immutable, *if a component needs to alter one of its attributes at some point in time, that attribute should be part of its STATE, otherwise it should just be a PROP for that component.*
- A component cannot change its own props, but it is responsible for putting together the props of its child components.
- The state starts with a default value when a component mounts, and then gets mutated (typically in response to user events).
- A component manages its own state internally, but (besides setting an initial state) has no business fiddling with the state of its children. You could say the state is *private*.
- Data from state in one component is still likely distributed *to other components* through props.

:point_right: Source: [this detailed discussion of props vs state](https://github.com/uberVU/react-guide/blob/master/props-vs-state.md); see in particular this nice [table overview of when props/state change](https://github.com/uberVU/react-guide/blob/master/props-vs-state.md#changing-props-and-state)

#### Should this component have state?
State is optional. Since state increases complexity and reduces predictability, a component without state is preferable. Even though you clearly can't do without state in an interactive app, you should avoid having too many stateful components.

> :pushpin: **State is only available to class components** - [see this section of the docs](https://reactjs.org/docs/state-and-lifecycle.html#converting-a-function-to-a-class) for more info.

#### Initialising state
Since state is an object, you create and initialise state within a component class

##### OPTION 1: Constructor syntax
```js
constructor() {
  super()  // call constructor of the Component class
  this.state = {
    score: 0  // set initial state, before the component mounts
  }
}
```

##### OPTION 2: Class property syntax
> This is not supported in all browsers, but since we transpile with Babel anyway, it doesn't really matter!
```js
state = {
  score: 0
};
```

##### Full component example using class property syntax:
```js
class Counter extends React.Component {
  state = {
    score: 0
  };
  
  render() {
    return (
      <div className="counter">
        <button className="counter-action decrement"> - </button>
        <span className="counter-score">{ this.state.score }</span>
        <button className="counter-action increment"> + </button>
      </div>
    );
  }
}
```
#### The `setState()` method
**NB: state cannot be modified directly**, i.e. `this.state.score += 1;` *would not work*! Instead, React's built-in [**`setState()`**](https://reactjs.org/docs/react-component.html#setstate) method needs to be used. You pass this an object containing the part of the state that should update, and the value it should update to, i.e.:

```js
this.setState({
  score: this.state.score + 1
});
```

Using `setState()` ensures that the component is re-rendered on state changes.

> :zap: Be aware that `this.props` and `this.state` may be updated asynchronously, so relying on their values for calculating the next state, as in the above example, isn't best practice and can lead to race conditions. [See docs](https://reactjs.org/docs/state-and-lifecycle.html#state-updates-may-be-asynchronous) for more detail, but in short, `setState()` alternatively accepts a callback function that produces state based on the previous state in a more reliable way:

```js
this.setState( prevState => ({
  score: prevState.score + 1
}));
```

</br>

### :paw_prints: Handling events
[React docs on Handling Events](https://reactjs.org/docs/handling-events.html) | [Passing arguments to Event Handlers](https://reactjs.org/docs/handling-events.html#passing-arguments-to-event-handlers)

In class components, a common pattern is to create event handlers as a method on the class - see `incrementScore()` and `decrementScore()` methods in the [example](#example-of-component-with-event-handling) below. This is then hooked up with [React's built-in events](https://reactjs.org/docs/events.html#supported-events), e.g. `onClick` - which are defined inline in the JSX template, and take a reference to the event handler they should call.

#### A note on method binding and `this` in React components
> :zap: When you create a class component that extends from `React.Component`, any custom methods you create are not bound to the component by default. You need to bind your custom methods, so that `this` refers to the component instance. There are several ways to do this, including:
- call `bind()` in the `render()` method where the React event is set up, e.g. `onClick={this.incrementScore.bind(this)}`
- pass an arrow function to the React event, e.g. `onClick={() => this.incrementScore}` (may cause performance issues in some cases, as a different callback is created each time the component renders - see [docs](https://reactjs.org/docs/handling-events.html) for more details)
- define the event handler method itself as an arrow function (`incrementScore = () => {...}`; cf. [example](#example-of-component-with-event-handling) below), or bind the event handler in the constructor (`constructor() { this.incrementScore = this.incrementScore.bind(this); }`) - both of these approaches enable you to just reference `this` in the event: `onClick={this.incrementScore}`

#### Example of component with event handling
```js
class Counter extends React.Component {
  state = {
    score: 0
  };

  // event handler 1
  incrementScore = () => {
    this.setState( prevState => ({
      score: prevState.score + 1
    }));
  }

  // event handler 2
  decrementScore = () => {
    this.setState( prevState => ({
      score: prevState.score - 1
    }));
  }

  render() {
    return (
      <div className="counter">
        // pass event handlers as a reference to React's onClick event
        <button className="counter-action decrement" onClick={this.decrementScore}> - </button>
        <span className="counter-score">{ this.state.score }</span>
        <button className="counter-action increment" onClick={this.incrementScore}> + </button>
      </div>
    );
  }
}
```

_______________

## React Context API
In the typical React data flow, components communicate with each other via [props](#paw_prints-props). A parent passes props down to child components. Sometimes the intermediary components get props passed to them *with the sole purpose of passing that data down one (or several) more levels*. This cascade of props is often referred to as ["prop drilling"](https://kentcdodds.com/blog/prop-drilling).

:point_right: **The React [Context API](https://reactjs.org/docs/context.html) provides a way to pass data to components without having to pass props manually at every single level.**

> Prior to Context being a stable feature in React, developers would use state management libraries like [MobX](https://mobx.js.org/README.html) and [Redux](https://redux.js.org/) instead.
