---
title: Rule prefer-const
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Suggest using `const` (prefer-const)

# 建议使用`const` (prefer-const)

If a variable is never modified, using the `const` declaration is better.

如果一个变量从没有被修改过，最好使用`const`进行声明。

`const` declaration tells readers, "this variable is never modified," reducing cognitive load and improving maintainability.

`const`声明告诉读者，”这个变量从没有被修改过“，可以减少了认知负荷，提高可维护性。

## Rule Details

This rule is aimed at flagging variables that are declared using `let` keyword, but never modified after the initial assignment.

该规则旨在标记那些使用`let`声明，但在初始化赋值后从未被修改过的变量。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint prefer-const: 2*/
/*eslint-env es6*/

let a = 3;               /*error `a` is never modified, use `const` instead.*/
console.log(a);

// `i` is re-defined (not modified) on each loop step.
for (let i in [1,2,3]) {  /*error `i` is never modified, use `const` instead.*/
    console.log(i);
}

// `a` is re-defined (not modified) on each loop step.
for (let a of [1,2,3]) { /*error `a` is never modified, use `const` instead.*/
    console.log(a);
}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint prefer-const: 2*/
/*eslint-env es6*/

let a; // there is no initialization.
console.log(a);

// `end` is never modified, but we cannot separate the declarations without modifying the scope.
for (let i = 0, end = 10; i < end; ++i) {
    console.log(a);
}

// suggest to use `no-var` rule.
var b = 3;
console.log(b);
```

## When Not to Use It

If you don't want to be notified about variables that are never modified after initial assignment, you can safely disable this rule.

如果你不想被通知哪些变量初始化赋值后再没有被修改过，禁用此规则即可。

## Related

* [no-var](no-var)

## Version

This rule was introduced in ESLint 0.23.0.

该规则在ESLint 0.23.0 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/prefer-const.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/prefer-const.md)
