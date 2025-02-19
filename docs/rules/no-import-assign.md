---
title: no-import-assign - Rules
layout: doc
edit_link: https://github.com/eslint/eslint/edit/main/docs/rules/no-import-assign.md
rule_type: problem
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# disallow assigning to imported bindings (no-import-assign)

(recommended) The `"extends": "eslint:recommended"` property in a configuration file enables this rule.

The updates of imported bindings by ES Modules cause runtime errors.

## Rule Details

This rule warns the assignments, increments, and decrements of imported bindings.

Examples of **incorrect** code for this rule:

```js
/*eslint no-import-assign: "error"*/

import mod, { named } from "./mod.mjs"
import * as mod_ns from "./mod.mjs"

mod = 1          // ERROR: 'mod' is readonly.
named = 2        // ERROR: 'named' is readonly.
mod_ns.named = 3 // ERROR: The members of 'mod_ns' are readonly.
mod_ns = {}      // ERROR: 'mod_ns' is readonly.
// Can't extend 'mod_ns'
Object.assign(mod_ns, { foo: "foo" }) // ERROR: The members of 'mod_ns' are readonly.
```

Examples of **correct** code for this rule:

```js
/*eslint no-import-assign: "error"*/

import mod, { named } from "./mod.mjs"
import * as mod_ns from "./mod.mjs"

mod.prop = 1
named.prop = 2
mod_ns.named.prop = 3

// Known Limitation
function test(obj) {
    obj.named = 4 // Not errored because 'obj' is not namespace objects.
}
test(mod_ns) // Not errored because it doesn't know that 'test' updates the member of the argument.
```

## When Not To Use It

If you don't want to be notified about modifying imported bindings, you can disable this rule.

## Version

This rule was introduced in ESLint 6.4.0.

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/HEAD/lib/rules/no-import-assign.js)
* [Documentation source](https://github.com/eslint/eslint/tree/HEAD/docs/rules/no-import-assign.md)
