---
title: Rule no-magic-numbers
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Magic Numbers (no-magic-numbers)

# 禁止幻数 (no-magic-numbers)

'Magic numbers' are numbers that occur multiple time in code without an explicit meaning.
They should preferably be replaced by named constants.

'Magic numbers'是在代码中出现多次的没有明确含义的数字。他们应该被定义为常量。


```js
var now = Date.now(),
    inOneHour = now + (60 * 60 * 1000);
```

## Rule Details

The `no-magic-numbers` rule aims to make code more readable and refactoring easier by ensuring that special numbers
are declared as constants to make their meaning explicit.

`no-magic-numbers`规则目的在于通过确保特殊的数字被声明为常量使得他们意义明确，使代码更加可读和易于重构

The following pattern is considered a problem:

以下模式被认为是有问题的：

```js
/*eslint no-magic-numbers: 2*/

var dutyFreePrice = 100,
    finalPrice = dutyFreePrice + (dutyFreePrice * 0.25); /*error No magic number: 0.25*/
```

The following pattern is considered okay:

以下模式被认为是没有问题的：

```js
/*eslint no-magic-numbers: 2*/

var TAX_PERCENTAGE = 0.25;

var dutyFreePrice = 100,
    finalPrice = dutyFreePrice + (dutyFreePrice * TAX_PERCENTAGE);
```

## Options

### ignore

An array of numbers to ignore. It's set to `[0, 1, 2]` by default.
If provided, it must be an `Array`.

默认设置为`[0, 1, 2]`，数组数字会被忽略。如果被提供，他必须是一个`Array`。

### enforceConst

A boolean to specify if we should check for the const keyword in variable declaration of numbers. `false` by default.

指定一个布尔值，如果我们应该在数字变量声明中检测const关键字。默认为`false`。

### detectObjects

A boolean to specify if we should detect numbers when setting object properties for example. `false` by default.

指定一个布尔值，例如如果我们应该在对象属性中检测数字。默认为`false`。

## Version

This rule was introduced in ESLint 1.7.0.

此规则在ESLint 1.7.0中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-magic-numbers.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-magic-numbers.md)
