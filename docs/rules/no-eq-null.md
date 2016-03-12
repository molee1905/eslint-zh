---
title: Rule no-eq-null
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow Null Comparisons (no-eq-null)

# 禁止Null比较 (no-eq-null)

Comparing to `null` without a type-checking operator (`==` or `!=`), can have unintended results as the comparison will evaluate to true when comparing to not just a `null`, but also an `undefined` value.

做非类型检测的`null`比较时，可能有意外的结果，因为当匹配到`null`或者`undefined`时，对比操作会认为是true。

```js
if (foo == null) {
  bar();
}
```

## Rule Details

The `no-eq-null` rule aims reduce potential bug and unwanted behavior by ensuring that comparisons to `null` only match `null`, and not also `undefined`. As such it will flag comparisons to null when using `==` and `!=`.

`no-eq-null`规则目的在于，通过确保比较`null`仅匹配`null`而不是也匹配`undefined`，来减少潜在的bug或者不希望发生的情况。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-eq-null: 2*/

if (foo == null) {
  bar();
}

while (qux != null) {
  baz();
}
```

The following patterns are considered okay:

以下模式被认为是没有问题的：

```js
/*eslint no-eq-null: 2*/

if (foo === null) {
  bar();
}

while (qux !== null) {
  baz();
}
```

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-eq-null.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-eq-null.md)
