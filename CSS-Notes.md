# CSS Notes

## Contents
- **[Basics](#basics)**
  - [Selectors](#selectors)
  - [Rule Precedence](#rule-precedence)
- **[Text & Fonts](#text--fonts)**
  - [Web fonts](#web-fonts)
- **[Box Model Elements](#box-model-elements)**
  - [Borders](#borders)
  - [Margin, padding, width and box-sizing](#margin-padding-width-and-box-sizing)
  - [The calc() function](#the-calc-function)
  - [Why margins collapse](#why-margins-collapse)
- **[Colour & Background Images](#colour--background-images)**
- **[Media Queries for Responsive Design](#media-queries-for-responsive-design)**
  - [Breakpoints](#breakpoints)
  - [Mobile first](#mobile-first)
  - [Viewport meta tag](#viewport-meta-tag)
- **[Fancy Design](#fancy-design)**
   - [Shadow effects](#shadow-effects)
   - [Rounded corners](#rounded-corners)
   - [Gradients](#gradients)
- **[Layout Techniques](#layout-techniques)**
  - [CSS Reset with Normalize](#css-reset-with-normalize)
  - [Layout Wrapper](#layout-wrapper)
  - [Display Modes](#display-modes)
  - [Floats](#floats)

______________________

## Basics
- A **CSS rule** is comprised of a *selector*, and a *declaration block* containing one or more declarations; each declaration contains a *property* and its chosen value
- A comment is denoted by `/* ....... */`
- **Don't repeat yourself:** If you find that a certain style declaration is repeated in lots of different rules, it might be worth breaking out a different class rule for it.

### Selectors
- A **universal selector** can be used via the `*` character
- **Type** or **element selectors** like `h1` or `p` will target all elements of a given HTML tag - good for defining defaults
- **Id selectors** like `#intro-text` target the specific html element that has that id in its attributes (NB: elements can only have one id, and ids have to be unique)
- **Class selectors** like `.primary-content` target all html elements with that class in their attributes (NB: elements can have multiple classes)
- **Descendant selectors** like `.primary-content p` can be made up of two or more selectors and will target all elements that match that relationship, e.g. all "paragraphs" within any elements marked by the "primary-content" class
- **Pseudo-classes** like `:link` `:visited` or `:hover` target elements dynamically based on user interaction, an element’s state
- *Multiple selectors*, separated by commas, can be used in a rule, such as `.primary-content, .secondary-content`

### Rule Precedence
- The **cascade** determines which styles are assigned to a HTML element; follows 3 main steps to determine which rule to apply:
  - **Importance:** User agent styles < User styles < Author styles
  - **Specificity:** Styles with more specific selectors will override styles with less specific selectors: universal selector < element selectors < class selectors < id selectors < inline styles
  - **Source order:** If there are two or more conflicting declarations within the same rule or level of specificity, the one appearing latest in the source takes precedence. (If there are multiple style sheets, the one linked in last takes precedance.)

- **Inheritance:** if no specific rules are in place for them, elements will inherit the style values of their parent element.


## Text & Fonts
- Create a **font stack** to make sure we have fallbacks of *websafe fonts* as well as *generic font families* defined in case our desired font doesn't work on a given machine
- When using **`font-family`** with multi-word name, use " "s
- Use **font** property as shorthand to specify weight, size (obligatory), line height and family (obligatory), eg.: `font: normal 1em/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif;`
- `em`s are relative to parent element's pixel size, but the default of 1 "em" is 16px (which is the value of em at the root value) 
- `rem`s are relative to root element's pixel size, i.e. avoid compounding issues when sizing up or down

Other tips:
- Use `text-decoration: none;` to get rid of underlines on links
- The default `font-weight` of headlines is bold
- Adjust **`line-height`** with unit-less values like 1.5 or 2
- You can also adjust letter spacing, e.g.: `letter-spacing: .065em;`

### Web fonts
Web fonts are special types of fonts optimized for screen display, and linked to our web pages from an external source. They eliminate the need to depend on the limited number of fonts installed on a user's computer.

Web font formats:
- `.eot` - proprietary Internext Explorer format
- `.woff` - open format developed by Mozilla and compatible with most modern browsers
- `.ttf` - used for Safari, Android & iOS display

Add a web font to your style sheet like this:
```
@font-face {
  font-family: 'Abolition Regular';
  src: url('../fonts/abolition-regular-webfont.eot');
  src: url('../fonts/abolition-regular-webfont.eot?#iefix') format('embedded-opentype'),
       url('../fonts/abolition-regular-webfont.woff') format('woff'),
       url('../fonts/abolition-regular-webfont.ttf') format('truetype');
}
```

## Box Model Elements

![CSS Box Model](https://github.com/minkaotic/front-end-notes/blob/master/box_model.png)

### Borders
- **Border shorthand**: `border: [width] [style] [color]` - or do each of them individually for control over each side, eg.: `border-width: 10px 20px`, or `border-top: 2px solid lightgrey;`. NB:
  - when not specifying a colour, the colour is inherited from the element's text colour.
  - When using **2 value shorthand**, the first value refers to top/bottom and the second to left/right.
  - When using **3 value shorthand**, the values refer in order to: TOP, LEFT/RIGHT, BOTTOM
- *Similar rules apply to settings for margin and padding*

### Margin, padding, width and box-sizing
- **`margin: auto`** will generally **centre** content on the page!
- `width` values provided as **percentages** are applied in relation to the *parent container* - and `width` generally applies only to the *content* of the box, i.e. not including its padding and border, however...
- **`box-sizing: border-box`** dynamically subtracts the borders and paddings of the element from the width and height properties we set, making it easier to define flexible widths and heights in our project (it's one of the few good uses for the universal selector!) *
- `max-width` sets the maximum width of an element, preventing elements to become too large to look good on big screens; when set as percentage values can also be used as part of responsive design *

(* for more on `box-sizing` and `max-width` see https://teamtreehouse.com/library/boxsizing-and-maxwidth)

### The calc() function
- Allows to apply mathematical operations and assign the result to any CSS property that takes a length or other number value
- Different types of units can be mixed (`%`, `vh`, `px`, `em` etc.)
- Leave whitespace around operator to ensure correct interpretation, e.g.: `height: calc(100% - 3em);`

### Why margins collapse
- If there is no content, padding, or border area to interrupt two touching margins, the margins collapse to the largest of the two margin values.
- Depending on what causes the collapsing, the collapsed margin can end up outside the parent.
- You may experience margins collapsing in adjacent elements like paragraphs and divs.
- If a div's bottom margin is larger than the top margin of the div below it, the margin area between the divs collapses to the largest of the two margin values.
- **Only vertical margins are affected by this; horizontal margins do not collapse.**

NB: The margins of floating and absolutely positioned elements never collapse.
For more info see: https://developer.mozilla.org/en-US/docs/Web/CSS/CSS_Box_Model/Mastering_margin_collapsing


## Colour & Background Images
Every HTML element has a background layer that is transparent by default, but can be filled using `background-image` or `background-color`

**Colours** can be set as either:
- **keyword values**, e.g. `orange`
- **hexadecimal values**, e.g. `#fff or #878787`
- or **rgb functions**, e.g. `rgb(255, 169, 73)`
  - these optionally allow setting transparency via alpha value, eg. `rgba(255, 255, 255, .5)`

**Background images** can be specified like so: `background-image: url('../img/mountains.jpg')`
- By default, `background-image`s are left-aligned and repeated (aka tiled)
- Specify the size of the background image as a percentage of the containing element width with `background-size: 60%;`
- `background-size: cover` adjusts the background area so that it's **completely covered by the background image** (if using), while maintaining its width and height proportions
- Best practice: set background colour as well when using background images, to preserve the contrast between the background and content in case the image isn't available
- `background-position` has a number of nifty options - *[try them out here](https://developer.mozilla.org/en-US/docs/Web/CSS/background-position)!*
- Handy all-in-one **background shorthand:** `background: #ffa949 url('../img/mountains.jpg') no-repeat center / cover;`

*NB: Multiple images can be layered on top of each other*, e.g.: `background: url('rock.png'), url('header-bg.jpg');`! For an example of how do do so and then dynamically position each layer to create a neat effect, see: https://teamtreehouse.com/library/using-calc-as-background-position-offsets


## Media Queries for Responsive Design
Media queries allow us to tailor our content to a wide range of devices and viewport sizes without having to change anything in the HTML. For example, to set up various media query breakpoints for different styles depending on browser size:

```
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
For more detail on the technical use of `@media` queries, see: https://developer.mozilla.org/en-US/docs/Web/CSS/@media

### Breakpoints
The question of where you should set your breakpoints is much debated, the three main camps can be summarised as:
1. **Breakpoints match common screen sizes:** set breakpoints based on common screen resolutions of popular devices
1. **Breakpoints between clusters of screen sizes:** fit breakpoints around clusters of common screen sizes - see diagram below
1. **Breakpoints based on content:** Set breakpoints based on the ranges within which a given design works well

![Breakpoints according to camp 2](https://github.com/minkaotic/front-end-notes/blob/master/breakpoints.png)
*Breakpoints between clusters of screen sizes ([Source](https://medium.freecodecamp.org/the-100-correct-way-to-do-css-breakpoints-88d6a5ba1862))*

- According to this breakdown, sensible breakpoints would be `600, 900, 1200, 1800`

### Mobile first
In the stylesheet, serve the basic layout styles and minimal amount of code to style a page for a small, mobile device first. Then, using media queries, you add breakpoints which successively adjust the layout for wider screens and devices.

A common approach starting out a basic mobile-first design, is to use a simple 1-column approach with a little padding left & right on mobile, then add a percentage based width in the first media query (which will still be applied to higher screen sizes unless overridden in later media queries):
```
@media screen and (min-width: 769px) {
  .container {
    width: 70%;
    max-width: 1000px;
    margin: 0 auto;
  }
```
**NB:** To make this approach (where space around the content is defined by a combination of padding and width percentages) more manageable, it helps to use the `box-sizing: border-box` rule, which forces any padding and borders into the width and height of an element instead of expanding it. For more details see the [Margin, padding and box-sizing](#margin-padding-and-box-sizing) section above.

### Viewport meta tag

Using **mobile device emulation in Chrome dev tools**, you'll notice that often our CSS rules for responsive design using media queries might not be applied to certain mobile phones, as they may be using virtual viewports rather than the real viewport size. To get around this, we need to use the HTML `viewport` meta tag in the head of any HTML pages:

```
<head>
    <title>...</title>
    <link rel="stylesheet" href="css/style.css">
    <meta name "viewport" content="width=device-width">
</head>
```

For more information, see: https://developer.mozilla.org/en-US/docs/Mozilla/Mobile/Viewport_meta_tag


## Fancy Design
### Shadow effects
- **Text shadow** takes 4 values: *horizontal offset, vertical offset, blur radius (optional) and colour*, e.g. `text-shadow: 5px 8px 10px #222;`. Multiple sets of values, separated by commas, will build more complex shadow effects.
- **Box shadow** is similar to text shadow but with optional value of *spread* before the colour value, e.g. for a small bottom box-shadow: `box-shadow: 0 20px 10px -12px rgba(0,0,0, .8);`
- Neat **inner** shadow effect: `box-shadow: inset 0 0 50px 10px rgba(0,0,0, 1);`

### Rounded corners
- use `border-radius` - takes any absolute or relative length value (px, em, % etc.), e.g. `border-radius: 50px 10px;`

### Gradients
Gradients create smooth and gradual transitions between two or more colours. Some examples:
- Simple gradient with default top-to-bottom angle: `background-image: linear-gradient(#ffa949, firebrick);`
- With specific angle defined: `linear-gradient(to left, #ffa949, firebrick)` or `linear-gradient(45deg, #ffa949, firebrick)`
- Radial gradient with circular centre: `background-image: radial-gradient(circle, #ffa949, firebrick);`
- Radial gradient with 3 colours & moved centre circle: `radial-gradient(circle at top right, #ffa949, firebrick, dodgerblue)`
- As above, plus specificed colour stops: `radial-gradient(circle at top right, #ffa949 0%, firebrick 20%, dodgerblue 100%)`

It is also possible to layer a number of gradients on top of each other, or layer a gradient over a background image:
```
background: linear-gradient(#ffa949, transparent 60%),
            #ffa949 url('../img/mountains.jpg') no-repeat center;
```


## Layout Techniques
### CSS Reset with Normalize
- Any browser will apply its own defaults with the User Agent Stylesheet to any webpage, before other styles are applied.
- As the defaults for things like margins, padding, line-height and font sizes are slightly different between different browsers, it is sensible practice to do a *CSS reset*, to ensure that your layout displays as consistently as possible across all browsers.
- A modern day alternative to a classic reset is using the *Normalize* approach ([more detail about this](http://nicolasgallagher.com/about-normalize-css/))

Download the [normalize.css](https://necolas.github.io/normalize.css/)

Other CSS reset methods
- [Eric Meyer’s Reset CSS](https://meyerweb.com/eric/tools/css/reset/)
- [Popular CSS resets, all in one place](https://cssreset.com/)


### Layout Wrapper
A *wrapper* (or *container*) is commonly used to center a layout on the page. The wrapper keeps a layout from looking too wide or too narrow depending on the device or viewport width.

![Wrapper diagram](https://github.com/minkaotic/front-end-notes/blob/master/wrapper_diagram.png)

Using a wrapper `div` to contain the other elements on the page:

```
.wrapper {
  width: 70%;       /*prevents the layout from stretching too wide*/
  margin: 0 auto;   /*setting L+R margins to auto centres the wrapper in the browser*/
}
```
- Depending on the desired design, you can use this wrapper around all contents of the site, or just around the main contents, leaving the header and footer at 100% width.
- One approach for the latter layout is to create a wrapper around the main content and, optionally, an inner wrapper for the content inside the header and footer (if they have significant amounts of content which you'd like to align with the main content). Note that all of these wrappers can use the same class name (e.g. `container`) as they will need to have the same `width` and `margin` rules applied to them.

#### Creating a sticky Footer
*Basic method:* With a `<div class="wrap">` container around all content *but* the footer, do:
```
.wrap {
  min-height: calc(100vh - [height of footer]px);
}
```
- `vh` is a relative unit referring to the viewport, with `100vh` making an element the full width of the viewport (screen).
- If you still see a gap below the footer in browsers like Firefox and IE, or when you change the browser's zoom, give .main-footer a height or min-height value of `[height of footer]px`.


### Display Modes
Most common values for the `display` property, and elements defaulting to that display mode:

| Block          | Inline     | Inline-block  |
|----------------|------------|---------------|
| `h1`, `h2` etc | `span`     | `img`         |
| `p`            | `a`        |               |
| `div`          |            |               |
| `ol`/`ul`/`li` |            |               |

- `block` span the entire width of their container, forcing all subsequent elements to the next line

- `inline` elements  only span the width of their contents, allowing any inline level element to flow up next to it on the same line. ***NB:** width and height properties, or top/bottom margin or padding settings won't be applied to inline elements*; only left/right margins and padding will work.

- `inline-block` is useful in cases when we want items to appear next to each other, but still want top/bottom margin to be applied as if the whole set was a block element 

:sparkles: Interesting article on leveraging the display mode as an alternative to using floats: "[The Secret To Designing Website Layouts Without CSS Floats]( https://www.webdesignerdepot.com/2014/07/the-secret-to-designing-website-layouts-without-css-floats/)" :sparkles:

#### Gotchas when using inline-block to lay out columns

##### Gaps between inline/inline-block elements

The browser interprets the line breaks and spaces in the HTML as content, and adds spaces between elements displayed inline and inline-block, just like it adds spaces between words.

The size of the gap is commonly `4px`, but depends on the element's font size too - the larger the font size, the larger the gap. You can remove the gaps by either:
- applying a small, negative right margin to the elements: `margin-right: -4px;`
- setting `font-size: 0;` on the parent element - this makes the size of the space zero as well. You'll then need to set the font size of the inline-block child elements back to your desired size.

##### Columns aren't top-aligned

Since the default vertical alignment for inline(-block) items is `baseline`, the lack of top-alginment will become visible in columns that are different height. To change this behaviour, set the column `div`s to `vertical-align: top;`.

#### Nifty examples
- `li { display: inline; }` to keep list items next to each other on one line, then use padding and margin to neaten up visually (for more about list manipulation, see: https://teamtreehouse.com/library/lists-5)
- Setting an `<a>` element's display value to block makes its hover area expand within its parent (nicer for clickability) and lets you apply top and bottom padding values.

### Floats
Floats are one of the most commonly used methods for laying out a page with CSS. When an element is floated, the element is taken out of the normal flow of the page and placed along the left or right side of its container, causing other elements to wrap around it.

- First, change the element's `width` to something less than 50% (just like width, floats are relative to the parent container!)
- **`float: right`** will float something to the right, vice versa for left

**Common issues:** If a block element contains floated children, its height will collapse, causing elements to overlap where they shouldn't... options for resolving this:
- Add `overflow: auto;` for the parent element. Possible downsides: in some browsers, unwanted scroll bars might appear, or bits of content might be cut off
- **Clearfix** is the most reliable way to prevent these issues! - Targeting the parent element of the elements that are floated, it looks like this: 

```
[parent selector]:after {
  content: "";
  display: table;
  clear: both;
}
```
- often, a new `.group` class is used for clearfix, which can be assigned to any parent requiring it
- cf. https://developer.mozilla.org/en-US/docs/Web/CSS/clear and http://nicolasgallagher.com/micro-clearfix-hack/


________________________________________
