---
title: Rule block-spacing
layout: doc
translator: @molee1905
proofreader: @ILFront-End
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow or enforce spaces inside of single line blocks. (block-spacing)

# 禁止或强制在单行代码块中使用空格。 (block-spacing)

This rule is for spacing style within single line blocks.

该规则是关于在单行代码快中代码间距风格的。

**Fixable:** This rule is automatically fixable using the `--fix` flag on the command line.

**Fixable:** 该规则可以通过在命令行中使用 `--fix` 命令进行自动修复。

## Rule Details

This rule is aimed to flag usage of spacing inside of blocks.

该规则旨在标示代码块中空格的用法。

This rule has a option, its value is `"always"` or `"never"`.

该规则有一个可选项, 值为 `"always"` 或 `"never"`。

- `"always"` (by default) enforces one or more spaces.

- `"always"` (默认) 强制使用一个或多个空格。

- `"never"` disallows space(s).

- `"never"` 禁用空格。


### always

```json
{
  "block-spacing": [2, "always"]
}
```

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint block-spacing: 2*/
function foo() {return true;} /*error Requires a space after "{".*/ /*error Requires a space before "}".*/
if (foo) { bar = 0;}          /*error Requires a space before "}".*/
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint block-spacing: 2*/

function foo() { return true; }
if (foo) { bar = 0; }
```

### never

```json
{
  "block-spacing": [2, "never"]
}
```

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint block-spacing: [2, "never"]*/

function foo() { return true; } /*error Unexpected space(s) after "{".*/ /*error Unexpected space(s) before "}".*/
if (foo) { bar = 0;}            /*error Unexpected space(s) after "{".*/
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint block-spacing: [2, "never"]*/

function foo() {return true;}
if (foo) {bar = 0;}
```

## When Not to Use It

If you don't want to be notified about spacing style inside of blocks, you can safely disable this rule.

如果你不想收到有关代码块间距问题的通知，你完全可以禁用此规则。


## Version

This rule was introduced in ESLint 1.2.0.

该规则在 ESLint 1.2.0 被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/block-spacing.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/block-spacing.md)
