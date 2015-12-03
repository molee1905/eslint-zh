---
title: Rule init-declarations
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Enforce/Disallow Variable Initializations (init-declarations)
# 强制/禁止变量初始化（初始化声明）

In JavaScript, variables can be assigned during declaration, or at any point afterwards using an assignment statement. For example, in the following code, `foo` is initialized during declaration, while `bar` is initialized later.

在JavaScript中，变量可在声明时初始化，或者在赋值语句中初始化。例如，在下面的代码中， `foo` 在声明时被初始化，然而 `bar` 在之后被初始化。

```js
var foo = 1;
var bar;

if (foo) {
    bar = 1;
} else {
    bar = 2;
}
```

## Rule Details

This rule is aimed at enforcing or eliminating variable initializations during declaration. For example, in the following code, `foo` is initialized during declaration, while `bar` is not.

此规则旨在声明的过程中强制或限制变量初始化。例如，在下面的代码， `foo` 在声明过程中初始化，然而 `bar` 不是。

```js
var foo = 1;
var bar;

bar = 2;
```

This rule aims to bring consistency to variable initializations and declarations.

这一规则的目的是使变量初始化和声明一致。

### Options

The rule takes two options:

1. A string which must be either `"always"` (the default), to enforce initialization at declaration, or `"never"` to disallow initialization during declaration. This rule applies to `var`, `let`, and `const` variables, however `"never"` is ignored for `const` variables, as unassigned `const`s generate a parse error.
2. An object that further controls the behavior of this rule. Currently, the only available parameter is `ignoreForLoopInit`, which indicates if initialization at declaration is allowed in `for` loops when `"never"` is set, since it is a very typical use case.

此规则有两个配置项：

1. 字符串，必须是二者之一， `"always"` （默认值）：强制在声明时初始化，或 `"never"` ：声明时不允许初始化。此规则适用于 `var`， `let` ，和 `const` 变量，但是 `"never"` 被 `const` 变量忽略，而未初始化 `const` 会产生解析错误。
2. 对象，进一步控制该规则的行为。目前，唯一可用的参数是 `ignoreForLoopInit` ，这表明是否允许在 `for` 循环语句中声明并初始化变量， 即使设置 `"nerver"`，这是一个非常典型的用例。

### Options

This rule is configured by passing in the string `"always"` (the default)

这条规则是通过传字符串 `"always"` （默认）配置的

You can configure the rule as follows:

您可以配置规则，如下：

(default) All variables must be initialized at declaration

（默认值）所有变量必须在声明时初始化

```json
{
    "init-declarations": [2, "always"],
}
```

Variables must not be initialized at declaration

变量不能在声明时初始化

```json
{
    "init-declarations": [2, "never"]
}
```

Variables must not be initialized at declaration, except in for loops, where it is allowed

变量不能在声明时初始化，除在for循环中，在那里它被允许

```json
{
    "init-declarations": [2, "never", { "ignoreForLoopInit": true }]
}
```

When configured with `"always"` (the default), the following patterns are considered problems:


当配置了  `"always"` (默认值） ，以下模式被认为有问题：

```js
/*eslint init-declarations: [2, "always"]*/
/*eslint-env es6*/

function foo() {
    var bar;     /*error Variable 'bar' should be initialized on declaration.*/
    let baz;     /*error Variable 'baz' should be initialized on declaration.*/
}
```

The following patterns are not considered problems with `"always"`.

下面的模式不被视为有问题 `"always"`。

```js
/*eslint init-declarations: [2, "always"]*/
/*eslint-env es6*/

function foo() {
    var bar = 1;
    let baz = 2;
    const qux = 3;
}
```

When configured with `"never"`, the following patterns are considered problems.

当配置 `"never"`，以下模式被认为有问题。

```js
/*eslint init-declarations: [2, "never"]*/
/*eslint-env es6*/

function foo() {
    var bar = 1;   /*error Variable 'bar' should not be initialized on declaration.*/
    let baz = 2;   /*error Variable 'baz' should not be initialized on declaration.*/

    for (var i = 0; i < 1; i++) {}  /*error Variable 'i' should not be initialized on declaration.*/
}
```

The following patterns are not considered problems with `"never"`. Note that `const` variable initializations are ignored with `"never"`.

下面的模式不被视有问题 `"never"`。需要注意的是 `const` 变量初始化忽略 `"never"`。

```js
/*eslint init-declarations: [2, "never"]*/
/*eslint-env es6*/

function foo() {
    var bar;
    let baz;
    const buzz = 1;
}
```

With `"ignoreForLoopInit"` enabled, the following pattern is not considered a problem.

随着 `"ignoreForLoopInit"` 启用，下面的模式不被视为有问题。

```js
/*eslint init-declarations: [2, "never", { "ignoreForLoopInit": true }]*/
for (var i = 0; i < 1; i++) {}
```

### When Not To Use It

When you are indifferent as to how your variables are initialized.

你还会对于怎样初始化变量莫不关心。

## Version

This rule was introduced in ESLint 1.0.0-rc-1.

此规则在ESLint 1.0.0-rc-1中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/init-declarations.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/init-declarations.md)
