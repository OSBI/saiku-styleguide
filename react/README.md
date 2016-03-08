<img src="https://raw.githubusercontent.com/OSBI/saiku-styleguide/assets/icon-react-256.png" width="200" alt="Saiku React code styleguide" align="right" />

# React

> Saiku React code styleguide.

## Table of Contents

1. [Basic Rules](#basic-rules)
2. [Class vs `React.createClass` vs stateless](#class-vs-reactcreateclass-vs-stateless)
3. [Naming](#naming)
4. [Declaration](#declaration)
5. [Alignment](#alignment)
6. [Quotes](#quotes)
7. [Spacing](#spacing)
8. [Props](#props)
9. [Parentheses](#parentheses)
10. [Tags](#tags)
11. [Methods](#methods)
12. [Ordering](#ordering)
13. [`isMounted`](#ismounted)
14. [Resources](#resources)

## Basic Rules

* [1.1](#1.1) <a name="1.1"></a> Only include one React component per file.
  * [1.1.1](#1.1.1) <a name="1.1.1"></a> However, multiple [Stateless, or Pure, Components](https://facebook.github.io/react/docs/reusable-components.html#stateless-functions) are allowed per file. eslint: [`react/no-multi-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-multi-comp.md#ignorestateless).
* [1.2](#1.2) <a name="1.2"></a> Always use JSX syntax.
* [1.3](#1.3) <a name="1.3"></a> Do not use `React.createElement` unless you're initializing the app from a file that is not JSX.

**[⬆ back to top](#table-of-contents)**

## Class vs `React.createClass` vs stateless

* [2.1](#2.1) <a name="2.1"></a> If you have internal state and/or refs, prefer `class extends React.Component` over `React.createClass` unless you have a very good reason to use mixins. eslint: [`react/prefer-es6-class`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-es6-class.md) [`react/prefer-stateless-function`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/prefer-stateless-function.md)

```javascript
// Bad
const Listing = React.createClass({
  // ...
  render() {
    return <div>{this.state.hello}</div>;
  }
});

// Good
class Listing extends React.Component {
  // ...
  render() {
    return <div>{this.state.hello}</div>;
  }
}
```

And if you don't have state or refs, prefer normal functions (not arrow functions) over classes:

```javascript

// Bad
class Listing extends React.Component {
  render() {
    return <div>{this.props.hello}</div>;
  }
}

// Bad (since arrow functions do not have a "name" property)
const Listing = ({ hello }) => (
  <div>{hello}</div>
);

// Good
function Listing({ hello }) {
  return <div>{hello}</div>;
}
```

**[⬆ back to top](#table-of-contents)**

## Naming

* [3.1](#3.1) <a name="3.1"></a> **Extensions**: Use `.jsx` extension for React components.
* [3.2](#3.2) <a name="3.2"></a> **Filename**: Use PascalCase for filenames. E.g., `ReservationCard.jsx`.
* [3.1](#3.3) <a name="3.3"></a> **Reference Naming**: Use PascalCase for React components and camelCase for their instances. eslint: [`react/jsx-pascal-case`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-pascal-case.md)

```javascript
// Bad
import reservationCard from './ReservationCard';

// Good
import ReservationCard from './ReservationCard';

// Bad
const ReservationItem = <ReservationCard />;

// Good
const reservationItem = <ReservationCard />;
```

* [3.4](#3.4) <a name="3.4"></a> **Component Naming**: Use the filename as the component name. For example, `ReservationCard.jsx` should have a reference name of `ReservationCard`. However, for root components of a directory, use `index.jsx` as the filename and use the directory name as the component name:

```javascript
// Bad
import Footer from './Footer/Footer';

// Bad
import Footer from './Footer/index';

// Good
import Footer from './Footer';
```

**[⬆ back to top](#table-of-contents)**

## Declaration

* [4.1](#4.1) <a name="4.1"></a> Do not use `displayName` for naming components. Instead, name the component by reference.

```javascript
// Bad
export default React.createClass({
  displayName: 'ReservationCard',
  // stuff goes here
});

// Good
export default class ReservationCard extends React.Component {
}
```

**[⬆ back to top](#table-of-contents)**

## Alignment

* [5.1](#5.1) <a name="5.1"></a> Follow these alignment styles for JSX syntax. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

```javascript
// Bad
<Foo superLongParam="bar"
     anotherSuperLongParam="baz" />

// Good
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
/>

// if props fit in one line then keep it on the same line
<Foo bar="bar" />

// children get indented normally
<Foo
  superLongParam="bar"
  anotherSuperLongParam="baz"
>
  <Quux />
</Foo>
```

**[⬆ back to top](#table-of-contents)**

## Quotes

* [6.1](#6.1) <a name="6.1"></a> Always use double quotes (`"`) for JSX attributes, but single quotes for all other JS. eslint: [`jsx-quotes`](http://eslint.org/docs/rules/jsx-quotes)

> Why? JSX attributes [can't contain escaped quotes](http://eslint.org/docs/rules/jsx-quotes), so double quotes make conjunctions like `"don't"` easier to type.
> Regular HTML attributes also typically use double quotes instead of single, so JSX attributes mirror this convention.

```javascript
// Bad
<Foo bar='bar' />

// Good
<Foo bar="bar" />

// Bad
<Foo style={{ left: "20px" }} />

// Good
<Foo style={{ left: '20px' }} />
```

**[⬆ back to top](#table-of-contents)**

## Spacing

* [7.1](#7.1) <a name="7.1"></a> Always include a single space in your self-closing tag.

```javascript
// Bad
<Foo/>

// Very bad
<Foo                 />

// Bad
<Foo
 />

// Good
<Foo />
```

**[⬆ back to top](#table-of-contents)**

## Props

* [8.1](#8.1) <a name="8.1"></a> Always use camelCase for prop names.

```javascript
// Bad
<Foo
  UserName="hello"
  phone_number={12345678}
/>

// Good
<Foo
  userName="hello"
  phoneNumber={12345678}
/>
```

* [8.2](#8.2) <a name="8.2"></a> Omit the value of the prop when it is explicitly `true`. eslint: [`react/jsx-boolean-value`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-boolean-value.md)

```javascript
// Bad
<Foo
  hidden={true}
/>

// Good
<Foo
  hidden
/>
```

**[⬆ back to top](#table-of-contents)**

## Parentheses

* [9.1](#9.1) <a name="9.1"></a> Wrap JSX tags in parentheses when they span more than one line. eslint: [`react/wrap-multilines`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/wrap-multilines.md)

```javascript
// Bad
render() {
  return <MyComponent className="long body" foo="bar">
           <MyChild />
         </MyComponent>;
}

// Good
render() {
  return (
    <MyComponent className="long body" foo="bar">
      <MyChild />
    </MyComponent>
  );
}

// Good, when single line
render() {
  const body = <div>hello</div>;
  return <MyComponent>{body}</MyComponent>;
}
```

**[⬆ back to top](#table-of-contents)**

## Tags

* [10.1](#10.1) <a name="10.1"></a> Always self-close tags that have no children. eslint: [`react/self-closing-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/self-closing-comp.md)

```javascript
// Bad
<Foo className="stuff"></Foo>

// Good
<Foo className="stuff" />
```

* [10.2](#10.2) <a name="10.2"></a> If your component has multi-line properties, close its tag on a new line. eslint: [`react/jsx-closing-bracket-location`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-closing-bracket-location.md)

```javascript
// Bad
<Foo
  bar="bar"
  baz="baz" />

// Good
<Foo
  bar="bar"
  baz="baz"
/>
```

**[⬆ back to top](#table-of-contents)**

## Methods

* [11.1](#11.1) <a name="11.1"></a> Bind event handlers for the render method in the constructor. eslint: [`react/jsx-no-bind`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/jsx-no-bind.md)

> Why? A bind call in the render path creates a brand new function on every single render.

```javascript
// Bad
class extends React.Component {
  onClickDiv() {
    // do stuff
  }

  render() {
    return <div onClick={this.onClickDiv.bind(this)} />
  }
}

// Good
class extends React.Component {
  constructor(props) {
    super(props);

    this.onClickDiv = this.onClickDiv.bind(this);
  }

  onClickDiv() {
    // do stuff
  }

  render() {
    return <div onClick={this.onClickDiv} />
  }
}
```

* [11.2](#11.2) <a name="11.2"></a> Do not use underscore prefix for internal methods of a React component.

```javascript
// Bad
React.createClass({
  _onClickSubmit() {
    // do stuff
  },

  // other stuff
});

// Good
class extends React.Component {
  onClickSubmit() {
    // do stuff
  }

  // other stuff
}
```

**[⬆ back to top](#table-of-contents)**

## Ordering

* [12.1](#12.1) <a name="12.1"></a> Ordering for `class extends React.Component`:

1. optional `static` methods
2. `constructor`
3. `getChildContext`
4. `componentWillMount`
5. `componentDidMount`
6. `componentWillReceiveProps`
7. `shouldComponentUpdate`
8. `componentWillUpdate`
9. `componentDidUpdate`
10. `componentWillUnmount`
11. *clickHandlers or eventHandlers* like `onClickSubmit()` or `onChangeDescription()`
12. *getter methods for `render`* like `getSelectReason()` or `getFooterContent()`
13. *Optional render methods* like `renderNavigation()` or `renderProfilePicture()`
14. `render`

* [12.2](#12.2) <a name="12.2"></a> How to define `propTypes`, `defaultProps`, `contextTypes`, etc...

```javascript
import React, { PropTypes } from 'react';

const propTypes = {
  id: PropTypes.number.isRequired,
  url: PropTypes.string.isRequired,
  text: PropTypes.string,
};

const defaultProps = {
  text: 'Hello World',
};

class Link extends React.Component {
  static methodsAreOk() {
    return true;
  }

  render() {
    return <a href={this.props.url} data-id={this.props.id}>{this.props.text}</a>
  }
}

Link.propTypes = propTypes;
Link.defaultProps = defaultProps;

export default Link;
```

* [12.3](#12.3) <a name="12.3"></a> Ordering for `React.createClass`: eslint: [`react/sort-comp`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/sort-comp.md)

1. `displayName`
2. `propTypes`
3. `contextTypes`
4. `childContextTypes`
5. `mixins`
6. `statics`
7. `defaultProps`
8. `getDefaultProps`
9. `getInitialState`
10. `getChildContext`
11. `componentWillMount`
12. `componentDidMount`
13. `componentWillReceiveProps`
14. `shouldComponentUpdate`
15. `componentWillUpdate`
16. `componentDidUpdate`
17. `componentWillUnmount`
18. *clickHandlers or eventHandlers* like `onClickSubmit()` or `onChangeDescription()`
19. *getter methods for `render`* like `getSelectReason()` or `getFooterContent()`
20. *Optional render methods* like `renderNavigation()` or `renderProfilePicture()`
21. `render`

**[⬆ back to top](#table-of-contents)**

## `isMounted`

* [13.1](#13.1) <a name="13.1"></a> Do not use `isMounted`. eslint: [`react/no-is-mounted`](https://github.com/yannickcr/eslint-plugin-react/blob/master/docs/rules/no-is-mounted.md)

> Why? [`isMounted` is an anti-pattern][anti-pattern], is not available when using ES6 classes, and is on its way to being officially deprecated.

[anti-pattern]: https://facebook.github.io/react/blog/2015/12/16/ismounted-antipattern.html

**[⬆ back to top](#table-of-contents)**

## Resources

### Inspiration

* [Airbnb JavaScript Style Guide](https://github.com/airbnb/javascript)

**[⬅ back to main](../../../)**&nbsp;&nbsp;&nbsp;&nbsp;**[⬆ back to top](#table-of-contents)**
