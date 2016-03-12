---
title: Rule no-undef
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow Undeclared Variables (no-undef)

# 不允许使用未申明变量 (no-undef)

This rule can help you locate potential ReferenceErrors resulting from misspellings of variable and parameter names, or accidental implicit globals (for example, from forgetting the `var` keyword in a `for` loop initializer).

此规则可帮助你定位由变量漏写，参数名漏写和accidental implicit globals所导致的潜在ReferenceErrors错误（比如，在`for`循环语句中初始化变量忘写`var`关键字）

## Rule Details

Any reference to an undeclared variable causes a warning, unless the variable is explicitly mentioned in a `/*global ...*/` comment.

对未声明的变量的任何引用都会引起警告，除非显式地在`/*global ...*/`注释中指定。

Examples of **incorrect** code for this rule:

**错误** 代码示例：

```js
/*eslint no-undef: 2*/

var a = someFunction();
b = 10;
```

Examples of **correct** code with `global` declaration for this rule:

声明`global`情况下，该规则的 **正确** 代码示例：

```js
/*global someFunction b:true*/
/*eslint no-undef: 2*/

var a = someFunction();
b = 10;
```

The `b:true` syntax in `/*global */` indicates that assignment to `b` is correct.

Examples of **incorrect** code with `global` declaration for this rule:

声明`global`情况下，该规则的 **错误** 代码示例：

```js
/*global b*/
/*eslint no-undef: 2*/

b = 10;
```

By default, variables declared in `/*global */` are read-only, therefore assignment is incorrect.

默认地，在`/*global */`声明的变量是只读的，因此对其赋值是错误的。

## Options

* `typeof` set to true will warn for variables used inside typeof check (Default false).
* `typeof` 设置为true，typeof 检查中使用未定义变量将发出警告 (默认值：false)

### typeof

Examples of **correct** code for the default option:

默认选项的 **正确** 代码示例：

```js
/*eslint no-undef: 2*/

if (typeof UndefinedIdentifier === "undefined") {
    // do something ...
}
```

You can use this option if you want to prevent `typeof` check on a variable which has not been declared.

如果想阻在止运算中有未申明的变量导致的警告，可以用此项。

Examples of **incorrect** code for the `{ "typeof": true }` option:

选项`{ "typeof": true }`的 **错误** 代码示例：

```js
/*eslint no-undef: [2, { "typeof": true }] */

if(typeof a === "string"){}
```

Examples of **correct** code for the `{ "typeof": true }` option:

选项`{ "typeof": true }`的 **正确** 代码示例：

```js
/*global a*/
/*eslint no-undef: [2, { "typeof": true }] */

if(typeof a === "string"){}
```

## Environments

For convenience, ESLint provides shortcuts that pre-define global variables exposed by popular libraries and runtime environments. This rule supports these environments, as listed in [Specifying Environments](http://eslint.org/docs/user-guide/configuring#specifying-environments).  A few examples are given below.

为了方便，ESlint通过流行类库和运行时环境快捷预定义暴露的全局变量。此快捷方式支持[环境](http://eslint.org/docs/user-guide/configuring#specifying-environments)。使用如下：

### browser

Defines common browser globals.

普通浏览器中使用全局变量。

```js
/*eslint-env browser*/

setTimeout(function() {
    alert("Hello");
});
```

### node

Defines globals for Node.js development.

Node.js中全局变量。

```js
/*eslint-env node*/

var fs = require("fs");
module.exports = function() {
    console.log(fs);
};
```

## When Not To Use It

If explicit declaration of global variables is not to your taste.

如果明确不需要申明全局变量。

## Compatibility

This rule provides compatibility with treatment of global variables in [JSHint](http://www.jshint.com) and [JSLint](http://www.jslint.com).

## Further Reading

* ['{a}' is not defined](http://jslinterrors.com/a-is-not-defined)

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-undef.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-undef.md)
