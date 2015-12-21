---
title: Rule handle-callback-err
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Enforce Callback Error Handling (handle-callback-err)

# 强制回调错误处理 (handle-callback-err)

In node, a common pattern for dealing with asynchronous behavior is called the callback pattern.
This pattern expects an `Error` object or `null` as the first argument of the callback.
Forgetting to handle these errors can lead to some really strange behavior in your application.

在node中，一普通的模式为了处理异步行为被叫做回调模式。这个模式期望一个`Error`对象和`null`作为回调的第一个参数。忘记处理这个错误能导致奇怪的行为在你的应用中。

```js
function loadData (err, data) {
    doSomething(); // forgot to handle error
}
```

## Rule Details

This rule expects that when you're using the callback pattern in node you'll handle the error and
requires that you specify the name of your error object. The name of the argument will default to `err`.

此规则期待当你在node中使用回调形式，你将处理这个错误并要求指定错误对象的名称。参数名称默认是`err`。

The following are considered problems:

以下模式被认为有问题的：

```js
/*eslint handle-callback-err: 2*/

function loadData (err, data) { /*error Expected error to be handled.*/
    doSomething();
}

```

The following are not considered problems:

以下模式被认为没有问题的：

```js
/*eslint handle-callback-err: 2*/

function loadData (err, data) {
    if (err) {
        console.log(err.stack);
    }
    doSomething();
}

function generateError (err) {
    if (err) {}
}
```

You can also customize the name of the error object:

你也可以自定义错误对象的名称：

```js
/*eslint handle-callback-err: [2, "error"]*/

function loadData (error, data) {
    if (error) {
       console.log(error.stack);
    }
}
```

### Advanced configuration

Sometimes (especially in big projects) the name of the error variable is not consistent across the project,
so you need a more flexible configuration to ensure all unhandled error getting recognized by this rule.

有时候（特别是在大项目中）错误变量名不都一致在整个项目中，所以你需要一个更加灵活的配置去确保未处理的错误得到此规则的认可。

If the configured name of the error variable begins with a `^` it is considered to be a regexp pattern.

如果错误变量的配置名以`^`开头被认为是一个正则模式。

Examples for valid configurations:

如下一个有效配置：

1. Rule configured to warn if an unhandled error is detected where the name of the error variable can be `err`, `error` or `anySpecificError`.

1. 规则配置如下将报警告，如果发现一个未处理错误，错误变量名是`err`, `error`或者`anySpecificError`。

    ```json
    // ...
    "handle-callback-err": [2, "^(err|error|anySpecificError)$" ]
    // ...
    ```

2. Rule configured to warn if an unhandled error is detected where the name of the error variable ends with `Error` (e. g. `connectionError` or `validationError` will match).

1. 规则配置如下将报警告，如果发现一个未处理错误，错误变量名以`Error`结尾。

    ```json
    // ...
    "handle-callback-err": [2, "^.+Error$" ]
    // ...
    ```

3. Rule configured to warn if an unhandled error is detected where the name of the error variable matches any string that contains `err` or `Err` (e. g. `err`, `error`, `anyError`, `some_err` will match).

1. 规则配置如下将报警告，如果发现一个未处理错误，错误变量名匹配中包含`err`或则`Err`。

    ```json
    // ...
    "handle-callback-err": [2, "^.*(e|E)rr" ]
    // ...
    ```

## When Not To Use This Rule

There are cases where it may be safe for your application to ignore errors, however only ignore errors if you are
confident that some other form of monitoring will help you catch the problem.

有些情况可能是安全为你的应用程序去忽略错误，也就仅仅可忽略此错误，如果你相信一些其他形式的监督将帮助你发现问题。

## Further Reading

* [The Art Of Node: Callbacks](https://github.com/maxogden/art-of-node#callbacks)
* [Nodejitsu: What are the error conventions?](http://docs.nodejitsu.com/articles/errors/what-are-the-error-conventions)

## Version

This rule was introduced in ESLint 0.4.5.

此规则在ESLint 0.4.5被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/handle-callback-err.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/handle-callback-err.md)
