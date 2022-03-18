---
title: vim配置
date: 2018-10-19 17:20:00
categories:
	-Linux
---

### vim

使用vim能提高代码编写的工作效率。

### 安装

```
apt-get install vim
```

### 常用命令

按ESC后，输入“:”，进行命令操作
 w 保存
 q 退出
 /[字符串] 查找字符串，然后按n查找下一个，N查找上一个
 ％s 替换，例：将整个文件里的abcd全部替换为efgh %s/abcd/efgh/g
 输入行号回车，转到行
 set paste 切换至粘贴模式，粘代码时不会自动补齐及自动注释
 set nu/set nonu 显示关闭行号

### 快捷操作

i 插入
x 删除（剪切）
dd 删除（剪切）一行
 yy 复制一行
 p 粘贴
 v 开始选中，可以移动光标选中
 $ 移到行尾
 0 移到行首
 D 从当前位置删除到行尾
 J 删除该行的换行符，与下一行变成一行
 u 撤消(命令red是重做)
 % 括号配对(){}等
 查找：光标移到单词上，按*，直接查找这个单词
 格式化对齐：按V后，移动光标，选中多行文本，按=

### 代码浏览

借助cscope和ctags能在vim中浏览代码，跳转函数，查找定义等

安装cscope和ctags:

```
apt-get install cscope
apt-get install exuberant-ctags
```

 转到代码目录执行：

```
cscope -Rbq; ctags -R
```

当项目为C语言项目的时候不会出问题，如果操作python项目的时候可能会出现如下错误：

```
cscope: no source files found
```

这种是因为默认情况下cscope仅仅会在当前目录下针对c、iex和yacc（扩展名分别为.c、.h、.I、.y）程序文件进行解析（如果指定了-R参数则包含其自身的子目录）。py文件不在这个范畴之内，因此需要在代码路径中执行以下命令（以python为例）：

```
find . -name '*.py' > cscope.files
cscope -Rbq; ctags -R
```



vim支持cscope的配置文件[vimcfg.tar.gz](https://pan.baidu.com/s/1JnMc5Ctz6_UjXdy6iiEUWw)(提取码：jqhm)解压到主目录

vim -t <函数名>直接能跳转到函数
 进入vim后，光标转到函数名上，快捷键：
 转到函数定义：Ctrl+] 对应命令cs f g <函数名>
 返回跳转：Ctrl+t
 转到调用处：Ctrl+\松开后按c
 全文查找：Ctrl+\松开后按e

F8函数变量定义列表
 F6,F7多窗口切换

### 块操作

按快捷键v后，可进行块操作，移动光标选择文本块，并可选择多行文本块，
 选定后可进行x删除（剪切）、y复制等操作。
 V(shift+v)选择整行；
 Ctrl+v可以选择整列进行操作。
 选择列后，按x删除一列；
 选择列后，依次按I，字符(可多个)，ESC。可以增加一列字符；