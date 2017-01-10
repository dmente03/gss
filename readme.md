![Logo of Guava Stylesheet Structure](https://dl.dropboxusercontent.com/u/13659411/Guava/gss.png)

GSS is a module-based approach to CSS structuration with a human-friendly syntax. The main idea is to divide the user interface into (almost) independent modules, which in turn contain attributes that can be combined to compose variations of their parent module. All of that alongside a more natural readability of the classes. This way, it’s easy to understand, develop and maintain stylesheets, from small to big projects.

## Features

- Modular styling.
- Simplicity and readability above everything.
- Easy recognition and debug of which module you are working on.
- Seamless maintainability of code.
- Simple structure that leverages the power of cascading stylesheet.

## Naming principles

- Use of `lisp-case` for naming classes. All lowercase.
- Words separated by a single hyphen (never double).
- Modules are only named by its purpose.
- Attributes are named by either its purpose, appearance, behavior or dependence. They must be prefixed with a verb or a preposition.
- Both modules and attributes are separated by a space in the HTML or `.` in the CSS or nested in SCSS/LESS.


## Modules & attributes

Essentially, every user interface part is a module, and ideally, they should be the most independent and self-contained from other modules as possible.

A module can range from a basic piece of a standalone HTML element (like a simple button), to a more complex user interface system (a grid for example). They are named by its *purpose*. E.g.: `button`, or `grid`.

An attribute is a part and/or an extension of the parent module (or a module of a module) — and can only exist within them. They are prefixed with a verb or a preposition (`has-`, `is-`, `at-`, `on-`, `of-` etc) and are named by either its *purpose*, *appearance*, *behavior* or *dependence*. E.g.: `is-primary`, `is-large`,  `is-submitting` or `has-icon`.

#### Example
```html
<!--           Module               Attributes             Dependence-->
<button class="button    is-primary is-large is-submitting    has-icon">
```
In which `button` is the module; `is-primary`, `is-large`,  `is-submitting` are its attributes; and `has-icon` is its dependence from another module.

#### Example — a more complex one
```html
<div class="grid is-container is-horizontal">
  <div class="column is-half-wide">…</div>
  <div class="column is-half-wide">…</div>
</div>
```

#### Example — an even more complex one
```html
<div class="grid is-row">
  <div class="grid is-container is-horizontal">
    <div class="column is-half-wide">
      <button class="button is-primary has-icon">
        Submit
        <span class="icon of-submit"></span>
      </button>
    </div>
    <div class="column is-half-wide">
      <button class="button has-icon">
        Cancel
        <span class="icon of-cancel"></span>
      </button>
    </div>    
  </div>
</div>
```

#### Example — different modules within a same HTML element _(separated by a slash `/`)_
```html
<div class="grid is-container is-horizontal">
  <div class="column is-half-wide">
    <button class="button is-primary has-icon / motion is-waiting is-first">
      Submit
      <span class="icon of-submit"></span>
    </button>
  </div>
  <div class="column is-half-wide">
    <button class="button has-icon / motion is-waiting is-second">
      Cancel
      <span class="icon of-cancel"></span>
    </button>
  </div>    
</div>
```

### Core modules
Some modules are more important than others and may cascade throughout the stylesheet. These notorious blocks are the most basic building units, and some of its parts — like variables and mixins — may spread to other modules. E.g.: colors, typographic scale, grid measures, motion callouts etc.

Core modules | Description
------------ | ---------------
`core` / `utils` | Functions, helper classes and uncategorized mixins
`core` / `colors` | Colors, sorted by name and semantic purpose (e.g.: `blue` and `primary`)
`core` / `type` | Typographic modular scale and text elements (`h1`,  `p`, etc) 
`core` / `grid` / `grid` | Dimensions, rows, containers, alignments and responsive rules
`core` / `grid` / `columns` | Columns, offsetting, nesting, ordering and more responsive rules
`core` / `motion` | Keyframes, triggers and special mixins for UI animation
_(ordered by importance)_

### Other modules
Examples of modules | Description
------------------- | ---------------
`articles` | Articles layouts
`alerts` | Alerts and notifications
`backgrounds` | Textures, patterns and other things
`buttons` | Buttons and its variations
`figures` | Images, illustrations, infographics
`footers` | Footers layouts
`forms` | Inputs & fieldsets layouts
`headers` | Headers layouts
`groups` | Groups of standalone elements, like button, inputs, figures, icons, etc
`icons` | Iconography
`inputs` | Inputs and its variations
`logos` | Logos and its variations
`menus` | Menu layouts
`overlays` | Modals, popovers and other things that overlays basic UI
`sections` | Special sections layouts
`tables` / `tables` | Tables header, body and footer layouts
`tables` / `cells` | Table cells, rows and columns
`…` | …

_PS: The naming scheme of classes and files are: if it's a file, then is plural; if it's the module class name, then is singular._

### Specific page styles
Sometimes, it's hard to map some user interface components (or aspects) to modules. Also, there may be specific styles that make more sense belonging to a page rather than a building block. For that, there is the `pages/`  folder. These styles classes are prefixed with `page-`.

### Vendors
The open source world is vast and vibrant. In order to deal with these huge amount of awesomeness, it's prudent to specify what you relies on and overwrites over. GSS does this by separating the overwrites into its own folder and files. These style classes are prefixed with `vendor-`.


## File structure of the front-end (CSS + JS)

Both CSS and JS files can be separate to maintain a framework's structure. However, it would be nice to replicate their very same structure on its specific folders.

```
modules/  .........................................................  Modules
↳core/  ....................................  Shared styles between modules
pages/  ..............................................  Specific page styles
vendors/  ............................................  Third-party software
↳overwrites/  .................................................  Overwrites
```


## General guidelines

> Every line of code should appear to be written by a single person, no matter the number of contributors.

GSS follows [mdo's guidelines](http://codeguide.co/) for HTML and CSS for seamless coding experience. Regarding stylesheets, you should pay attention specially for the topics bellow.

### Syntax
- Use soft tabs with two spaces—they're the only way to guarantee code renders the same in any environment.
- When grouping selectors, keep individual selectors to a single line.
- Include one space before the opening brace of declaration blocks for legibility.
- Place closing braces of declaration blocks on a new line.
- Include one space after `:` for each declaration.
- Each declaration should appear on its own line for more accurate error reporting.
- End all declarations with a semi-colon. The last declaration's is optional, but your code is more error prone without it.
- Comma-separated property values should include a space after each comma (e.g., `box-shadow`).
- Don't include spaces after commas *within* `rgb()`, `rgba()`, `hsl()`, `hsla()`, or `rect()` values. This helps differentiate multiple color values (comma, no space) from multiple property values (comma with space).
- Don't prefix property values or color parameters with a leading zero (e.g., `.5` instead of `0.5` and `-.5px` instead of `-0.5px`).
- Lowercase all hex values, e.g., `#fff`. Lowercase letters are much easier to discern when scanning a document as they tend to have more unique shapes.
- Use shorthand hex values where available, e.g., `#fff` instead of `#ffffff`.
- Quote attribute values in selectors, e.g., `input[type="text"]`. [They’re only optional in some cases](http://mathiasbynens.be/notes/unquoted-attribute-values#css), and it’s a good practice for consistency.
- Avoid specifying units for zero values, e.g., `margin: 0;`instead of `margin: 0px;`.

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

### Single declarations
In instances where a rule set includes _only one declaration_, consider removing line breaks for readability and faster editing. Any rule set with multiple declarations should be split to separate lines.

### Comments
Code is written and maintained by people. Ensure your code is descriptive, well commented, and approachable by others. Great code comments convey context or purpose. Do not simply reiterate a component or class name. Be sure to write in complete sentences for larger comments and succinct phrases for general notes.


## Further reading

- [Atomic Design Methodology](http://atomicdesign.bradfrost.com/chapter-2/), by Brad Frost
- [Learning from Lego: A Step Forward in Modular Web Design](http://alistapart.com/article/learning-from-lego-a-step-forward-in-modular-web-design), by Samantha Zhang
- [Depth of Applicability](https://smacss.com/book/applicability), by Jonathan Snook
- [Code Guide](http://codeguide.co/), by mdo
- [BEM sucks](https://twitter.com/samuelfine/status/575646836251344897), by Samuel Fine
