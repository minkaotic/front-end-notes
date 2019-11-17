# Asnchrony in JavaScript

[blurb]

### Contents

- **[JS Concurrency Model & Event Loop](#js-concurrency-model--event-loop)**

--------------

## JS Concurrency Model & Event Loop
JavaScript is a single-threaded language and has a concurrency model based on an "event loop". This model is quite different from models in other languages like C and Java.
* The *event loop* is a constantly running process that checks i fthe call stack is empty
* A JavaScript runtime uses a *message queue*, which is a list of messages to be processed
* Each message has an associated *function*, which gets called in order to handle the message.
* At some point during the *event loop*, the runtime starts handling the messages on the queue, starting with the oldest one.

**Examples:**
* In web browsers, messages are added to the event loop anytime an event occurs and there is an event listener attached to it. If there is no listener, the event is lost.

*[to be continued...]*

For more detail, refer to [this article on MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop) or [this article on HackerNoon](https://hackernoon.com/understanding-js-the-event-loop-959beae3ac40).
