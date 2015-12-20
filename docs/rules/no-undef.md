---
title: Rule no-undef
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Undeclared Variables (no-undef)

# 不允许使用未申明变量(no-undef)

Any reference to an undeclared variable causes a warning, unless the variable is explicitly mentioned in a `/*global ...*/` comment. This rule provides compatibility with [JSHint](http://www.jshint.com)'s and [JSLint](http://www.jslint.com)'s treatment of global variables.

引用任何一个未申明的变量都会报警告，除非此变量在全局中明确被提到。此规则兼容[JSHint](http://www.jshint.com) and [JSLint](http://www.jslint.com)。

This rule can help you locate potential ReferenceErrors resulting from misspellings of variable and parameter names, or accidental implicit globals (for example, from forgetting the `var` keyword in a `for` loop initializer).

此规则可帮助你定位由变量漏写，参数名漏写和accidental implicit globals所导致的潜在ReferenceErrors错误（比如，在`for`循环语句中初始化变量忘写`var`关键字）

## Rule Details

### Options

* `typeof` set to true will warn for variables used inside typeof check (Default false).
* `typeof`设置为true，检测在运算中的变量，不符合规则报警告(默认值：false)

The following code causes 2 warnings, as the globals `someFunction` and `b` have not been declared.

当在全局环境中没有申明过`someFunction`和`b`，下面代码导致两个警告。

```js
/*eslint no-undef: 2*/

var a = someFunction();  /*error "someFunction" is not defined.*/
b = 10;                  /*error "b" is not defined.*/
```

In this code, no warnings are generated, since the global variables have been properly declared in a `/*global */` block.

在这种情况下，没有警告，因为全局变量已经被申明过。

```js
/*global someFunction b:true*/
/*eslint no-undef: 2*/

var a = someFunction();
b = 10;
```

By default, variables declared in `/*global */` are considered read-only. Assignment to a read-only global causes a warning:

默认全局变量只可读，赋值给一个只可读的全局变量引起警告。

```js
/*global b*/
/*eslint no-undef: 2*/


b = 10;                  /*error "b" is read only.*/
```

Use the `variable:true` syntax to indicate that a variable can be assigned to.

使用`variable:true`语法来表示一个变量可被赋值。

```js
/*global b:true*/
/*eslint no-undef: 2*/

b = 10;
```

Explicitly checking an undefined identifier with `typeof` causes no warning.

适应`typeof`检测一个未定义的标示符不会提示警告。

```js
/*eslint no-undef: 2*/

if (typeof UndefinedIdentifier === "undefined") {
    // do something ...
}
```

#### typeof

You can use this option if you want to prevent `typeof` check on a variable which has not been declared.

如果想阻在止运算中有未申明的变量导致的警告，可以用此项。

The following patterns are considered problems with option `typeof` set:

当设置为`typeof`，以下模式被认为是有问题的：

```js
/* eslint no-undef: [2, { typeof: true }] */

if(typeof a === "string"){}      /* error "a" is not defined. */
```

The following patterns are not considered problems with option `typeof` set:

当设置为`typeof`，以下模式被认为是没有问题的：

```js
/* eslint no-undef: [2, { typeof: true }] */
/*global a*/

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

## Further Reading

* ['{a}' is not defined](http://jslinterrors.com/a-is-not-defined)

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-undef.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-undef.md)
