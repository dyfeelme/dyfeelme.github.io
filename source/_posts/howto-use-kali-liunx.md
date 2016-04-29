---
title: 安全审计系统-Kali Linux
tags:
  - linux
categories:
  - linux
date: 2016-01-29 10:19:34
---


## 简介 ##
[Kali Linux](https://www.kali.org/)是一款基于Debain系统，并专注于安全领域的操作系统，设计用于数字取证和渗透测试。Kali Linux的前身为[BackTrack](http://www.backtrack-linux.org/)（简称BT）。

## 安装 ##
本文将介绍Kali Linux发行组推荐的Portable安装方式，即安装在便携存储设备的方式，我们需要准备如下工具：

* 安装有Linux系统或者Macos系统的电脑或者虚拟机,本文使用虚拟机进行。
* 容量大于8G的U盘。
* Kali Linux发行版的镜像文件。[下载地址](https://www.kali.org/downloads/)

步骤：

1. 备份优盘数据。__重要__,__重要__,__重要__
2. 拷贝镜像文件至当前Linux系统的用户目录,比如可以从windows拷贝至优盘，然后挂载至虚拟机，拷贝，或者在装有VMware Tools的虚拟机上拷贝。
此处常见问题：
	* 优盘不能挂载 - 检查设备版本和虚拟机设备版本是否一致，比如我的电脑为USB3.0接口，需要更改虚拟机设备参数为一致。
	* 文件无法拖动至虚拟机内 - 重装VMWare Tools或者重启虚拟机，使VMware Tools生效。
3. 打开Terminal窗口，输入以下命令：

```bash
$ sudo -i						#切换终端会话为root用户
# cd [镜像文件所在目录]
# fdisk -l						#查看设备状态
我的为/dev/sdb
# dd if=kali-linux-2016.1-amd64.iso of=/dev/sdb bs=512k
等待完成后会输出如下结果,大致如下
5823+1 records in
5823+1 records out
3053371392 bytes (3.1 GB) copied, 746.211 s, 4.1 MB/s
```
到此为止，我们Kali已经安装到我们的优盘了。
输入fdisk -l验证，此时我们看到/dev/sdb1和/dev/sdb2两个分区。

## 持久化 ##
我们启动Kali通过Live的方式是无法存储文件和配置的，Kali Linux提供了可存储的启动方式来帮助我们实现配置和文件的持久化。

依然如上面，我们先通过挂载优盘至虚拟机，然后同过fdisk来检测
```bash
# end=7gb
# read start _ < <(du -bcm kali-linux-1.0.8-amd64.iso | tail -1); echo $start
# parted /dev/sdb mkpart primary $start $end
```
上述命令创建了一个主分区，过程中会有一些警告提示，我们输入Ignore来忽略。
完成后我们可能需要弹出优盘，重新插拔优盘，然后重新挂载来生效。
然后输入fdisk -l来验证，正常情况会多出/dev/sdb3的分区。

Kali linux提供了普通和加密分区两种方式，本文选择加密的方式来处理，如下：

```bash
# apt install cryptsetup-bin
# cryptsetup --verbose --verify-passphrase luksFormat /dev/sdb3
提示输入两次密码来加密优盘分区
# cryptsetup luksOpen /dev/sdb3 my_usb
输入密码来解密优盘分区，此处可能会一直等待，不用理会。
```

开启另一个终端，重新以root用户身份登陆
```bash
# fdisk -l	检测解密优盘的挂载位置，我的为/dev/dm-0
# mkfs.ext3 -L persistence /dev/dm-0
# e2label /dev/dm-0 persistence
```
上述命令格式化加密分区，并设置了分区label为persistence

接下来我们将生成持久化配置到加密分区，如下：
```bash
# mkdir -p /mnt/my_usb
# mount /dev/dm-0 /mnt/my_usb
# echo "/ union" > /mnt/my_usb/persistence.conf
# umount /dev/dm-0
```

重新加密磁盘：
```bash
# cryptsetup luksClose /dev/dm-0
```

至此，带有加密分区可存储的便携启动系统制作完成。
{% img Kali启动界面 /images/howto-use-kali-linux-bootimg.png 600 450 %}

## 参考 ##
[Making a Kali Bootable USB Drive](http://docs.kali.org/downloading/kali-linux-live-usb-install)
[Kali Linux Live USB Persistence](http://docs.kali.org/downloading/kali-linux-live-usb-persistence)