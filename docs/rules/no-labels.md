---
title: Rule no-labels
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Disallow Labeled Statements (no-labels)

# 禁止标签语句 (no-labels)

Labeled statements in JavaScript are used in conjunction with `break` and `continue` to control flow around multiple loops. For example:

JavaScript中的标签语句用来连同`break` 和 `continue` 控制多个绕流循环。例如：

```js
outer:
    while (true) {

        while (true) {
            break outer;
        }
    }
```

The `break outer` statement ensures that this code will not result in an infinite loop because control is returned to the next statement after the `outer` label was applied. If this statement was changed to be just `break`, control would flow back to the outer `while` statement and an infinite loop would result.

`break outer`语句确保代码不会无限循环,因为在被引用的`outer`标签之后控制被返回至下一个语句。如果这个语句的改变只为`break`，控制会回流到外部的`while`语句并导致无限循环。

While convenient in some cases, labels tend to be used only rarely and are frowned upon by some as a remedial form of flow control that is more error prone and harder to understand.

然而方便在某些情况下，标签往往只有很少使用，而被一些人视为是更多的错误倾向和难以理解的流量控制补救形式会被唾弃。

## Rule Details

This rule aims to eliminate the use of labeled statements in JavaScript. It will warn whenever a labeled statement is encountered and whenever `break` or `continue` are used with a label.

此规则目的在于消除JavaScript中标签的使用。它会给出警告每当遇到一个标签语句和`break` 或者 `continue` 在标签中被使用时。

The following patterns are considered problems:

以下模式被认为是有问题的：

```js
/*eslint no-labels: 2*/

label:
    while(true) {
        // ...
    }

label:
    while(true) {
        break label;
    }

label:
    while(true) {
        continue label;
    }

label:
    switch (a) {
    case 0:
        break label;
    }

label:
    {
        break label;
    }

label:
    if (a) {
        break label;
    }
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint no-labels: 2*/

var f = {
    label: "foo"
};

while (true) {
    break;
}

while (true) {
    continue;
}
```

## Options

```json
{
    "no-labels": [2, {"allowLoop": false, "allowSwitch": false}]
}
```

* `"allowLoop"` (`boolean`, default is `false`) - If this option was set `true`, this rule ignores labels which are sticking to loop statements.
* `"allowSwitch"` (`boolean`, default is `false`) - If this option was set `true`, this rule ignores labels which are sticking to switch statements.

Actually labeled statements in JavaScript can be used with other than loop and switch statements.
However, this way is ultra rare, not well-known, so this would be confusing developers.

Those options allow us to use labels only with loop or switch statements.

The following patterns are considered problems when configured `{"allowLoop": true, "allowSwitch": true}`:

```js
label:
    {
        break label;
    }

label:
    if (a) {
        break label;
    }
```

The following patterns are not considered problems when configured `{"allowLoop": true, "allowSwitch": true}`:

```js
label:
    while (true) {
        break label;
    }

label:
    switch (a) {
        case 0:
            break label;
    }
```

## When Not To Use It

If you need to use labeled statements everywhere, then you can safely disable this rule.

如果你需要在任何地方都使用标签语句，你可以安全的禁用此规则。

## Related Rules

* [no-extra-label](./no-extra-label)
* [no-label-var](./no-label-var)
* [no-unused-labels](./no-unused-labels)

## Version

This rule was introduced in ESLint 0.4.0.

此规则在ESLint 0.4.0中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-labels.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-labels.md)
