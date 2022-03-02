---
title: shell输出固定位数整数的方法
date: 2018-10-19 17:22:00
categories:
	-Linux
	-shell
---
Qos:

如何使用[shell](https://so.csdn.net/so/search?q=shell&spm=1001.2101.3001.7020)输出例如0001和0025这种固定位数的方法呢？

Ans：

例如需要输出0001，则可以将变量设为10001，然后不输出第一位。

```bash
a="10001" && echo "${a:1}"
0001
```