---
title: Rule no-self-compare
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Self Compare (no-self-compare)

# 禁止自身比较（no-self-compare）

Comparing a variable against itself is usually an error, either an typo or refactoring error. It is confusing to the reader and may potentially introduce a runtime error.

比较变量自身是一个错误，一个打字错误或者重构错误。给读者造成困扰并且可能会引入运行错误。

The only time you would compare a variable against itself is when you are testing for `NaN`. However, it is far more appropriate to use `typeof x === 'number' && isNaN(x)` or the [Number.isNaN ES2015 function](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isNaN) for that use case rather than leaving the reader of the code to determine the intent of self comparison.

只有一种时候你可以对变量自身做比较，那就是当你在测试变量是否是`NaN`时。然而，对这种情况使用`typeof x === 'number' && isNaN(x)`或者[Number.isNaN ES2015 函数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/isNaN) 远比让代码的读者去决定自身比较的目的更合适。

## Rule Details

This error is raised to highlight a potentially confusing and potentially pointless piece of code. There are almost no situations in which you would need to compare something to itself.

这个错误突出高亮了一个潜在的混淆和潜在的无意义的代码。几乎没有这种情况，你需要去和变量自身做些比较。


```js
/*eslint no-self-compare: 2*/

var x = 10;
if (x === x) { /*error Comparing to itself is potentially pointless.*/
    x = 20;
}
```

## Further Reading

* [Weird Relation](http://jslinterrors.com/weird-relation/)

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-self-compare.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-self-compare.md)
