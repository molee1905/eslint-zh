---
title: Rule no-label-var
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Labels That Are Variables Names (no-label-var)

# 不允许标签是变量名 (no-label-var)

## Rule Details

This rule aims to create clearer code by disallowing the bad practice of creating a label that shares a name with a variable that is in scope.

此规则希望创建更清晰的代码，通过不允许同一作用域中变量名和标记名相同。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-label-var: 2*/

var x = foo;
function bar() {
x:               /*error Found identifier with same name as label.*/
  for (;;) {
    break x;
  }
}
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-label-var: 2*/

// The variable that has the same name as the label is not in scope.

function foo() {
  var q = t;
}

function bar() {
q:
  for(;;) {
    break q;
  }
}
```

## Further Reading

* ['{a}' is a statement label](http://jslinterrors.com/a-is-a-statement-label/)

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-label-var.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-label-var.md)
