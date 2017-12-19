---
title: hexo博客添加常用插件
permalink: hexo-blog-to-ad-comon-plug-ins
categories:
  - hexo
tags: hexo插件
date: 2017-10-26 18:54:57
---

Hexo提供了诸多插件来增强博客体验，地址`http://hexo.io/plugins`


<!--more-->

## hexo-translate-title

使用Google翻译，百度翻译和有道翻译将Hexo中的汉字标题转成英文标题

### [](https://github.com/cometlj/hexo-translate-title#安装与使用)安装与使用

### [](https://github.com/cometlj/hexo-translate-title#安装)安装

```source-shell
npm install hexo-translate-title --save
```

### [](https://github.com/cometlj/hexo-translate-title#使用)使用

配置hexo根项目下的`_config.yml`

```source-yaml
translate_title:
  translate_way: google    #google | baidu | youdao
  youdao_api_key: XXX
  youdao_keyfrom: XXX
  is_need_proxy: true     #true | false
  proxy_url: http://localhost:8123
```

**注意**：判断是否需要配置google本地代理，因为我在本地是开启时才能访问google翻译的，如果没有被墙，请将`_config.yml` 下的`is_need_proxy: true`改为false。如果设置为true,请设置本地代理地址

## 添加pdf浏览插件
安装 **hexo-pdf**
`cnpm install --save hexo-pdf`
使用

```
{% pdf http://7xov2f.com1.z0.glb.clouddn.com/bash_freshman.pdf %}
{% pdf ./bash_freshman.pdf %}
```

## 添加生成文章目录插件hexo-toc
1 安装

`cnpm install hexo-toc --save`

2 配置
在博客根目录下的`_config.yml`中如下配置：

```
toc:
  maxdepth: 3
```

3 使用
在Markdown中需要显示文章目录的地方添加

<!-- toc -->
## 添加百度统计支持
`yilia`主题自带统计支持

1 打开[百度统计](https://tongji.baidu.com)网站，注册账号
![baidu_stat_01.png](http://oligvdnzp.bkt.clouddn.com/baidu_stat_01.png)

2 填写注册信息
![baidu_stat_02.png](http://oligvdnzp.bkt.clouddn.com/baidu_stat_02.png)

3 记录百度统计ID号码
![baidu_stat_03.png](http://oligvdnzp.bkt.clouddn.com/baidu_stat_03.png)

4 编辑修改`themes\yilia`目录下的`_config.yml`文件

```
# Miscellaneous
baidu_analytics: 'xxxxxxxxxxxx'   # xxxxxx是刚获得的百度统计ID号码
```

5 统计代码安装检查，确保代码安装正确
![baidu_stat_04.png](http://oligvdnzp.bkt.clouddn.com/baidu_stat_04.png)

## 添加多说评论支持
1 打开多说网站
![duoshuo_01.png](http://oligvdnzp.bkt.clouddn.com/duoshuo_01.png)

2 选择微信登陆
![duoshuo_02.png](http://oligvdnzp.bkt.clouddn.com/duoshuo_02.png)

3 点击我要安装
![duoshuo_03.png](http://oligvdnzp.bkt.clouddn.com/duoshuo_03.png)

4 填写相应信息
![duoshuo_04.png](http://oligvdnzp.bkt.clouddn.com/duoshuo_04.png)

5 编辑修改`themes\yilia`目录下的`_config.yml`文件

```
#是否开启多说评论，开启填写你在多说申请的项目的short_name: dbanote
#duoshuo: false
duoshuo: dbanote
```

## 参考链接
[Hexo站点中添加文章目录以及归档](http://www.ituring.com.cn/article/199624)
[hexo优化目录](http://www.cnblogs.com/peihao/p/5269131.html)

文章来自：[刘雅君](https://dbanote.github.io/)
