---
title: no-confusing-arrow - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-confusing-arrow.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow arrow functions where they could be confused with comparisons (no-confusing-arrow)

(fixable) The `--fix` option on the [command line](../user-guide/command-line-interface#fixing-problems) can automatically fix some of the problems reported by this rule.

Arrow functions (`=>`) are similar in syntax to some comparison operators (`>`, `<`, `<=`, and `>=`). This rule warns against using the arrow function syntax in places where it could be confused with a comparison operator.

Here's an example where the usage of `=>` could be confusing:

```js
// The intent is not clear
var x = a => 1 ? 2 : 3;
// Did the author mean this
var x = function (a) { return 1 ? 2 : 3 };
// Or this
var x = a <= 1 ? 2 : 3;
```

## Rule Details

Examples of **incorrect** code for this rule:

```js
/*eslint no-confusing-arrow: "error"*/
/*eslint-env es6*/

var x = a => 1 ? 2 : 3;
var x = (a) => 1 ? 2 : 3;
```

Examples of **correct** code for this rule:

```js
/*eslint no-confusing-arrow: "error"*/
/*eslint-env es6*/

var x = a => (1 ? 2 : 3);
var x = (a) => (1 ? 2 : 3);
var x = a => { return 1 ? 2 : 3; };
var x = (a) => { return 1 ? 2 : 3; };
```

## Options

This rule accepts a single options argument with the following defaults:

```json
{
    "rules": {
        "no-confusing-arrow": ["error", {"allowParens": true}]
    }
}
```

`allowParens` is a boolean setting that can be `true`(default) or `false`:

1. `true` relaxes the rule and accepts parenthesis as a valid "confusion-preventing" syntax.
2. `false` warns even if the expression is wrapped in parenthesis

Examples of **incorrect** code for this rule with the `{"allowParens": false}` option:

```js
/*eslint no-confusing-arrow: ["error", {"allowParens": false}]*/
/*eslint-env es6*/
var x = a => (1 ? 2 : 3);
var x = (a) => (1 ? 2 : 3);
```

## Related Rules

* [no-constant-condition](no-constant-condition)
* [arrow-parens](arrow-parens)

## Version

This rule was introduced in ESLint 2.0.0-alpha-2.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-confusing-arrow.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-confusing-arrow.md)
