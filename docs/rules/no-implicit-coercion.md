---
title: Rule no-implicit-coercion
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow the type conversion with shorter notations. (no-implicit-coercion)

# 禁止使用较短的符号实现类型转换 (no-implicit-coercion)

In JavaScript, there are a lot of different ways to convert value types.
Some of them might be hard to read and understand.

在JavaScript中，有许多不同的方式转换值的类型。其中有些可能很难阅读和理解。

Such as:

例如：

```js
var b = !!foo;
var b = ~foo.indexOf(".");
var n = +foo;
var n = 1 * foo;
var s = "" + foo;
foo += "";
```

Those can be replaced with the following code:

这些能被下面的代码所替换：

```js
var b = Boolean(foo);
var b = foo.indexOf(".") !== -1;
var n = Number(foo);
var n = Number(foo);
var s = String(foo);
foo = String(foo);
```

## Rule Details

This rule is aimed to flag shorter notations for the type conversion, then suggest a more self-explanatory notation.

此规则目的在于标记出较短的类型转换符号，然后推荐一个更加不言自明的表达方式。

## Options

This rule has three main options and one override option to allow some coercions as required.

此规则有三个选项。

```js
{
    "rules": {
        "no-implicit-coercion": [2, {
            "boolean": true,
            "number": true,
            "string": true,
            "allow": [/* "!!", "~", "*", "+" */]
        }]
    }
}
```

* `"boolean"` (`true` by default) - When this is `true`, this rule warns shorter type conversions for `boolean` type.

* `"boolean"`(默认是`true`)－当为`true`时，规则会对简短的`boolean`值类型转换给出警告。

* `"number"` (`true` by default) - When this is `true`, this rule warns shorter type conversions for `number` type.

* `"number"`(默认是`true`)－当为`true`时，规则会对简短的`number`值类型转换给出警告。

* `"string"` (`true` by default) - When this is `true`, this rule warns shorter type conversions for `string` type.

* `"string"`(默认是`true`)－当为`true`时，规则会对简短的`string`值类型转换给出警告。

* `"allow"` (`empty` by default) - Each entry in this array can be one of `~`, `!!`, `+` or `*` that are to be allowed.

* `"allow"` (默认是`empty`) - 这个数组的每一项可以是 `~`，`!!`， `+` 或`*`。

Note that operator `+` in `allow` list would allow `+foo` (number coercion) as well as `"" + foo` (string coercion).

### `boolean`

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-implicit-coercion: 2*/

var b = !!foo;
var b = ~foo.indexOf(".");
// only with `indexOf`/`lastIndexOf` method calling.

```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-implicit-coercion: 2*/

var b = Boolean(foo);
var b = foo.indexOf(".") !== -1;

var n = ~foo; // This is a just binary negating.
```

### `number`

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-implicit-coercion: 2*/

var n = +foo;
var n = 1 * foo;
```

The following patterns are not considered problems:

以下模式被认为是没有问题的

```js
/*eslint no-implicit-coercion: 2*/

var b = Number(foo);
var b = parseFloat(foo);
var b = parseInt(foo, 10);
```

### `string`

The following patterns are considered problems:

以下模式被认为是有问题的：


```js
/*eslint no-implicit-coercion: 2*/

var n = "" + foo;

foo += "";
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-implicit-coercion: 2*/

var b = String(foo);
```

### Fine-grained control

Using `allow` list, we can override and allow specific operators.

当时使用`allow`列表，我们可以覆盖和允许指定的操作符。

For example, when the configuration is like this:

例如，当这样配置时：

```json
{
    "rules": {
        "no-implicit-coercion": [2, {
            "boolean": true,
            "number": true,
            "string": true,
            "allow": ["!!", "~"]
        }]
    }
}
```

The following patterns are not considered problems:

以下模式被认为是有问题的：

```js
var b = !!foo;
var c = ~foo.indexOf(".");
```

## When Not To Use It

If you don't want to be notified about shorter notations for the type conversion, you can safely disable this rule.

如果你不想限制类型转换的简短表述，可以安全的禁用此规则。

## Version

This rule was introduced in ESLint 1.0.0-rc-2.

此规则在ESLint 1.0.0-rc-2中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-implicit-coercion.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-implicit-coercion.md)
