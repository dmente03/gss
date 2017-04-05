![Logo of Guava Stylesheet Standards](https://guava.com.br/images/gss/gss.svg)

GSS is a module-based methodology to CSS structuration with a human-friendly syntax. It aims to facilitate the process of understanding, naming and organizing CSS. This way, it’s easier to develop and maintain stylesheets, from small to big projects.

It's heavily inspired by a lot of great ideas, like [Atomic Design](http://atomicdesign.bradfrost.com/), [SMACSS](https://smacss.com/), [mdo's Code Guide](http://codeguide.co/), [Semantic UI](http://semantic-ui.com/) and so on.

## What it feats

- Modular styling.
- Simplicity and readability above everything.
- Easy recognition and debug of which module you are working on.
- Seamless maintainability of code.
- Structure that leverages the power of cascading stylesheet.

## How it works
GSS is based on four main ideas:
1. An element is shaped by _Attribute_ classes;
2. _Base_ HTML elements and styles comes first.
3. The overall UI is formed by _Modules_ — reusable and functional block of UI components.
4. Specific and non-reusable styles are categorized as _Pages_.

### Stylesheet organization
![GSS categories. Icon created by Oliviu Stoian from the Noun Project](https://guava.com.br/images/gss/intro.svg)

## Attributes
The core idea of GSS is the use of _Attribute_ classes. They define and categorize the components — be it an simple HTML element, a Module or even a Page. For example, you can set default styles for a `p` element, and then creates a variation of it, like `p.is-lead`
_Attributes_ prefixed by a verb/preposition, which leads to a more natural and contextual naming scheme; they can be named in a wide variety of ways: purpose, appearance, behavior, dependence, relationship, context and so on.

Examples of Attributes classes | Type
------------------------------ | ----
`.of-login` | _Relationship_
`.is-submit` | _Purpose_
`.is-large` | _Appearance_
`.has-icon` | _Dependence_
`.is-submiting` | _Behavior_

## Base
![Base. Icon created by ProSymbols from the Noun Project](https://guava.com.br/images/gss/base-small.svg)

Defaults and styles of HTML and UI elements goes here. They are the most basic styles of every project. Its properties are applied using an element selector and/or an _Attribute_ class. _Base_ styles are categorized by:

* Colors: variables sorted by name and semantic purpose.
* Forms: inputs, fieldsets, buttons, etc.
* Tables: tables, cells, its rows and columns.
* Typography: headers, paragraphs, links, lists, labels, etc.

![Example of a post](https://guava.com.br/images/gss/post.svg)

## Modules
![Modules. Icon created by Lluisa Iborra from the Noun Project](https://guava.com.br/images/gss/modules-small.svg)

Reusable and functional block of UI components that forms the bulk of any project. Sometimes, a Module can sit within other Module, but oftentimes they are a group of Base elements in which you only need to put classes on the parent. They are prefixed its own name as a class, which is named just like the parent Module (e.g., `.card` for `cards` Module).

![Example of a card](https://guava.com.br/images/gss/card.svg)

![Example of a dropdown. Icons: profile by Ananth; settings by Leonides Delgado; and logout by Andrea Greco; all from the Noun Project](https://guava.com.br/images/gss/dropdown.svg)

![Example of a menu. Icons: graph by Jian Wei; people by Gregor Cresnar; projects by chinnan; all from the Noun Project](https://guava.com.br/images/gss/menu.svg)

## Pages
![Pages. Icon created by Melvin Salas from the Noun Project](https://guava.com.br/images/gss/pages-small.svg)

Context and page-specific styles that can’t be reused or alocated within a Module. These styles classes must be prefixed with `.page-`.

![Example of a page theme](https://guava.com.br/images/gss/page-theme.svg)

## Naming principles
- Use of `lisp-case` for naming classes. All lowercase.
- Words separated by a single hyphen (never double).
- _Modules_ and _Attributes_ are separated with a space in the HTML markup.
- Different _Modules_ in a same HTML element are separated by a slash (e.g., `<span class="icon of-submit / motion of-submit>`) for visual convenience.

## Everything in its right place

### Base files
Base styles | Description
----------- | ----------
`base/colors` | Colors, sorted by name and semantic purpose (e.g., `blue` and `primary`)
`base/forms` | Inputs, fieldsets, buttons, etc
`base/tables` | Table header, body and footer layouts; cells, rows and columns
`base/typography` | Headers, paragraphs, links, lists, labels, etc
`base/utils` | Functions, placeholders and uncategorized mixins (for Sass and LESS)

### Modules files (examples)
Examples of _Modules_ | Description
------------------- | ---------------
`alerts` | Alerts and notifications
`articles` | Articles layouts
`cards` | Content displayed in a manner similar to a playing card
`dropdowns` | Allows a user to select a value from a series of options
`figures` | Images, illustrations, infographics
`footers` | Footers layouts
`graphs` | Graphic visualizations for dynamic and interactive data
`grid` | Dimensions, rows, containers, alignments, columns, ordering, etc
`headers` | Headers layouts
`icons` | Iconography
`logos` | Logos and its variations
`menus` | Menu layouts
`motion` | Keyframes, triggers and special mixins for UI animation
`overlays` | Modals, popovers and other things that overlays basic UI
`sections` | Special sections layouts
`sidebars` | Asides and secondary pieces of content
`…` | …

### Dealing with vendors
The open source world is vast and vibrant. In order to deal with these huge amount of awesomeness, it's prudent to specify what you relies on and overwrites over. GSS does this by separating the overwrites into its own folder and files. These style classes must be prefixed with `.vendor-`.

### Pluralization rules
The naming scheme of classes and files is: if it's a file, then is plural; if it's a Base/Module class name, then is singular.

### Folders
Folder | Description
------ | -----------
`base/` | Defaults and base HTML elements
`modules/` | Independent, reusable and functional UI components
`pages/` | Specific page styles
`vendors/` | Third-party software
`vendors/overwrites/` | Third-party overwrites

---

## Code style guidelines

> Every line of code should appear to be written by a single person, no matter the number of contributors.

### Syntax
- Use soft tabs with two spaces — they're the only way to guarantee code renders the same in any environment.
- When grouping selectors, keep individual selectors to a single line.
- Include one space before the opening brace of declaration blocks for legibility.
- Place closing braces of declaration blocks on a new line.
- Include one space after `:` for each declaration.
- Each declaration should appear on its own line for more accurate error reporting.
- End all declarations with a semi-colon. The last declaration's is optional, but your code is more error prone without it.
- Comma-separated property values should include a space after each comma (e.g., `box-shadow`).
- Don't include spaces after commas _within_ `rgb()`, `rgba()`, `hsl()`, `hsla()`, or `rect()` values. This helps differentiate multiple color values (comma, no space) from multiple property values (comma with space).
- Don't prefix property values or color parameters with a leading zero (e.g., `.5` instead of `0.5` and `-.5px` instead of `-0.5px`).
- Lowercase all hex values, e.g., `#fff`. Lowercase letters are much easier to discern when scanning a document as they tend to have more unique shapes.
- Use shorthand hex values where available, e.g., `#fff` instead of `#ffffff`.
- Quote attribute values in selectors, e.g., `input[type="text"]`. [They’re only optional in some cases](http://mathiasbynens.be/notes/unquoted-attribute-values#css), and it’s a good practice for consistency.
- Avoid specifying units for zero values, e.g., `margin: 0;`instead of `margin: 0px;`.

_(From [Code Guide](http://codeguide.co/).)_

### Order of styles inside a module
1. Variables
2. Mixins
3. Basic HTML element — `input[type="password"] {}`
4. Module class — `.input {}`
5. Module attribute class — `.input.is-large {}`

### Order of properties inside a style
1. Positioning — `position`,  `left`, …
2. Box model — `display`,  `float`,  `width`,  `padding`,  `margin` …
3. Typographic — `font`,  `text-align`, …
4. Visual — `background`,  `border`, …
5. Misc — `opacity`, …

_(From [Code Guide](http://codeguide.co/).)_

### Single declarations
In instances where a rule set includes _only one declaration_, consider removing line breaks for readability and faster editing. Any rule set with multiple declarations should be split to separate lines. _(From [Code Guide](http://codeguide.co/).)_
```css
.icon           { background-position: 0 0; }
.icon.of-home   { background-position: 0 -20px; }
.icon.of-work   { background-position: 0 -40px; }
```

### Comments
Code is written and maintained by people. Ensure your code is descriptive, well commented, and approachable by others. Great code comments convey context or purpose. Do not simply reiterate a component or class name. Be sure to write in complete sentences for larger comments and succinct phrases for general notes. _(From [Code Guide](http://codeguide.co/).)_
```css
/* Wrapping element for .modal.is-title and .modal.is-close */
.modal.is-header {
  …
}
```

### Linter
Use [SCSS Lint](https://github.com/brigade/scss-lint) to help you be on the right track. Install its [plugin](https://github.com/brigade/scss-lint#editor-integration) on your editor of choice. Also, use [this GSS configuration file](https://gist.github.com/sergiofontes/47ec6addc1768855b3e7b2aba992f96f) to remain compliant with these standards.

### Autoprefixer
Use [Autoprefixer](https://github.com/postcss/autoprefixer) to deal with CSS vendor prefixes. In other words, you must not manually write these annoying prefixes — let the PostCSS' [Autoprefixer](https://github.com/postcss/autoprefixer) do it for you. Doing this, you keep the code clean and also improve maintainability, since you can easily configure what browsers the project should support.

### Git
Keep an eye on Guava's [Git standards](https://github.com/guava/standards/blob/master/git.md) and on the following naming convention for branches.
* Use hyphen to separate words (eg.: `name-of-branch`).
* Use slash to separate branch prefix from branch name (eg.: `prefix/name-of-branch`).
* `master` — the main branch of design version.
* `feature/…` — adds something new.
* `fix/…` — fixes one or more bugs.
* `chore/…` — improves perfomance, etc.

## Further reading

- [Code Guide](http://codeguide.co/), by mdo
- [Atomic Design Methodology](http://atomicdesign.bradfrost.com/chapter-2/), by Brad Frost
- [Depth of Applicability](https://smacss.com/book/applicability), by Jonathan Snook
- [Learning from Lego: A Step Forward in Modular Web Design](http://alistapart.com/article/learning-from-lego-a-step-forward-in-modular-web-design), by Samantha Zhang
- [BEM sucks](https://twitter.com/samuelfine/status/575646836251344897), by Samuel Fine
