# Positioning things in CSS

A session on layout, placement, and generally moving things around in CSS, using the challenge below as an example:
https://www.frontendmentor.io/challenges/github-user-search-app-Q09YOgaH6

Format: code-along
Artifact: cheat sheet (either below or separate doc) to refer back to

**CONTENTS**
1. Understanding display modes
2. The CSS box model
3. Different layout techniques & when to use them
4. Flexbox basics

----------------------------------------------------------------

## 1. Understanding display modes
...and how they affect positioning of elements

## Display Modes

- TODO: explain `display` property
- All HTML elements have a default, for most elements this is `block` or `inline`:

| Block          | Inline     | Inline-block  |
|----------------|------------|---------------|
| `h1`, `h2` etc | `span`     | `img`         |
| `p`            | `a`        |               |
| `div`          |            |               |
| `ol`/`ul`/`li` |            |               |

- `block` elements span the entire width of their container, forcing all subsequent elements to the next line
- `inline` elements  only span the width of their contents, allowing any inline level element to flow up next to it on the same line.
  - ***NB:** width and height properties, or top/bottom margin or padding settings won't be applied to inline elements*; only left/right margins and padding will work.
- `inline-block`'s main two differences vs. `inline` is that it allows to set a width and height on the element, and that the top and bottom margins/paddings are respected.
- need different ways to centre it
- can simply change the display mode if desired! (Better than using a less semantically appropriate element to achieve the desired result) 

-> demonstrate these differences!

:sparkles: Display mode can be leveraged as an alternative to using floats: "[The Secret To Designing Website Layouts Without CSS Floats]( https://www.webdesignerdepot.com/2014/07/the-secret-to-designing-website-layouts-without-css-floats/)" :sparkles:


-> Common techniques for aligning each of these
-> How to use a layout wrapper

## 2. The CSS box model


- common units

## 3. Different layout techniques & when to use them
- Floats
- Flexbox
- CSS Grid
- CSS Positioning

## 4. Flexbox basics

