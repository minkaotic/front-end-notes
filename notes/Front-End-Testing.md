# Front End Testing
## Contents
- [Overview](#overview)
- [Taking Screenshots with Selenium in .NET](#taking-screenshots-with-selenium-in-net)
- [Testing React Components](#testing-react-components)

____________________________________

# Overview
Sources: [Ham Vocke: The Practical Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html) | [Super high-level library overview on Treehouse](https://teamtreehouse.com/library/testing-javascript)

## Client-side rendered applications 
Modern **single page application frameworks** (React, Vue.js, Angular and the like) often come with their own tools and helpers that allow you to thoroughly test these interactions in a pretty low-level (unit test) fashion - see list below for a few libraries/frameworks.

Even if you roll your own frontend implementation using **vanilla JavaScript** you can use general purpose testing tools like Jasmine or Mocha.

* [Mocha](https://mochajs.org/) is one of the most used JS testing frameworks. It runs on Node as well as in the browser.
* [Jasmine](https://jasmine.github.io/), as well as being a general popular BDD-centric testing framework, is a particularly common choice for testing Angular applications.
* [Jest](https://jestjs.io/) is a JS test runner and assertion library created by Facebook and is setup automatically when creating a React app. It is built for unit- and integration testing, and can also be used with other client side frameworks, as well as Typescript or Node.
* [Enzyme](https://airbnb.io/enzyme/) is a JS testing utility library developed by AirBnB for testing React compontents; originally built for use with Mocha, but is also compatible with other testing libraries.

Additionally, [Karma](https://karma-runner.github.io/latest/index.html) is a test runner that aims to simplify the testing & debugging process.

## Server-side rendered applications 
With more traditional, server-side rendered applications, [Selenium](https://www.seleniumhq.org/)-based tests will be your best choice.

____________________________________

# Taking Screenshots with Selenium in .NET
Use the Selenium `ITakesScreenshot` interface:
```c#
private Image GetScreenshot(IWebDriver webDriver)
{
  var screenshot = ((ITakesScreenshot)webDriver).GetScreenshot().AsByteArray;
  using (var ms = new MemoryStream(screenshot))
  {
      var img = (Bitmap)Image.FromStream(ms);
      return img;
  }
}
```
For details on taking **full page** screenshots, see the [sample code here](https://github.com/minkaotic/code-quality-notes/blob/master/selenium-testing.md).

____________________________________

# Testing React Components
Sources: [Pluralsight Course](https://www.pluralsight.com/courses/testing-react-components) | [Enzyme vs react-testing-library](https://medium.com/@boyney123/my-experience-moving-from-enzyme-to-react-testing-library-5ac65d992ce) | [Tutorial](https://jestjs.io/docs/en/tutorial-react) | [Testing recipes](https://reactjs.org/docs/testing-recipes.html)
> :bulb: Test *logic* (behaviour), not implementation, to avoid brittle tests

## Setting up a test environment
- **`create-react-app`** will set up a test environment (using Jest and React Testing Library) out of the box, which can be run straightaway with `npm test`
- In order to test components *in isolation* from the rest of the application, you can use [Storybook](https://storybook.js.org/) ([setup instructions for React](https://www.learnstorybook.com/intro-to-storybook/react/en/get-started/)):
  - easier to mock hard to reach use cases, as we can render components in key states that are tricky to reproduce in an app
  - offers visual verification of each component in isolation

**What to test?** - React ultimately has two responsibilities:
1. render user interfaces based on some state
2. produce and manage user interface events

:point_right: These are the responsibilies we want to test in our components!


## Testing component rendering
### What's with all the different libraries??
- You can use a full testing library ([React Testing Library](https://testing-library.com/docs/react-testing-library/example-intro) being the most popular choice, [Enzyme]() being another option), or *test components directly without any special tooling*.
- [Test Renderer](https://reactjs.org/docs/test-renderer.html) is a half-way house between direct testing of the `render()` function and testing with React Testing Library, as it provides some level of abstraction that you run assertions against.
- [Test Utilities](https://reactjs.org/docs/test-utils.html) is a selection of useful functions to test React components.

> **Ultimately, Test Utilities and Test Renderer contain a subset of functionality, and Enzyme and React Testing Library were built upon them.** :+1: The next few sections provide more detail on all of the above.

### React Testing Library (RTL)
- aims to support writing tests that avoid including implementation details
- guiding principle: tests should resemble the way the software is used:
  - encourages rendering components to DOM nodes and making assertions against those
  - **testing strategy:** test things that should be visible to the user, based on different sitations
  
Basic sample test:
```js
import React from 'react';
import { render } from '@testing-library/react';
import MyComponent from './MyComponent';

test('renders important text', () => {
  const { getByText } = render(<MyComponent />);
  const linkElement = getByText(/important text here/i);
  expect(linkElement).toBeInTheDocument();
});
```

**The `render()` function** is at the heart of RTL
- renders React component into a simulated browser environment (good compromise of speed and being a realistic emulation)
- returns the container div which the component has been rendered into:
  ```js
  const container = render(<MyComponent prop1="foo" prop2={true} />);
  ```
- it also returns [a set of query functions](https://testing-library.com/docs/dom-testing-library/api-queries#queries), that are bound to the rendered component, and provide an effective way to query for specific DOM elements to trigger events or make assertions about the rendered content:
  ```js
  container.getByLabelText('First Name');   // find a form field with a given label
  container.getByText('some text');   // find text by string
  container.getByText(/some text/i);   // find text by RegEx
  container.getByTitle('Title text');   // find element with matching title attribute
  ```
- as the container div is a DOM element, you can also use any [element properties](https://developer.mozilla.org/en-US/docs/Web/API/Element) too:
  ```js
  container.innerHTML;
  
  ```

> :bulb: RTL query functions intend to approach the component under test in the same way a user would look at the UI, avoiding any implementation specifics (e.g. querying by class or id selectors or based on DOM structure).


### Enzyme vs React Testing Library
Different philosophies:
- Enzyme allows you to access the internal workings of your components. You can read and set the state, and you can mock children to make tests run faster.
- By contrast, react-testing-library doesn't give you any access to the implementation details. It renders the components and provides utility methods to interact with them. The idea is that you should communicate with your application in the same way a user would. So rather than set the state of a component you reproduce the actions a user would do to reach that state.

Maintainability:
- Enzyme is easier to grasp but in the long run, it's harder to maintain.
- react-testing-library forces you to write tests that are a bit more complex on average but rewards with higher confidence in your code.


### Testing components directly
You don't need any libraries at all if you prefer testing from first principles: you can just invoke the component function directly. To test a `Message` component:
```js
const Message = (props) => {
    return (
      <p>
        {props.isImportant 
          ? <strong title='Important content'>{props.content}</strong> 
          : <span title='Regular content'>{props.content}</span>}    
      </p>);
  };
```
You invoke the component like so: `Message({ content: "I see everything twice", isImportant: false })`
```js
import Message from './Message';

describe('Message', () => {
    it('should always render the message', () => {
        const notImportantMessage = Message({ content: "I see everything twice", isImportant: false });
        expect(notImportantMessage.props.children.props.children).toBe('I see everything twice');
        const importantMessage = Message({ content: "I see everything twice", isImportant: true });
        expect(importantMessage.props.children.props.children).toBe('I see everything twice');
    });

    it('should make important messages strong', () => {
        const importantMessage = Message({ content: "I see everything twice", isImportant: true });
        expect(importantMessage.props.children.type).toBe('strong');
    });

    it('should not make not important messages strong', () => {
        const importantMessage = Message({ content: "I see everything twice", isImportant: false });
        expect(importantMessage.props.children.type).not.toBe('strong');
    });
});
```
- *Disadvantage:* having to navigate deeply nested structures; this is not only noisy, but also encodes the implementation of the component, therefore making the tests very brittle


### Testing with Test Utilities
- library that can be used with different testing frameworks, not just Jest
- has functions for rendering components into a virtual browser environment, mocking components, triggering events on elements and much more
- `act()` function provides a wrapper for component rendering and updating components:
  ```js
  act(() => {
    ReactDOM.render(<Message content="some stuff" isImportant={true} />, container);
  });
  ```
- can then use DOM methods like `queryselector()` to find elements to assert against/dispatch events on:
  ```js
  const button = container.querySelector('button');
  
  act(() => {
    button.dispatchEvent(new MouseEvent('click', {bubbles: true}))
  });
  ```
- *Disadvantages:* very limited API compared to feature set of RTL/Enzyme libaries; much more boilerplate (e.g. having to wrap event triggers in `act()` method and having to explicitely render components into a container); makes tests harder to read


### Testing with Test Renderer
- renders React components to pure JS objects (= object representations of the component hierarchy), without depending on the DOM
- allows to test against React abstractions such as components and props
- not using virtual DOM approach like Enzyme/RTL, but closer to actual user impression of a component than when testing components directly
- renders components using `create()` function:
  ```js
  const root = TestRenderer.create(<Message content="Some stuff" isImportant={true} />).root;
  ```
- provides an API for traversing the component graph:
  ```js
  root.findAllByType("div");
  root.findByProps({"data-testid": "rover-curiosity"});
  root.findAll((i) => i.children.length > 0);
  ```


## Testing component events
## Testing components with state and effects
## Testing components with state management

