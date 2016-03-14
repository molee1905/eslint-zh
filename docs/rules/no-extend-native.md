---
title: Rule no-extend-native
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow Extending of Native Objects (no-extend-native)

# 禁止扩展原生对象 (no-extend-native)

In JavaScript, you can extend any object, including builtin or "native" objects. Sometimes people change the behavior of these native objects in ways that break the assumptions made about them in other parts of the code.

在JavaScript中，你可以扩展任何对象，包括内置或者"原生"对象。有时人们改变这些本地对象的行为，以这种方式打破在其他代码中关于它们所做的假设。

For example here we are overriding a builtin method that will then affect all Objects, even other builtins.

例如我们重写了一个内建方法，而所有的对象都会受其影响，甚至是其他内建对象。

```js
// seems harmless
Object.prototype.extra = 55;

// loop through some userIds
var users = {
    "123": "Stan",
    "456": "David"
};

// not what you'd expect
for (var id in users) {
    console.log(id); // "123", "456", "extra"
}
```

A common suggestion to avoid this problem would be to wrap the inside of the `for` loop with `users.hasOwnProperty(id)`. However, if this rule is strictly enforced throughout your codebase you won't need to take that step.

避免这个问题的一个常见建议是使用`users.hasOwnProperty(id)`包裹`for`循环里面的代码。然而，如果此规则严格执行你的基础代码你不用做以上处理。

## Rule Details

Disallows directly modifying the prototype of builtin objects by looking for the following styles:

禁止直接修改内建对象的属性，通过寻找以下模式：

* `Object.prototype.a = "a";`
* `Object.defineProperty(Array.prototype, "times", {value: 999});`

It *does not* check for any of the following less obvious approaches:

它*不会*检查以下任何一个不太明显的方法。

* `var x = Object; x.prototype.thing = a;`
* `eval("Array.prototype.forEach = 'muhahaha'");`
* `with(Array) { prototype.thing = 'thing'; };`
* `window.Function.prototype.bind = 'tight';`

## Options

This rule accepts an `exceptions` option, which can be used to specify a list of builtins for which extensions will be allowed:

此规则接受一个`exceptions`选项，可以用来指定允许扩展的内建列表。

```json
{
    "rules": {
        "no-extend-native": [2, {"exceptions": ["Object"]}]
    }
}
```

## When Not To Use It

You may want to disable this rule when working with polyfills that try to patch older versions of JavaScript with the latest spec, such as those that might `Function.prototype.bind` or `Array.prototype.forEach` in a future-friendly way.

你可能想要禁用此规则当处理polyfills试图使用最新规范修补旧版的JavaScript,比如那些将来可能更加友好的`Function.prototype.bind`或者`Array.prototype.forEach`。

## Related Rules

* [no-native-reassign](no-native-reassign)

## Version

This rule was introduced in ESLint 0.1.4.

此规则在ESLint 0.1.4中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-extend-native.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-extend-native.md)
