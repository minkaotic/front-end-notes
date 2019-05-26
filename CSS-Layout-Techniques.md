# CSS Layout Techniques

## Contents
- **[Basics](#basics)**
  - [CSS Reset with Normalize](#css-reset-with-normalize)
  - [Layout Wrapper](#layout-wrapper)
- **[Responsive Design](#responsive-design)**
  - [Media Queries](#media-queries)
  - [Breakpoints](#breakpoints)
  - [Mobile first](#mobile-first)
  - [Viewport meta tag](#viewport-meta-tag)  
- **[Display Modes](#display-modes)**
  - [Using `inline-block` to lay out columns](#using-inline-block-to-lay-out-columns)
  - [Other nifty usages of `display`](#other-nifty-usages-of-display)
- **[Floats](#floats)**
  - [Common issues & workarounds](#common-issues--workarounds)
- **[Flexbox](#flexbox)**
  - [Flex container properties](#flex-container-properties)
  - [Flex item properties](#flex-item-properties)
- **[CSS Positioning](#css-positioning)**
  - [Five `position` properties](#five-position-properties)
  - [Combining absolute & relative positioning](#combining-absolute--relative-positioning)
  - [Z-Index](#z-index)

______________________________________________

## Basics
### CSS Reset with Normalize
- Any browser will apply its own defaults with the User Agent Stylesheet to any webpage, before other styles are applied.
- As the defaults for things like margins, padding, line-height and font sizes are slightly different between different browsers, it is sensible practice to do a *CSS reset*, to ensure that your layout displays as consistently as possible across all browsers.
- A modern day alternative to a classic reset is using the *Normalize* approach - [more detail about this here](http://nicolasgallagher.com/about-normalize-css/).

> ➭ Download the [normalize.css](https://necolas.github.io/normalize.css/)

Other CSS reset methods:
- [Eric Meyer’s Reset CSS](https://meyerweb.com/eric/tools/css/reset/)
- [Popular CSS resets, all in one place](https://cssreset.com/)


### Layout Wrapper
A *wrapper* (or *container*) is commonly used to center a layout on the page. The wrapper keeps a layout from looking too wide or too narrow depending on the device or viewport width.

![Wrapper diagram](https://github.com/minkaotic/front-end-notes/blob/master/img/wrapper_diagram.png)

Using a wrapper `div` to contain the other elements on the page:

```css
.wrapper {
  width: 70%;       /*prevents the layout from stretching too wide*/
  margin: 0 auto;   /*setting L+R margins to auto centres the wrapper in the browser*/
}
```
- Depending on the desired design, you can use this wrapper around all contents of the site, or just around the main contents, leaving the header and footer at 100% width.
- One approach for the latter layout is to create a wrapper around the main content and, optionally, an inner wrapper for the content inside the header and footer (if they have significant amounts of content which you'd like to align with the main content). Note that all of these wrappers can use the same class name (e.g. `container`) as they will need to have the same `width` and `margin` rules applied to them.

#### Creating a sticky Footer
*Basic method:* With a `<div class="wrap">` container around all content *but* the footer, do:
```css
.wrap {
  min-height: calc(100vh - [height of footer]px);
}
```
- If you still see a gap below the footer in browsers like Firefox and IE, or when you change the browser's zoom, give .main-footer a height or min-height value of `[height of footer]px`.



## Responsive Design
- Responsive web design is a collection of techniques for building websites that work on multiple screen sizes.
- [This seminal article](http://alistapart.com/article/responsive-web-design/) by Ethan Marcotte first introduced the idea.
- **Horizontal vs vertical units:** For sizing the vertical layout, it's common to use pixel as the default unit, but for the horizontal layout, it is advisable to use [relative units](https://github.com/minkaotic/front-end-notes/blob/master/CSS-Fundamentals.md#units) (such as percentage or `em` / `rem`), which will adjust based on the size of the device.

### Media Queries
Media queries are CSS rules that help us include CSS code only when certain conditions are met. These conditions are called *media features*, and in the case of responsive web design, the media feature most commonly used is width, or more specifically, min-width. (Other features that can be queried include: orientation; resolution.)

Media queries allow us to tailor our content to a wide range of devices and viewport sizes without having to change anything in the HTML. For example, to set up various media query breakpoints for different styles depending on browser size:

```css
@media all and (max-width: 960px) {
  [selector] {
    [style declaration]
  }
}

@media all and (max-width: 480px) {
  [selector] {
    [style declaration]
  }
}
```
For more detail on the technical use of `@media` queries, see [MDN docs](https://developer.mozilla.org/en-US/docs/Web/CSS/@media)

### Breakpoints
The question of where you should set your breakpoints is much debated, with the three main camps being:
1. **Breakpoints match common screen sizes:** set breakpoints based on common screen resolutions of popular devices
1. **Breakpoints between clusters of screen sizes:** fit breakpoints around clusters of common screen sizes - see diagram below
1. **Breakpoints based on content:** Rather than being defined by devices, breakpoints reflect the points at which a given design 'breaks' (stops working well) and needs to be adjusted

![Breakpoints according to camp 2](https://github.com/minkaotic/front-end-notes/blob/master/img/breakpoints.png)
*Breakpoints between clusters of screen sizes ([Source](https://medium.freecodecamp.org/the-100-correct-way-to-do-css-breakpoints-88d6a5ba1862))*

- According to this perspective from the 2nd camp, sensible breakpoints would be `600, 900, 1200, 1800`

### Mobile first
In the stylesheet, serve the basic layout styles and minimal amount of code to style a page for a small, mobile device first. Then, using media queries, you add breakpoints which successively adjust the layout for wider screens and devices.

A common approach starting out a basic mobile-first design, is to use a simple 1-column approach with a little padding left & right on mobile, then add a percentage based width in the first media query (which will still be applied to higher screen sizes unless overridden in later media queries):
```css
@media screen and (min-width: 769px) {
  .container {
    width: 70%;
    max-width: 1000px;
    margin: 0 auto;
  }
```
**NB:** To make this approach (where space around the content is defined by a combination of padding and width percentages) more manageable, it helps to use the `box-sizing: border-box` [rule](https://github.com/minkaotic/front-end-notes/blob/master/CSS-Fundamentals.md#margin-padding-width-and-box-sizing), which forces any padding and borders into the width and height of an element instead of expanding it.

### Viewport meta tag

Using **mobile device emulation in Chrome dev tools**, you'll notice that often our CSS rules for responsive design using media queries might not be applied to certain mobile phones, as they may be using virtual viewports rather than the real viewport size. To get around this, we need to use the HTML `viewport` meta tag in the head of any HTML pages:

```html
<head>
    <title>...</title>
    <link rel="stylesheet" href="css/style.css">
    <meta name "viewport" content="width=device-width">
</head>
```

For more information on this, see [MDN docs](https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag).



## Display Modes
Most common values for the `display` property, and elements defaulting to that display mode:

| Block          | Inline     | Inline-block  |
|----------------|------------|---------------|
| `h1`, `h2` etc | `span`     | `img`         |
| `p`            | `a`        |               |
| `div`          |            |               |
| `ol`/`ul`/`li` |            |               |

- `block` elements span the entire width of their container, forcing all subsequent elements to the next line

- `inline` elements  only span the width of their contents, allowing any inline level element to flow up next to it on the same line. ***NB:** width and height properties, or top/bottom margin or padding settings won't be applied to inline elements*; only left/right margins and padding will work.

- `inline-block`'s main two differences vs. `inline` is that it allows to set a width and height on the element, and that the top and bottom margins/paddings are respected.

:sparkles: Interesting article on leveraging the display mode as an alternative to using floats: "[The Secret To Designing Website Layouts Without CSS Floats]( https://www.webdesignerdepot.com/2014/07/the-secret-to-designing-website-layouts-without-css-floats/)" :sparkles:

### Using `inline-block` to lay out columns
E.g., to lay out two `div`s as equal width side-by-side columns:
```css
.col {
  display: inline-block;
  width: 50%;
  margin-right: -4px;  /* (explanation below) */
}
```

#### Gaps between inline/inline-block elements

The browser interprets the line breaks and spaces in the HTML as content, and adds spaces between elements displayed inline and inline-block, just like it adds spaces between words.

The size of the gap is commonly `4px`, but depends on the element's font size too - the larger the font size, the larger the gap. You can remove the gaps by either:
- applying a small, negative right margin to the elements: `margin-right: -4px;`
- setting `font-size: 0;` on the parent element - this makes the size of the space zero as well. You'll then need to set the font size of the inline-block child elements back to your desired size.

#### Top aligning columns

Since the default vertical alignment for inline(-block) items is `baseline`, the the tops of columns that are different height won't be aligned. To change this behaviour, set the column `div`s to `vertical-align: top;`.

### Other nifty usages of `display`
- `li { display: inline; }` to keep list items next to each other on one line, then use padding and margin to neaten up visually (for more on list manipulation, see: https://teamtreehouse.com/library/lists-5)
- Setting an `<a>` element's display value to block makes its hover area expand within its parent (nicer for clickability) and lets you apply top and bottom padding values.



## Floats
Floats are one of the most commonly used methods for laying out a page with CSS. When an element is floated, the element is taken out of the normal flow of the page and placed along the left or right side of its container, causing other elements to wrap around it.

*Common use cases:* wrap text around images; float the links in a navigation; float content columns in a container.

- First, ensure the element's **`width`** is smaller than the parent container so there is space for other things to wrap around it after it's been floated. If you are laying out *columns* using float, use *percentages* to create evenly sized float elements.
- **`float: right;`** will float something to the right, **`float: left;`** to the left.

### Common issues & workarounds
#### Collapsing parents
If a block element contains floated children, its height will collapse (bar any `padding` or fixed `height` value), causing elements to overlap where they shouldn't...

![Collapsing Height](https://github.com/minkaotic/front-end-notes/blob/master/img/float-collapsing-height.png)

Options for resolving this:

1. Set a fixed height. :zap: But this is a very clunky & inflexible solution.
1. Add `overflow: auto;` or `overflow: hidden` for the parent element. :zap: But in some browsers, unwanted scroll bars might appear with `auto`, or bits of content might be cut off with `hidden`.
1. **Clearfix** is the most reliable way to prevent these issues! It uses a CSS pseudo element to force a container to clear its floated children:
  ```css
  [parent selector]::after {
    content: "";
    display: table;
    clear: both;
  }
  ```
  - `content: "";` generates a blank pseudo element at the bottom of (*::after*) the parent container
  - `display: table;` changes display mode from `inline` to `table`
  - `clear: both;` clears any collapsed space on both sides of the container
  - often, a new `.clearfix` class is used for this, which can be assigned to any parent requiring it
  - Further resources: 
    - https://developer.mozilla.org/en-US/docs/Web/CSS/clear
    - http://nicolasgallagher.com/micro-clearfix-hack/

#### Centering floated elements
Center-aligning an element containing floats can be tricky, since we are often floating items within parent containers that are block-level elements by default, taking up the full width of the container. For example:

###### HTML
```html
<header>
  <nav>
    <ul>
      <li><a href="#">About</a></li>
      <li><a href="#">Articles</a></li>
      <li><a href="#">News</a></li>
      <li><a href="#">Contact</a></li>  
    </ul>
  </nav>
</header>
```
###### CSS
```css
li {
  float: left;
}

header {
  text-align: center
}
```
➭ since both `<nav>` and `<ul>` are block-level elements, the navigation elements won't be centered

To fix this, set `<nav>` to `display: inline-block;` - et voila! :raised_hands:


## Flexbox
CSS layout methods like floats, inline-block and absolute positioning have quirks and limitations, as they were ultimately not designed to handle the layout demands of today’s complex responsive websites. By contrast, `flexbox` is a collection of CSS properties that were specifically designed to lay out a collection of items in one direction or another, control the dimensions of the items, and control the spacing between items.

- The two most important elements in flexbox layout are **flex *containers*** (sets context for flexbox layout; contains flex items) and **flex *items*** (the actual items to be layed out).

- Flexbox follows two axes that determine the layout direction of flex items: **main axis** (default direction of left-to-right) and **cross axis** (default direction of top-to-bottom).

> Flexbox plays an important role in modern [responsive web design](#responsive-design) due to it's ability to easily switch between a vertical column layout (more suited to mobile sceens) and a horizontal layout of the items in a container (better suited to tablet and desktop screens).

![Layout examples using Flexbox](https://github.com/minkaotic/front-end-notes/blob/master/img/flexbox-example.png)

### Flex container properties
***To define a flex container***, and turn all its direct children into flex items, set the `display` property of an element to one of the flexbox layout values: `flex` or `inline-flex`:
```css
.container {
  display: flex;
}
```
- **Direction:** By default, flex items are laid out horizontally on the main axis from left to right (equivalent to `flex-direction: row;`). You can change this by changing the `flex-direction` property to `column`, `column-reverse` or `row-reverse`.

- **Automatically wrap based on available space:** With the `flex-wrap` property, you can control whether the flex container is a single-line (`flex-wrap: nowrap;`; default) or multi-line layout (`flex-wrap: wrap;`) - in the latter case, allowing items to wrap onto multiple lines as needed.

- **Distribute items along main axis:**
  - The `justify-content` property will distribute the space that's available after the container's padding and items' margins are accounted for. It defaults to `flex-start`, which places items towards the start of each flex line. By contrast, `justify-content: center;` will center the items on the line, and `justify-content: space-between;` and `..space-around;` will *evenly* distribute the children across a line.
  - If you want to distribute some items to the left and some to the right, with space in between, you can use `margin-right: auto;` on the *flex item* after which the dynamic gap should be inserted:
  ![Flex and margin: auto](https://github.com/minkaotic/front-end-notes/blob/master/img/flex-and-margin-auto.png)

- **Distribute items along cross axis:**
  - The `align-items` property determines where a flex container's items are aligned along the cross axis. By default, flex items stretch to fill the flex container's height (`align-items: stretch;`), but common alternative values are `center` and `flex-start`.
  - **NB:** an equivalent to `align-items` that works on the level of individual item properties is `align-self`.

### Flex item properties
- **Order:** The `order` property allows us to change the order of any flex item, without having to edit the HTML. The default `order` value of all flex items is `0`, and flex items will be placed relative to the other items' `order` values;

- **Item size across main axis:**
  - The **`flex-grow`** property determines how much of the available space inside the flex container an item should take up. (By default, flex items do not take up the full space inside of a container, since the default value of `flex-grow` is `0`.)
    - Assigning a `flex-grow` value of `1` to *all* flex items expands them evenly to take up the full space of a line.
    - The higher the `flex-grow` value, the more an item grows relative to the other items.
    - However, contrary to common belief, `flex-grow: 2;` will not (always) make the item twice as wide as its `flex-grow: 1;` siblings. See the article ["Flex-grow is weird"](https://css-tricks.com/flex-grow-is-weird/) for a fuller explanation.
    - A handy use for `flex-grow` is to lay out the main content of a page alongside a side bar (both of which would be flex items in a parent flex container), so they would keep the same width-ratio regardless of browser size.
    
  - **`flex-basis`** specifies the initial size of an item along the cross axis of a flex item (i.e. before any "remaining space" is distributed), which at the same time sets the minimum size value below which an item will be distributed to the next line (if using `flex-wrap`).
    
  - Since `flex-basis` is commonly used in conjunction with `flex-grow`, the **`flex`** shorthand can be used to set both. It also sets smart defaults for the optional values, for example, `flex: 1;` sets the `flex-basis` to `0` (default is `auto`). (See ["MDN - Flex"](https://developer.mozilla.org/en-US/docs/Web/CSS/flex) for more details.)
  ```css
  .item {
    flex: 1 200px;  /* sets flex-grow to 1 and flex-basis to 200px */
  }
  ```

**Further resources**
- https://css-tricks.com/snippets/css/a-guide-to-flexbox/
- https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties
- https://demos.scotch.io/visual-guide-to-css3-flexbox-flexbox-playground/demos/
- https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Flexible_Box_Layout/Typical_Use_Cases_of_Flexbox



## CSS Positioning
### Five `position` properties
- **`static`** - default value; element is placed within the normal flow
- **`relative`** - element is placed within normal flow (and honored accordingly by elements around it), but it's actual position can be altered using offsets. This also creates a coordinate system for child elements (see [below](#combining-absolute--relative-positioning)).
- **`absolute`** - element is neither affected by, nor affects other elements in the normal flow of the page. Instead, behaves as if it were on a different *layer*. Like `relative` elements, `absolute` elements create a coordinate system for child elements.
- **`fixed`** - like `absolute`, but element is *always* positioned in relation to the viewport; for example, it doesn't move when scrolling.
- **`inherit`** - element inherits the value of its parent element. (Position property elements do not automatically inherit their parent’s values and instead default to `static` if no position value is given.)

#### Example
- To position elements with `relative` or `absolute` positioning, use *positioning offsets* for the element's top, right, bottom or left position

- The following example will place the `.ice-cream` element in the top left corner of the browser window:
  ```css
  .ice-cream {
    position: absolute;
    top: 0;
    left: 0;
  }
  ```
- **NB:** if only *one* offset value is used, the element will retain it's original position along the other coordinate axis!

### Combining absolute & relative positioning
Absolute and relative positioning work hand in hand:
- When using `absolute` positioning by itself, the element is typically positioned in relation to the browser viewport.
- This is called an element's *positioning context*.
- To change the positioning context to another containing (i.e. parent) element, set that element as `relative` - the `absolute` element will now be positioned in relation to that container.
- If multiple parent containers of an `absolute` element are `relative`, then the parent closest to the element will act as its positioning context. 

> **In other words:** An element with relative positioning gives you the control to absolutely position elements anywhere inside it.

#### Use case as part of responsive design
Use all four offset properties, and you can stretch an element without defining any width or height - it’s bound only by its parent element or the document itself!

### Z-Index

Elements positioned as `absolute`, `fixed`, or `relative` follow a **stacking order** that determines which elements display above or below other elements:
- By default, the stacking order is the order they appear in the source code, with elements appearing later in the HTML sitting on top on elements appearing earlier.
- The [`z-index`](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index) property allows to manipulate the stacking order.
- An element with a higher `z-index` value overlaps an element with a lower `z-index` value.
  ![Illustration of z-index](https://github.com/minkaotic/front-end-notes/blob/master/img/z-index.png)

- Non-statically positioned elements have a `z-index` of `0` by default.
- `z-index` only works on elements with a `position` property set to `absolute`, `fixed`, or `relative`. Setting a `z-index` on a `static` element will do nothing.

**NB:** When you give a positioned element a `z-index`, you establish a new **stacking context** for any descendants (children) of that element. Therefore, it is possible to have a higher `z-index` element that's underneath another element with a lower `z-index`. Check articles below for more detail.

**Further resources**
- CSS Positioning 101: http://alistapart.com/article/css-positioning-101/
- MDN 3-part guide on 1. [Stacking without the z-index property](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/Stacking_without_z-index) - 2. [Using z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/Adding_z-index) - 3. [The stacking context](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context)

