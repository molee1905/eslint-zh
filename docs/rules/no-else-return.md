---
title: Rule no-else-return
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow return before else (no-else-return)

# 禁止在else前有return (no-else-return)

If an `if` block contains a `return` statement, the `else` block becomes unnecessary. Its contents can be placed outside of the block.

如果`if`区块包含 `return`语句，`else`块就成了多余的了。可以将else中内容移至块外。

```js
function foo() {
    if (x) {
        return y;
    } else {
        return z;
    }
}
```

## Rule Details

This rule is aimed at highlighting an unnecessary block of code following an `if` containing a return statement. As such, it will warn when it encounters an `else` following a chain of `if`s, all of them containing a `return` statement.

该规则目的在于，突出那些跟随在包含return的`if`语句后的冗余代码。因此，当`else`跟随在每个块都包含`return`语句的`if`链后时，该规则会发出警告。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-else-return: 2*/

function foo() {
    if (x) {
        return y;
    } else {
        return z;
    }
}

function foo() {
    if (x) {
        return y;
    } else if (z) {
        return w;
    } else {
        return t;
    }
}

function foo() {
    if (x) {
        return y;
    } else {
        var t = "foo";
    }

    return t;
}

// Two warnings for nested occurrences
function foo() {
    if (x) {
        if (y) {
            return y;
        } else {
            return x;
        }
    } else {
        return z;
    }
}
```

The follow patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-else-return: 2*/

function foo() {
    if (x) {
        return y;
    }

    return z;
}

function foo() {
    if (x) {
        return y;
    } else if (z) {
        var t = "foo";
    } else {
        return w;
    }
}

function foo() {
    if (x) {
        if (z) {
            return y;
        }
    } else {
        return z;
    }
}
```

## Version

This rule was introduced in ESLint 0.0.9.

这条规则在ESLint 0.0.9中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-else-return.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-else-return.md)
