---
title: Rule no-mixed-requires
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Disallow Mixed Requires (no-mixed-requires)

# 不允许混淆Requires (no-mixed-requires)

In the Node.JS community it is often customary to separate the `require`d modules from other variable declarations, sometimes also grouping them by their type. This rule helps you enforce this convention.

在Node.JS社区，这是常事，区别被引入的模块和变量申明，有时候也按类型分组。此规则帮组你强记这个约定。

## Rule Details

When this rule is enabled, all `var` statements must satisfy the following conditions:

当这个规则启动，所有的`var`语句必须满足以下条件：

* either none or all variable declarations must be require declarations
* all require declarations must be of the same type (optional)

* 无或所有的变量申明必须是引入模块的声明。
* 所有的引入模块的必须是同一类型（可选）。

### Options

This rule comes with option called `grouping` which is turned off by default. You can set it in your `eslint.json`:

此规则带有`分组`配置项，默认是关闭的。你可以在你的`eslint.js`中设置。

```json
{
    "no-mixed-requires": [1, {"grouping": true}]
}
```

The second way to configure this rule is with boolean (This way of setting is deprecated).

配置此规则的第二种方式是用布尔值（不建议使用这种设置方式）

```json
{
    "no-mixed-requires": [1, true]
}
```

If enabled, violations will be reported whenever a single `var` statement contains require declarations of mixed types (see the examples below).

如果启用规则，一个单独的`var`语句包含混淆类型的模块引入声明，将会报错。

### Nomenclature

This rule distinguishes between six kinds of variable declaration types:

此规在六中变量申明类型中区分：

* `core`: declaration of a required [core module][1]
* `file`: declaration of a required [file module][2]
* `module`: declaration of a required module from the [node_modules folder][3]
* `computed`: declaration of a required module whose type could not be determined (either because it is computed or because require was called without an argument)
* `uninitialized`: a declaration that is not initialized
* `other`: any other kind of declaration


* `core`：[核心模块][1]引入的申明
* `file`：[文件模块][2]引入的申明
* `module`：[node模块][3]引入的申明
*  `computed`：不能确定模块引入的申明
*  `uninitialized`：未初始化模块的申明
*  `other`：其他形式的声明

In this document, the first four types are summed up under the term *require declaration*.

在这个文档中，前四个类型总结了必须申明。

#### Example

```javascript
var fs = require('fs'),        // "core"     \
    async = require('async'),  // "module"   |- these are "require declaration"s
    foo = require('./foo'),    // "file"     |
    bar = require(getName()),  // "computed" /
    baz = 42,                  // "other"
    bam;                       // "uninitialized"
```

## Examples

The following patterns are not considered problems:

以下模式被认为是没问题的：

```js
/*eslint no-mixed-requires: 2*/

// only require declarations (grouping off)
var eventEmitter = require('events').EventEmitter,
    myUtils = require('./utils'),
    util = require('util'),
    bar = require(getBarModuleName());

// only non-require declarations
var foo = 42,
    bar = 'baz';

// always valid regardless of grouping because all declarations are of the same type
var foo = require('foo' + VERSION),
    bar = require(getBarModuleName()),
    baz = require();
```

The following patterns are considered problems:

以下模式被认为有问题的：

```js
/*eslint no-mixed-requires: 2*/

var fs = require('fs'), /*error Do not mix 'require' and other declarations.*/
    i = 0;
```

The following patterns are considered problems when grouping is turned on:

当分组关闭时，以下模式被认为有问题的:

```js
/*eslint no-mixed-requires: [2, {"grouping": true}]*/

// invalid because of mixed types "core" and "file"
var fs = require('fs'),                /*error Do not mix core, module, file and computed requires.*/
    async = require('async');

// invalid because of mixed types "file" and "unknown"
var foo = require('foo'),              /*error Do not mix core, module, file and computed requires.*/
    bar = require(getBarModuleName());
```


## When Not To Use It

Internally, the list of core modules is retrieved via `require("repl")._builtinLibs`. If you use different versions of Node.JS for ESLint and your application, the list of core modules for each version may be different.
The above mentioned `_builtinLibs` property became available in 0.8, for earlier versions a hardcoded list of module names is used as a fallback. If your version of Node is older than 0.6 that list may be inaccurate.

内部的核心模块列表查找方式是`require("repl")._builtinLibs`。如果在你的ESlint和应用中使用不同的Node.JS版本，每个版本的核心模块可能不同。

If you use a pattern such as [UMD][4] where the `require`d modules are not loaded in variable declarations, this rule will obviously do nothing for you.

如果你使用[UMD][4]模式，当所需的模块没有加载在变量申明中，此规则不会为你做什么。

The implementation is not aware of any local functions with the name `require` that may shadow Node's global `require`.

应用不会意识到任何本地`require`方法可能会覆盖Node的全局`require`方法。

[1]: http://nodejs.org/api/modules.html#modules_core_modules
[2]: http://nodejs.org/api/modules.html#modules_file_modules
[3]: http://nodejs.org/api/modules.html#modules_loading_from_node_modules_folders
[4]: https://github.com/umdjs/umd

## Version

This rule was introduced in ESLint 0.0.9.

此规则在ESLint 0.0.9中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/no-mixed-requires.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/no-mixed-requires.md)
