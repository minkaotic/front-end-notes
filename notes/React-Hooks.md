# React Hooks
Notes based on [Treehouse React Hooks workshop](https://teamtreehouse.com/library/react-hooks) and [Pluralsight 'Using React Hooks' course](https://app.pluralsight.com/library/courses/using-react-hooks/table-of-contents)

**Jump to: [`useState`](#usestate) | [`useEffect`](#useeffect) | [`useContext`](#usecontext) | [`useReducer`](#usereducer) | [`useRef`](#useref)**

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

To **update state for objects** (or arrays), you have to merge the state object using [spread syntax](/Javascript-Syntax.md#spread-operator--rest-parameters), for example given a state variable `cat` that is an object and is updated with `setCat`:
```js
onChange = {e => {
  setCat(prevCat => ({ ...prevCat, name: e.target.value }));
}}
```

> ⚠️ **NB!** When working with **nested objects** or multidimensional arrays, the spread syntax will create a shallow copy instead of a deep copy. Ideally avoid nested objects, but [refer to this guide for more information and workarounds](https://blog.logrocket.com/a-guide-to-usestate-in-react-ecb9952e406c/#howtoupdatestateinanestedobjectinreactwithhooks).


### Multiple state variables vs state grouped into objects
- `useState()` can be called numerous times to declare multiple state variables
- In general, it is [recommended practice](https://reactjs.org/docs/hooks-faq.html#should-i-use-one-or-many-state-variables) to call `useState()` for each state variable that your component needs, rather than calling it once to initialise an object containing all the state properties.
- But using an object makes sense for pieces of state that will likely *change together*. For things that change independently, use multiple state variables.


## `useEffect`
- The code that is run via a component's [lifecycle methods](React-Notes.md#paw_prints-lifecycle-methods) is sometimes referred to as "side effects"
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
- `useEffect()` receives a **callback function as the 1st argument**, which is where you perform any side effects
- `useEffect()` takes an **optional array as a 2nd argument** which specifies any dependencies for the effect - typically state variables that are used or updated inside `useEffect()`
  - When no dependency array is specified, the provided callback function will be called when the component first renders and after each subsequent re-render / update
  - When a dependency array is specified, the callback function is **run only if one of its dependencies changes**, which can help prevent performance issues:

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
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    fetch('https://dog.ceo/api/breeds/image/random')
      .then(response => response.json())
      .then(content => setData(content.message))
      .catch(err => console.log('Oh noes!', err))
      .finally(() => setIsLoading(false))  // ensure is loading is always set to false at the end, even if request fails
  }, []);

  return (
    <div className="App">
      <img src={data} alt="A random dog breed" />
    </div>
  );
}
```

- With hooks, you don't need a separate function (akin to `componentWillUnmount()`) to perform **cleanup**. *Returning a function* from within your your effect callback function [takes care of the cleanup, running the function when the component unmounts](https://reactjs.org/docs/hooks-effect.html#effects-with-cleanup):
```js
useEffect(() => {
  console.log("In use effect!");
  return () => {
    console.log("In use effect cleanup!");
  }
})
```


### Multiple effects to separate concerns
- You can call `useEffect()` multiple times, and it is best practice to use this [to separate unrelated logic into different effects](https://reactjs.org/docs/hooks-effect.html#tip-use-multiple-effects-to-separate-concerns) - something that wasn't possible with traditional lifecycle methods!
- React will apply every effect used by the component, in the order they were specified
- This allows us to group related bits of state + lifecycle logic as follows:

```js
function FriendStatusWithCounter(props) {
  // logic for 'count'
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  // logic for 'isOnline', incl. adding subscriptions that need to be cleaned when component unmounts
  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    function handleStatusChange(status) {
      setIsOnline(status.isOnline);
    }

    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });
  // ...
}
```


## `useContext`
> See [separate notes on *when* to use Context](State-Management-in-React.md#woman_teacher-when-to-use-it) for more background on this.

- The [`useConext` hook](https://reactjs.org/docs/hooks-reference.html#usecontext) provides the functionality of the Context API in a single function.

???
- Once you've created your app's Context, call useContext() inside a function component to access any Context state and actions


## `useReducer`
- an alternative to `useState`, which takes a reducer function and inital state value and returns an array that holds the current state value and a `dispatch` method:
  ```js
  const [state, dispatch] = useReducer(reducer, initialState);
  ```

- especially useful when you have complex state logic that uses multiple sub-values, or when a state depends on the previous one
- If your state values are linked and often depend on the other state values, create a reducer



## `useRef`
- allows us to access an element in the DOM directly
- **ideally avoid direct access and use the flow of state/props to manage values being passed between components** - but sometimes this may not be possible

### Using it
- initialise the ref object: `const imageRef = useRef(null);`
- mount the ref on any element: `ref={imageRef}`
- call the ref object's `current` property to interact with the mounted element: `imageRef.current.src = "/someImage.png"`

The below example shows a component that toggles an element from one image to another on mouseover/mouse out:
```js
import React, { useRef } from 'react';

export const ImageTogglerOnMouseOver = ({ primaryImg, secondaryImg }) => {
  const imageRef = useRef(null);

  return (
    <img
      onMouseOver={() => imageRef.current.src = secondaryImg}
      onMouseOut={() => imageRef.current.src = primaryImg}
      src={primaryImg}
      alt=""
      ref={imageRef}
    />
  );
};
```






