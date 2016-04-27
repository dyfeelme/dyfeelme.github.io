---
title: 使用Eclipse IDE
tags:
  - java
  - ide
  - eclipse
categories:
  - java
  - ide
date: 2014-04-14 19:00:21
---


## 快捷键 ###

### 比较重要的快捷键 ###
```code
代码助手:Ctrl+Space（简体中文操作系统是Alt+/）
快速修正：Ctrl+1
单词补全：Alt+/
打开外部Java文档：Shift+F2

显示搜索对话框：Ctrl+H
快速Outline：Ctrl+O
打开资源：Ctrl+Shift+R
打开类型：Ctrl+Shift+T
显示重构菜单：Alt+Shift+T

上一个/下一个光标的位置：Alt+Left/Right 
上一个/下一个成员（成员对象或成员函数）：Ctrl+Shift+Up/Down
选中闭合元素：Alt+Shift+Up/Down/Left/Right
删除行：Ctrl+D
在当前行上插入一行：Ctrl+Shift+Enter
在当前行下插入一行： Shift+Enter
上下移动选中的行：Alt+Up/Down


组织导入：Ctrl+Shift+O

### 定位 ### 
```code
2.1行内定位 
行末/行首：End/Home
前一个/后一个单词：Ctrl+Right/Left
2.2文件内定位 
跳到某行：Ctrl+L
上下滚屏：Ctrl+Up/Down
上一个/下一个成员（成员对象或成员函数）：Ctrl+Shift+Up/Down
快速Outline：Ctrl+O 
2.3跨文件定位 
打开声明：F3
打开资源：Ctrl+Shift+R
打开类型：Ctrl+Shift+T
在workspace中搜索选中元素的声明：Ctrl+G
在workspace中搜索选中的文本：Ctrl+Alt+G
在workspace中搜索选中元素的引用：Ctrl+Shift+G
打开调用层次结构：Ctrl+Alt+H
快速层次结构：Ctrl+T
反悔：Ctrl+Z
2.4其它 
上一个/下一个光标所在位置：Alt+Left/Right
上一个编辑的位置：Ctrl+Q 
```

### 选中快捷键 ###
```code
3.1行内选中 
选中到行末/行首：Shift+End/Home
选中上一个/下一个单词：Ctrl+Shift+Left/Right
3.2文件内选中 
选中闭合元素：Alt+Shift+Up
恢复到上一个选中：Alt+Shift+Down
选中下一个/上一个元素：Alt+Shift+Right/Left 
```


### 定位/选中/操作同时 ###
```code
删除行：Ctrl+D
删除下一个/上一个单词：Ctrl+Delete/Backspace
删除到行末：Ctrl+Shift+Delete
在当前行上插入一行：Ctrl+Shift+Enter
在当前行下插入一行： Shift+Enter
上下移动选中的行：Alt+Up/Down
拷贝选中的行：Ctrl+Alt+Up/Down 
```
 

### 代码编辑 ###
```code
保存：Ctrl+S
保存所有：Ctrl+Shift+S
下一个命中的项（搜索之后）：Ctrl+.
注释：Ctrl+/
添加导入：Ctrl+Shift+M
显示快捷键帮助：Ctrl+Shift+L
变为大/小写：Ctrl+Shift+X/Y
```

### 代码重构 ###
```code
显示重构菜单：Alt+Shift+T
重构-改变方法签名：Alt+Shift+C
重构-移动：Alt+Shift+V
重构-重命名：Alt+Shift+R 
```
 

### 编辑器、视图、透视图切换 ###
```code
下一个编辑器：Ctrl+F6
下一个视图：Ctrl+F7
下一个透视图：Ctrl+F8
最大化当前视图或编辑器：Ctrl+M
激活编辑器：F12 
```
### 调试 ###
```code
F5：Step Into（debug）
F6：Step over（debug）
F7：Step return（debug）
F8：Resume（debug）
F11：debug上一个应用（debug） 
```
 
### 方向键 ###
```code
Ctrl
前一个/后一个单词：Ctrl+Right/Left
上下滚屏：Ctrl+Up/Down
Alt
上一个/下一个光标的位置：Alt+Left/Right
上下移动选中的行：Alt+Up/Down
Shift
选中上一个/下一个字符：Shift+Left/Right
选中上一行/下一行（从当前光标位置开始）：Shift+Up/Down
Ctrl+Shift
上一个/下一个成员（成员对象或成员函数）：Ctrl+Shift+Up/Down
选中上一个/下一个单词：Ctrl+Shift+Left/Right
Alt+Shift
选中闭合元素：Alt+Shift+Up
恢复到上一个选中：Alt+Shift+Down
选中下一个/上一个元素：Alt+Shift+Right/Left
拷贝选中的行：Ctrl+Alt+Up/Down
Ctrl+Alt
拷贝选中的行：Ctrl+Alt+Up/Down 
```

### F类快捷键 ###
```
F2：显示提示/重命名
F3：打开选中元素的声明
F4：打开选中元素的类型继承结构
F5：刷新
F5：Step Into（debug）
F6：Step over（debug）
F7：Step return（debug）
F8：Resume（debug）
F11：debug上一个应用（debug）
F12：激活编辑器
```
## 插件 ##
### 安装方式 ###
常用的安装方式有三种
 
 * link文件安装，需离线，推荐。
 * 将插件目录中features和plugins目录中文件分别拷贝至eclipse安装目录中同名目录中，需离线，不推荐。
 * 通过Eclipse Marketplace进行在线安装，需联网，推荐。

普通插件插件推荐link方式
在eclipse安装目录新建links目录，编写xxx.link,内容如下：
```code
path=[插件绝对路径]，如C:/dev/eclipse-plugins/svn-1.8.22
或者
path=[相对路径]，如: ../eclipse-plugins/svn-1.8.22
注：相对路径为eclipse执行文件目录
```
### theme color ###
Update Site:
```code
http://eclipse-color-theme.github.com/update
```
效果图
![colorthemes](/images/howto-use-eclipse-colorthemes.png)


### subclipse ###
SVN代码管理的集成插件，下载地址：[]()
### propedit ###
Java Properties文件编辑插件
Update Site:
```code 
http://propedit.sourceforge.jp/eclipse/updates/
```
### checkstyle ###
![checkstyle](http://checkstyle.sourceforge.net/images/header-checkstyle-logo.png)
官网:http://checkstyle.sourceforge.net/


### emmet ###
![emmet](http://emmet.io/-/4076541266/i/logo.svg)
官网：http://emmet.io/
> Emmet is a plugin for many popular text editors which greatly improves HTML & CSS workflow

Updte Site:
```code
http://emmet.io/eclipse/updates/
```

注意：以上插件均可通过Eclipse Marketplace安装

## 问题 ##
* eclipse 4.4以后不支持maven2 版本，所以想要打包只能在系统命令行也执行。
