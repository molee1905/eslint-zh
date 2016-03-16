---
title: Rule strict
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Strict Mode Directives (strict)

# 严格模式 (strict)
 
A strict mode directive at the beginning of a script or function body enables strict mode semantics:

在脚本或方法体的开始位置使用严格模式指令开启严格模式语义：

```js
"use strict";
```

When used globally, as in the preceding example, the entire script, including all contained functions, are strict mode code. It is also possible to specify function-level strict mode, such that strict mode applies only to the function in which the directive occurs:

当上面的示例代码被用在全局，整个脚本，包括脚本内包含的方法是严格模式代码。指定函数级严格模式是可能的，如严格模式仅仅应用于函数中，当以下指令出现。

```js
function foo() {
    "use strict";
    return;
}

var bar = function() {
    "use strict";
    return;
};
```

Unlike scripts, ECMAScript modules are always in strict mode. Strict mode directives in ECMAScript modules have no effect.

## Rule Details

This rule is aimed at using strict mode directives effectively, and as such, will flag any unexpected uses or omissions of strict mode directives.

此规则旨在有效地使用严格模式指令，因此，将标记任何不符合期望使用放肆和严格模式指令遗漏。

## Options

There are four options for this rule:

* `"never"` - don't use `"use strict"` at all
* `never` - 不使用`"use strict"`
* `"global"` - require `"use strict"` in the global scope
* `"global"` - 在全局作用域使用 `"use strict"`
* `"function"` - require `"use strict"` in function scopes only
* `"function"` - 在函数作用域使用 `"use strict"`
* `"safe"` - require `"use strict"` globally when inside a module wrapper and in function scopes everywhere else.
* `"safe"` - 当在模块内部或函数作用域的任何地方要求使用全局`"use strict"`
 
