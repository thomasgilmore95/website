---
title: no-cond-assign - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-cond-assign.md
rule_type: problem
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# disallow assignment operators in conditional statements (no-cond-assign)

(recommended) The `"extends": "eslint:recommended"` property in a configuration file enables this rule.

In conditional statements, it is very easy to mistype a comparison operator (such as `==`) as an assignment operator (such as `=`). For example:

```js
// Check the user's job title
if (user.jobTitle = "manager") {
    // user.jobTitle is now incorrect
}
```

There are valid reasons to use assignment operators in conditional statements. However, it can be difficult to tell whether a specific assignment was intentional.

## Rule Details

This rule disallows ambiguous assignment operators in test conditions of `if`, `for`, `while`, and `do...while` statements.

## Options

This rule has a string option:

* `"except-parens"` (default) allows assignments in test conditions *only if* they are enclosed in parentheses (for example, to allow reassigning a variable in the test of a `while` or `do...while` loop)
* `"always"` disallows all assignments in test conditions

### except-parens

Examples of **incorrect** code for this rule with the default `"except-parens"` option:

```js
/*eslint no-cond-assign: "error"*/

// Unintentional assignment
var x;
if (x = 0) {
    var b = 1;
}

// Practical example that is similar to an error
function setHeight(someNode) {
    "use strict";
    do {
        someNode.height = "100px";
    } while (someNode = someNode.parentNode);
}
```

Examples of **correct** code for this rule with the default `"except-parens"` option:

```js
/*eslint no-cond-assign: "error"*/

// Assignment replaced by comparison
var x;
if (x === 0) {
    var b = 1;
}

// Practical example that wraps the assignment in parentheses
function setHeight(someNode) {
    "use strict";
    do {
        someNode.height = "100px";
    } while ((someNode = someNode.parentNode));
}

// Practical example that wraps the assignment and tests for 'null'
function setHeight(someNode) {
    "use strict";
    do {
        someNode.height = "100px";
    } while ((someNode = someNode.parentNode) !== null);
}
```

### always

Examples of **incorrect** code for this rule with the `"always"` option:

```js
/*eslint no-cond-assign: ["error", "always"]*/

// Unintentional assignment
var x;
if (x = 0) {
    var b = 1;
}

// Practical example that is similar to an error
function setHeight(someNode) {
    "use strict";
    do {
        someNode.height = "100px";
    } while (someNode = someNode.parentNode);
}

// Practical example that wraps the assignment in parentheses
function setHeight(someNode) {
    "use strict";
    do {
        someNode.height = "100px";
    } while ((someNode = someNode.parentNode));
}

// Practical example that wraps the assignment and tests for 'null'
function setHeight(someNode) {
    "use strict";
    do {
        someNode.height = "100px";
    } while ((someNode = someNode.parentNode) !== null);
}
```

Examples of **correct** code for this rule with the `"always"` option:

```js
/*eslint no-cond-assign: ["error", "always"]*/

// Assignment replaced by comparison
var x;
if (x === 0) {
    var b = 1;
}
```

## Related Rules

* [no-extra-parens](no-extra-parens)

## Version

This rule was introduced in ESLint 0.0.9.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-cond-assign.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-cond-assign.md)
