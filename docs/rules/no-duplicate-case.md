---
title: Rule no-duplicate-case
layout: doc
translator: ybbjegj
proofreader: molee1905
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Rule to disallow a duplicate case label (no-duplicate-case)

# 禁止重复 case 标签（no-duplicate-case）

A switch statements with duplicate case labels is normally an indication of a programmer error.

在 switch 语句中出现重复 case 标签通常是开发者出现错误的标志。

In the following example the 3rd case label uses again the literal 1 that has already been used in the first case label.
Most likely the case block was copied from above and it was forgotten to change the literal.

下面例子中的第三个 case 使用的字面量 1 已经在第一个 case 中使用过了。这种情况最有可能是直接复制上面的 case 块，但是忘记改变字面量造成的。

```js
var a = 1;

switch (a) {
    case 1:
        break;
    case 2:
        break;
    case 1:         // duplicate literal 1
        break;
    default:
        break;
}
```

## Rule Details

This inspection reports any duplicated case labels on JavaScript switch statements.

该检查报告 JavaScript switch 语句中出现重复 case 标签的情况。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-duplicate-case: 2*/

var a = 1,
    one = 1;

switch (a) {
    case 1:
        break;
    case 1:      /*error Duplicate case label.*/
        break;
    case 2:
        break;
    default:
        break;
}

switch (a) {
    case "1":
        break;
    case "1":    /*error Duplicate case label.*/
        break;
    case "2":
        break;
    default:
        break;
}

switch (a) {
    case one:
        break;
    case one:    /*error Duplicate case label.*/
        break;
    case 2:
        break;
    default:
        break;
}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-duplicate-case: 2*/

var a = 1;

switch (a) {
    case 1:
        break;
    case 2:
        break;
    default:
        break;
}
```

## Version

This rule was introduced in ESLint 0.17.0.

该规则在 ESLint 0.17.0 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-duplicate-case.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-duplicate-case.md)
