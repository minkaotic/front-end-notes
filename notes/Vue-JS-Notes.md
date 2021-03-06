# Vue.JS Notes

## Contents
- [Setup](#setup)
- [Templates & Data](#templates--data)
- [Instance Options](#instance-options)
- [Directives](#directives)
- [Event Handling](#event-handling)
- [Components](#Components)
- [Sources](#sources)
_______________
## To Do
- [ ] Finish https://teamtreehouse.com/library/vuejs-basics (107m left)
- [ ] Recap Vue Component Tests (13 mins) https://www.youtube.com/watch?v=OIpfWTThrK8
- [ ] More on unit testing Vue components by the creator of vue-test-utils https://www.youtube.com/watch?v=LxXsGNXsMo8
- [ ] Docs: https://vue-test-utils.vuejs.org/ - using this and the above video, create a simple TDD Vue app for practice! (Todo, TicTacToe...)
- [ ] Best Practices etc: https://medium.com/js-dojo/vuejs-tips-best-practices-39d9962bb255
- [ ] Check out https://livebook.manning.com/book/testing-vue-js-applications/chapter-2/5
- [ ] Check out VuePress - a static site generator based on Vue.js! https://vuepress.vuejs.org/

_______________


## Setup
Vue can be set up via:
- Direct inclusion of framework files in `<script>` tag
- NPM :point_right: `$ npm install vue` (recommended approach for larger scale projects)
- The dedicated [Vue.js CLI](https://github.com/vuejs/vue-cli)

For more information on either of these, see the [Installation docs](https://vuejs.org/v2/guide/installation.html).

_______________


## Templates & Data
[Vue](https://vuejs.org/) helps separate a website's *data* from the user's *view* of the website and provides better seperation from the *view logic* (where, when and how certain information is displayed). Vue also allows you to define behaviour and connect data to a template, that is used to render the view.

![Vue.js purpose overview](/img/vue_overview.png)

Every Vue app starts with at least 2 things: some data, and a template (= the representation of how you want the structure of your application - i.e. the HTML - to relate to your data), for example:

***HTML - basic syntax of a Vue template***
```html
<div id="helloVue">
  <h1>{{ title }}</h1>
  <p>{{ message }}</p>
</div>
```
- A Vue template generally consists of HTML, data bindings (`{{ title }}`) and Vue directives. This is where you lay out the rules of how Vue should display your data. In our example, we've built a template that creates two data bindings: a title and a message.

***JS - basic syntax of a Vue instance***
```js
const helloWorld = new Vue({
  el: '#helloVue',
  data: {
    title: "HELLO WORLD!!!",
    message: "This is my first Vue template!"
  }
});
```
- *You pass the Vue instance an object containing [options](#instance-options) that give you the ability to store data and define methods.* The data and methods you define are then used in a Vue template to control the behavior of your application.

> :bulb: Most projects will only contain one root Vue instance. However, you can include as many as you want.

You can also use Javascript directly in the HTML template, or bind multiple pieces of data within the same element, e.g.:
```html
<div id="example">
  <h1>{{ title }}, {{ name.toUpperCase() }}</h1>
  <p>{{ message }}</p>
</div>
```
- :point_right: More about [using JS expressions in Vue](https://vuejs.org/v2/guide/syntax.html#Using-JavaScript-Expressions) - including possibilities and limitations.

_______________


## Instance Options
Below are options that are most commonly used; refer to the docs for a full overview of [data options](https://vuejs.org/v2/api/#Options-Data), [DOM options](https://vuejs.org/v2/api/#Options-DOM), [Lifecycle Hooks](https://vuejs.org/v2/api/#Options-Lifecycle-Hooks) and other options.

| Option       | Description                                                          |
|--------------|----------------------------------------------------------------------|
| `components` | The child components used by the instance / component                |
| `props`      | Attributes that are exposed to accept data from the parent component |
| `data`       | Define data properties (variables) for the Vue instance or component |
| `methods`    | Functions bound to the Vue instance                                  |
| `computed`   | Properties representing derived values; will automatically update whenever values used to calculate is updated |
| `mounted`    | Called after the instance has been mounted; see [Lifecycle Hooks](https://vuejs.org/v2/api/#Options-Lifecycle-Hooks) |

-> More detail on [Methods vs Computed](https://stackoverflow.com/questions/44350862/method-vs-computed-in-vue)

-> Data properties can be accessed in the methods object with the `this` keyword, but [this doesn't work when using arrow function syntax](https://codingexplained.com/coding/front-end/vue-js/using-es6-arrow-functions-vue-js). It is therefore recommended not to use arrow functions in Vue.

_______________


## Directives
A ***Vue directive*** is a special attribute that you add to an HTML element in a Vue template. These are like special instructions just for Vue: used to define certain behaviors such as when a method should be called in response to an event, or when to show/not show pieces of a UI element.

### `v-text`
[`v-text`](https://vuejs.org/v2/api/#v-text) updates the element’s `textContent`. :bulb: **NB:** If you need to update the part of `textContent`, use `{{ Mustache }}` interpolations instead.

#### Example
Instead of the 'mustache syntax' used in the examples above, i.e. `<h1>{{ title }}</h1>`, we could achieve the same result by using the  directive: `<h1 v-text="title"></h1>`

### `v-html`
[`v-html`](https://vuejs.org/v2/api/#v-html) updates the element’s `innerHTML`, for example: `<div v-html="html"></div>`.
> :zap: Dynamically rendering HTML on your website can easily lead to [XSS attacks](https://en.wikipedia.org/wiki/Cross-site_scripting). Only use `v-html` on trusted content and never on user-provided content.

### `v-bind`
[`v-bind`](https://vuejs.org/v2/api/#v-bind) dynamically binds **attributes**, or a **component prop** to an expression.

#### Example - binding values to various attributes
*In the template:*
```html
<p v-text="title"></p>
<a v-bind:href="link">A link to somewhere </a>
<img v-bind:src="img.src" v-bind:alt="img.alt">
```
*In the Vue instance:*
 ```js
 new Vue({
   el: '#anHTMLElement',
   data: {
     title: "A nice title",
     link: "https://www.alinksomewhere.com",
     img: {
      src: 'https://placeimg.com/200/200/animals',
      alt: 'A placeholder image of animals'
  }
});
```
> :point_right: **The `:` shorthand can be used instead of `v-bind:`!**

#### Example - binding values to props, using `v-bind` shorthand
Note that "prop" must be declared in `my-component`.
```html
<my-component :prop="someThing"></my-component>
```


### Conditional rendering
For details on conditional rendering, including `v-show`, `v-if` and others, refer to [this section of the docs](https://vuejs.org/v2/guide/conditional.html).

_______________


## Event Handling
The [**`v-on`**](https://vuejs.org/v2/api/#v-on) directive attaches an event listener to an element. The event type is denoted by the argument. The expression is most commonly a function name or inline statement.

> :bulb: When used on a normal element, it listens to [native DOM events](https://developer.mozilla.org/en-US/docs/Web/Events) only. When used on a *custom element component*, it listens to custom events emitted on that child component.

When listening to native DOM events, you can refer to the native event as follows:
1. If `v-on` is used with a function name, the method receives the native event as the only argument.
2. If `v-on` is used with an inline statement, this has access to the special `$event` property, e.g.: `v-on:click="handle('ok', $event)"`.

#### Example
*In the template:*
```html
<div id="app">
  <h1 v-on:mouseover="functionToRun">Click Me!</h1>
</div>
```

*In the Vue instance:*
```js
 new Vue({
   el: '#app',
   data: {
     ...
   }, 
   methods: {
     functionToRun: function() {
      //Do stuff on mouseover
     }
   }
});
```

## Components
Since components are reusable Vue instances, they accept the same options as `new Vue`, such as `data`, `computed`, `watch`, `methods`, and lifecycle hooks. The only exceptions are a few root-specific options like `el`.

### `Vue.extend()` vs `Vue.component()`

https://vuejs.org/v2/api/#Vue-extend
https://vuejs.org/v2/guide/components.html

https://stackoverflow.com/questions/40719200/what-is-vue-extend-for
https://frontendsociety.com/why-you-shouldnt-use-vue-component-ff019fbcac2e

_______________


## Sources
- [Treehouse VueJS Basics course](https://teamtreehouse.com/library/vuejs-basics)
- [Vue Essentials](https://vuejs.org/v2/guide/index.html) section in public docs
