---
title: Rule no-native-reassign
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Reassignment of Native Objects (no-native-reassign)

# 禁止对原生对象赋值 (no-native-reassign)

Reports an error when they encounter an attempt to assign a value to built-in native object.

当他们遇到试图分配一个内置对象时，会报告错误。

```js
String = "hello world";
```

## Rule Details

The native objects reported by this rule are the `builtin` variables from [globals](https://github.com/sindresorhus/globals/).

此规则报告的内置对象是从全局`内建`的变量。 

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-native-reassign: 2*/

String = new Object(); /*error String is a read-only native object.*/
```

## Options

This rule accepts an `exceptions` option, which can be used to specify a list of builtins for which reassignments will be allowed:

此规则接受一个`exceptions`选项，可以用来指定一个可以被分配的内建列表。

```json
{
    "rules": {
        "no-native-reassign": [2, {"exceptions": ["Object"]}]
    }
}
```

## When Not To Use It

If you are trying to override one of the native objects.

如果你想尝试覆盖其中一个内置对象。

## Related Rules

* [no-extend-native](no-extend-native)
* [no-redeclare](no-redeclare)
* [no-shadow](no-shadow)

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-native-reassign.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-native-reassign.md)
