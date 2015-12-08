---
title: Rule no-bitwise
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Bitwise Operators (no-bitwise)

# 禁止按位运算符 (no-bitwise)

The use of bitwise operators in JavaScript is very rare and often `&` or `|` is simply a mistyped `&&` or `||`, which will lead to unexpected behavior.

在Javascript是很少使用按位运算符，`&` 或 `|`经常会错写为`&&` 或 `||`，这将导致意外的情况出现。

```js
var x = y | z;
```

## Rule Details

This rule is aimed at catching typos that end up as bitwise operators, but are meant to be the much more common `&&`, '||', `<`, `>` operators. As such, it will warn whenever it encounters a bitwise operator:

该规则旨在捕捉原本打算使用更普通的`&&`, '||', `<`, `>`操作符，却错写为按位操作符这样的打字错误。因此，当遇到按位操作符时，该规则将发出提醒。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-bitwise: 2*/

var x = y | z;   /*error Unexpected use of '|'.*/

var x = y & z;   /*error Unexpected use of '&'.*/

var x = y ^ z;   /*error Unexpected use of '^'.*/

var x = ~ z;     /*error Unexpected use of '~'.*/

var x = y << z;  /*error Unexpected use of '<<'.*/

var x = y >> z;  /*error Unexpected use of '>>'.*/

var x = y >>> z; /*error Unexpected use of '>>>'.*/

x |= y;          /*error Unexpected use of '|='.*/

x &= y;          /*error Unexpected use of '&='.*/

x ^= y;          /*error Unexpected use of '^='.*/

x <<= y;         /*error Unexpected use of '<<='.*/

x >>= y;         /*error Unexpected use of '>>='.*/

x >>>= y;        /*error Unexpected use of '>>>='.*/
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-bitwise: 2*/

var x = y || z;

var x = y && z;

var x = y > z;

var x = y < z;

x += y;
```

## Version

This rule was introduced in ESLint 0.0.2.

该规则在ESLint 0.0.2 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-bitwise.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-bitwise.md)
