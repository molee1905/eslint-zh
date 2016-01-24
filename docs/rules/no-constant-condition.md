---
title: Rule no-constant-condition
layout: doc
translator: ybbjegj
proofreader: molee1905
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow use of constant expressions in conditions (no-constant-condition)

# 禁止在条件中使用常量表达式 (no-constant-condition)

Comparing a literal expression in a condition is usually a typo or development trigger for a specific behavior.

在条件中，比较字面表达式通常是个书写错误或者是为了触发某个特定的行为。

```js
if (false) {
    doSomethingUnfinished();
}
```

This pattern is most likely an error and should be avoided.

这种模式最有可能个错误，应该避免。

## Rule Details

The rule is aimed at preventing the use of a constant expression in a condition.
As such, it warns whenever it sees a constant expression inside a condition expression.

该规则的目的在于防止在条件中使用常量表达式。因此，当在条件表达式中发现常量表达式时，该规则就发出警告。

The following patterns are considered problems:

以下模式被认为是有问题的：

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

以下模式被认为是没有问题的：

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

该规则在 ESLint 0.4.1 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-constant-condition.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-constant-condition.md)
