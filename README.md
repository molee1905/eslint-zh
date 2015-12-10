# 翻译原则
1. 忠于作者表达的思想
2. 语句简洁通顺，符合中文读写习惯
3. 不主动、不刻意删减原文内容
4. 不主动、不刻意增加原文不存在的内容
5. 暂无法翻译的词或语句可保留原始英文
6. 规则里的  除一级标题（# xxx）外，其他标题不翻译：

   `## 二级标题`
   
   `### 三级标题`
   
   `#### 四级标题`
   
   `...`
7. 提交某文件时，假如该文件为xxx.md，
   则提交时的注释为: update xxx

   如有补充，逗号分隔紧随其后: update xxx, resolve the conflict...

### 下载eslint-zh


下载eslint-zh到本地目录，切换到mixed分支（对`.md`文档翻译时保留原始英文，以便校对）

```bash
$ git clone git@github.com:smocean/eslint-zh.git
$ cd eslint-zh
$ git checkout -b mixed origin/mixed
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

### 提交

确认无误后，提交到mixed
```bash
$ git pull
$ git add *
$ git commit -m 'update xxx'
$ git push origin mixed
```


[1]: https://rubygems.org/gems/bundler

---

# ESLint Web Site

This contains the code running on eslint.org.

## Pull Requests

Please note that all HTML documentation is split between this repository and the main [ESLint repository](https://github.com/eslint/eslint). Documentation for rules and APIs is located in the core repository, the rest is located in this repository. You can easily determine if original documentation file is native to website repository by checking for `<!-- Note: No pull requests accepted for this file. See README.md in the root directory for details. -->` comment just below the header of the markdown file. If that header is present, this file is located in the core ESLint repository and any pull requests should be send there. Otherwise, file is native to this site repository and can be fixed by creating a pull request in this repository.

## How to add your company/project logo to the site

* Create a fork of this repository
* Clone it locally
* Create a new branch
* Add your logo image to /img/logos/ directory. Logo should be at least 150px of height. Name your logo with your company/project name.
* Update /_data/logos.yml file and add an entry for your company with the name, url and src (should point to the logo you just added).
* Commit your changes to your fork and create a pull request into the main repository.

## License

MIT
