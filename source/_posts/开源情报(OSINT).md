---
title: 开源情报(OSINT)
date: 2023-08-13 18:26:00
categories:
	-网络安全
    -威胁情报
---

# 1.开源情报简介

开源情报（OSINT）——是指从公开可获得的来源收集信息及其分析以产生可操作的情报。OSINT的范畴不仅限于网络安全，还包括企业、商业和军事情报或其他信息重要的领域。

无论你是招聘人员、营销经理、网络安全工程师，还是仅仅是一个好奇的人阅读这篇文章，你都会发现对自己有用的东西。也许你想知道你的哪些数据可以被其他人发现，或者仅仅想查看与你在线联系的个人或组织是否合法。在本文中，我将解释如何发现一个人的数字足迹、执行数字调查以及收集信息以进行竞争情报或渗透测试。

目前有许多[OSINT工具](https://osintframework.com/)可供使用，因此我不打算涵盖它们全部，仅介绍最流行的工具以及在所描述的用例中有用的工具。在本指南中，我展示了一种通用方法以及你可以根据要求和你拥有的初始数据使用的不同工具和方法。如果你无法定义你的调查起点——请阅读下面的文章。

[我想在网上找到某个人，我该从何开始？](https://www.osintteam.com/i-need-to-find-someone-online-where-to-start/?source=post_page-----5029a3c7fd56--------------------------------)

开源情报的步骤：

1.从你知道的信息开始入手(email, username, etc.)

2.定义需求（你想得到什么信息）

3.收集数据

4.分析收集的数据

5.使用新收集的数据，根据需要进行透视

6.验证假设

7.生成报告

# 2.利用真实姓名

## 1.真实姓名开源情报流程

![real name](开源情报(OSINT)/real-name.jpg)

## 2.政府资源利用

有许多网站可以找到关于个人或组织的信息，而且根据国家的不同，信息的公开程度也可能有所不同。我不打算详细写这方面的内容，因为我提供的政府资源对你来说可能不太相关，毕竟你是另一个国家的居民。只需记住这样的资源是存在的，在需要时可以通过谷歌搜索找到它们，尤其是使用我下面描述的高级搜索查询，这并不难。

## 3.Google Dorks

2002年，Johnny Long开始收集Google搜索查询，这些查询揭露了易受攻击的系统或敏感信息泄露。他将它们称为Google Dorks。由于本文讨论的是合法获得的信息，我不会展示如何获取未授权的访问权限，但是你可以探索拥有数千个不同查询的Google Hacking Database。下面的查询可能返回通过简单搜索难以定位的信息。

```
“john doe” site:instagram.com — 引号强制Google搜索进行绝对精确匹配，同时在Instagram上进行搜索。
“john doe” -“site:instagram.com/johndoe” site:instagram.com — 隐藏目标自己账户的帖子，但显示他们在Instagram其他帖子上的评论。
“john” “doe” -site:instagram.com — 显示完全匹配给定名字和姓氏的结果，但以不同组合形式出现。同时排除Instagram的结果。
“CV” OR “Curriculum Vitae” filetype:PDF “john” “doe” — 搜索包含“CV”或“Curriculum Vitae”并且是PDF格式的目标简历。
```

如果你对拼写100%确定，可以用引号将单个单词括起来，因为默认情况下Google会尝试将你的关键词转换成大众想要的内容。顺便说一下，关于Instagram有趣的是，使用正确的Google Dork，你可以看到私人账户的评论和点赞。

![Google Dorks](开源情报(OSINT)/google_dorks.jpg)

使用高级搜索查询在Bing、Yandex和DuckDuckGo上进行搜索，因为其他搜索引擎可能会给你Google无法提供的结果。

## 4.人物搜索

有专门进行人物搜索的网站，可以提供真实姓名、用户名、电子邮件或电话号码进行搜索。

```
https://www.spokeo.com
https://thatsthem.com
https://www.beenverified.com
https://www.fastpeoplesearch.com
https://www.truepeoplesearch.com
https://www.familytreenow.com
https://people.yandex.ru
```

人物搜索网站允许退出，但在人们将自己从名单中删除后，其他新的搜索服务可能会出现他们的记录。原因是同一数据集被不同服务购买和使用。一些公司拥有这些数据集，即使在他们的一个网站上人们删除了列表，在新域名上旧数据又重新出现，因此之前删除的个人资料又在搜索中出现。因此，如果人们做得很好地清理了他们的信息，你只需等待新数据库出现。找到选择退出的人的方法之一是去人物搜索服务，找到一个独特的段落，对其进行引用的Google搜索，找到该公司拥有的所有域名。有可能你的目标从网站A删除的信息现在在网站B上。

[人物搜索.如何根据姓名和姓氏找到一个人](https://www.osintteam.com/people-search-how-to-find-a-person-by-name-and-surname/?source=post_page-----5029a3c7fd56--------------------------------)

# 3.利用用户名

## 1.用户名开源情报流程

![username](开源情报(OSINT)/username.jpg)

首先，我们需要找到一个用户名。通常是姓名加姓氏的组合，或者由电子邮件、个人使用或拥有的网站域名衍生而来。从你拥有的数据开始，反向查找你需要的信息。显然，最简单的方法是用Google搜索你目前已知的任何相关数据，尝试找到带有用户名的页面。此外，你可以使用专门的网站进行反向用户名搜索，如socialcatfish.com, usersearch.org, peekyou.com。

## 2.Google Dorks

我之前展示的用于真实姓名搜索的同样Google Dorks，在搜索用户名时也很有用。此外，URL搜索可能会给你好的结果因为通常URLs中会包含用户名。

```
inurl:johndoe site:instagram.com — 在Instagram上搜索包含johndoe的urls
allinurl:john doe ny site:instagram.com — 在Instagram的网页中搜索包含john doe ny的url，这个关键字与inurl相似，但支持多词搜索
```

根据您的搜索的复杂性以及使用以前的方法的有效程度，您可能需要生成一个单词列表。 当您需要尝试很多选项时，它很有用，因为您不清楚用户名应该是什么，但有很多猜测。 可以使用[这个 Python 脚本](https://gist.github.com/superkojiman/11076951)来生成下面的单词列表：

```python

#!/usr/bin/env python3

'''
NameMash by superkojiman
Generate a list of possible usernames from a person's first and last name. 
https://blog.techorganic.com/2011/07/17/creating-a-user-name-list-for-brute-force-attacks/
'''

import sys
import os.path

if __name__ == '__main__': 
    if len(sys.argv) != 2:
        print(f'usage: {sys.argv[0]} names.txt')
        sys.exit(0)

    if not os.path.exists(sys.argv[1]): 
        print(f'{sys.argv[1]} not found')
        sys.exit(0)

    with open(sys.argv[1]) as f:
        for line in enumerate(f): 

            # remove anything in the name that aren't letters or spaces
            name = ''.join([c for c in line[1] if  c == ' ' or  c.isalpha()])
            tokens = name.lower().split()

            if len(tokens) < 1: 
                # skip empty lines
                continue
            
            # assume tokens[0] is the first name
            fname = tokens[0]

            # remaining elements in tokens[] must be the last name
            lname = ''

            if len(tokens) == 2: 
                # assume traditional first and last name
                # e.g. John Doe
                lname = tokens[-1]

            elif len(tokens) > 2: 
                # assume multi-barrelled surname
                # e.g. Jane van Doe

                # remove the first name
                del tokens[0]

                # combine the multi-barrelled surname
                lname = ''.join([s for s in tokens])

            # create possible usernames
            print(fname + lname)           # johndoe
            print(lname + fname)           # doejohn
            print(fname + '.' + lname)     # john.doe
            print(lname + '.' + fname)     # doe.john
            print(lname + fname[0])        # doej
            print(fname[0] + lname)        # jdoe
            print(lname[0] + fname)        # djoe
            print(fname[0] + '.' + lname)  # j.doe
            print(lname[0] + '.' + fname)  # d.john
            print(fname)                   # john
            print(lname)                   # joe
```

![wordlist](开源情报(OSINT)/wordlist.gif)

## 3.用户名搜索

有很多网站提供用户名搜索，我发现这里边最好的两个网站：instantusername.com 和 namechk.com。 通常，一项服务可以找到其他服务无法找到的帐户，因此最好同时使用这两个网站。 除了在线服务之外，您还可以使用 [WhatsMyName](https://github.com/WebBreacher/WhatsMyName) — 一个 Github 项目，也被包含在更高级的工具中：Spiderfoot 和 Recon-ng。 但是，您可以将其用作运行 Python 脚本的独立检查器。

![usernamesearch](开源情报(OSINT)/usernamesearch.gif)

当进行搜索时，你可能会获取到误报，因为会有别的人使用相同的用户名，因此需要对此有所准备。

注意：当运行WhatsMyName以及其他本地安装的工具时，某些网站可能会被ISP服务商锁定导致异常，在这种情况下，你需要使用proxy来解决这些异常。另外为了避免暴漏你自己你可以使用匿名者。

[SOCMINT：像夏洛克福尔摩斯一样搜索用户名](https://www.osintteam.com/socmint-search-usernames-like-sherlock-holmes/?source=post_page-----5029a3c7fd56--------------------------------)

# 4.利用邮件地址

## 1.邮件地址开源情报流程

![email](开源情报(OSINT)/email.jpg)

## 2.Google Dorks

```
    “@example.com” site:example.com — 根据一个指定的域名搜索所有的邮件地址
    HR “email” site:example.com filetype:csv | filetype:xls | filetype:xlsx — find HR contact lists on a given domain.根据一个给定的域名发现HR的联系方式列表
    site:example.com intext:@gmail.com filetype:xls — 冲一个给定的域名中提取电子邮件的ID
```

## 3.Email tools

[Hunter](https://hunter.io/) - 对电子邮件的域名进行快速扫描并揭示其通用模式；

[Email permutator](http://metricsparrow.com/toolkit/email-permutator/#) - 生成最多三个域名的排列，目标可能在其中拥有电子邮件地址，支持多个变量输入以生成自定义结果。

[Proofy](https://proofy.io) - 允许批量电子邮件验证，当你使用排列工具生成电子邮件列表并希望立即检查所有电子邮件时，这非常有用。

[Verifalia](https://verifalia.com/validate-email) - 免费且免注册的验证单个邮件地址，若要使用批量验证，必须注册。

## 4.浏览器插件

[Prophet](https://chrome.google.com/webstore/detail/prophet/alikckkmddkoooodkchoheabgakpopmg) - 揭示更多关于人的信息。它使用先进的引擎，根据姓名、公司和其他社交数据预测给定人员最有可能的电子邮件组合。然后，Prophet会验证生成的电子邮件，以确保其正确且可送达。

[OSINT browser extension](http://www.osintbrowser.com/) - 包含许多有用的链接，包括用于电子邮件搜索和验证的链接。与Firefox和Chrome兼容。

 [LinkedIn Sales Navigator](https://chrome.google.com/webstore/detail/linkedin-sales-navigator/hihakjfhbmlmjdnnhegiciffjplmdhin) - Chrome插件，可直接在Gmail中显示关联的Twitter帐户和丰富的LinkedIn个人资料数据。

## 5.受损的数据库

数据泄露已成为一个大问题，最近我们看到越来越多的数据窃取转储。安全研究员特洛伊·亨特（Troy Hunt）收集了已发布的数据，剥离了密码，为他们参与的违规行为分配了电子邮件，并将其上传到 [haveibeenpwned.com](https://haveibeenpwned.com/)。虽然违规本身的事实可能并不那么重要，但重要的是，通过电子邮件，您可能会获得该人使用或至少使用过的服务列表。

另一种选择是使用 [dehashed.com](https://dehashed.com/)。使用免费帐户时，它的工作方式类似于 Troy Hunt 的网站，但在有效订阅中，它会以明文或密码哈希显示密码。从 OSINT 的角度来看，我们需要它来搜索这些邮箱地址否在其他网站上使用过——这是找出该人使用或至少使用过哪些服务的另一种方法。通过密码或其哈希值进行搜索，不仅会显示使用哪个网站，还会显示与其关联的电子邮件地址。因此，我们可以获得目标的电子邮件，否则我们无法获得。需要注意的是，如果密码不是唯一的，我们可能会得到误报，因为其他人也可能使用目标邮件地址。

[你的电子邮件揭示了什么？终极邮箱调查指南](https://www.osintteam.com/learn-to-investigate-email-addresses/?source=post_page-----5029a3c7fd56--------------------------------)

# 5.利用电话号码

## 1.电话号码开源情报流程

![phone](开源情报(OSINT)/phone.jpg)

有时，人们会将电话号码和电子邮件链接到他们的 Facebook 个人资料，因此在 Facebook 搜索中输入它可能会向您显示个人资料。另一种选择是查找用户提供的电话号码数据库，例如 [whocalledme.com](https://www.whocalledme.com/)。该数据库不仅限于美国，还可以查看来自欧洲的数字。此外，对于那些想要这样的东西但在移动设备上的人来说，有几个应用程序：[privacystar.com](https://privacystar.com/index.html)、[getcontact.com](https://www.getcontact.com/) 和 [everycaller.com](http://www.everycaller.com/)。有许多反向电话查找服务，它们通常是针对特定国家/地区的，因此请找到适合您需求的服务。

## 2.PhoneInfoga

[PhoneInfoga](https://github.com/sundowndev/PhoneInfoga) 是仅使用免费资源扫描电话号码的最先进工具之一。目标是首先以非常高的准确性收集任何国际电话号码的基本信息，例如国家、地区、运营商和线路类型。然后尝试确定VoIP提供商或在搜索引擎上搜索足迹以尝试识别所有者。

特征：

​	1.检查电话号码是否存在且可能
​    2.收集标准信息，例如国家/地区、线路类型和运营商
​    3.一次检查多个号码
​    4.使用外部 API、Google Hacking、电话簿和搜索引擎进行 OSINT 侦察
​    5.使用自定义形式进行更有效的 OSINT 侦测

![PhoneInfoga](开源情报(OSINT)/PhoneInfoga.gif)

## 3.安卓模拟器

许多 Android 应用程序可以在模拟器上稳定运行，但有些应用程序可能无法正常运行。例如，在 [freephonenum.com](https://freephonenum.com/) 上测试Viber 的 VoIP 电话号码存在问题。但是，在模拟器上运行应用程序有很多优点：您的真实帐户或电话号码将是安全的，因为您不必在手机上安装有问题的应用程序，并且您可以轻松欺骗 GPS 坐标。

将号码保存在手机中，然后查看 Viber 或 WhatsApp 联系人列表。这些服务允许添加照片、传记和所有者姓名，只需知道电话号码即可提取此信息。

[Bluestacks ](https://www.bluestacks.com/)- 主要为游戏玩家制作，但也运行其他应用程序。适用于 Windows、Mac 和 Linux，不需要虚拟机进行设置，因此安装比 Genymotion 更容易。

[Genymotion](https://www.genymotion.com/fun-zone/) — 被开发人员广泛使用，但也有供个人使用的免费版本。适用于 Windows、Mac 和 Linux，并有一系列虚拟设备可供选择。使用英特尔技术的本指南来设置仿真器。

[AMIDuOS](http://android-emulators.com/amiduos) — 仅适用于 Windows，并利用系统中的设备驱动程序在 Android 中实现接近原生的性能。它速度快，安装简单。但是，虽然上述模拟器可以免费安装，但 AMIDuOS 的价格为 10 美元。

# 6.利用域名

1.域名开源情报流程

![domain](开源情报(OSINT)/domain.jpg)

如果个人或组织拥有一个网站，您应该知道如何获取有关它的信息。调查可能会揭示正在使用的操作系统、软件版本、个人联系信息等。我不得不提的是，建议在不“接触”目标环境的情况下进行调查，这种技术称为被动侦察——涉及使用工具和资源的足迹，这些工具和资源可以帮助获取有关目标的更多信息，而无需直接与之交互。下面我将介绍在保持隐藏的同时获取信息的方法。

## 1.Google Dorks

Google Dorks 是一种被动的信息收集方法，上面已经提到过。在这里，我将展示哪些查询在域调查期间可能有用。

```
site：example.com — 将搜索限制为特定网站或域。
filetype：DOC — 返回 DOC 文件或其他指定类型，如 PDF、XLS 和 INI。通过用“|”分隔扩展名，可以同时搜索多个文件类型。
intext：word1 — 搜索包含您正在搜索的特定单词的页面和网站。
allintext： word1 word2 word3 — 搜索页面或网站中的所有给定单词。
related：example.com — 将列出与指定网页“相似”的网页。
site：*.example.com — 显示所有子域。星号在搜索查询中充当一个或多个完整单词的替代品。
```

## 2.Whois信息

Whois 提供有关互联网资源（例如域名、IP 地址块或自治系统）的注册用户或受让人的信息。有许多 Whois 资源，这些是好的：[whois.icann.org](https://whois.icann.org/en) 和 [whois.com](https://www.whois.com/)。

## 3.反向Whois信息

反向 Whois 为您提供了在其 Whois 记录中具有相同组织名称或电子邮件地址的域列表。例如，如果您正在调查一家名为“John Doe Inc.”的公司，您可以看到在“John Doe Inc.”下注册的所有其他域名。我最喜欢的网站之一是 [viewdns.info](https://viewdns.info/) 因为它有一个广泛的工具包，包括[反向 whois](https://viewdns.info/reversewhois/) 查找。

## 4.相同的 IP地址

通常，发现与目标网站在同一台服务器上运行的站点会发现有价值的信息。例如，您可能会找到子域或开发站点。通常，托管此站点的服务提供商也负责其他服务——可以使用 www.atsameip.intercode.ca 和 www.sameip.org 来检查。

## 5.被动DNS

仅使用 DNS 记录，您可以查看哪个 IP 解析为名称或哪个名称解析为 IP。有时这还不够，这就是被动DNS记录派上用场的地方。它们允许检查解析为研究 IP 的所有名称，因此您可以构建有用的解析历史记录。我最喜欢的产品是 [RiskIQ 社区版](https://community.riskiq.com/home)，因为它提供的不仅仅是被动 DNS，而是更多信息。[VirusTotal](https://www.virustotal.com/) 或 [SecurityTrails](https://securitytrails.com/) 也可用于此目的。

## 6.Internet 存档和缓存

[WaybackMachine](http://web.archive.org/) 可用于查找以前版本的网页，使人们能够查看网站之前的外观或恢复已删除的页面。

[Archive.today](http://archive.is/) 是网页的另一个时间胶囊，能够手动将实时 URL 快照添加到存档中。

在某些情况下，已删除的页面未存档，但仍被搜索引擎缓存。它们可以在 [cachedview.com](http://cachedview.com/) 上找到，或者您可以使用以下 Google 查询请求缓存版本：cache：website.com。在 Google 上没有找到任何内容？检查其他搜索引擎的缓存，但请记住，缓存显示的是上次将页面编入索引的时间。因此，您可能会收到缺少图像和过时信息的页面。

[visualping.io](https://visualping.io/) — 一种监控服务，可在选定时间截取网页的屏幕截图，并在发生更改时向您发送电子邮件警报。

## 7.网站声誉、恶意软件和推荐分析

声誉对于了解您正在与谁打交道以及网站是否值得信任都比较重要。如果有任何怀疑，使用免费的在线工具进行恶意活动检查可能会为您省去在 VM 中打开网站或执行其他预防措施的麻烦。引荐分析是对向内和向外 HTML 链接的搜索。尽管自行进行测试不会获得精确的结果，但它仍然是可能向您显示关联域名的方法之一。

www.siteworthtraffic.com — 分析网站流量（用户、页面浏览量）并估计它可以通过广告产生多少收入。
www.alexa.com — 分析网站流量和竞争对手，展示他们做得更好的地方，并提供有关 SEO 改进的建议。
www.similarweb.com — 分析工具，提供有关网站或移动排名、性能、流量来源等的深入信息。最重要的是，它进行推荐分析。
https://sitecheck.sucuri.net — 扫描网站以查找已知恶意软件、黑名单状态、网站错误和过时软件。
www.quttera.com — 提供免费的恶意软件扫描，并提供全面的报告，包括恶意文件、可疑文件、黑名单状态等。
www.urlvoid.com — 帮助您检测潜在的恶意网站。此外，它还提供有关域（IP 地址、DNS 记录等）的更多信息，并将其与已知的黑名单进行交叉引用。

## 8.物联网搜索引擎

IoT（物联网）搜索引擎向您显示连接到网络空间的设备——想想谷歌搜索，但适用于连接互联网的设备。为什么有用？例如，您可以请求有关开放端口、应用程序和协议的可用信息，而不是使用 Nmap 主动扫描端口和服务。[Shodan.io](https://www.shodan.io/) 是最受欢迎的互联网扫描器，具有公共 API 并与许多安全工具集成。对于营销人员来说，它提供了有关产品用户及其所在位置的数据。安全研究人员使用它来发现易受攻击的系统并访问各种物联网设备。还有其他替代品，比如 [Censys](https://www.censys.io/)，或者国内的类似引擎—[Fofa](https://en.fofa.info/) 和 [ZoomEye](https://www.zoomeye.org/)。

# 7.利用位置搜索

![location](开源情报(OSINT)/location.jpg)

## 1.地理定位工具

[Creepy](http://www.geocreepy.com/) 是一款免费工具，允许从社交网络和图像托管服务收集数据以进行位置研究。商业选择是 [Echosec](https://www.echosec.net/)，每月花费近 500 美元。

## 2.基于 IP 的地理定位

基于 IP 的地理位置是 IP 地址或 MAC 地址到实际地理位置的映射。有许多网站将 IP 地址映射到位置，其中之一是 [iplocation.net](https://www.iplocation.net/)。当您知道此人之前连接过的 WI-FI 接入点时，请使用 [wigle.net](https://wigle.net/index) 绘制这些接入点的地图，并在 Google 地球上进行更详细的研究。

## 3.一些有用的网站

www.emporis.com — 建筑数据库，提供来自世界各地的建筑物图像。可能有助于确定图片上的建筑物。
http://snradar.azurewebsites.net — 搜索带有地理标记的公共帖子 VKontakte 并按日期过滤它们。
http://photo-map.ru — 允许搜索带有地理标记的VKontakte帖子，作为以前的服务，但需要授权。
www.earthcam.com — 拥有和运营的实时流媒体网络摄像头的全球网络，在位置研究期间可能很有用。
www.insecam.org — 在线安全摄像头的目录。摄像机的坐标是近似值，指向 ISP 地址，而不是摄像机的物理地址。

# 8.利用图片

当您有一张图片并想知道它在哪里使用或它何时首次出现时，请使用 [Google 图片](https://images.google.com/)、[必应图片](http://www.bing.com/images/discover?FORM=ILPMFT)和[百度图片](http://image.baidu.com/)进行**反向图像搜索**。此外，[TinEye](http://tineye.com/) 的算法设计与 Google 的算法不同，因此可以返回不同的结果。为什么有用？作为调查员，您可以通过头像找到此人，因为人们通常不会费心更改他们使用的各种社交网络的个人资料图片。作为记者，您可以执行图像搜索与过滤配对以揭露假新闻。例如，使用早于所述事件的日期筛选器范围搜索的事件当天拍摄的照片无法更早找到。因此，如果图像被发现——它是在事件发生之前创建的，因此它是假的。如果您需要在社交网络上进行狭窄的搜索，通过Vkontakte 的 [Findclone](https://findclone.ru/) 和 [Findmevk.com](https://findmevk.com/) 获取联系方式或 Reddit 的 [karmadecay](http://karmadecay.com/) 可以完成这项工作。此外，值得一提的是浏览器扩展：适用于 Chrome 的 [RevEye](https://chrome.google.com/webstore/detail/reveye-reverse-image-sear/keaaclcjhehbbapnphnmpiklalfhelgf?hl=en) 和适用于 Firefox 的[图像搜索选项](https://addons.mozilla.org/en-US/firefox/addon/image-search-options/)。像 [CamFind](https://camfindapp.com/) for iOS 这样的移动应用程序可能会帮助您从物理世界中搜索事物。此外，还有[一个图像识别项目](https://www.imageidentify.com/)，可以使用人工智能识别图像上的内容。

图像本身包含许多有用的信息，例如相机信息、地理协调等——它被称为 EXIF 数据，如果不删除它，您可能会发现很多有趣的信息。例如，使用地图地理编码来找出照片的拍摄地点。使用相机序列号，您可以查看互联网上是否有使用该相机拍摄的照片——[stolencamerafinder.com](https://www.stolencamerafinder.com/)。图像编辑工具允许查看元数据。如果您不想安装复杂的程序：[Exiftool](https://exiftool.org/) — 跨平台免费软件可能是您正在寻找的东西。第三种选择是在线查看EXIF数据：[exifdata.com](http://exifdata.com/) 或 [viewexifdata.com](http://www.viewexifdata.com/)。要删除EXIF数据，您可以使用本地安装的工具：[exifpurge.com](http://www.exifpurge.com/) 或在线执行：[verexif.com](https://www.verexif.com/en/)。

您是否需要执行图像取证并确定图像是否被篡改？使用[Forensically](https://29a.ch/photo-forensics/#forensic-magnifier) 或 [FotoForensics](http://fotoforensics.com/)。如果您不想在线上传图像，可以在本地运行 [Phoenix](https://github.com/ebemunk/phoenix) 或 [Ghiro](http://www.getghiro.org/)。后者比上述在线工具自动化程度更高，并为您提供更多功能。除此之外，在处理图像时，您可能需要对其进行去模糊处理或提高质量，因此这里有一些增强工具：

[Smartdeblur](http://smartdeblur.net/) — 恢复运动模糊并消除高斯模糊。有助于恢复焦点并改善图像，从而带来惊人的效果。
[Blurity](https://www.blurity.com)  — 只专注于去模糊图像，不像以前的工具那样提供那么多选项，并且仅在 Mac 上可用。
[Letsenhance.io](https://letsenhance.io/) — 使用 AI 在线增强和升级图像。

[如何根据图片去找到一个人，反向图片搜索的秘密](https://www.osintteam.com/how-to-find-anyone-by-photo-the-secrets-of-reverse-image-search/?source=post_page-----5029a3c7fd56--------------------------------)

# 9.SOCMINT

SOCMINT 是 OSINT 的一个子集，专注于社交媒体平台上的数据收集和监控。我已经描述了一些社交媒体情报技术。在这里，我将通过列出更多工具来完成描述。

[社交媒体情报-实战技巧和工具](https://www.osintteam.com/social-media-intelligence-socmint-practical-tips-tools/?source=post_page-----5029a3c7fd56--------------------------------)

## 1.脸书

[ExractFace](https://sourceforge.net/projects/extractface/) — 从 Facebook 中提取数据，使其可离线用作证据或执行高级离线分析。
[Facebook 睡眠统计](https://github.com/sqren/fb-sleep-stats) — 根据用户在线/离线状态估计睡眠模式。
[lookup-id.com](https://lookup-id.com/) — 帮助您查找个人主页或群组的 Facebook ID。

## 2.Twitter

[Twitter高级搜索](https://twitter.com/search-advanced) — 嗯，这是不言自明的:)
[TweetDeck](https://tweetdeck.twitter.com/) — 为您提供一个仪表板，显示 Twitter 帐户不同的活动列。例如，您可能会在屏幕上的一个位置看到主页动态、通知、私信和活动的单独列。
[Trendsmap](https://www.trendsmap.com/) — 向您显示来自世界任何地方的 Twitter 上最受欢迎的趋势、主题标签和关键字。
[Foller](https://foller.me/) — 为您提供有关任何公开 Twitter 个人资料的丰富见解（提及到个人资料公开信息、推文和关注者数量、主题、主题标签等）。
[Socialbearing](https://socialbearing.com/) — 免费的 Twitter 分析和搜索包括推文、时间线和 Twitter 地图。按参与度、影响力、位置、情绪等查找、筛选和排序推文或人员。
[Sleepingtime](http://sleepingtime.org/) — 显示 Twitter 公共账号的睡眠时间表。
[Tinfoleak](https://tinfoleak.com/) — 显示 Twitter 用户使用的设备、操作系统、应用程序和社交网络。此外，它还显示地点和地理位置坐标，以生成所访问位置的跟踪地图。在 Google 地球中绘制用户推文地图等。

## 3.Instagram

www.picodash.com — 将所选用户的关注者统计信息或所选 hastag 的统计信息导出到电子表格 （CSV）。此外，它还导出点赞和评论。
https://web.stagram.com — 在线图像和视频查看器/下载器。
https://codeofaninja.com/tools/find-instagram-user-id — 获取用户 ID。 用户名可能会更改，因此了解个人资料的 ID 对于不丢失页面很有用。
http://instadp.com — 以全尺寸显示个人资料描述。
https://sometag.org — 搜索热门主题标签、位置和帐户。此外，它还会比较帐户并导出关注者和主题标签统计信息。

## 4.LinkedIn

[InSpy](https://github.com/leapsecurity/InSpy) — 用 Python 编写的枚举工具。可用于搜索特定组织的员工。此外，它可以找出组织使用的技术，这是通过抓取特定关键字的作业列表来完成的。
[LinkedInt](https://github.com/vysecurity/LinkedInt) — 抓取选定组织中员工的电子邮件地址。支持对给定公司域名进行自动电子邮件前缀检测。
[ScrapedIn](https://github.com/dchrastil/ScrapedIn) — 一个 Python 脚本，用于抓取配置文件数据并将其导入 XLSX 文件（旨在与 Google 电子表格一起使用）。

# 10.自动化OSINT

互联网是数据的海洋，手动查找信息可能既耗时又无效，而且自动化工具可能会产生您无法发现的相关性。这完全取决于您的情况，您是否需要使用这些工具，因为它们中的大多数都有陡峭的学习曲线，并且需要解决复杂的问题。因此，如果您需要完成几项简单的任务——不要费心安装软件，只需使用我之前描述的在线服务和独立脚本即可。为了节省一些时间并准备好调查环境，在安装了以下所有工具（摘录 FOCA）后，您可以下载 [Buscador OS](https://inteltechniques.com/buscador/) — 为 OSINT 预配置的 Linux 虚拟机。

## 1.SpiderFoot

如果您想自动化 OSINT，[SpiderFoot](http://www.spiderfoot.net/)是目前最好的侦察工具之一，因为它可用于同时查询 100 多个公共数据源，并且其模块化允许微调查询的源。我个人喜欢的是按用例扫描。有四种不同的用例：获取有关目标的所有信息，了解目标向 Internet 暴露的内容（通过网络爬虫和搜索引擎使用完成），查询黑名单和其他来源以检查目标的恶意，以及通过不同的开源收集情报。最后一个是被动侦察的理想选择。

## 2.theHarvester

[theHarvester](https://github.com/laramies/theharvester) 是一个非常简单但有效的工具，用于在信息收集阶段获取有关目标的有价值的信息。它非常适合扫描与域相关的信息和收集电子邮件。对于被动侦察，theHarvester使用许多资源来获取数据，如Bing，百度，雅虎和谷歌搜索引擎，以及LinkedIn，Twitter和Google Plus等社交网络。对于主动侦测，它会执行 DNS 反向查找、DNS TDL 扩展和 DNS 暴力破解。

## 3.Recon-ng

[Recon-ng](https://tools.kali.org/information-gathering/recon-ng) 是另一个很棒的命令行工具，用于彻底快速地执行信息收集。这个功能齐全的 Web 侦察框架包括一系列用于被动侦察的模块、便利功能和交互式帮助，以指导您如何正确使用它。对于那些熟悉 Metasploit 的人来说，Recon-ng 将更容易学习，因为它具有类似的使用模型。如果您正在寻找可以快速检查贵公司在互联网上的知名度的强大功能，那么这就是首选工具。
[用Recon-ng侦察](https://www.osintteam.com/people-recon-with-recon-ng/?source=post_page-----5029a3c7fd56--------------------------------)

## 4.Maltego

[Maltego](https://www.paterva.com/web7/downloads.php) 是为分析复杂环境而开发的高级平台。除了数据挖掘之外，它还进行数据关联并直观地呈现它。Maltego 与您连接的实体（人员、公司、网站、文档等）合作，以便从不同来源收集有关它们的进一步信息，以获得有意义的结果。该工具的显着特点是“转换”——一个插件库，有助于运行不同类型的测试以及与外部应用程序的数据集成。

## 5.FOCA

[FOCA](https://github.com/ElevenPaths/FOCA)（Fingerprinting Organizations with Collected Archives）是一种用于从分析的文档中提取隐藏信息和元数据的工具。当分析所有文档并提取元数据时，它会执行自动元数据分析，以确定哪些文档是由同一用户创建的。此外，它还通过服务器和打印机进行关联。最新版本仅适用于 Windows。

## 6.Metagoofil

[Metagoofil](http://www.edge-security.com/metagoofil.php) 是一个命令行工具，用于从网站下载公共文档，并进行以下分析和元数据提取。它适用于 pdf、doc、xls、ppt 和其他格式。

# 11.结论

总而言之，在后隐私世界中保持私密性并控制哪些信息漂浮在这个数字海洋中是很困难的。虽然你无法控制关于你的一切，但至少要意识到这一点是很重要的。毋庸置疑，在数字时代，信息起着关键作用，所以那些知道如何找到它的人将永远领先一步。这就是本文的目的，旨在展示 OSINT 如何帮助解决广泛的问题：从营销到调查再到网络安全。然而，我只描述了冰山一角，文章中的大多数技术都很简单，但功能强大。因此，某些技术在用于恶意目的时可能会造成损害，因此请明智地使用它们。

虽然这篇文章更多的是关于情报收集，但下一篇文章将是关于准备阶段的。如果您想了解有关准备调查环境的具体信息，请在评论中告诉我。顺便问一下，你使用什么工具和技术来收集情报？

原博客链接：https://osintteam.blog/osint-how-to-find-information-on-anyone-5029a3c7fd56
