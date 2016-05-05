---
title: 优雅的折腾Mac系统
date: 2013-09-01 15:39:04
tags:
 - macos
 - apple
categories:
 - 开发环境
---

本文收录了一些macos上开发所用到的技巧和相关软件，仅为作者个人偏好。
<!-- more -->

## 包管理 ##
Mac平台提供了应用商店来管理和购买软件，一般开发工具和一些非主流的工具并没有在该商店提供，所以作为开发者，我们经常需要手动去下载软件包（*.dmg）来安装，所以Homebrew这样的神器就出现了。
homebrew可以提供主流开发包的一键下载和安装，并且通过cask提供了APP的下载，如下：

``` bash
$ brew install curl wget vim git ...
$ brew cask install java eclipse-jee firefox ...
```

所以我们需要在mac上安装如上的工具：

```bash
$ /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

获取 cask

``` bash
$ brew tap caskroom/cask
```

## 常用工具 ##

* 浏览器类
	* firefox : brew cask install firefox/firefox-cn
	* google-chrome : brew cask install google-chrome
* 编辑器类
	* sublime text : brew cask install sublime-text
	* atom : brew cask install atom
	* mou : brew cask instal mou
* 开发套件
	* eclipse : brew cask install eclipse-jee
	* Intellij IDEA : brew cask install intellij-idea
	* WebStorm : brew cask install webstorm
* 系统工具
	* iterm2 : brew cask install iterm2
	* f.lux : brew cask install f.lux
* 数据库工具
	* navicate : brew cask install navicate-mysql
	* 

## oh-my-zsh ##
[oh-my-zsh]()丰富了枯燥的bash,zsh等，通过各种主题和插件的集成提供了强大的shell操作，如图:
{% img oh-my-zsh http://ohmyz.sh/img/themes/nebirhos.jpg %}

安装：
``` bash
$ sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
或者
$ sh -c "$(wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O -)"
```
配置：
oh-my-zsh默认的配置文件是用户目录下的.zshrc文件。