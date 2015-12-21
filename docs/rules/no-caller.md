---
title: Rule no-caller
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Use of caller/callee (no-caller)

# 禁用caller或callee (no-caller)

The use of `arguments.caller` and `arguments.callee` make several code optimizations impossible. They have been deprecated in future versions of JavaScript and their use is forbidden in ECMAScript 5 while in strict mode.

`arguments.caller` 和 `arguments.callee`的使用使一些代码优化变得不可能。在JavaScript的未来版本中他们已被弃用，同时在ECMAScript 5的严格模式下，也是被禁用的。


```js
function foo() {
    var callee = arguments.callee;
}
```

## Rule Details

This rule is aimed at discouraging the use of deprecated and sub-optimal code, but disallowing the use of `arguments.caller` and `arguments.callee`. As such, it will warn when `arguments.caller` and `arguments.callee` are used.

此规则目的在于，阻止使用已弃用的代码和次优的代码，而且禁止使用`arguments.caller` 和 `arguments.callee`。因此，当`arguments.caller` 和 `arguments.callee`被使用时会给出警告。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-caller: 2*/

function foo(n) {
    if (n <= 0) {
        return;
    }

    arguments.callee(n - 1);   /*error Avoid arguments.callee.*/
}

[1,2,3,4,5].map(function(n) {
    return !(n > 1) ? 1 : arguments.callee(n - 1) * n; /*error Avoid arguments.callee.*/
});
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-caller: 2*/

function foo(n) {
    if (n <= 0) {
        return;
    }

    foo(n - 1);
}

[1,2,3,4,5].map(function factorial(n) {
    return !(n > 1) ? 1 : factorial(n - 1) * n;
});
```

## Version

This rule was introduced in ESLint 0.0.6.

此规则在ESLint 0.0.6中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-caller.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-caller.md)
