---
title: Rule eqeqeq
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Require === and !== (eqeqeq)
# 要求使用 === 和 !== (eqeqeq)

It is considered good practice to use the type-safe equality operators `===` and `!==` instead of their regular counterparts `==` and `!=`.

被认为是最好的实践 使用类型安全的相等运算符`===` 和 `!==` 代替他们的常规同行`==` 和 `!=`。

The reason for this is that `==` and `!=` do type coercion which follows the rather obscure [Abstract Equality Comparison Algorithm](http://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3).
For instance, the following statements are all considered `true`:

这样做的原因是，`==` 和 `!=` 遵循默默无闻的抽象平等比较算法做类型强制。例如，以下语句被认为是`true`。

* `[] == false`
* `[] == ![]`
* `3 == "03"`

If one of those occurs in an innocent-looking statement such as `a == b` the actual problem is very difficult to spot.

这些发生在一个类似`a == b`这样看起来无害的声明中时，实际问题是很难被识别的。

## Rule Details

This rule is aimed at eliminating the type-unsafe equality operators.

此规则目的在于，消除类型不安全的相等运算。

**Fixable:** This rule is automatically fixable using the `--fix` flag on the command line.

**可修复:**此规则通过在命令行中使用`--fix`自动修复。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/* eslint eqeqeq: 2 */

if (x == 42) { }                     /*error Expected '===' and instead saw '=='.*/

if ("" == text) { }                  /*error Expected '===' and instead saw '=='.*/

if (obj.getStuff() != undefined) { } /*error Expected '!==' and instead saw '!='.*/
```

### Options

* `"smart"`

This option enforces the use of `===` and `!==` except for these cases:

此选项，强制使用`===` 和 `!==`除了以下情况：

* Comparing two literal values
* Evaluating the value of `typeof`
* Comparing against `null`

You can specify this option using the following configuration:

你可以通过如下配置指定选项：

```json
"eqeqeq": [2, "smart"]
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/* eslint eqeqeq: [2, "smart"] */

typeof foo == 'undefined'
'hello' != 'world'
0 == 0
true == true
foo == null
```

The following patterns are considered problems with "smart":

以下模式在"smart"下被认为是有问题的：

```js
/* eslint eqeqeq: [2, "smart"] */

// comparing two variables requires ===
a == b              /*error Expected '===' and instead saw '=='.*/

// only one side is a literal
foo == true         /*error Expected '===' and instead saw '=='.*/
bananas != 1        /*error Expected '!==' and instead saw '!='.*/

// comparing to undefined requires ===
value == undefined  /*error Expected '===' and instead saw '=='.*/
```

* `"allow-null"`

This option will enforce `===` and `!==` in your code with one exception - it permits comparing to `null` to check for `null` or `undefined` in a single expression.

此选项在你的代码中会强制要求`===` 和 `!==`，有一例外，它允许`null`和`null`或者`undefined`在表达式中做比较。

You can specify this option using the following configuration:

你可以通过如下配置指定选项。

```json
"eqeqeq": [2, "allow-null"]
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/* eslint eqeqeq: [2, "allow-null"] */

foo == null
```

The following patterns are considered problems with "allow-null":

如果设置了"allow-null"，以下模式被认为是有问题的：

```js
/* eslint eqeqeq: [2, "allow-null"] */

bananas != 1              /*error Expected '!==' and instead saw '!='.*/
typeof foo == 'undefined' /*error Expected '===' and instead saw '=='.*/
'hello' != 'world'        /*error Expected '!==' and instead saw '!='.*/
0 == 0                    /*error Expected '===' and instead saw '=='.*/
foo == undefined          /*error Expected '===' and instead saw '=='.*/
```

## When Not To Use It

If you don't want to enforce a style for using equality operators, then it's safe to disable this rule.

如果你不想强制使用相等运算的类型，可以安全的禁用此规则。

## Version

This rule was introduced in ESLint 0.0.2.

此规则在ESLint 0.0.2中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/eqeqeq.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/eqeqeq.md)
