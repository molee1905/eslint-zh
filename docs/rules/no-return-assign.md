---
title: Rule no-return-assign
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow Assignment in return Statement (no-return-assign)

# 禁止给返回语句赋值 (no-return-assign)

One of the interesting, and sometimes confusing, aspects of JavaScript is that assignment can happen at almost any point. Because of this, an errant equals sign can end up causing assignment when the true intent was to do a comparison. This is especially true when using a `return` statement. For example:

JavaScript有趣的，有时又是困惑的是，赋值可以发生在任何位置。正因如此，错误的等于号会最终导致赋值当真正的目的是做比较时。尤其是当使用`return`语句时，例如：

```js
function doSomething() {
    return foo = bar + 2;
}
```

It is difficult to tell the intent of the `return` statement here. It's possible that the function is meant to return the result of `bar + 2`, but then why is it assigning to `foo`? It's also possible that the intent was to use a comparison operator such as `==` and that this code is an error.

很难表述这里的`return`语句的意图。这是可能的,函数是为了返回`bar + 2`的结果,但是为什么赋值`foo`呢?也有可能目的是使用比较运算符比如`==`,如果是这样的话代码是错误的。

Because of this ambiguity, it's considered a best practice to not use assignment in `return` statements.

由于这种模棱两可,在返回语句中不使用赋值，被认为是一个最佳实践。


## Rule Details

This rule aims to eliminate assignments from `return` statements. As such, it will warn whenever an assignment is found as part of `return`.

此规则目的在于从`return`语句中移除赋值。因此，每当在`return`中发现赋值它会给出警告。

## Options

The rule takes one option, a string, which must contain one of the following values:

此规则带有一个选项，一个字符串，它必须包含下列值之一：

* `except-parens` (default): Disallow assignments unless they are enclosed in parentheses.
* `except-parens`（默认）：禁止赋值除非被括号包裹。
* `always`: Disallow all assignments.
* `always`：禁止所有赋值

### "except-parens"

This is the default option.
It disallows assignments unless they are enclosed in parentheses.

这是默认的选项。它不允许赋值,除非他们被包围在圆括号中。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-return-assign: 2*/

function doSomething() {
    return foo = bar + 2;
}

function doSomething() {
    return foo += 2;
}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-return-assign: 2*/

function doSomething() {
    return foo == bar + 2;
}

function doSomething() {
    return foo === bar + 2;
}

function doSomething() {
    return (foo = bar + 2);
}
```

### "always"

This option disallows all assignments in `return` statements.
All assignments are treated as problems.

此选项禁止`return`中所有的赋值。所有的赋值都被认为是有问题的。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-return-assign: [2, "always"]*/

function doSomething() {
    return foo = bar + 2;
}

function doSomething() {
    return foo += 2;
}

function doSomething() {
    return (foo = bar + 2);
}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-return-assign: [2, "always"]*/

function doSomething() {
    return foo == bar + 2;
}

function doSomething() {
    return foo === bar + 2;
}
```

## When Not To Use It

If you want to allow the use of assignment operators in a `return` statement, then you can safely disable this rule.

如果你想允许`return`语句中赋值操作符的使用，你可以安全的关闭此规则。

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-return-assign.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-return-assign.md)
