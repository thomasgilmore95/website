---
title: no-continue - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-continue.md
rule_type: suggestion
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# disallow `continue` statements (no-continue)

The `continue` statement terminates execution of the statements in the current iteration of the current or labeled loop, and continues execution of the loop with the next iteration. When used incorrectly it makes code less testable, less readable and less maintainable. Structured control flow statements such as `if` should be used instead.

```js
var sum = 0,
    i;

for(i = 0; i < 10; i++) {
    if(i >= 5) {
        continue;
    }

    a += i;
}
```

## Rule Details

This rule disallows `continue` statements.

Examples of **incorrect** code for this rule:

```js
/*eslint no-continue: "error"*/

var sum = 0,
    i;

for(i = 0; i < 10; i++) {
    if(i >= 5) {
        continue;
    }

    a += i;
}
```

```js
/*eslint no-continue: "error"*/

var sum = 0,
    i;

labeledLoop: for(i = 0; i < 10; i++) {
    if(i >= 5) {
        continue labeledLoop;
    }

    a += i;
}
```

Examples of **correct** code for this rule:

```js
/*eslint no-continue: "error"*/

var sum = 0,
    i;

for(i = 0; i < 10; i++) {
    if(i < 5) {
       a += i;
    }
}
```

## Compatibility

* **JSLint**: `continue`

## Version

This rule was introduced in ESLint 0.19.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-continue.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-continue.md)
