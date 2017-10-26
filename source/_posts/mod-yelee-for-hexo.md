---
title: hexo更换主题并个性化定制
categories:
  - hexo
tags: hexo插件
permalink: hexo-change-theme-and-personalize-custom
date: 2017-07-09 14:37:26
---

**我喜欢的主题是yeleee**
<!--more-->

> hexo系统默认的主题虽然也不错，但我更喜欢yelee和yilia这两款主题

## 安装yelee主题

1 主题说明文档：http://moxfive.coding.me/yelee/

2 在博客根目录下执行以下命令

```
# 克隆最新一次提交（git clone速度很慢，可只克隆最新一次提交）
git clone --depth 1 https://github.com/MOxFIVE/hexo-theme-yelee.git themes/yelee
```

3 编辑修改根目录下的`_config.yml`文件

```
# theme: landscape
theme: yelee
```

4 更换主题后需要清理并重新生成静态页

`hexo clean && hexo g && hexo s`

5 安装搜索插件

`cnpm install hexo-generator-search --save`

6 参照文档修改`themes\yelee`目录下的`_config.yml`文件

## 安装yilia主题
1 在博客根目录下执行以下命令

```
git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia
# 或者
git clone git@github.com:litten/hexo-theme-yilia.git themes/yilia

# 克隆最新一次提交（git clone速度很慢，可只克隆最新一次提交）
git clone --depth 1 https://github.com/litten/hexo-theme-yilia.git themes/yilia
```

2 在博客根目录（注意不是yilia根目录）执行以下命令：

`cnpm i hexo-generator-json-content --save`

3 编辑修改根目录下的`_config.yml`文件

```
# theme: landscape
theme: yilia

# 添加以下内容
# jsonContent
jsonContent:
    meta: false
    pages: false
    posts:
      title: true
      date: true
      path: true
      text: true
      raw: false
      content: false
      slug: false
      updated: false
      comments: false
      link: false
      permalink: false
      excerpt: false
      categories: false
      tags: true
更换主题后需要清理并重新生成静态页

hexo clean
hexo g
hexo s
更换后效果
update_theme.png

编辑修改themes\yilia目录下的_config.yml文件

# 修改menu
menu:
  主页: /
  归档: /archives/
  #随笔: /tags/随笔/

# 修改并注释掉不需要的项
# SubNav
subnav:
  github: "https://github.com/dbanote"
  weibo: "http://weibo.com/foxbei"
  #rss: "#"
  #zhihu: "#"
  qq: "http://sighttp.qq.com/msgrd?v=1&uin=9320802"
  #weixin: "#"
  #jianshu: "#"
  #douban: "#"
  mail: "mailto:15004618839@139.com"

# 文章太长，截断按钮文字
# 截断需要在文章中添加 <!--more-->
#excerpt_link: more
excerpt_link: false

# 设置打赏二维码
# 打赏基础设定：0-关闭打赏； 1-文章对应的md文件里有reward:true属性，才有打赏； 2-所有文章均有打赏
reward_type: 2
# 打赏wording
reward_wording: '喜欢的话，支付1元请我吃糖吧！'

# 支付宝二维码图片地址，跟你设置头像的方式一样。比如：/assets/img/alipay.jpg
# 支付宝收款1元二维码图片
alipay: /img/zhifubao01.png
# 支付宝收款无金额设置二维码图片
# alipay: /img/zhifubao.png

# 微信二维码图片地址
# 微信收款1元二维码图片
weixin: /img/weixin01.png
# 微信收款无金额设置二维码图片
# alipay: /img/weixin.png

# 修改网站收藏夹图标
favicon: /img/favicon.png

#你的头像url
avatar: /img/avatar.jpg

# 根据需要修改以下内容
# 智能菜单
# 如不需要，将该对应项置为false
# 比如
#smart_menu:
#  friends: false
smart_menu:
  innerArchive: '所有文章'
  friends: '常用网站'
  aboutme: '关于我'

friends:
  My Oracle Support: https://support.oracle.com/
  Oracle Edelivery: https://edelivery.oracle.com/
  Oracle Help Center: http://docs.oracle.com/
  练数成金: http://www.dataguru.cn/
  三通IT论坛: http://www.santongit.com/
  一起自学吧: http://www.17zixueba.com/

aboutme: DBA<br><br>工作学习笔记<br>谢谢大家

```

