# Asnchrony in JavaScript

**`JavaScript is a single-threaded, non-blocking, asynchronous, concurrent programming language.`**

:cold_sweat: **_But what does this even mean???_** :dizzy_face: - - - > **`Let's explore!`**

![Async kittens](/img/kittens.png)

### Contents

- **[Introduction](#introduction)**
- **[JS Concurrency Model & Event Loop](#js-concurrency-model--event-loop)**
- **[Resources](#resources)**

--------------

## Introduction
JavaScript is a **single-threaded** language, i.e., it can (*technically*) only process one task at a time. But some tasks take longer to execute (network requests etc.), and if nothing else could run in your application in that time, it would negatively impact performance and overall user experience. This is exacerbated by the way browsers work: all user interactions would be blocked until the lenghty JS operation finishes executing.

Any time you have code that needs to execute after some period of time, in response to an event (like a mouse click), or upon receiving the data it needs, you're introducing **asynchronous behavior** into your program. JavaScript and its runtime environment provide efficient ways to handle async operations, and code that is designed/written to work asynchronously is called **non-blocking**.

#### Example: Blocking & non-blocking code

```js
function wait() {
  console.log('starting...');
  const start = new Date().getTime();
  while (new Date().getTime() - start < 8000);
  console.log('finished!');
}
```
-> line 5 is *blocking* and the code after it cannot run until it's completed

```js
function carryOn() {
  console.log('starting...');
  setTimeout(() => {
    console.log('finished!');
  }, 8000);
}
```
-> JS' runtime in the browser provides the `setTimeout()` method to allow asynchronously scheduling code to run after a given amount of time - meanwhile code execution can continue.



## JS Concurrency Model & Event Loop
JavaScript is a single-threaded language and has a concurrency model based on an "event loop". This model is quite different from models in other languages like C and Java.
* The *event loop* is a constantly running process that checks i fthe call stack is empty
* A JavaScript runtime uses a *message queue*, which is a list of messages to be processed
* Each message has an associated *function*, which gets called in order to handle the message.
* At some point during the *event loop*, the runtime starts handling the messages on the queue, starting with the oldest one.

**Examples:**
* In web browsers, messages are added to the event loop anytime an event occurs and there is an event listener attached to it. If there is no listener, the event is lost.

*[to be continued...]*



## Resources
#### Reading:
- [MDN Docs: Concurrency Model & Event Loop](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop)
- [MDN Docs: Introducing asynchronous JavaScript](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Asynchronous/Introducing)
- [Understanding JS: The Event Loop (HackerNoon article)](https://hackernoon.com/understanding-js-the-event-loop-959beae3ac40)
- [Understanding Asynchronous JavaScript (Bits & Pieces article)](https://blog.bitsrc.io/understanding-asynchronous-javascript-the-event-loop-74cd408419ff)

#### Videos & courses:
- [Treehouse course on Asynchronous JS Programming](https://teamtreehouse.com/library/asynchronous-programming-with-javascript)
- [What the heck is the event loop anyway? (Philip Roberts, JSConf EU)](https://youtu.be/8aGhZQkoFbQ)
- [In The Loop (Jake Archibald, JSConf.Asia)](https://youtu.be/cCOL7MC4Pl0)
- [Further Adventures of the Event Loop (Erin Zimmer, JSConf EU)](https://youtu.be/u1kqx6AenYw)
