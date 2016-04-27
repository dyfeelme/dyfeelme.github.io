---
title: 版本控制工具-Git
date: 2016-04-19 09:18:53
tags:
 - 版本控制
 - git
categories:
 - 版本控制
---

## 简介 ##
Git是目前最为流行的分布式版本控制工具之一，有别于VCS、SVN等集中式版本控制系统，Git不需要单独提供集中管控的服务器，因此不存在单点故障或导致服务器数据丢失的致命缺陷。

## 分布式版本控制体系 ##
分布式版本控制体系，英文全称Distributed Version Control System，简称 DVCS。
特点：

* 记录快照而非差异
* 

## 常用命令 ##
```bash
usage: git [--version] [--help] [-C <path>] [-c name=value]
           [--exec-path[=<path>]] [--html-path] [--man-path] [--info-path]
           [-p | --paginate | --no-pager] [--no-replace-objects] [--bare]
           [--git-dir=<path>] [--work-tree=<path>] [--namespace=<name>]
           <command> [<args>]

These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   branch     List, create, or delete branches
   checkout   Switch branches or restore working tree files
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.

```

## 配置 ##
```bash
$ git config --list
初次使用推荐配置
$ git config --global user.name "xxx"
$ git config --global user.email xxx@xxx.com
配置默认文本编辑器
$ git config --global core.editor emacs [可选vim, vi等]
配置默认差异比较工具
$ git config --global merge.tool vimdiff [可选kdiff3，tkdiff，meld，xxdiff，emerge，vimdiff，gvimdiff，ecmerge，和 opendiff 等]
更多参考
$ git help config
```

## 入门 ##
``` bash
初始化，将当前项目纳入版本控制
$ git init
添加文件到版本控制
$ git add *.js
$ git add README
$ git add --all
查看当前版本状态
$ git status
提交变更
$ git commit -m "comment"
```

## 克隆 ##
``` bash
克隆仓库项目至本地,默认新建repo目录
$ git clone git://git.repo.com/repo.git
克隆仓库至本地指定目录
$ git clone https://github.com/dyfeelme/dyfeelme.github.io blog

```

## gitignore ##
如果想要让git忽略某些不关心或者不适合提交到版本控制的文件或目录，则需要通过配置.gitignore文件来指定。
```bash
用户级别的gitignore,一般存放在用户目录下，当然也可以在.gitconfig中指定其他位置。项目自定义的则存放于项目根目录（与.git目录同级），如下：
$ cat ~/.gitignore
*.swp
build
.DS_store
如上为用户级别的gitignore,指定了所有以.swp为后缀的文件，build目录和.DS_store目录。
$ cat project/.gitignore
.settings
build
*.iso
如上为项目级别的gitignore,其中指定了.settings目录,build目录和所有以.iso为后缀的镜像文件。
```
规则如下：
 > 所有空行或者以注释符号 ＃ 开头的行都会被 Git 忽略。
 > 可以使用标准的 glob 模式匹配。 * 匹配模式最后跟反斜杠（/）说明要忽略的是目录。 * 要忽略指定模式以外的文件或目录，可以在模式前加上惊叹号（!）取反。
 >所谓的 glob 模式是指 shell 所使用的简化了的正则表达式。星号（*）匹配零个或多个任意字符；[abc] 匹配任何一个列在方括号中的字符（这个例子要么匹配一个 a，要么匹配一个 b，要么匹配一个 c）；问号（?）只匹配一个任意字符；如果在方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如[0-9] 表示匹配所有 0 到 9 的数字）。

## 比较 ##
```bash
$ git diff 比较当前文件和暂存区域快照的差异
$ git diff --cache 或 --staged 比较暂存区域和上次提交版本快照的差异
```

## 移除&重命名 ##
``` bash
移除
$ git rm file 将文件从已跟踪文件清单中移除，区别于直接rm命令删除
重命名
$ git mv file newfile 重名名文件，虽然git不像svn等会记录文件改名操作，但git通过以下命令组合完成了改名操作
$ mv file newfile && git rm file && git add newfile
```

## 日志 ##
``` bash
$ git log 查看提交日志
可选参数
-p 按补丁格式显示每个更新之间的差异。
--stat 显示每次更新的文件修改统计信息。
--shortstat 只显示 --stat 中最后的行数修改添加移除统计。
--name-only 仅在提交信息后显示已修改的文件清单。
--name-status 显示新增、修改、删除的文件清单。
--abbrev-commit 仅显示 SHA-1 的前几个字符，而非所有的 40 个字符。
--relative-date 使用较短的相对时间显示（比如，“2 weeks ago”）。
--graph 显示 ASCII 图形表示的分支合并历史。
--pretty 使用其他格式显示历史提交信息。可用的选项包括 oneline，short，full，fuller 和 format（后跟指定格式）。
```

## 撤销 ##
``` bash
$ git reset
```

## 远程仓库 ##
```bash
$ git remote 列出每个远程库的简短名字
origin
-v 选项（译注：此为 --verbose 的简写，取首字母），显示对应的克隆地址
$ git remote -v
origin	https://github.com/dyfeelme/dyfeelme.github.io
```
## 分支 ##

## 合并 ##

## 进阶 ##

## 参考 ##
[Git命令](http://www.open-open.com/lib/view/open1328069733264.html#articleHeader16)