---
title: Windows终端神器Cmder
tags:
  - 开发环境
  - windows
  - cmd
categories:
  - 开发环境
date: 2016-03-26 10:08:57
---


## 简介 ##
[Cmder](https://github.com/cmderdev/cmder)作为Windows命令提示符的替代者，可谓神级应用，没有之一。
当然它是基于开源神器ConEmu的，也算是集大成者吧。
所以如果你还没有转向macos,或linux之流,拥有如iTerm2之类的终端神器，
那cmder你值得拥有。

## 快捷键 ##
作为神器，你当然必须要知道驾驭它的要领，也就是快捷键，下面列出了几个最常用或者最酷炫的快捷键
```bash
Ctrl + `  [全局快捷键] 显示或隐藏Cmder至任务栏
Ctrl + t  新建一个Tab页，带选项
Alt + enter 全屏切换
Ctrl + w 关闭当前Tab,会弹出提示，确认关闭
```
更多请查看[官方文档](http://cmder.net/)

## 配置
邮件标题栏，或者使用快捷键Win+Alt+p打开设置面板，如图：
![Setting](/images/howto-use-windows-cmder-setting.png)

* 添加自定义Task

Startup -> Tasks 点击'+',添加一个默认的Task。

* 设置环境变量

Startup -> Environment 在面板逐行添加环境变量。

## 问题 ##
版本1.2.9 对 Virtualbox 5.0.16 可能 以上不兼容，具体原因不详，换用1.3.0beta版解决。

