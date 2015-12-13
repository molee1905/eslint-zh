---
title: Rule arrow-body-style
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Require braces in arrow function body (arrow-body-style)

# 要求箭头函数体使用大括号 (arrow-body-style)

Arrow functions can omit braces when there is a single statement in the body. This rule enforces the consistent use of braces in arrow functions.

箭头函数体内只有单独一条语句是，可以省略大括号。该规则强制箭头函数中大括号的使用的一致性。

Additionally, this rule specifically warns against a possible developer error when the intention is to return an empty object literal but creates an empty block instead, returning undefined.

此外，当开发者想要返回一个空对象但却创建了一个空的块，返回了undefined时，该规则将发出警告。

```js
/*eslint-env es6*/
// Bad
var foo = () => {};

// Good
var foo = () => ({});
```

## Rule Details

This rule can enforce the use of braces around arrow function body.

该规则强制在箭头函数体周围大括号的使用。

### Options

The rule takes one option, a string, which can be:

该规则有一个选项，是个字符串，可以是：

* `"always"` enforces braces around the function body
* `"always"` 强制在箭头函数体周围使用大括号
* `"as-needed"` enforces no braces where they can be omitted (default)
* `"as-needed"` 当大括号是可以省略的，强制不使用它们 (默认)

#### "always"

```json
"arrow-body-style": [2, "always"]
```

When the rule is set to `"always"` the following patterns are considered problems:

当设置为`"always"`，以下模式被认为是有问题的：

```js
/*eslint arrow-body-style: [2, "always"]*/
/*eslint-env es6*/
let foo = () => 0;
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
let foo = () => {
    return 0;
};
let foo = (retv, name) => {
    retv[name] = true;
    return retv;
};
```

#### "as-needed"

When the rule is set to `"as-needed"` the following patterns are considered problems:

当设置为`"as-needed"` ，以下模式被认为是有问题的：

```js
/*eslint arrow-body-style: [2, "as-needed"]*/
/*eslint-env es6*/

let foo = () => {
    return 0;
};

let foo = () => {};
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint arrow-body-style: [2, "as-needed"]*/
/*eslint-env es6*/

let foo = () => 0;
let foo = (retv, name) => {
    retv[name] = true;
    return retv;
};
let foo = () => { bar(); };
let foo = () => { /* do nothing */ };
let foo = () => {
    // do nothing.
};
```

## Version

This rule was introduced in ESLint 1.8.0.

该规则在ESLint 1.8.0 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/arrow-body-style.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/arrow-body-style.md)
