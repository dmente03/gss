![Logo of Guava Stylesheet Standards](https://dl.dropboxusercontent.com/u/13659411/Guava/gss.svg)

GSS is a module-based methodology to CSS structuration with a human-friendly syntax. It aims to facilitate the process of understanding, naming and organizing CSS. This way, it’s easier to develop and maintain stylesheets, from small to big projects.

It's heavily inspired by a lot of great ideas, like [Atomic Design](http://atomicdesign.bradfrost.com/), [SMACSS](https://smacss.com/), [mdo's Code Guide](http://codeguide.co/), [Semantic UI](http://semantic-ui.com/) and so on.

## What it feats

- Modular styling.
- Simplicity and readability above everything.
- Easy recognition and debug of which module you are working on.
- Seamless maintainability of code.
- Structure that leverages the power of cascading stylesheet.

_TODO: Visual introduction_

## How it works

Every UI component has its own characteristics. These qualities can simply be set in its own element (`p {…}`, for example), or can be extended by the use of classes (`p.is-lead {…}`). These extension classes are **Attributes** (`.is-lead`). Attributes defines and categorizes the components. Since they are prefixed by a verb/preposition, they are named in a more natural and contextual way.

In GSS, the stylesheets are categorized into three types, which can (or not) contain Attributes:

1. **Base** — defaults and styles of base HTML and UI elements (`p {…}`).
2. **Modules** — (almost) independent, reusable and functional UI components. (`.card {…}`).
3. **Page** — contextual and page-specific styles (`.page-login {…}`).

_TODO: Visual examples_

## Going deeper

### Base
Defaults and styles of base HTML and UI elements. They are the most basic styles of every project. Also, its rules are applied using an element selector.

#### Post
```html
<article class="article is-post">
  <h1>What is love?</h1>
  <p class="is-lead">Baby don't hurt me</p>
  <p>What is love?<br>
     What is love?<br>
     What is love?<br>
     Baby don't hurt me<br>
     Don't hurt me<br>
     No more<br>
     Don't hurt me<br>
     Don't hurt me</p>
  <blockquote>
    What is love?<br>
    What is love?
    <cite>— Haddaway</cite>
  </blockquote>
</article>
```

_Base (Typography)_
```css
h1 {…}

p {
  …
  &.is-lead {…}
}

blockquote {
  …
  cite {…}
}
```

### Modules
Independent, reusable and functional UI components that forms the bulk of any project. Sometimes, a Module can sit within other Module, but oftentimes they are a group of Base elements in which you only need to put classes on the parent.

#### Example of Card
```html
<article class="card is-employee">
  <header>
    <img src="" alt="Sérgio photo">
  </header>
  <section>
    <h3>Sérgio Fontes</h3>
    <p>Designer</p>
    <small>Member since Oct 2013</small>
  </section>
</article>
```

_Base (Typography)_
```css
h3 {…}
p {…}
small {…}
```

_Module (Cards)_
```css
.card.is-employee {
  …
  header {…}
  section {…}
  img {…}
  small {…}
}
```

#### Example of Dropdown
```html
<div class="dropdown is-centered has-icons">
  <ul>
    <li>
      <a href="#">
        <span class="icon of-profile"></span>
        Profile
      </a>
    </li>
    <li>
      <a href="#">
        <span class="icon of-configuration"></span>
        Configuration
      </a>
    </li>
    <li>
      <a href="#">
        <span class="icon of-logout"></span>
        Log out
      </a>
    </li>
  </ul>
</div>
```

_Module (Dropdowns)_
```css
.dropdown.is-centered {
  …
  ul {…}
  li {…}
  a {…}
  &.has-icon {
    .icon {…}
  }
}
```

_Module (Icons)_
```css
.icon {
  &.of-profile {…}
  &.of-configuration {…}
  &.of-logout {…}
}
```

#### Menu
```html
<nav class="menu is-side-nav is-fixed">
  <img class="logo of-guava is-small" src="…">
  <ul>
    <li class="is-active">
      <a href="#">
        <span class="icon of-dashboard"></span>
        Dashboard
      </a>
    </li>
    <li>
      <a href="#">
        <span class="icon of-people"></span>
        People
      </a>
    </li>
    <li>
      <a href="#">
        <span class="icon of-project"></span>
        Project
      </a>
    </li>
  </ul>
  <input type="search" placeholder="Search for something...">
  <span class="icon of-search"></span>
</nav>
```

_Base (Forms)_
```css
input[type="search"] {…}
```

_Module (Logos)_
```css
.logo.of-guava {
  …
  &.is-small {…}
}
```

_Module (Icons)_
```css
.icon {
  &.of-dashboard {…}
  &.of-people {…}
  &.of-projects {…}
}
```

_Module (Menus)_
```css
.menu.is-side-nav {
  …
  ul {…}
  li {…}
  a {…}
  input[type="search"] {…}
  .icon {…}
  .is-active a {…}
  .logo.of-guava {…}
}
```

#### Grid
```html
<div class="grid is-container">
  <div class="grid is-row">
    <div class="grid is-column of-quarter">…</div>
    <div class="grid is-column of-quarter">…</div>
    <div class="grid is-column of-quarter">…</div>
    <div class="grid is-column of-quarter">…</div>
  </div>
  <div class="grid is-row">
    <div class="grid is-column of-third">…</div>
    <div class="grid is-column of-third">…</div>
    <div class="grid is-column of-third">…</div>
  </div>
  <div class="grid is-row">
    <div class="grid is-column of-half">…</div>
    <div class="grid is-column of-half">…</div>
  </div>
</div>
```

_Module (Grid)_
```css
.grid.is-container {…}
.grid.is-row {…}
.grid.is-column {
  …
  &.of-half {…}
  &.of-third {…}
  &.of-quarter {…}
}
```

### Pages
Context and page-specific styles that can’t be reused or alocated within a Module. These styles classes must be prefixed with `.page-`.

#### Example of Color Theme
```html
<body class="page-color">
  <article class="article is-post">
    <h1>What is love?</h1>
    <p class="is-lead">Baby don't hurt me</p>
    <p>What is love?<br>
       What is love?<br>
       What is love?<br>
       Baby don't hurt me<br>
       Don't hurt me<br>
       No more<br>
       Don't hurt me<br>
       Don't hurt me</p>
    <blockquote>
      What is love?<br>
      What is love?
      <cite>— Haddaway</cite>
    </blockquote>
  </article>
</body>
```

Page (Color)
```css
.page-color {
  …
  .article.is-post {
    h1 {…}
    p {…}
    blockquote {
      …
      cite {…}
    }
  }
}
```

### Attributes
UI characteristics classes. They are prefixed by a verb/preposition; and can be named in a wide variety of ways: purpose, appearance, behavior, dependence, relationship, context and so on.

#### Example of Login Card
```html
<article class="card of-login">
  <h3>Login</h3>
  <input class="is-large" type="email" placeholder="Type your email">
  <input class="is-large" type="password" placeholder="And your password">
  <button class="of-submit has-icon">
    Log me in
    <span class="icon of-submit / motion is-submiting"></span>
  </button>
</article>
```

_Base (Forms)_
```css
input {
  …
  &.is-large {…}
}

input[type="email"] {…}
input[type="password"] {…}
```

Module (Cards)
```css
.card.is-login {
  …
  > h3 {…}
  > input {…}
  button {…}
}
```

_Module (Icons)_
```css
.icon {
  …
  &.of-submit {…}
}
```

_Module (Motion)_
```css
.motion {
  …
  &.is-submiting {…}
}
```

Class | Category
----- | --------
`.of-login` | _Relationship_
`.is-submit` | _Purpose_
`.is-large` | _Appearance_
`.has-icon` | _Dependence_
`.is-submiting` | _Behavior_
`.at-login` | _Context_

### Naming principles
- Use of `lisp-case` for naming classes. All lowercase.
- Words separated by a single hyphen (never double).
- Modules and Attributes are separated with a space in the HTML markup.
- Different Modules in a same HTML element are separated by a slash (e.g., `<span class="icon of-submit / motion of-submit>`) for visual convenience.

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
Examples of Modules | Description
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

### Naming files and classes
The naming scheme of classes and files is: if it's a file, then is plural; if it's a Base/Module class name, then is singular.

### Folders
Folder | Description
------ | -----------
`base/` | Defaults and base HTML elements
`modules/` | Independent, reusable and functional UI components
`pages/` | Specific page styles
`vendors/` | Third-party software
`vendors/overwrites/` | Third-party overwrites

###  

---

###  

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
.icon-home      { background-position: 0 -20px; }
.icon-account   { background-position: 0 -40px; }
```

### Comments
Code is written and maintained by people. Ensure your code is descriptive, well commented, and approachable by others. Great code comments convey context or purpose. Do not simply reiterate a component or class name. Be sure to write in complete sentences for larger comments and succinct phrases for general notes. _(From [Code Guide](http://codeguide.co/).)_
```css
/* Wrapping element for .modal-title and .modal-close */
.modal-header {
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
