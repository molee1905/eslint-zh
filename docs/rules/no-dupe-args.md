---
title: Rule no-dupe-args
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# No duplicate arguments (no-dupe-args)
# 不支持重复参数（no-dupe-args）

In strict mode you will receive a `SyntaxError` if a function takes multiple arguments with the same name.
Outside of strict mode duplicate arguments will mask the value of the first argument. This rule checks for duplicate
parameter names to help prevent that mistake.

在严格模式下，函数若有相同名字的多个参数，将会抛出 `SyntaxError`。在非严格模式下，将使用第一个参数的值。该规则检测重复名字的参数来防止该错误。


## Rule Details

This rule prevents having duplicate param names.

该规则防止重复参数名的错误。

For example the following code will cause the rule to warn:

例如下面的代码会导致规则警告:

```js
/*eslint no-dupe-args: 2*/

function foo(a, b, a) {               /*error Duplicate param 'a'.*/
    console.log("which a is it?", a);
}
```


## When Not To Use It

If your project uses strict mode this rule may not be needed as unique param names will be automatically enforced.

如果你的项目使用严格模式，就不需要用该规则。唯一的参数名将被强制使用。

## Version

This rule was introduced in ESLint 0.16.0.

该规则是在ESLint 0.16.0 中被引入的。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-dupe-args.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-dupe-args.md)
