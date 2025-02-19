---
title: no-shadow-restricted-names - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-shadow-restricted-names.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow Shadowing of Restricted Names (no-shadow-restricted-names)

(recommended) The `"extends": "eslint:recommended"` property in a configuration file enables this rule.

ES5 §15.1.1 Value Properties of the Global Object (`NaN`, `Infinity`, `undefined`) as well as strict mode restricted identifiers `eval` and `arguments` are considered to be restricted names in JavaScript. Defining them to mean something else can have unintended consequences and confuse others reading the code. For example, there's nothing preventing you from writing:

```js
var undefined = "foo";
```

Then any code used within the same scope would not get the global `undefined`, but rather the local version with a very different meaning.

## Rule Details

Examples of **incorrect** code for this rule:

```js
/*eslint no-shadow-restricted-names: "error"*/

function NaN(){}

!function(Infinity){};

var undefined = 5;

try {} catch(eval){}
```

Examples of **correct** code for this rule:

```js
/*eslint no-shadow-restricted-names: "error"*/

var Object;

function f(a, b){}

// Exception: `undefined` may be shadowed if the variable is never assigned a value.
var undefined;
```

## Further Reading

* [Annotated ES5 - §15.1.1](https://es5.github.io/#x15.1.1)
* [Annotated ES5 - Annex C](https://es5.github.io/#C)

## Related Rules

* [no-shadow](no-shadow)

## Version

This rule was introduced in ESLint 0.1.4.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-shadow-restricted-names.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-shadow-restricted-names.md)
