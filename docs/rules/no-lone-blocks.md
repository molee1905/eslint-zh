---
title: Rule no-lone-blocks
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Unnecessary Nested Blocks (no-lone-blocks)

# 禁止不必要的嵌套块 (no-lone-blocks)

In JavaScript, prior to ES6, standalone code blocks delimited by curly braces do not create a new scope and have no use. For example, these curly braces do nothing to `foo`:

在JavaScript中，ES6之前，限定在花括号中的独立代码块不会创建一个新的作用域并且没有用途。例如，下面的花括号对`foo`起不到什么作用：

```js
{
    var foo = bar();
}
```

In ES6, code blocks may create a new scope if a block-level binding (`let` and `const`), a class declaration or a function declaration (in strict mode) are present. A block is not considered redundant in these cases.

在ES6中，代码块可能会创建一个新的作用域如果被块级绑定(`let`和 `const`)，类声明或者函数声明（在严格模式下）就是这样。在这些情况下块不被认为是冗余的。

## Rule details

This rule aims to eliminate unnecessary and potentially confusing blocks at the top level of a script or within other blocks.

此规则目的在于消除不必要的和潜在混淆的块存在于脚本的顶部或者其他块中。

The following patterns are considered problems:

以下默认被认为是有问题的：

```js
/*eslint no-lone-blocks: 2*/

{}                    /*error Block is redundant.*/

if (foo) {
    bar();
    {                 /*error Nested block is redundant.*/
        baz();
    }
}

function bar() {
    {                 /*error Nested block is redundant.*/
        baz();
    }
}

{                     /*error Block is redundant.*/
    function foo() {}
}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint-env es6*/
/*eslint no-lone-blocks: 2*/

while (foo) {
    bar();
}

if (foo) {
    if (bar) {
        baz();
    }
}

function bar() {
    baz();
}

{
    let x = 1;
}

{
    const y = 1;
}

{
    class Foo {}
}
```

In strict mode, with `ecmaFeatures: { blockBindings: true }`, the following will not warn:

在严格模式下，带有 `ecmaFeatures: { blockBindings: true }`这种形式，以下的模式不会出现警告：

```js
/*eslint-env es6*/
/*eslint no-lone-blocks: 2*/
"use strict";

{
    function foo() {}
}
```

## Version

This rule was introduced in ESLint 0.4.0.

此规则在ESLint 0.4.0中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-lone-blocks.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-lone-blocks.md)
