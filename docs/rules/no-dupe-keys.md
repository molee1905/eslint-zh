---
title: Rule no-dupe-keys
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Duplicate Keys (no-dupe-keys)
# 禁止重复键

Creating objects with duplicate keys in objects can cause unexpected behavior in your application. The `no-dupe-keys` rule flags the use of duplicate keys in object literals.

创建有重复键的对象在应用程序中可能导致不可预测的行为。`no-dupe-keys`规则在对象字面量中有重复键时使用。

```js
var foo = {
    bar: "baz",
    bar: "qux"
};
```

## Rule Details

This rule is aimed at preventing possible errors and unexpected behavior that might arise from using duplicate keys in object literals. As such, it warns whenever it finds a duplicate key.

该规则旨在防止有使用重复键的对象字面量引起可能错误和异常行为。 因此，只要有重复键就会报出警告。

The following patterns are considered problems:

下面是有问题的代码：

```js
/*eslint no-dupe-keys: 2*/

var foo = {
    bar: "baz",
    bar: "qux"     /*error Duplicate key 'bar'.*/
};

var foo = {
    "bar": "baz",
    bar: "qux"     /*error Duplicate key 'bar'.*/
};

var foo = {
    0x1: "baz",
    1: "qux"       /*error Duplicate key '1'.*/
};
```

The following patterns are not considered problems:

下面是正确的代码：

```js
/*eslint no-dupe-keys: 2*/

var foo = {
    bar: "baz",
    quxx: "qux"
};
```

## Version

This rule was introduced in ESLint 0.0.9.

该规则是在ESLint 0.0.9 中被引入的。


## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-dupe-keys.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-dupe-keys.md)
