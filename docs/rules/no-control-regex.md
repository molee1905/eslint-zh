---
title: Rule no-control-regex
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Controls Characters in Regular Expressions (no-control-regex)

# 禁止在正则表达式中使用控制字符（no-control-regex）

Control characters are special, invisible characters in the ASCII range 0-31. These characters are rarely used in JavaScript strings so a regular expression containing these characters is most likely a mistake.

在ASCII的0-31范围内的控制字符是种特殊，无形的字符。这些字符很少在JavaScript字符串中使用，所以在正则表达式中包含这些字符很可能是个错误。

## Rule Details

This rule is aimed at ensuring all regular expressions don't use control characters.

该规则目的在于保证所有的正则表达式中不使用控制字符。

The following patterns are considered problems:

下面的模式被认为是有问题的：

```js
/*eslint no-control-regex: 2*/

var pattern1 = /\\x1f/;
var pattern2 = new RegExp("\x1f"); /*error Unexpected control character in regular expression.*/
```

The following patterns do not cause a warning:

下面的模式不会引发警告：

```js
/*eslint no-control-regex: 2*/

var pattern1 = /\\x20/;
var pattern2 = new RegExp("\x20");
```

## When Not To Use It

If you need to use control character pattern matching, then you should turn this rule off.

如果你需要使用控制字符进行模式匹配，你应该关闭该规则。

## Related Rules

* [no-div-regex](no-div-regex)
* [no-regex-spaces](no-regex-spaces)


## Version

This rule was introduced in ESLint 0.1.0.

这个规则是在ESLint 0.1.0中引进发布的。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-control-regex.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-control-regex.md)
