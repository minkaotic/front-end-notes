# SASS Notes
## Contents
- [The Powers of Sass](#the-powers-of-sass)
- [Compiling a Directory of Sass Files](#compiling-a-directory-of-sass-files)

__________________

## The Powers of Sass
[Sass](http://sass-lang.com/) is a stylesheet language that extends CSS with features like **variables**, **nested rules**, **mixins** and **functions**, in a CSS-compatible syntax. A stylesheet written in Sass needs to be compiled into plain CSS before the browser can read it.

- Store values in variables you can reference anywhere in your stylesheet
- Compose reusable blocks of styles that can be shared with other rule sets
- Split styles into partials to make styles more modular and easier to maintain

**> [Sass Installation options](http://sass-lang.com/install)**

**Two Syntaxes**
- "Indented Syntax" using file ending `.sass` - the original syntax; not compatible with regular CSS
- "Sassy CSS" using file ending `.scss` - the latest generation of Sass; *CSS-friendly syntax*, i.e. any regular CSS is still valid in SCSS


## Compiling a Directory of Sass Files
You'll usually instruct Sass to auto-compile a directory of Sass files into one output CSS file. To watch an input directory called *scss* and generate the compiled output into a directory called *css*, run:
```
sass --watch scss:css
```
