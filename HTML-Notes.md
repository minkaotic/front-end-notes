# HTML Notes
**H**yper**t**ext **M**arkup **L**anguage provides the ***content layer*** of a webpage (*cf. CSS=presentation layer, JS=behaviour layer*) and forms its structural foundation. A webpage's HTML layer is sometimes referred to as *'template'*, especially if it is used in conjunction with frameworks like Angular or ASP.NET MVC.

### Contents
- **[Global structure of an HTML document](#global-structure-of-an-HTML-document)**
- **[Semantic HTML](#semantic-html)**
- **[Complex elements](#complex-elements)**
  - [Forms & inputs](#forms--inputs)
- **[SVGs](#svgs)**
  - [Adding SVGs to a web page](#adding-svgs-to-a-web-page)

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

- Comments in HTML starts with `<!--`, and ends with `-->`.

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


## Complex elements

### Forms & inputs
To create a **text input** with placeholder text:
```html
<input type="text" placeholder="cat photo URL">
```

*NB:* You can build **web forms** that actually submit data to a server purely using HTML. To do this, wrap the `input` element in a `form` element and specify an `action`. Then add a `button` of type `submit` to your form. Clicking this button will send the data from your form to the URL you specified with your form's `action` attribute.:
```html
<form action="/submit-cat-photo">
  <input type="text" placeholder="cat photo URL">
  <button type="submit">Submit</button>
</form>
```

To make an input field **required**, you can just add the attribute `required` within your input element: `<input type="text" required>`. When used in combination with a `button` inside a `form`, this will actually prevent the button from being clicked until the required field is filled in.


## SVGs
**Scalable Vector Graphics** (SVG) is an XML-based markup language for describing two-dimensional vector graphics. *SVG is essentially to graphics what HTML is to text.*

A ***vector graphic*** is composed of points in space (=vectors) each defined by an x- & y-coordinate, that are connected to create a shape. This means that, as opposed to raster graphics (like PNGs or JPGs), it won't become pixellated, no matter how much you zoom in.

**Tools for drawing & optimising vector graphics:**
- [Adobe Illustrator](https://www.adobe.com/uk/products/illustrator.html)
- [Method Draw](https://editor.method.ac/) (free online editor)
- [Ballpoint](https://ballpoint.io/) (free online editor)
- [SVG Edit](https://svg-edit.github.io/svgedit/releases/svg-edit-2.8.1/svg-editor.html) (free online editor)
- [SVGO](https://jakearchibald.github.io/svgomg/) (free online SVG optimiser; removes unneccesary metadata)

***SVG is a text-based open Web standard***, explicitly designed to work with other web standards such as CSS and DOM. SVG images and their related behaviors are defined in *XML text files* which means they can be searched, indexed, scripted and compressed. Additionally this means they can be created and edited with any text editor and with drawing software. 

**SVG or raster graphic??**
- If an image needs a great deal of variance in each pixel to render it properly (such as in a photograph or traditional artwork), storing the image as pixel data is more efficient than storing it as vector data.
- Typical uses cases for vector graphics include Vector logos, illustrations, technical drawings; but any image that can be drawn as a path by a computer is more efficiently stored as vector data.

### Adding SVGs to a web page
There are two different ways to do this: 
1. Use it just like a normal image file. All modern browsers will accept the SVG file format in the `<img>` element. SVGs can also be added as backround images in the same way as other image formats.
1. Embed SVG markup directly into HTML documents.

**Sources:**
- [MDN SVG Documentation](https://developer.mozilla.org/en-US/docs/Web/SVG)
- [SVG Basics on Treehouse](https://teamtreehouse.com/library/vector-graphics)
