---
title: no-catch-shadow - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-catch-shadow.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow Shadowing of Variables Inside of catch (no-catch-shadow)

This rule was **deprecated** in ESLint v5.1.0.

In IE 8 and earlier, the catch clause parameter can overwrite the value of a variable in the outer scope, if that variable has the same name as the catch clause parameter.

```js
var err = "x";

try {
    throw "problem";
} catch (err) {

}

console.log(err)    // err is 'problem', not 'x'
```

## Rule Details

This rule is aimed at preventing unexpected behavior in your program that may arise from a bug in IE 8 and earlier, in which the catch clause parameter can leak into outer scopes. This rule will warn whenever it encounters a catch clause parameter that has the same name as a variable in an outer scope.

Examples of **incorrect** code for this rule:

```js
/*eslint no-catch-shadow: "error"*/

var err = "x";

try {
    throw "problem";
} catch (err) {

}

function err() {
    // ...
};

try {
    throw "problem";
} catch (err) {

}
```

Examples of **correct** code for this rule:

```js
/*eslint no-catch-shadow: "error"*/

var err = "x";

try {
    throw "problem";
} catch (e) {

}

function err() {
    // ...
};

try {
    throw "problem";
} catch (e) {

}
```

## When Not To Use It

If you do not need to support IE 8 and earlier, you should turn this rule off.

## Version

This rule was introduced in ESLint 0.0.9.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-catch-shadow.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-catch-shadow.md)
