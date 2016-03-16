---
title: Documentation
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->

# Command Line Interface

# 命令行界面

To run ESLint on Node.js, you must have npm installed. If npm is not installed, follow the instructions here: https://www.npmjs.com/

为了在Node.js上运行ESLint，你必须先安装npm。如果npm还没安装，跟着这里的说明一步步安装就好: https://www.npmjs.com/

Once npm is installed, run the following

一旦安装了npm，执行下面的命令：

    npm i -g eslint

This installs the ESLint CLI from the npm repository. To run ESLint, use the following format:

这句命令从npm 仓库安装了ESlint CLI。执行下面命令使用ESlint：

    eslint [options] [file|dir|glob]*

Such as:

比如：

    eslint file1.js file2.js

or:

或者：

    eslint lib/**

## Options

## 选项

The command line utility has several options. You can view the options by running `eslint -h`.

命令行工具有几个选项，你可以执行`eslint -h`查看选项。

```text
Basic configuration:
  -c, --config path::String  Use configuration from this file or shareable
                             config
  --no-eslintrc              Disable use of configuration from .eslintrc
  --env [String]             Specify environments
  --ext [String]             Specify JavaScript file extensions - default: .js
  --global [String]          Define global variables
  --parser String            Specify the parser to be used - default: espree

Caching:
  --cache                    Only check changed files - default: false
  --cache-file path::String  Path to the cache file - default: .eslintcache.
                             Deprecated: use --cache-location
  --cache-location path::String  Path to the cache file or directory.

Specifying rules and plugins:
  --rulesdir [path::String]  Use additional rules from this directory
  --plugin [String]          Specify plugins
  --rule Object              Specify rules

Ignoring files:
  --ignore-path path::String  Specify path of ignore file
  --no-ignore                Disable use of .eslintignore
  --ignore-pattern [String]  Patterns of files to ignore (in addition to those
                             in .eslintignore)

Using stdin:
  --stdin                    Lint code provided on <STDIN> - default: false
  --stdin-filename String    Specify filename to process STDIN as

Handling warnings:
  --quiet                    Report errors only - default: false
  --max-warnings Int         Number of warnings to trigger nonzero exit code -
                             default: -1

Output:
  -o, --output-file path::String  Specify file to write report to
  -f, --format String        Use a specific output format - default: stylish
  --no-color                 Disable color in piped output

Miscellaneous:
  --init                     Run config initialization wizard - default: false
  --fix                      Automatically fix problems
  --debug                    Output debugging information
  -h, --help                 Show help
  -v, --version              Outputs the version number
  --no-inline-config         Prevent comments from changing eslint rules -
                             default: false
  --print-config             Print the configuration to be used
```

Options that accept array values can be specified by repeating the option or with a comma-delimited list (other than `--ignore-pattern` which does not allow the second style).

选项可以用以下两种方式接受多值：

Example:

    eslint --ext .jsx --ext .js file.js

    eslint --ext .jsx,.js file.js

### Basic configuration

### 基本配置

#### `-c`, `--config`

#### `-c`, `--config`

This option allows you to specify an additional configuration file for ESLint (see [Configuring ESLint](configuring) for more).

选项允许你为ESLint指定额外的配置文件(更多信息请查阅[配置 ESLint](configuring))

Example:

例如：

    eslint -c ~/my-eslint.json file.js

This example uses the configuration file at `~/my-eslint.json`.

这个例子使用`~/my-eslint.json`作为配置文件。

It also accepts a module ID of [sharable config](../developer-guide/shareable-configs).

它也可以接受[可分享的配置](../developer-guide/shareable-configs)的一个模块的ID

Example:

例如：

    eslint -c myconfig file.js

This example directly uses the sharable config `eslint-config-myconfig`.

这个例子直接使用可分享的配置`eslint-config-myconfig`

#### `--no-eslintrc`

#### `--no-eslintrc`

Disables use of configuration from `.eslintrc` and `package.json` files.

不使用`.eslintrc` 和 `package.json`的配置。

Example:

    eslint --no-eslintrc file.js

#### `--env`

#### `--env`

This option enables specific environments. Details about the global variables defined by each environment are available on the [configuration](configuring) documentation. This flag only enables environments; it does not disable environments set in other configuration files. To specify multiple environments, separate them using commas, or use the flag multiple times.

这个选项允许指定环境。有关每个环境决定什么全局变量的详情请查阅[配置文档](configuring)

Examples:

例如：

    eslint --env browser,node file.js
    eslint --env browser --env node file.js

#### `--ext`

#### `--ext`

This option allows you to specify which file extensions ESLint will use when searching for JavaScript files. By default, it uses `.js` as the only file extension.

这个选项允许你指定使用什么扩展，ESLint会在查找js文件的时候使用它。默认地，扩展文件只使用`.js`后缀。

Examples:

例如：

    # Use only .js2 extension
    # 只使用 .js2 扩展
    eslint --ext .js2

    # Use both .js and .js2
    # 使用 .js 和 .js2
    eslint --ext .js --ext .js2

    # Also use both .js and .js2
    # 使用 .js 和 .js2
    eslint --ext .js,.js2

#### `--global`

#### `--global`

This option defines global variables so that they will not be flagged as undefined by the `no-undef` rule. Global variables are read-only by default, but appending `:true` to a variable's name makes it writable. To define multiple variables, separate them using commas, or use the flag multiple times.

这个选项定义了全局变量，这样他们就不会被`no-undef`规则检测为`undefined`了。全局变量默认是只读的，但是在变量名字后追加`:true`会使他变得可写，多个选项可以使用逗号分隔或者使用多次选项。

Examples:

例如：

    eslint --global require,exports:true file.js
    eslint --global require --global exports:true

#### `--parser`

#### `--parser`

This option allows you to specify a parser to be used by eslint. By default, `espree` will be used.

这个选项允许你为 eslint 指定一个解析器。默认使用`espree`。

### Caching

### 缓存

#### `--cache`

Store the info about processed files in order to only operate on the changed ones.

为了只操作改变的文件，存储处理过的文件。

#### `--cache-file`

Path to the cache file. If none specified `.eslintcache` will be used. The file will be created in the directory where the `eslint` command is executed. **Deprecated**: Use `--cache-location` instead.

指定指向缓存文件的路径。如果没明确指定则使用`.eslintcache`。这个文件会在 `eslint` 命令行被执行的文件目录被创建。**否则(Deprecated)**: 使用`--cache-location`指定缓存文件的路径。

#### `--cache-location`

Path to the cache location. Can be a file or a directory. If none specified `.eslintcache` will be used. The file will be created in the directory where the `eslint` command is executed.

指定缓存文件的路径。可以使一个文件或者一个目录。如果没有明确指定则默认使用`.eslintcache`。`.eslintcache`文件会在`eslint`命令行执行的目录下被创建。

In case a directory is specified a cache file will be created inside the specified folder. The name of the file will be based on the hash of the current working directory (CWD). e.g.: `.cache_hashOfCWD`

为了防止万一缓存文件名被占用，缓存文件的名字基于当前工作目录的hash创建，例如e.g.: `.cache_hashOfCWD`

**Important note:** If the directory for the cache does not exist make sure you add a trailing `/` on *nix systems or `\` in windows. Otherwise the path will be assumed to be a file.

**请注意:**如果缓存文件不存在，请确认您在*nix 系统里文件路径最后增加了`/`(window 下是 `\`)，否则路径会被假设为文件

Example:

例如：

    eslint 'src/**/*.js' --cache --cache-location '/Users/user/.eslintcache/'

