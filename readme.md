![Logo of Guava Stylesheet Standards](https://dl.dropboxusercontent.com/u/13659411/Guava/gss.svg)

GSS is a module-based approach to CSS structuration with a human-friendly syntax. The main idea is to divide the user interface into (almost) independent **modules**, which in turn contain **attributes** that _can be combined to compose variations of their parent module_. All of that alongside a more natural readability of the classes. This way, it’s easy to understand, develop and maintain stylesheets, from small to big projects.

It's heavily inspired by a lot of great ideas, like Atomic Design, SMACSS, mdo's Code Guide, Semantic UI and so on.

### Features
- Modular styling.
- Simplicity and readability above everything.
- Easy recognition and debug of which module you are working on.
- Seamless maintainability of code.
- Simple structure that leverages the power of cascading stylesheet.

### Naming principles
- Modules are only named by its purpose.
- Attributes of a module are named by either its purpose, appearance, behavior or dependence. They must be prefixed with a verb or a preposition.
- Use of `lisp-case` for naming classes. All lowercase.
- Words separated by a single hyphen (never double).
- Modules and attributes are separated by a space in the HTML or `.` in the CSS or nested in SCSS/LESS.
- Different modules in a same HTML element are separated by a slash (e.g.: '<span class="icon of-submit / motion of-submiting">') for visual convenience.

## How it works
Essentially, every user interface piece is (or can be) a module, and ideally, they should be the most independent and self-contained from other modules as possible.

The stylesheets are organized by:
- **Independent modules** of some piece of UI.
- **Combinable attributes**, prefixed by a verb/preposition.

A **module** can range from a basic piece of a standalone HTML element (like a simple button), to a more complex user interface system (a grid for example). They are named by its _purpose_. An **attribute** is a part and/or an extension of the parent module (or a module of a module) — and can only exist within them. They are prefixed with a verb or a preposition (`has-`, `is-`, `at-`, `on-`, `of-` etc) and are named by either its _purpose_, _appearance_, _behavior_ or _dependence_.

### Example
![Example](https://dl.dropboxusercontent.com/u/13659411/Guava/gssexample.svg)

#### The markup
_Note that the combination of modules and attributes brings an intuitive understanding of how this UI piece looks like._
```html
<button class="button is-primary is-large has-icon">
  Submit
  <span class="icon of-submit"></span>
</button>
```

#### Button's module stylesheet
```css
button, .button {                         /* Module */
  display: inline-block;
  padding: .2rem .5rem;
  color: black;
  font-weight: 1rem;
  line-height: 1rem;
  text-align: center;
  white-space: nowrap;
  vertical-align: middle;
  appearance: none;
  border: 2px solid black;
}

.button.is-primary {                       /* Attribute */
  color: #f6494d;
  background-color: #f6494d;
}

.button.is-large { padding: .5rem 1rem; } /* Attribute */
.button.has-icon { position: relative; }  /* Attribute */
```

#### Icon's module stylesheet
```css
.icon {                                   /* Module */
  display: inline-block;
  width: 1rem;
  height: 1rem;
}

.icon.of-submit {                         /* Attribute */
  position: absolute;
  top: .5rem;
  right: 1rem;
  background-image: url("...");  
}
```
P.S.: A module can either contain base styles (that are combined with its attributes, like `.button`) or not (in this case, by being just an remark of the current module file, e.g.: `.grid`).
P.S.2: The modules are created _by demand_ of developers and designers (except the [core modules](https://github.com/guava/gss#the-core)).

## Modules and stylesheets structure

### The core
Some modules are more important than others and may cascade throughout the stylesheet. These notorious blocks are the most basic building units, and some of them — like typography, colors, functions and global attributes — may spread to other modules.

Core modules | Description
------------ | ---------------
`core/utils.scss` | Functions and uncategorized mixins
`core/colors.scss` | Colors, sorted by name and semantic purpose (e.g.: `blue` and `primary`)
`core/type.scss` | Typographic modular scale and text elements (`h1`,  `p`, etc)
`core/grid.scss` | Dimensions, rows, containers, alignments, columns, ordering, etc
`core/attributes.scss` | Shared attributes between different modules

_(Ordered by importance.)_

### Other modules
The table below shows _examples_ of possible modules. It's up to developers and designers decide which modules can fit in your project — or even create new different modules.

Examples of modules | Description
------------------- | ---------------
`articles.scss` | Articles layouts
`alerts.scss` | Alerts and notifications
`backgrounds.scss` | Textures, patterns and other things
`buttons.scss` | Buttons and its variations
`figures.scss` | Images, illustrations, infographics
`footers.scss` | Footers layouts
`forms.scss` | Inputs & fieldsets layouts
`groups.scss` | Groups of standalone elements, like button, inputs, figures, icons, etc
`headers.scss` | Headers layouts
`icons.scss` | Iconography
`inputs.scss` | Inputs and its variations
`logos.scss` | Logos and its variations
`menus.scss` | Menu layouts
`motion.scss` | Keyframes, triggers and special mixins for UI animation
`overlays.scss` | Modals, popovers and other things that overlays basic UI
`sections.scss` | Special sections layouts
`tables.scss` | Tables header, body and footer layouts, cells, rows and columns
`…` | …

_(Examples of modules.)_

### Specific page styles
Sometimes, it's hard to map some user interface components (or aspects) to modules. Also, there may be specific styles that make more sense belonging to a page rather than a building block. For that, there is the `pages/`  folder. These styles classes must be prefixed with `.page-`.

### Vendors
The open source world is vast and vibrant. In order to deal with these huge amount of awesomeness, it's prudent to specify what you relies on and overwrites over. GSS does this by separating the overwrites into its own folder and files. These style classes must be prefixed with `.vendor-`.

### File structure
The naming scheme of classes and files is: if it's a file, then is plural; if it's the module class name, then is singular.

Folder | Description
------ | -----------
`vendors/` | Third-party software
`vendors/overwrites/` | Third-party overwrites
`modules/core/` | Shared styles between modules
`modules/` | User interface modules
`pages/` | Specific page styles

_(Ordered by importance.)_

## Code guidelines

> Every line of code should appear to be written by a single person, no matter the number of contributors.

GSS follows HTML and CSS of [mdo's Code Guide](http://codeguide.co/) for seamless coding experience. Regarding stylesheets, you should pay attention specially for the topics bellow.

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
In instances where a rule set includes _only one declaration_, consider removing line breaks for readability and faster editing. Any rule set with multiple declarations should be split to separate lines.

_(From [Code Guide](http://codeguide.co/).)_

### Comments
Code is written and maintained by people. Ensure your code is descriptive, well commented, and approachable by others. Great code comments convey context or purpose. Do not simply reiterate a component or class name. Be sure to write in complete sentences for larger comments and succinct phrases for general notes.

_(From [Code Guide](http://codeguide.co/).)_

### Linter
Use [SCSS Lint](https://github.com/brigade/scss-lint) to help you be on the right track. Install its [plugin](https://github.com/brigade/scss-lint#editor-integration) on your editor of choice. Also, use the [GSS configuration file](https://gist.github.com/sergiofontes/47ec6addc1768855b3e7b2aba992f96f) to remain compliant with these standards.

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

- [Atomic Design Methodology](http://atomicdesign.bradfrost.com/chapter-2/), by Brad Frost
- [Learning from Lego: A Step Forward in Modular Web Design](http://alistapart.com/article/learning-from-lego-a-step-forward-in-modular-web-design), by Samantha Zhang
- [Depth of Applicability](https://smacss.com/book/applicability), by Jonathan Snook
- [Code Guide](http://codeguide.co/), by mdo
- [BEM sucks](https://twitter.com/samuelfine/status/575646836251344897), by Samuel Fine
