---
title: Rule max-statements
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Limit Maximum Number of Statements (max-statements)

# 限制语句的最大数量 (max-statements)

The `max-statements` rule allows you to specify the maximum number of statements allowed in a function.

该规则允许你指定一个函数中允许的语句的最大数值。

```js
function foo() {
  var bar = 1; // one statement
  var baz = 2; // two statements
  var qux = 3; // three statements
}
```

## Rule Details

This rule allows you to configure the maximum number of statements allowed in a function.  The default is 10.

该规则允许配置函数中允许的最大语句数量。默认为10。

The following patterns are considered problems:

以下模式被认为是没有问题的：

```js
/*eslint max-statements: [2, 2]*/  // Maximum of 2 statements.
function foo() { /*error This function has too many statements (3). Maximum allowed is 2.*/
  var bar = 1;
  var baz = 2;

  var qux = 3; // Too many.
}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint max-statements: [2, 2]*/  // Maximum of 2 statements.
function foo() {
  var bar = 1;
  return function () {

    // The number of statements in the inner function does not count toward the
    // statement maximum.

    return 42;
  };
}
```

## Related Rules

* [complexity](complexity)
* [max-depth](max-depth)
* [max-len](max-len)
* [max-nested-callbacks](max-nested-callbacks)
* [max-params](max-params)

## Version

This rule was introduced in ESLint 0.0.9.

该规则在ESLint 0.0.9 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/max-statements.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/max-statements.md)
