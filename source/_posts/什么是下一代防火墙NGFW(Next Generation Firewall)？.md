---
title: 什么是下一代防火墙NGFW(Next Generation Firewall)？
date: 2020-12-12 16:21:00
categories:
	-网络安全
	-安全产品
---

下一代防护墙（Next Generation Firewall, 简称 NGFW），在2007年Gartner提出了这一概念。两年后的2009年，Gartner正式发布了《[Defining the Next-Generation Firewall](https://www.gartner.com/en/documents/1204914/defining-the-next-generation-firewall)》，对下一代防火墙的定义做了明确说明。相对于IPS、VPN等当时现有安全产品，NGFW给人的感觉就是：我全都要！

![20201212162217968](../images/什么是下一代防火墙NGFW(Next Generation Firewall)？/20201212162217968.jpeg)

NGFW在诞生之初作为一个全新的概念和产品形态，为边界类的安全产品的发展指明了方向。然而这个为安全厂商指明发展方向的标准却是有一个咨询公司定义，不仅是一个由一个咨询公司定义还收到了国内外安全厂商的普遍认可。随着相关技术的不断成熟和完善，已经不在是一个概念。很多国内安全大厂已经在参照的等报的合规标准逐渐完善标准和安全功能和检测性能。并逐渐依托自身的特点完成产品的孵化和发展。目前国内的安全大厂已经完成了NGFW的产品化。

华为：

[https://e.huawei.com/cn/products/enterprise-networking/security](https://e.huawei.com/cn/products/enterprise-networking/security)

深信服：

[https://www.sangfor.com.cn/zh-CN/product-and-solution/sangfor-security/22](https://www.sangfor.com.cn/zh-CN/product-and-solution/sangfor-security/22)

山石网科：

[https://www.hillstonenet.com.cn/product-and-service/border-security/ngfw/](https://www.hillstonenet.com.cn/product-and-service/border-security/ngfw/)

绿盟科技：

[https://www.nsfocus.com.cn/html/2019/197_0909/113.html](https://www.nsfocus.com.cn/html/2019/197_0909/113.html)

下一代防火墙的关键特点：

1.满足国内市场的《网络安全等级保护基本要求》

以安全资质打开市场，以安全能力保护安全。

2.高效的并行处理能力，提高检测效率。区别于传统的UTM等网关类的防护安全产品的串行检测，NGFW有“一次解包，并行检测”的能力，举例来说，一次解包可以实现协议分析、策略匹配、用户识别、内容识别等多功能的并行处理。

3.多种安全能力的一体化能力，提高检测范围。现有不同的边界防护安全产品存在很多的功能重复，因此如果将一体化的安全防护能力集成到一起，综合IPS、WAF、VPN、UTM等防护功能的众家之长，去除冗余实现一次部署一体防御。

4.结合人工智能、数据分析等新技术的全新威胁检测技术。检测技术的多样化也是NGFW的一个重要特点，无论是AI和威胁情报的全新检测技术，还是大数据和威胁情报分析相结合的分析技术，都可以提高对APT、恶意软件、0Day等攻击的检测能力。

5.高速稳定的流量处理速度，包括支持IPv6、多种NAT的多种地址形式和多种地址转换方法。针对IPv4的地址枯竭以及IPv6的逐渐兴起，NGFW要对IPv6以及地址转换等流量场景有高速稳定的处理能力。