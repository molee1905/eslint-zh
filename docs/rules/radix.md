---
title: Rule radix
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Require Radix Parameter (radix)
#需要基数参数(radix)

When using the `parseInt()` function it is common to omit the second argument, the radix, and let the function try to determine from the first argument what type of number it is. By default, `parseInt()` will autodetect decimal and hexadecimal (via `0x` prefix). Prior to ECMAScript 5, `parseInt()` also autodetected octal literals, which caused problems because many developers assumed a leading `0` would be ignored.

使用`parseInt()`函数时，通常省略第二个参数，基数，并让函数尝试从第一个参数确定它是什么类型的数字。默认情况下，`parseInt()` 将自动检测十进制和十六进制 (通过`0x`前缀)。ECMAScript 5 之前，`parseInt()`也自动探测八进制文本，这会引起问题，因为许多开发人员认为前导`0`会被忽略。

This confusion led to the suggestion that you always use the radix parameter to `parseInt()` to eliminate unintended consequences. So instead of doing this:

这种混乱，导致建议始终在`parseInt()`中使用基数参数，消除产生意想不到的后果。因此我们可以这样做:

```js
var num = parseInt("071");      // 57
```

Do this:

```js
var num = parseInt("071", 10);  // 71
```

ECMAScript 5 changed the behavior of `parseInt()` so that it no longer autodetects octal literals and instead treats them as decimal literals. However, the differences between hexadecimal and decimal interpretation of the first parameter causes many developers to continue using the radix parameter to ensure the string is interpreted in the intended way.

ECMAScript 5 更改 `parseInt()` 的行为，因此，它不再自动检测八进制文本，而是将他们视为十进制文字。然而，十六进制和十进制解释的第一个参数之间的差异会导致许多开发人员继续使用基数参数以确保字符串在按预定的方式被解释。

On the other hand, if the code is targeting only ES5-compliant environments passing the radix `10` may be redundant. In such a case you might want to disallow using such a radix.

另一方面，如果代码针对只有ES5兼容环境传递基数`10`可能是多余的。在这种情况下你可能会想要不允许使用这种基数。

## Rule Details

This rule is aimed at preventing the unintended conversion of a string to a number of a different base than intended or at preventing the redundant `10` radix if targeting modern environments only.

此规则目的在于防止一个字符串意想不到的转换成与预期不同的数字或防止多余的`10`基数,如果只针对现代环境。

## Options

There are two options for this rule:

此规则有两个选项：

* `"always"` enforces providing a radix (default)
* `"always"`强制提供一个基数（默认的）
* `"as-needed"` disallows providing the `10` radix
* `"as-needed"` 禁止提供基数`10`

Depending on your coding conventions, you can choose either option by specifying it in your configuration:

根据你代码的习惯，你可以选择指定其中一个选项在你的配置中：

```json
"radix": [2, "always"]
```

### "always"

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint radix: 2*/

var num = parseInt("071");

var num = parseInt(someValue);

var num = parseInt("071", "abc");

var num = parseInt();
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint radix: 2*/

var num = parseInt("071", 10);

var num = parseInt("071", 8);

var num = parseFloat(someValue);
```

### "as-needed"

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint radix: [2. "as-needed"] */

var num = parseInt("071", 10);

var num = parseInt("071", "abc");

var num = parseInt();
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint radix: [2. "as-needed"] */

var num = parseInt("071");

var num = parseInt("071", 8);

var num = parseFloat(someValue);
```

## When Not To Use It

If you don't want to enforce either presence or omission of the `10` radix value you can turn this rule off.

如果你不想执行存在或遗漏的`10`基数值你可以关掉这个规则。

## Further Reading

* [parseInt and radix](http://davidwalsh.name/parseint-radix)
* [Missing radix parameter](http://jslinterrors.com/missing-radix-parameter/)

## Version

This rule was introduced in ESLint 0.0.7.

此规则在ESLint 0.0.7中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/radix.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/radix.md)
