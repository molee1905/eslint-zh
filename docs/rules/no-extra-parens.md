---
title: Rule no-extra-parens
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Extra Parens (no-extra-parens)
# 禁止冗余的括号（no-extra-parens）

This rule restricts the use of parentheses to only where they are necessary. It may be restricted to report only function expressions.

该规则限制只有在必要的地方才使用圆括号。也可能仅限于对函数表达式的检测。

## Rule Details

### Exceptions

A few cases of redundant parentheses are always allowed:

一些冗余括号是被允许的:

* RegExp literals: `(/abc/).test(var)` is always valid.
* RegExp 字面量: `(/abc/).test(var)`是有效的。

* IIFEs: `var x = (function () {})();`, `((function foo() {return 1;})())` are always valid.
* IIFEs: `var x = (function () {})();`, `((function foo() {return 1;})())`是有效的。

### Options

The default behavior of the rule is specified by `"all"` and it will report unnecessary parentheses around any expression.The following patterns are considered problems:

该规则的默认行为被指定 ‘“all”’，它将检测所有表达式的冗余括号。下面是有问题的代码：

```js
/*eslint no-extra-parens: 2*/

a = (b * c); /*error Gratuitous parentheses around expression.*/

(a * b) + c; /*error Gratuitous parentheses around expression.*/

typeof (a);  /*error Gratuitous parentheses around expression.*/
```

The following patterns are not considered problems:

下面是正确的代码：

```js
/*eslint no-extra-parens: 2*/

(0).toString();

({}.toString.call());

(function(){} ? a() : b())

(/^a$/).test(x);
```

If the option is set to `"functions"`, only function expressions will be checked for unnecessary parentheses. The following patterns are considered problems:

如果设定为 `"functions"`, 仅仅函数表达式会被检测冗余括号。下面是有问题的代码：

```js
/*eslint no-extra-parens: [2, "functions"]*/

((function foo() {}))();           /*error Gratuitous parentheses around expression.*/

var y = (function () {return 1;}); /*error Gratuitous parentheses around expression.*/
```

The following patterns are not considered problems:

下面是正确代码：

```js
/*eslint no-extra-parens: [2, "functions"]*/

(0).toString();

({}.toString.call());

(function(){} ? a() : b());

(/^a$/).test(x);

a = (b * c);

(a * b) + c;

typeof (a);
```


## Further Reading

* [MDN: Operator Precedence](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Operator_Precedence)

## Version

This rule was introduced in ESLint 0.1.4.

该规则是在ESLint 0.1.4 中被引入的。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-extra-parens.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-extra-parens.md)
