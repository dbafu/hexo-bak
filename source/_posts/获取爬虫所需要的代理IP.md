---
title: 获取爬虫所需要的代理IP
categories:
  - 爬虫
tags:
  - 代理
  - 爬虫
permalink: get-the-proxy-ip-required-for-the-crawler
date: 2017-10-26 18:29:49
---

> 原文首发：获取爬虫所需要的代理IP - [ZKeeer's Blog](http://zkeeer.space/?p=383)
<!--more-->

对某个网站进行高频次采集时经常会遇到IP被封的情况，这时候需要使用代理IP了。建立一个数据库，提供稳定可用的代理IP给爬虫使用，也是主要任务之一。

**主要功能：**

 - 从代理网站获取代理IP
 - 对代理IP进行检测，检测是否可用。检测方法是访问一稳定的网站，例如百度，腾讯等，查看状态码。
 - 写入数据库
 - 清洗数据库，剔除不可用的IP
 - 获取一条可用的代理


**数据库只需要一个表，表中只要一列：**

`CREATE TABLE IF NOT EXISTS IPPORT (IP_PORT TEXT NOT NULL PRIMARY KEY);`
逻辑图：

!['逻辑图'](https://pic2.zhimg.com/v2-948e04aed9db25203fc422b68fb6372d_b.png)

数据来源：

> http://www.kuaidaili.com/free/
  http://www.66ip.cn/
  http://www.xicidaili.com/nn/
  http://www.ip3366.net/free/
  http://www.proxy360.cn/Region/China
  http://www.mimiip.com/
  http://www.data5u.com/free/index.shtml
  http://www.ip181.com/
  http://www.kxdaili.com/

使用：

查看`demo.py`文件

`Util.Refresh()`：数据库和新的数据需要主动调用此函数更新，建议最少十五分钟更新一次

`Util.Get()`：调用可获取一条可用的代理，Util.Get()返回的代理：

`{‘http’: ‘http://115.159.152.130:81‘, ‘https’: ‘https://115.159.152.130:81′}`

`requests`可以直接使用：`requests.get(url,proxies=Util.Get(),headers={})`

**`Config.py` 部分：**

如果你还有代理网站可以添加，请添加在Url_Regular字典中。

代理IP网址和对应的正则式，正则式一定要IP和Port分开获取，例如[(192.168.1.1, 80), (192.168.1.1, 90),]

只抓取首页，想要抓取首页以后页面的可以将链接和正则式贴上来，例如，将某网站的1、2、……页的链接和对应的正则式分别添加到Url_Regular字典中。

添加正则式之前请先在 站长工具-正则表达式在线测试 测试通过后添加

** Github：[ZKeeer/IPProxy](https://github.com/ZKeeer/IPProxy) **



**测试：**

按照十五分钟一次刷新的速度，半天时间可以获得上千可用IP



**声明：**

不要高频次刷代理IP，不要给以上数据来源服务器造成过大的压力

