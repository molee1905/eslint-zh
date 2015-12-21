---
title: Rule no-use-before-define
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Early Use (no-use-before-define)

# 不允许提早使用 (no-use-before-define)


In JavaScript, prior to ES6, variable and function declarations are hoisted to the top of a scope, so it's possible to use identifiers before their formal declarations in code. This can be confusing and some believe it is best to always declare variables and functions before using them.

在ES6标准之前的JavaScript中，某个作用域中变量和函数的申明要提前到作用域之前，所以可能存在这种情况：此变量在申明前被使用。这会扰乱读者，部分人认为最好的做法是使用变量之前先申明变量。

In ES6, block-level bindings (`let` and `const`) introduce a "temporal dead zone" where a `ReferenceError` will be thrown with any attempt to access the variable before its declaration.

ES6中，块级绑定(`let` and `const`)引入"temporal dead zone"，当企图使用未申明的变量会抛出`ReferenceError`。

## Rule Details

This rule will warn when it encounters a reference to an identifier that has not been yet declared.

当使用一个还未申明的标示符是会报警告。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-use-before-define: 2*/
/*eslint-env es6*/

alert(a);       /*error a was used before it was defined*/
var a = 10;

f();            /*error f was used before it was defined*/
function f() {}

function g() {
    return b;  /*error b was used before it was defined*/
}
var b = 1;

// With blockBindings: true
{
    alert(c);  /*error c was used before it was defined*/
    let c = 1;
}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-use-before-define: 2*/
/*eslint-env es6*/

var a;
a = 10;
alert(a);

function f() {}
f(1);

var b = 1;
function g() {
    return b;
}

// With blockBindings: true
{
    let C;
    c++;
}
```

The rule accepts an additional option that can take the value `"nofunc"`. If this option is active, function declarations are exempted from the rule, so it is allowed to use a function name *before* its declaration.

此规则接收一个额外选项，值为`"nofunc"`。如果此项被激活，可无视函数申明，即允许提前使用未申明的函数名。

The following patterns are not considered problems when `"nofunc"` is specified:

当存在`"nofunc"`，以下写法正确：

```js
/*eslint no-use-before-define: [2, "nofunc"]*/

f();
function f() {}
```

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-use-before-define.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-use-before-define.md)
