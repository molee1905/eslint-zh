---
title: Rule no-cond-assign
layout: doc
translator: ybbjegj
proofreader: molee1905
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Assignment in Conditional Statements (no-cond-assign)

# 禁止在条件语句中赋值（no-cond-assign）

In conditional statements, it is very easy to mistype a comparison operator (such as `==`) as an assignment operator (such as `=`). For example:

在条件语句中，很容易将一个比较运算符（像 `==`）错写成赋值运算符（如 `=`）。例如：

```js
// Check the user's job title
if (user.jobTitle = "manager") {
    // user.jobTitle is now incorrect
}
```

There are valid reasons to use assignment operators in conditional statements. However, it can be difficult to tell whether a specific assignment was intentional.

在条件语句中使用赋值是合法的。但是，很难辨别某个特定的赋值是否是有意为之。

## Rule Details

This rule is aimed at eliminating ambiguous assignments in `for`, `if`, `while`, and `do...while` conditional statements.

这个规则的目的在于消除 `for`，`if`， `while`，和 `do...while` 条件语句中的模棱两可的赋值。

### Options

The rule takes one option, a string, which must contain one of the following values:

该规则有一个选项，是个字符串，它必须包含下列值之一：

* `except-parens` (default): Disallow assignments unless they are enclosed in parentheses.

* `except-parens` (默认): 禁止出现赋值语句，除非赋值语句被圆括号括起来。

* `always`: Disallow all assignments. 

* `always`: 禁止所有的赋值。

#### "except-parens"

This is the default option. It disallows assignments unless they are enclosed in parentheses. This option makes it possible to use common patterns, such as reassigning a value in the condition of a `while` or `do...while` loop, without causing a warning.

这个是默认选项。它禁止出现赋值语句，除非赋值语句被圆括号括起来。这个选项可以使用普通模式，如在 `while` 或 `do...while` 循环的条件中重新分配一个值，不会引起警告。

The following patterns are considered problems:

下面的模式是被认为有问题的。

```js
/*eslint no-cond-assign: 2*/

// Unintentional assignment
var x;
if (x = 0) {         /*error Expected a conditional expression and instead saw an assignment.*/
    var b = 1;
}

// Practical example that is similar to an error
function setHeight(someNode) {
    "use strict";
    do {             /*error Expected a conditional expression and instead saw an assignment.*/
        someNode.height = "100px";
    } while (someNode = someNode.parentNode);
}
```

The following patterns are not considered problems:

下面的模式是被认为没有问题的。

```js
/*eslint no-cond-assign: 2*/

// Assignment replaced by comparison
var x;
if (x === 0) {
    var b = 1;
}

// Practical example that wraps the assignment in parentheses
function setHeight(someNode) {
    "use strict";
    do {
        someNode.height = "100px";
    } while ((someNode = someNode.parentNode));
}

// Practical example that wraps the assignment and tests for 'null'
function setHeight(someNode) {
    "use strict";
    do {
        someNode.height = "100px";
    } while ((someNode = someNode.parentNode) !== null);
}
```

#### "always"

This option disallows all assignments in conditional statement tests. All assignments are treated as problems.

该选项禁止所有的赋值出现在条件语句中。所有的赋值都会被视为是问题。

The following patterns are considered problems:

以下模式是被认为有问题的。

```js
/*eslint no-cond-assign: [2, "always"]*/

// Unintentional assignment
var x;
if (x = 0) {         /*error Unexpected assignment within an 'if' statement.*/
    var b = 1;
}

// Practical example that is similar to an error
function setHeight(someNode) {
    "use strict";
    do {             /*error Unexpected assignment within a 'do...while' statement.*/
        someNode.height = "100px";
    } while (someNode = someNode.parentNode);
}

// Practical example that wraps the assignment in parentheses
function setHeight(someNode) {
    "use strict";
    do {             /*error Unexpected assignment within a 'do...while' statement.*/
        someNode.height = "100px";
    } while ((someNode = someNode.parentNode));
}

// Practical example that wraps the assignment and tests for 'null'
function setHeight(someNode) {
    "use strict";
    do {             /*error Unexpected assignment within a 'do...while' statement.*/
        someNode.height = "100px";
    } while ((someNode = someNode.parentNode) !== null);
}
```

The following patterns are not considered problems:

以下模式是被认为没有问题的。

```js
/*eslint no-cond-assign: [2, "always"]*/

// Assignment replaced by comparison
var x;
if (x === 0) {
    var b = 1;
}
```

## Further Reading

* [JSLint -- Unexpected assignment expression](http://jslinterrors.com/unexpected-assignment-expression/)

## Version

This rule was introduced in ESLint 0.0.9.

该规则是在 ESLint 0.0.9 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-cond-assign.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-cond-assign.md)
