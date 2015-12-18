---
title: Rule quote-props
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Quoting Style for Property Names (quote-props)

# 属性名称的引号风格 (quote-props)

Object literal property names can be defined in two ways: using literals or using strings. For example, these two objects are equivalent:

对象字面量的属性名称可以用两种方式进行定义：使用文本或字符串。例如，这两个对象是等效的：

```js
var object1 = {
    property: true
};

var object2 = {
    "property": true
};
```

In many cases, it doesn't matter if you choose to use an identifier instead of a string or vice-versa. Even so, you might decide to enforce a consistent style in your code.

在很多情况下，你选择使用标识符或字符串，这都不影响。即便如此，你可以决定在代码中执行一致的风格。

There are, however, some occasions when you must use quotes:

然而，有一些场合，你必须使用引号：

1. If you are using an ECMAScript 3 JavaScript engine (such as IE8) and you want to use a keyword (such as `if`) as a property name. This restriction was removed in ECMAScript 5.

1. 如果你在使用ECMAScript 3 JavaScript引擎(例如在IE8中)，而且想使用一个关键字(比如`if`)作为属性名。这个限制在ECMAScript 5被移除。

2. You want to use a non-identifier character in your property name, such as having a property with a space like `"one two"`.

2. 你现在你的属性名种使用非标识符的字符，比如一个属性中间有一个空格，像`"one two"`这样。

Another example where quotes do matter is when using numeric literals as property keys:

另外一个示例说明引号的重要性，即在使用数字文本作为属性的键时。

```js
var object = {
    1e2: 1,
    100: 2
};
```

This may look alright at first sight, but this code in fact throws a syntax error in ECMAScript 5 strict mode. This happens because `1e2` and `100` are coerced into strings before getting used as the property name. Both `String(1e2)` and `String(100)` happen to be equal to `"100"`, which causes the "Duplicate data property in object literal not allowed in strict mode" error. Issues like that can be tricky to debug, so some prefer to require quotes around all property names.

这可能咋一看起来是没有的问题的，但在ECMAScript 5严格模式下，这段代码实际上会抛出一个语法错误。因为 `1e2` 和 `100`在作为属性名使用之前被强制转换为字符串。`String(1e2)` 和 `String(100)` 碰巧是等于`"100"`，造成了”严格模式下对象字面量中不允许重复的数据属性“的错误。这样的问题调试起来非常棘手，所以一些人喜欢要求所有的属性名都要有引号。

## Rule Details

This rule aims to enforce use of quotes in property names and as such will flag any properties that don't use quotes (default behavior).

该规则旨在强制引号在属性名种的使用，因此，该规则将标记任何没有使用引号的属性(默认行为)。

### Options

There are four behaviors for this rule: `"always"` (default), `"as-needed"`, `"consistent"` and `"consistent-as-needed"`. You can define these options in your configuration as:

该规则有四种行为：`"always"` (默认), `"as-needed"`, `"consistent"` 和 `"consistent-as-needed"`。你可以在你的配置像下面这样定义这些选项：

```json
{
    "quote-props": [2, "as-needed"]
}
```

#### always

