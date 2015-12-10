---
title: Rule no-trailing-spaces
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow trailing spaces at the end of lines (no-trailing-spaces)

# 禁用行尾空格 (no-trailing-spaces)

Sometimes in the course of editing files, you can end up with extra whitespace at the end of lines. These whitespace differences can be picked up by source control systems and flagged as diffs, causing frustration for developers. While this extra whitespace causes no functional issues, many code conventions require that trailing spaces be removed before checkin.

有时在编辑文件的过程中，你可以在行的末尾以额外的空格作为结束。这些空格差异可以被源码控制系统识别出并被标记为差异，给开发人员带来挫败感。虽然这种额外的空格并不会造成功能性的问题，许多编码规范要求在checkin之前删除尾部空格。

**Fixable:** This rule is automatically fixable using the `--fix` flag on the command line.

**Fixable:** 该规则可以通过`--fix`命令行进行自动修复。

## Rule Details

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-trailing-spaces: 2*/

// spaces, tabs and unicode whitespaces
// are not allowed at the end of lines
var foo = 0;//•••••  /*error Trailing spaces not allowed.*/
var baz = 5;//••     /*error Trailing spaces not allowed.*/
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-trailing-spaces: 2*/

var foo = 0;

var baz = 5;
```

### Options

There is one option for this rule, `skipBlankLines`. When set to true, the rule will not flag any lines that are made up purely of whitespace. In short, if a line is zero-length after being trimmed of whitespace, then the rule will not flag that line when `skipBlankLines` is enabled.

该规则有一个可选项， `skipBlankLines`。当设置为true时，该规则将不会标记任何空行。简而言之，如果删除空格后，某一行的长度为0，那么在`skipBlankLines` 启用的情况下，该规将不会标记该行。

You can enable this option in your config like this:

你可以在你的配置中像下面这样启用该可选项：

```json
{
    "no-trailing-spaces": [2, { "skipBlankLines": true }]
}
```

With this option enabled, The following patterns are not considered problems:

当该选项启用后，以下模式被认为是没有问题的：

```js
/*eslint no-trailing-spaces: [2, { "skipBlankLines": true }]*/

var foo = 0;
//••••
var baz = 5;
```

## Version

This rule was introduced in ESLint 0.7.1.

该规则在ESLint 0.7.1 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-trailing-spaces.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-trailing-spaces.md)
