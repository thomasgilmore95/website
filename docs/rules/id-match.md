---
title: id-match - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/id-match.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# require identifiers to match a specified regular expression (id-match)

> "There are only two hard things in Computer Science: cache invalidation and naming things." — Phil Karlton

Naming things consistently in a project is an often underestimated aspect of code creation.
When done correctly, it can save your team hours of unnecessary head scratching and misdirections.
This rule allows you to precisely define and enforce the variables and function names on your team should use.
No more limiting yourself to camelCase, snake_case, PascalCase or oHungarianNotation. Id-match has all your needs covered!

## Rule Details

This rule requires identifiers in assignments and `function` definitions to match a specified regular expression.

## Options

This rule has a string option for the specified regular expression.

For example, to enforce a camelcase naming convention:

```json
{
    "id-match": ["error", "^[a-z]+([A-Z][a-z]+)*$"]
}
```

Examples of **incorrect** code for this rule with the `"^[a-z]+([A-Z][a-z]+)*$"` option:

```js
/*eslint id-match: ["error", "^[a-z]+([A-Z][a-z]+)*$"]*/

var my_favorite_color = "#112C85";
var _myFavoriteColor  = "#112C85";
var myFavoriteColor_  = "#112C85";
var MY_FAVORITE_COLOR = "#112C85";
function do_something() {
    // ...
}

obj.do_something = function() {
    // ...
};

class My_Class {}

class myClass {
    do_something() {}
}

class myClass {
    #do_something() {}
}
```

Examples of **correct** code for this rule with the `"^[a-z]+([A-Z][a-z]+)*$"` option:

```js
/*eslint id-match: ["error", "^[a-z]+([A-Z][a-z]+)*$"]*/

var myFavoriteColor   = "#112C85";
var foo = bar.baz_boom;
var foo = { qux: bar.baz_boom };
do_something();
var obj = {
    my_pref: 1
};

class myClass {}

class myClass {
    doSomething() {}
}

class myClass {
    #doSomething() {}
}
```

This rule has an object option:

* `"properties": false` (default) does not check object properties
* `"properties": true` requires object literal properties and member expression assignment properties to match the specified regular expression
* `"classFields": false` (default) does not class field names
* `"classFields": true` requires class field names to match the specified regular expression
* `"onlyDeclarations": false` (default) requires all variable names to match the specified regular expression
* `"onlyDeclarations": true` requires only `var`, `function`, and `class` declarations to match the specified regular expression
* `"ignoreDestructuring": false` (default) enforces `id-match` for destructured identifiers
* `"ignoreDestructuring": true` does not check destructured identifiers

### properties

Examples of **incorrect** code for this rule with the `"^[a-z]+([A-Z][a-z]+)*$", { "properties": true }` options:

```js
/*eslint id-match: ["error", "^[a-z]+([A-Z][a-z]+)*$", { "properties": true }]*/

var obj = {
    my_pref: 1
};
```

### classFields

Examples of **incorrect** code for this rule with the `"^[a-z]+([A-Z][a-z]+)*$", { "classFields": true }` options:

```js
/*eslint id-match: ["error", "^[a-z]+([A-Z][a-z]+)*$", { "properties": true }]*/

class myClass {
    my_pref = 1;
}

class myClass {
    #my_pref = 1;
}
```

### onlyDeclarations

Examples of **correct** code for this rule with the `"^[a-z]+([A-Z][a-z]+)*$", { "onlyDeclarations": true }` options:

```js
/*eslint id-match: [2, "^[a-z]+([A-Z][a-z]+)*$", { "onlyDeclarations": true }]*/

do_something(__dirname);
```

### ignoreDestructuring: false

Examples of **incorrect** code for this rule with the default `"^[^_]+$", { "ignoreDestructuring": false }` option:

```js
/*eslint id-match: [2, "^[^_]+$", { "ignoreDestructuring": false }]*/

var { category_id } = query;

var { category_id = 1 } = query;

var { category_id: category_id } = query;

var { category_id: category_alias } = query;

var { category_id: categoryId, ...other_props } = query;
```

### ignoreDestructuring: true

Examples of **incorrect** code for this rule with the `"^[^_]+$", { "ignoreDestructuring": true }` option:

```js
/*eslint id-match: [2, "^[^_]+$", { "ignoreDestructuring": true }]*/

var { category_id: category_alias } = query;

var { category_id, ...other_props } = query;
```

Examples of **correct** code for this rule with the `"^[^_]+$", { "ignoreDestructuring": true }` option:

```js
/*eslint id-match: [2, "^[^_]+$", { "ignoreDestructuring": true }]*/

var { category_id } = query;

var { category_id = 1 } = query;

var { category_id: category_id } = query;
```

## When Not To Use It

If you don't want to enforce any particular naming convention for all identifiers, or your naming convention is too complex to be enforced by configuring this rule, then you should not enable this rule.

## Version

This rule was introduced in ESLint 1.0.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/id-match.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/id-match.md)
