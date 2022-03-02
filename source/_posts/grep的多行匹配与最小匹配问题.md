---
title: grep的多行匹配与最小匹配问题
date: 2018-10-19 17:22:00
categories:
	-Linux
	-shell
---
grep匹配是linux的最常用的shell命令之一，grep的匹配的默认匹配为单行匹配和贪婪匹配，因此需要特殊的技巧将其转化为多行匹配和最小匹配。

### 1.多行匹配

```
cat aa.txt
aa
bb
aa
ff
cc
dd
ee
ff
aa
bb
```

多行匹配：

```
grep -zoe "start-string.*stop-string" file
```

举例来说：

```
grep -zoe "aa.*ff" aa.txt
aa
bb
aa
ff
cc
dd
ee
ff
```

### 2.grep最小匹配

grep最小匹配的方法与sed最小匹配的方法相同：

```
grep -o "strart-string[^stop-string]*stop-string" file
```

