---
title: Rule guard-for-in
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Require Guarding for-in (guard-for-in)
# 需要把关for-in (guard-for-in)

Looping over objects with a `for in` loop will include properties that are inherited through the prototype chain. This behavior can lead to unexpected items in your "for" loop.

在使用`for in`语句遍历对象时，通过原型链继承而来的属性也会被访问到。这种遍历行为会导致意外的情况发生。

```js
for (key in foo) {
    doSomething(key);
}
```

## Rule Details

This rule is aimed at preventing unexpected behavior that could arise from using a `for in` loop without filtering the results in the loop. As such, it will warn when `for in` loops do not filter their results with an `if` statement.

此规则目的在于，阻止在`for in`遍历过程中， 由于不对结果进行筛选而导致意想不到的行为发生。因此，当`for in`循环中，没有使用`if` 语句对结果进行筛选时，会给出警告。

The following patterns are considered problems:

错误示例如下：

```js
/*eslint guard-for-in: 2*/

for (key in foo) {
    doSomething(key);
}
```

The following patterns are not considered problems:

正确示例如下：

```js
/*eslint guard-for-in: 2*/

for (key in foo) {
    if ({}.hasOwnProperty.call(foo, key)) {
        doSomething(key);
    }
}
```

## Further Reading

* [Exploring JavaScript for-in loops](http://javascriptweblog.wordpress.com/2011/01/04/exploring-javascript-for-in-loops/)
* [The pitfalls of using objects as maps in JavaScript](http://www.2ality.com/2012/01/objects-as-maps.html)

## Version

This rule was introduced in ESLint 0.0.6.

此规则在ESLint 0.0.6中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/guard-for-in.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/guard-for-in.md)
