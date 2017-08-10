---
layout:     post
title:      virtualbox建立共享文件夹
date:       2017-03-27
author:     HDB
header-img: img/post-bg-re-vs-ng2.jpg
catalog: true
tags:
    - Linux
---

系统 ： windows10   
软件 ： virtualbox 5.1.18
虚拟机安装的系统 : ubuntu16.04

1. 在windows的C盘底下建立一个名为share的文件夹

2. 在virtualBox中选择要操作的虚拟机，点击顶部的"设置"按钮，然后选择"共享文件夹"

3. 在添加共享文件夹窗口的共享文件夹路径选择刚创建的文件夹，即C盘底下的share. 共享文件夹名称设置为share，不要勾选"自动挂载"

4. 进入虚拟机中，在home目录下建立一个share文件夹

5. 在命令行工具里执行挂载操作 。
~~~
sudo mount -t vboxsf -o dmode=777 share /home/hdb/share
~~~

6. 完成。

7.设置开机自动挂载
在/etc/fstab 末尾加入
```
share /home/hdb/share vboxsf rw,dmode=777,auto 0 0
```