When configured with `"always"` as the first option (the default), quoting for all properties will be enforced. Some believe that ensuring property names in object literals are always wrapped in quotes is generally a good idea, since [depending on the property name you may need to quote them anyway](https://mathiasbynens.be/notes/javascript-properties). Consider this example:

当配置`"always"`作为第一个选项时(默认的)，所有的属性将被强制带引号。自从[取决于你可能需要用引号把属性名括起来](https://mathiasbynens.be/notes/javascript-properties)，一些人相信保证对象字面量中的属性名称总是被包裹在引号中通常是个好主意。请考虑以下示例：

```js
var object = {
    foo: "bar",
    baz: 42,
    "qux-lorem": true
};
```

Here, the properties `foo` and `baz` are not wrapped in quotes, but `qux-lorem` is, because it doesn’t work without the quotes. This is rather inconsistent. Instead, you may prefer to quote names of all properties:

这里，属性`foo` 和 `baz`没有被包裹在引号中，但 `qux-lorem`被括在引号中，以为如果没有引号，它将不起作用。这是相当不一致的。相反的，你可能更愿意把所有的属性名都用引号括起来。

```js
var object = {
    "foo": "bar",
    "baz": 42,
    "qux-lorem": true
};
```

or, if you prefer single quotes:

或，如果你更喜欢单引号：

```js
var object = {
    'foo': 'bar',
    'baz': 42,
    'qux-lorem': true
};
```

When configured with `"always"` as the first option (the default), quoting for all properties will be enforced. The following patterns are considered problems:

当配置`"always"`作为第一个选项时(默认的)时，所有的属性将被强制带引号。以下模式被认为是有问题的：

```js
/*eslint quote-props: [2, "always"]*/

var object = {
    foo: "bar",         /*error Unquoted property `foo` found.*/
    baz: 42,            /*error Unquoted property `baz` found.*/
    "qux-lorem": true
};
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint quote-props: [2, "always"]*/
/*eslint-env es6*/

var object1 = {
    "foo": "bar",
    "baz": 42,
    "qux-lorem": true
};

var object2 = {
    'foo': 'bar',
    'baz': 42,
    'qux-lorem': true
};

var object3 = {
    foo() {
        return;
    }
};
```

#### as-needed

When configured with `"as-needed"` as the first option, quotes will be enforced when they are strictly required, and unnecessary quotes will cause warnings. The following patterns are considered problems:

当配置`"as-needed"`作为第一个选项时，严格要求带引号的属性将被强制带引号，不必要的引号将发出警告。以下模式被认为是有问题的：

```js
/*eslint quote-props: [2, "as-needed"]*/

var object = {
    "a": 0,    /*error Unnecessarily quoted property `a` found.*/
    "0": 0,    /*error Unnecessarily quoted property `0` found.*/
    "true": 0, /*error Unnecessarily quoted property `true` found.*/
    "null": 0  /*error Unnecessarily quoted property `null` found.*/
};
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint quote-props: [2, "as-needed"]*/
/*eslint-env es6*/

var object1 = {
    "a-b": 0,
    "0x0": 0,
    "1e2": 0
};

var object2 = {
    foo: 'bar',
    baz: 42,
    true: 0,
    0: 0,
    'qux-lorem': true
};

var object3 = {
    foo() {
        return;
    }
};
```

When the `"as-needed"` mode is selected, an additional `keywords` option can be provided. This flag indicates whether language keywords can be used unquoted as properties. By default it is set to `false`.

当`"as-needed"`方式被选用时，可提供一个额外的`keywords`选项。此标记指示关键字作为属性是否可以不用引号。默认情况下它被设置为`false`。

```json
{
    "quote-props": [2, "as-needed", { "keywords": true }]
}
```

When `keywords` is set to `true`, the following patterns become problems:

当`keywords`被设置为`true`，以下模式是有问题的：

```js
/*eslint quote-props: [2, "as-needed", { "keywords": true }]*/

var x = {
    while: 1,       /*error Unquoted reserved word `while` used as key.*/
    volatile: "foo" /*error Unquoted reserved word `volatile` used as key.*/
};
```

Another modifier for this rule is the `unnecessary` option which defaults to `true`. Setting this to `false` will prevent the rule from complaining about unnecessarily quoted properties. This comes in handy when you _only_ care about quoting keywords.

该规则的另一个修饰符是`unnecessary`选项默认为`true`。设置这个选项为`false`，该规则将不对不必要的被引号括起来的属性进行检查。当你值关注被括起来的关键字时，这会很方便。

```json
{
    "quote-props": [2, "as-needed", { "keywords": true, "unnecessary": false }]
}
```

When `unnecessary` is set to `false`, the following patterns _stop_ being problems:

当设置`unnecessary`为`false`时，以下模式是没有问题的：

```js
/*eslint quote-props: [2, "as-needed", { "keywords": true, "unnecessary": false }]*/

var x = {
    "while": 1,
    "foo": "bar"  // Would normally have caused a warning
};
```

A `numbers` flag, with default value `false`, can also be used as a modifier for the `"as-needed"` mode. When it is set to `true`, numeric literals should always be quoted.

`numbers`标记，默认为`false`，也可以在`"as-needed"`方式下被用作修饰符。当设置为`true`是，数字文本应该被引号括起来。

```json
{
    "quote-props": [2, "as-needed", {"numbers": true}]
}
```

When `numbers` is set to `true`, the following patterns become problems:

当`numbers`设置为`true`时，以下模式是有问题的：

```js
/*eslint quote-props: [2, "as-needed", { "numbers": true }]*/

var x = {
    100: 1 /*error Unquoted number literal `100` used as key.*/
}
```

and the following patterns _stop_ being problems:

以下模式没有问题：

```js
var x = {
    "100": 1
}
```

#### consistent

When configured with `"consistent"`, the patterns below are considered problems. Basically `"consistent"` means all or no properties are expected to be quoted, in other words quoting style can't be mixed within an object. Please note the latter situation (no quotation at all) isn't always possible as some property names require quoting.

当配置为`"consistent"`，以下模式被认为是有问题的。`"consistent"`意味着所有属性或没有属性被引号括起来，换句话说，在同一个对象中不能混合使用不同的引号风格。请注意后一种情况(没有引号)并不总是可能因为某些属性名需要用引号括起来。

```js
/*eslint quote-props: [2, "consistent"]*/

var object1 = {        /*error Inconsistently quoted property `baz` found.*/ /*error Inconsistently quoted property `qux-lorem` found.*/
    foo: "bar",
    "baz": 42,
    "qux-lorem": true
};

var object2 = {        /*error Inconsistently quoted property `baz` found.*/
    'foo': 'bar',
    baz: 42
};
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint quote-props: [2, "consistent"]*/

var object1 = {
    "foo": "bar",
    "baz": 42,
    "qux-lorem": true
};

var object2 = {
    'foo': 'bar',
    'baz': 42
};

var object3 = {
    foo: 'bar',
    baz: 42
};
```

#### consistent-as-needed

When configured with `"consistent-as-needed"`, the behavior is similar to `"consistent"` with one difference. Namely, properties' quoting should be consistent (as in `"consistent"`) but whenever all quotes are redundant a warning is raised. In other words if at least one property name has to be quoted (like `qux-lorem`) then all property names must be quoted, otherwise no properties can be quoted. The following patterns are considered problems:

当配置了`"consistent-as-needed"`，它的行为类似于`"consistent"`，仅有一个区别。即，除了所有的引号都是多余的引起了警告，属性的引号应该是一致的(同在 `"consistent"`中一样)。换句话说，如果有一个属性名是被引号括起来的(像`qux-lorem`)，其他的属性名必须也被引号括起来，否则，任何属性都不能被括起来。以下模式被认为是有问题的：

```js
/*eslint quote-props: [2, "consistent-as-needed"]*/

var object1 = {         /*error Inconsistently quoted property `baz` found.*/ /*error Inconsistently quoted property `qux-lorem` found.*/
    foo: "bar",
    "baz": 42,
    "qux-lorem": true
};

var object2 = {         /*error Properties shouldn't be quoted as all quotes are redundant.*/
    'foo': 'bar',
    'baz': 42
};
```

The following patterns are not considered problems:

以下模式被认为是没有问题的：

```js
/*eslint quote-props: [2, "consistent-as-needed"]*/

var object1 = {
    "foo": "bar",
    "baz": 42,
    "qux-lorem": true
};

var object2 = {
    foo: 'bar',
    baz: 42
};
```

When the `"consistent-as-needed"` mode is selected, an additional `keywords` option can be provided. This flag indicates whether language keywords can be used unquoted as properties. By default it is set to `false`.

当`"consistent-as-needed"`方式被选用时，可提供一个额外的`keywords`选项。此标记指示关键字作为属性是否可以不用引号。默认情况下它被设置为`false`。

```json
{
    "quote-props": [2, "consistent-as-needed", { "keywords": true }]
}
```

When `keywords` is set to `true`, the following patterns are considered problems:

当`keywords`被设置为`true`，以下模式被认为是有问题的：

```js
/*eslint quote-props: [2, "consistent-as-needed", { "keywords": true }]*/

var x = {           /*error Properties should be quoted as `while` is a reserved word.*/ /*error Properties should be quoted as `volatile` is a reserved word.*/
    while: 1,
    volatile: "foo"
};
```

## When Not To Use It

If you don't care if property names are consistently wrapped in quotes or not, and you don't target legacy ES3 environments, turn this rule off.

如果你并不关系属性名是否有引号的一致性，也不把ES3环境当成你的目标，关闭此规则即可。

## Further Reading

* [Reserved words as property names](http://kangax.github.io/compat-table/es5/#Reserved_words_as_property_names)
* [Unquoted property names / object keys in JavaScript](https://mathiasbynens.be/notes/javascript-properties)

## Version

This rule was introduced in ESLint 0.0.6.

该规则在ESLint 0.0.6中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/quote-props.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/quote-props.md)
