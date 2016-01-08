---
title: Documentation
layout: doc
translator: molee1905
proofreader: fengnana
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Working with Plugins

# 使用插件

Each plugin is an npm module with a name in the format of `eslint-plugin-<plugin-name>`, such as `eslint-plugin-jquery`. You can also use scoped packages in the format of `@<scope>/eslint-plugin-<plugin-name>` such as `@jquery/eslint-plugin-jquery`.

每个插件是一个命名格式为`eslint-plugin-<plugin-name>`的npm模块，比如`eslint-plugin-jquery`。你也可以用这样的格式`@<scope>/eslint-plugin-<plugin-name>` 限定在包作用域下，比如`@jquery/eslint-plugin-jquery`。

## Create a Plugin

## 创建一个插件

The easiest way to start creating a plugin is to use the [Yeoman generator](https://npmjs.com/package/generator-eslint). The generator will guide you through setting up the skeleton of a plugin.

创建一个插件最简单的方式是使用[Yeoman generator](https://npmjs.com/package/generator-eslint)。它将引导你完成插件框架的设置。

### Rules in Plugins

### 插件中的规则

If your plugin has rules, then it must export an object with a `rules` property. This `rules` property should be an object containing a key-value mapping of rule ID to rule. The rule ID does not have to follow any naming convention (so it can just be `dollar-sign`, for instance).

如果你的插件包含规则，那么它必须输出一个带有`rules`属性的对象。这个`rules`属性应该是包含规则ID和对应规则的键值对对象。这个规则ID不需要遵循任何命名规范（所以，比如，它可以是`dollar-sign`）。

```js
module.exports = {
    rules: {
        "dollar-sign": function (context) {
            // rule implementation ...
        }
    }
};
```

### Processors in Plugins

### 插件中的处理器

You can also create plugins that would tell ESLint how to process files other than JavaScript. In order to create a processor, object that is exported from your module has to conform to the following interface:

你也可以创建插件告诉ESLint如何处理JavaScript之外的文件。为了创建一个处理器，从你的模块中输出的对象必须符合以下接口：

```js
processors: {

    // assign to the file extension you want (.js, .jsx, .html, etc.)
    ".ext": {
        // takes text of the file and filename
        preprocess: function(text, filename) {
            // here, you can strip out any non-JS content
            // and split into multiple strings to lint

            return [string];  // return an array of strings to lint
        },

        // takes a Message[][] and filename
        postprocess: function(messages, filename) {
            // `messages` argument contains two-dimensional array of Message objects
            // where each top-level array item contains array of lint messages related
            // to the text that was returned in array from preprocess() method

            // you need to return a one-dimensional array of the messages you want to keep
            return [Message];
        }
    }
}
```

The `preprocess` method takes the file contents and filename as arguments, and returns an array of strings to lint. The strings will be linted separately but still be registered to the filename. It's up to the plugin to decide if it needs to return just one part, or multiple pieces. For example in the case of processing `.html` files, you might want to return just one item in the array by combining all scripts, but for `.md` file where each JavaScript block might be independent, you can return multiple items.

`preprocess`将文件内容和文件名称作为参数，返回一个要检查的字符串数组。这些字符串将被分别检查，但仍要注册到文件名。决定它需要返回的只是一部分还是多个块，取决于这个插件。例如，在处理`.html`文件时，通过合并所有的脚本，你可能想要返回数组中的一项，但是对于`.md`文件，每个javascript块可能是独立的，你可以返回多个项。


The `postprocess` method takes a two-dimensional array of arrays of lint messages and the filename. Each item in the input
array corresponds to the part that was returned from the `preprocess` method. The `postprocess` method must adjust the location of all errors and aggregate them into a single flat array and return it.

`postprocess`方法需要一个二维数组作为参数，用于检查消息和文件名。传入数组中的每一项对应着从`preprocess`方法返回的部分。`postprocess`方法必须调整所有错误的位置并将他们汇集到一个的扁平的数组中，然后返回该数组。

You can have both rules and processors in a single plugin. You can also have multiple processors in one plugin.
To support multiple extensions, add each one to the `processors` element and point them to the same object.

你可以在一个插件中同时有规则和处理器。你也可以一个插件中有多个处理器。
为了支持多个扩展，将每一个处理器添加到`processors`元素，然后将它们指向同一个对象。

### Default Configuration for Plugins

### 插件的默认配置

You can provide default configuration for the rules included in your plugin by modifying
exported object to include `rulesConfig` property. `rulesConfig` follows the same pattern as
you would use in your .eslintrc config `rules` property, but without plugin name as a prefix.

你可以在你的插件中通过输出一个包含`rulesConfig`属性的对象为规则提供默认的配置。同你在 .eslintrc 中使用的`rules`属性一样，`rulesConfig`遵循同样的模式，但是没有插件名作为前缀。

```js
module.exports = {
    rules: {
        "myFirstRule": require("./lib/rules/my-first-rule"),
        "mySecondRule": require("./lib/rules/my-second-rule")
    },
    rulesConfig: {
        "myFirstRule": 1,
        "mySecondRule": [2, "on"]
    }
};
```

### Peer Dependency

### peer 依赖

To make clear that the plugin requires ESLint to work correctly you have to declare ESLint as a `peerDependency` in your `package.json`.
The plugin support was introduced in ESLint version `0.8.0`. Ensure the `peerDependency` points to ESLint `0.8.0` or later.

为了明确插件需要ESLint才能正常运行，你必须在你的`package.json`中声明将ESLint作为一个`peerDependency`。对插件的支持在ESLint`0.8.0`版本中被引入。要确保`peerDependency`指向ESLint `0.8.0`或之后的版本。

```json
{
    "peerDependencies": {
        "eslint": ">=0.8.0"
    }
}
```

### Testing

### 测试

You can test the rules of your plugin [the same way as bundled ESLint rules](working-with-rules) using [`ESLintTester`](https://github.com/eslint/eslint-tester).

你可以使用[`ESLintTester`](https://github.com/eslint/eslint-tester)测试你插件中的规则[同测试ESLint规则一样](working-with-rules)。

Example:

示例：

```js
"use strict";

var rule = require("../../../lib/rules/custom-plugin-rule"),
    RuleTester = require("eslint").RuleTester;

var ruleTester = new RuleTester();
ruleTester.run("custom-plugin-rule", rule, {
    valid: [
        "var validVariable = true",
    ],

    invalid: [
        {
            code: "var invalidVariable = true",
            errors: [ { message: "Unexpected invalid variable." } ]
        }
    ]
});
```

## Share Plugins

In order to make your plugin available to the community you have to publish it on npm.

为了让你的插件在社区中可用，你需要将它发布到npm。

Recommended keywords:

推荐的关键字：

* `eslint`
* `eslintplugin`

Add these keywords into your `package.json` file to make it easy for others to find.

将这些关键字添加到你的`package.json`中，会让其他人更容易找到它。

## Further Reading

* [npm Developer Guide](https://docs.npmjs.com/misc/developers)
