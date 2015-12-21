---
title: Rule no-eval
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow eval() (no-eval)
# 禁止使用eval()（no-eval）

JavaScript's `eval()` function is potentially dangerous and is often misused. Using `eval()` on untrusted code can open a program up to several different injection attacks. The use of `eval()` in most contexts can be substituted for a better, alternative approach to a problem.

JavaScript中的`eval()`函数有可能是危险的并且经常被误用。对不信任的代码使用`eval()`会给一些不同的注入攻击开启一个程序。`eval()`的使用在大多数情况下可以被更好，可替代的方案解决问题。

```js
var obj = { x: "foo" },
    key = "x",
    value = eval("obj." + key);
```

## Rule Details

This rule is aimed at preventing potentially dangerous, unnecessary, and slow code by disallowing the use of the `eval()` function. As such, it will warn whenever the `eval()` function is used.

此规则目的在于通过禁止使用`eval()`函数，防止潜在危险的，没有必要的、和运行效率低下的代码。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-eval: 2*/

var obj = { x: "foo" },
    key = "x",
    value = eval("obj." + key); /*error eval can be harmful.*/
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-eval: 2*/

var obj = { x: "foo" },
    key = "x",
    value = obj[key];
```

## Further Reading

* [Eval is Evil, Part One](http://blogs.msdn.com/b/ericlippert/archive/2003/11/01/53329.aspx)
* [How evil is eval](http://javascriptweblog.wordpress.com/2010/04/19/how-evil-is-eval/)

## Related Rules

* [no-implied-eval](no-implied-eval)

## Version

This rule was introduced in ESLint 0.0.2.

此规则在ESLint 0.0.2中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-eval.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-eval.md)
