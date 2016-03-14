---
title: Rule no-extra-bind
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow unnecessary function binding (no-extra-bind)

# 禁止不必要的函数绑定 (no-extra-bind)

The `bind()` method is used to create functions with specific `this` values and, optionally, binds arguments to specific values. When used to specify the value of `this`, it's important that the function actually use `this` in its function body. For example:

`bind()`方法被用来通过指定`this`值创建函数，并可选的绑定参数给指定的值。当被用来指定`this`值时，函数实际上在函数体中使用的`this`值很重要。例如：

```js
var boundGetName = (function getName() {
    return this.name;
}).bind({ name: "ESLint" });

console.log(boundGetName());      // "ESLint"
```

This code is an example of a good use of `bind()` for setting the value of `this`.

以上代码是一个很好的使用`bind()`来设置`this`值的例子。

Sometimes during the course of code maintenance, the `this` value is removed from the function body. In that case, you can end up with a call to `bind()` that doesn't accomplish anything:

有时在代码维护过程中，`this`值从函数体中被移除。在这种情况下，你可以结束没有做任何处理的`bind()`调用。

```js
// useless bind
var boundGetName = (function getName() {
    return "ESLint";
}).bind({ name: "ESLint" });

console.log(boundGetName());      // "ESLint"
```

In this code, the reference to `this` has been removed but `bind()` is still used. In this case, the `bind()` is unnecessary overhead (and a performance hit) and can be safely removed.

在代码中，`this`的引用已经被删除但是`bind()`依然在使用。在这种情况下，`bind()`是不必要的开销（和性能损耗）可以安全的移除。

## Rule Details

This rule is aimed at avoiding the unnecessary use of `bind()` and as such will warn whenever an immediately-invoked function expression (IIFE) is using `bind()` and doesn't have an appropriate `this` value. This rule won't flag usage of `bind()` that includes function argument binding.

此规则目的在于避免不必要的`bind()`使用并且每当立即执行的函数表达式(IIFE)中使用`bind()`，但是没有一个合适的`this`值时会给出警告。此规则不会标记`bind()`用法中有函数参数的绑定。

**Note:** Arrow functions can never have their `this` value set using `bind()`. This rule flags all uses of `bind()` with arrow functions as a problem

**注意:**箭头函数不会有他们的`this`值设置功能通过使用`bind()`。此规则把所有使用`bind()`的箭头函数标记为有问题的。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-extra-bind: 2*/
/*eslint-env es6*/

var x = function () {
    foo();
}.bind(bar);

var x = (() => {
    foo();
}).bind(bar);

var x = (() => {
    this.foo();
}).bind(bar);

var x = function () {
    (function () {
      this.foo();
    }());
}.bind(bar);

var x = function () {
    function foo() {
      this.bar();
    }
}.bind(baz);
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-extra-bind: 2*/

var x = function () {
    this.foo();
}.bind(bar);

var x = function (a) {
    return a + 1;
}.bind(foo, bar);
```

## When Not To Use It

If you are not concerned about unnecessary calls to `bind()`, you can safely disable this rule.

如果你不担心不必要的`bind()`调用，你可以安全的关闭此规则。

## Further Reading

* [Function.prototype.bind](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)
* [Understanding JavaScript's Function.prototype.bind](http://www.smashingmagazine.com/2014/01/understanding-javascript-function-prototype-bind/)

## Version

This rule was introduced in ESLint 0.8.0.

此规则在ESLint 0.8.0中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-extra-bind.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-extra-bind.md)
