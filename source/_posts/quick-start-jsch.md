---
title: 基于Java的SFTP组件－JSCH
date: 2015-08-08 15:38:07
tags:
 - java
 - ssh2
categories:
 - java
---

Jsch（Java Secure Channel）是纯Java实现的SSH2库，允许使用端口转发、文件传输等。
<!-- more -->

## API ##

* public void put(String src, String dst) 	

``` bash
将本地文件名为src的文件上传到目标服务器，目标文件名为dst，若dst为目录，则目标文件名将与src文件名相同。
采用默认的传输模式：OVERWRITE
```

* public void put(String src, String dst, int mode) 	

``` bash
将本地文件名为src的文件上传到目标服务器，目标文件名为dst，若dst为目录，则目标文件名将与src文件名相同。
指定文件传输模式为mode（mode可选值为：ChannelSftp.OVERWRITE，ChannelSftp.RESUME，
ChannelSftp.APPEND）
 ```

* public void put(String src, String dst, SftpProgressMonitor monitor)
	
``` bash
将本地文件名为src的文件上传到目标服务器，目标文件名为dst，若dst为目录，则目标文件名将与src文件名相同。
采用默认的传输模式：OVERWRITE
并使用实现了SftpProgressMonitor接口的monitor对象来监控文件传输的进度。
```

* public void put(String src, String dst,SftpProgressMonitor monitor, int mode)
	
``` bash
将本地文件名为src的文件上传到目标服务器，目标文件名为dst，若dst为目录，则目标文件名将与src文件名相同。
指定传输模式为mode
并使用实现了SftpProgressMonitor接口的monitor对象来监控文件传输的进度。
```

* public void put(InputStream src, String dst) 	

``` bash
将本地的input stream对象src上传到目标服务器，目标文件名为dst，dst不能为目录。
采用默认的传输模式：OVERWRITE
```

* public void put(InputStream src, String dst, int mode) 	

``` bash
将本地的input stream对象src上传到目标服务器，目标文件名为dst，dst不能为目录。
指定文件传输模式为mode
```

* public void put(InputStream src, String dst, SftpProgressMonitor monitor)
	
``` bash
将本地的input stream对象src上传到目标服务器，目标文件名为dst，dst不能为目录。
采用默认的传输模式：OVERWRITE
并使用实现了SftpProgressMonitor接口的monitor对象来监控传输的进度。
```

* public void put(InputStream src, String dst,SftpProgressMonitor monitor, int mode)
	
``` bash
将本地的input stream对象src上传到目标服务器，目标文件名为dst，dst不能为目录。
指定文件传输模式为mode
并使用实现了SftpProgressMonitor接口的monitor对象来监控传输的进度。
```

* public OutputStream put(String dst) 	

```bash
该方法返回一个输出流，可以向该输出流中写入数据，最终将数据传输到目标服务器，目标文件名为dst，dst不能为目录。
采用默认的传输模式：OVERWRITE

```

* public OutputStream put(String dst, final int mode) 	

``` bash
该方法返回一个输出流，可以向该输出流中写入数据，最终将数据传输到目标服务器，目标文件名为dst，dst不能为目录。
指定文件传输模式为mode
```

* public OutputStream put(String dst, final SftpProgressMonitor monitor, final int mode)  	

``` bash
该方法返回一个输出流，可以向该输出流中写入数据，最终将数据传输到目标服务器，目标文件名为dst，dst不能为目录。
指定文件传输模式为mode
并使用实现了SftpProgressMonitor接口的monitor对象来监控传输的进度。
```

* public OutputStream put(String dst, final SftpProgressMonitor monitor, final int mode, long offset) 	

``` bash
该方法返回一个输出流，可以向该输出流中写入数据，最终将数据传输到目标服务器，目标文件名为dst，dst不能为目录。
指定文件传输模式为mode
并使用实现了SftpProgressMonitor接口的monitor对象来监控传输的进度。
offset指定了一个偏移量，从输出流偏移offset开始写入数据。
```

