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
- `@media (min-width: 576px) { ... }` - Small devices (landscape phones, portrait tablets)
- `@media (min-width: 768px) { ... }` - Medium devices (tablets)
- `@media (min-width: 992px) { ... }` - Large devices (desktops)
- `@media (min-width: 1200px) { ... }` - Extra large devices (large desktops)

### Grid
- Bootstrap uses a 12-column system
- The grid's main components are *containers*, *rows* and *columns*
- Adding the `.col` class to all columns in a row will make them display with equal width in all screen sizes
- **Use breakpoint-specific column classes to layout columns differently for different device sizes (i.e. 1 column on mobile, multiple columns on larger devices) --- more work needed here**


## Nifty Things
### Centering Elements
- Use the `.text-center` class to [center align text](https://getbootstrap.com/docs/4.0/utilities/text/#text-alignment) on all viewport sizes
- Bootstrap also includes an `.mx-auto` class for [horizontally centering block level content](https://getbootstrap.com/docs/4.0/utilities/spacing/#horizontal-centering) that has a fixed `width` by setting the horizontal margins to `auto`

### Responsive Images
- Using the [`.img-fluid` class](https://getbootstrap.com/docs/4.0/content/images/#responsive-images) on an image makes it scale with parent column (by applying `max-width: 100%;` and `height: auto;`), and prevent it from being too large.


## Questions
- [ ] Bundle size - how does Bootstrap get pulled in, and can I limit how much of it gets included?
