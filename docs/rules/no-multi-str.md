---
title: Rule no-multi-str
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow Multiline Strings (no-multi-str)

# 禁止多行字符串 (no-multi-str)

It's possible to create multiline strings in JavaScript by using a slash before a newline, such as:

在JavaScript中，在新行前面使用斜线可以创建多行字符串，例如：

```js
var x = "Line 1 \
         Line 2";
```

Some consider this to be a bad practice as it was an undocumented feature of JavaScript that was only formalized later.

有些人认为这是一个不好的实践，正如后来序列化之后，他是JavaScript中一个无法证实的使用。

## Rule Details

This rule is aimed at preventing the use of multiline strings.

此规则目的在于防止多行字符串的使用：

The following generates a warning:

如下操作将生成警告：

```js
/*eslint no-multi-str: 2*/ var x = "Line 1 \
         Line 2";
```

The following does not generate a warning:

如下不会生成警告：

```js
/*eslint no-multi-str: 2*/

var x = "Line 1\n" +
        "Line 2";
```



## Further Reading

* [Bad escapement of EOL](http://jslinterrors.com/bad-escapement-of-eol-use-option-multistr-if-needed/)

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-multi-str.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-multi-str.md)
