# Using SVGs

### Contents
- [SVG basics](#svg-basics)
- [Different ways of adding SVGs to a web page](#different-ways-of-adding-svgs-to-a-web-page)
- [Styling SVGs with CSS](#styling-svgs-with-css)

## SVG basics
**Scalable Vector Graphics** (SVG) is an XML-based markup language for describing two-dimensional vector graphics. *SVG is essentially to graphics what HTML is to text.*

A ***vector graphic*** is composed of points in space (=vectors) each defined by an x- & y-coordinate, that are connected to create a shape. This means that, as opposed to raster graphics (like PNGs or JPGs), it won't become pixellated, no matter how much you zoom in.

**Tools for drawing & optimising vector graphics:**
- [Adobe Illustrator](https://www.adobe.com/uk/products/illustrator.html)
- [Sketch](https://www.sketchapp.com/)
- [Inkscape](https://inkscape.org/) (free software)
- [Method Draw](https://editor.method.ac/) (free online editor)
- [Ballpoint](https://ballpoint.io/) (free online editor)
- [SVG Edit](https://svg-edit.github.io/svgedit/releases/svg-edit-2.8.1/svg-editor.html) (free online editor)
- [SVGO](https://jakearchibald.github.io/svgomg/) (free online SVG optimiser; removes unneccesary metadata)

***SVG is a text-based open Web standard***, explicitly designed to work with other web standards such as CSS and DOM. SVG images and their related behaviors are defined in *XML text files* which means they can be searched, indexed, scripted and compressed. Additionally this means they can be created and edited with any text editor and with drawing software. 

**SVG or raster graphic??**
- If an image needs a great deal of variance in each pixel to render it properly (such as in a photograph or traditional artwork), storing the image as pixel data is more efficient than storing it as vector data.
- Typical uses cases for vector graphics include Vector logos, illustrations, technical drawings; but any image that can be drawn as a path by a computer is more efficiently stored as vector data.

## Different ways of adding SVGs to a web page
**Three different ways:**
1. **Image:** Use it just like a normal image file. All modern browsers will accept the SVG file format in the `<img>` element. SVGs can also be added as background images in the same way as other image formats.
1. **Inline:** Embed SVG markup directly into HTML documents. This allows to access and style parts of the SVG with CSS.
1. **Object:** Embed SVG using the HTML `object` element - allows for browser caching *as well as* applying styling, but is more fiddly in assigning the right stylesheet and often not worth the resulting maintainability cost.

    ![3 Modes of SVG](https://github.com/minkaotic/front-end-notes/blob/master/img/3-ways-with-svgs.png)
  *Source: [Front End Center — Why Inline SVG is Best SVG](https://www.youtube.com/watch?v=af4ZQJ14yu8)*

**Performance considerations:**
- embedding into HTML will reduce the number of HTTP requests required to load the page
- however, directly embedded SVGs will not be cached by the browser like other images, so will need to be reloaded every time
- therefore, directly embedded SVGs should have a small file size

**Manageability:**
- stylesheets might affect SVGs that they shouldn't, and it can become hard to track what styles are applied to which SVGs.

> **Ideally add SVGs like a normal image, and only embed them if you absolutely have a requirement to style them.**

## Styling SVGs with CSS
- Make parts transparent with `opacity` and `stroke-opacity` (value between 0 and 1)
- Define the fill colour with `fill`
- Make things bolder with `stroke-width` - this can be useful for smaller screen sizes when styling responsive SVGs, as thicker stroke-widths can help lower resolution SVGs to retain detail and make it appear more iconographic.

**More resources:**
- [MDN SVG Documentation](https://developer.mozilla.org/en-US/docs/Web/SVG)
- [Front End Center — Why Inline SVG is Best SVG](https://www.youtube.com/watch?v=af4ZQJ14yu8)
