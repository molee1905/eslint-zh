---
title: Rule brace-style
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Require Brace Style (brace-style)

# 大括号风格要求 (brace-style)

Brace style is closely related to [indent style](http://en.wikipedia.org/wiki/Indent_style) in programming and describes the placement of curly braces relative to their control statement and body. There are probably a dozen, if not more, brace styles in the world.

在编程过程中，大括号风格与[缩进风格](http://en.wikipedia.org/wiki/Indent_style)紧密联系,用来描述大括号相对控制语句和代码块的位置，少说也有十几种。

The *one true brace style* is one of the most common brace styles in JavaScript, in which the opening curly brace of a block is placed on the same line as its corresponding statement or declaration. For example:

在Javascript，*one true brace style*也是最常见的一种就是将大括号放在控制语句或声明语句
同一行的位置。例如：

```js
if (foo) {
  bar();
} else {
  baz();
}
```

One common variant of one true brace style is called Stroustrup, in which the `else` statements in an `if-else` construct, as well as `catch` and `finally`, must be on its own line after the preceding closing brace, as in this example:

one true brace style的一种常见的变体形式叫做Stroustrup，`if-else`中的`else`语句，连同`catch` 和 `finally`，都必须在右括号后另起一行，如下面这个例子：

```js
if (foo) {
  bar();
}
else {
  baz();
}
```

Another style is called [Allman](https://en.wikipedia.org/wiki/Indent_style#Allman_style), in which all the braces are expected to be on their own lines without any extra indentation:

另一种风格叫做[Allman](https://en.wikipedia.org/wiki/Indent_style#Allman_style)，
括号必须单独成行且没有任何缩进：

```js
if (foo)
{
  bar();
}
else
{
  baz();
}
```

While no style is considered better than the other, most developers agree that having a consistent style throughout a project is important for its long-term maintainability.

尽管没有哪种风格被认为会比另一种更好，但大多数开发者一致认可在同一项目中保持一致的风格对于长期的可维护性是很重要的。

## Rule Details

This rule is aimed at enforcing a particular brace style in JavaScript. As such, it warns whenever it sees a statement or declaration that does not adhere to the one true brace style.

该规则旨在强制在Javascript中使用特定的括号风格。因此，如果某条语句或声明没有遵守该该风格，它将发出警告。

### Options

The rule takes two options:

该规则有两个可选项：

1. A string which must be either "1tbs", "stroustrup" or "allman". The default is "1tbs".

1. 一个字符串，必须是"1tbs"、"stroustrup"或"allman"。默认值是"1tbs"。

2. An object that further controls the behaviour of this rule. Currently, the only available parameter is `allowSingleLine`, which indicates whether start and end braces may be on the same line.

2. 一个对象，进一步限制该规则的行为。目前，唯一可用的参数是 'allowSingleLine'，用来指示是否开始和结束大括号是否在同一行。

You can set the style in configuration like this:

你可以在配置中这样设置：

```json
"brace-style": [2, "stroustrup", { "allowSingleLine": true }]
```

#### "1tbs"

This is the default setting for this rule and enforces one true brace style. While using this setting, the following patterns are considered problems:

该选项是此默认设置，强制使用one true brace style。当使用此设置时，以下模式被认为是有问题的：


```js
/*eslint brace-style: 2*/
function foo()       /*error Opening curly brace does not appear on the same line as controlling statement.*/
{
  return true;
}

if (foo)             /*error Opening curly brace does not appear on the same line as controlling statement.*/
{
  bar();
}

try                  /*error Opening curly brace does not appear on the same line as controlling statement.*/
{
  somethingRisky();
} catch(e)           /*error Opening curly brace does not appear on the same line as controlling statement.*/
{
  handleError();
}

if (foo) {
  bar();
}
else {              /*error Closing curly brace does not appear on the same line as the subsequent block.*/
  baz();
}
```

The following patterns use the one true brace style and are not considered problems:

以下模式使用one true brace style，被认为是没有问题的：

```js
/*eslint brace-style: 2*/

function foo() {
  return true;
}

if (foo) {
  bar();
}

if (foo) {
  bar();
} else {
  baz();
}

try {
  somethingRisky();
} catch(e) {
  handleError();
}

// when there are no braces, there are no problems
if (foo) bar();
else if (baz) boom();
```

With one-line form enabled, the following is also valid:

one-line 形式启用的情况下，以下模式也是有效的：

```js
/*eslint brace-style: [2, "1tbs", { "allowSingleLine": true }]*/

function nop() { return; }

if (foo) { bar(); }

if (foo) { bar(); } else { baz(); }

try { somethingRisky(); } catch(e) { handleError(); }
```

#### "stroustrup"

This enforces Stroustrup style. While using this setting, the following patterns are considered problems:

该选项强制使用Stroustrup风格。当使用此设置时，以下模式被认为是有问题的：

```js
/*eslint brace-style: [2, "stroustrup"]*/

function foo()        /*error Opening curly brace does not appear on the same line as controlling statement.*/
{
  return true;
}

if (foo)              /*error Opening curly brace does not appear on the same line as controlling statement.*/
{
  bar();
}

try                   /*error Opening curly brace does not appear on the same line as controlling statement.*/
{
  somethingRisky();
} catch(e)            /*error Opening curly brace does not appear on the same line as controlling statement.*/ /*error Closing curly brace appears on the same line as the subsequent block.*/
{
  handleError();
}

if (foo) {
  bar();
} else {              /*error Closing curly brace appears on the same line as the subsequent block.*/
  baz();
}
```

The following patterns use the Stroustrup style and are not considered problems:

以下模式使用Stroustrup风格，被认为是没有问题的：

```js
/*eslint brace-style: [2, "stroustrup"]*/

function foo() {
  return true;
}

if (foo) {
  bar();
}

if (foo) {
  bar();
}
else {
  baz();
}

try {
  somethingRisky();
}
catch(e) {
  handleError();
}

// when there are no braces, there are no problems
if (foo) bar();
else if (baz) boom();
```

With one-line form enabled, the following is also valid:

one-line 形式启用的情况下，以下模式也是有效的：

```js
/*eslint brace-style: [2, "stroustrup", { "allowSingleLine": true }]*/

function nop() { return; }

if (foo) { bar(); }

if (foo) { bar(); }
else { baz(); }

try { somethingRisky(); }
catch(e) { handleError(); }
```

#### "allman"


This enforces Allman style. While using this setting, the following patterns are considered problems:

该选项强制使用Allman风格。当使用此设置时，以下模式被认为是有问题的：

```js
/*eslint brace-style: [2, "allman"]*/

function foo() {     /*error Opening curly brace appears on the same line as controlling statement.*/
  return true;
}

if (foo)
{
  bar(); }           /*error Closing curly brace should be on the same line as opening curly brace or on the line after the previous block.*/

try
{
  somethingRisky();
} catch(e)           /*error Closing curly brace appears on the same line as the subsequent block.*/
{
  handleError();
}

if (foo) {           /*error Opening curly brace appears on the same line as controlling statement.*/ /*error Opening curly brace appears on the same line as controlling statement.*/
  bar();
} else {             /*error Closing curly brace appears on the same line as the subsequent block.*/
  baz();
}
```

The following patterns use the Allman style and are not considered problems:

以下模式使用Allman风格，被认为是没有问题的：

```js
/*eslint brace-style: [2, "allman"]*/

function foo()
{
  return true;
}

if (foo)
{
  bar();
}

if (foo)
{
  bar();
}
else
{
  baz();
}

try
{
  somethingRisky();
}
catch(e)
{
  handleError();
}

// when there are no braces, there are no problems
if (foo) bar();
else if (baz) boom();
```

With one-line form enabled, the following is also valid:

one-line 形式启用的情况下，以下模式也是有效的：

```js
/*eslint brace-style: [2, "allman", { "allowSingleLine": true }]*/

function nop() { return; }

if (foo) { bar(); }

if (foo) { bar(); }
else { baz(); }

try { somethingRisky(); }
catch(e) { handleError(); }
```

## When Not To Use It

If your project will not be using the one true brace style, turn this rule off.

如果你的项目不使用one true brace style，关闭此规则即可。

## Further Reading

* [Indent style](http://en.wikipedia.org/wiki/Indent_style)

## Version

This rule was introduced in ESLint 0.0.7.

该规则实在ESLint 0.0.7中被引进的。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/brace-style.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/brace-style.md)
