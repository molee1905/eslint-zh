---
title: Rule comma-dangle
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow or Enforce Dangling Commas (comma-dangle)
# 禁止或执行多余的逗号（comma-dangle）
Trailing commas in object literals are valid according to the ECMAScript 5 (and ECMAScript 3!) spec. However, IE8 (when not in IE8 document mode) and below will throw an error when it encounters trailing commas in JavaScript.

根据ECMAScript5和ECMAScript3规范，对象字面量中的尾逗号是合法的。但是，尾逗号在IE8（非IE8文档模式）及以下将抛出错误。

```js
var foo = {
    bar: "baz",
    qux: "quux",
};
```

On the other hand, trailing commas simplify adding and removing items to objects and arrays, since only the lines you are modifying must be touched.

另外，尾逗号简化对象和数组的添加和删除，因为仅仅涉及到你修改的行。

## Rule Details

This rule enforces consistent use of trailing commas in object and array literals.

这个规则强制在对象和数组字面量中使用一致的尾逗号。

This rule takes one argument, which can be one of the following options:

这个规则接受一个参数，可以是如下选项之一：

- `"always"` - warn whenever a missing comma is detected.

- `"always"` - 只要检测到缺失逗号，就显示警告。

- `"always-multiline"` - warn if there is a missing trailing comma on arrays or objects that span multiple lines, and warns if there is a trailing comma present on single line arrays or objects.

- `"always-multiline"` - 在跨行的数组和对象中缺失尾逗号或者在单行数组和对象中出现尾逗号，都将显示警告。

- `"never"` - warn whenever a trailing comma is detected.

- `"never"` - 只要检测到尾逗号，就显示警告。

The default value of this option is `"never"`.

接受的默认选项是 `"never"`。

The following patterns are considered problems when configured `"never"`:

规则配置成 `"never"`,下面的模式是被认为有问题的:

```js
/*eslint comma-dangle: [2, "never"]*/

var foo = {
    bar: "baz",
    qux: "quux",   /*error Unexpected trailing comma.*/
};

var arr = [1,2,];  /*error Unexpected trailing comma.*/

foo({
  bar: "baz",
  qux: "quux",     /*error Unexpected trailing comma.*/
});
```

The following patterns are not considered problems when configured `"never"`:

规则配置成 `"never"`,下面的模式是被认为没有问题的

```js
/*eslint comma-dangle: [2, "never"]*/

var foo = {
    bar: "baz",
    qux: "quux"
};

var arr = [1,2];

foo({
  bar: "baz",
  qux: "quux"
});
```

The following patterns are considered problems when configured `"always"`:

规则配置成 `"always"`,下面的模式是被认为有问题的:

```js
/*eslint comma-dangle: [2, "always"]*/

var foo = {
    bar: "baz",
    qux: "quux"   /*error Missing trailing comma.*/
};

var arr = [1,2];  /*error Missing trailing comma.*/

foo({
  bar: "baz",
  qux: "quux"     /*error Missing trailing comma.*/
});
```

The following patterns are not considered problems when configured `"always"`:

规则配置成 `"always"`,下面的模式是被认为没有问题的:

```js
/*eslint comma-dangle: [2, "always"]*/

var foo = {
    bar: "baz",
    qux: "quux",
};

var arr = [1,2,];

foo({
  bar: "baz",
  qux: "quux",
});
```

The following patterns are considered problems when configured `"always-multiline"`:

规则配置成 `"always-multiline"`,下面的模式是被认为有问题的:


```js
/*eslint comma-dangle: [1, "always-multiline"]*/

var foo = {
    bar: "baz",
    qux: "quux"                         /*error Missing trailing comma.*/
};

var foo = { bar: "baz", qux: "quux", }; /*error Unexpected trailing comma.*/

var arr = [1,2,];                       /*error Unexpected trailing comma.*/

var arr = [1,
    2,];                                /*error Unexpected trailing comma.*/

var arr = [
    1,
    2                                   /*error Missing trailing comma.*/
];

foo({
  bar: "baz",
  qux: "quux"                           /*error Missing trailing comma.*/
});
```

The following patterns are not considered problems when configured `"always-multiline"`:

规则配置成 `"always-multiline"`,下面的模式是被认为没有问题的:

```js
/*eslint comma-dangle: [2, "always-multiline"]*/

var foo = {
    bar: "baz",
    qux: "quux",
};

var foo = {bar: "baz", qux: "quux"};
var arr = [1,2];

var arr = [1,
    2];

var arr = [
    1,
    2,
];

foo({
  bar: "baz",
  qux: "quux",
});
```

## When Not To Use It

You can turn this rule off if you are not concerned with dangling commas.

如果不关心多余逗号的问题，你可以关闭这个规则。

## Version

This rule was introduced in ESLint 0.16.0.

该规则是在ESLint 0.16.0 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/comma-dangle.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/comma-dangle.md)
