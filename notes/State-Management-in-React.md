# State Management in React
In which we cover: [React Context API](#react-context-api) and [Redux](#redux)
Sources: Team Treehouse React/Redux courses

_______________________________
## React Context API 
  - [Background: Prop drilling](#background-prop-drilling)
  - [Using Context](#using-context)

### Background: Prop drilling
In the [typical React data flow](#paw_prints-unidirectional-data-flow), components communicate with each other via [props](#paw_prints-props). A parent passes props down to child components. Sometimes the intermediary components get props passed to them *with the sole purpose of passing that data down one (or several) more levels*. This cascade of props is often referred to as ["prop drilling"](https://kentcdodds.com/blog/prop-drilling).

:point_right: **The React [Context API](https://reactjs.org/docs/context.html) provides a way to pass data to components without having to pass props manually at every single level.**

> Prior to Context being a stable feature in React, developers would use state management libraries like [MobX](https://mobx.js.org/README.html) and [Redux](/notes/Redux.md) instead.


### Using Context
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

_______________________________

## Redux
### Intro
[Redux](https://redux.js.org/) is a popular JavaScript framework for managing and maintaining application state in a scaleable, predictable and testable way. It is often used with React, although it can be used with other frameworks too.

*Redux provides a single source of truth for your app, making it easier to keep application state in sync and distribute data.* -
This is achieved by keeping application state in a single container (and following a number of design patterns and [key principles](https://redux.js.org/introduction/three-principles)). It also offers data governance / data tracking and makes data universally accessible to all parts of your application.

#### Redux Terms
- **Store:** Refers to the application state container for the entire application
- **Action:** Refers to an explicit event that occurs within a Redux application that will impact application state
- **Container component:** A React component that usually defines no markup of its own but is responsible for propagating data to other React components known as *presentational components* (see next points). It typically sits at the top of the React component tree and subscribes to specific Reducer updates.
- **Logical Component:** Presentational component that has its own state to manage and may or may not make use of React lifecycle events
- **Pure Component:** Presentation component that is implemented as a pure function. These components are passed props and return markup with no side-effects. That means they do not manage a state of their own and do not take part in React lifecycle events.
- **[React-Redux](https://react-redux.js.org/):** A library that simplifies the amount of boiler plate code needed to use Redux in React apps 

#### When To Use Redux?
Redux adds substantial overhead to your projects and, as an opininated framework, expects you to follow some very explicit patterns. This can benefit developers as consistent patterns make debugging / testing applications easier and, once familiar with Redux, it will be easy to understand the structure of other apps using it.

Whilst it offers clear separation of application responsibilities, for smaller or more straightforward applications, Redux is in most cases overkill. 

See also: ["You Might Not Need Redux" by Dan Abramov](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367)
