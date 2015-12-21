---
title: Rule no-shadow
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Shadowing (no-shadow)

# 不允许覆盖 (no-shadow)

Shadowing is the process by which a local variable shares the same name as a variable in its containing scope. For example:

覆盖是指在同一作用域里局部变量和全局变量同名，比如：

```js
var a = 3;
function b() {
    var a = 10;
}
```

In this case, the variable `a` inside of `b()` is shadowing the variable `a` in the global scope. This can cause confusion while reading the code and it's impossible to access the global variable.

在这种情况中，`b()`作用域中的`a`覆盖了全局环境中的`a`。这会混淆读者并且在`b`中不能获取全局变量。

## Rule Details

This rule aims to eliminate shadowed variable declarations.

此规则旨在消除变量声明覆盖。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-shadow: 2*/
/*eslint-env es6*/

var a = 3;
function b() {
    var a = 10;       /*error a is already declared in the upper scope.*/
}

var b = function () {
    var a = 10;       /*error a is already declared in the upper scope.*/
}

function b(a) {       /*error a is already declared in the upper scope.*/
    a = 10;
}
b(a);

if (true) {
    let a = 5;        /*error a is already declared in the upper scope.*/
}
```

### Options

This rule takes one option, an object, with properties `"builtinGlobals"`, `"hoist"` and `"allow"`.

对象配置项，包含属性`"builtinGlobals"`,`"hoist"` 和`"allow"`.

```json
{
    "no-shadow": [2, {"builtinGlobals": false, "hoist": "functions", "allow": []}]
}
```

#### builtinGlobals

`false` by default.
If this is `true`, this rule checks with built-in global variables such as `Object`, `Array`, `Number`, ...

默认值是`false`，如果builtinGlobals是`true`，会检测内置对象如`Object`,`Array`,`Number`, ...


When `{"builtinGlobals": true}`, the following patterns are considered problems:

当`{"builtinGlobals": true}`，以下写法错误：

```js
/*eslint no-shadow: [2, { "builtinGlobals": true }]*/

function foo() {
    var Object = 0; /*error Object is already declared in the upper scope.*/
}
```

#### hoist

The option has three settings:

此配置项有三个值：

* `all` - reports all shadowing before the outer variables/functions are defined.
* `all`-在被覆盖之前呈报函数和变量的覆盖错误。
* `functions` (by default) - reports shadowing before the outer functions are defined.
* `functions`(默认值)-在被覆盖前呈报函数覆盖错误。
* `never` - never report shadowing before the outer variables/functions are defined.
* `never`-不呈报覆盖错误。


##### { "hoist": "all" }

With `"hoist"` set to `"all"`, both `let a` and `let b` in the `if` statement are considered problems.

当`"hoist"`配置项为`"all"`，在条件语句中`let a`和`let b`是不恰当的。

```js
/*eslint no-shadow: [2, { "hoist": "all" }]*/
/*eslint-env es6*/

if (true) {
    let a = 3;    /*error a is already declared in the upper scope.*/
    let b = 6;    /*error b is already declared in the upper scope.*/
}

let a = 5;
function b() {}
```

##### { "hoist": "functions" } (default)

With `"hoist"` set to `"functions"`, `let b` is considered a warning. But `let a` in the `if` statement is not considered a warning, because it is before `let a` of the outer scope.

当`"hoist"`配置项为`"functions"`，在条件语句中有`let a`和`let b`会报警告。


```js
/*eslint no-shadow: [2, { "hoist": "functions" }]*/
/*eslint-env es6*/

if (true) {
    let a = 3;
    let b = 6;    /*error b is already declared in the upper scope.*/
}

let a = 5;
function b() {}
```

##### { "hoist": "never" }

With `"hoist"` set to `"never"`, neither `let a` nor `let b` in the `if` statement are considered problems, because they are before the declarations of the outer scope.

当`"hoist"`设置为`"never"`,条件语句中有`let a`和`let b`不会报警告，因为他们在外面声明了。

```js
/*eslint no-shadow: [2, { "hoist": "never" }]*/
/*eslint-env es6*/

if (true) {
    let a = 3;
    let b = 6;
}

let a = 5;
function b() {}
```

#### allow

The option is an array of identifier names to be allowed (ie. "resolve", "reject", "done", "cb" etc.):

此配置项是一个数组,数组里的标示被允许覆盖

```json
{
    "rules": {
        "no-shadow": [2, {"allow": ["done"]}]
    }
}
```

Allows for the following code to be valid:

下面的代码是有效的：

```js
import async from 'async';

function foo(done) {
  async.map([1, 2], function (e, done) {
    done(null, e * 2)
  }, done);
}

foo(function (err, result) {
  console.log({ err, result });
});
```

## Further Reading

* [Variable Shadowing](http://en.wikipedia.org/wiki/Variable_shadowing)

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-shadow.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-shadow.md)
