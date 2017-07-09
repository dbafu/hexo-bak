---
title: mod yelee by myself
tags: test
permalink: mod-yele-by-myself
date: 2017-07-09 14:37:26
---

yelee：

1  style.styl  末尾添加了如下代码：

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

from： http://lupeng.me/2015/06/23/%E6%B7%BB%E5%8A%A0%E5%A4%9A%E7%BA%A7%E5%88%86%E7%B1%BB.html



在/yelee/layout/left/_partial/left-col.ejs   末尾 </header> 之上添加如下代码：

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

同一文件 <% if (theme.subtitle){ %> 之上  添加<br> 换

同一文件 <% if (theme.search.on){ %> 之上  添加<br> 换

代码片段：

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


修改 yelee/layout/_partial/footer.ejs

改 footer-left 为  footer-right. 并且 删除 原有的 footer-right 和 所有的<% %>包含的统计访问量代码



```yml
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
