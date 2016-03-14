---
title: Rule dot-notation
layout: doc
proofreader: @ILFront-End
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Require Dot Notation (dot-notation)

# 要求使用点号 (dot-notation)

In JavaScript, one can access properties using the dot notation (`foo.bar`) or square-bracket notation (`foo["bar"]`). However, the dot notation is often preferred because it is easier to read, less verbose, and works better with aggressive JavaScript minimizers.

在JavaScript中，可以使用点 (`foo.bar`) 或者方括号 (`foo["bar"]`) 来访问属性。然而，点通常更受青睐
，因为它易读，简洁，且更适应激进的 JavaScript 压缩器。

```js
foo["bar"];
```

## Rule Details

This rule is aimed at maintaining code consistency and improving code readability by encouraging use of the dot notation style whenever possible. As such, it will warn when it encounters an unnecessary use of square-bracket notation.

此规则旨在通过鼓励使用点符号，尽可能维护代码统一，提高代码可读性。
当遇到方括号使用不当的情况时，它会给出警告。


The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint dot-notation: 2*/

var x = foo["bar"]; /*error ["bar"] is better written in dot notation.*/
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint dot-notation: 2*/

var x = foo.bar;

var x = foo[bar];    // Property name is a variable, square-bracket notation required
```

### Options

This rule accepts a single options argument with the following defaults:

此规则接受一个可选参数，默认值如下：

```json
{
    "rules": {
        "dot-notation": [2, {"allowKeywords": true, "allowPattern": ""}]
    }
}
```

#### `allowKeywords`

Set the `allowKeywords` option to `false` (default is `true`) to follow ECMAScript version 3 compatible style, avoiding dot notation for reserved word properties.

为了兼容ECMAScript 第3版，即避免保留字作为属性，可设置 `allowKeywords` 选项为 `false` （默认是 `true`）。

```json
  "dot-notation": [2, {"allowKeywords": false}],
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：


```js
/*eslint dot-notation: [2, {"allowKeywords": false}]*/

var foo = { "class": "CS 101" }
var x = foo["class"]; // Property name is a reserved word, square-bracket notation required
```

#### `allowPattern`

Set the `allowPattern` option to a regular expression string to allow bracket notation for property names that match a pattern (by default, no pattern is tested).

设置 `allowPattern` 选项为正则表达式，允许为属性名使用方括号，去和匹配模式进行匹配。（默认匹配模式为空）


For example, when preparing data to be sent to an external API, it is often required to use property names that include underscores.  If the `camelcase` rule is in effect, these [snake case](http://en.wikipedia.org/wiki/Snake_case) properties would not be allowed.  By providing an `allowPattern` to the `dot-notation` rule, these snake case properties can be accessed with bracket notation.

如这个例子，当包含下划线的属性名被传送到接口，如果 `camelcase` 规则生效，[snake case](http://en.wikipedia.org/wiki/Snake_case) 属性是不被允许的。通过设置 `allowPattern` 为 `dot-notation`，这些snake case属性可以使用括号符号来访问。

Example configuration:

配置如下：

```json
{
    "rules": {
        "camelcase": 2
        "dot-notation": [2, {"allowPattern": "^[a-z]+(_[a-z]+)+$"}]
    }
}
```

Example code patterns:

正则模式示例：

```js
/*eslint camelcase: 2*/
/*eslint dot-notation: [2, {"allowPattern": "^[a-z]+(_[a-z]+)+$"}]*/

var data = {};
data.foo_bar = 42;    /*error Identifier 'foo_bar' is not in camel case.*/

var data = {};
data["fooBar"] = 42;  /*error ["fooBar"] is better written in dot notation.*/

var data = {};
data["foo_bar"] = 42; // no warning
```

## Version

This rule was introduced in ESLint 0.0.7.

此规则在 ESLint 0.0.7中被引入

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/dot-notation.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/dot-notation.md)
