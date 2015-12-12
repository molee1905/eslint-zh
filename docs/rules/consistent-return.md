---
title: Rule consistent-return
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Require Consistent Returns (consistent-return)

#需要一致的返回

One of the confusing aspects of JavaScript is that any function may or may not return a value at any point in time. When a function exits without any `return` statement executing, the function returns `undefined`. Similarly, calling `return` without specifying any value will cause the function to return `undefined`.Only when `return` is called with a value is there a change in the function's return value. 

JavaScript混乱之一是，任何函数中可能会也可能不会在任何时刻返回一个值。
当函数中没有任何`return`语句执行时，函数返回`undefined`。
同样的，调用没有指定任何返回值的`return`，函数也会返回`undefined`。
只有当调用带有返回值的`return`，才会改变函数的返回值。

Unlike statically-typed languages that will catch when a function doesn't return the type of data expected, JavaScript has no such checks, meaning that it's easy to make mistakes such as this:

静态类型语言,将会捕获到函数没有返回期望类型，与其不同，JavaScript没有类似的检测，意味着它很容易引起如下的错误：

```js
function doSomething(condition) {

    if (condition) {
        return true;
    } else {
        return;
    }
}
```

Here, one branch of the function returns `true`, a Boolean value, while the other exits without specifying any value (and so returns `undefined`). 

如上，函数的一个分支返回了`true`，一个布尔值，然而另一个分支则没有指定任何值（所以返回`undefined`）。

This may be an indicator of a coding error, especially if this pattern is found in larger functions.

它可能是一个编码错误的指示，特别是如果这种模式在较大的函数中被发现时。

## Rule Details

This rule is aimed at ensuring all `return` statements either specify a value or don't specify a value.

此规则目的在于，确保所有的`return`语句指定或者不指定一个值。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint consistent-return: 2*/

function doSomething(condition) {

    if (condition) {
        return true;
    } else {
        return;      /*error Expected a return value.*/
    }
}

function doSomething(condition) {

    if (condition) {
        return;
    } else {
        return true; /*error Expected no return value.*/
    }
}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint consistent-return: 2*/

function doSomething(condition) {

    if (condition) {
        return true;
    } else {
        return false;
    }
}
```

## When Not To Use It

If you want to allow functions to have different `return` behavior depending on code branching, then it is safe to disable this rule.

如果你想要允许函数根据代码分支有不同的`return`行为，可以安全的禁用此规则。

## Version

This rule was introduced in ESLint 0.4.0.

此规则在ESLint 0.4.0中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/consistent-return.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/consistent-return.md)
