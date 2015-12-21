---
title: Rule no-empty-pattern
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow empty destructuring patterns (no-empty-pattern)
# 禁止空的解构模式 (no-empty-pattern)

When using destructuring, it's possible to create a pattern that has no effect. This happens when empty curly braces are used to the right of an embedded object destructuring pattern, such as:

当使用解构时，它可以创建一个没有副作用的模式。这个发生在空花括号被正确用于嵌入式对象解构模式时，例如：

```
// doesn't create any variables
var {a: {}} = foo;
```

In this code, no new variables are created because `a` is just a location helper while the `{}` is expected to contain the variables to create, such as:

在以上代码中，没有创建新的变量因为`a`只是一个辅助作用而`{}`预计用包裹变量来创建变量，例如：

```
// creates variable b
var {a: { b }} = foo;
```

In many cases, the empty object pattern is a mistake where the author intended to use a default value instead, such as:

在许多情况中，作者意图使用默认值替换的空对象模式是一个错误，例如：

```
// creates variable a
var {a = {}} = foo;
```

The difference between these two patterns is subtle, especially because the problematic empty pattern looks just like an object literal.

这两种模式之间的区别是不明显的，尤其是因为有问题的空模式看起来就像对象字面量。

## Rule Details

This rule aims to flag any empty patterns in destructured objects and arrays, and as such, will report a problem whenever one is encountered.

此规则目的在于标记出在对象和数组中的任何的空模式，因此，每当遇到这样一个空模式就会报告一个错误。


The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-empty-pattern: 2*/

var {} = foo;
var [] = foo;
var {a: {}} = foo;
var {a: []} = foo;
function foo({}) {}
function foo([]) {}
function foo({a: {}}) {}
function foo({a: []}) {}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-empty-pattern: 2*/

var {a = {}} = foo;
var {a = []} = foo;
function foo({a = {}}) {}
function foo({a = []}) {}
```

## Version

This rule was introduced in ESLint 1.7.0.

此规则在ESLint 1.7.0中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-empty-pattern.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-empty-pattern.md)
