---
title: Rule no-case-declarations
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow lexical declarations in case/default clauses (no-case-declarations)

# 不允许在case或default子句中使用词法声明 (no-case-declarations)

This rule disallows lexical declarations (`let`, `const`, `function` and `class`)
in `case`/`default` clauses. The reason is that the lexical declaration is visible
in the entire switch block but it only gets initialized when it is assigned, which
will only happen if the case where it is defined is reached.

此规则禁止在`case`/`default`分句中声明语法（`let`, `const`, `function` and `class`）。原因是语法声明在整个switch块中是可见的，但是如果能达到被定义的位置时才能被初始化。

```js
switch (foo) {
    case 1:
        let x = 1;
        break;
    case 2:
        const y = 2;
        break;
    case 3:
        function f() {}
        break;
    default:
        class C {}
}
```

To ensure that the lexical declaration only applies to the current case clause
wrap your clauses in blocks.

为了确保语法声明只适用于当前情况，将你的声明进行包裹。

```js
switch (foo) {
    case 1: {
        let x = 1;
        break;
    }
    case 2: {
        const y = 2;
        break;
    }
    case 3: {
        function f() {}
        break;
    }
    default: {
        class C {}
    }
}
```

## Rule Details

This rule aims to prevent access to uninitialized lexical bindings as well as accessing hoisted functions across case clauses.

此规则目的在于，防止访问未初始化的词语以及跨case分支访问悬挂的函数。

```js
/*eslint no-case-declarations: 2*/

switch (foo) {
    case 1:
        let x = 1;  /*error Unexpected lexical declaration in case block.*/
        break;
    case 2:
        const y = 2;  /*error Unexpected lexical declaration in case block.*/
        break;
    case 3:
        function f() {}  /*error Unexpected lexical declaration in case block.*/
        break;
    default:
        class C {}  /*error Unexpected lexical declaration in case block.*/
}
```

## When Not To Use It

If you depend on fall through behavior and want access to bindings introduced in the case block.

## Related Rules

* [no-fallthrough](no-fallthrough)

## Version

This rule was introduced in ESLint 1.9.0.

该规则在ESLint 1.9.0中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-case-declarations.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-case-declarations.md)
