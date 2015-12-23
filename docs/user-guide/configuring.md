---
title: Documentation
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Configuring ESLint

# 配置 ESLint

ESLint is designed to be completely configurable, meaning you can turn off every rule and run only with basic syntax validation, or mix and match the bundled rules and your custom rules to make ESLint perfect for your project. There are two primary ways to configure ESLint:

ESlint 被设计为完全可配置的，这意味着你可以关闭所有规则，只运行基本的语法验证，或混合和匹配绑定的规则和你自定义规则，让ESLint更适合于你项目。有两个主要的方法配置ESLint：

1. **Configuration Comments** - use JavaScript comments to embed configuration information directly into a file.
1. **Configuration Comments** - 使用JavaScript注释直接包含配置信息到一个文件。
2. **Configuration Files** - use a JavaScript, JSON or YAML file to specify configuration information for an entire directory and all of its subdirectories. This can be in the form of an [.eslintrc.*](#configuration-file-formats) file or an `eslintConfig` field in a `package.json` file, both of which ESLint will look for and read automatically, or you can specify a configuration file on the [command line](command-line-interface).
2. **Configuration Files** - 使用JavaScript、JSON 或者 YAML 文件去描述配置信息，目录下所有的子目录都会生效。这也可以是以下两种形式：[.eslintrc.*](#configuration-file-formats)文件 或者在 `package.json`文件里配置`eslintConfig`域，这两种配置方式ESLint都会自动读取。再或者，你可以在[command line](command-line-interface)指定一个配置文件。

There are several pieces of information that can be configured:

有很多信息可以配置：

* **Environments** - which environments your script is designed to run in. Each environment brings with it a certain set of predefined global variables.
* **Environments** - 指定你脚本的运行环境。每种环境都有特定的一组预定义全局变量。
* **Globals** - the additional global variables your script accesses during execution.
* **Globals** - 脚本在执行期间需要的额外的全局变量
* **Rules** - which rules are enabled and at what error level.
* **Rules** - 指定在什么错误级别应该使用什么规则


All of these options give you fine-grained control over how ESLint treats your code.

所有这些选项，让你可以细粒度地控制ESLint如何对待你的代码。

## Specifying Language Options

## 描述语言选项

ESLint allows you to specify the JavaScript language options you want to support. By default, ESLint supports only ECMAScript 5 syntax. You can override that setting to enable support for ECMAScript 6 as well as [JSX](http://facebook.github.io/jsx/) by using configuration settings.

ESLint 允许你指定你想要支持的JavaScript语言选项。默认情况下，ESLint支持ES 5语法，但是你可以通过配置让它支持ES 6 或者 [JSX](http://facebook.github.io/jsx/)。

Configuration settings are set in your `.eslintrc` file by using the `ecmaFeatures` property. The available options are:

配置设置在`.eslintrc`文件使用`ecmaFeatures`属性设置。可用的选项有：

* `arrowFunctions` - enable [arrow functions](https://leanpub.com/understandinges6/read#leanpub-auto-arrow-functions)
* `arrowFunctions` - 开启[arrow functions](https://leanpub.com/understandinges6/read#leanpub-auto-arrow-functions)
* `binaryLiterals` - enable [binary literals](https://leanpub.com/understandinges6/read#leanpub-auto-octal-and-binary-literals)
* `binaryLiterals` - 开启 [binary literals](https://leanpub.com/understandinges6/read#leanpub-auto-octal-and-binary-literals)
* `blockBindings` - enable `let` and `const` (aka [block bindings](https://leanpub.com/understandinges6/read#leanpub-auto-block-bindings))
* `blockBindings` - 开启 `let` and `const` (aka [block bindings](https://leanpub.com/understandinges6/read#leanpub-auto-block-bindings))
* `classes` - enable classes
* `classes` - 开启 classes
* `defaultParams` - enable [default function parameters](https://leanpub.com/understandinges6/read/#leanpub-auto-default-parameters)
* `defaultParams` - 开启 [default function parameters](https://leanpub.com/understandinges6/read/#leanpub-auto-default-parameters)
* `destructuring` - enable [destructuring](https://leanpub.com/understandinges6/read#leanpub-auto-destructuring-assignment)
* `destructuring` - 开启 [destructuring](https://leanpub.com/understandinges6/read#leanpub-auto-destructuring-assignment)
* `forOf` - enable [`for-of` loops](https://leanpub.com/understandinges6/read#leanpub-auto-iterables-and-for-of)
* `forOf` - 开启 [`for-of` loops](https://leanpub.com/understandinges6/read#leanpub-auto-iterables-and-for-of)
* `generators` - enable [generators](https://leanpub.com/understandinges6/read#leanpub-auto-generators)
* `generators` - 开启 [generators](https://leanpub.com/understandinges6/read#leanpub-auto-generators)
* `modules` - enable modules and global strict mode
* `modules` - 开启 modules 和 global strict mode
* `objectLiteralComputedProperties` - enable [computed object literal property names](https://leanpub.com/understandinges6/read#leanpub-auto-computed-property-names)
* `objectLiteralComputedProperties` - 开启 [computed object literal property names](https://leanpub.com/understandinges6/read#leanpub-auto-computed-property-names)
* `objectLiteralDuplicateProperties` - enable [duplicate object literal properties](https://leanpub.com/understandinges6/read#leanpub-auto-duplicate-object-literal-properties) in strict mode
* `objectLiteralDuplicateProperties` - 在严格模式开启 [duplicate object literal properties](https://leanpub.com/understandinges6/read#leanpub-auto-duplicate-object-literal-properties)
* `objectLiteralShorthandMethods` - enable [object literal shorthand methods](https://leanpub.com/understandinges6/read#leanpub-auto-method-initializer-shorthand)
* `objectLiteralShorthandMethods` - 开启 [object literal shorthand methods](https://leanpub.com/understandinges6/read#leanpub-auto-method-initializer-shorthand)
* `objectLiteralShorthandProperties` - enable [object literal shorthand properties](https://leanpub.com/understandinges6/read#leanpub-auto-property-initializer-shorthand)
* `objectLiteralShorthandProperties` - 开启 [object literal shorthand properties](https://leanpub.com/understandinges6/read#leanpub-auto-property-initializer-shorthand)
* `octalLiterals` - enable [octal literals](https://leanpub.com/understandinges6/read#leanpub-auto-octal-and-binary-literals)
* `octalLiterals` - 开启 [octal literals](https://leanpub.com/understandinges6/read#leanpub-auto-octal-and-binary-literals)
* `regexUFlag` - enable the [regular expression `u` flag](https://leanpub.com/understandinges6/read#leanpub-auto-the-regular-expression-u-flag)
* `regexUFlag` - 开启 [regular expression `u` flag](https://leanpub.com/understandinges6/read#leanpub-auto-the-regular-expression-y-flag)
* `restParams` - enable the [rest parameters](https://leanpub.com/understandinges6/read#leanpub-auto-rest-parameters)
* `restParams` - 开启 [rest parameters](https://leanpub.com/understandinges6/read#leanpub-auto-rest-parameters)
* `spread` - enable the [spread operator](https://leanpub.com/understandinges6/read#leanpub-auto-the-spread-operator) for arrays
* `spread` - 开启 [spread operator](https://leanpub.com/understandinges6/read#leanpub-auto-the-spread-operator) for arrays
* `superInFunctions` - enable `super` references inside of functions
* `superInFunctions` - 在函数里开启 `super` 引用
* `templateStrings` - enable [template strings](https://leanpub.com/understandinges6/read/#leanpub-auto-template-strings)
* `templateStrings` - 开启 [template strings](https://leanpub.com/understandinges6/read/#leanpub-auto-template-strings)
* `unicodeCodePointEscapes` - enable [code point escapes](https://leanpub.com/understandinges6/read/#leanpub-auto-escaping-non-bmp-characters)
* `unicodeCodePointEscapes` - 开启 [code point escapes](https://leanpub.com/understandinges6/read/#leanpub-auto-escaping-non-bmp-characters)
* `globalReturn` - allow `return` statements in the global scope
* `globalReturn` - 在全局作用域中允许声明 `return`
* `jsx` - 开启 [JSX](http://facebook.github.io/jsx/)
* `jsx` - enable [JSX](http://facebook.github.io/jsx/)
* `experimentalObjectRestSpread` - enable support for the experimental [object rest/spread properties](https://github.com/sebmarkbage/ecmascript-rest-spread) (**IMPORTANT:** This is an experimental feature that may change significantly in the future. It's recommended that you do *not* write rules relying on this functionality unless you are willing to incur maintenance cost when it changes.)
* `experimentalObjectRestSpread` - 开启对实验性属性的支持 [object rest/spread properties](https://github.com/sebmarkbage/ecmascript-rest-spread) (**注意:** 这是一个处于试验阶段的特征，未来有可能会变化。建议你*不*要写依赖这个功能的规则，除非你愿意当其变化时花费精力去维护。


Here's an example `.eslintrc` file:

这里是一个`.eslintrc`文件的例子：

```json
{
    "ecmaFeatures": {
        "blockBindings": true,
        "forOf": true,
        "jsx": true
    },
    "rules": {
        "semi": 2
    }
}
```

Setting language options helps ESLint determine what is a parsing error. All language options are `false` by default.

设置语言的选项让ESLint知道如何解析，所有语言选项默认都是`false`。

## Specifying Parser

## 指定解析器

By default, ESLint uses [Espree](https://github.com/eslint/espree) as its parser. You can optionally specify that a different parser should be used in your configuration file so long as the parser meets the following requirements:

ESLint默认使用[Espree](https://github.com/eslint/espree)做它的解析器，你可以在配置文件中任意地指定一个不同的解析器，只要它满足以下要求：

1. It must be an npm module installed locally.
1. 它必须是本地安装的npm模块
2. It must have an Esprima-compatible interface (it must export a `parse()` method).
2. 它必须有兼容Esprima的接口（即：它必须导出一个parse()方法）
3. It must produce Esprima-compatible AST and token objects.
3. 它必须提供兼容Esprima的AST 和 token 对象。



Note that even with these compatibilities, there are no guarantees that an external parser will work correctly with ESLint and ESLint will not fix bugs related to incompatibilities with other parsers.

注意：即使有这些兼容性，也不能保证一个外部解析器可以很好地和ESLint一起工作，ESLint也不会修复和其它解析器结合产生的兼容性问题。

To indicate the npm module to use as your parser, specify it using the `parser` option in your `.eslintrc` file. For example, the following specifies to use Esprima instead of Espree:

为了让npm模块使用你自己的解析器，你需要在你的`.eslintrc`文件里指定`parser` 选项。例如：下面配置文件指定Esprima作为解析器而不是Espree：

```json
{
    "parser": "esprima",
    "rules": {
        "semi": 2
    }
}
```

The following parsers are compatible with ESLint:

下面的解析器和ELint兼容良好：

* [Esprima](https://npmjs.com/package/esprima)
* [Esprima-FB](https://npmjs.com/package/esprima-fb) - Facebook's fork of Esprima that includes their proprietary syntax additions.
* [Esprima-FB](https://npmjs.com/package/esprima-fb) - Facebook基于Esprima的库，另增加了它们专用的语法
* [Babel-ESLint](https://npmjs.com/package/babel-eslint) - A wrapper around the [Babel](http://babeljs.io) parser that makes it compatible with ESLint.
* [Babel-ESLint](https://npmjs.com/package/babel-eslint) -[Babel](http://babeljs.io) 解析器的封装，使它和ESLint兼容


Note when using a custom parser, the `ecmaFeatures` configuration property is still required for ESLint to work properly with features not in ECMAScript 5 by default. Parsers may or may not also use `ecmaFeatures` to determine which features to enable.

请注意：当使用自定义解析器的时候，为了兼容ES5默认不支持的特性，配置属性`ecmaFeatures`依然是必须的。解析器可能会也可能不会使用`ecmaFeatures`去决定开启那个特征。

## Specifying Environments

## 配置环境

An environment defines global variables that are predefined. The available environments are:

一个环境定义了预定义的全局变量。可用的环境有：

* `browser` - browser global variables.
* `browser` - browser 全局变量。
* `node` - Node.js global variables and Node.js scoping.
* `node` - Node.js 全局变量和 Node.js 作用域。
* `commonjs` - CommonJS global variables and CommonJS scoping (use this for browser-only code that uses Browserify/WebPack).
* `commonjs` - CommonJS 全局变量和 CommonJS 作用域 (为了兼容使用 Browserify/WebPack 的仅支持浏览器的代码)。
* `worker` - web workers global variables.
* `worker` - web workers 全局变量。
* `amd` - defines `require()` and `define()` as global variables as per the [amd](https://github.com/amdjs/amdjs-api/wiki/AMD) spec.
* `amd` - 定义 `require()` 和 `define()` 作为像 [amd](https://github.com/amdjs/amdjs-api/wiki/AMD) 一样的全局变量。
* `mocha` - adds all of the Mocha testing global variables.
* `mocha` - 添加所有 Mocha testing 全局变量。
* `jasmine` - adds all of the Jasmine testing global variables for version 1.3 and 2.0.
* `jasmine` - 添加版本号1.3和1.2的所有 Jasmine testing 全局变量。
* `jest` - Jest global variables.
* `jest` - Jest 全局变量。
* `phantomjs` - PhantomJS global variables.
* `phantomjs` - PhantomJS 全局变量。
* `protractor` - Protractor global variables.
* `protractor` - Protractor 全局变量。
* `qunit` - QUnit global variables.
* `qunit` - QUnit 全局变量。
* `jquery` - jQuery global variables.
* `jquery` - jQuery 全局变量。
* `prototypejs` - Prototype.js global variables.
* `prototypejs` - Prototype.js 全局变量。
* `shelljs` - ShellJS global variables.
* `shelljs` - ShellJS 全局变量。
* `meteor` - Meteor global variables.
* `meteor` - Meteor 全局变量。
* `mongo` - MongoDB global variables.
* `mongo` - MongoDB 全局变量。
* `applescript` - AppleScript global variables.
* `applescript` - AppleScript全局变量。
* `nashorn` - Java 8 Nashorn global variables.
* `nashorn` - Java 8 Nashorn 全局变量。
* `serviceworker` - Service Worker global variables.
* `serviceworker` - Service Worker 全局变量。
* `embertest` - Ember test helper globals.
* `embertest` - Ember test 全局变量。
* `webextensions` - WebExtensions globals.
* `webextensions` - WebExtensions 全局变量。
* `es6` - enable all ECMAScript 6 features except for modules.
* `es6` - 支持除了modules所有 ECMAScript 6 特性。


These environments are not mutually exclusive, so you can define more than one at a time.

这些环境不是相互排斥的，所以你可以一次定义多个。

Environments can be specified inside of a file, in configuration files or using the `--env` [command line](command-line-interface) flag.

环境可在配置文件中被定义在一个文件里，或者使用`--env`[命令行](command-line-interface)进行配置。

To specify environments using a comment inside of your JavaScript file, use the following format:

使用以下注释语法格式去配置环境：

```js
/*eslint-env node, mocha */
```

This enables Node.js and Mocha environments.

该设置开启了 Node.js 和 Mocha 环境。

To specify environments in a configuration file, use the `env` key and specify which environments you want to enable by setting each to `true`. For example, the following enables the browser and Node.js environments:

在配置文件里配置环境的时候，使用`env`关键字，并且给你想要的环境赋值：`true`。例如，下面这段代码开启了支持browser 和 Node.js 的环境：

```json
{
    "env": {
        "browser": true,
        "node": true
    }
}
```

Or in a `package.json` file

或者可以在`package.json`里进行配置：

```json
{
    "name": "mypackage",
    "version": "0.0.1",
    "eslintConfig": {
        "env": {
            "browser": true,
            "node": true
        }
    }
}
```

And in YAML:

在YAML文件里也可以：

```yaml
---
  env:
    browser: true
    node: true
```

## Specifying Globals

## 配置全局变量

The [no-undef](../rules/no-undef) rule will warn on variables that are accessed but not defined within the same file. If you are using global variables inside of a file then it's worthwhile to define those globals so that ESLint will not warn about their usage. You can define global variables either using comments inside of a file or in the configuration file.

当变量被使用，但是变量声明不在同一文件的时候 [no-undef](../rules/no-undef) 规则会报出警告错误。如果你想在一个文件里使用全局变量，推荐你定义这些全局变量，这样ESLint就不会警告了。你可以将全局变量定义在文件内注释或者配置文件里。

To specify globals using a comment inside of your JavaScript file, use the following format:

使用下面格式，在注释里定义全局变量：

```js
/*global var1, var2*/
```

This defines two global variables, `var1` and `var2`. If you want to optionally specify that these global variables should never be written to (only read), then you can set each with a `false` flag:

这里定义了两个全局变量：`var1` 和 `var2`。如果你想声明这些变量为只读的，你可以赋值`false`：

```js
/*global var1:false, var2:false*/
```

To configure global variables inside of a configuration file, use the `globals` key and indicate the global variables you want to use. Set each global variable name equal to `true` to allow the variable to be overwritten or `false` to disallow overwriting. For example:

在配置文件里配置全局变量的时候，使用关键字`globals`声明全局变量。赋值`true`表示允许变量被覆盖，赋值`false`进制重写。比如：

```json
{
    "globals": {
        "var1": true,
        "var2": false
    }
}
```

And in YAML:

在YAML文件里应该这样配置：

```yaml
---
  globals:
    var1: true
    var2: false
```

These examples allow `var1` to be overwritten in your code, but disallow it for `var2`.

这些例子允许`var1`可被重写，但是`var2`是只读的。

## Configuring Plugins

## 配置插件

ESLint supports the use of third-party plugins. Before using the plugin you have to install it using npm.

ESLint支持第三方插件。在使用之前，你应该先用npm去安装它们。

To configure plugins inside of a configuration file, use the `plugins` key, which contains a list of plugin names. The `eslint-plugin-` prefix can be omitted from the plugin name.

在配置文件里配置插件，要使用关键字`plugins`包含一系列的插件名字。`eslint-plugin-`前缀可被省略。

```json
{
    "plugins": [
        "plugin1",
        "eslint-plugin-plugin2"
    ]
}
```

And in YAML:

在YAML里配置：

```yaml
---
  plugins:
    - plugin1
    - eslint-plugin-plugin2
```

**Note:** A globally-installed instance of ESLint can only use globally-installed ESLint plugins. A locally-installed ESLint can make use of both locally- and globally- installed ESLint plugins.

**注意** 全局安装的ESLint只能使用全局安装的插件。本地安装的ESLint不仅可以使用本地安装的插件还可以使用全局安装的插件。

## Configuring Rules

## 配置规则

ESLint comes with a large number of rules. You can modify which rules your project uses either using configuration comments or configuration files. To change a rule setting, you must set the rule ID equal to one of these values:

ESLint 带来了大量的规则。你可以使用配置文件或者注释修改你要使用哪些规则。修改一个规则的时候，你必须设置下面ID中的一个：

* 0 - turn the rule off
* 0 - 关闭规则
* 1 - turn the rule on as a warning (doesn't affect exit code)
* 1 - 开启规则，使用警告级别的错误：`warn`(不会导致程序退出)
* 2 - turn the rule on as an error (exit code is 1 when triggered)
* 2 - 开启规则，使用错误级别的错误：`error`(当被触发的时候，程序会退出)

To configure rules inside of a file using configuration comments, use a comment in the following format:

使用以下格式在文件注释里配置规则：

```js
/*eslint eqeqeq:0, curly: 2*/
```

In this example, [`eqeqeq`](../rules/eqeqeq) is turned off and [`curly`](../rules/curly) is turned on as an error. If a rule has additional options, you can specify them using array literal syntax, such as:

在这个例子里，[`eqeqeq`](../rules/eqeqeq) 规则被关闭，[`curly`](../rules/curly) 规则被打开，并且会报错。如果一个规则有别的选项，你可以用数组字面量配置它们，比如：

```js
/*eslint quotes: [2, "double"], curly: 2*/
```

This comment specifies the "double" option for the [`quotes`](../rules/quotes) rule.

这条注释为规则[`quotes`](../rules/quotes)指定了"double"选项。

To configure rules inside of a configuration file, use the `rules` key along with an error level and any options you want to use. For example:

若要在一个配置文件中配置规则，使用关键字`rules`连同任何你想使用的选项和一个错误级别，例如：


```json
{
    "rules": {
        "eqeqeq": 0,
        "curly": 2,
        "quotes": [2, "double"]
    }
}
```

And in YAML:

在YAML中：

```yaml
---
  rules:
    eqeqeq: 0
    curly: 2
    quotes:
      - 2
      - "double"
```

To configure a rule which is defined within a plugin you have to prefix the rule ID with the plugin name and a `/`. For example:

配置定义在插件中的规则的时候，你必须使用`插件名/规则ID`的形式，比如：

```json
{
    "plugins": [
        "plugin1"
    ],
    "rules": {
        "eqeqeq": 0,
        "curly": 2,
        "quotes": [2, "double"],
        "plugin1/rule1": 2
    }
}
```

And in YAML:

在YAML中：

```yaml
---
  plugins:
    - plugin1
  rules:
    eqeqeq: 0
    curly: 2
    quotes:
      - 2
      - "double"
    plugin1/rule1: 2
```

In these configuration files, the rule `plugin1/rule1` comes from the plugin named `plugin1`. You can also use this format with configuration comments, such as:

这些配置文件中，规则`plugin1/rule1`表示来自插件`plugin1`的`rule1`规则。你也可以使用注释的格式去配置，比如：

```js
/*eslint "plugin1/rule1": 2*/
```

**Note:** When specifying rules from plugins, make sure to omit `eslint-plugin-`. ESLint uses only the unprefixed name internally to locate rules.

**注意** 当配置从插件来的规则的时候，确保删除`eslint-plugin-`前缀。因为声明该前缀，ESLint只在内部规则里去寻找。

All rules that are enabled by default are set to 2, so they will cause a non-zero exit code when encountered. You can lower these rules to a warning by setting them to 1, which has the effect of outputting the message onto the console but doesn't affect the exit code.

所有被包含的规则默认错误级别是 2，所以当触发时，它们会报错一个非零错误。你可以通过设置它们错误级别为 1 降低这些规则的级别，这样报错只会在控制台显示，而不会导致程序退出。

To temporary disable warnings in your file use the following format:

你可以使用下面格式，暂时关闭这些警告错误：

```js
/*eslint-disable */

//suppress all warnings between comments
alert('foo');

/*eslint-enable */
```

You can also disable and enable back warnings of specific rules

你还可以针对具体的规则禁用或者启用警告。


```js
/*eslint-disable no-alert, no-console */

alert('foo');
console.log('bar');

/*eslint-enable no-alert */
```

To disable warnings on a specific line

禁用某个具体的规则

```js
alert('foo'); // eslint-disable-line
```

To disable a specific rule on a specific line

在某一特定的行禁用某个特定的规则

```js
alert('foo'); // eslint-disable-line no-alert
```

## Adding Shared Settings

## 添加分享设置

ESLint supports adding shared settings into configuration file. You can add `settings` object to ESLint configuration file and it will be supplied to every rule that will be executed. This may be useful if you are adding custom rules and want them to have access to the same information and be easily configurable.

ESLint支持在配置文件添加分享设置。你可以添加`settings`对象到配置文件，它将提供给每个规则。如果你想让添加的自定义规则可以访问到相同的信息并且容易被配置，这将会很有用。

In JSON:

JSON文件中：

```json
{
    "settings": {
        "sharedData": "Hello"
    }
}
```

And in YAML:

YAML文件中：

```yaml
---
  settings:
    sharedData: "Hello"
```

## Using Configuration Files

## 使用配置文件

There are two ways to use configuration files. The first is to save the file wherever you would like and pass its location to the CLI using the `-c` option, such as:

有两种方式使用配置文件。第一种是在保存文件到你喜欢的地方，然后使用`-c`选项指定CLI的路径，比如：

    eslint -c myconfig.json myfiletotest.js

The second way to use configuration files is via `.eslintrc` and `package.json` files. ESLint will automatically look for them in the directory of the file to be linted, and in successive parent directories all the way up to the root directory of the filesystem. This option is useful when you want different configurations for different parts of a project or when you want others to be able to use ESLint directly without needing to remember to pass in the configuration file.

第二种方式是通过`.eslintrc`和`package.json`。ESLint将自动在文件目录里寻找配置文件，如果存不到它会在连续的父目录一路攀升到文件系统的根目录寻找。当你想对一个项目的不同部分的使用不同配置，或当你希望别人能够直接使用ESLint，而无需记住要通过在配置文件中，此选项很有用。

In each case, the settings in the configuration file override default settings.

每种情况，配置文件都会重写默认设置。


## Configuration File Formats

## 配置文件格式

ESLint supports configuration files in several formats:

ESLint 配置文件支持以下几种格式：

* **JavaScript** - use `.eslintrc.js` and export an object containing your configuration.
* **JavaScript** - 使用 `.eslintrc.js` 然后导出一个包含你的配置项的对象
* **YAML** - use `.eslintrc.yaml` or `.eslintrc.yml` to define the configuration structure.
* **YAML** - 使用 `.eslintrc.yaml` 或者 `.eslintrc.yml` 去定义配置的结构
* **JSON** - use `.eslintrc.json` to define the configuration structure. ESLint's JSON files also allow JavaScript-style comments.
* **JSON** - 使用 `.eslintrc.json` 去定义配置的结构，ESLint的JSON文件允许js风格的注释
* **package.json** - create an `eslintConfig` property in your `package.json` file and define your configuration there.
* **package.json** - 创建一个在`package.json`里创建一个`eslintConfig`属性，在这里定义你的配置。
* **Deprecated** - use `.eslintrc`, which can be either JSON or YAML.
* **Deprecated** - 使用 `.eslintrc`可以使JSON 也可以是 YAML


If there are multiple `.eslintrc.*` files in the same directory, ESLint will only use one. The priority order is:

如果同一个文件目录有多个`.eslintrc.*`，ESLint 只会使用一个，优先级是：

1. `.eslintrc.js`
1. `.eslintrc.yaml`
1. `.eslintrc.yml`
1. `.eslintrc.json`
1. `.eslintrc`


## Configuration Cascading and Hierarchy

## 配置层叠和继承

When using `.eslintrc` and `package.json` files for configuration, you can take advantage of configuration cascading. For instance, suppose you have the following structure:

当使用`.eslintrc` 和 `package.json`配置的时候，你可以利用配置的层叠。例如，加入你有以下文件结构：


```text
your-project
├── .eslintrc
├── lib
│ └── source.js
└─┬ tests
  ├── .eslintrc
  └── test.js
```

The configuration cascade works by using the closest `.eslintrc` file to the file being linted as the highest priority, then any configuration files in the parent directory, and so on. When you run ESLint on this project, all files in `lib/` will use the `.eslintrc` file at the root of the project as their configuration. When ESLint traverses into the `tests/` directory, it will then use `your-project/tests/.eslintrc` in addition to `your-project/.eslintrc`. So `your-project/tests/test.js` is linted based on the combination of the two `.eslintrc` files in its directory hierarchy, with the closest one taking priority. In this way, you can have project-level ESLint settings and also have directory-specific overrides.

层叠配置是这样工作的：关联文件使用最近的`.eslintrc`文件作为最高优先级，然后才是父目录里的配置信息。当你在项目中跑 ESLint 的时候，`lib/`下面的所有文件将使用项目根目录里的`.eslintrc`文件作为它的配置文件。当 ESLint 扫描到`test/`目录下，它就会用`your-project/tests/.eslintrc` 而不是 `your-project/.eslintrc`。所以`your-project/tests/test.js`是基于它的目录层次结构中的两个`.eslintrc`文件的组合去检查的，并且最近的一个优先级更高。通过这种方式，你可以有项目级ESLint设置，也有覆盖特定目录的ESLint设置。


In the same way, if there is a `package.json` file in the root directory with an `eslintConfig` field, the configuration it describes will apply to all subdirectories beneath it, but the configuration described by the `.eslintrc` file in the tests directory will override it where there are conflicting specifications.

同理，如果你在项目根目录有一个包含`eslintConfig`域的`package.json`文件，所有子目录都会使用它作为配置文件，但是当`tests`目录下的`.eslintrc`与根目录下的冲突的时候，会覆盖根目录的配置项。

```text
your-project
├── package.json
├── lib
│ └── source.js
└─┬ tests
  ├── .eslintrc
  └── test.js
```

If there is an `.eslintrc` and a `package.json` file found in the same directory, both will be used, with the `.eslintrc` having the higher precendence.

如果同一目录下`.eslintrc` 和 `package.json`同时存在，两者都会被使用，`.eslintrc`拥有更高的优先级。

**Note:** If you have a personal configuration file in your home directory (`~/.eslintrc`), it will only be used if no other configuration files are found. Since a personal configuration would apply to everything inside of a user's directory, including third-party code, this could cause problems when running ESLint.

**注意** 如果你家目录下有自定义配置文件(`~/.eslintrc`)，当且仅当没有其它配置文件被发现的时候它才会被使用。因为家目录里的配置系那个会作用于用户的每一个文件，包括第三方的代码，当ESLint运行时会导致问题。

By default, ESLint will look for configuration files in all parent folders up to the root directory. This can be useful if you want all of your projects to follow a certain convention, but can sometimes lead to unexpected results. To limit ESLint to a specific project, place `"root": true` inside the `eslintConfig` field of the `package.json` file or in the `.eslintrc` file at your project's root level.  ESLint will stop looking in parent folders once it finds a configuration with `"root": true`.

ESLint 默认会向上寻找父目录里所有配置文件直到根目录。当你想要你所有项目都使用一个特定的代码风格和语法的时候，这将会很有用，但有时候会导致出乎预料的问题。为了使ESLint作用于特定的项目，请在你项目根目录下的`package.json` 或者 `.eslintrc` 里的`eslintConfig`域下配置 `"root": true`。ESLint就会停止向上寻找。

```js
{
    "root": true
}
```

And in YAML:

在YAML中：

```yaml
---
  root: true
```

For example, consider `projectA` which has `"root": true` set in the `.eslintrc` file in the main project directory.  In this case, while linting `main.js`, the configurations within `lib/`will be used, but the `.eslintrc` file in `projectA/` will not.

假设`projectA`项目`main`目录的`.eslintrc`里有`"root": true`，当检测`main.js`的时候，`lib/`下的配置文件会被使用，但是`projectA/`下的`.eslintrc`不会被使用。

```text
home
└── user
    ├── .eslintrc <- Always skipped if other configs present
    └── projectA
        ├── .eslintrc  <- Not used
        └── lib
            ├── .eslintrc  <- { "root": true }
            └── main.js
```

```text
home
└── user
    ├── .eslintrc <- 当有其它配置文件的时候永远不会被调用
    └── projectA
        ├── .eslintrc  <- 不会使用
        └── lib
            ├── .eslintrc  <- { "root": true }
```

The complete configuration hierarchy, from highest precedence to lowest precedence, is as follows:

完整的配置体系里，优先级从高到低分别如下：

1. Inline configuration
    1. `/*eslint-disable*/` and `/*eslint-enable*/`
    1. `/*global*/`
    1. `/*eslint*/`
    1. `/*eslint-env*/`

2. Command line options:
    1. `--global`
    1. `--rule`
    1. `--env`
    1. `-c`, `--config`
3. Project-level configuration:
    1. `.eslintrc` file in same directory as linted file
    1. `package.json` file in same directory as linted file
    1. Continue searching for `.eslintrc` and `package.json` files in ancestor directories (parent has highest precedence, then grandparent, etc.), up to and including the root directory or until a config with `"root": true` is found.
    1. In the absence of any configuration from (1) thru (3), fall back to a personal default configuration in  `~/.eslintrc`.

1. 行内配置
    1. `/*eslint-disable*/` 和 `/*eslint-enable*/`
    1. `/*global*/`
    1. `/*eslint*/`
    1. `/*eslint-env*/`
2. 命令行选项:
    1. `--global`
    1. `--rule`
    1. `--env`
    1. `-c`, `--config`
3. 项目级别的配置:
    1. `.eslintrc`
    1. `package.json`
    1. 继续向上寻找`.eslintrc` 和 `package.json`(父目录拥有最高优先级，其次是父目录的父目录，等等),直到找到包含`"root": true`的配置文件，否则一直找到根目录
    1. 如果1-3都没哟，就会使用`~/.eslintrc`.

## Extending Configuration Files

## 扩展配置文件

If you want to extend a specific configuration file, you can use the `extends` property and specify the path to the file. The path can be either relative or absolute.

如果你想要扩展一个描述配置文件，你可以使用`extends`属性，然后指定文件目录，目录可以是相对目录，也可以是绝对目录。

Configurations can be extended by using:

可以使用以下方式扩展配置：

1. YAML file
1. YAML 文件
1. JSON file
1. JSON 文件
1. JS file
1. JS 文件
1. Shareable configuration package
1. 可分享的配置包


The extended configuration provides base rules, which can be overridden by the configuration that references it. For example:

扩展配置提供了基本的规则，可被覆盖，例子如下：

```js
{
    "extends": "./node_modules/coding-standard/.eslintrc",

    "rules": {
        // Override any settings from the "parent" configuration
        "eqeqeq": 1
    }
}
```

Configurations may also be provided as an array, with additional files overriding any properties provided in the previous file. For example:

配置信息也可能是一个覆盖之前培植信息的文件的数组，例如：

```js
{
    "extends": [
        "./node_modules/coding-standard/eslintDefaults.js",
        // Override eslintDefaults.js
        "./node_modules/coding-standard/.eslintrc-es6",
        // Override .eslintrc-es6
        "./node_modules/coding-standard/.eslintrc-jsx",
    ],

    "rules": {
        // Override any settings from the "parent" configuration
        "eqeqeq": 1
    }
}
```

The extended configurations can also contain their own `extends`, resulting in recursive merging of the referenced configurations.

扩展配置也可以包含它们自己的`extends`，导致递归合并引用配置。

You can also extend configurations using shareable configuration packages. To do so, be sure to install the configuration package you want from npm and then use the package name, such as:

你也可以使用可分享包扩展配置。首先你得从npm安装想使用的配置包，比如：

```js
{
    "extends": "eslint-config-myrules",

    "rules": {
        // Override any settings from the "parent" configuration
        "eqeqeq": 1
    }
}
```

In this example, the `eslint-config-myrules` package will be loaded as an object and used as the parent of this configuration.

在这个例子中，`eslint-config-myrules`包会被当做一个对象加载进来，被当做此配置文件的父级配置使用。

**Note:** You can omit `eslint-config-` and ESLint will automatically insert it for you, similar to how plugins work. See [Shareable Configs](../developer-guide/shareable-configs) for more information.

**注意** 你可以删除 `eslint-config-`前缀，ESLint 会自动帮你上的，类似插件的工作。更多资料请查看 [Shareable Configs](../developer-guide/shareable-configs)

## Comments in Configuration Files

## 配置文件里的注释

Both the JSON and YAML configuration file formats support comments (`package.json` files should not include them). You can use JavaScript-style comments or YAML-style comments in either type of file and ESLint will safely ignore them. This allows your configuration files to be more human-friendly. For example:

JSON和YAML配置文件格式都支持注释(`package.json` 本应该支持但是没有支持)。 ESLint 会安全过滤掉配置文件中JS或者YAML风格的注释。这允许你更友好地配置。比如：

```js
{
    "env": {
        "browser": true
    },
    "rules": {
        // Override our default settings just for this directory
        "eqeqeq": 1,
        "strict": 0
    }
}
```

## Ignoring Files and Directories

## 忽略文件和目录

You can tell ESLint to ignore specific files and directories by creating an `.eslintignore` file in your project's root directory. The `.eslintignore` file is a plain text file where each line is a glob pattern indicating which paths should be omitted from linting. For example, the following will omit all JavaScript files:

你可以通过在项目根目录创建`.eslintignore`文件告诉ESLint去忽略文件或者目录。`.eslintignore`文件是一个纯文本文件，其中的每一行指定哪些路径应该从被检测中文件中忽略。

```text
**/*.js
```

When ESLint is run, it looks in the current working directory to find an `.eslintignore` file before determining which files to lint. If this file is found, then those preferences are applied when traversing directories. Only one `.eslintignore` file can be used at a time, so `.eslintignore` files other than the one in the current working directory will not be used.

当ESLint 运行的时候，它会在决定哪些文件应该被检查之前在当前文件中寻找`.eslintignore`文件。如果找到，这些规则就会在被扫描的时候用上。同一时间只有一个`.eslintignore`会被应用。所以当前工作目录的`.eslintignore`文件不会被使用。

Globs are matched using [minimatch](https://github.com/isaacs/minimatch), so a number of features are available:

规律规则使用 [最小匹配](https://github.com/isaacs/minimatch)，所以大量特征都可以被利用：

* Lines beginning with `#` are treated as comments and do not affect ignore patterns.
* Lines preceded by `!` are negated patterns that re-include a pattern that was ignored by an earlier pattern.
* Brace expansion can refer to multiple files in a pattern. For example, `file.{js,ts,coffee}` will ignore `file.js`, `file.ts`, and `file.coffee`.

* 以`#`开头的行会被当做注释处理
* 行前加`!`表示否定模式，不忽略后面匹配的模式
* 大括号可以在一个模式里一次性指定多个文件。如：`file.{js,ts,coffee}`会忽略`file.js`, `file.ts`, 和 `file.coffee`.

In addition to any patterns in a `.eslintignore` file, ESLint always ignores files in `node_modules/**`.

此外，文件里的任何模式，ESLint都会忽略`node_modules/**`文件。

For example, placing the following `.eslintignore` file in the current working directory will ignore all of `node_modules`, any files with the extensions `.ts.js` or `.coffee.js` extension that might have been transpiled, and anything in the `build/` directory except `build/index.js`:

例如：把下面`.eslintignore`文件放到当前工作目录里，可能会忽略`node_modules`下所有以`.ts.js` 或者 `.coffee.js`结尾的文件，和除了`build/index.js` `build/` 目录下所有文件。

```text
# node_modules ignored by default

# 默认 忽略 node_modules

# Ignore files compiled from TypeScript and CoffeeScript

# 忽略从TypeScript 和 CoffeeScript编译的文件
**/*.{ts,coffee}.js

# Ignore built files except build/index.js

# 忽略 除了build/index.js 的 built文件

build/
!build/index.js
```

### Using an Alternate File

### 使用替补文件

If you'd prefer to use a different file than the `.eslintignore` in the current working directory, you can specify it on the command line using the `--ignore-path` option. For example, you can use `.jshintignore` file because it has the same format:

如果你更喜欢使用一个不同的文件而不是在当前文件夹下使用`.eslintignore`文件，你可以在命令行使用`--ignore-path` 选项去配置。比如，你可以使用`.jshintignore`文件，因为它有相似的格式：

    eslint --ignore-path .jshintignore file.js

You can also use your `.gitignore` file:

你也可以使用你的`.gitignore` 文件：

    eslint --ignore-path .gitignore file.js

Any file that follows the standard ignore file format can be used. Keep in mind that specifying `--ignore-path` means that any existing `.eslintignore` file will not be used. Note that globbing rules in .eslintignore are more strict than in .gitignore. See all supported patterns in [minimatch docs](https://github.com/isaacs/minimatch)

任何文件只要满足标准忽略格式都可以用。注意使用`--ignore-path`指定忽略文件会使得`.eslintignore`不可用。另外，`.eslintignore`里的语法规则比`.gitignore`里的语法规则更严谨，查看所有支持的模式: [minimatch docs](https://github.com/isaacs/minimatch)

### Ignored File Warnings

### 忽略文件警告

When you pass directories to ESLint, files and directories are silently ignored. If you pass a specific file to ESLint, then you will see a warning indicating that the file was skipped. For example, suppose you have an `.eslintignore` file that looks like this:

当你忽略一个文件目录的时候，ESLint就会默默地忽略它下面的所有文件。当你忽略一个文件的时候，ESLint就会发出警告说那个文件被跳过了。比如，你有一个类似下面代码的`.eslintignore` 文件

```text
foo.js
```


And then you run:

然后你执行以下命令：

    eslint foo.js

You'll see this warning:

你将会看到下面的警告：

```text
foo.js
  0:0  warning  File ignored because of your .eslintignore file. Use --no-ignore to override.

✖ 1 problem (0 errors, 1 warning)
```

This message occurs because ESLint is unsure if you wanted to actually lint the file or not. As the message indicates, you can use `--no-ignore` to omit using the ignore rules.

这种警告会发生是因为ESLint不知道你是否真的希望这个文件被忽略。就像错误信息所表示的你可以使用`--no-ignore`去删除这个忽略规则。
