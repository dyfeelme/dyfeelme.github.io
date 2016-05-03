---
title: 轻量级博客系统Jekyll
tags:
 - 博客
 - blog
categories:
 - 博客杂言
date: 2016-03-03 13:09:11
---

## 简介 ##
{% blockquote Jekyll http://www.jekyllcn.com %}
[Jekyll](http://jekyllcn.com/docs/home/) 是一个简单的博客形态的静态站点生产机器。它有一个模版目录，其中包含原始文本格式的文档，通过一个转换器（如 Markdown）和我们的 Liquid 渲染器转化成一个完整的可发布的静态网站，你可以发布在任何你喜爱的服务器上。
{% endblockquote %}
Jekyll也是Github官方推荐的博客系统，可以免费在[Github Page](https://pages.github.com/)建立属于自己的个人博客系统。

## 起步 ##
jekyll是基于ruby构建的，所以需要先安装ruby组件。当然一些插件也依赖于nodejs，请一并安装。
``` bash
$ gem install jekyll
$ jekyll new myblog
$ cd myblog
$ jekyll serve
=> Now browse to http://localhost:4000
```
注：

* 如果你希望把 jekyll 安装到当前目录，你可以运行 jekyll new . 来代替。
* 如果当前目录非空，你还需要增添 --force 参数，所以命令应为 jekyll new . --force。

## 命令概览 ##
``` bash
$ jekyll build
=> 当前文件夹中的内容将会生成到 ./_site 文件夹中。

$ jekyll build --destination <destination>
=> 当前文件夹中的内容将会生成到目标文件夹<destination>中。

$ jekyll build --source <source> --destination <destination>
=> 指定源文件夹<source>中的内容将会生成到目标文件夹<destination>中。

$ jekyll build --watch
=> 当前文件夹中的内容将会生成到 ./_site 文件夹中

$ jekyll serve
=> 一个开发服务器将会运行在 http://localhost:4000/ ,
	Auto-regeneration（自动再生成文件）: 开启。使用 `--no-watch` 来关闭。

$ jekyll serve --detach
=> 功能和`jekyll serve`命令相同，但是会脱离终端在后台运行。
   如果你想关闭服务器，可以使用`kill -9 1234`命令，"1234" 是进程号（PID）。
   如果你找不到进程号，那么就用`ps aux | grep jekyll`命令来查看，然后关闭服务器。[更多](http://unixhelp.ed.ac.uk/shell/jobz5.html).

```

## 目录结构 ##
``` bash
.
├── _config.yml
├── _drafts
|   ├── begin-with-the-crazy-ideas.textile
|   └── on-simplicity-in-technology.markdown
├── _includes
|   ├── footer.html
|   └── header.html
├── _layouts
|   ├── default.html
|   └── post.html
├── _posts
|   ├── 2007-10-29-why-every-programmer-should-play-nethack.textile
|   └── 2009-04-26-barcamp-boston-4-roundup.textile
├── _site
├── .jekyll-metadata
└── index.html
```

* _config.yml 保存配置数据。 
* _drafts 是未发布的草稿文章。这些文件的格式中都没有 title.MARKUP 数据。 
* _includes 放置可以重用的部分。
* _layouts 是存放布局模板的目录。布局可以在 YAML 头信息中根据不同文章进行选择。 
* _posts 是发布的文章目录。文件格式很重要，必须要符合: YEAR-MONTH-DAY-title.MARKUP。 永久链接 可以在文章中自己定制，但是数据和标记语言都是根据文件名来确定的。
* _data 存放格式化好的网站数据。jekyll 会自动加载在该目录下所有的 yaml 文件（后缀是 .yml, .yaml, .json 或者 .csv ）。这些文件可以经由 ｀site.data｀ 访问。如果有一个 members.yml 文件在该目录下，你就可以通过 site.data.members 获取该文件的内容。 
* _site 通过jekyll命令生成的网站页面默认保存在此处。
* .jekyll-metadata 该文件帮助 Jekyll 跟踪哪些文件从上次建立站点开始到现在没有被修改，哪些文件需要在下一次站点建立时重新生成。该文件不会被包含在生成的站点中。 

建议：以上目录中.jekyll-metadata和_site目录不需要提交至版本库，所以最好通过.gitignore来排除。

## 配置 ##
* Site Source	修改 Jekyll 读取文件的路径
* Site Destination 修改 Jekyll 写入文件的路径
* Safe 禁用 自定义插件。
* Exclude 转换时排除某些文件、文件夹
* Include 转换时强制包含某些文件、文件夹。.htaccess 是个典型的例子，因为默认排除 . 开头的文件。
* Keep files 当生成站点时，保留选择的文件。对文件不是由 jekyll 生成是有用的。例如由你的构建工具生成的文件或者资源。路径是相对于 destination 。 
* Time Zone 设置时区，这个设置作用于 TZ 变量， Ruby 用它来处理日期和时间。 IANA Time Zone Database 里边的都有效，比如 America/New_York 。默认值为操作系统的时区。 
* Encoding 设置文件的编码，仅 Ruby 1.9 以上可用。2.0.0　版本以后默认值为 utf-8，之前版本默认值为 nil，使用 Ruby 默认的 ASCII-8BIT。可以用命令 ruby -e 'puts Encoding::list.join("\n")' 查看 Ruby 可用的编码。 
* Defaults 设置 YAML 头信息 的默认值。 


## 发布 ##
我们使用Github Page作为免费的主机来部署博客系统，步骤如下：

* 在github上申请用户，新申请的用户名将作为博客的主机名，比如dyfeelme用户所对应的博客为dyfeelme.github.io
* 在github上建立仓库，仓库名为：用户名.github.io，如本博客的仓库名：dyfeelme.github.io
* 将jekyll生成的代码提交至master下

此时便可尝试访问。

## 总结 ##
Jekyll作为Github官方推荐的博客系统，简洁而且高效，同时定制性极强，官方提供了最新的文档。
以上内容均来自于Jekyll官方文档，[更多详情](http://jekyllcn.com/docs/home/)
