# Javascript Frameworks
## Contents
- [Vue.js](#vuejs)
  - [Templates & Data](#templates--data)
  - [Directives](#directives)


_______________

## Vue.js
### Templates & Data
Vue helps separate a website's *data* from the user's *view* of the website and provides better seperation from the *view logic* (where, when and how certain information is displayed). Vue also allows you to define behaviour and connect data to a template, that is used to render the view.

![Vue.js purpose overview](https://github.com/minkaotic/front-end-notes/blob/master/img/vue_overview.png)

Every Vue app starts with at least 2 things: some data, and a template (= the representation of how you want the structure of your application - i.e. the HTML - to relate to your data), for example:

***HTML - basic syntax of a Vue template***
```
<div id="helloVue">
  <h1>{{ title }}</h1>
  <p>{{ message }}</p>
</div>
```
- A Vue template generally consists of HTML, data bindings (`{{ title }}}`) and Vue directives. This is where you lay out the rules of how Vue should display your data. In our example, we've built a template that creates two data bindings: a title and a message.

***JS - basic syntax of a Vue instance***
```
const helloWorld = new Vue({
  el: '#helloVue',
  data: {
    title: "HELLO WORLD!!!",
    message: "This is my first Vue template!"
  }
});
```
- You pass the Vue instance an object containing options that give you the ability to store data and define methods. The data and methods you define are then used in a Vue template to control the behavior of your application.

**NB: Templating and data binding is used in all JS frameworks in some way or other.**

You can also use Javascript directly in the HTML template, or bind multiple pieces of data within the same element, e.g.:
```
<div id="example">
  <h1>{{ title }}, {{ name.toUpperCase() }}</h1>
  <p>{{ message }}</p>
</div>
```
- More about [using JS expressions in Vue](https://vuejs.org/v2/guide/syntax.html#Using-JavaScript-Expressions) - including possibilities and limitations.

_______________

### Directives
Instead of the 'mustache syntax' used in the examples above, i.e. `<h1>{{ title }}</h1>`, we could achieve the same result by using the directive **`v-text`**: `<h1 v-text="title"></h1>`

A ***Vue directive*** is a special attribute that you add to an HTML element in a Vue template. These are like special instructions just for Vue: used to define certain behaviors such as when a method should be called in response to an event, or when to show/not show pieces of a UI element.

***Vue directive syntax examples***

Vue directives start with v-, for example: `v-text`, `v-html`, `v-bind`.

*In the template:*
```
<p v-text="title"></p>
<a v-bind:href="link">A link to somewhere </a>
<img v-bind:src="img.src" v-bind:alt="img.alt">
```

*In the Vue instance:*
 ```
 new Vue({
   el: '#anHTMLElement',
   data: {
     title: "A nice title",
     link: "https://www.alinksomwhere.com",
     img: {
      src: 'https://placeimg.com/200/200/animals',
      alt: 'A placeholder image of animals'
  }
});
```
