---
title: Rule no-div-regex
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow Regexs That Look Like Division (no-div-regex)

# 禁止使用看起来像除法的正则表达式 (no-div-regex)

Require regex literals to escape division operators.

需要将正则表达式避开除法运算符


```js
function bar() { return /=foo/; }
```

## Rule Details

This is used to disambiguate the division operator to not confuse users.

此规则用来消除除法符号的歧义使用户不产生疑惑。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-div-regex: 2*/

function bar() { return /=foo/; }
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-div-regex: 2*/

function bar() { return /\=foo/; }
```

## Related Rules

* [no-control-regex](no-control-regex)
* [no-regex-spaces](no-regex-spaces)

## Version

This rule was introduced in ESLint 0.1.0.

此规则在ESLint 0.1.0中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-div-regex.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-div-regex.md)
