# Bootstrap
:point_right: [**Bootstrap docs**](https://getbootstrap.com/docs/4.0/getting-started/introduction/) :point_left:

### Contents
- **[Intro](#intro)**
- **[Principles & Concepts](#principles--concepts)**
  - [Important Globals](#important-globals)
  - [Reboot](#reboot)
  - [Containers](#containers)
  - [Breakpoints](#breakpoints)
  - [Grid](#grid)
- **[Nifty Things](#nifty-things)**
  - [Centering Elements](#centering-elements)
  - [Responsive Images](#responsive-images)
  - [ScrollSpy](#scrollspy)
- **[Questions](#questions)**

-------------

## Intro
[Bootstrap](https://getbootstrap.com/) is the most popular front-end component library, and can help build a functional design and layout very quickly. It's open source too.

- Provides reusable HTML and CSS for common elements like buttons, forms, navigations, grids etc.
- Adds interactivity to your site with Bootstrap's custom JavaScript plugins
- Offers cross-browser compatibility
- Components are responsive and mobile-first by design


## Principles & Concepts
### Important Globals
- **HTML5 doctype:** Bootstrap requires the use of the HTML5 `doctype`. Without it, you’ll see some funky incomplete styling.
  ```html
  <!doctype html>
  <html lang="en">
    ...
  </html>
  ```
- **Responsive meta tag:** Bootstrap is developed mobile first (code is optimised for mobile devices first and components are then scaled up as necessary using CSS media queries). To ensure proper rendering and touch zooming for all devices, add the responsive viewport meta tag to the `<head>`:
  ```html
  <meta name="viewport" content="width=device-width, initial-scale=1, shrink-to-fit=no">
  ```

### Reboot
Bootstrap builds on the [Normalize.css](https://necolas.github.io/normalize.css/) reset with a custom set of base styles called [Reboot](https://getbootstrap.com/docs/4.0/content/reboot/), to correct inconsistencies across browsers and devices while providing slightly more opinionated resets to common HTML elements.

### Containers
[Containers](https://getbootstrap.com/docs/4.0/layout/overview/#containers) are the most basic layout element in Bootstrap and are required when using its default grid system. There are two types of containers to choose from:
- `.containter` - a responsive, fixed-width container (meaning its max-width changes at each breakpoint)
- `.container-fluid` - a fluid-width container (meaning it’s 100% wide all the time)

> :bulb: While containers can be nested, most layouts do not require a nested container.

### Breakpoints
Bootstrap uses the following [responsive breakpoints](https://getbootstrap.com/docs/4.0/layout/overview/#responsive-breakpoints):
- `@media (min-width: 576px) { ... }` - `sm` - Small devices (landscape phones, portrait tablets)
- `@media (min-width: 768px) { ... }` - `md` - Medium devices (tablets)
- `@media (min-width: 992px) { ... }` - `lg` - Large devices (desktops)
- `@media (min-width: 1200px) { ... }` - `xl` - Extra large devices (large desktops)

> :bulb: The breakpoints `sm`, `md` etc can be combined with many of Bootstraps built in classes, for example: `text-center` will centre text for all screen sizes, but `text-md-center` will only centre it for medium screens and up!

### Grid
- Bootstrap uses a 12-column system built with flexbox
- The grid's main components are *containers*, *rows* and *columns*
- Docs: https://getbootstrap.com/docs/4.0/layout/grid/

There are a number of different ways to define a column's width:
- Use `.col` for all columns in a row to create columns that are always equal in width
- **Breakpoint-specific column classes** using the breakpoint terms above will layout equal width columns only from a certain breakpoint upwards, defaulting to a one-column layout for viewports below it (e.g. `.col-sm` to have equal width columns for small, medium and large devices, but a one-column layout on extra small devices such as mobile phones)
- Use `.col-{breakpoint}-auto` classes to size columns based on the natural width of their content
- Use the **numbered column classes** like `.col-6` or `.col-sm-6` to define a specific number of columns (out of 12) that this column should span

> :bulb: If the total column count within a single row is more than 12, each group of extra columns will wrap onto a new line! (So, if you have 6 `<div>`s with a `col-6` class each, they would wrap onto 3 lines.)

The class types above can be combined to create responsive layouts, for example:
```html
<div class="container">
  <div class="row">
    <div class="col-md col-xl-6">...</div>
    <div class="col-md">...</div>
    <div class="col-md">...</div>
  </div>
</div>
```
➭ the columns will display in single column layout for extra small and small screens </br>
➭ then switch to 3 equal width columns for medium and large screens </br>
➭ then on extra large screens, expand the first column to span 6 columns (effectively taking up half the screen width), with the remaining columns resizing to accomodate it


## Nifty Things
### Centering Elements
- Use the `.text-center` class to [center align text](https://getbootstrap.com/docs/4.0/utilities/text/#text-alignment) on all viewport sizes
- Bootstrap also includes an `.mx-auto` class for [horizontally centering block level content](https://getbootstrap.com/docs/4.0/utilities/spacing/#horizontal-centering) that has a fixed `width` by setting the horizontal margins to `auto`

### Responsive Images
- Using the [`.img-fluid` class](https://getbootstrap.com/docs/4.0/content/images/#responsive-images) on an image makes it scale with parent column (by applying `max-width: 100%;` and `height: auto;`), and prevent it from being too large.

### ScrollSpy
- [ScrollySpy](https://getbootstrap.com/docs/4.0/components/scrollspy/) is an interactive JavaScript plugin that highlights the active navigation links, automatically updating your navigation links based on a user's scroll position.
- It can be used [via data attributes or via JavaScript](https://getbootstrap.com/docs/4.0/components/scrollspy/#usage).
- For a recap on how it works and how to set it up, see this [Treehouse course video](https://teamtreehouse.com/library/using-scrollspy-to-highlight-nav-links).


## Questions
- [ ] Bundle size - how does Bootstrap get pulled in, and can I limit how much of it gets included?