### Specifying rules and plugins

### 指定规则和插件

#### `--rulesdir`


This option allows you to specify a second directory from which to load rules files. This allows you to dynamically load new rules at run time. This is useful when you have custom rules that aren't suitable for being bundled with ESLint.

这个选项允许你指定第二个文件夹去加载规则。这允许你在执行的时候动态加载新的规则。当你有不适合和ESLint绑定的自定义规则的时候，这个非常有用。

Example:

例如：

    eslint --rulesdir my-rules/ file.js

The rules in your custom rules directory must follow the same format as bundled rules to work properly. You can also specify multiple locations for custom rules by including multiple `--rulesdir` flags:

为了使用户自定义规则能很好使用，必须遵循绑定的规则的格式。您可通过使用`--rulesdir`指定多个自定义规则文件

    eslint --rulesdir my-rules/ --rulesdir my-other-rules/ file.js

#### `--plugin`

This option specifies a plugin to load. You can omit the prefix `eslint-plugin-` from the plugin name.
Before using the plugin you have to install it using npm.

这个选项可加载插件。你可以删除插件名的`eslint-plugin-`前缀，在使用之前，必须先使用npm安装。

Examples:

例如：

    eslint --plugin jquery file.js
    eslint --plugin eslint-plugin-mocha file.js

