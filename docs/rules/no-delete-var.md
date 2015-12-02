---
title: Rule no-delete-var
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Variables Deletion (no-delete-var)
# 不允许删除变量 (no-delete-var)

This rule prevents the use of `delete` operator on variables:

此规则阻止在变量上使用 `delete` 操作。

```js
/*eslint no-delete-var: 2*/

var x;
delete x;  /*error Variables should not be deleted.*/
```

The delete operator will only delete the properties of objects. It cannot "delete" variables or anything else. Using them on variables might lead to unexpected behavior.

"delete" 操作仅仅能删除对象属性。它不能 "delete" 变量或者其他。对变量使用 "delete" 操作会导致意外情况。
## Further Reading

* [Only properties should be deleted](http://jslinterrors.com/only-properties-should-be-deleted/)

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9 中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-delete-var.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-delete-var.md)
