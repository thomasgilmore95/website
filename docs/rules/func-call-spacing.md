---
title: func-call-spacing - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/func-call-spacing.md
rule_type: layout
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# require or disallow spacing between function identifiers and their invocations (func-call-spacing)

(fixable) The `--fix` option on the [command line](../user-guide/command-line-interface#fixing-problems) can automatically fix some of the problems reported by this rule.

When calling a function, developers may insert optional whitespace between the function's name and the parentheses that invoke it. The following pairs of function calls are equivalent:

```js
alert('Hello');
alert ('Hello');

console.log(42);
console.log (42);

new Date();
new Date ();
```

## Rule Details

This rule requires or disallows spaces between the function name and the opening parenthesis that calls it.

## options

This rule has a string option:

- `"never"` (default) disallows space between the function name and the opening parenthesis.
- `"always"` requires space between the function name and the opening parenthesis.

Further, in `"always"` mode, a second object option is available that contains a single boolean `allowNewlines` property.

### never

Examples of **incorrect** code for this rule with the default `"never"` option:

```js
/*eslint func-call-spacing: ["error", "never"]*/

fn ();

fn
();
```

Examples of **correct** code for this rule with the default `"never"` option:

```js
/*eslint func-call-spacing: ["error", "never"]*/

fn();
```

### always

Examples of **incorrect** code for this rule with the `"always"` option:

```js
/*eslint func-call-spacing: ["error", "always"]*/

fn();

fn
();
```

Examples of **correct** code for this rule with the `"always"` option:

```js
/*eslint func-call-spacing: ["error", "always"]*/

fn ();
```

#### allowNewlines

By default, `"always"` does not allow newlines. To permit newlines when in `"always"` mode, set the `allowNewlines` option to `true`. Newlines are never required.

Examples of **incorrect** code for this rule with `allowNewlines` option enabled:

```js
/*eslint func-call-spacing: ["error", "always", { "allowNewlines": true }]*/

fn();
```

Examples of **correct** code for this rule with the `allowNewlines` option enabled:

```js
/*eslint func-call-spacing: ["error", "always", { "allowNewlines": true }]*/

fn (); // Newlines are never required.

fn
();
```

## When Not To Use It

This rule can safely be turned off if your project does not care about enforcing a consistent style for spacing within function calls.

## Related Rules

- [no-spaced-func](no-spaced-func) (deprecated)

## Compatibility

- **JSCS**: [disallowSpacesInCallExpression](https://jscs-dev.github.io/rule/disallowSpacesInCallExpression)
- **JSCS**: [requireSpacesInCallExpression](https://jscs-dev.github.io/rule/requireSpacesInCallExpression)

## Version

This rule was introduced in ESLint 3.3.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/func-call-spacing.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/func-call-spacing.md)
