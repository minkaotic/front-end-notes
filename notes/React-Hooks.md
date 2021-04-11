# React Hooks
Notes based on [Treehouse React Hooks workshop](https://teamtreehouse.com/library/react-hooks) and [Pluralsight 'Using React Hooks' course](https://app.pluralsight.com/library/courses/using-react-hooks/table-of-contents)

**Jump to: [`useState`](#usestate) | [`useEffect`](#useeffect) | [`useContext`](#usecontext) | [`useRef`](#useref)**

## Intro
- Prior to hooks, React allowed developers to [create/manage state](React-Notes.md#paw_prints-state) and use [lifecycle methods](React-Notes.md#paw_prints-lifecycle-methods), but this required writing the component as a _class_ component, which has a number of drawbacks compared to function components:
  - require additional syntax (which can feel noisy) & learning/understanding classes in JS
  - optimising classes for minification can be slower
  - class components can interfere with some React tools/features, for example hot reloading
- Additionally, attaching reusable logic to a component also required understanding trickier concepts, such as using [_render props_](https://reactjs.org/docs/render-props.html) or [_higher order components (HOC)_](https://reactjs.org/docs/higher-order-components.html).


**👉 [React Hooks](https://reactjs.org/docs/hooks-intro.html) are special, built-in functions, that allow you to replicate these capabilities with a cleaner and more straightforward syntax.** They:
- manage state (+ rendering of UI when state changes)
- provide easier access to your React app's context
- update components with an alternative to lifecycle methods
- offer a mechanism to extract code that can be reused between components
- work in function components only (can't be used in class components)


## `useState`
- adds React state to function components
- equivalent of both `this.state` and `this.setState(`) in class components

### Using it
```js
// import useState from React
import React, { useState } from 'react';

function App() {
  // declare a state variable named score by calling useState()
  const [ score, setScore ] = useState(0);
  ...
}
```
- [`useState()`](https://reactjs.org/docs/hooks-reference.html#usestate) accepts one optional argument – the initial value of the state variable
- calling `useState()` with the initial state returns an array with two values:
  - a variable with the current state value (0 in this case) - similar to `this.state`
  - a function to update that value - similar to `this.setState()`
- 👍 The variable `score` now holds the current state, and you can use that value in your component as you would any variable.

### Updating state
To update the `score` state, call `setScore()` and pass it the new state:
```js
function App() {
  const [score, setScore] = useState(0);

  return (
    <div className="App">
      <header className="App-header">
        <h1>{ score }</h1>
        <button onClick={() => setScore(100)}> // update the score state
          Score 100!
        </button>
      </header>
    </div>
  );
}
```

To **update state *based on the previous state*** value, pass a function to the method updating state. The function receives the previous state value and uses it to return the updated value:
```js
<button onClick={() => setScore(prevScore => prevScore + 1)}>
  Increase score by 1
</button>
```

### Multiple state variables
- you can call `useState()` numerous times to declare multiple state variables

> It is [recommended practice](https://reactjs.org/docs/hooks-faq.html#should-i-use-one-or-many-state-variables) to call `useState()` for each state variable that your component needs, rather than calling it once to initialise an object containing all the state properties.


## `useEffect`
- The code that is run via a component's lifecycle methods is sometimes referred to as "side effects"
- The [`useEffect`](https://reactjs.org/docs/hooks-reference.html#useeffect) hook lets you perform side effects in function components, giving them access to common lifecycle events. This allows us to do things after the component renders or after the component unmounts.

### Using it
```js
// import useEffect from React
import React, { useState, useEffect } from 'react';

function App() {
  const [score, setScore] = useState(0);
  const [message] = useState('Welcome!');

  // Define the useEffect() hook
  // The effect happens after render
  useEffect(() => {
    console.log('useEffect called!');   
  });

  return (...);
}
```
- `useEffect()` receives a callback function as the first argument, which is where you perform any side effects
- the provided callback function is called when the component first renders and after each subsequent re-render / update
- `useEffect()` takes an optional array as a 2nd argument which specifies any dependencies for the effect - typically state variables that are used or updated inside `useEffect()`. The array instructs the `useEffect()` hook to **run only if one of its dependencies changes**, which can help prevent performance issues:

```js
// example with dependencies
function App() {
  const [score, setScore] = useState(0);
  const [message] = useState('Welcome!');

  // The effect happens whenever message or score change
  useEffect(() => {
    document.title = `${message}. Your score is ${score}`;
  }, [message, score]);

  return (...);
}
```

- passing an *empty array* as the second argument will run `useEffect()` only *once* after the initial render - useful e.g. for inital data fetching, similar to when you would use `componentDidMount`.

```js
function App() {
  const [data, setData] = useState('');

  useEffect(() => {
    fetch('https://dog.ceo/api/breeds/image/random')
      .then(response => response.json())
      .then(content => setData(content.message))
      .catch(err => console.log('Oh noes!', err))
  }, []);

  return (
    <div className="App">
      <img src={data} alt="A random dog breed" />
    </div>
  );
}
```

- With hooks, you don't need a separate function (akin to `componentWillUnmount()`) to perform **cleanup**. Returning a function from your effect [takes care of the cleanup, running the function when the component unmounts](https://reactjs.org/docs/hooks-effect.html#effects-with-cleanup).
- **Multiple effects to separate concerns:** 

https://reactjs.org/docs/hooks-effect.html#effects-with-cleanup


## `useContext`



## `useRef`
- allows us to access an element in the DOM directly
- **ideally avoid direct access and use the flow of state/props to manage values being passed between components** - but sometimes this may not be possible
