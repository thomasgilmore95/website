---
title: prefer-named-capture-group - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/prefer-named-capture-group.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Suggest using named capture group in regular expression (prefer-named-capture-group)


## Rule Details

With the landing of ECMAScript 2018, named capture groups can be used in regular expressions, which can improve their readability.
This rule is aimed at using named capture groups instead of numbered capture groups in regular expressions:

```js
const regex = /(?<year>[0-9]{4})/;
```

Alternatively, if your intention is not to _capture_ the results, but only express the alternative, use a non-capturing group:

```js
const regex = /(?:cauli|sun)flower/;
```

Examples of **incorrect** code for this rule:

```js
/*eslint prefer-named-capture-group: "error"*/

const foo = /(ba[rz])/;
const bar = new RegExp('(ba[rz])');
const baz = RegExp('(ba[rz])');

foo.exec('bar')[1]; // Retrieve the group result.
```

Examples of **correct** code for this rule:

```js
/*eslint prefer-named-capture-group: "error"*/

const foo = /(?<id>ba[rz])/;
const bar = new RegExp('(?<id>ba[rz])');
const baz = RegExp('(?<id>ba[rz])');
const xyz = /xyz(?:zy|abc)/;

foo.exec('bar').groups.id; // Retrieve the group result.
```

## When Not To Use It

If you are targeting ECMAScript 2017 and/or older environments, you should not use this rule, because this ECMAScript feature is only supported in ECMAScript 2018 and/or newer environments.

## Related Rules

* [no-invalid-regexp](./no-invalid-regexp)

## Version

This rule was introduced in ESLint 5.15.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/prefer-named-capture-group.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/prefer-named-capture-group.md)
