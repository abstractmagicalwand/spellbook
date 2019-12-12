# Variables

A variable is a "named storage" for data.

We can declare variables to store data by using the var, let, or const keywords.

- `var` – is an old-school variable declaration.
- `let` – is a modern variable declaration. The code must be in strict mode to use let in Chrome (V8).
- `const` – is like let, but the value of the variable can’t be changed.

## Variable naming

1. The name must contain only letters, digits, or the symbols $ and _.
2. The first character must not be a digit.
3. There is a [list of reserved words](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Lexical_grammar#Keywords),
which cannot be used as variable names because they are used by the language itself.

## An assignment without "use strict"

```js
// note: no "use strict" in this example

num = 5; // the variable "num" is created if it didn't exist

alert(num); // 5
```

```js
'use strict';

num = 5; // Uncaught ReferenceError: num is not defined
```

## Constants

Variables declared using const are called "constants". They cannot be changed. An attempt to do so
would cause an error:

```js
const myBirthday = '18.04.1982';

myBirthday = '01.01.2001'; // Uncaught TypeError: Assignment to constant variable.
```

### Capital-named constants

```js
const COLOR_RED = '#F00';
```

We generally use upper case for constants that are "hard-coded". Or, in other words, when the value
is known prior to execution and directly written into the code.

## Details

- [Variables](http://javascript.info/variables#name-things-right)
