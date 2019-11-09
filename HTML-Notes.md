# HTML Notes
**H**yper**t**ext **M**arkup **L**anguage provides the ***content layer*** of a webpage (*cf. CSS=presentation layer, JS=behaviour layer*) and forms its structural foundation. A webpage's HTML layer is sometimes referred to as *'template'*, especially if it is used in conjunction with frameworks like Angular or ASP.NET MVC.

### Contents
- **[Global structure of an HTML document](#global-structure-of-an-HTML-document)**
- **[HTML5](#html5)**
  - [Browser Compatibility](#browser-compatibility)
- **[Semantic HTML](#semantic-html)**
  - [Core elements](#core-elements)
  - [Elements for describing sections of content](#elements-for-describing-sections-of-content)
- **[Complex elements](#complex-elements)**
  - [Forms & inputs](#forms--inputs)
  - [HTML tables](#html-tables)
  
--------------------------

## Global structure of an HTML document
```html
<!DOCTYPE html>
<html>
  <head>
    <title>A Nice Webpage</title>
  </head>
  <body>
  </body>
</html>
```

- Comments in HTML start with `<!--`, and end with `-->`.

**Further resources:**
- [What's in the head? Metadata in HTML](https://developer.mozilla.org/en-US/docs/Learn/HTML/Introduction_to_HTML/The_head_metadata_in_HTML)
- [HTML elements reference](https://developer.mozilla.org/en-US/docs/Web/HTML/Element)

--------------------------

## HTML5
- Opera & Mozilla started WHATWG (Web Hypertext Application Technology Working Group) as they were frustrated with slow evolution of HTML, and proposed the HTML5 standard to the W3C in 2011.
- This standard was adopted, but the W3C and WHATWG definitions of of HTML5 have drifted, with the former defining it as a living standard subject to constant evolution

### Browser Compatibility
- Most browsers treat unrecognised tags as generic `<div>` tags
- there is also a "famous" html5shiv.js polyfill for older browsers

> :bulb: **[Progressive Enhancement](https://en.wikipedia.org/wiki/Progressive_enhancement)** is a strategy for web design that emphasizes core webpage content first. This strategy then progressively adds more nuanced and technically rigorous layers of presentation and features on top of the content as the end-user's browser/internet connection allow.

More resources:
- [Chris Northwood: The Full Stack Developer](https://www.amazon.co.uk/Full-Stack-Developer-Essential-Everyday/dp/1484241517)
- https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5
- https://en.wikipedia.org/wiki/HTML5

--------------------------

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

*[to be continued...]*

--------------------------

## Complex elements

### Forms & inputs
- [Web forms 101](#web-forms-101)
- [Logically grouping form sections](#logically-grouping-form-sections)
- [Select menus](#select-menus)
- [Radio buttons & checkboxes](#radio-buttons--checkboxes)
- [HTML5 form validation](#html5-form-validation)

#### Web forms 101
> :bulb: You can build **web forms** that actually submit data to a server purely using HTML.

The `<form>` element wraps a section of the document that contains form controls. It takes two attributes: `action`, which specifies the web address to send the data to on submission, and `method`, which specifies the HTTP method to use. For example: 
```html
<form action="index.html" method="post"></form>
```

The `<input>` element is used to create many different types of form controls. Its `type` attribute specifies what kind of form control should be rendered, e.g. `text`, `email`, `password`, etc. The `name` attribute is submitted with form data so that server-side code can parse the information. The `id` attribute works like `id` elsewhere, but additionally is used to associate a `<label>` to a specific form control, e.g.:
```html
<label for="mail">Email address:</label>
<input type="email" id="mail" name="user_email">
```

Finally, add a `<button>` of type `submit` to your form. (The type attribute specifies whether the button should `submit` the form data, `reset` the form, or - `button` - have no default behavior for use with JavaScript.) Clicking this button will send the data from your form to the web address specified with your form's `action` attribute.
```html
<form action="/submit-cat-photo" method="post">
  <label for="photo-url">Cat pic:</label>
  <input type="text" id="photo-url" name="photo_url" placeholder="cat photo URL">
  <button type="submit">Submit</button>
</form>
```

#### Logically grouping form sections
Sometimes, certain form controls belong together in a logical grouping. Form controls can be grouped together using `<fieldset>` elements and then labeled using a `<legend>`.

The `<fieldset>` element wraps multiple form elements into common groups. This can help organize a form and make it easier to understand for users. The `<legend>` element is similar to the label element, but instead of labeling a form control, it labels a `<fieldset>`, providing helpful context for users that are filling out a form.

##### Example:
```html
<form action="index.html" method="post">
  <h1>Sign Up</h1>
  <fieldset>
    <legend>Your basic info</legend>
    <label for="name">Name:</label>
    <input type="text" id="name" name="user_name">
    <label for="mail">Email address:</label>
    <input type="email" id="mail" name="user_email">
  </fieldset>
  <fieldset>
    <legend>Your profile</legend>
    <label for="bio">Bio:</label>
    <textarea id="bio" name="user_bio"></textarea>
  </fieldset>
  <button type="submit">Sign Up</button>
</form>
```
This will create the following form:
![fieldset example](/img/fieldset-example.png)

#### Select menus

The [`<select>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/select) element renders a drop-down menu that contains selectable options. This type of form control is ideal for scenarios where the user must choose one option from a preset list of 5 or more choices. The [`<option>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/option) element represents one of the choices that a user can choose in a select menu. It should always be nested inside of a `<select>` element. The [`<optgroup>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/optgroup) element wraps one or more `<option>` elements and helps to create logical groups. The `label` attribute specifies the text that the `<optgroup>` should display above the nested options.

##### Example:
```html
<select id="job" name="user_job">
  <optgroup label="Web">
    <option  value="frontent_developer">Front-End Developer</option>
    <option  value="backend_developer">Back-End Developer</option>
    <option  value="web_designer">Web Designer</option>
    <option  value="wordpress_developer">WordPress Developer</option>
  </optgroup>
  <optgroup label="Mobile">
    <option  value="android_developer">Android Developer</option>
    <option  value="ios_developer">iOS Developer</option>
    <option  value="mobile_designer">Mobile Designer</option>
  </optgroup>
  <optgroup label="Business">
    <option  value="business_owner">Business Owner</option>
    <option  value="freelancer">Freelancer</option>
  </optgroup>
</select>
```
> :bulb: The `<option>`'s **`value`** attribute specifies the value of the selected option to be sent to the server on form submission.


#### Radio buttons & checkboxes
If the user only needs to choose from 5 or fewer options, it's typically better to use **radio buttons** instead of a select menu.
A group of radio buttons is created by a group of several `<input>` elements of type `radio`.
> NB: *In order to group radio buttons together and allow only one at a time to be selected, they must all share the same value for the `name` attribute.*

##### Example - 2 radio buttons under a header label
```html
<label>Age:</label>
<input type="radio" id="under_13" value="under_13" name="user_age">
<label for="under_13" class="light">Under 13</label><br>
<input type="radio" id="over_13" value="over_13" name="user_age">
<label for="over_13" class="light">13 or older</label>
```

**Checkboxes**, where multiple options can be selected at once are created similarly to radio buttons, but use `<input>` elements of type `checkbox`.

##### Example - 3 checkboxes under a header label
```html
<label>Interests:</label>
<input type="checkbox" id="development" value="interest_development" name="user_interest">
<label for="development" class="light">Development</label><br>
<input type="checkbox" id="design" value="interest_design" name="user_interest">
<label for="design" class="light">Design</label><br>
<input type="checkbox" id="business" value="interst_business" name="user_interest">
<label for="business" class="light">Business</label>
```

#### HTML5 form validation
HTML5 has a number of built in form validations available, which can be described as constraints using a range of [validation attributes](https://developer.mozilla.org/en-US/docs/Web/Guide/HTML/HTML5/Constraint_validation#Validation-related_attributes).

Validation attributes allow specifying rules for a form input, for example:
- whether a value must be filled in (`required`)
- the minimum and maximum length of the data (using `minlength` and `maxlength` attributes)
- whether the data needs to be a number, an email address, or something else (using `type` attribute)
- a pattern that the data must match (`pattern` attribute)

**Example 1:** To make an input field **required**, you can just add the attribute `required` within your input element: `<input type="text" required>`. When used in combination with a `button` inside a `form`, this will actually prevent the button from being clicked until the required field is filled in.

**Example 2:** To specify a **valid pattern** for the input, use the `pattern` attribute with a regex:
```html
<form>
  <label for="choose">Would you prefer a banana or cherry?</label>
  <input id="choose" required pattern="banana|cherry">
  <button>Submit</button>
</form>
```

**Example 3:** To validate by **input type**:
```html
<form>
  <input required type="email">
  <button>Submit</button>
</form>
```

###### When an element is valid:
- The element matches the `:valid` CSS pseudo-class, which lets you apply a specific style to valid elements
- If the user tries to send the data, the browser will submit the form, provided there is nothing else stopping it from doing so (e.g., JavaScript).

###### Likewise, when an element is invalid:
- The element matches the `:invalid` CSS pseudo-class, which lets you apply a specific style to invalid elements.
- If the user tries to send the data, the browser will block the form and display an error message.

#### Drawbacks to HTML5 form validation
Using HTML form validation means that the way the error message is displayed depends on the browser. Two problems with this:
- There is no standard way to change their look and feel with CSS.
- Error messages depend on the browser locale, which means that you can have a page in one language but an error message displayed in another language.

![Illustration of browser variance when using html5 form validation](/img/html-form-validation.png)

**Further resources on forms & inputs:**
- FreeCodeCamp on HTML forms, starting from [this section of the syllabus](https://learn.freecodecamp.org/responsive-web-design/basic-html-and-html5/create-a-form-element/)
- [MDN tutorial on form validation](https://developer.mozilla.org/en-US/docs/Learn/HTML/Forms/Form_validation)

__________________________

### HTML Tables
> :exclamation: Tables should only be used for displaying tabular data, and never for page layout.

#### Table elements
- [`<table>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/table) - Root element of a table; represents data in a series of rows and columns.
- [`<tr>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/tr) - The *table row* element defines a row of cells in a table. Table rows can be filled with table cells and table header cells.
- [`<td>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/td) - The *table data* element represents a single table cell. Each table cell should be inside a table row.
- [`<th>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/th) - The *table header* cell helps label a group of cells in either a column or a row. The nature of this group can be defined with the `scope` attribute, e.g. `scope="col"` or `scope="row"`.

> :bulb: Columns are implicit, and are simply emergent from how many cells are in each row.

##### Table elements that are not required, but are nice to haves for accessibility (screen readers), SEO, and styling:

- [`<caption>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/caption) - A title or brief description of the table; always appears immediately after the opening `<table>` tag.
- [`<thead>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/thead) - Wraps a set of rows that make up the header of a table.
- [`<tbody>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/tbody) - Defines one or more rows that make up the primary contents (or "body") of a table.
- [`<tfoot>`](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/tfoot) - The table footer element contains one or more rows summarizing the columns of the table. This might be totals for columns of numerical data, or meta information about the table.
  - it can be placed after `<thead>` (allows to load the table footer before the table body data is loaded) or after `<tbody>`
  - the `colspan` attribute can be used to make the footer cell(s) span across multiple columns, e.g. `colspan="3"`.

##### Example:
```html
    <table>
      <caption>Employee Information</caption>
      <thead>
        <tr>
          <th scope="col">Name</th>
          <th scope="col">E-mail</th>
          <th scope="col">Job role</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <th scope="row">Paul</th>
          <td>paul@example.com</td>
          <td>Master chef</td>
        </tr>
        <tr>
          <th scope="row">Roger</th>
          <td>roger@example.com</td>
          <td>Chicken tester</td>
        </tr>
        <tr>
          <th scope="row">Elsie</th>
          <td>elsie@example.com</td>
          <td>Duster</td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td colspan="3">Data is updated every 15 minutes</td>
        </tr>
      </tfoot>
    </table>
```

This will produce a table like this:

![table made with html](/img/table-example.png)
