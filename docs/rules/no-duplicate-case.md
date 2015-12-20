---
title: Rule no-duplicate-case
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Rule to disallow a duplicate case label (no-duplicate-case)

# 禁止重复case标签（no-duplicate-case）

A switch statements with duplicate case labels is normally an indication of a programmer error.

开发者很容易犯的错误就是在switch语句中出现重复case。

In the following example the 3rd case label uses again the literal 1 that has already been used in the first case label.
Most likely the case block was copied from above and it was forgotten to change the literal.

下面例子中的第三个case使用的字面量1已经在第一个case中被使用。最可能出现该情况的是复制上面的case块，但是忘记改变文字。

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

检测JavaScript switch语句中重复的case标签。

The following patterns are considered problems:

下面是有问题的代码：

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

下面是正确的代码：

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

该规则是在ESLint 0.17.0 中被引入的。


## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-duplicate-case.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-duplicate-case.md)
