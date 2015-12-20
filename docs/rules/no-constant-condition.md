---
title: Rule no-constant-condition
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow use of constant expressions in conditions (no-constant-condition)

# 禁止在条件中使用常量表达式

Comparing a literal expression in a condition is usually a typo or development trigger for a specific behavior.

比较表达字面量在条件中通常是个typo(错字)或者是某个特殊行为的触发器。

```js
if (false) {
    doSomethingUnfinished();
}
```

This pattern is most likely an error and should be avoided.

该模式绝大部分情况下是个错误，应该避免。

## Rule Details

The rule is aimed at preventing the use of a constant expression in a condition.
As such, it warns whenever it sees a constant expression inside a condition expression.

该规则的目的在于防止在条件中使用常量表达式。因此，在条件表达式中发现常量表达式就发布警告。

The following patterns are considered problems:

下面的模式被认为是有问题的：

```js
/*eslint no-constant-condition: 2*/

if (true) {             /*error Unexpected constant condition.*/
    doSomething();
}
```

```js
/*eslint no-constant-condition: 2*/

var result = 0 ? a : b; /*error Unexpected constant condition.*/
```

```js
/*eslint no-constant-condition: 2*/

while (-2) {            /*error Unexpected constant condition.*/
    doSomething();
}
```

```js
/*eslint no-constant-condition: 2*/

for (;true;) {          /*error Unexpected constant condition.*/
    doSomething();
}
```

```js
/*eslint no-constant-condition: 2*/

do{                     /*error Unexpected constant condition.*/
    something();
} while (x = -1)
```

The following patterns are not considered problems:

```js
/*eslint no-constant-condition: 2*/

if (x === 0) {
    doSomething();
}
```

```js
/*eslint no-constant-condition: 2*/

do {
    something();
} while (x)
```

```js
/*eslint no-constant-condition: 2*/

for (;;) {
    something();
}
```

## Version

This rule was introduced in ESLint 0.4.1.

该规则是在ESLint 0.4.1中被引入的

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-constant-condition.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-constant-condition.md)
