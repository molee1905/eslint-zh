### 校对原则
1. 忠于作者表达的思想
2. 语句简洁通顺，符合中文读写习惯
3. 不主动、不刻意删减原文内容
4. 不主动、不刻意增加原文不存在的内容
5. 暂无法翻译的词或语句可保留原始英文
6. 使用“你”，不使用“您”
7. 使用“它”，“它们”；不使用“他”，“她”，“他们”，“她们”
8. 英文和数字与中文之间要留空格，中文标点符号和中文之间不需要留空格
9. 提交某文件时，假如该文件为xxx.md，
   
   则提交时的注释为: update xxx

   如有补充，逗号分隔紧随其后: update xxx, resolve the conflict...

### 认领
在 issue：[All Task](https://github.com/smocean/eslint-zh/issues/15) 中选择未被认领的任务，在 issue：[Apply for a task](https://github.com/smocean/eslint-zh/issues/16) 中进行回复，格式如下：

```
**Application:** `file path`

// 如果 file path 为cla/index.md，则如下：

**Application:** `cla/index.md`
```
如果申请格式正确，管理员会在第一时间回复：
```
  thanks @your name: `cla/index.md`
```
如果你收到此回复或看到 issue：[Apply for a task](https://github.com/smocean/eslint-zh/issues/16)中你选择的已被管理员设置为选中，你就可以开始了。

**注意：**原则上每次只能申领一个任务，每个任务不超过**1周**，对于较长篇幅，一般不超过**2周**。

### 下载eslint-zh

fork [eslint-zh](https://github.com/smocean/eslint-zh)

下载eslint-zh到本地目录，切换到alpha分支

```bash
$ git clone git@github.com:[your name]/eslint-zh.git
$ cd eslint-zh
$ git checkout -b alpha origin/alpha
```

### 修改文件

### 本地预览

在本地进行调试预览，安装[bundler][1] ，如果已安装，可跳过此步：
```bash
$ [sudo] gem install bundler
$ bundle -h
```
下载需要等待一段时间，国内可先替换一下，再安装bundler:
```bash
$ gem sources --add https://ruby.taobao.org/ --remove https://rubygems.org/
$ gem sources -l
```

安装依赖包
```bash
$ bundle install
```
启动jekyll
```bash
$ jekyll server
```
然后访问 http://127.0.0.1:4000/

### 提交到自己的仓库

确认无误后，提交到alpha
```bash
$ git pull
$ git add -A
$ git commit -m 'update xxx'
$ git push origin alpha
```

然后pull request。

### 发pull request
在md文件顶部
```
---
title: List of available rules
layout: doc
---
```
加上译者的github名和你的github名：
```
---
title: List of available rules
layout: doc
translator: translator's github ID
proofreader: your github ID
---
```
**注意：**合并的是`alpha`，也就是`[your name]:alpha`向`smocean:alpha`分支发出合并请求。

[1]: https://rubygems.org/gems/bundler



### 参考
英文 | 中文 
------ | :-----
pluggable | 插件化的
by default | 默认地
style guideline | 风格指南
require | 要求
disallow | 不允许、禁止
enforce | 强制
issue | 议题（issue）
pull request | 合并请求（pull request）
upstream | 上游（upstream）
rebase | [衍合](http://git-scm.com/book/zh/v2/Git-%E5%88%86%E6%94%AF-%E5%8F%98%E5%9F%BA)（rebase)
This rule aims to do| 该规则旨在
squash your commits | 压缩你的提交

* The following patterns are considered problems:
* 以下模式被认为是有问题的：

* The following patterns are considered errors: 
* 以下模式被认为是有错误的：

* The following patterns are considered valid:
* 以下模式被认为是有效的：

* The following patterns are not considered problems:
* 以下模式被认为是没有问题的：

* The following patterns are not considered errors:
* 以下模式被认为是正确的：

* The following patterns do not cause a warning: 
* 以下模式不会引起警告：

* This rule was introduced in ESLint 0.0.9.
* 该规则在ESLint 0.0.9 中被引入。

* No empty labels (no-empty-label)
* 禁止使用空标签 (no-empty-label) (此处No是不允许、禁止的意思，同disallow)




