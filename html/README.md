<img src="https://raw.githubusercontent.com/OSBI/saiku-styleguide/assets/icon-html5-256.png" alt="Saiku HTML code styleguide" align="right" />

# HTML

> Saiku HTML code styleguide.

## Table of Contents

1. [Syntax](#syntax)
2. [Doctype](#doctype)
3. [Language attribute](#language-attribute)
4. [Encoding](#encoding)
5. [IE compatibility mode](#ie-compatibility-mode)
6. [CSS and JavaScript includes](#css-and-javascript-includes)
7. [Organization](#organization)
8. [Boolean attributes](#boolean-attributes)
9. [JavaScript hooks](#javascript-hooks)
10. [Whitespace](#whitespace)
11. [Resources](#resources)

## Syntax

* [1.1](#1.1) <a name='1.1'></a> Always use double quotes `"`.

```html
<!-- Bad -->
<div id=foo></div>

<!-- Bad -->
<div id='foo'></div>

<!-- Good -->
<div id="foo"></div>
```

* [1.2](#1.2) <a name='1.2'></a> Always close self closing tags with a slash `/`.

```html
<!-- Bad -->
<p>Lorem ipsum<br>dolor sit</p>

<!-- Good -->
<p>Lorem ipsum<br />dolor sit</p>

<!-- Bad -->
<img src="path/to/image.png">

<!-- Good -->
<img src="path/to/image.png" />
```

* [1.3](#1.3) <a name='1.3'></a> Always close optional closing tags.

```html
<!-- Bad -->
<ul>
  <li>Once
  <li>Upon
  <li>A Time
</ul>

<!-- Good -->
<ul>
  <li>Once</li>
  <li>Upon</li>
  <li>A Time</li>
</ul>
```

**[⬆ back to top](#table-of-contents)**

## Doctype

* [2.1](#2.1) <a name='2.1'></a> Follow HTML5 doctype to enforce standards and a more consistent rendering.

```html
<!doctype html>
<html>
  <head></head>
  <body></body>
</html>
```

**[⬆ back to top](#table-of-contents)**

## Language attribute

* [3.1](#3.1) <a name='3.1'></a> Always specify a language for documents.

```html
<html lang="en-us">
  <!-- ... -->
</html>
```

**[⬆ back to top](#table-of-contents)**

## Encoding

* [4.1](#4.1) <a name='4.1'></a> Use `utf-8` as de default encoding of HTML documents.

```html
<head>
  <meta charset="utf-8">
</head>
```

**[⬆ back to top](#table-of-contents)**

## IE compatibility mode

* [5.1](#5.1) <a name='5.1'></a> Internet Explorer supports the use of a document compatibility `<meta>` tag to specify what version of IE the page should be rendered. You should force edge mode.

```html
<meta http-equiv="X-UA-Compatible" content="IE=Edge">
```

**[⬆ back to top](#table-of-contents)**

## CSS and JavaScript includes

* [6.1](#6.1) <a name='6.1'></a> There's no need to specify the `type` attribute of include tags.

```html
<!-- External CSS -->
<link rel="stylesheet" href="path/to/external.css">

<!-- Inline CSS -->
<style>
  /* ... */
</style>

<!-- JavaScript -->
<script src="path/to/script.js"></script>
```

**[⬆ back to top](#table-of-contents)**

## Organization

* [7.1](#7.1) <a name='7.1'></a> The order of rules declaration should look like the following.
  1. Generic classes (utils, typography, grid and so on)
  2. Specific classes
  3. `id` and `name`
  4. States
  5. Data attributes
  6. Other element attributes
  7. Boolean attributes

```html
<input type="text" class="u-pull-left input--big is-disabled" id="user-input" name="user-input" data-component="input-text" data-parameters="{value: 42}" disabled />
```

**[⬆ back to top](#table-of-contents)**

## Boolean attributes

* [8.1](#8.1) <a name='8.1'></a> Do not add values to boolean attributes.

```html
<!-- Bad -->
<input type="checkbox" value="Bar" checked="checked">Foo</input>

<!-- Good -->
<input type="checkbox" value="Bar" checked>Foo</input>

<!-- Bad -->
<input type="submit" disabled="disabled">Send email</input>

<!-- Good -->
<input type="submit" disabled>Send email</input>
```

**[⬆ back to top](#table-of-contents)**

## JavaScript hooks

* [9.1](#9.1) <a name='9.1'></a> JavaScript hooks should be declared as `component` data attribute.

```html
<button class="c-button c-button--big" data-component="buy-it-button">Buy it</button>
```

* [9.2](#9.2) <a name='9.2'></a> Always use `parameters` data attribute for component parameters following the literal object syntax.

```html
<div class="c-carousel" data-component="carousel" data-parameters="{direction: 'left-to-right', speed: 2.5, easing: 'easeOutExpo'}">
  <!-- ... -->
</div>
```

**[⬆ back to top](#table-of-contents)**

## Whitespace

* [10.1](#10.1) <a name='10.1'></a> Use soft tabs set to `4` spaces and never mix tabs with spaces.

* [10.2](#10.2) <a name='10.2'></a> Always add an empty line at the end of your file.

* [10.3](#10.3) <a name='10.3'></a> Break multiple attributes in new lines when needed.

```html
<div
  class="modal"
  id="main-modal"
  style="display: none;"
  hidden
>
</div>
```

* [10.4](#10.4) <a name='10.4'></a> When closing self closing tags, always add a single space before `/>`.

```html
<!-- Bad -->
<img src="doge.png"/>

<!-- Good -->
<img src="doge.png" />
```

**[⬆ back to top](#table-of-contents)**

## Resources

### Inspiration

* [Code Guide by @mdo](http://codeguide.co)
* [Harry Roberts coding style](http://csswizardry.com/2012/04/my-html-css-coding-style)
* [Magnetis Front-End Styleguide](https://github.com/magnetis/styleguide)
* [Netshoes markup code styleguide](https://github.com/netshoes/styleguide/blob/master/markup)

**[⬅ back to main](../../../)**&nbsp;&nbsp;&nbsp;&nbsp;**[⬆ back to top](#table-of-contents)**
