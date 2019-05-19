# CSS Notes

## Contents
- **[Basics](#basics)**
- **[Selectors](#selectors)**
- **[Rule Precedence](#rule-precedence)**
- **[Text & Fonts](#text--fonts)**
  - [Web fonts](#web-fonts)
- **[The CSS Box Model](#the-css-box-model)**
  - [Borders](#borders)
  - [Margin, padding, width and box-sizing](#margin-padding-width-and-box-sizing)
  - [Min-Height/Weight & Max-Height/Weight](#min-heightweight--max-heightweight)
  - [The calc() function](#the-calc-function)
  - [Why margins collapse](#why-margins-collapse)
- **[Colour & Background Images](#colour--background-images)**
- **[Fancy Design](#fancy-design)**
   - [Shadow effects](#shadow-effects)
   - [Rounded corners](#rounded-corners)
   - [Gradients](#gradients)
- **[Advanced CSS Snippets](#advanced-css-snippets)**

______________________

## Basics
- To include a stylesheet in your page, you typically link it in the `head` of the HTML. You can either link to a file in your project or to a file hosted elsewhere:
  ```html
  <head>
    <title></title>
    <link href='https://fonts.googleapis.com/css?family=Varela+Round' rel='stylesheet' type='text/css'>
    <link href='styles/main.css' rel='stylesheet' type="text/css">
  </head>
  ```
- A **CSS rule** is comprised of a *selector*, and a *declaration block* containing one or more declarations; each declaration contains a *property* and its chosen value.
- A comment is denoted by `/* ....... */`
- **Don't repeat yourself:** If you find that a certain style declaration is repeated in lots of different rules, it might be worth breaking out a different class rule for it.


## Selectors
- A **universal selector** can be used via the `*` character
- **Type** or **element selectors** like `h1` or `p` will target all elements of a given HTML tag - good for defining defaults
- **Id selectors** like `#intro-text` target the specific html element that has that id in its attributes (NB: elements can only have one id, and ids have to be unique)
- **Class selectors** like `.primary-content` target all html elements with that class in their attributes (NB: elements can have multiple classes)
- **Descendant selectors** like `.primary-content p` can be made up of two or more selectors and will target all elements that match that relationship, e.g. all "paragraphs" within any elements marked by the "primary-content" class
- **Pseudo-classes** like `:link` `:visited`, `:hover` or `:first-child:` target elements dynamically based on user interaction or an element’s special state
- **Pseudo-elements** like `::before` or `::after` for advanced styling needs (*NB:* as of CSS3 all pseudo-elements need to use the `::` syntax, as opposed to `:` used in older versions, to differentiate them from pseudo-classes.)

> *Multiple selectors*, separated by commas, can be used in a rule, such as `.primary-content, .secondary-content`

### Attribute selectors
- `[class] {...}` - target all elements with a class attribute
- `[class="form-contact"] {...}` - target all elements with a class attribute of value "form-contact"
- `form[class="form-contact"] {...}` - target all `form` elements with a class attribute of value "form-contact" (equivalent to `.form-contact`)
- `div[id="container"] {...}` - target all `div` elements with an id attribute of value "container" (equivalent to `#container`)

> Attribute selectors can be slower to interpret than class or element selectors, and the are less readable. Their main purpose is for styling form elements, i.e., styles for specific "type" attributes, such as `input[type="email"] {...}`


## Rule Precedence
- The **cascade** determines which styles are assigned to a HTML element; follows 3 main steps to determine which rule to apply:
  - **Importance:** User agent styles < User styles < Author styles
  - **Specificity:** Styles with more specific selectors will override styles with less specific selectors: universal selector < element selectors < class selectors < id selectors < inline styles
  - **Source order:** If there are two or more conflicting declarations within the same rule or level of specificity, the one appearing latest in the source takes precedence. (If there are multiple style sheets, the one linked in last takes precedance.)

- **Inheritance:** if no specific rules are in place for them, elements will inherit the style values of their parent element.

### Some more detail on Specificity
- **Exceptions:** When **`!important`** is used on a style declaration, this declaration overrides any other declarations. *This is bad practice and should be avoided.* 

- **When using descendant selectors**, the selector with the most IDs in it takes precendence; if they are equal, then the selector with the greatest number of classes, attributes & pseudo-classes, and if these are equal too, then the selector with the highest number of elements (incl. pseudo elements).
  - Use this [Specificity Calculator](https://specificity.keegan.st/) if in doubt about any two selectors :).

As with any other specificity calculations, if there are two `!important` rules, or two descendant selectors with the same specificity, then the decision is made on source order.


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
```css
@font-face {
  font-family: 'Abolition Regular';
  src: url('../fonts/abolition-regular-webfont.eot');
  src: url('../fonts/abolition-regular-webfont.eot?#iefix') format('embedded-opentype'),
       url('../fonts/abolition-regular-webfont.woff') format('woff'),
       url('../fonts/abolition-regular-webfont.ttf') format('truetype');
}
```

## The CSS Box Model

![CSS Box Model](https://github.com/minkaotic/front-end-notes/blob/master/img/box_model.png)

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

### Min-Height/Weight & Max-Height/Weight
- `max-width`/`min-width` will override `width` (same for `height`, of course)
- **By contrast**, `width`/`height` will *only* affect the element if they are *within the previously specified `min` or `max` values!*

*Continue reading here: https://css3-tutorial.net/dimensions/min-width-max-width-min-height-max-height/*


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
```css
background: linear-gradient(#ffa949, transparent 60%),
            #ffa949 url('../img/mountains.jpg') no-repeat center;
```

________________________________________

## Advanced CSS Snippets

To apply some logic to all but the first sibling, `.item-class:not(:first-child)` can be used. In the following example, this is used to apply some pipe separators between a list of inline items:

```css
.item-class:not(:first-child) {
  border-left: 1px #d7d7d7 solid;
  padding-left: 20px;
  margin-left: 15px;
}
```
