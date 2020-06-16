# Redux


## Intro
[Redux](https://redux.js.org/) is a popular JavaScript framework for managing and maintaining application state in a scaleable, predictable and testable way. It is often used with React, although it can be used with other frameworks too.

*Redux provides a single source of truth for your app, making it easier to keep application state in sync and distribute data.* -
This is achieved by keeping application state in a single container (and following a number of design patterns and [key principles](https://redux.js.org/introduction/three-principles)). It also offers data governance / data tracking and makes data universally accessible to all parts of your application.

### Redux Terms
- **Store:** Refers to the application state container for the entire application
- **Action:** Refers to an explicit event that occurs within a Redux application that will impact application state
- **Container component:** A React component that usually defines no markup of its own but is responsible for propagating data to other React components known as *presentational components* (see next points). It typically sits at the top of the React component tree and subscribes to specific Reducer updates.
- **Logical Component:** Presentational component that has its own state to manage and may or may not make use of React lifecycle events
- **Pure Component:** Presentation component that is implemented as a pure function. These components are passed props and return markup with no side-effects. That means they do not manage a state of their own and do not take part in React lifecycle events.
- **[React-Redux](https://react-redux.js.org/):** A library that simplifies the amount of boiler plate code needed to use Redux in React apps 

### When To Use Redux?
Redux adds substantial overhead to your projects and, as an opininated framework, expects you to follow some very explicit patterns. This can benefit developers as consistent patterns make debugging / testing applications easier and, once familiar with Redux, it will be easy to understand the structure of other apps using it.

Whilst it offers clear separation of application responsibilities, for smaller or more straightforward applications, Redux is in most cases overkill. 

See also: ["You Might Not Need Redux" by Dan Abramov](https://medium.com/@dan_abramov/you-might-not-need-redux-be46360cf367)
