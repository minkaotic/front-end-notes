# Front End Testing
## Contents
- [Overview](#overview)
- [Taking Screenshots with Selenium in .NET](#taking-screenshots-with-selenium-in-net)
- [Testing React Components](#testing-react-components)

____________________________________

## Overview
Sources: [Ham Vocke: The Practical Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html) | [Super high-level library overview on Treehouse](https://teamtreehouse.com/library/testing-javascript)

### Client-side rendered applications 
Modern **single page application frameworks** (React, Vue.js, Angular and the like) often come with their own tools and helpers that allow you to thoroughly test these interactions in a pretty low-level (unit test) fashion - see list below for a few libraries/frameworks.

Even if you roll your own frontend implementation using **vanilla JavaScript** you can use general purpose testing tools like Jasmine or Mocha.

* [Mocha](https://mochajs.org/) is one of the most used JS testing frameworks. It runs on Node as well as in the browser.
* [Jasmine](https://jasmine.github.io/), as well as being a general popular BDD-centric testing framework, is a particularly common choice for testing Angular applications.
* [Jest](https://jestjs.io/) is a testing library created by Facebook and is setup automatically when creating a React app. It is built for unit- and integration testing, and can also be used with other client side frameworks, as well as Typescript or Node.
* [Enzyme](https://airbnb.io/enzyme/) is a JS testing utility library developed by AirBnB for testing React compontents; originally built for use with Mocha, but is also compatible with other testing libraries.

Additionally, [Karma](https://karma-runner.github.io/latest/index.html) is a test runner that aims to simplify the testing & debugging process.

### Server-side rendered applications 
With more traditional, server-side rendered applications, [Selenium](https://www.seleniumhq.org/)-based tests will be your best choice.

____________________________________

## Taking Screenshots with Selenium in .NET
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

## Testing React Components
Sources: [Pluralsight Course](https://www.pluralsight.com/courses/testing-react-components) | [Tutorial](https://jestjs.io/docs/en/tutorial-react) | [Testing recipes](https://reactjs.org/docs/testing-recipes.html) | [React Testing Library intro](https://testing-library.com/docs/react-testing-library/example-intro)



