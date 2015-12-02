---
title: Rule no-console
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Use of console (no-console)

In JavaScript that is designed to be executed in the browser, it's considered a best practice to avoid using methods on `console`. Such messages are considered to be for debugging purposes and therefore not suitable to ship to the client. In general, calls using `console` should be stripped before being pushed to production.

在JavaScript中，console用于在浏览器中运行，是一种避免在控制台使用方法的最佳实践。console输出的消息被认为是用于调试目的，因此不适合输出到客户端。通常在发布到产品时应该删除掉。

```js
console.log("Made it here.");
console.error("That shouldn't have happened.");
```


## Rule Details

This rule is aimed at eliminating unwanted `console` references from your JavaScript. As such, it warns whenever it sees `console` used as an identifier in code.

该规则目的在于消除javascript代码中不需要的 `console` 引用，因此，只要发现 `console` 作为标示在代码中使用就会发出警告。

The following patterns are considered problems:

下面的模式被认为是有问题的：

```js
/*eslint no-console: 2*/

console.log("Hello world!");              /*error Unexpected console statement.*/
console.error("Something bad happened."); /*error Unexpected console statement.*/
```

The following patterns are not considered problems:

下面的模式被认为是没有问题的：

```js
/*eslint no-console: 2*/

// custom console
Console.log("Hello world!");
```

## When Not To Use It

If you're using Node.js, however, `console` is used to output information to the user and so is not strictly used for debugging purposes. If you are developing for Node.js then you most likely do not want this rule enabled.

如果你使用Node.js, `console` 主要用于向用户输出信息，而不是严格用于调试目的的。在开发Node.js时，最好不要启用该规则。


## Related Rules

* [no-alert](no-alert)
* [no-debugger](no-debugger)

## Version

This rule was introduced in ESLint 0.0.2.

这个规则是在ESLint 0.0.2中引进发布的。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-console.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-console.md)
