---
title: Rule no-floating-decimal
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Floating Decimals (no-floating-decimal)

# 禁止浮点小数 (no-floating-decimal)

Float values in JavaScript contain a decimal point, and there is no requirement that the decimal point be preceded or followed by a number. For example, the following are all valid JavaScript numbers:

浮点型值在JavaScript中会包含一个小数点，小数点的前后没有必要存在一个数字。例如，以下例子都是有效的JavaScript数字：

```js
var num = .5;
var num = 2.;
var num = -.7;
```

Although not a syntax error, this format for numbers can make it difficult to distinguish between true decimal numbers and the dot operator. For this reason, some recommend that you should always include a number before and after a decimal point to make it clear the intent is to create a decimal number.

尽管不是语法错误，这种格式的数字使真正的小数和点操作符变的难以区分。由于这个原因，有些人提议应该总是在小数点前面或者后面有一个数字使得创建一个小数这种行为变的明晰。

## Rule Details

This rule is aimed at eliminating floating decimal points and will warn whenever a numeric value has a decimal point but is missing a number either before or after it.

此规则目的在于消除浮动小数点，而且当数字类型值的小数点前面或者后面丢失数字时给出警告。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-floating-decimal: 2*/

var num = .5;  /*error A leading decimal point can be confused with a dot.*/
var num = 2.;  /*error A trailing decimal point can be confused with a dot.*/
var num = -.7; /*error A leading decimal point can be confused with a dot.*/
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-floating-decimal: 2*/

var num = 0.5;
var num = 2.0;
```

## Compatibility

* **JSHint**: W008

## When Not To Use It

If you aren't concerned about misinterpreting floating decimal point values, then you can safely turn this rule off.

如果你不认为浮动的小数点会被误读，你可以安全的关闭此规则。

## Further Reading

* [A leading decimal point can be confused with a dot](http://jslinterrors.com/a-leading-decimal-point-can-be-confused-with-a-dot-a/)

## Version

This rule was introduced in ESLint 0.0.6.

此规则在ESLint 0.0.6中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-floating-decimal.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-floating-decimal.md)