以上内容来自：  [dbanote刘雅君](https://dbanote.github.io/2017/02/10/tools/hexo%E6%9B%B4%E6%8D%A2%E4%B8%BB%E9%A2%98%E5%B9%B6%E4%B8%AA%E6%80%A7%E5%8C%96%E5%AE%9A%E5%88%B6/)


--------------


## yelee theme

### 1  style.styl  末尾添加了如下代码：

```
.category-list
  font-size 0.9em
  padding 15px 20px
  .category-list-count
    margin-left 8px
    font-size 0.8em
    color color-meta
    &:before
      content '('
    &:after
      content ')'

ul, ol, dl
  list-style none
  ul, ol, dl
    margin-left 20px
    li:before
      content '> '
```

<!--more-->

[lupeng博客](http://lupeng.me/2015/06/23/%E6%B7%BB%E5%8A%A0%E5%A4%9A%E7%BA%A7%E5%88%86%E7%B1%BB.html)


### 2 在/yelee/layout/left/_partial/left-col.ejs   末尾 </header> 之上添加如下代码：

```ejs
    <% if (!is_post()) { %>
        <% if (site.categories.length){ %>
            <div class="widget tag">
              <h3 class="title"><%= __('分类 :') %></h3>
                <%- list_categories(site.categories) %>
                </div>
            <% } %>
            <% } %>
```
出处同上

同一文件 `<% if (theme.subtitle){ %>` 之上  添加<br> 换

同一文件 `<% if (theme.search.on){ %>` 之上  添加<br> 换

代码片段：

  ```
  <hgroup>

              <h1 class="header-author">
                  <a href="<%= config.root %>">
                      <%=theme.author%>
                  </a>
              </h1>
          </hgroup>

          <br>

          <% if (theme.subtitle){ %>
              <p class="header-subtitle">
                  <%=theme.subtitle%>
              </p>
              <%}%>

                  <br>

                  <% if (theme.search.on){ %>
                      <form id="search-form">

```

### 4 修改 yelee/layout/_partial/footer.ejs

改 footer-left 为  footer-right. 并且 删除 原有的 footer-right 和 所有的<% %>包含的统计访问量代码


```
  # Hexo Configuration
  ## Docs: https://hexo.io/docs/configuration.html
  ## Source: https://github.com/hexojs/hexo/

  # Site
  title: 一个DBA的工作学习笔记
  subtitle: 欲事之无繁，则必劳于始而逸于终
  description: 一个DBA的工作学习笔记
  author: 付腾飞
  language: zh-Hans
  timezone:

  # URL
  ## If your site is put in a subdirectory, set url as 'http://yoursite.com/child' and root as '/child/'
  url: http://dbafu.github.io
  root: /
  permalink: :year/:month/:day/:title/
  permalink_defaults:

  # Directory
  source_dir: source
  public_dir: public
  tag_dir: tags
  archive_dir: archives
  category_dir: categories
  code_dir: downloads/code
  i18n_dir: :lang
  skip_render:

  # Writing
  new_post_name: :title.md # File name of new posts
  default_layout: post
  titlecase: false # Transform title into titlecase
  external_link: true # Open external links in new tab
  filename_case: 0
  render_drafts: false
  post_asset_folder: false
  relative_link: false
  future: true
  highlight:
    enable: true
    line_number: false
    auto_detect: false
    tab_replace:

  # Category & Tag
  default_category: uncategorized
  category_map:
  tag_map:

  # Date / Time format
  ## Hexo uses Moment.js to parse and display date
  ## You can customize the date format as defined in
  ## http://momentjs.com/docs/#/displaying/format/
  date_format: YYYY-MM-DD
  time_format: HH:mm:ss

  # Pagination
  ## Set per_page to 0 to disable pagination
  per_page: 10
  pagination_dir: page

  # Extensions
  ## Plugins: https://hexo.io/plugins/
  ## Themes: https://hexo.io/themes/
  # theme: landscape
  theme: yelee
  # theme: next
  # 添加以下内容
  # jsonContent
  jsonContent:
      meta: false
      pages: false
      posts:
        title: true
        date: true
        path: true
        text: true
        raw: false
        content: false
        slug: false
        updated: false
        comments: false
        link: false
        permalink: false
        excerpt: true
        categories: true
        tags: true


  translate_title:
    translate_way: google    #google | baidu | youdao
    youdao_api_key: XXX
    youdao_keyfrom: XXX
    is_need_proxy: false     #true | false
    proxy_url: http://localhost:8123


  # Deployment
  ## Docs: https://hexo.io/docs/deployment.html
  deploy:
    type: git
    repository: git@github.com:dbafu/dbafu.github.io.git
    branch: master

```

