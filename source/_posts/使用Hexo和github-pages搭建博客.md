---
title: 使用Hexo和github pages搭建博客
permalink: use-hexo-and-github-pages-to-build-blogs
categories:
  - hexo
tags:
  - hexo
date: 2017-10-26 15:28:49
---

##### Tips :

1. **Hexo的基本命令**

```
  hexo clean    #出现任何问题，删除博客目录下的db.json文件
  hexo d -g
  hexo g = hexo generate  #生成
  hexo s = hexo server  #启动本地预览
  hexo d = hexo deploy  #远程部署

  hexo n "文章标题" = hexo new "文章标题"  #新建一篇博文
  or
  hexo new post "文章标题"   #新建一篇博文

  hexo s -g  #等同先输入hexo g，再输入hexo s
  hexo d -g  #等同先输入hexo g，再输入hexo d
```

<!--more-->

2. **写博客**

  hexo的文章存放在`source`目录下

```
  ├── source
  |   ├── _posts    #存放文章
  |   └── _drafts   #存放草稿
  $ hexo new post "postName"        # 在source/_posts 目录下创建postName.md文件

```

  创建文件的命名格式可以在_config.yml文件配置

```
  Writing

  new_post_name: :year-:month-:day-:title.md
```

  文件创建完成后会自动生成以下格式（可以自己添加）

