---
title: DGA简述
date: 2022-02-22 22:22:22
categories:
	-网络安全
	-攻击类型
---


### 一、DGA的定义

根据某安全厂商的定义，Fast-Flux僵尸网络通信所采用的域名一般被称为DGA域名，即通过特定算法随机生成的域名，是一种通过输入一些种子，包含字符串、数字、特定英文字典中的单词以及日期，利用加密算法（比如异或操作等），从而产生一系列伪随机字符串生成的域名。DGA域名是随机生成的，用于逃避域名黑名单检测技术。

DGA是英文Domain Generation Algorithm的缩写，中文翻译为域名生成算法。首先需要明确DGA指的是算法，这种算法的功能和目的就是可以生成域名，通过DGA生成的域名被称为AGD，英文Algorithmically-Generated Domain。根据[dgarchive](https://dgarchive.caad.fkie.fraunhofer.de/welcome/)的作者 [Daniel Plohmann](https://net.cs.uni-bonn.de/wg/cs/staff/daniel-plohmann/)2015年在第三届Botconf会议上的[报告](https://www.botconf.eu/wp-content/uploads/2015/12/OK-P06-Plohmann-DGArchive.pdf)内容，DGA最早在2008年被提出，当时被称为Domain Flux，到目前为止，DGA的家族种类已经超过70种，累计生成的域名超过1亿个。

### 二、DGA的种类

参考绿盟的[相关研究](https://www.secrss.com/articles/14369#:~:text=DGA%E7%AE%97%E6%B3%95%E7%94%B1%E4%B8%A4%E9%83%A8%E5%88%86%E6%9E%84%E6%88%90%EF%BC%8C%E7%A7%8D%E5%AD%90%EF%BC%88%E7%AE%97%E6%B3%95%E8%BE%93%E5%85%A5%EF%BC%89%E5%92%8C%E7%AE%97%E6%B3%95%EF%BC%8C%E5%8F%AF%E4%BB%A5%E6%A0%B9%E6%8D%AE%E7%A7%8D%E5%AD%90%E5%92%8C%E7%AE%97%E6%B3%95%E5%AF%B9DGA%E5%9F%9F%E5%90%8D%E8%BF%9B%E8%A1%8C%E5%88%86%E7%B1%BB%EF%BC%8CDGA%E5%9F%9F%E5%90%8D%E5%8F%AF%E4%BB%A5%E8%A1%A8%E7%A4%BA%E4%B8%BAAGD%EF%BC%88Algorithmically-Generated%20Domains%EF%BC%89%E3%80%82,2.1%20%E6%8C%89%E7%85%A7%E7%A7%8D%E5%AD%90%E8%BF%9B%E8%A1%8C%E5%88%86%E7%B1%BB)并根据个人经验，DGA的主要有两部分组成，分别是种子（seed）和针对种子的DGA处理算法。通过这两步，就可以生成一个DGA域名。

第一部分是种子，种子是DGA算法中最重要的输入参数之一，不同的种子即使采用相同的DGA处理算法，也可以生成不同的DGA域名。种子可以分为三种类型：

​	1.基于词典的种子，通过事先设定词典并通过一定的逻辑筛选其中的部分种子，通过排列组合就可以生成DGA域名；

​	2.基于时间的种子，DGA算法可以将时间信息作为输入种子，通过感染主机的系统时间、HTTP的响应时间，以及其他控制与被控端可以同时明确的时间都可以作为输入，生成对应的DGA域名；

​	3.其他动态数据作为种子，比如Bedep是以欧洲中央银行每天发布的外汇参考汇率作为种子，Torpig使用twitter的关键字作为种子，这些动态变化的数据只有在确定的时间窗口内注册域名才会生效；

通过Thomas Barabosch等人对DGA的[分析论文](https://net.cs.uni-bonn.de/fileadmin/user_upload/wichmann/Extraction_DNGA_Malware.pdf)中，的信息我们可以看出，有的种子是固定的，比如字典或者某一个固定的时间；有些种子是跟随时间动态变化的不可确定的种子。因此根据这种特性DGA域名可以分为四类：

1.TID（time-independent and deterministic），与时间不相关，可确定；

2.TDD（time-dependent and deterministic），与时间相关，可确定；

3.TDN（time-dependent and non-deterministic），与时间相关，不可确定；

4.TIN（time-independent and non-deterministic），与时间不相关，不可确定；

Daniel Plohmann在[技术分享](https://www.botconf.eu/wp-content/uploads/2015/12/OK-P06-Plohmann-DGArchive.pdf)中，对多个DGA家族基于以上的分类进行归纳总结，归纳结果如下图：

![DGA家族的分类](../images/DGA简述/企业微信截图_16460268114223.png)

### 三、DGA的用途

DGA的主要用于被恶意控制的被控端与黑客的控制端之间的C2通信。完成整个C2通信主要分为以下几个步骤：

​	step1：黑客在DGA生成的大量域名中找一个进行域名XXX.biz注册；

​	stdp2：被控端查询DGA生成的域名，通过查找碰撞找到域名XXX.biz对应的IP地址；

​	step3：通过连接IP地址向被控端服务器发送保活包并接受C2命令.

在这个工程中，第一、因为DGA生成的域名具有很强的伪随机性且随着时间和seed等信息不断变化，因此很难通过黑名单的方法进行拦截；第二、而且通过提前注册DGA生成的域名，就可以将IP地址隐藏起来，降低IP地址被黑名单拦截的风险。第三、DGA生成算法可以进行不断的更新迭代，通过嵌入特定的英文单词作为seed，域名看上去更加正常且具备一定的语义信息，提高了检测难度。

### 四、DGA的破绽

虽然DGA算法可以规避黑名单等检测方法，但是由于其独特的生成方法和DNS查询特点，还是存在明显的破绽。第一点就是每一次DGA会生成多个DGA域名，因此在这个过程当中会产生多于正常时候的NXDomain类型的DNS查询次数；第二，因为DGA生成的域名的主要作用就是为了找到控制端对应的IP地址，因此DGA生成的域名地址很少还会有子域名，域名的级数和子域名的个数都较少；第三，相比于正常域名DGA域名的长度更长，可读性更差。第四，鉴于用户的上网习惯，一般常用的DNS查询都会历史记录，但是DGA很可能是初测注册，因此大概率会是首次出现的DNS查询；第五，DGA生成的域名一般临时快速的，因此注册时间和被控端DNS查询之间的时间差会很短；第六，DNS的存活时间很短，一般是在1到7天。

以上的这些特点都可以通过不同的检测方法进行针对性的检测。其中包括机器学习的方法、异常检测的方法、以及阈值和正则的方法、以及DNS查询记录分析和Whois查询等多种方法。安全厂商可以根据不同安全产品的数据和计算能力，进行针对性分析。

### 五、DGA的检测方法

后续更新。
