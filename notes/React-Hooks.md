# React Hooks
Notes based on [Treehouse React Hooks workshop](https://teamtreehouse.com/library/react-hooks) and [Pluralsight 'Using React Hooks' course](https://app.pluralsight.com/library/courses/using-react-hooks/table-of-contents)

**Jump to: [`useState`](#usestate) | [`useEffect`](#usestate) | [`useContext`](#usecontext)**

## Intro
- Prior to hooks, React allowed developers to create and manage state based on [lifecycle methods](/React-Notes.md#paw_prints-lifecycle-methods), but this required writing the component as a _class_ component, which has a number of drawbacks compared to function components:
  - require additional syntax (which can feel noisy) & learning/understanding classes in JS
  - optimising classes for minification can be slower
  - class components can interfere with some React tools/features, for example hot reloading
- Additionally, there were ways of attaching reusable logic to a component, but this either required using [_render props_](https://reactjs.org/docs/render-props.html) or [_higher order components (HOC)_](https://reactjs.org/docs/higher-order-components.html).


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
- you can call `useState()` numerous times to declare multiple state variables 

> 👍 The variable `score` now holds the current state, and you can use that value in your component as you would any variable.

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

To **update state based on the previous state** value, pass a function to the method updating state. The function receives the previous state value and uses it to return the updated value:
```js
<button onClick={() => setScore(prevScore => prevScore + 1)}>
  Increase score by 1
</button>
```



## `useEffect`


## `useContext`
