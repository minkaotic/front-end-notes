# HTML Notes
**H**yper**t**ext **M**arkup **L**anguage provides the ***content layer*** of a webpage (*cf. CSS=presentation layer, JS=behaviour layer*) and forms its structural foundation. A webpage's HTML layer is sometimes referred to as *'template'*, especially if it is used in conjunction with frameworks like Angular or ASP.NET MVC.

### Contents
- [Global structure of an HTML document](#global-structure-of-an-HTML-document)
- [Semantic HTML](#semantic-html)
- [SVGs](#svgs)

--------------------------

## Global structure of an HTML document
```
<!DOCTYPE html>
<html>
  <head>
    <title>A Nice Webpage</title>
  </head>
  <body>
  </body>
</html>
```

**Further resources:**
- [What's in the head? Metadata in HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/The_head_metadata_in_HTML)
- [HTML elements reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)


## Semantic HTML
= markup that describes the *meaning* of content (as opposed to, say, how it looks). Benefits:
- makes a webpage more understandable to search engines
- makes it more accessible to users who rely on assistive technologies (screen readers etc.)

### Core elements
- `<h1>`, `<h2>`, up to `<h6>` - Headings
- `<p>` - Paragraphs
- Lists:
  - `<ul>` - Unordered list
  - `<ol>` - Ordered list
  - `<dl>` - [Description list](http://html5doctor.com/the-dl-element/) (used to create groups of terms and descriptions, such as a glossary)
- `<a href="http://a-nice-link.com" target="_blank">` - Anchor elements, i.e. links

### Elements for describing sections of content
- `<header>` - The top layer of a page, typically containing the site's logo, navigation, main heading and site description.
- `<footer>` - Typically contains information about the author of the section (or page), copyright data or links to related documents. A page can have more than one footer.
- `<section>` - A standalone [section](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/section) — which doesn't have a more specific semantic element to represent it — contained within an HTML document. The first element in a section should be its heading.
- `<article>` - 


## SVGs
**Scalable Vector Graphics** (SVG) is an XML-based markup language for describing two-dimensional based vector graphics. SVG is essentially to graphics what HTML is to text.

A ***vector graphic*** is composed of points in space (=vectors) each defined by an x- & y-coordinate, that are connected to create a shape. This means that, as opposed to raster graphics (like PNGs or JPGs), it won't become pixellated, no matter how much you zoom in.

**Tools for drawing vector graphics:**
- Adobe Illustrator
- [Method Draw](https://editor.method.ac/) (free online editor)
- [Ballpoint](https://ballpoint.io/) (free online editor)
- [SVG Edit](https://svg-edit.github.io/svgedit/releases/svg-edit-2.8.1/svg-editor.html) (free online editor)

***SVG is a text-based open Web standard***, explicitly designed to work with other web standards such as CSS and DOM. SVG images and their related behaviors are defined in *XML text files* which means they can be searched, indexed, scripted and compressed. Additionally this means they can be created and edited with any text editor and with drawing software. 




**Sources:**
- [MDN SVG Documentation](https://developer.mozilla.org/en-US/docs/Web/SVG)
- [SVG Basics on Treehouse](https://teamtreehouse.com/library/vector-graphics)
