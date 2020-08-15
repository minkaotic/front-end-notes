# React Router
> *Notes largely based on [React Router course on Treehouse](https://teamtreehouse.com/library/react-router-4-basics-2), but updated to match the latest recommended syntax for React Router.*

[React Router](https://reactrouter.com/web/guides/quick-start) is a declarative routing solution for React, to manage navigation and rendering of components in your applications.
- Allows matching a URL to the set of components being rendered
- Dynamically loads and unloads components to changes what's displayed in the browser as users navigate an app, all without reloading the page

## Contents
- [Setup](#paw_prints-setup)
- [Links & NavLinks](#paw_prints-links--navlinks)
- [Match & Redirect](#paw_prints-match--redirect)
- [Switch](#paw_prints-switch)
- [URL Parameters](#paw_prints-url-parameters)

____________
### Basic concepts
> **Single-page app (SPA) recap:** HTML, CSS and JS are only loaded once by the browser, and content changes dynamically as user interacts with the app. The app itself never reloads, unless manually refreshed by the user.

> **A good routing solution** should *keep track of browser history* - so users can use the browsers back/forth buttons to navigate - and seamlessly *link users to specific sections of your app* - so users can bookmark specific sections. React Router allows for this.
____________


## :paw_prints: Setup
```
$ npm install --save react-router-dom
```
React Router lets you declare routes from anywhere in your component tree, but is commonly used inside the root app component. It uses JSX syntax to declare routes and provides 2 core components:
- [**`<BrowserRouter />`**](https://reactrouter.com/web/api/BrowserRouter) - Route routing component that keeps your UI in sync with the URL; it wraps all your app components - and renders the root router that listens for URL changes and provides other React Router components information about the current URL and which components to render
- [**`<Route />`**](https://reactrouter.com/web/api/Route) - responsible for rendering a component in your app when the URL matches its path; create a route by specifying the path and the component you want to render for that path
  - Use the [`exact`](https://reactrouter.com/web/api/Route/exact-bool) property on a route to only render the component when the path matches exactly (i.e. not just partial match)

```js
import React from 'react';
import { BrowserRouter, Route } from 'react-router-dom';
// etc.

export const App = () => (
  <BrowserRouter>
    <div className="container">
      <Header />
      <Route exact path="/">
          <Home />
        </Route>
        <Route path="/about" >
          <About />
        </Route>
        <Route path="/teachers">
          <Teachers />
        </Route>
        <Route path="/courses">
          <Courses />
        </Route>
    </div>
  </BrowserRouter>
);
```

## :paw_prints: Links & NavLinks
- with React Router, you don't use regular `<a>` tags to link to the routes in your app
- [**`<Link />`**](https://reactrouter.com/web/api/Link) renders fully accessible anchor tags and will load the component without a page refresh

```js
import React from 'react';
import { Link } from 'react-router-dom';

const Header = () => (
  <header>
    <span className="icn-logo"><i className="material-icons">code</i></span>
    <ul className="main-nav">
      <li><Link to="/">Home</Link></li>
      <li><Link to="/about">About</Link></li>
      <li><Link to="/teachers">Teachers</Link></li>
      <li><Link to="/courses">Courses</Link></li>
    </ul>    
  </header>
);
```

- The [**`<NavLink>`**](https://reactrouter.com/web/api/NavLink) component is a special version of `<Link>` that can recognize when it matches the current URL, and will give those links a default class of `active`.
  ```js
  <li><NavLink to="/courses">Courses</NavLink></li>
  ```
- Use the `exact` prop to only make the link appear active only if it matches exactly:
  ```js
  <li><NavLink exact to="/">Home</NavLink></li>
  ```
- Alternatively to using the default `active` class, assign a custom class with the `activeClassName` prop, or define active styles inline with the `activeStyle` prop:
  ```js
  <li><NavLink to="/about" activeClassName="selected">About</NavLink></li>
  <li><NavLink to="/teachers" activeStyle={{ background: "tomato" }}>Teachers</NavLink></li>
  ```
  
## :paw_prints: Match & Redirect
- React Router provides a [**`<Redirect>`**](https://reactrouter.com/web/api/Redirect) component that redirects from one route to another

- The [**`match` object**](https://reactrouter.com/web/api/match) can be accessed from inside components being rendered by `<Route>`, and contains information about how a route is matching the URL. This can be used to dynamically match `<Route>` and `<NavLink>` to the current URL and path, and is particularly useful for [nested routing](https://reactrouter.com/web/guides/quick-start/2nd-example-nested-routing).

**Example:** Using `match` and `<Redirect>` in a lower level component in the routing tree:
```js
import { Route, Redirect, useRouteMatch } from 'react-router-dom';
// etc.

const Courses = () => {
  // one way of accessing match is via the useRouteMatch hook
  let match = useRouteMatch();

  return (<div className="main-content courses">
    <SubHeader />
    <Route exact path={match.path}>
      <Redirect to={`${match.url}/html`} />
    </Route>
    <Route path={`${match.url}/html`}>
      <HTML />
    </Route>
    <Route path={`${match.url}/css`}>
      <CSS />
    </Route>
    <Route path={`${match.url}/javascript`}>
      <JavaScript />
    </Route>
  </div>)
};
```
- This provides sub-routing for the path associated with `Courses`, and sets one of its children as the default via the redirect, to ensure that some content is rendered when the user navigates to `/courses`
- As the `Courses` component has been associated with the `/courses` path, its children are navigable via `/courses/html`, `/courses/css` etc.

## :paw_prints: Switch
- [**`<Switch>`**](https://reactrouter.com/web/api/Switch) can wrap your routes, and only renders the first route / redirect that matches the path.
- This allows us to include a **fallback route** at the bottom of the switch statement, i.e. to display 404 if none of our routes matched the requested URL

```js
<Switch>
  <Route exact path="/">
    <Home />
  </Route>
  ...
  <Route path="/courses">
    <Courses />
  </Route>
  <Route>
    <NotFound />
  </Route>
</Switch>
```

## :paw_prints: URL parameters
- Dynamic routes can be declared using special [**URL parameters**](https://reactrouter.com/web/example/url-params)
  - Use `:` to denote a parameter
  - To make a parameter optional, add a `?` to the end:
```js
<Route path="/teachers/:topic/:fname-:lname?">
  <Featured />
</Route>
```
- The data passed to the URL parameters can be accessed via `match.params` in the component rendered for that route; for example:
```js
import React from 'react';
import { useRouteMatch } from 'react-router-dom';

const Featured = () => {
  let match = useRouteMatch();
  let name = `${match.params.fname} ${match.params.lname}`;
  let topic = match.params.topic;

  return (
    <div className="main-content">
      <h2>{name}</h2>
      <p>Introducing <strong>{name}</strong>, a teacher who loves teaching courses about <strong>{topic}</strong>!</p>
    </div>
  );
}
```
- As with any other route, you can create Links or NavLinks that match URL parameterised routes:
```js
<Link to="teachers/Chicken/Roger-Cat">Roger the cat</Link>
```
