---
title: Rule no-empty-label
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# No empty labels (no-empty-label)
# 禁用空标签（no-empty-label）

**Replacement notice**: This rule was removed in ESLint v2.0 and replaced by [no-labels](no-labels) rule.

Labeled statements are only used in conjunction with labeled break and continue statements. ECMAScript has no goto statement.

ECMAScript没有goto语句.标签语句只能被用来标记break和continue语句。

## Rule Details

This error occurs when a label is used to mark a statement that is not an iteration or switch

当标签被用来标记非循环或者非switch分支语句时，会发生错误。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-empty-label: 2*/

labeled:
var x = 10;
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-empty-label: 2*/

labeled:
for (var i=10; i; i--) {
    // ...
}
```

## When Not To Use It

If you don't want to be notified about usage of labels, then it's safe to disable this rule.

## Related Rules

* [no-labels](./no-labels)
* [no-label-var](./no-label-var)
* [no-unused-labels](./no-unused-labels)

## Version

This rule was introduced in ESLint 0.0.9 and removed in 2.0.0-rc.0.

该规则在ESLint 0.0.9 中被引入，在 2.0.0-rc.0 中移除。

## Resources

* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-empty-label.md)
