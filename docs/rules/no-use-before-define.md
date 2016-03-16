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

This rule will warn when it encounters a reference to an identifier that has not yet been declared.

当使用一个还未申明的标示符是会报警告。

Examples of **incorrect** code for this rule:

**错误**代码示例：

```js
/*eslint no-use-before-define: 2*/
/*eslint-env es6*/

alert(a);
var a = 10;

f();
function f() {}

function g() {
    return b;
}
var b = 1;

// With blockBindings: true
{
    alert(c);
    let c = 1;
}
```

Examples of **correct** code for this rule:

**正确**代码示例：

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

## Options

```json
{
    "no-use-before-define": [2, { "functions": true, "classes": true }]
}
```

* `functions` (`boolean`) -
  The flag which shows whether or not this rule checks function declarations.
  If this is `true`, this rule warns every reference to a function before the function declaration.
  Otherwise, ignores those references.
  Function declarations are hoisted, so it's safe.
  Default is `true`.
* `classes` (`boolean`) -
  The flag which shows whether or not this rule checks class declarations of upper scopes.
  If this is `true`, this rule warns every reference to a class before the class declaration.
  Otherwise, ignores those references if the declaration is in upper function scopes.
  Class declarations are not hoisted, so it might be danger.
  Default is `true`.

This rule accepts `"nofunc"` string as a option.
`"nofunc"` is the same as `{ "functions": false, "classes": true }`.

### functions

Examples of **correct** code for the `{ "functions": false }` option:

选项`{ "functions": false }`的 **正确**代码示例：

```js
/*eslint no-use-before-define: [2, { "functions": false }]*/

f();
function f() {}
```

### classes

Examples of **incorrect** code for the `{ "classes": false }` option:

选项`{ "classes": false }`的 **错误**代码示例：

```js
/*eslint no-use-before-define: [2, { "classes": false }]*/
/*eslint-env es6*/

new A();
class A {
}
```

Examples of **correct** code for the `{ "classes": false }` option:

选项`{ "classes": false }`的 **正确**代码示例：

```js
/*eslint no-use-before-define: [2, { "classes": false }]*/
/*eslint-env es6*/

function foo() {
    return new A();
}

class A {
}
```

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-use-before-define.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-use-before-define.md)
