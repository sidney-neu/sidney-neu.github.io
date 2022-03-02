---
title: gperftools-程序性能分析的利器(Linux)
date: 2020-05-09 11:26:00
categories:
	-Linux
	-调试工具
---

gperftools是google出品的一个性能分析工具.它既可以将程序运行的内存情况输出到终端,也可以以流程图的形式展示程序运行中内存占用情况.

1.下载并安装libunwind+gperftools+graphviz

2.开启终端A:

​	(1)配置环境变量:

```
export LD_PRELOAD=/usr/local/lib/libtcmalloc.so
export HEAPPROFILE=<path to store heap file>
HEAPPROFILE=<head name prefix>
```


​	(2)运行程序至结束,期间会生成prefix_xxxx.0001.heap等文件

3.开启终端B:

​	(1).输出内存情况到终端或者文件:               

```
/usr/local/bin/pprof --text  ./<process>  <path to heap file>
```


​	(2).输出内存情况到gift图片文件:

```
/usr/local/bin/pprof --gif  ./<process>  <path to heap file> >> prof.gif
```