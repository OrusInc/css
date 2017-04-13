## Orus CSS / Sass Style guide
*An intuitive approach to CSS and Sass.*

## CSS

These are set of principles and techniques to helps you clean your stylesheets and optimize your team workflow.

### General formatting

Spaces are the only way to assure code renders the same in any person’s environment.

- Always use soft-tabs with a two space indent. 
- Do not use ID selectors
- When grouping selectors, keep individual selector to a single line.
- Always use a semicolon as a terminator.
- Put space before `{ ` in rule declarations.
- Put line breaks between rulesets.
- Put spaces after : but never before in property declarations.
- Place closing braces of declaration blocks on a new line.
- Each declaration should appear on its own line for readability.
- Avoid specifying units for zero values, e.g., `margin: 0;` instead of `margin: 0px;`.
- Strive to limit use of shorthand declarations to instances where you must explicitly set all the available values.
- Use `//` for comment blocks (instead of `/* */) `.
- Prefer comments on their own line. Avoid end-of-line comments.
- Write detailed comments for code that isn't self-documenting:
  - Uses of `z-index`
  - Compatibility or browser-specific hacks

```css
// Not so good
.multiple,.classes,.get-new-lines{
    background-color:red;color:white;margin: 0 0 20px;}
#hell-no{
	// ...
}

// Better 
.multiple,
.classes,
.get-new-lines {
  background-color: red;
  color: white;
  margin-bottom: 20px;
}
```

### Units
Use unitless values when you can. Favor `rem` if you use relative units. Prefer seconds over milliseconds.

```css
// Not so good
div {
  margin: 0px;
  font-size: .9em;
  line-height: 22px;
  transition: 500ms;
}

// Better
div {
  margin: 0;
  font-size: .9rem;
  line-height: 1.5;
  transition: .5s;
}
```

### Class naming conventions
We recommend you [SMACSS](https://smacss.com/) for your class naming convention.
It allows for less nesting and lower specificity  for building scalable stylesheets. It also helps create clear relationships between CSS and HTML and helps you create reusable components.

**SMACSS** or "Scalable and Modular Architecture for CSS" is an approach to web development written by Jonathan Snook.
- Getting started with [SMACSS](https://smacss.com/book/)

```css
// Menu module
.menu { }

// descendant of .menu
.menu-item { }

// Menu item with state
.menu-item.is-active { }
```

### Colors
Always use the hexadecimal format unless you need transparency.

```css
// Not so good
div {
  color: hsl(103%, 40%, 53%);
}

// Better
div {
  color: #d8d8d8;
}
```

### JavaScript hooks

Avoid binding to the same class in your CSS and JavaScript. Developers might be afraid to make changes for fear of breaking functionality.
We recommend creating JavaScript-specific classes to bind to, prefixed with `.js-`.

```html
<button class="btn btn-primary js-request-to-book">Request to Book</button>
```

Never reference ` js-` prefixed class names from CSS files. ` js-` are used exclusively from JS files.

### Border
Use `0` instead of `none` to specify that a style has no border.

```css
// Not so good
.box {
  border: none;
}
 
// Better
.box {
  border: 0;
}
```

### Specificity
Please make sure that you have no more than one id selector in your rule declaration.

```css
// Bad Bad Bad!
#header .search #quicksearch {
  box-shadow: 0px 4px 8px rgba(10, 14, 18, .315);
}

// Better
#quicksearch {
  box-shadow: 0px 4px 8px rgba(10, 14, 18, .315);
}
```

Try to use specific class names when modifying an element for a precise use. (see SMACSS below)

```css
// Not so good
.listings-layout.bigger {
  font-size: 16px;
}

// Better
.listings-layout.is-bigger {
  font-size: 1.6rem;
}
```

When an element occur only once inside your document you may use ID, otherwise, prior classes. And in any doubt always prefer classes.
- Good candidates for ids: header, footer, modal popups.
- Bad candidates for ids: navigation, item listings, item view pages (ex: issue view).

```css
// Not so good
<ul id="category">
  <li>Category 1</li>
  <li>Category 2</li>
  <li>Category 3</li>
</ul>


// Better
<ul class="category-list">
  <li class="category-item">Category 1</li>
  <li class="category-item">Category 2</li>
  <li class="category-item">Category 3</li>
</ul>
```

When styling a component, start with an element + class namespace, prefer direct descendant selectors by default, and use as little specificity as possible.

```css
// Not so good
.category-list { }
.category-list li {
  list-style-type: disc;
}
.category-list li a {
  color: #f00;
  padding: 10px;
  margin: 0;
  position: relative;
}

// Better
ul.category-list { }
ul.category-list > li {
  list-style-type: disc;
}
ul.category-list > li > a {
  color: #f00;
}
```

### Drawing, Animations & Language
Avoid HTTP requests when the resources are easily replicable with CSS.

```css
// Not so good
div::before {
  content: url(white-circle.svg);
}

// Better
div::before {
  content: "";
  display: block;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  background: #fff;
}
```

Favor transitions over animations. Avoid animating other properties than opacity and transform.

```css
// Not so good
div:hover {
  animation: move 1s forwards;
}
@keyframes move {
  100% {
    margin-left: 100px;
  }
}

// Better
div:hover {
  transition: 1s;
  transform: translateX(100px);
}
```

Always Prefer English over math when you can.

```css
// Not so good
:nth-child(2n + 1) {
  transform: rotate(360deg);
}

// Better
:nth-child(odd) {
  transform: rotate(1turn);
}
```

### Brevity
Use shorthand properties and do not use multiple properties when it's not needed.

```css
// Not so good
div {
  transition: all 1s;
  top: 50%;
  margin-top: -10px;
  padding-top: 5px;
  padding-right: 10px;
  padding-bottom: 20px;
  padding-left: 10px;
}

// Better
div {
  transition: 1s;
  top: calc(50% - 10px);
  padding: 5px 10px 20px;
}
```

### Overriding
Unless you have good reasons, do not Override styles.

```css
// Not so good
li {
  visibility: hidden;
}
li:first-child {
  visibility: visible;
}

// Better
li + li {
  visibility: hidden;
}
```

### Selectors
Add a class to the elements you want to match when your selector exceeds 3 structural pseudo-classes, descendant or sibling combinators.

```css
// Not so good
div:first-of-type :last-child > p ~ *

// Better
div:first-of-type .info
```

### Positioning
There are many ways to position elements in CSS but try to restrict yourself to the properties/values below. By order of preference:

```css
display: block;
display: flex;
position: relative;
position: sticky;
position: absolute;
position: fixed;
```

### Flow
Don't change the default behavior of an element if you can avoid it. Keep elements in the natural document flow as much as you can. For example, removing the white-space below an image shouldn't make you change its default display:

```css
// Not so good
img {
  display: block;
}

// Better
img {
  vertical-align: middle;
}
```

Similarly, don't take an element off the flow if you can avoid it.

```css
// Not so good
div {
  width: 100px;
  position: absolute;
  right: 0;
}

// Better
div {
  width: 100px;
  margin-left: auto;
}
```

## Sass
We recommend Sass as css preprocessor. Always prior .scss files over .sass.

Order your regular CSS and `@include ` declarations logically.

```scss
.btn-green {
  background: green;
  font-weight: bold;
  @include transition(background 0.5s ease);
  // ...
}
```

### Nested selectors
**Please do not ever nest selectors more than three levels deep.**

When selectors become this long, you're likely writing CSS that is fragile and not reusable.

```scss
.container {
  .body {
    .profile {
      // PLEASE STOP!
    }
  }
}
```

When you have nested selectors, put them at the end and make sur nothing goes after them.

Add whitespace between your rule declarations and nested selectors, as well as between adjacent nested selectors.

```scss
// Not so good
.btn {
  background: green;
  font-weight: bold;
  .icon {
    margin-right: 10px;
  }
  @include transition(background 0.5s ease);
  
}

// Better
.btn {
  background: green;
  font-weight: bold;
  @include transition(background 0.5s ease);

  .icon {
    margin-right: 10px;
  }
}
```


### Variables
Prefer dash-cased variable names (e.g. $my-variable) over camelCased or snake\_cased variable names.

```scss
//Not so good
$colorPrimary = #d8d8d8;

// Better
$color-primary = #d8d8d8;
```

### File structure
We always recommend to break things down by components (separate compiled CSS files) and sections (directories of related content). (refer to SMACSS below).

### Files inclusion
Use explicit lists of **imports** to control the cascade, specificity and more.

```scss
// Imports
@import "primer";
@import "component";
@import "another_component";

// Rules
.rule { ... }
```

### Misc
While it is possible to select elements by ID in CSS, it should generally be considered as an anti-pattern. ID selectors introduce an unnecessarily high level of [specificity](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) to your rule declarations, and they are not reusable.

For more on this subject, read [CSS Wizardry's article](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) on dealing with specificity.

Again: **PLEASE never nest ID selectors!**

*If you must use an ID selector in the first place (and you should really try not to), they should never be nested. If you find yourself doing this, you need to revisit your markup, or figure out why such strong specificity is needed. If you are writing well formed HTML and CSS, you should never need to do this.*
