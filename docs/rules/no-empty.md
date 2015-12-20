---
title: Rule no-empty
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Empty Block Statements (no-empty)

# 禁止空块语句

Empty statements usually occur due to refactoring that wasn't completed, such as:

空语句通常由于重构没有完成造成的,如:

```js
if (foo) {
}
```

Empty block statements such as this are usually an indicator of an error, or at the very least, an indicator that some refactoring is likely needed.

空块语句通常是一个错误指标，或者是标示可能需要重构。

## Rule Details

This rule is aimed at eliminating empty block statements. While not technically an error, empty block statements can be a source of confusion when reading code.
A block will not be considered a warning if it contains a comment line.

该规则旨在消除空块语句。虽然不是技术错误,但空语句是阅读代码时困惑的根源。
如果空块语句包含注释行，则不会被认为是一个警告

The following patterns are considered problems:

下面是有问题的代码：

```js
/*eslint no-empty: 2*/

if (foo) {         /*error Empty block statement.*/
}

while (foo) {      /*error Empty block statement.*/
}

switch(foo) {      /*error Empty switch statement.*/
}

try {
    doSomething();
} catch(ex) {      /*error Empty block statement.*/

} finally {        /*error Empty block statement.*/

}
```

The following patterns are not considered problems:

下面是正确的代码：

```js
/*eslint no-empty: 2*/

if (foo) {
    // empty
}

while (foo) {
    // test
}

try {
    doSomething();
} catch (ex) {
    // Do nothing
}

try {
    doSomething();
} finally {
    // Do nothing
}
```

Since you must always have at least a `catch` or a `finally` block for any `try`, it is common to have empty statements when execution should continue regardless of error.

由于使用 `try` 时必须至少有一个 `catch` 或 `finally`，通常该空语句用于忽略出现的错误。

## When Not To Use It

If you intentionally use empty statements then you can disable this rule.

如果你故意使用空语句，你可以禁用该规则。

## Version

This rule was introduced in ESLint 0.0.2.

该规则是在ESLint 0.0.2 中被引入的。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-empty.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-empty.md)
