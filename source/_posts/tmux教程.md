---
title: tmux教程
date: 2021-10-19 21:20:00
categories:
	-Linux
---

### 安装tmux

以下以ubuntu操作系统举例，其他linux系统区别不大。

```
sudo apt-get install tmux
tmux -V                       
sudo apt-get install build-essential           
sudo apt-get install libevent-dev libncurses5-dev        
```

### 启动tmux

```
tmux                 （启动一个名为“session”的tmux）
exit                     （退出当前tmux）
```

### 创建一个命名的session

```
tmux new-session -s basic         （创建一个名为“basic”的session）
tmux new -s basic           （简化创建一个名为“basic”的session）
exit                     （退出当前tmux）
```

### session分离

Session的分离（Detaching）不会是session中的进程中断，而是仍在后台运行中。如果需要使用，可以连接到（Attaching）已经分离的session中。

```
tmux new -s basic           （简化创建一个名为“basic”的session）
top                 （监控内存与cpu用途）
Ctrl+b ➷ ➹ d➷           （从当前的session分离，返回到主页面）
```

### 重连一个已有session

```
tmux list-sessions                 （列出已有的session）
tmux ls                     （简化列出已有的session）
tmux attach                 （仅有一个session存在时的连接命令）
tmux new -s sessionname -d           （创建一个新tmux实例）
tmux attach -t sessionname            （连接到sessionname实例）
```

### 关闭session

可以在进入session后使用exit关闭相关session，也可以在使用命令关闭。

```
&      （关闭名为sessionname的session）
```

### 使用windows

windows是指在session中创建不同的窗口

```
tmux new -s windows -n shell         （创建名为windows的session，并且通过 –n 可以对window进行命名，以便于确认其身份）
Ctrl+b ➷ ➹ c➷             （在当前session下创建新的window）
Ctrl+b ➷ ➹ ，➷          （重命名当前window,“第三个按键为逗号”）
Ctrl+b ➷ ➹ n➷           （进去当前session的下一个window）
Ctrl+b ➷ ➹ p➷            （进入最近操作的那个window）
Ctrl+b ➷ ➹ 0➷         （进去当前session下命名为“0”的window中）
Ctrl+b ➷ ➹ f➷         （通过名字查找当前session下的window）
Ctrl+b ➷ ➹ w➷        （将当前session下的window列出，并选择进入）
```

### 关闭window

关闭window可以计入相应的window中，并在其中运行exit关闭，也可以使用快捷键关闭。

```
Ctrl+b ➷ ➹ &➷        （关闭当前window，其中&=shift+7）
```

1.5.1使用panes

创建名为panes的session，以便于理解panes是如何工作。

```
tmux new -s panes                （创建一个名为panes的session）
Ctrl+b ➷ ➹ %➷ tmux            （将panes切为左右两个，其中%=shift+5）
Ctrl+b ➷ ➹ “➷            （将panes切为上下两个，其中%=shift+’）
Ctrl+b ➷ ➹ 向上➷         （将panes切换到上面一个，可上下左右）
Ctrl+b+向上➷               （将当前panes向上扩大，可上下左右）
Ctrl+b ➷ ➹ o➷            （在当前window下的panes之间循环）
Ctrl+b ➷ ➹ 空格➷          （在当前window下的panes进行自动布局）
```

### 关闭panes

关闭panes可以计入相应的panes中，并在其中运行exit关闭，也可以使用快捷键关闭。

```
Ctrl+b ➷ ➹ x➷                 （关闭当前panes）
```

