---
title: Rule eol-last
layout: doc
translator: @molee1905
proofreader:  @ILFront-End
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Require file to end with single newline (eol-last)

# 要求文件末尾多留一空行(eol-last)

Trailing newlines in non-empty files are a common UNIX idiom. Benefits of
trailing newlines include the ability to concatenate or append to files as well
as output files to the terminal without interfering with shell prompts. This
rule enforces newlines for all non-empty programs.

非空文件的尾部留空行常见于UNIX风格中。这样的好处是，串联和追加文件，或者是把文件输出到终端时，都不受 shell 提示语句的影响。该规则强制在所有非空程序中留空行。


Prior to v0.16.0 this rule also enforced that there was only a single line at
the end of the file. If you still want this behaviour, consider enabling
[no-multiple-empty-lines](no-multiple-empty-lines) with `maxEOF` and/or
[no-trailing-spaces](no-trailing-spaces).

在 v0.16.0 之前此规则强制在文件末尾只留一行空行。如果你仍然想要这样，可以使 [no-multiple-empty-lines](no-multiple-empty-lines) 为 `maxEOF` 和/或
[no-trailing-spaces](no-trailing-spaces)。


**Fixable:** This rule is automatically fixable using the `--fix` flag on the command line.

**Fixable:** 该规则可以通过 `--fix` 命令行自行修正错误。

## Rule Details

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint eol-last: 2*/

function doSmth() {
  var foo = 2;
}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint eol-last: 2*/

function doSmth() {
  var foo = 2;
}
// spaces here
```

### Options

This rule may take one option which is either `unix` (LF) or `windows` (CRLF). When omitted `unix` is assumed.

该规则有一个可选项：`unix` (LF) 或 `windows` (CRLF)。如果省略的话，默认设置为 `unix`。

## Version

This rule was introduced in ESLint 0.7.1.

该规则在 ESLint 0.7.1 被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/eol-last.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/eol-last.md)
