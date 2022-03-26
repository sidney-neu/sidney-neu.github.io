---
title: Docker安装
date: 2022-03-19 22:47:00
categories:
	-云原生
---

### 云原生的起源

### Docker的诞生

2008年dotCloud公司成立，该公司专注于PaaS平台为开发者或研发厂商提供技术服务。2013年Docker作为公共项目发布，同年dotCloud改名为Docker Inc，转型专注于Docker引擎和Docker生态系统。

在Docker的官网上有以下的介绍：

> Docker takes away repetitive, mundane configuration tasks and is used throughout the development lifecycle for fast, easy and portable application development – desktop and cloud. Docker’s comprehensive end to end platform includes UIs, CLIs, APIs and security that are engineered to work together across the entire application delivery lifecycle.

关于Docker的其他介绍可以参见笔者的另外一篇博客：[云原生简介](https://www.shenyong.zone/2022/03/12/%E4%BA%91%E5%8E%9F%E7%94%9F%E7%AE%80%E4%BB%8B/)。

### Docker的操作系统支持

Docker支持在多种操作系统上的安装和运行。

| Docker类型     | 操作系统 | 安装要求                                                     |
| -------------- | -------- | ------------------------------------------------------------ |
| Docker Server  | Linux    | X86架构：CentOS、Debian、Fedora、Ubuntu<br>ARM 64架构：CentOS、Debian、Fedora、Ubuntu<br>ARM 32架构：Debian、Raspbian、Ubuntu<br>Kernel版本>=3.10<br>iptables版本>=1.4 |
| Docker Desktop | Windows  | Windows10 64-bit家庭/专业版 2004 build19041<br>windows10 64-bit企业/教育版 1909 build18363<br>WSL2或Hyper-V后台模式 |
| Docker Desktop | Mac      | macOS版本大于10.14<br>不能同时安装VirtualBox版本4.3.30以上<br>4G以上内存<br>Apple自研芯片版本：加装Rosetta 2 |



### Ubuntu上安装Docker

笔者使用的操作系统是Ubuntu 20.04

删除存在的旧版本Docker：

```bash
sudo apt-get remove docker docker-engine docker.io containerd runc
```

安装前更新并安装依赖：

```
sudo apt-get update
sudo apt install apt-transport-https ca-certificates curl gnupg lsb-release
```

使用https获取仓库：

```bash
sudo apt-get install apt-transport-https ca-certificates curl gnupg lsb-release
```

添加Docker官方GPG key

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

添加Docker源：

```bash
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```

安装Docker(安装文件较大，需要一些时间)：

```
sudo apt update
sudo apt-get install docker-ce docker-ce-cli containerd.io
```

查看docker客户端版本

```
sudo docker version

Client: Docker Engine - Community
 Version:           20.10.13
 API version:       1.41
 Go version:        go1.16.15
 Git commit:        a224086
 Built:             Thu Mar 10 14:07:51 2022
 OS/Arch:           linux/amd64
 Context:           default
 Experimental:      true
Cannot connect to the Docker daemon at unix:///var/run/docker.sock. Is the docker daemon running?
```

上面最后一行的提示是因为Docker服务未启动，可以通过一下命令启动docker服务

```javascript
sudo service docker start 
```