---
title: 打造自己的windows开发环境-chocolatey
tags:
  - windows
  - 开发环境
  - dotfiles
  - choco
categories:
  - howto
  - windows
  - choco
date: 2015-12-11 14:16:12
---


## 简介 ##
 > Chocolatey NuGet is a Machine Package Manager, somewhat like apt-get, but built with Windows in mind.
 喜大普奔的记下这个良心之作-chocolatey。

## 安装 ##

打开CMD命令提示符，执行以下命令
```cmd
@powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))" && SET PATH=%PATH%;%ALLUSERSPROFILE%\chocolatey\bin
```
或者打开PowerShell窗口，执行以下命令
```powershell
iex ((new-object net.webclient).DownloadString('https://chocolatey.org/install.ps1'))
```
注意：执行之前请设置powershell执行权限,通过管理员身份启动powershell执行环境，输入如下命令：
```powershell
Set-ExecutionPolicy RemoteSigned
```

## 命令概览 ##
输入choco --help打印命令
```cmd
This is a listing of all of the different things you can pass to choco.

Commands

 * list - lists remote or local packages
 * search - searches remote or local packages (alias for list)
 * install - installs packages from various sources
 * version - [DEPRECATED] will be removed in v1 - use `cup <pkg|all> -whatif` instead
 * pin - suppress upgrades to a package
 * update - [DEPRECATED] RESERVED for future use (you are looking for upgrade, these are not the droids you are looking for)
 * upgrade - upgrades packages from various sources
 * outdated - retrieves packages that are outdated. Similar to upgrade all --noop
 * uninstall - uninstalls a package
 * source - view and configure default sources
 * sources - view and configure default sources (alias for source)
 * feature - view and configure choco features
 * features - view and configure choco features (alias for feature)
 * unpackself - have chocolatey set it self up
 * pack - packages up a nuspec to a compiled nupkg
 * push - pushes a compiled nupkg
 * new - generates files necessary for a chocolatey package
 * apikey - retrieves or saves an apikey for a particular source
 * setapikey - retrieves or saves an apikey for a particular source (alias for apikey)
 * config - Retrieve and configure config file settings


Please run chocolatey with `choco command -help` for specific help on 
 each command.

How To Pass Options / Switches

You can pass options and switches in the following ways:

 * `-`, `/`, or `--` (one character switches should not use `--`)
 * **Option Bundling / Bundled Options**: One character switches can be
   bundled. e.g. `-d` (debug), `-f` (force), `-v` (verbose), and `-y` 
   (confirm yes) can be bundled as `-dfvy`.
 * ***Note:*** If `debug` or `verbose` are bundled with local options 
   (not the global ones above), some logging may not show up until after
   the local options are parsed.
 * **Use Equals**: You can also include or not include an equals sign 
   `=` between options and values.
 * **Quote Values**: When you need to quote things, such as when using 
   spaces, please use apostrophes (`'value'`). In cmd.exe you may be 
   able to use just double quotes (`"value"`) but in powershell.exe 
   you may need to either escape the quotes with backticks 
   (`` `"value`" ``) or use a combination of double quotes and 
   apostrophes (`"'value'"`). This is due to the hand off to 
   PowerShell - it seems to strip off the outer set of quotes.
 * Options and switches apply to all items passed, so if you are 
   installing multiple packages, and you use `--version=1.0.0`, choco 
   is going to look for and try to install version 1.0.0 of every 
   package passed. So please split out multiple package calls when 
   wanting to pass specific options.

Default Options and Switches

```
### 常用命令 ###

检索远程可用包
```cmd
choco search ruby
```
安装软件
```cmd
cinst ruby -y
choco install ruby -y
choco install ruby -y --force
```
卸载软件
```cmd
choco uninstall ruby
```
配置
```cmd
choco config list
choco config get key
choco config key value
```

## 配置 ##
配置包安装路径
可以通过设置环境变量ChocolateyBinRoot来改变,如图
![Setting](/images/howto-use-windows-choco-env.png)
配置包缓存路径
可以通过运行以下命令
```cmd
choco config set cacheLocation [path]
```
配置代理
可以通过运行以下命令
```cmd
choco config set proxy [url:port]
choco config set proxyUser [username]
choco config set proxyPassword [password]
```
[更多](https://github.com/chocolatey/choco/wiki/CommandsConfig)

## 进阶 ##
分享我自己的环境初始化脚本，参考官方文档：
文件名：setup.psl
```code
function Install-NeededFor {
param(
   [string] $packageName = ''
  ,[bool] $defaultAnswer = $true
)
  if ($packageName -eq '') {return $false}

  $yes = '6'
  $no = '7'
  $msgBoxTimeout='-1'
  $defaultAnswerDisplay = 'Yes'
  $buttonType = 0x4;
  if (!$defaultAnswer) { $defaultAnswerDisplay = 'No'; $buttonType= 0x104;}

  $answer = $msgBoxTimeout
  try {
    $timeout = 10
    $question = "Do you need to install $($packageName)? Defaults to `'$defaultAnswerDisplay`' after $timeout seconds"
    $msgBox = New-Object -ComObject WScript.Shell
    $answer = $msgBox.Popup($question, $timeout, "Install $packageName", $buttonType)
  }
  catch {
  }

  if ($answer -eq $yes -or ($answer -eq $msgBoxTimeout -and $defaultAnswer -eq $true)) {
    write-host "Installing $packageName"
    return $true
  }

  write-host "Not installing $packageName"
  return $false
}


# Install Chocolatey
if (Install-NeededFor 'chocolatey') {
  iex ((new-object net.webclient).DownloadString('http://chocolatey.org/install.ps1'))
  #set choco
  $cacheRoot = 'D:\cache'
  setx CacheRoot $cacheRoot
  $cachePath = Join-Path $cacheRoot  'chocolatey'
  choco config set cacheLocation $cachePath
  #set system env
  $chocoBinRoot = 'C:\ChocoBinRoot'
  setx ChocolateyBinRoot $chocoBinRoot
  if (!(Test-Path $chocoBinRoot)) {
    md $chocoBinRoot
  }
}

if (Install-NeededFor 'chocolateygui') {
  cinst chocolateygui -y
}

# install nuget, ruby.devkit, and ruby if they are missing
cinst nuget.commandline -y

if (Install-NeededFor 'ruby / ruby devkit') {
  cinst ruby -version 2.2.2 -y
  cinst ruby2.devkit -y
}


# restore the nuget packages
$nugetConfigs = Get-ChildItem '.\\' -Recurse | ?{$_.name -match "packages\\.config"} | select
foreach ($nugetConfig in $nugetConfigs) {
  Write-Host "restoring packages from $($nugetConfig.FullName)"
  nuget install $($nugetConfig.FullName) /OutputDirectory packages
}
```
调用以上脚本
文件名：start.cmd
```code
@echo off
SET DIR=%~dp0%
@PowerShell -NoProfile -ExecutionPolicy unrestricted -Command "& '%DIR%setup.ps1' %*"
pause
```

## 小结 ##
不说啦，只能帮你到这儿了。