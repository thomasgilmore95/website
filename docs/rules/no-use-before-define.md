---
title: no-use-before-define - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-use-before-define.md
rule_type: problem
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow Early Use (no-use-before-define)

In JavaScript, prior to ES6, variable and function declarations are hoisted to the top of a scope, so it's possible to use identifiers before their formal declarations in code. This can be confusing and some believe it is best to always declare variables and functions before using them.

In ES6, block-level bindings (`let` and `const`) introduce a "temporal dead zone" where a `ReferenceError` will be thrown with any attempt to access the variable before its declaration.

## Rule Details

This rule will warn when it encounters a reference to an identifier that has not yet been declared.

Examples of **incorrect** code for this rule:

```js
/*eslint no-use-before-define: "error"*/
/*eslint-env es6*/

alert(a);
var a = 10;

f();
function f() {}

function g() {
    return b;
}
var b = 1;

{
    alert(c);
    let c = 1;
}
```

Examples of **correct** code for this rule:

```js
/*eslint no-use-before-define: "error"*/
/*eslint-env es6*/

var a;
a = 10;
alert(a);

function f() {}
f(1);

var b = 1;
function g() {
    return b;
}

{
    let c;
    c++;
}
```

## Options

```json
{
    "no-use-before-define": ["error", { "functions": true, "classes": true }]
}
```

* `functions` (`boolean`) -
  The flag which shows whether or not this rule checks function declarations.
  If this is `true`, this rule warns every reference to a function before the function declaration.
  Otherwise, ignores those references.
  Function declarations are hoisted, so it's safe.
  Default is `true`.
* `classes` (`boolean`) -
  The flag which shows whether or not this rule checks class declarations of upper scopes.
  If this is `true`, this rule warns every reference to a class before the class declaration.
  Otherwise, ignores those references if the declaration is in upper function scopes.
  Class declarations are not hoisted, so it might be danger.
  Default is `true`.
* `variables` (`boolean`) -
  This flag determines whether or not the rule checks variable declarations in upper scopes.
  If this is `true`, the rule warns every reference to a variable before the variable declaration.
  Otherwise, the rule ignores a reference if the declaration is in an upper scope, while still reporting the reference if it's in the same scope as the declaration.
  Default is `true`.

This rule accepts `"nofunc"` string as an option.
`"nofunc"` is the same as `{ "functions": false, "classes": true, "variables": true }`.

### functions

Examples of **correct** code for the `{ "functions": false }` option:

```js
/*eslint no-use-before-define: ["error", { "functions": false }]*/

f();
function f() {}
```

This option allows references to function declarations. For function expressions and arrow functions, please see the [`variables`](#variables) option.

### classes

Examples of **incorrect** code for the `{ "classes": false }` option:

```js
/*eslint no-use-before-define: ["error", { "classes": false }]*/
/*eslint-env es6*/

new A();
class A {
}
```

Examples of **correct** code for the `{ "classes": false }` option:

```js
/*eslint no-use-before-define: ["error", { "classes": false }]*/
/*eslint-env es6*/

function foo() {
    return new A();
}

class A {
}
```

### variables

Examples of **incorrect** code for the `{ "variables": false }` option:

```js
/*eslint no-use-before-define: ["error", { "variables": false }]*/

console.log(foo);
var foo = 1;

f();
const f = () => {};

g();
const g = function() {};
```

Examples of **correct** code for the `{ "variables": false }` option:

```js
/*eslint no-use-before-define: ["error", { "variables": false }]*/

function baz() {
    console.log(foo);
}
var foo = 1;

const a = () => f();
function b() { return f(); }
const c = function() { return f(); }
const f = () => {};

const e = function() { return g(); }
const g = function() {}
```

## Version

This rule was introduced in ESLint 0.0.9.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-use-before-define.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-use-before-define.md)
