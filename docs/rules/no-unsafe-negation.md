---
title: no-unsafe-negation - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-unsafe-negation.md
rule_type: problem
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# disallow negating the left operand of relational operators (no-unsafe-negation)

(recommended) The `"extends": "eslint:recommended"` property in a configuration file enables this rule.

(hasSuggestions) Some problems reported by this rule are manually fixable by editor [suggestions](../developer-guide/working-with-rules#providing-suggestions).

Just as developers might type `-a + b` when they mean `-(a + b)` for the negative of a sum, they might type `!key in object` by mistake when they almost certainly mean `!(key in object)` to test that a key is not in an object. `!obj instanceof Ctor` is similar.

## Rule Details

This rule disallows negating the left operand of the following relational operators:

- [`in` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/in).
- [`instanceof` operator](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/instanceof).

Examples of **incorrect** code for this rule:

```js
/*eslint no-unsafe-negation: "error"*/

if (!key in object) {
    // operator precedence makes it equivalent to (!key) in object
    // and type conversion makes it equivalent to (key ? "false" : "true") in object
}

if (!obj instanceof Ctor) {
    // operator precedence makes it equivalent to (!obj) instanceof Ctor
    // and it equivalent to always false since boolean values are not objects.
}
```

Examples of **correct** code for this rule:

```js
/*eslint no-unsafe-negation: "error"*/

if (!(key in object)) {
    // key is not in object
}

if (!(obj instanceof Ctor)) {
    // obj is not an instance of Ctor
}
```

### Exception

For rare situations when negating the left operand is intended, this rule allows an exception.
If the whole negation is explicitly wrapped in parentheses, the rule will not report a problem.

Examples of **correct** code for this rule:

```js
/*eslint no-unsafe-negation: "error"*/

if ((!foo) in object) {
    // allowed, because the negation is explicitly wrapped in parentheses
    // it is equivalent to (foo ? "false" : "true") in object
    // this is allowed as an exception for rare situations when that is the intended meaning
}

if(("" + !foo) in object) {
    // you can also make the intention more explicit, with type conversion
}
```

Examples of **incorrect** code for this rule:

```js
/*eslint no-unsafe-negation: "error"*/

if (!(foo) in object) {
    // this is not an allowed exception
}
```

## Options

This rule has an object option:

- `"enforceForOrderingRelations": false` (default) allows negation of the left-hand side of ordering relational operators (`<`, `>`, `<=`, `>=`)
- `"enforceForOrderingRelations": true` disallows negation of the left-hand side of ordering relational operators

### enforceForOrderingRelations

With this option set to `true` the rule is additionally enforced for:

- `<` operator.
- `>` operator.
- `<=` operator.
- `>=` operator.

The purpose is to avoid expressions such as `! a < b` (which is equivalent to `(a ? 0 : 1) < b`) when what is really intended is `!(a < b)`.

Examples of additional **incorrect** code for this rule with the `{ "enforceForOrderingRelations": true }` option:

```js
/*eslint no-unsafe-negation: ["error", { "enforceForOrderingRelations": true }]*/

if (! a < b) {}

while (! a > b) {}

foo = ! a <= b;

foo = ! a >= b;
```

## When Not To Use It

If you don't want to notify unsafe logical negations, then it's safe to disable this rule.

## Version

This rule was introduced in ESLint 3.3.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-unsafe-negation.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-unsafe-negation.md)
