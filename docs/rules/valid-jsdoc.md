---
title: Rule valid-jsdoc
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Validates JSDoc comments are syntactically correct (valid-jsdoc)

# 验证JSDoc注释是语法正确的

[JSDoc](http://usejsdoc.org) is a JavaScript API documentation generator. It uses specially-formatted comments inside of code to generate API documentation automatically. For example, this is what a JSDoc comment looks like for a function:

[JSDoc](http://usejsdoc.org)是一个Javascript API 文档生成器。它在代码中使用特殊格式的注释来自动生成API文档。例如，这就是一个函数的JSDoc注释的样子：

```js
/**
 * Adds two numbers together.
 * @param {int} num1 The first number.
 * @param {int} num2 The second number.
 * @returns {int} The sum of the two numbers.
 */
function sum(num1, num2) {
    return num1 + num2;
}
```

The JSDoc comments have a syntax all their own, and it is easy to mistakenly mistype a comment because comments aren't often checked for correctness in editors. Further, it's very easy for the function definition to get out of sync with the comments, making the comments a source of confusion and error.

JSDoc注释有自己的语法，它很容易错误书写一个注释，因为编辑器不检查注释的正确性。此外，它很容易造成函数定义和注释的不同步，使得注释是混乱和错误的。

## Rule Details

This rule aims to prevent invalid and incomplete JSDoc comments. In doing so, it will warn when:

该规则旨在防止无效的和不完整的JSDoc注释。这样做，它将发出警告，当：

1. There is a JSDoc syntax error
1. 有JSDoc语法错误
1. A `@param` or `@returns` is used without a type specified
1. `@param` 或 `@returns` 没有指定类型
1. A `@param` or `@returns` is used without a description
1. `@param` 或 `@returns` 没有描述
1. A comment for a function is missing `@returns`
1. 函数的注释缺少 `@returns`
1. A parameter has no associated `@param` in the JSDoc comment
1. 一个参数在JSDoc注释中没有对应的`@param`
1. `@param`s are out of order with named arguments
1. `@param`与命名的参数顺序不对应

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint valid-jsdoc: 2*/

// missing type for @param and missing @returns
/**                                 // 2 errors
 * A description
 * @param num1 The first number.
 */
function foo(num1) {
    // ...
}

// missing description for @param
/**                                 //error Missing JSDoc parameter description for 'num1'.
 * A description
 * @param {int} num1
 * @returns {void}
 */
function foo(num1) {
    // ...
}

// no description for @returns
/**                                 //error Missing JSDoc return description.
 * A description
 * @returns {int}
 */
function foo() {
    // ...
}

// no type for @returns
/**                                 //error JSDoc syntax error.
 * A description
 * @returns Something awesome
 */
function foo() {
    // ...
}

// missing @param
/**                                 //error Missing JSDoc for parameter 'a'.
 * A description
 * @returns {void}
 */
function foo(a) {
    // ...
}

// incorrect @param
/**                                 //error Expected JSDoc for 'a' but found 'b'.
 * A description
 * @param {string} b Desc
 * @returns {void}
 */
function foo(a) {
    // ...
}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint valid-jsdoc: 2*/

/**
 * Adds two numbers together.
 * @param {int} num1 The first number.
 * @param {int} num2 The second number.
 * @returns {int} The sum of the two numbers.
 */
function foo(num1, num2) {
    return num1 + num2;
}

/**
 * Represents a sum.
 * @param {int} num1 The first number.
 * @param {int} num2 The second number.
 * @constructor
 */
function foo(num1, num2) { }

// use of @override make @param and @returns optional
/**
 * A description
 * @override
 */
function foo(a) {
    return a;
}
```

### Options

#### prefer

JSDoc offers a lot of tags with overlapping meaning. For example, both `@return` and `@returns` are acceptable for specifying the return value of a function. However, you may want to enforce a certain tag be used instead of others. You can specify your preferences regarding tag substitution by providing a mapping called `prefer` in the rule configuration. For example, to specify that `@returns` should be used instead of `@return`, you can use the following configuration:

JSDoc提供了很多有重叠的标签.例如，`@return` 和 `@returns`都是可接受的，用来指定一个函数的返回值。然而，你可能想强制使用一个特定的标签而不是其他的。你可以通过在规则配置中提供一个`prefer`映射，指定你关于标签的替代的首选项。例如，指定必须使用`@returns`而不是`@return`，你可以使用如下配置：

```json
"valid-jsdoc": [2, {
    "prefer": {
        "return": "returns"
    }
}]
```

With this configuration, ESLint will warn when it finds `@return` and recommend to replace it with `@returns`.

在这个配置中，当ESLint发现`@return`，它将发出警告，并推荐使用`@returns`代替。


#### requireReturn

By default ESLint requires you to specify `@return` for every documented function regardless of whether there is anything returned by the function. While using `@return {void}` or `@return {undefined}` stops it from asking for a description of the return value using the `requireReturn` option and setting it to `false` prevents an error from being logged unless there is a return in the function. Note that with this option set to `false`, if there is a return in the function, an error will still be logged and if there is a `@return` specified and there are no `return` statements in the function an error will also be logged. This option is purely to prevent the forced addition of `@return {void}` to an entire codebase not to turn off JSDoc return checking.

默认情况下，ESLint要求你为每个documented函数指定`@return`，不管该函数中是否有返回值。当使用`@return {void}` 或 `@return {undefined}`不再要求返回值有描述，使用`requireReturn`并设置它为`false`, 防止一个错误被记入日志，除非函数中有一个返回语句。注意，该选项设置为`false`时，如果函数中有一个返回语句，一个错误仍将被记入日志。如果有个指定的`@return`，并且函数中没有`return`语句一个错误仍将被记入日志。这个选项纯粹是为了防止不关掉JSDoc返回检查的情况下强制添加`@return {void}`到整个代码库。

```json
"valid-jsdoc": [2, {
    "requireReturn": false
}]
```

#### requireParamDescription

By default ESLint requires you to specify a description for each `@param`. You can choose not to require descriptions for `@param` by setting `requireParamDescription` to `false`.

默认情况下，ESLint要求你为每个`@param`指定一个描述。你可以通过设置`requireParamDescription`为`false`选择不要求`@param`有描述。

```json
"valid-jsdoc": [2, {
    "requireParamDescription": false
}]
```

#### requireReturnDescription

By default ESLint requires you to specify a description for each `@return`. You can choose not to require descriptions for `@return` by setting `requireReturnDescription` to `false`.

默认情况下，ESLint要求你为每个`@reutrn`指定一个描述。你可以通过设置`requireReturnDescription`为`false`选择不要求`@return`有描述。

```json
"valid-jsdoc": [2, {
    "requireReturnDescription": false
}]
```

#### matchDescription

Specify a regular expression to validate JSDoc comment block description against.

指定一个正则表达式验证JSDoc注释块的描述。

```json
"valid-jsdoc": [2, {
    "matchDescription": "^[A-Z][A-Za-z0-9\\s]*[.]$"
}]
```

#### requireReturnType

By default ESLint requires you to specify `type` for `@return` tag for every documented function.

默认情况下，ESLint要求你为每个documented函数的`@return`标签指定`type`。

```json
"valid-jsdoc": [2, {
    "requireReturnType": false
}]
```

## When Not To Use It

If you aren't using JSDoc, then you can safely turn this rule off.

如果你不使用JSDoc，你可以关闭此规则。

## Further Reading

* [JSDoc](http://usejsdoc.org)

## Version

This rule was introduced in ESLint 0.4.0.

该规则在ESLint 0.4.0中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/valid-jsdoc.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/valid-jsdoc.md)
