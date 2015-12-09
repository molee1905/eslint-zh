---
title: Getting source code
layout: doc
---

# Source Code

ESLint is hosted at [GitHub](http://www.github.com) and uses [Git](http://git-scm.com/) for source control. In order to obtain the source code, you must first install Git on your system. Instructions for installing and setting up Git can be found at [http://help.github.com/set-up-git-redirect](http://help.github.com/set-up-git-redirect).

If you simply want to create a local copy of the source to play with, you can clone the main repository using this command:

    git clone git://github.com/eslint/eslint.git

If you're planning on contributing to ESLint, then it's a good idea to fork the repository. You can find instructions for forking a repository at [http://help.github.com/fork-a-repo/](http://help.github.com/fork-a-repo/). After forking the ESLint repository, you'll want to create a local copy of your fork.

# 源码

ESLint 被托管在 [GitHub](http://www.github.com)，使用 [Git](http://git-scm.com/) 作为版本控制工具。你需要在操作系统中安装 [Git](http://git-scm.com/) ，才能获取到源码。可以在 [http://help.github.com/set-up-git-redirect](http://help.github.com/set-up-git-redirect) 找到安装和配置 Git 的说明。

如果你仅仅想创建一个源码的本地副本，你可以使用此命令 clone 主干仓库。

    git clone git://github.com/eslint/eslint.git

如果你计划向 ESLint 贡献代码，那么 fork 此仓库是一个好的选择。你可以在 [http://help.github.com/fork-a-repo/](http://help.github.com/fork-a-repo/) 找到关于如何 fork 仓库的说明。在你 fork  ESLint 仓库后，你可以创建一个 fork 仓库的本地副本。

## Start Developing

Before you can get started developing, you'll need to have a couple of things installed:

* [Node.JS](http://nodejs.org)
* [npm](http://npmjs.org)

Once you have a local copy and have Node.JS and npm installed, you'll need to install the ESLint dependencies:

    cd eslint
    npm install

Now when you run `eslint`, it will be running your local copy and showing your changes.

**Note:** It's a good idea to re-rerun `npm install` whenever you pull from the main repository to ensure you have the latest development dependencies.

## 开始开发
在你开始开发之前，你需要安装一些软件。

* [Node.JS](http://nodejs.org)
* [npm](http://npmjs.org)

一旦你有一个本地的副本并且已经安装了 Node.JS and npm。你需要安装 ESLint 的依赖:

    cd eslint
    npm install

现在当你运行 `eslint` 命令，将会运行本地的副本并显示你的更改。

**Note:** 当你从主干仓库上 pull 代码后请重新运行 `npm install`，确保安装最新的开发者依赖。

## Directory structure


The ESLint directory and file structure is as follows:

* `bin` - executable files that are available when ESLint is installed
* `conf` - default configuration information
* `docs` - documentation for the project
* `lib` - contains the source code
    * `formatters` - all source files defining formatters
    * `rules` - all source files defining rules
* `tests` - the main unit test folder
    * `lib` - tests for the source code
        * `formatters` - tests for the formatters
        * `rules` - tests for the rules
