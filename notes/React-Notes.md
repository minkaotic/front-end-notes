# React Notes ⚛️
Main Resources: [Treehouse React Track](https://teamtreehouse.com/tracks/learn-react) | [React docs](https://reactjs.org/docs/getting-started.html)

**[React](https://reactjs.org/) is a JavaScript library for building user interfaces.**
- Simplifies building and maintaining the UI of your application by breaking it up into smaller, reusable *components*.
- Reduces the complexity of updating your DOM elements when users interact with your application, thanks to the *virtual DOM*: when your application's data changes, React figures out which parts of your document need to be changed, and immediately updates only those parts.


## Contents
- [Setup](#setup)
- [React Basics](#react-basics)
  - [Creating & rendering React elements](#paw_prints-creating--rendering-react-elements)
  - [JSX: declarative syntax for UI elements](#paw_prints-jsx-declarative-syntax-for-ui-elements)
  - [Iteration in rendering](#paw_prints-iteration-in-rendering)
  - [Components](#paw_prints-components)
  - [Props](#paw_prints-props)
  - [State](#paw_prints-state)
  - [Handling events](#paw_prints-handling-events)
  - [Forms](#paw_prints-forms)
- [React Components in Depth](#react-components-in-depth)
  - [Unidirectional Data Flow](#paw_prints-unidirectional-data-flow)
  - [Lifecycle Methods](#paw_prints-lifecycle-methods)
  - [Advanced props](#paw_prints-advanced-props)
  - [PureComponent](#paw_prints-purecomponent)
  - [Refs](#paw_prints-refs)
- [React Context API](#react-context-api)
  - [Background: Prop drilling](#paw_prints-background-prop-drilling)
  - [Using Context](#paw_prints-using-context)

_______________
## To Do
- [ ] **Docs:** Read remaining "Main Concepts", starting from ["Conditional Rendering"](https://reactjs.org/docs/conditional-rendering.html) | Understand [render props](https://reactjs.org/docs/render-props.html)
- [ ] Finish [Learn React](https://teamtreehouse.com/tracks/learn-react) track on Treehouse
  - [ ] revisit [this video](https://teamtreehouse.com/library/the-provider-and-consumer-solution) at 2:19 and make separate notes about using spread operator for props!
- [ ] **Testing:** [Pluralsight Course](https://www.pluralsight.com/courses/testing-react-components) | [Tutorial](https://jestjs.io/docs/en/tutorial-react) | [Testing recipes](https://reactjs.org/docs/testing-recipes.html) | [React Testing Library intro](https://testing-library.com/docs/react-testing-library/example-intro)
- [ ] [React Authentication workshop](https://teamtreehouse.com/library/react-authentication/introducing-the-authentication-project/what-is-basic-authentication)

**Bonus!**
- [ ] Dmitri Pavlutin: [7 Architectural Attributes of a Reliable React Component](https://dmitripavlutin.com/7-architectural-attributes-of-a-reliable-react-component/) | [Orthogonal React Components](https://dmitripavlutin.com/orthogonal-react-components/) | [3 Rules of React State Management](https://dmitripavlutin.com/react-state-management/) | [Lifecycle methods, hooks, suspense: which is best for fetching in React?](https://dmitripavlutin.com/react-fetch-lifecycle-methods-hooks-suspense/)
- [ ] [React Europe 2020 conf videos](https://www.youtube.com/watch?v=nzeL1wZltf0&list=PLCC436JpVnK0Q4WHoB85ZYBwcCyTaMgAl)

</br>

_______________

## Setup
There are 2 common ways to add React to a new project:
1. Using [React toolchains](https://reactjs.org/docs/create-a-new-react-app.html), e.g. [Create React App](https://reactjs.org/docs/create-a-new-react-app.html#create-react-app) (see below) - suitable for developing production-ready apps.
2. With [React's CDN links](https://reactjs.org/docs/cdn-links.html) - can be convenient for quick experiments or demos.

#### Create React App
- To create a project, run `npx create-react-app my-app`
- This sets up your development environment with tools like *Babel* (to compile JSX to JavaScript), *Webpack* (to process and bundle your JS files and project assetts) and *Jest* (JS testing framework).
- It also provides helpful runtime errors in the browser.
- It sets you up with a few starting commands for your project:
  - `npm start` - starts the development server
  - `npm run build` - bundles the app into static files for production
  - `npm test` - starts the test runner
  - `npm eject` - removes the single build dependency on `react-scripts` which wraps all the default build configurations, therefore allowing you to customise your own build setup (Babel, Webpack, ESLint...) - *this cannot be undone!*

###### PWA by default
`create-react-app` sets up a **progressive web app** by default. PWAs rely on special scripts called *service workers* to give users that app-like experience. This caches assets locally, allowing your app to be performant even on slower, unreliable networks. Another key feature of PWAs is the web app manifest (`manifest.json`) - a json file containing metadata associated with your app, the main purpose of which is to install the app to the home screen of the device, for quicker access / richer experience.

#### Why 2 separate libraries?
:bulb: When building web applications in React, you use two libraries: `React` and `ReactDom`:
- React started out as a library for building interfaces in the browser, but the patterns and tools it provided proved so useful that it has since been extended to native application development.
- When React Native came along, `React` (as the core library), and `ReactDom` (for web app development) were split into two libraries.

#### Bonus: React Bootstrap
= a popular framework [for integrating Bootstrap with React apps](https://react-bootstrap.github.io/). To add it to your React project:
```npm
npm install --save react-bootstrap bootstrap
```
To add the Bootstrap styles to your project, add the following import to your `src/index.js` or `App.js` file:
```js
import 'bootstrap/dist/css/bootstrap.min.css';
```
And to use Bootstrap components in a React component:
```js
import { Container, Jumbotron } from 'react-bootstrap';
```

</br>

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

- The first part of a JSX tag determines the type of the React element. Capitalized types indicate that the JSX tag is referring to a React component (see [next section]((#paw_prints-components))).

- JSX allows embedding JavaScript expressions within it, written inside curly braces. This allows making your JSX dynamic.

- No `"..."` needed in the `<h1>`'s attribute when using a JSX expression

- JSX attributes aren't always like for like; e.g. to set classes, use JSX attribute `className` (this is due to `class` being a reserved word in JS)

- JSX comments are in curly braces too, combined with `/*...*/` - this applies to both inline and multi-line comments. `{/* this is a comment */}`

</br>

### :paw_prints: Iteration in Rendering
You can use any common [iteration methods](/notes/Javascript-Syntax.md#loops--iteration-methods) to generate [lists of elements](https://reactjs.org/docs/lists-and-keys.html) in React:

```js
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);
```

#### Keys
:warning: The above example would create a React console warning, as the `<li>` elements created with an iteration method haven't been given a unique key.

> :bulb: **Pass a key prop to a component any time you are creating elements by iterating over an array of items!**

React manages what gets rendered to the DOM. In order for this process to be fast and efficient, React needs a way to quickly know which items were changed, added, or removed. For this, React gives elements a special built-in prop named `key` - a unique identifier for an element in a list. [The React docs on keys](https://reactjs.org/docs/lists-and-keys.html#keys) recommend this should be a string.

> React does not recommend using `index` for unique keys, because the `index` might not always uniquely identify elements. It's usually best to use a unique id.

##### Updated example using keys
```js
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

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
        <Player name={player.name} score={player.score} key={player.id.toString()} />
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


</br>

### :paw_prints: State
#### Props vs State
There are 2 ways data gets handled in React components: props & state. Both props and state changes trigger a *render update*. However:
- Since props are immutable, *if a component needs to alter one of its attributes at some point in time, that attribute should be part of its STATE, otherwise it should just be a PROP for that component.*
- A component cannot change its own props, but it is responsible for putting together the props of its child components.
- The state starts with a default value when a component mounts, and then gets mutated (typically in response to user events).
- A component manages its own state internally, but (besides setting an initial state) has no business fiddling with the state of its children. You could say the state is *private*, or encapsulated.
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

> :zap: Be aware that `this.props` and `this.state` may be updated asynchronously, so relying on their values for calculating the next state, as in the above example, isn't best practice and can lead to race conditions. [See docs](https://reactjs.org/docs/state-and-lifecycle.html#state-updates-may-be-asynchronous) for more detail, but in short, the above usage of `setState()` should be reserved for setting state that isn't dependent on previous state, and where previous state is involved, use an alternative signature of `setState()` instead, which accepts a callback function that produces state based on the previous state in a more reliable way:

```js
this.setState( prevState => ({
  score: prevState.score + 1
}));
```

> :fire: **Likewise, avoid mutating `prevState`!**

:x: Avoid doing things like:
```js
this.setState( prevState => ({
  score: prevState.players[index].score += delta
}));
```

:heavy_check_mark: Instead, do this:
```js
this.setState( prevState => {
  // using spread operator to make a new copy, independent of the old objects
  const updatedPlayers = [ ...prevState.players ];
  const updatedPlayer = { ...updatedPlayers[index] };

  // Update the target player's score
  updatedPlayer.score += delta;
  updatedPlayers[index] = updatedPlayer;

  return {
    players: updatedPlayers
  };
});
```

</br>

### :paw_prints: Handling events
[React docs on Handling Events](https://reactjs.org/docs/handling-events.html) | [Passing arguments to Event Handlers](https://reactjs.org/docs/handling-events.html#passing-arguments-to-event-handlers)

In class components, a common pattern is to create event handlers as a method on the class - see `incrementScore()` and `decrementScore()` methods in the example below. This is then hooked up with [React's built-in events](https://reactjs.org/docs/events.html#supported-events), e.g. `onClick` - which are defined inline in the JSX template, and take a reference to the event handler they should call.

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

#### A note on method binding and `this` in React components
> :zap: When you create a class component that extends `React.Component`, any custom methods you create are not bound to the component by default. You need to bind your custom methods, so that `this` refers to the component instance. There are several ways to do this, including:
- call `bind()` in the `render()` method where the React event is set up, e.g. `onClick={this.incrementScore.bind(this)}`
- pass an arrow function to the React event, e.g. `onClick={() => this.incrementScore}` (may cause performance issues in some cases, as a different callback is created each time the component renders - see [docs](https://reactjs.org/docs/handling-events.html) for more details)
- define the event handler method itself as an arrow function (`incrementScore = () => {...}` - as used in above example), or bind the event handler in the constructor (`constructor() { this.incrementScore = this.incrementScore.bind(this); }`) - both of these approaches enable you to just reference `this` in the event: `onClick={this.incrementScore}`

(For more context on this, see notes on [`this` in JavaScript](/JavaScript-Quirks.md#this-in-javascript), and [this article](https://www.freecodecamp.org/news/this-is-why-we-need-to-bind-event-handlers-in-class-components-in-react-f7ea1a6f93eb/) focusing specifically on React class components.)

</br>

### :paw_prints: Forms
[Form elements in React](https://reactjs.org/docs/forms.html) work differently from other elements, because form elements naturally keep some internal state. For example, `<input>`, `<textarea>` and `<select>` elements in HTML are typically considered stateful, and maintain their own state based on user input. 

In React, a form element's state needs to be handled explicitely:
- The React component that renders a form also controls what happens in that form on subsequent user input.
- Mutable state is typically kept in the [state](#paw_prints-state) property of components, and only updated with [`setState()`](#the-setstate-method).

:point_right: A React component that controls an input form element's state in this way is called a **“Controlled Component”**.

Creating a controlled component usually involves the following:
1. initialise state for the value of the input
2. listen for changes on the input to detect when value is updated
3. create event handler that updates the value state

```js
class AddPlayerForm extends Component {
  state = {
    value: ''  // initialise state for the value of the input
  };

  // event handler that updates the value state
  handleValueChanged = (e) => {
    this.setState({ value: e.target.value });
  }

  render() {
    return (
      <form>
        <input
          type="text"
          value={this.state.value}            // use state for value of the input
          onChange={this.handleValueChanged}  // listen for changes on the input to detect when value is updated
          placeholder="Enter a player's name"
        />
        <input
          type="submit"
          value="Add Player"
        />
      </form>
    );
  }   
}
```

**Things to note:**
- Since the `value` attribute is set on our form element, the displayed value will always be `this.state.value`, making the React state the **source of truth**.
- `onChange` gets triggered immediately after each change / keystroke.
- The DOM event `e` passed to the event handler is in fact a normalised event created by React. React uses a cross-browser wrapper around the browser's native event called [**'synthetic event'**](https://reactjs.org/docs/events.html), so that cross-browser differences of DOM events won't get in our way.
- JSX requires a **closing tag** on `<input>` elements (omitting this results in a syntax error).

For details on **how other input elements differ between HTML and React**, see the React docs on [`<textarea>`](https://reactjs.org/docs/forms.html#the-textarea-tag) and [`<select>`](https://reactjs.org/docs/forms.html#the-textarea-tag).

> :fire: **[Controlled vs uncontrolled components](https://reactjs.org/docs/glossary.html#controlled-vs-uncontrolled-components):** it is possible to use [uncontrolled components](https://reactjs.org/docs/uncontrolled-components.html) in React, but most of the time controlled components are preferable. [File inputs](https://reactjs.org/docs/glossary.html#controlled-vs-uncontrolled-components) are a noteworthy exception.

</br>

_______________

## React Components in Depth

### :paw_prints: Unidirectional Data Flow 
#### Application state vs. Component state
1. **Application State** (global) - Main state; data that is available to the entire application (Flux or a flux-like library like [Redux](/notes/Redux.md), use what they call "stores" to hold application state. That means any component, anywhere in the app can access it so long as they hook into it.)

2. **Component State** (local) - State that is specific to a component and not shared outside of that component. As such, it can only be updated within that component and passed down to its children via props.

#### Data flows down
> :bulb: In React, data naturally flows *down* the component tree, from the app's top-level component down to the child components, via props. This is called **"unidirectional data flow"**.

> :bulb: When two or more components need access to the same state, we move the state into their common parent. This is called **["lifting state up"](https://reactjs.org/docs/lifting-state-up.html)**.

But if we lift state up, and if data flows down, how can a child component communicate information back up to its ancestors? <br/>
:point_right: Instead of passing state to a component, a parent can pass down **[a callback function](https://medium.com/@thejasonfile/callback-functions-in-react-e822ebede766)** that can allow children to communicate events and changes upwards - meanwhile data can continue to flow down!

</br>

### :paw_prints: Lifecycle Methods

- **Mounting** refers to the moment a React component is rendered to the DOM for the first time. The `render()` method is called just before this (so React can determine what should be displayed on the screen). The lifecycle method which runs straight after this first render is [`componentDidMount() {...}`](https://reactjs.org/docs/react-component.html#componentdidmount).

- Whenever the **component updates** e.g. due to `setState()` being called, the `render()` is called again (= the component is re-rendered).

- **Unmounting** refers to the moment the component is removed from the DOM - and the lifecycle method [`componentWillUnmount() {...}`](https://reactjs.org/docs/react-component.html#componentwillunmount) runs straight after this, and is useful for running any teardown to free up resources and help prevent memory leaks in your application.

```js
componentDidMount() {
    this.intervalId = setInterval(() => this.tick(), 100);
}

componentWillUnmount() {
    clearInterval(this.intervalId);
}
```

</br>

### :paw_prints: Advanced props
#### 1. DESTRUCTURING PROPS
[Destructuring](/notes/Javascript-Syntax.md#destructuring) provides a more concise way to write your props, and can make components cleaner and easier to understand as you don't have to repeat `props.` everywhere. Instead of doing this:

```js
const MyComponent = (props) => {
  return (
    <div>
      <h1>{props.title}</h1>
      <ChildComponent name={props.childName} />
      <button onClick={() => props.doSomething()}>Click me!</button>
    </header>
  );
};
```

...in a **function component** you can do:

```js
const MyComponent = ({ title, childName, doSomething }) => {
  return (
    <div>
      <h1>{title}</h1>
      <ChildComponent name={childName} />
      <button onClick={() => doSomething()}>Click me!</button>
    </header>
  );
};
```

For **class components**, you have to explicitely assign the destructure like this:

```js
class MyComponent extends Component {
  render() {
    const { title, childName, doSomething } = this.props;
    return (
      <div>
        <h1>{title}</h1>
        <ChildComponent name={childName} />
        <button onClick={() => doSomething()}>Click me!</button>
      </header>
    );
  }
}
```

#### 2. VALIDATE PROPS WITH PROPTYPES
As your app grows, it's a good practice to "type check" or validate the data a component receives from props. There are **3 popular ways** to handle type checking in React: **[PropTypes](https://www.npmjs.com/package/prop-types)**, **[TypeScript](https://www.typescriptlang.org/)** and **[Flow](https://flow.org/)**.

- Proptypes used to be built into React, but is now separate library; cf. [React docs on using PropTypes](https://reactjs.org/docs/typechecking-with-proptypes.html)
- PropTypes provide helpful warnings at runtime if the type passed to a prop doesn't match its defined type. This not only helps you catch and avoid bugs, but PropTypes also serve as documentation for components.
- For performance reasons, PropTypes are only checked in development mode.

> :bulb: **Static type checkers like Flow and TypeScript** identify certain types of problems before you even run your code. They can also improve developer workflow by adding features like auto-completion. For this reason, [React recommends](https://reactjs.org/docs/static-type-checking.html) using Flow or TypeScript instead of PropTypes for larger code bases. (See also: docs on [using TypeScript with React](https://reactjs.org/docs/static-type-checking.html#typescript))

##### Using PropTypes
To run type checking on a component, you assign it the `propTypes` property. For a function component: `MyComponent.propTypes = {...};` - the `propTypes` object describes the props being passed to the component, and defines what type they should be using one of the [available `PropTypes` validators](https://reactjs.org/docs/typechecking-with-proptypes.html#proptypes):

```js
import React from 'react';
import PropTypes from 'prop-types';

const MyComponent = ({ players, title, score, changeScore }) => {
  return (
    // some JSX
  );
};

MyComponent.propTypes = {
  players: PropTypes.arrayOf(PropTypes.object),
  title: PropTypes.string
  score: PropTypes.number,
  changeScore: PropTypes.func
};
```

You can define key properties of an object passed as a prop even more specifically, by using `PropTypes.shape()` instead of `PropTypes.object`:

```js
MyComponent.propTypes = {
  players: PropTypes.arrayOf(PropTypes.shape({
        score: PropTypes.number
    })),
  ...
};
```

Defining `propTypes` in this way (outside the component itself) works for **class components** too. But a commonly used alternative is to define the types at the top of the class, with an assigment to `static propTypes`:

```js
import React, { Component } from 'react';
import PropTypes from 'prop-types';

class MyComponent extends Component {
  static propTypes = {
    players: PropTypes.arrayOf(PropTypes.object),
    title: PropTypes.string
    score: PropTypes.number,
    changeScore: PropTypes.func
  };
  
  render() {
    return (
      // some JSX
    );
  }
};
```

To **mark a prop as required**, simply add `.isRequired` to the validator:

```js
MyComponent.propTypes = {
  players: PropTypes.arrayOf(PropTypes.object).isRequired,
  ...
};
```

You can also define **[default values](https://reactjs.org/docs/typechecking-with-proptypes.html#default-prop-values) for props**, by assigning to the special `defaultProps` property:

```js
MyComponent.defaultProps = {
  title: 'Scoreboard'
}
```

</br>

### :paw_prints: PureComponent
React provides a special type of component, called [`PureComponent`](https://reactjs.org/docs/react-api.html#reactpurecomponent), that helps prevent unnecessary re-renders. If your component’s `render()` method renders the same result given the same props and state, you can use `PureComponent` for a performance boost in some cases.

`PureComponent` implements the lifecycle method [`shouldComponentUpdate()`](https://reactjs.org/docs/react-component.html#shouldcomponentupdate), which does a shallow prop and state comparison and only calls `render()` when it detects changes.

```js
import React, { PureComponent } from 'react';

class Player extends PureComponent {
  render() {
    return (
      // JSX for this component
    );
  }
}
```

#### When to use it
> :warning: **A `PureComponent` should only contain child components that are also `PureComponents`.**

Use `PureComponent` when you have performance issues and have determined that a specific component is rerendering too often.

Further reading: [Using a <PureComponent/> in React (by Chris Burgin)](https://medium.com/front-end-weekly/using-a-purecomponent-in-reacts-262972f9f1e0)

</br>

### :paw_prints: Refs
In React, you typically do not target elements directly and modify them as you would when working in [JavaScript with the DOM](/notes/Javascript-and-the-DOM.md).

There may however be times when you need to target elements outside the normal React data flow: [**React Refs**](https://reactjs.org/docs/refs-and-the-dom.html) let you access and interact with DOM nodes created in the `render()` method, and make it possible to do the more traditional DOM manipulation.

They're commonly used to access form elements and get their values, which avoids having to use [controlled components for a form in React](#paw_prints-forms).

#### To use a Ref:
1. Create a Ref using `React.createRef()` method
2. Attach the Ref to a React element via the `ref` attribute

> :zap: **Use refs sparingly, as they go against the intended React data flow and can comprise an antipattern.**

</br>

_______________

## React Context API
### :paw_prints: Background: Prop drilling
In the [typical React data flow](#paw_prints-unidirectional-data-flow), components communicate with each other via [props](#paw_prints-props). A parent passes props down to child components. Sometimes the intermediary components get props passed to them *with the sole purpose of passing that data down one (or several) more levels*. This cascade of props is often referred to as ["prop drilling"](https://kentcdodds.com/blog/prop-drilling).

:point_right: **The React [Context API](https://reactjs.org/docs/context.html) provides a way to pass data to components without having to pass props manually at every single level.**

> Prior to Context being a stable feature in React, developers would use state management libraries like [MobX](https://mobx.js.org/README.html) and [Redux](/notes/Redux.md) instead.

</br>

### :paw_prints: Using Context
#### To use or not to use Context?

:point_right: Context is mainly used when certain data needs to be accessed by many components at different nesting levels.

#### 3 parts of the Context API
1. **`React.createContext()`** - sets up a context and returns an object with a *Provider* and *Consumer* (the two main components of the context API)
2. **Provider** - a single Provider component, used as high as possible in the component tree, which allows Consumer components to subscribe to context changes
3. **Consumer(s)** - access the Provider to get any data they need - thus avoiding "prop drilling"

> :bulb: The communication between the Provider and Consumers is what makes Context work.

#### Example
First, set up context in file `src\components\Context\index.js`:
```js
import React from React;

const MyAppContext = React.createContext();

export const Provider = MyAppContext.Provider;
export const Consumer = MyAppContext.Consumer;
```

Next, set up Provider in `src\components\App.js`:
- to provide the context to all children of `App`, wrap all the JSX returned in `<Provider>` tags
- this Provider component provides the data that needs to be shared in the component tree
- the Provider component requires a `value` prop to share data (usually the application state, and any actions / event handlers shared between components) - any descendent component will have access to this
```js
import React from 'react';
import { Provider } from './Context';

class App extends Component {
  ...
  
  render() {
    return (
      <Provider value={this.state.importantThing}>
        <div className="main">
          <ChildComp1 />  // which contains a <GrandChildComp /> that needs to access importantThing
          <ChildComp2 />
          <ChildComp3 />          
        </div>
      </Provider>
    );
  }
```

Finally, set up Consumers that will subscribe to the Provider in order to make use of Context;  in `src\components\GrandChildComp.js`:
- move all JSX into the [**render prop**](https://reactjs.org/docs/render-props.html) of the `<Consumer>` component
- `context` (sometimes named `value` instead) is equal to the `value` prop set on the Provider! (In our case, `importantThing`.)

> :bulb: [**Render props**](https://reactjs.org/docs/render-props.html) is a pattern/technique in React for sharing code between components, by using a prop whose value is a function that returns a React element. It is also sometimes called 'function as a child', because you can also write the function in between the opening and closing tags of the component.

```js
import React from 'react';
import { Consumer } from './Context';

const Stats = () => {
  return (
    <Consumer>
      { context => {
        const foo = context.something;
        const bar = context.somethingElse;

        return (
          <table>
            <tbody>
              <tr>
                <td>Cool:</td>
                <td>{ foo }</td>
              </tr>
              <tr>
                <td>Lovely:</td>
                <td>{ bar }</td>
              </tr>
            </tbody>
          </table>
        )
      }}
    </Consumer>
  ); 
}
```

:point_right: All this allows the parent component (`ChildComp1`) to not have to worry about `importantThing` data, and be a much simpler, stateless component instead.

#### Partially wrapping JSX in Consumer
The `Consumer` **doesn't have to wrap all of the JSX** - you can wrap it around just the parts of the UI that need to consume the `context`:

```js
render() {
    ...

    return (
      <div className="player">
        <Consumer>
          { context => (
            <span className="player-name">
              <button className="remove-player" onClick={() => context.actions.removePlayer(id)}>✖</button>
              { name }
            </span> 
          )}
        </Consumer>
        <Counter 
          score={score}
          index={index}
        />
      </div>
    );
  }
```

#### Passing more complex context
It's common to pass the `Provider`'s `value` prop an object to store multiple properties in application state, as well as any callback functions, i.e. *actions* you want to perform on the data which need to be triggered in other components.

```js
render() {
  return (
    <Provider value={{
      players: this.state.players,
      actions: {
        changeScore: this.handleScoreChange,
        removePlayer: this.handleRemovePlayer,
        addPlayer: this.handleAddPlayer
      }
    }}>
      <div className="scoreboard">
        <Header />
        <PlayerList />   
        <AddPlayerForm />
      </div>
    </Provider>
  );
}
```