```
  ---
  title: 使用Hexo和github pages搭建博客
  date: 2016-04-18 19:50:26
  categories:
   - blog                  # 分类
  tags:
   - blogs
   - hexo               # 标签，格式：- 标签 换行 - 标签2
  ---
```

  关与写作的各种参数可以参见：(https://hexo.io/docs/writing.html)

  写完后预览的时候发现，文章在首页就全部显示出来了，如果不想全部显示，可以在文章中间添加下面标记，在首页列表就会出现Read More的标记

  `<!--more-->`


#### 1. 简介

hexo是一个基于node.js的静态博客程序，可以方便的生成静态网页（纯html）支持多个平台（Windows/MAC/Linux），风格优雅，更适合写技术博客，与hexo类似的博客程序还有jekyll，jekyll被github着力推荐官方就提供了jekyll教程，但是jekyll是基于ruby写的，并且关于代码高亮没找到比较好的方案，就选择了用hexo

#### 2. 配置环境

##### 2.1 安装git

作者用的是mac，可以使用brew下面命令安装

  `$ brew install git`

也可以直接上git官网下载安装

##### 2.2 安装node.js

建议使用nodejs 6.9， 8.XX有些小毛病 去[nodejs 官网](https://nodejs.org/en/)下载

同样的，mac可以使用brew安装，新版的node.js已经包含npm工具，不需要再另外安装了

`$ brew install node`
可以通过下面命令检查是否已安装

```
$ node -v
$ npm -v
```

如果是windows用户可以通过[官网下载](https://nodejs.org/en/) node.js

##### 安装淘宝的cnpm源
访问国外源速度较慢，建议安装淘宝的cnpm源，以后使用`cnpm`命令代替`npm`

`npm install -g cnpm --registry=https://registry.npm.taobao.org`


##### 2.3 Hexo安装 (-g 是全局化安装)

`cnpm install hexo-cli -g `

##### 初始化hexo博客

#######在当前目录下新建blog目录初始化博客

```
cd blog
hexo init blog
cnpm install
```

##### npm install
hexo generate             #根据当前配置生成静态页面
hexo server               #启动本地服务，默认为：[http://localhost:4000/](http://localhost:4000/)
接下来就可以通过http://localhost:4000/查看效果了
hello hexo

#### 3. 配置github pages

每个github账户都可以有一个外部空间/Responsitory，可以直接通过用户名.github.io访问到该仓库的内容

在github上新增一个responsitory，仓库名为 用户名.github.io 或 用户名.github.com
创建完成后，github会自动将 用户名.github.io指向该仓库，默认访问根目录下的index.html页面
可以进入Responsitory的Setting页查看
github会提供几个模板搭建站点，我们可以不用他提供的模板，可以在仓库里面，添加一个简单的index.html文件，如果能通过用户名.github.com访问，则表明创建成功了

#### 4. 写博客

hexo的文章存放在`source`目录下
```
├── source
|   ├── _posts    #存放文章
|   └── _drafts   #存放草稿
$ hexo new post "postName"        # 在source/_posts 目录下创建postName.md文件
```

创建文件的命名格式可以在_config.yml文件配置

##### Writing

`new_post_name: :year-:month-:day-:title.md`

文件创建完成后会自动生成以下格式（可以自己添加）

```
---
title: 使用Hexo和github pages搭建博客
date: 2016-04-18 19:50:26
categories: blog                  # 分类
tags: [blogs, hexo]               # 标签，格式：[标签, 标签2]
---
```

关与写作的各种参数可以参见：(https://hexo.io/docs/writing.html)

写完后预览的时候发现，文章在首页就全部显示出来了，如果不想全部显示，可以在文章中间添加下面标记，在首页列表就会出现Read More的标记

`<!--more-->`


#### 5. 主题

官方自带主题基本够用，有能力可以自己改造，当然，网上已经有很多人做了一些很好看的主题了，我们可以直接拿来用，下面是官方列出的一些主题，找到喜欢的可以直接用

> https://github.com/hexojs/hexo/wiki/Themes
https://hexo.io/themes

在hexo上，主题放在themes目录下，我们只需要把别人做好的主题clone下来就好了，然后在`_config.yml`修改一下配置
例如：我们可以https://github.com/xiangming/landscape-plus这个主题clone下来

`git clone git@github.com:xiangming/landscape-plus.git themes/landscape-plus`

修改设置`_config.yml`

`theme: landscape-plus`


#### 6. 添加多说评论插件

到多说官网注册和创建一个站点

修改配置
到`themes/landscape-plus/_config.yml`添加多说的配置，shortname即注册的站点名称

##### Duoshuo
duoshuo_shortname: bomo
参见官方说明，替换评论相关的代码http://dev.duoshuo.com/threads/541d3b2b40b5abcd2e4df0e9

完成，如下图评论有了
评论

7. 部署到github上

修改配置`_config.yml`

```
deploy:
  type: git
  repository: https://github.com/zhengbomo/zhengbomo.github.io.git
  branch: master
```
安装 hexo-deployer-git

$ npm install hexo-deployer-git --save
部署hexo到git上

$ hexo deploy
部署过程需要输入账号密码，然后会push到github上，参考：https://hexo.io/docs/deployment.html

hexo部署时会把最终生成的博客文件（public目录下的文件）push到git远程仓库，而博客程序还是在本地，当我们切换电脑的时候，无法对博客进行重新编辑和发布，这个时候我们可以在git添加一个分支hexo用来存放博客程序和编写的内容，详情可以参见： git创建分支hexo存放博客程序

#### 8. 域名绑定

通常域名在godaddy注册比较靠谱，这个是最大的域名提供商，而且不需要备案，支持支付宝付款，购买的时候可以使用优惠码会便宜一些，网上有很多优惠码，可以自行搜索，购买过程很简单，这里就不贴了

注册和配置DNS服务器
Godaddy自带的域名解析服务器比较慢，在国内推荐使用DNSpod：快，免费，稳定。

到DNSpod注册登陆，然后到用户中心，添加域名，例如我的域名为bomobox.org


进入设置

添加两个A记录指向github提供的ip，参见这里

```
192.30.252.153
192.30.252.154
```
添加一个CNAME记录指向自己的github域名：username.github.io
把其他的删除

注册域名和配置DNS

到Godaddy购买域名完成后完成后进入MyAccount


进入DNS Manager修改DNS服务器
```
f1g1ns1.dnspod.net
f1g1ns2.dnspod.net
```

到github仓库的根目录添加CNAME文件，文件内添加自己的域名，否则会出现404访问错误，也可以在hexo的source目录下添加，然后不熟到github


上面步骤设置完成后可能会有几个小时的延迟，才能生效，总的来说还是比较简单的

#### 9. 问题

在使用别人的主题的时候可能会报错或者有些功能用不了，原因可能是部分插件没有安装，例如RSS用不了，那可能是hexo-generator-feed没安装，下面列举一些常用的插件，建议都安装，没有用到也没有关系，需要先到hexo程序目录下在执行命令，插件位于node_modules目录下

```
$ npm install hexo-generator-feed --save                  #支持RSS
$ npm install hexo-generator-sitemap --save               #生成站点地图
$ npm install hexo-generator-baidu-sitemap --save         #生成百度站点地图
$ npm install hexo-html-minifier --save                   #HTML 压缩
$ npm install hexo-uglify --save                          #JavaScript 压缩
$ npm install hexo-clean-css --save                       #CSS 压缩插件
$ npm install hexo-generator-seo-friendly-sitemap --save  #SEO优化
$ npm install hexo-deployer-git --save                    #git部署插件
```

并在博客配置文件_config.yml配置plugin

Plugins:
- hexo-generator-feed
- hexo-generator-sitemap
更多插件可以在 (https://hexo.io/plugins/) 找到

#### 10. vs code 插件

由于我编写md使用的是vs code，这里推荐插件Markdown Preview Enhanced
快捷键ctrl + shift + m 预览

#### 11. 总结

使用hexo搭建博客环境还是非常方便的，基本上都是自动的，当然还有一些详细的配置，例如分页，分类，评论等，Hexo支持的插件也相当多的，接下来可以好好写博客了，以后再慢慢完善了，今天先到这里

#### 12. 参考链接

 - (https://hexo.io)
 - [dbanote](https://dbanote.github.io/2017/02/06/tools/hexo+github%E6%90%AD%E5%BB%BA%E4%B8%AA%E4%BA%BA%E5%8D%9A%E5%AE%A2/)
 - [bomo](http://blog.bombox.org/2016-04-18/hexo-for-blog/)
