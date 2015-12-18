---
title: Rule max-len
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Limit Maximum Length of Line (max-len)

# 限制行的最大长度 (max-len)

Very long lines of code in any language can be difficult to read. In order to aid in readability and maintainability many coders have developed a convention to limit lines of code to X number of characters (traditionally 80 characters).

代码中非常长的行在任何语言中都很难约定。为了提高可读性和可维护性，许多程序员制定了一项约定，来限制一行代码的字符数量(按照惯例80个字符)。

```js
// max-len: [1, 80, 4]; // maximum length of 80 characters
var foo = { "bar": "This is a bar.", "baz": { "qux": "This is a qux" }, "difficult": "to read" }; // too long
```


## Rule Details

This rule is aimed at increasing code readability and maintainability by enforcing a line length convention. As such it will warn on lines that exceed the configured maximum.

该规则旨在通过强制代码行的长度来提高代码的可读性和可维护性。因此，如果超过了配置的最大值，该规则将发出警告。

**Note:** This rule calculates the length of a line via code points, not characters. That means if you use a double-byte character in your code, it will count as 2 code points instead of 1, and 2 will be used to calculate line length. This is a technical limitation of JavaScript that is made easier with ES2015, and we will look to update this when ES2015 is available in Node.js.

**注意：** 该规则是通过代码点而非字符来计算行的长度的。这就意味着如果你在代码中使用了一个双字节字符，它将计为2个代码点而不是1个，这个2将被用来计算行的长度。这是Javascript的一个技术上的局限性，使得它较ES2015容易一下，当ES2015在Node.js中可用时，我们将会升级这个问题。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint max-len: [2, 80, 4]*/ // maximum length of 80 characters

var foo = { "bar": "This is a bar.", "baz": { "qux": "This is a qux" }, "difficult": "to read" }; /*error Line 3 exceeds the maximum line length of 80.*/
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint max-len: [2, 80, 4]*/ // maximum length of 80 characters

var foo = {
    "bar": "This is a bar.",
    "baz": {
        "qux": "This is a qux"
    },
    "difficult": "to read"
};
```

### Options

The `max-len` rule has two required options:

该规则有两个必须的选项：

* The total number of characters allowed on each line of code. This character count includes indentation.
* 每行代码允许的字符总数。这里的字符计数包含缩进。
* The character count to use whenever a tab character is encountered.
* 一个tab字符占用的字符数

For example, to specify a maximum line length of 80 characters with each tab counting as 4 characters, use the following configuration:

例如，指定行的最大字符数为80，每个tab记为4个字符，使用如下配置：

```json
"max-len": [2, 80, 4]
```

There are additional optional arguments to ignore comments, lines with URLs, or lines matching a regular expression.

有额外的可选参数用于忽略注释，包含URL的行或者匹配某个正则表达式的行。

```json
"max-len": [2, 80, 4, {"ignoreComments": true, "ignoreUrls": true, "ignorePattern": "^\\s*var\\s.+=\\s*require\\s*\\("}]
```

The `ignoreComments` option only ignores trailing comments and comments on their own line. For example, `function foo(/*string*/ bar) { /* ... */ }` isn't collapsed.

`ignoreComments`选项值忽略行尾注释和同一行上的注释(之前)。例如，`function foo(/*string*/ bar) { /* ... */ }` 是不折叠的。

Be aware that regular expressions can only match a single line and need to be doubly escaped when written in YAML or JSON.

请注意，正则表达式只能匹配单行，当写在YAML或JSON中时需要双重转义。


## Related Rules

* [complexity](complexity)
* [max-depth](max-depth)
* [max-nested-callbacks](max-nested-callbacks)
* [max-params](max-params)
* [max-statements](max-statements)

## Version

This rule was introduced in ESLint 0.0.9.

该规则在ESLint 0.0.9 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/max-len.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/max-len.md)
