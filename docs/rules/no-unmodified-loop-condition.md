---
title: no-unmodified-loop-condition - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-unmodified-loop-condition.md
rule_type: problem
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow unmodified conditions of loops (no-unmodified-loop-condition)

Variables in a loop condition often are modified in the loop.
If not, it's possibly a mistake.

```js
while (node) {
    doSomething(node);
}
```

```js
while (node) {
    doSomething(node);
    node = node.parent;
}
```

## Rule Details

This rule finds references which are inside of loop conditions, then checks the
variables of those references are modified in the loop.

If a reference is inside of a binary expression or a ternary expression, this rule checks the result of
the expression instead.
If a reference is inside of a dynamic expression (e.g. `CallExpression`,
`YieldExpression`, ...), this rule ignores it.

Examples of **incorrect** code for this rule:

```js
/*eslint no-unmodified-loop-condition: "error"*/

var node = something;

while (node) {
    doSomething(node);
}
node = other;

for (var j = 0; j < items.length; ++i) {
    doSomething(items[j]);
}

while (node !== root) {
    doSomething(node);
}
```

Examples of **correct** code for this rule:

```js
/*eslint no-unmodified-loop-condition: "error"*/

while (node) {
    doSomething(node);
    node = node.parent;
}

for (var j = 0; j < items.length; ++j) {
    doSomething(items[j]);
}

// OK, the result of this binary expression is changed in this loop.
while (node !== root) {
    doSomething(node);
    node = node.parent;
}

// OK, the result of this ternary expression is changed in this loop.
while (node ? A : B) {
    doSomething(node);
    node = node.parent;
}

// A property might be a getter which has side effect...
// Or "doSomething" can modify "obj.foo".
while (obj.foo) {
    doSomething(obj);
}

// A function call can return various values.
while (check(obj)) {
    doSomething(obj);
}
```

## When Not To Use It

If you don't want to notified about references inside of loop conditions, then it's safe to disable this rule.

## Version

This rule was introduced in ESLint 2.0.0-alpha-2.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-unmodified-loop-condition.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-unmodified-loop-condition.md)
