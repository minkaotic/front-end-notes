# Front End Testing

## Overview
### Client-side rendered applications 
Modern **single page application frameworks** (React, Vue.js, Angular and the like) often come with their own tools and helpers that allow you to thoroughly test these interactions in a pretty low-level (unit test) fashion - see list below for a few libraries/frameworks.

Even if you roll your own frontend implementation using **vanilla JavaScript** you can use general purpose testing tools like Jasmine or Mocha.

* [Mocha](https://mochajs.org/) is one of the most used JS testing frameworks. It runs on Node as well as in the browser.

* [Jasmine](https://jasmine.github.io/), as well as being a general popular BDD-centric testing framework, is a particularly common choice for testing Angular applications.

* [Jest](https://jestjs.io/) is a testing library created by Facebook and is setup automatically when creating a React app. It is built for unit- and integration testing, and can also be used with other client side frameworks, as well as Typescript or Node.

* [Enzyme](https://airbnb.io/enzyme/) is a JS testing utility library developed by AirBnB for testing React compontents; originally built for use with Mocha, but is also compatible with other testing libraries.


### Server-side rendered applications 
With more traditional, server-side rendered applications, Selenium-based tests will be your best choice.



**Sources:**
- [Ham Vocke: The Practical Test Pyramid](https://martinfowler.com/articles/practical-test-pyramid.html)
- [Super high-level library overview on Treehouse](https://teamtreehouse.com/library/testing-javascript)
