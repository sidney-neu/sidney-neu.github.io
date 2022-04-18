---
title: 如何在C语言中使用tensorflow（三）测试
date: 2020-05-16 19:38:00
categories:
	-AI工程化框架
---

本文主要介绍tensorflow的cpu版本的C语言使用方法。

下载libtensorflow对应版本后，可以测试libtensorflow在当前环境下是否可用。

测试代码路径：

DIR：

    |--lib:
    	|--libtensorflow.so
    	|--libtensorflow_framework.so
    
    |--include:
    	|--/include/tensorflow/c/c_api.h
    	|--/include/tensorflow/c/LICENSE
    
    |--src:
    	|--test.c
    	|--Makefile

测试代码test.c：

```
#include <stdio.h>
#include <tensorflow/c/c_api.h>

int main() {
  printf("Hello from TensorFlow C library version %s\n", TF_Version());
  return 0;
}
```


Makefile文件:

```
INC=-I../include
LIB=-L../Lib \
        -ltensorflow \
	-ltensorflow_framework 
SRC=test.c
CC=gcc
all:
	${CC}  ${SRC} ${INC} ${LIB} -o test
clean:
	rm test
```


编译过程：

```
make     #编译生成可执行文件
make clean     #删除可执行文件
```


运行可执行文件test：

```
./test
Hello from TensorFlow C library version 1.15.0
```


至此，动态库版本与硬件版本匹配完成。 