---
title: Rule no-arrow-condition
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow arrow functions where a condition is expected (no-arrow-condition)

# 禁止在本应使用条件语句的地方使用箭头函数 (no-arrow-condition)

Arrow functions (`=>`) are similar in syntax to some comparison operators (`>`, `<`, `<=`, and `>=`). This rule warns against using the arrow function syntax in places where a condition is expected. Even if the arguments of the arrow function are wrapped with parens, this rule still warns about it.

箭头函数 (`=>`) 在语法上类似于一些比较运算符 (`>`, `<`, `<=`, and `>=`)。当本应使用条件语句的地方使用了箭头函数，该规则将发出警告。及时箭头函数的参数被括号括起来，该规则仍然发出警告。

Here's an example where the usage of `=>` is most likely a typo:

下面的这个示例，`=>`的使用很有可能是个书写错误：

```js
// This is probably a typo
if (a => 1) {}
// And should instead be
if (a >= 1) {}
```

There are also cases where the usage of `=>` can be ambiguous and should be rewritten to more clearly show the author's intent:

还有一些情况下，`=>`的使用可能会模棱两可，应该重新，以更清楚的表明作者意图：

```js
// The intent is not clear
var x = a => 1 ? 2 : 3
// Did the author mean this
var x = function (a) { return a >= 1 ? 2 : 3 }
// Or this
var x = a <= 1 ? 2 : 3
```

## Rule Details

The following patterns are considered warnings:

以下模式被认为是警告：

```js
/*eslint no-arrow-condition: 2*/
/*eslint-env es6*/

if (a => 1) {}
while (a => 1) {}
for (var a = 1; a => 10; a++) {}
a => 1 ? 2 : 3
(a => 1) ? 2 : 3
var x = a => 1 ? 2 : 3
var x = (a) => 1 ? 2 : 3
```

## Related Rules

* [arrow-parens](arrow-parens)

## Version

This rule was introduced in ESLint 1.8.0.

该规则在ESLint 1.8.0 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-arrow-condition.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-arrow-condition.md)
