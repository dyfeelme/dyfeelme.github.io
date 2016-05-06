---
title: 构建跨平台APP-Meteor
date: 2016-01-05 18:15:48
tags:
 - nodejs
 - android
 - ios
categories:
 - NodeJS
---


[Meteor](https://www.meteor.com/) 是一款开源的跨平台项目开发框架，可以快速适配Web,手机，桌面等平台。
<!-- more -->

## 快速开始 ##
``` bash
安装：
linux/osx:curl https://install.meteor.com/ | sh
windows: https://install.meteor.com/windows
创建项目：
meteor create whatsapp
```

## 命令概览 ##
``` bash
Usage: meteor [--release <release>] [--help] <command> [args]
       meteor help <command>
       meteor [--version] [--arch]

With no arguments, 'meteor' runs the project in the current
directory in local development mode. You can run it from the root
directory of the project or from any subdirectory.

Use 'meteor create <path>' to create a new Meteor project.

Commands:
   run                [default] Run this project in local development mode.
   debug              Run the project, but suspend the server process for debugging.
   create             Create a new project.
   update             Upgrade this project's dependencies to their latest versions.
   add                Add a package to this project.
   remove             Remove a package from this project.
   list               List the packages explicitly used by your project.
   add-platform       Add a platform to this project.
   remove-platform    Remove a platform from this project.
   list-platforms     List the platforms added to your project.
   build              Build this project for all platforms.
   lint               Build this project and run the linters printing all errors and warnings.
   shell              Launch a Node REPL for interactively evaluating server-side code.
   mongo              Connect to the Mongo database for the specified site.
   reset              Reset the project state. Erases the local database.
   deploy             Deploy this project to Meteor.
   logs               Show logs for specified site.
   authorized         View or change authorized users and organizations for a site.
   claim              Claim a site deployed with an old Meteor version.
   login              Log in to your Meteor developer account.
   logout             Log out of your Meteor developer account.
   whoami             Prints the username of your Meteor developer account.
   test-packages      Test one or more packages.
   test               Test the application
   admin              Administrative commands.
   list-sites         List sites for which you are authorized.
   publish-release    Publish a new meteor release to the package server.
   publish            Publish a new version of a package to the package server.
   publish-for-arch   Builds an already-published package for a new platform.
   search             Search through the package server database.
   show               Show detailed information about a release or package.

See 'meteor help <command>' for details on a command.

```

## Android 平台##
增加android平台支持
``` bash
$ meteor add-platform android
```

## IOS 平台##
增加IOS平台支持
``` bash
$ meteor add-platform ios
```

## 模板 ##
替换默认模板blaze为angular
``` bash
$ meteor remove blaze-html-templates
$ meteor add angular-templates
$ meteor add dab0mb:ionic-assets
$ meteor npm install ionic-scripts --save
$ meteor npm install angular-meteor --save
```