#### `--rule`

This option specifies rules to be used. These rules will be merged with any rules specified with configuration files. (You can use `--no-eslintrc` to change that behavior.) To define multiple rules, separate them using commas, or use the flag multiple times. The [levn](https://github.com/gkz/levn#levn--) format is used for specifying the rules.

这个选项指定了要使用的规则。这些规则会和配置文件里的规则合并(你可以使用`--no-eslintrc`去阻止这个行为)。为了定义多个规则，使用逗号分隔，或者多次使用。levn](https://github.com/gkz/levn#levn--) 格式用来指定特定的规则。

If the rule is defined within a plugin you have to prefix the rule ID with the plugin name and a `/`.

如果规则定义在插件内，你需使用规则id、插件名、`/`作为前缀。

Examples:

例如：

    eslint --rule 'quotes: [2, double]'
    eslint --rule 'guard-for-in: 2' --rule 'brace-style: [2, 1tbs]'
    eslint --rule 'jquery/dollar-sign: 2'

### Ignoring files

#### `--ignore-path`

This option allows you to specify the file to use as your `.eslintignore`. By default, ESLint looks in the current working directory for `.eslintignore`. You can override this behavior by providing a path to a different file.

这个选项允许您指定文件作为`.eslintignore`。默认，ESLint 在当前目录查找 `.eslintignore`。您可以通过提供一个不同文件的路径覆盖这个行为。

Example:

例如：

    eslint --ignore-path tmp/.eslintignore file.js

#### `--no-ignore`

Disables excluding of files from `.eslintignore` and `--ignore-path` files.

从`.eslintignore` 和 `--ignore-path` 文件里 关闭排除文件。

Example:

例如：

    eslint --no-ignore file.js

### Using stdin

### 使用stdin

#### `--stdin`

This option tells ESLint to read and lint source code from STDIN instead files. You can use this to pipe code to ESLint.

这个选项告诉 ESLint 从 STDIN 读取源代码并检测。您可以用管道来使用标准输入输出。

Example

例如：

    cat myfile.js | eslint --stdin

#### `--stdin-filename`

This option allows you to specify a filename to process STDIN as. This is useful when processing files from STDIN and you have rules which depend on the filename.

这个选项允许您指定一个文件名去处理stdin。当从stdin里处理文件的时候，当您必须有依赖于文件名的规则的时候，这个很有用。

Example

例如：

    cat myfile.js | eslint --stdin --stdin-filename=myfile.js

### Handling warnings

### 处理警告

#### `--quiet`

This option allows you to disable reporting on warnings. If you enable this option only errors are reported by ESLint.

这个选项允许你禁止报告警告。如果开启这个选项，ESLint只会报告错误。

Example:

例如：

    eslint --quiet file.js

#### `--max-warnings`

This option allows you to specify a warning threshold, which can be used to force ESLint to exit with an error status if there are too many warning-level rule violations in your project.

这个选项允许你指定一个警告的下限，这个可以使ESLint遇到错误状态的时候，如果项目中遇到太多警告，则强制退出。

Normally, if ESLint runs and finds no errors (only warnings), it will exit with a success exit status. However, if this option is specified and the total warning count is greater than the specified threshold, ESLint will exit with an error status. Specifying a threshold of `-1` or omitting this option will prevent this behavior.

一般情况下，如果 ESLint 运行，而且并没有找到错误(只是警告)，他就会返回一个成功退出状态然后退出。然而，如果这个选项已经指定，并且总警告数比指定的下限多，ESLint就会退出，并且返回一个错误状态。指定一个下限`-1`或者删除这个规则，可避免这种行为。

Example:

例如：

    eslint --max-warnings 10 file.js

### Output

### 输出

#### `-o`, `--output-file`

Enable report to be written to a file.

开启 将结果输出到一个文件。

Example:

例如：

    eslint -o ./test/test.html

When specified, the given format is output into the provided file name.

当指定这个选项，文件就会按照给出的格式输出到指定的文件名内。

#### `-f`, `--format`

This option specifies the output format for the console. Possible formats are:

这个选项指定输出到控制台的格式。可用的格式有：

* [checkstyle](formatters/#checkstyle)
* [compact](formatters/#compact)
* [html](formatters/#html)
* [jslint-xml](formatters/#jslint-xml)
* [json](formatters/#json)
* [junit](formatters/#junit)
* [stylish](formatters/#stylish) (the default)
* [table](formatters/#table)
* [tap](formatters/#tap)
* [unix](formatters/#unix)
* [visualstudio](formatters/#visualstudio)

Example:

例如：

    eslint -f compact file.js

You can also use a custom formatter from the command line by specifying a path to the custom formatter file.

您也可以通过在命令行指定自定义格式文件使用自定义格式。

Example:

例如：

    eslint -f ./customformat.js file.js

When specified, the given format is output to the console. If you'd like to save that output into a file, you can do so on the command line like so:

当指定之后，给出的文件会输出到控制台。如果您想将输出写入到一个文件内，可以在命令行像下面这样做：

    eslint -f compact file.js > results.txt

This saves the output into the `results.txt` file.

这条命令会将输出文件保存到`results.txt`文件。

#### `--no-color`

Disable color in piped output.

在管道输出中禁用颜色。

Example:

例如：

    eslint --no-color file.js

### Miscellaneous

### 其他

#### `--init`

This option will start config initialization wizard. It's designed to help new users quickly create .eslintrc file by answering a few questions. File will be created in current directory.

这个选项将会开始配置初始化引导程序。这用于引导新手快速创建`.eslintrc`文件 通过回答几个问题。文件会在正确的文件夹里被创建。

#### `--fix`

This option instructs ESLint to try to fix as many issues as possible. The fixes are made to the actual files themselves and only the remaining unfixed issues are output. Not all problems are fixable using this flag, and the flag does not work in these situations:

这个选项告诉ESLint尽可能多的解决问题。只未被解决的问题被输出。不是所有问题都可以使用这句被修复，这句在以下情况不会工作：

1. This option throws an error when code is piped to ESLint.
1. This option has no effect on code that uses processors.

1. 当代码使用管道连接到ESLint的时候，这个选项会抛出一个错误
1. 这个选项对使用处理器的代码没作用

#### `--debug`

This option outputs debugging information to the console. This information is useful when you're seeing a problem and having a hard time pinpointing it. The ESLint team may ask for this debugging information to help solve bugs.

这个选项会将调试错误信息输出到控制台。当你遇到一个问题的时候这个信息将会很有用。ESLint 团队帮解决bug的时候也会问到这些调试信息。

#### `-h`, `--help`

This option outputs the help menu, displaying all of the available options. All other flags are ignored when this is present.

这个选项会输出帮助菜单，展示所有可用选项，忽略所有其他参数。

#### `-v`, `--version`

This option outputs the current ESLint version onto the console. All other options are ignored when present.

这个选项输出当前ESlint的版本到控制台。所有其他选项都会被忽略。

Example:

例如：

    eslint -v

#### `--no-inline-config`

This option prevents inline comments like `/*eslint-disable*/` or
`/*global foo*/` from having any effect. This allows you to set an ESLint
config without files modifying it. All inline config comments are ignored, e.g.:

这个选项会忽略`/*eslint-disable*/`或者`/*global foo*/` 这样的内联注释命令。这允许你不用修改配置文件就可以修改ESLint的配置。所有类似下面的内联注释都会被忽略：

* `/*eslint-disable*/`
* `/*eslint-enable*/`
* `/*global*/`
* `/*eslint*/`
* `/*eslint-env*/`
* `// eslint-disable-line`
* `// eslint-disable-next-line`

Example:

例如：

    eslint --no-inline-config file.js

#### `--print-config`

This option outputs the configuration to be used for the file passed. When present, no linting is performed and only config-related options are valid.

Example:

    eslint --print-config file.js

## Ignoring files from linting

## 忽略检查的文件

ESLint supports `.eslintignore` files to exclude files from the linting process when ESLint operates on a directory. Files given as individual CLI arguments will be exempt from exclusion. The `.eslintignore` file is a plain text file containing one pattern per line. It can be located in any of the target directory's ancestors; it will affect files in its containing directory as well as all sub-directories. Here's a simple example of a `.eslintignore` file:

当ESLint作用在一个文件夹的时候，ESLint支持`.eslintignore` 文件从检查进程中排除一些文件。被给出 独立客户端 参数的文件会被排除。`.eslintignore`是一个纯文本文件，每行一个模式。他可以被放在任何祖先文件夹里，它会影响被它包含的所有文件，这里是一个简单的`.eslintignore` 文件：

    node_modules/*
    **/vendor/*.js

A more detailed breakdown of supported patterns and directories ESLint ignores by default can be found in [Configuring ESLint](http://eslint.org/docs/user-guide/configuring#ignoring-files-and-directories).
