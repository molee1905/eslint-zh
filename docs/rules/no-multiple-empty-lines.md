---
title: Rule no-multiple-empty-lines
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallows multiple blank lines (no-multiple-empty-lines)

# 不允许多重空行 (no-multiple-empty-lines)

Some developers prefer to have multiple blank lines removed, while others feel that it helps improve readability. Whitespace is useful for separating logical sections of code, but excess whitespace takes up more of the screen.

一些开发者喜欢删除多重空行，然而其他人认为多重空行可以提高可读性。空白对于分离代码代码段逻辑是有帮助的，但过量的空白会占用更多的屏幕。

## Rule Details

This rule aims to reduce the scrolling required when reading through your code. It will warn when the maximum amount of empty lines has been exceeded.

该规则目的在于，当你读代码时，减少滚动。当超过最大空行数，该规则将发出警告。

### Options

The second argument can be used to configure this rule:

第二个参数被用来配置该规则：

* `max` sets the maximum number of consecutive blank lines.
* `max` 设置连续的空行的最大数量。
* `maxEOF` can be used to set a different number for the end of file. The last
  blank lines will then be treated differently. If omitted, the `max` option is
  applied everywhere.
* `maxEOF` 用来设置文件末尾空行数。最后的空行将被区分对待。如果省略，`max`选项被应用到任何地方。

For example, this sets the rule as an error (code is 2) with a maximum
tolerated blank lines of 2 (for the whole file):

例如：设置规则为错误级别，最大可允许的空行数为2(整个文件)：

```json
"no-multiple-empty-lines": [2, {"max": 2}]
```

While this tolerates three consecutive blank lines within the file, but only
one at the end:

在一个文件中当忽略耽搁连续的空行，但行尾保留一行空行，如下设置：

```json
"no-multiple-empty-lines": [2, {"max": 3, "maxEOF": 1}]
```

### Examples

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-multiple-empty-lines: [2, {max: 2}]*/

var foo = 5;


                  /*error Multiple blank lines not allowed.*/
var bar = 3;

```

```js
/*eslint no-multiple-empty-lines: [2, {max: 2, maxEOF: 1}]*/

var foo = 5;

                  /*error Too many blank lines at the end of file.*/
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-multiple-empty-lines: [2, {max: 2}]*/

var foo = 5;

var bar = 3;
```

```js
/*eslint no-multiple-empty-lines: [2, {max: 4}]*/

var foo = 5;




var bar = 3;
```

```js
/*eslint no-multiple-empty-lines: [2, {max: 2}]*/

var foo = 5;
// extra line
```

```js
/*eslint no-multiple-empty-lines: [2, {max: 2, maxEOF: 10}]*/

var foo = 5;

// 10 extra lines
```

## When Not To Use It

If you do not care about extra blank lines, turn this off.

如果你不关心额外的空行，关闭此规则即可。

## Version

This rule was introduced in ESLint 0.9.0.

该规则在ESLint 0.9.0 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-multiple-empty-lines.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-multiple-empty-lines.md)
