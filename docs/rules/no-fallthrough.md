---
title: Rule no-fallthrough
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Case Statement Fallthrough (no-fallthrough)

#禁止case向下通过

The `switch` statement in JavaScript is one of the more error-prone constructs of the language thanks in part to the ability to "fall through" from one `case` to the next. For example:

在JavaScript中，`switch`语句是最容易出错的语言结构之一，一部分要归功于通过一个`case`到下一个的能力。比如：

```js
switch(foo) {
    case 1:
        doSomething();

    case 2:
        doSomethingElse();
}
```

In this example, if `foo` is `1`,then execution will flow through both cases, as the first falls through to the second. You can prevent this by using `break`, as in this example:

在这个例子中，如果`foo`值为`1`，则会执行所有case分支，因为通过第一个分支走向第二个分支。你可以使用`break`阻止这种情况，例如以下例子：

```js
switch(foo) {
    case 1:
        doSomething();
        break;

    case 2:
        doSomethingElse();
}
```

That works fine when you don't want a fallthrough, but what if the fallthrough is intentional, there is no way to indicate that in the language. It's considered a best practice to always indicate when a fallthrough is intentional using a comment:

当你不想fallthrough,以上运行正常，但是如果fallthrough行为是故意的，在语言中是没有办法表明的。当fallthrough是故意为之时，总是使用注释给出提示，被认为是一个很好的实践。

```js
switch(foo) {
    case 1:
        doSomething();
        // falls through

    case 2:
        doSomethingElse();
}

switch(foo) {
    case 1:
        doSomething();
        // fall through

    case 2:
        doSomethingElse();
}

switch(foo) {
    case 1:
        doSomething();
        // fallsthrough

    case 2:
        doSomethingElse();
}
```

In this example, there is no confusion as to the expected behavior. It is clear that the first case is meant to fall through to the second case.

在这个例子中，没有混淆预期的结果。第一个case走向第二个case是很清晰的行为。

## Rule Details

This rule is aimed at eliminating unintentional fallthrough of one case to the other. As such, it flags and fallthrough scenarios that are not marked by a comment.

此规则目的在于消除一个case走向另一个的意外情况。因此，它会标记并且流经那个没有被注释的情况。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-fallthrough: 2*/

switch(foo) {
    case 1:            /*error Expected a "break" statement before "case".*/
        doSomething();

    case 2:
        doSomething();
}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-fallthrough: 2*/

switch(foo) {
    case 1:
        doSomething();
        break;

    case 2:
        doSomething();
}

function bar(foo) {
    switch(foo) {
        case 1:
            doSomething();
            return;

        case 2:
            doSomething();
    }
}

switch(foo) {
    case 1:
        doSomething();
        throw new Error("Boo!");

    case 2:
        doSomething();
}

switch(foo) {
    case 1:
    case 2:
        doSomething();
}

switch(foo) {
    case 1:
        doSomething();
        // falls through

    case 2:
        doSomething();
}
```

Note that the last `case` statement in these examples does not cause a warning because there is nothing to fall through into.

注意下，在上面的例子中，最后的`case`语句，不会引起警告，因为没有下文需要到达。

## When Not To Use It

If you don't want to enforce that each `case` statement should end with a `throw`, `return`, `break`, or comment, then you can safely turn this rule off.

如果你不想强制每个`case`语句中都要有`throw`, `return`, `break`, 或者注释，你可以放心的关闭此规则。

## Related Rules

* [default-case](default-case)

## Version

This rule was introduced in ESLint 0.0.7.

此规则在ESLint 0.0.7中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-fallthrough.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-fallthrough.md)
