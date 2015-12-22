---
title: New Rules
layout: doc
---
# New Rules

# 新建规则

ESLint is all about rules. For most of the project's lifetime, we've had over 100 rules, and that list continues to grow. However, we can't just accept any proposed rule because all rules need to work cohesively together. As such, we have some guidelines around which rules can be part of the ESLint core and which are better off as custom rules and plugins.

ESLint 全都由规则组成。在项目的大多数时间中，我们已经创建了超过100条规则，并且规则列表还在持续增加中。然而我们不能一味地接受这些提出的规则，我们需要这些规则在一起能协同工作。因此，我们制定了一些准则,它告诉我们哪些规则可以成为 ESLint 核心的一部分，哪些更适合作为自定义规则或插件。

## Core Rule Guidelines

In general, ESLint core rules must be:

一般而言，ESLint 核心规则必须是：

1. **Widely applicable.** The rules we distribute need to be of importance to a large number of developers. Individual preferences for uncommon patterns are not supported.

1. **适用广泛。** 我们发布的规则重点针对于大众的开发者，不支持小众的个人偏好。

1. **Generic.** Rules cannot be so specific that users will have trouble understanding when to use them. A rule is typically too specific if describing what it does requires more than two "and"s (if a and b and c and d, then this rule warns).

1. **通用性。** 规则不能太具体而导致用户使用过程中产生误解。如果一条规则需要2个以上的“and”来描述，那么它通常就是太具体了(if a and b and c and d, then this rule warns)。

1. **Atomic.** Rules must function completely on their own. Rules are expressly forbidden from knowing about the state or presence of other rules.

1. **原子性** 规则必须能完全依靠自己来工作。获取其他规则的状态或存在是明令禁止的。

1. **Unique.** No two rules can produce the same warning. Overlapping rules confuse end users and there is an expectation that core ESLint rules do not overlap.

1. **唯一性。** 两条规则不能产生相同的警告信息。重叠的规则混淆最终用户，我们期望核心 ESLint 规则绝不重叠。

1. **Library agnostic.** Rules must be based solely on JavaScript runtime environments and not on specific libraries or frameworks. For example, core rules shouldn't only apply if you're using jQuery but we may have some rules that apply only if you're using Node.js (a runtime).

1. **类库不确定性。**  规则必须完全运行在 JavaScript 运行时环境而不是其他类库或者框架。举一个例子，核心规则不应该仅仅在使用 jQuery 的环境中生效，但是我们可能有一些规则仅仅在你使用 Node.js(a runtime) 中生效。

1. **No conflicts.** No rule must directly conflict with another rule. For example, if we have a rule requiring semicolons, we cannot also have a rule disallowing semicolons (which is why we have one rule, `semi`, that does both).

1. **无冲突。** 规则之间绝对不能有直接的冲突。举个例子，如果我们有一个规则依赖分号，我们就不会有其他规则禁用分号（which is why we have one rule, `semi`, that does both）。

Even though these are the formal criteria for inclusion, each rule is evaluated on its own basis.

尽管这些规则都已经纳入正式的标准，但是每条规则都通过了以上规则的评估。

## Proposing a Rule

If you want to propose a new rule, [create an issue](https://github.com/eslint/eslint/issues/new?body=**When%20does%20this%20rule%20warn%3F%20Please%20describe%20and%20show%20example%20code%3A**%0A%0A**Is%20this%20rule%20preventing%20an%20error%20or%20is%20it%20stylistic%3F**%0A%0A**Why%20is%20this%20rule%20a%20candidate%20for%20inclusion%20instead%20of%20creating%20a%20custom%20rule%3F**%0A%0A**Are%20you%20willing%20to%20create%20the%20rule%20yourself%3F**%0A%0A) be sure to include:

如果你想提出一条新规则，[新建一个议题（issue）](https://github.com/eslint/eslint/issues/new?body=**When%20does%20this%20rule%20warn%3F%20Please%20describe%20and%20show%20example%20code%3A**%0A%0A**Is%20this%20rule%20preventing%20an%20error%20or%20is%20it%20stylistic%3F**%0A%0A**Why%20is%20this%20rule%20a%20candidate%20for%20inclusion%20instead%20of%20creating%20a%20custom%20rule%3F**%0A%0A**Are%20you%20willing%20to%20create%20the%20rule%20yourself%3F**%0A%0A) 请确保包含以下几点：


1. When the rules will warn. Include a description as well as sample code.
1. 当这些规则发生警告时，请包涵类似于示例代码的描述。
1. Whether the rule prevents an error or is stylistic.
1. 这条规则会防止一种错误或者是规范代码风格。
1. Why the rule should be in the core instead of creating a custom rule.
1. 为什么这条规则应该属于核心规则而不是一个自定义规则。
1. Are you willing to create the rule yourself?
1. 你愿意自己创建这条规则吗？

We need all of this information in order to determine whether or not the rule is a good core rule candidate.

我们需要所有这些信息来判断它是否满足核心规则的候选要求。

## Resource Limitations

Please keep in mind that we receive a lot of rule proposals and the ESLint team is completely a volunteer team that works in its free time to maintain ESLint. As a result, even if we like the idea for a rule, we may not have the resources to implement it. You greatly increase the likelihood of getting a new core rule into ESLint if you are willing to implement it yourself. The team is very good at guiding first-time contributors through the rule creation process.

请牢记我们接受了许多规则提案，ESLint 团队是一支由完全由志愿者组成的团队，他们用业余时间维护 ESLint。因此，即使我们喜欢这条规则，我们也许没有资源去实现它。如果你愿意自己实现这条规则，这将会大大增加它成为 ESLint 核心规则的可能性。这个团队非常善于指导首次贡献者完成规则创建过程。

## Creating Your Own Rules

Remember that ESLint is completely pluggable, which means you can create your own rules and distribute them using plugins. We did this on purpose because we don't want to be the gatekeepers for all possible rules. Even if we don't accept a rule into the core, that doesn't mean you can't have the exact rule that you want. See the [working with rules](../working-with-rules) and [working with plugins](../working-with-plugins) documentation for more information.

请记住，ESLint 是完全插件化的这意味着你可以创建自己的规则并将它们用插件的方式分发出去。我们有意为之因为我们不愿意做所有可能性规则的守门人。即使我们不能接受这条规则为核心规则，它也并不意味着你不能拥有自己想要的附加规则。你可以从[working with rules](../working-with-rules) 和[working with plugins](../working-with-plugins) 的文档中找到更多信息。
