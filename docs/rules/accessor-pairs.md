---
title: Rule accessor-pairs
layout: doc
---
<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->
# Enforces getter/setter pairs in objects (accessor-pairs)

# 强制getter/setter成对出现在对象中 (accessor-pairs)

It's a common mistake in JavaScript to create an object with just a setter for a property but never have a corresponding getter defined for it. Without a getter, you cannot read the property, so it ends up not being used.

在JavaScript中这是一个常见的错误，创建一个对象，对象中仅有一个setter设置属性，而没有定义对应的getter获取属性。没有getter，你不能读取属性，所以属性将终不会被使用。

Here are some examples:

这有些例子：

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

如果setters被定义而getters没有，此规则会给出警告。使用`getWithoutSet`选项，如果有一个getter而没有一个setter，它同样会给出警告。

## Rule Details

This rule enforces a style where it requires to have a getter for every property which has a setter defined.

对于每个属性，必须有一个getter和setter，这是此规则强制的编码风格。

By activating the option `getWithoutSet` it enforces the presence of a setter for every property which has a getter defined.

通过激活`getWithoutSet`选项，强制为每个定义了getter的属性提供对应的setter。


### Options

`getWithoutSet` set to `true` will warn for getters without setters (Default `false`).
`setWithoutGet` set to `true` will warn for setters without getters (Default `true`).

`getWithoutSet`设置为`true`，当有getters而没有setters，会给出警告（默认`false`）。

`setWithoutGet`设置为`true`，当有setters而没有getters，会给出警告（默认`true`）。

#### Usage

By default `setWithoutGet` option is always set to `true`.

`setWithoutGet`选项默认设置为`true`。

```json
{
    "accessor-pairs": [2, {"getWithoutSet": true}]
}
```

The following patterns are considered problems by default:

默认，以下模式被认为是有问题的：

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

默认，以下模式被认为是没有问题的：

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

在`getWithoutSet`选项设置时，以下模式被认为是有问题的：

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

在`getWithoutSet`选项设置时，以下模式被认为是没有问题的：

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

如果你对在对象里同时出现setters和getters不感兴趣，你可以关掉这个规则。

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
