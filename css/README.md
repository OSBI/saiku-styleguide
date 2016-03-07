<img src="https://raw.githubusercontent.com/OSBI/saiku-styleguide/assets/icon-css-256.png" alt="Saiku CSS code styleguide" align="right" />

# CSS

> Saiku CSS code styleguide.

## Table of Contents

1. [Preprocessor](#preprocessor)
2. [Best practices](#best-practices)
3. [Colors](#colors)
4. [Numbers and units](#numbers-and-units)
5. [Inline assets](#inline-assets)
6. [Pseudo elements](#pseudo-elements)
7. [Quotes](#quotes)
8. [Comments](#comments)
9. [Naming conventions](#naming-conventions)
10. [Namespaces](#namespaces)
11. [Whitespace](#whitespace)
12. [Code linting](#code-linting)
13. [Resources](#resources)

## Preprocessor

* [1.1](#1.1) <a name='1.1'></a> [Stylus](http://stylus-lang.com) is our preprocessor of choice.

* [1.2](#1.2) <a name='1.2'></a> Limit the use of its features to only variables and mixins.

> Getting too crazy with Stylus can lead to both terrible code maintenance and output.

* [1.3](#1.3) <a name='1.3'></a> `@extend` is allowed only when used with placeholders.

> `@extend`ing classes can lead to terrible code output.

**[⬆ back to top](#table-of-contents)**

## Best practices

* [2.1](#2.1) <a name='2.1'></a> Avoid the use of `!important` at all costs. Exceptions to the rule:
	1. It's being used within a helper class;
	2. You can explain its use.

* [2.2](#2.2) <a name='2.2'></a> Do not use ids.
> They kill modularity and are not necessary for styling.

* [2.3](#2.3) <a name='2.3'></a> Do not manually add vendor prefixes.
> Our tooling should be able to handle this.

* [2.4](#2.4) <a name='2.4'></a> Do not use vendor-specific font rendering techniques.
> They are not consistent, break constrast and typography rules.

* [2.5](#2.5) <a name='2.5'></a> Prefer `background` over `background-color` when possible.
> Simply because it's a shorthand.

* [2.6](#2.6) <a name='2.6'></a> Do not use `pointer-events`.
> It's not reliable and it's not CSS's role.

* [2.7](#2.7) <a name='2.7'></a> Avoid hard-coded magic numbers.
> These are definitelly a code smell and make super hard to maintain.

```styl
// Bad
.selector {
  width: 73px; // WTF is 73px? Why?
  z-index: 99999; // Brute force here, not good at all
  margin-top: 128px; // Again, what the heck is this?
}

// Good (values actually make sense)
.selector {
  width: grid-columns(2);
  z-index: $depth-screen-foreground;
  margin-top: $selector-inner-padding;
}
```

* [2.8](#2.8) <a name='2.8'></a> Avoid undoing styles.
> These are code smells and almost always have room for improvement.

```styl
// Bad
h2 {
  font-size: 2em;
  margin-bottom: 0.5em;
  padding-bottom: 0.5em;
  border-bottom: 1px solid #ccc;
}

.no-border {

  // Brute force resets down here
  padding-bottom: 0;
  border-bottom: none;
}

// Good
h2 {
  font-size: 2em;
  margin-bottom: 0.5em;
}

.headline {
  padding-bottom: 0.5em;
  border-bottom: 1px solid #ccc;
}
```

* [2.9](#2.9) <a name='2.9'></a> Prefer `em` over `px`.
> This allows for a more flexible element sizing.

**[⬆ back to top](#table-of-contents)**

## Colors

* [3.1](#3.1) <a name='3.1'></a> Hexadecimal values should always be in lower case.

> This approach improves code readability.

```styl
// Bad
.link {
  color: #EAEAE2;
}

// Good
.link {
  color: #eaeae2;
}
```

* [3.2](#3.2) <a name='3.2'></a> Prefer shorthand notation.

```styl
// Bad
$color: #cccccc;

// Good
$color: #ccc;

// Bad
$color: #ff6600;

// Good
$color: #f60;
```

* [3.3](#3.3) <a name='3.3'></a> Do not use CSS color names.

> They're not consistently implemented on browsers.

```styl
// Bad
.error {
  background: red;
}

// Good
.error {
  background: #ff0066;
}
```

**[⬆ back to top](#table-of-contents)**

## Numbers and units

* [4.1](#4.1) <a name='4.1'></a> Avoid specifying units for zero values.

```styl
// Bad
.square {
  border: 0px;
}

// Good
.square {
  border: 0;
}
```

* [4.2](#4.2) <a name='4.2'></a> Do not use floating decimals.

> They do make code harder to read.

```styl
// Bad
.heading {
  margin-left: -.75px;
  padding: .25px;
  border: 2.px;
}

// Good
.heading {
  margin-left: -0.75px;
  padding: 0.25px;
  border: 2.0px;
}
```

* [4.3](#4.3) <a name='4.3'></a> Use `pt` units to declare `letter-spacing` values.

> We found it easier to match Photoshop visual specifications.

```styl
// Bad
.text {
  letter-spacing: -0.75px;
}

// Good
.text {
  letter-spacing: -0.75pt;
}
```

* [4.4](#4.4) <a name='4.4'></a> Do not add units for `line-height` values.

> Not doing so will break vertical rythm.

```styl
// Bad
p {
  line-height: 1.5px;
}

// Good
p {

  // Equivalent to 150% of the font size
  line-height: 1.5;
}
```

**[⬆ back to top](#table-of-contents)**

## Inline assets

* [5.1](#5.1) <a name='5.1'></a> Inline assets are only allowed if they weight less than or equal to `1KB` and are presented only once in the code.

**[⬆ back to top](#table-of-contents)**

## Pseudo elements

* [6.1](#6.1) <a name='6.1'></a> Use double collons `::` to access pseudo elements.

```styl
// Bad
.button:after {
  background: #f60;
}

// Good
.button::before {
  outline: 1px solid;
}
```

**[⬆ back to top](#table-of-contents)**

## Quotes

* [7.1](#7.1) <a name='7.1'></a> Use single quotes `'` for everything.

* [7.2](#7.2) <a name='7.2'></a> Always wrap values with quotes.

> Even though some are not mandatory, it will enforce consistency.

```styl
// Bad
@import helpers/clearfix;

input[type=radio] {
  opacity: 0.35;
}

.selector {
  background: url(path/to/image.png) no-repeat;
}

// Good
@import 'helpers/clearfix';

input[type='radio'] {
  opacity: 0.35;
}

.selector {
  background: url('path/to/image.png') no-repeat;
}
```

**[⬆ back to top](#table-of-contents)**

## Comments

* [8.1](#8.1) <a name='8.1'></a> Following is an example of a well documented component following our standards.

```styl
/* ==========================================================================
   Component name
   ========================================================================== */

// Component theming properties
$component-background-color: #f06;
$component-color: #fff;

// Set component's layout direction, which changes the way arrows are drawn
$component-direction: 'down';

/**
 * Some description about my component.
 * Always try to be very concise and straightforward.
 *
 * TODO: Split this component in two other components.
 */

.component {
  // ...
}

/* Sub component name
   ========================================================================== */

/**
 * Some description about my sub component.
 *
 * FIXME: Rendenring issue on IE8.
 */

.component__sub-component {
}

/**
 * Modifier: Description of component modifier.
 */

.component--modifier {
  // ...
}

/**
 * Function: Description of component function.
 */

component-function() {
  // ...
}

/**
 * Mixin: Description of component mixin.
 */

component-mixin() {
  // ...
}
```

**[⬆ back to top](#table-of-contents)**

## Naming conventions

* [9.1](#9.1) <a name='9.1'></a> Use `hyphen-case` to name classes, variables, functions, mixins and placeholders.

```styl
// Bad
.fooBar {
  border: none;
}

LoremIpsumDolor {
  text-align: center;
}

// Good
.foo-bar {
  outline: 1px solid red;
}


// Good
.lorem-ipsum-dolor {
  vertical-align: middle;
}
```

* [9.2](#9.2) <a name='9.2'></a> Elements should have the base module name as a prefix and the name of the element, separated by double underscores `__`.

> The advantage of elements is to not rely on the markup to apply a certain style.

```styl
.menu-item {
  // ...
}

// Bad
.menu-item.icon {
  // ...
}

// Good
.menu-item__icon {
  // ...
}

// Bad
.menu-item-list {
  // ...
}

// Good
.menu-item__list {
  // ...
}
```

* [9.3](#9.3) <a name='9.3'></a> Modifiers should have the base module name as a prefix and the name of the modifier, separated by double hyphens `--`.

> Modifiers are also complementary, therefore a master/base class should exist to provide the visual foundation.

```styl
.logo {
  background: url('./logo.png') no-repeat;
}

// Bad
.logoBig {
  transform: scale(1.5);
}

// Good
.logo--big {
  transform: scale(1.25);
}

// Bad
.logo-with-small-size {
  transform: scale(0.25);
}

// Good
.logo--small {
  transform: scale(0.5);
}
```

* [9.4](#9.4) <a name='9.4'></a> States can be prefixed with `is`, `has` or `should`.

```styl
// Bad
.logo.logoHidden {
  opacity: 0;
}

// Good
.logo.is-hidden {
  opacity: 0;
}

// Bad
.logo.logo-disabled {
  border: 1px solid;
}

// Good
.logo.is-disabled {
  border: 1px solid fuchsia;
}

// Bad
.button-with-icon {
  // ...
}

// Good
.button.has-icon {
  // ...
}
```

**[⬆ back to top](#table-of-contents)**

## Namespaces

> Namespaces help us understand what role classes play.

| Prefix | Description | Example |
|---|---|---|
| `c` | For user interface components | `c-dropdown` |
| `ab` | For A/B testing stuff (usually removed and re-implemented once the test is done) | `ab-jira-ticket-42` |
| `u` | For utils | `u-clearfix` |
| `t` | For custom themes | `t-black-friday` |
| `_` | For hacks (that should be removed as soon as possible) | `_fix-dropdown-ie8` |
| `is`, `has`, `should` | For component states | `is-disabled` |
| `v` | For vendor service hooks (such as Optimizely, Crazy Egg, etc) | `v-optimizely` |

**[⬆ back to top](#table-of-contents)**

## Whitespace

* [11.1](#11.1) <a name='11.1'></a> Add a space after selector definition.

```styl
// Bad
.selector{content: 'foo';}

// Good
.selector { content: 'foo'; }
```

* [11.2](#11.2) <a name='11.2'></a> Add a space between a rule and its value.

```styl
// Bad
.button {
  color:#fff;
  background:#f06;
}

// Good
.button {
  color: #fff;
  background: #f06;
}
```

* [11.3](#11.3) <a name='11.3'></a> Add inner spaces to inline selectors.

```styl
// Bad
.selector {content: 'foo';}

// Good
.selector { content: 'foo'; }
```

* [11.4](#11.4) <a name='11.4'></a> If a selector has more than a single rule, break all the rules into new lines.

> This will improve code readability.

```styl
// Bad
.section { cursor: pointer; text-align: center; }

// Good
.section { cursor: default; }

// Good
.section {
  text-align: left;
  vertical-align: middle;
}
```

* [11.5](#11.5) <a name='11.5'></a> When targeting multiple selectors break each one in a new line.

```styl
// Bad
.footer, .header, .main {
  display: block;
}

// Good
.footer,
.header,
.main {
  margin: 0 auto;
}
```

* [11.6](#11.6) <a name='11.6'></a> Keep multiple rules in more than one line for better readability.

```styl
// Bad
.box {
  box-shadow: 0 1px 1px #eee,
  inset 0 1px 0 #f00;
}

// Good
.box {
  box-shadow: 0 1px 1px #eee, 
              0 1px 0   #f00 inset;
  background: linear-gradient(
              #1e5799 0%,
              #2989d8 50%,
              #207cca 51%,
              #7db9e8 100%);
}
```

* [11.7](#11.7) <a name='11.7'></a> Add a white space after each comma on multiple values.

```styl
// Bad
.selector {
  background: rgba(0,0,0,0.5);
}

// Good
.selector {
  background: rgba(255, 255, 255, 0.75);
}
```

**[⬆ back to top](#table-of-contents)**

## Code linting

* [12.1](#12.1) <a name='12.1'></a> We use [stylelint](http://stylelint.io) to lint our CSS code. All the rules can be found on the [`stylelint-config.js`](/linters/stylelint-config.js) file.

**[⬆ back to top](#table-of-contents)**

## Resources

### CSS naming methodologies

* [SMACSS](https://smacss.com)
* [BEM](https://bem.info)
* [SUIT CSS](http://suitcss.github.io)

### Blog posts

* [Code smells in CSS](http://csswizardry.com/2012/11/code-smells-in-css)
* [More Transparent UI Code with Namespaces](http://csswizardry.com/2015/03/more-transparent-ui-code-with-namespaces)
* [Line-height units](http://tzi.fr/css/text/line-height-units#Unitless)
* [Medium’s CSS is actually pretty f***ing good](https://medium.com/@fat/mediums-css-is-actually-pretty-fucking-good-b8e2a6c78b06)
* [Why Ems?](https://css-tricks.com/why-ems)
* [CSS Protips](https://github.com/AllThingsSmitty/css-protips)

**[⬅ back to main](../../../)**&nbsp;&nbsp;&nbsp;&nbsp;**[⬆ back to top](#table-of-contents)**
