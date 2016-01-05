title: 在树莓派上搭建inkpaper环境
date: 2016-01-05 18:10:00 +0800
author: me
cover:
draft: 
config:
    duoshuoKey: a-00006
tags:
    - code
    - raspberry Pi
    - inkpaper
preview: 

---

*注：本篇文章的编写，编译生成以及部署全部在树莓派上完成。*

<!--more-->

先简要介绍一下inkpaper。InkPaper（纸小墨）是一个使用GO语言编写的静态博客构建工具，可以快速搭建博客网站。优点是无依赖、跨平台，配置简单、构建快速，注重于简洁易用与排版优化。


本博客自从第二篇文章，就开始使用inkpaper了，拖了很长时间，早就该介绍一下如何在树莓派上搭建inkpaper环境了。


为了重新演示安装过程，我先卸载掉了安装好的go环境。重新开始。


简便起见，我们直接下载编译好的二进制文件就可以了。
因为某些众所周知的原因，golang的官网并不是很容易访问。好在国内还是有源的：[http://golangtc.com/download]


下载后缀为`linux-arm6.tar.gz`的版本即可。


下载完成后，使用`tar -xf`命令解压文件，然后如图所示放到`/usr/local/`目录下。


然后进入`/usr/local/go/bin`目录，你会看到`go`的二进制文件就在这里。


试试`./go`运行一下。正常。


为了在任何地方都能运行，并且能够正常使用`go`进行构建，还需要设置一下`PATH`。运行`sudo vim /etc/profile`进行编辑，添加如下内容:

    export GOROOT=
    export GOPATH=
    export GOBIN=
    export PATH=$PATH:$GOROOT:GOBIN

保存后重启X桌面环境，以便环境变量更改生效。重启后，执行`env`查看当前的环境变量。直接运行`go`，可以正常执行。
