---
title: no-array-constructor - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-array-constructor.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# disallow `Array` constructors (no-array-constructor)

Use of the `Array` constructor to construct a new array is generally
discouraged in favor of array literal notation because of the single-argument
pitfall and because the `Array` global may be redefined. The exception is when
the Array constructor is used to intentionally create sparse arrays of a
specified size by giving the constructor a single numeric argument.

## Rule Details

This rule disallows `Array` constructors.

Examples of **incorrect** code for this rule:

```js
/*eslint no-array-constructor: "error"*/

Array(0, 1, 2)

new Array(0, 1, 2)
```

Examples of **correct** code for this rule:

```js
/*eslint no-array-constructor: "error"*/

Array(500)

new Array(someOtherArray.length)

[0, 1, 2]
```

## When Not To Use It

This rule enforces a nearly universal stylistic concern. That being said, this
rule may be disabled if the constructor style is preferred.

## Related Rules

* [no-new-object](no-new-object)
* [no-new-wrappers](no-new-wrappers)

## Version

This rule was introduced in ESLint 0.4.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-array-constructor.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-array-constructor.md)
