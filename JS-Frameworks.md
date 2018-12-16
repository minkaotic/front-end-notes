# Javascript Frameworks
## Contents
- [Vue.js](#vuejs)
  - [Templates & Data](#templates--data)

- [AngularJS](#angularjs)
  - [AJAX vs Angular](#ajax-vs-angular)

_______________

## Vue.js
### Templates & Data
Vue helps separate a website's *data* from the user's *view* of the website and provides better seperation from the *view logic* (where, when and how certain information is displayed). Vue also allows you to define behaviour and connect data to a template, that is used to render the view.

![Vue.js purpose overview](https://github.com/minkaotic/front-end-notes/blob/master/vue_overview.png)

Every Vue app starts with at least 2 things: some data, and a template (= the representation of how you want the structure of your application - i.e. the HTML - to relate to your data):

***HTML***
```
<div id="helloVue">
  <h1>{{ title }}</h1>
  <p>{{ message }}</p>
</div>
```
***JS***
```
const helloWorld = new Vue({
  el: '#helloVue',
  data: {
    title: "HELLO WORLD!!!",
    message: "This is my first Vue template!"
  }
});
```
**NB: Templating and data binding is used in all JS frameworks in some way or other.**

_______________

## AngularJS

### AJAX vs Angular
AJAX is a technology that allows to get data from a server without the need to refresh a webpage.

Angular extends this idea with two-way data binding. So the HTML elements on your front end page are in constant communication with your back end server--and vice versa. Angular can achieve other things as well and is useful for separating your concerns, i.e. separating your data, the functions performed on that data, and how the user sees the data.

