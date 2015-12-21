---
title: Rule accessor-pairs
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Enforces getter/setter pairs in objects (accessor-pairs)

# 强制 getter/setter成对出现在对象中 (accessor-pairs)

It's a common mistake in JavaScript to create an object with just a setter for a property but never have a corresponding getter defined for it. Without a getter, you cannot read the property, so it ends up not being used.

在JavaScript中这是一个常见的错误，创建一个对象只有属性的设置但是没有为它定义一个对应的获取属性的方法。没有getter,你不能读取属性，所以它将终不会被使用。

Here are some examples:

以下有些例子：

```js
// Bad
var o = {
    set a(value) {
        this.val = value;
    }
};

// Good
var o = {
    set a(value) {
        this.val = value;
    },
    get a() {
        return this.val;
    }
};

```

This rule warns if setters are defined without getters. Using an option `getWithoutSet`, it will warn if you have a getter without a setter also.

此规则会给出警告如果setter被定义而getter却没有。使用`getWithoutSet`选项，它同样会给出警告如果存在getter而没有setter。

## Rule Details

This rule enforces a style where it requires to have a getter for every property which has a setter defined.

这个规则执行一个风格,它需要有一个getter对应每个属性的setter的定义。

By activating the option `getWithoutSet` it enforces the presence of a setter for every property which has a getter defined.

通过激活选项`getWithoutSet`强制执行为每个定义了getter的属性提供对应的setter。

### Options

`getWithoutSet` set to `true` will warn for getters without setters (Default `false`).
`setWithoutGet` set to `true` will warn for setters without getters (Default `true`).

`getWithoutSet`设置为`true`，会给出警告当有getter而没有setter（默认为`false`）。`setWithoutGet`设置为`true`，会给出警告当有setter而没有getter（默认为`true`）。

#### Usage

By default `setWithoutGet` option is always set to `true`.

默认的`setWithoutGet`选择总是被设置为`true`。

```json
{
    "accessor-pairs": [2, {"getWithoutSet": true}]
}
```

The following patterns are considered problems by default:

默认的以下模式被认为是有问题的：

```js
/*eslint accessor-pairs: 2*/

var o = {                       /*error Getter is not present*/
    set a(value) {
        this.val = value;
    }
};

var o = {d: 1};
Object.defineProperty(o, 'c', { /*error Getter is not present*/
    set: function(value) {
        this.val = value;
    }
});
```

The following patterns are not considered problems by default:

默认的以下模式被认为是没有问题的：

```js
/*eslint accessor-pairs: 2*/

var o = {
    set a(value) {
        this.val = value;
    },
    get a() {
        return this.val;
    }
};

var o = {d: 1};
Object.defineProperty(o, 'c', {
    set: function(value) {
        this.val = value;
    },
    get: function() {
        return this.val;
    }
});

```

#### getWithoutSet

The following patterns are considered problems with option `getWithoutSet` set:

在`getWithoutSet`设置下，以下模式被认为是有问题的：

```js
/*eslint accessor-pairs: [2, { getWithoutSet: true }]*/

var o = {                       /*error Getter is not present*/
    set a(value) {
        this.val = value;
    }
};

var o = {                       /*error Setter is not present*/
    get a() {
        return this.val;
    }
};

var o = {d: 1};
Object.defineProperty(o, 'c', { /*error Getter is not present*/
    set: function(value) {
        this.val = value;
    }
});

var o = {d: 1};
Object.defineProperty(o, 'c', { /*error Setter is not present*/
    get: function() {
        return this.val;
    }
});
```

The following patterns are not considered problems with option `getWithoutSet` set:

在`getWithoutSet`设置下，以下模式被认为是没有问题的：

```js
/*eslint accessor-pairs: [2, { getWithoutSet: true }]*/
var o = {
    set a(value) {
        this.val = value;
    },
    get a() {
        return this.val;
    }
};

var o = {d: 1};
Object.defineProperty(o, 'c', {
    set: function(value) {
        this.val = value;
    },
    get: function() {
        return this.val;
    }
});

```

## When Not To Use It

You can turn this rule off if you are not concerned with the simultaneous presence of setters and getters on objects.

你可以关掉这个规则如果你不关心对象同时出现setter和getter。

## Further Reading

* [Object Setters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/set)
* [Object Getters](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/get)
* [Working with Objects](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Working_with_Objects)

## Version

This rule was introduced in ESLint 0.22.0.

此规则在ESLint 0.22.0中被引入。

## Resources

* [Rule source](https://github.com/eslint/eslint/tree/master/lib/rules/accessor-pairs.js)
* [Documentation source](https://github.com/eslint/eslint/tree/master/docs/rules/accessor-pairs.md)