All strict mode directives are flagged as unnecessary if ECMAScript modules or implied strict mode are enabled (see [Specifying Parser Options](../user-guide/configuring#specifying-parser-options)). This behaviour does not depend on the rule options, but can be silenced by disabling this rule.

如果ECMAScript模块或隐式严格模式下，所有的严格模式指令将被标记为非必须(查看 [Specifying Parser Options](../user-guide/configuring#specifying-parser-options))。这种行为并不取决于规则选项，但可以禁用这个规则使其报告错误。

### "never"

This mode forbids any occurrence of a strict mode directive.

这个模式禁止任何严格模式指令出现。

The following patterns are considered problems:

以下模式被认为有问题：

```js
/*eslint strict: [2, "never"]*/

"use strict";

function foo() {
    "use strict";
    return;
}

var bar = function() {
    "use strict";
    return;
};

foo();
bar();
```

The following patterns are considered valid:

```js
/*eslint strict: [2, "never"]*/

function foo() {
    return;
}

var bar = function() {
    return;
};

foo();
bar();
```

### "global"

This mode ensures that all code is in strict mode and that there are no extraneous strict mode directives at the top level or in nested functions, which are themselves already strict by virtue of being contained in strict global code. It requires that global code contains exactly one strict mode directive. Strict mode directives inside functions are considered unnecessary. Multiple strict mode directives at any level also trigger warnings.

这个模式确保所有代码处于严格模式中，在代码头部没有多次使用严格模式指令，处在全局严格模式下的函数里没有严格模式指令。规则要求全局代码中确切包含一个严格模式指令。在函数里再使用严格模式指令是没有必要的。多次使用严格模式指令在任何级别里都触发警告。

The following patterns are considered problems:

以下模式被认为有问题：

```
/*eslint strict: [2, "global"]*/

"use strict";
"use strict";

function foo() {
    "use strict";

    return function() {
        "use strict";
        "use strict";

        return;
    };
}

foo();
```

The following patterns are considered valid:

一下模式被认为有效：

```
/*eslint strict: [2, "global"]*/

"use strict";

function foo() {
    return function() {
        return;
    };
}

foo();
```

### "function"

This mode ensures that all function bodies are strict mode code, while global code is not. Particularly if a build step concatenates multiple scripts, a strict mode directive in global code of one script could unintentionally enable strict mode in another script that was not intended to be strict code. It forbids any occurrence of a strict mode directive in global code. It requires exactly one strict mode directive in each function declaration or expression whose parent is global code. Strict mode directives inside nested functions are considered unnecessary. Multiple strict mode directives at any level also trigger warnings.

这个模式确保所有函数体里是严格模式代码，而全局代码不是。特别是如果一个构建过程连接了多个脚本，某一个脚本在全局使用了严格模式可能无意地启动了其他脚本的严格模式，那个脚本并不想使用严格模式。规则禁止任何一个严格模式指令在全局代码里出现。明确要求在每个函数申明或是函数表达式中有一个严格模式指令，函数表达式上层环境须全局环境。在函数嵌套中使用严格模式指令是没有必要的。多次使用严格模式指令在任何级别里都触发警告。

The following patterns are considered problems:

以下模式被认为有问题：

```
/*eslint strict: [2, "function"]*/

"use strict";

function foo() {
    // Missing strict mode directive

    return function() {
        "use strict";   // Unnecessary; parent should contain a strict mode directive
        "use strict";

        return;
    };
}

foo();
```

The following patterns are considered valid:

以下模式被认为合法：

```
/*eslint strict: [2, "function"]*/

function foo() {
    "use strict";

    return function() {
        return;
    };
}

(function() {
    "use strict";

    return;
}());

foo();
```

### "safe" (default)

Node.js and the CommonJS module system wrap modules inside a hidden function wrapper that defines each module's scope. The wrapper makes it safe to concatenate strict mode modules while maintaining their original strict mode directives. When the `node` or `commonjs` environments are enabled or `globalReturn` is enabled in `ecmaFeatures`, ESLint considers code to be inside the module wrapper, and `"safe"` mode corresponds to `"global"` mode and enforces global strict mode directives. Everywhere else, `"safe"` mode corresponds to `"function"` mode and enforces strict mode directives inside top-level functions.

### "deprecated" (Removed)

**Replacement notice**: This mode, previously enabled by turning on the rule without specifying a mode, has been removed in ESLint v1.0. `"function"` mode is most similar to the deprecated behavior.

**替换通知**：这个模式已经在ESLint v1.0中废除，通过不指定任何模式预先激活这个模式。`"function"`模式类似于废弃的模式，如果没有任何模式被指定，废弃模式是默认模式。

This mode ensures that all functions are executed in strict mode. A strict mode directive must be present in global code or in every top-level function declaration or expression. It does not concern itself with unnecessary strict mode directives in nested functions that are already strict, nor with multiple strict mode directives at the same level.

这个模式确保所有的函数在严格模式中执行。一个严格模式指令必须出现在全局代码里或在每个函数申明或函数表达式头部。它并不关心在已经是严格模式函数里再使用严格模式指令是没有不要，或是在同级别里多次使用严格模式指令。

The following patterns are considered problems:

以下模式被认为有问题：

```js
// "strict": 2

function foo() {
    return true;
}
```

The following patterns do not cause a warning:

以下模式不会引起警告：

```js
// "strict": 2

"use strict";

function foo() {
    return true;
}

// ----------------

function foo() {

    "use strict";

    return true;
}

// ----------------

(function() {
    "use strict";

    // other code
}());
```

## When Not To Use It

In a codebase that has both strict and non-strict code, either turn this rule off, or [selectively disable it](http://eslint.org/docs/user-guide/configuring) where necessary. For example, functions referencing `arguments.callee` are invalid in strict mode. A [full list of strict mode differences](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode/Transitioning_to_strict_mode#Differences_from_non-strict_to_strict) is available on MDN.

在一个基本代码库里，既有严格模式也有非严格模式，关闭其中一个模式，或者必要时[选择禁用严格模式](http://eslint.org/docs/user-guide/configuring)。比如：函数引用`arguments.callee`是无效的在严格模式下。一个[full list of strict mode differences](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode/Transitioning_to_strict_mode#Differences_from_non-strict_to_strict)是无效的在MDN。

## Version

This rule was introduced in ESLint 0.1.0.

此规则在ESLint 0.1.0中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/strict.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/strict.md)
