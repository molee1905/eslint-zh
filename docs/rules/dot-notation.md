---
title: Rule dot-notation
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Require Dot Notation (dot-notation)

#需要点符号

In JavaScript, one can access properties using the dot notation (`foo.bar`) or square-bracket notation (`foo["bar"]`). However, the dot notation is often preferred because it is easier to read, less verbose, and works better with aggressive JavaScript minimizers.

在JavaScript中，可以使用点符号(`foo.bar`)或者方括号(`foo["bar"]`)来访问属性。然而，点括号通常是首选
，因为他更加易读，简洁，也更好的适用于aggressive JavaScript minimizers。

```js
foo["bar"];
```

## Rule Details

This rule is aimed at maintaining code consistency and improving code readability by encouraging use of the dot notation style whenever possible. As such, it will warn when it encounters an unnecessary use of square-bracket notation.

此规则目的在于，通过鼓励尽可能的使用点括号风格，来保持代码的统一性和提高代码的可读性。因此，当遇到没必要使用方括号的情况发生时，他会给出警告。

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

此规则接受一个单一的选项参数，默认值如下：

```json
{
    "rules": {
        "dot-notation": [2, {"allowKeywords": true, "allowPattern": ""}]
    }
}
```

#### `allowKeywords`

Set the `allowKeywords` option to `false` (default is `true`) to follow ECMAScript version 3 compatible style, avoiding dot notation for reserved word properties.

为了遵循ECMAScript第3版的兼容风格，把`allowKeywords`选项设置为`false`（默认为`true`），避免保留字使用点符号。


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

设置`allowPattern`选项为正则表达式，来允许那些匹配模式的属性使用括号符号。（默认匹配模式为空）

For example, when preparing data to be sent to an external API, it is often required to use property names that include underscores.  If the `camelcase` rule is in effect, these [snake case](http://en.wikipedia.org/wiki/Snake_case) properties would not be allowed.  By providing an `allowPattern` to the `dot-notation` rule, these snake case properties can be accessed with bracket notation.

例如，当筹备数据发送到外部接口时，经常需要使用含有下划线的参数名，如果`camelcase` 规则开启，这些snake case属性是被允许的。
通过给`dot-notation` 规则提供`allowPattern`，这些snake case属性可以使用括号符号来访问。

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

此规则在ESLint 0.0.7中被引入

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/dot-notation.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/dot-notation.md)
