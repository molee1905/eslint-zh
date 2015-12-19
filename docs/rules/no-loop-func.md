---
title: Rule no-loop-func
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Functions in Loops (no-loop-func)

Writing functions within loops tends to result in errors due to the way the function creates a closure around the loop. For example:

在循环中编写函数会导致结果错误，是由于函数在循环中创建了一个闭包。例如：

```js
for (var i = 0; i < 10; i++) {
    funcs[i] = function() {
        return i;
    };
}
```

In this case, you would expect each function created within the loop to return a different number. In reality, each function returns 10, because that was the last value of `i` in the scope.

在例子中，你预期在循环中创建的各个函数返回不同的数字。实际上，各个函数都返回10，因为那是`i`在作用域中的最后值。

`let` or `const` mitigate this problem.

`let` 或者 `const`缓解此问题。 

```js
/*eslint-env es6*/

for (let i = 0; i < 10; i++) {
    funcs[i] = function() {
        return i;
    };
}
```

In this case, each function created within the loop returns a different number as expected.

在此例子中，在循环中创建的各个函数按预期返回不同的数字。


## Rule Details

This error is raised to highlight a piece of code that may not work as you expect it to and could also indicate a misunderstanding of how the language works. Your code may run without any problems if you do not fix this error, but in some situations it could behave unexpectedly.

引入错误来标记出不按你预期执行的代码片段，也能指出对代码如何运行的误解。如果不修复此错误，你的代码运行是不会有任何错误的，但是在一些情况下，它会有意想不到的行为。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-loop-func: 2*/
/*eslint-env es6*/

for (var i=10; i; i--) {
    (function() { return i; })();     /*error Don't make functions within a loop*/
}

while(i) {
    var a = function() { return i; }; /*error Don't make functions within a loop*/
    a();
}

do {
    function a() { return i; };      /*error Don't make functions within a loop*/
    a();
} while (i);

let foo = 0;
for (let i=10; i; i--) {
    // Bad, function is referencing block scoped variable in the outer scope.
    var a = function() { return foo; }; /*error Don't make functions within a loop*/
    a();
}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-loop-func: 2*/
/*eslint-env es6*/

var a = function() {};

for (var i=10; i; i--) {
    a();
}

for (var i=10; i; i--) {
    var a = function() {}; // OK, no references to variables in the outer scopes.
    a();
}

for (let i=10; i; i--) {
    var a = function() { return i; }; // OK, all references are referring to block scoped variable in the loop.
    a();
}
```

## Further Reading

* [Don't make functions within a loop](http://jslinterrors.com/dont-make-functions-within-a-loop/)

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-loop-func.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-loop-func.md)
