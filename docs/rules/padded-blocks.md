---
title: Rule padded-blocks
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Enforce padding within blocks (padded-blocks)

# 强制块内填充 (padded-blocks)

Some style guides require block statements to start and end with blank lines. The goal is
to improve readability by visually separating the block content and the surrounding code.

一些风格指南要求块语句以空行开始并且以空行结束。目标是通过视觉上的块内容和周围代码的分离来提高可读性。

```js
if (a) {

    b();

}
```

Since it's good to have a consistent code style, you should either always write
padded blocks or never do it.

有一个统一的代码风格是非常有好处的，你应总是写填充的块或永远不这么做。

## Rule Details

This rule enforces consistent padding within blocks.

该规则强制块内填充的一致性。

This rule takes one argument. If it is `"always"` then blocks must start **and** end with a blank line. If `"never"`
then all blocks should never start **or** end with a blank line. The default is `"always"`.

该规则只有一个参数。如果是`"always"`，块语句必须以空行开始**和**结束。如果为`"never"`，所有的块语句应该永远不以空行开始**或**结束。默认为`"always"`。

The following patterns are considered problems when set to `"always"`:

当设置为`"always"`时，以下模式被认为是有问题的：

```js
/*eslint padded-blocks: [2, "always"]*/

if (a) {         /*error Block must be padded by blank lines.*/
    b();
}                /*error Block must be padded by blank lines.*/

if (a) { b(); }  /*error Block must be padded by blank lines.*/

if (a)
{                /*error Block must be padded by blank lines.*/
    b();
}                /*error Block must be padded by blank lines.*/

if (a) {

    b();
}                /*error Block must be padded by blank lines.*/

if (a) {         /*error Block must be padded by blank lines.*/
    b();

}

if (a) {         /*error Block must be padded by blank lines.*/
    // comment
    b();

}
```

The following patterns are not considered problems when set to `"always"`:

当设置为`"always"`时，以下模式被认为是没有问题的：

```js
/*eslint padded-blocks: [2, "always"]*/

if (a) {

    b();

}

if (a)
{

    b();

}

if (a) {

    // comment
    b();

}
```

The following patterns are considered problems when set to `"never"`:

当设置为`"never"`时，以下模式被认为是有问题的：

```js
/*eslint padded-blocks: [2, "never"]*/

if (a) {  /*error Block must not be padded by blank lines.*/

    b();

}        /*error Block must not be padded by blank lines.*/

if (a)
{        /*error Block must not be padded by blank lines.*/

    b();

}        /*error Block must not be padded by blank lines.*/

if (a) { /*error Block must not be padded by blank lines.*/

    b();
}

if (a) {
    b();

}        /*error Block must not be padded by blank lines.*/
```

The following patterns are not considered problems when set to `"never"`:

当设置为`"never"`时，以下模式被认为是没有问题的：

```js
/*eslint padded-blocks: [2, "never"]*/

if (a) {
    b();
}

if (a)
{
    b();
}
```

## When Not To Use It

You can turn this rule off if you are not concerned with the consistency of padding within blocks.

如果你并不关心块内填充的一致性，你可以关闭此规则。

## Version

This rule was introduced in ESLint 0.9.0.

该规则在ESLint 0.9.0 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/padded-blocks.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/padded-blocks.md)
