---
title: Rule eqeqeq
layout: doc
translator: @fengnana
proofreader:  @ILFront-End
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Require === and !== (eqeqeq)
# 要求使用 === 和 !== (eqeqeq)

It is considered good practice to use the type-safe equality operators `===` and `!==` instead of their regular counterparts `==` and `!=`.

使用类型相等的比较操作符 `===` 和 `!==` 代替 `==` 和 `!=` 被认为是最佳实践。

The reason for this is that `==` and `!=` do type coercion which follows the rather obscure [Abstract Equality Comparison Algorithm](http://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3).
For instance, the following statements are all considered `true`:

这样做的原因是 `==` 和 `!=` 遵循相当模糊的 [Abstract Equality Comparison Algorithm](http://www.ecma-international.org/ecma-262/5.1/#sec-11.9.3) 来强制类型转换。如以下语句都被认为是 `true`。

* `[] == false`
* `[] == ![]`
* `3 == "03"`

If one of those occurs in an innocent-looking statement such as `a == b` the actual problem is very difficult to spot.

如果这些运算发生在 `a == b` 这样的看起来无害的声明中，实际存在的问题是非常难于定位的。

## Rule Details

This rule is aimed at eliminating the type-unsafe equality operators.

该规则旨在消除不安全的类型相等的运算。

**Fixable:** This rule is automatically fixable using the `--fix` flag on the command line.

**可修复:** 该规则可以通过 `--fix` 命令行自行修正错误。

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

该选项强制使用 `===` 和 `!==`， 除了以下情况：

* Comparing two literal values
* 比较两个文本值
* Evaluating the value of `typeof`
* 评估 `typeof` 运算的值
* Comparing against `null`
* 针对 `null` 的比较

You can specify this option using the following configuration:

你可以通过如下配置指定使用该选项：

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

以下模式在 "smart" 选项开启下被认为是有问题的：

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

该选项强制代码里使用 `===` 和 `!==`，有一例外，该规则允许在单一表达式中和 `null` ，和检测值为 `null` 或者 `undefined` 的值做比较。

You can specify this option using the following configuration:

你可以通过如下配置指定使用该选项。

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

如果设置了 "allow-null"，以下模式被认为是有问题的：

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

如果在使用比较操作时，你不强制使用这个风格，关闭该规则是安全的。

## Version

This rule was introduced in ESLint 0.0.2.

此规则在 ESLint 0.0.2 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/eqeqeq.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/eqeqeq.md)
