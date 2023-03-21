---
title: ubuntu内核版本回退
date: 2020-12-16 21:26:00
categories:
	-Linux
---

查看当前内核：

```
uname -a
```


查看系统上的所有内核：

```
sudo dpkg --get-selections | grep linux
```


打开grub：

```
sudo vim /etc/default/grub
```


修改：

```
#GRUB_DEFAULT=0
GRUB_DEFAULT=GRUB_DEFAULT="Advanced options for Ubuntu>Ubuntu, with Linux <回退的版本号>" 
```


例如：GRUB_DEFAULT="Advanced options for Ubuntu>Ubuntu, with Linux 4.18.0-1737-oem"

grub2.0以下的版本书写方式如下：

```
GRUB_DEFAULT=GRUB_DEFAULT=”Ubuntu, with Linux 4.18.0-1737-oem“
```


更新grub：

```
sudo update-grub
```


重启系统。

内核版本回退可以解决由于内核升级导致软件不兼容的问题，例如VMware启动失败等情况。

参考：

[https://blog.csdn.net/DL_ChenBo/article/details/52400044?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromBaidu-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromBaidu-1.control](https://blog.csdn.net/DL_ChenBo/article/details/52400044?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromBaidu-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromBaidu-1.control)

[https://blog.csdn.net/qq_41897558/article/details/107160449](https://blog.csdn.net/qq_41897558/article/details/107160449)