# Notes & Learnings about Front End Development
Based on https://teamtreehouse.com/tracks/front-end-web-development

## Table of Contents


## HTML learnings
- A comment is denoted by `<!-- ...... -->`
________________________________________

## CSS learnings
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


### Rule overriding
- Rules for id selectors will override rules for any other selectors


### Fonts
- Create a **font stack** to make sure we have fallbacks of *websafe fonts* as well as *generic font families* defined in case our desired font doesn't work on a given machine
- When using **`font-family`** with multi-word name, use " "s


### The Box Model
(**Also see diagram attached!**)

- Most common values for the `display` property are `block` (creating a new line after element), `inline` (not breaking into a new line), and `inline-block`
- `inline-block` is useful in cases when we want items to appear next to each other, but still want top/bottom margin to be applied as if the whole set was a block element 
- `li { display: inline; }` to keep list items next to each other on one line, then use padding and margin to neaten up visually





Text
------
- use `text-decoration: none;` to get rid of underlines on links
- the default `font-weight` of headlines is bold
- use **font** property as shorthand to specify weight, size (obligatory), line height and family (obligatory), eg.: `font: normal 1em/1.5 "Helvetica Neue", Helvetica, Arial, sans-serif;`
- **`em`**s are relative to parent element's pixel size, but the default of 1 "em" is 16px (which is the value of em at the root value) 
- **`rem`**s are relative to root element's pixel size, i.e. avoid compounding issues when sizing up or down
- **`line-height`** (takes unit-less values like 1.5 or 2)
____________________________________________

Colour
-------
Colours can be set as either:
- **keyword values**, e.g. `orange`
- **hexadecimal values**, e.g. `#fff or #878787`
- or **rgb functions**, e.g. `rgb(255, 169, 73)`

In addition, **rgba functions** allow setting transparency via alpha value, eg. `rgba(255, 255, 255, .5)`
____________________________________________

Box model elements
-------------------------
- **border shorthand**: 'border: [width] [style] [color]' - or do each of them individually for control over each side, eg.: `border-width: 10px 20px`, or `border-top: 2px solid lightgrey;`
- When using **2 value shorthand**, the first value refers to top/bottom and the second to left/right.
- When using **3 value shorthand**, the values refer in order to: TOP, LEFT/RIGHT, BOTTOM
- **`margin: auto`** will generally **centre** content on the page!
- `width` values provided as **percentages** are applied in relation to the *parent container* - and `width` generally applies only to the *content* of the box, i.e. not including its padding and border, however...
- **`box-sizing: border-box`** dynamically subtracts the borders and paddings of the element from the width and height properties we set, making it easier to define flexible widths and heights in our project (it's one of the few good uses for the universal selector!) *
- `max-width` sets the maximum width of an element, preventing elements to become too large to look good on big screens; when set as percentage values can also be used as part of responsive design *

(* for more on `box-sizing` and `max-width` see https://teamtreehouse.com/library/boxsizing-and-maxwidth)
____________________________________________

Manipulating the background
-----------------------------------
- Every HTML element has a background layer that is transparent by default, but can be filled using `background-image` or `background-color`
- By default, `background-image`s are tiled and repeated
- `background-size: cover` adjusts the background area so that it's **completely covered by the background image** (if using), while maintaining its width and height proportions
- Best practice: set background colour as well when using background images, to preserve the contrast between the background and content in case the image isn't available
- Handy all-in-one **background shorthand:** `background: #ffa949 url('../img/mountains.jpg') no-repeat center / cover;`
____________________________________________

Floats
--------
- First, change the element's `width` to something less than 50% (just like width, floats are relative to the parent container!)
- **`float: right`** will float something to the right, vice versa for left
- Common issues: If a block element contains floated children, its height will collapse, causing elements to overlap where they shouldn't...
- **Clearfix** is the most reliable way to prevent these issues! - Targeting the parent element of the elements that are floated, it looks like this: `[parent selector]:after {clear: both;}`
- cf. https://developer.mozilla.org/en-US/docs/Web/CSS/clear and http://nicolasgallagher.com/micro-clearfix-hack/
____________________________________________

Shadow effects
-------------------
- using either **`text-shadow:`** `[horizontal offset] [vertical offset] [blur radius] [colour]` or **`box-shadow`** (as text shadow, but with optional value of [spread] before the colour value)
- Example of a small bottom box-shadow: `box-shadow: 0 20px 10px -12px rgba(0,0,0, .8);`
- Nice inner shadow: `box-shadow: inset 0 0 50px 10px rgba(0,0,0, 1);`
_____________________________________________

Rounded corners
----------------------
- use `border-radius` - takes any absolute or relative length value (px, em, % etc.)
_____________________________________________

Gradients
------------
- add depth to designs by creating smooth and gradual transitions between two or more colours
_____________________________________________

Animations
-------------
- requires....
