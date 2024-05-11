---
title: 通过Hexo搭建个人博客（二）进行一些美化
date: 2024-05-02 19:49:36
categories: 
 - 折腾记录
tags:
 - 折腾
 - Hexo
---

对单调的blog页面添加一些组件，进行一些美化

<!-- more -->

参考材料：[**Documentation | NexT**](https://theme-next.js.org/docs/)；[**Hexo文档**](https://hexo.io/zh-cn/docs/)；[**从零开始搭建个人博客（超详细）**](https://zhuanlan.zhihu.com/p/102592286)；[**Hexo+Next主题搭建个人博客+优化全过程（完整详细版）**](https://zhuanlan.zhihu.com/p/618864711)；[**Home - APlayer**](https://aplayer.js.org/#/home?id=options)；[**APlayer GitHub**](https://github.com/MoePlayer/hexo-tag-aplayer/blob/master/docs/README-zh_cn.md)；[**hexo-next-pjax文档**](https://github.com/theme-next/theme-next-pjax)；[**为Hexo博客添加全局APlayer播放器**](https://hakurei.red/2019/11/25/%E4%B8%BAHexo%E5%8D%9A%E5%AE%A2%E6%B7%BB%E5%8A%A0%E5%85%A8%E5%B1%80APlayer%E6%92%AD%E6%94%BE%E5%99%A8/#APlayer)

### 设置基本信息

用npm
`cd [folder]]`
`npm install hexo-theme-next`或

或用git下载next主题
`git clone https://github.com/next-theme/hexo-theme-next themes/next`

打开根目录的_config.yml文件，将主题改为next

```yml
# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: next   
```

将./theme/next目录下的_config.yml的内容拷贝，在blog主目录下新建名为"_config.next.yml"的文件，将拷贝内容粘贴进去。将需要个性化修改的配置文件单拎出来总是会安全方便一些

添加信息，修改语言和时区
```yml
# Site
title: monoch-space
subtitle: ''
description: ''
keywords: 
author: monoch-
language: zh-CN
timezone: 'Asia/Shanghai'
```

next提供了四种主题以及深色模式的选择。*第三第四个主题的区别是边框的显著与否吧，大概*
```yml
# Schemes
#scheme: Muse
#scheme: Mist
#scheme: Pisces
scheme: Gemini



# Dark Mode
darkmode: false
```

### 拓展菜单

例如想添加tags,categories和about的菜单，则对_Config.next.yml进行编辑：
```yml
menu:
  home: / || fa fa-home
  about: /about/ || fa fa-user
  tags: /tags/ || fa fa-tags
  categories: /categories/ || fa fa-th
  archives: /archives/ || fa fa-archive
  #schedule: /schedule/ || fa fa-calendar
  #sitemap: /sitemap.xml || fa fa-sitemap
  #commonweal: /404/ || fa fa-heartbeat
```
其中||后面的是图标名，前面的是目标链接

在根目录中打开git bash，输入
```sh
hexo new page tags
hexo new page about
hexo new page categories
```

在blog\source\_posts中可以看到新的tags和about文件夹，里面都有index.md文件，对其进行编辑：
```yml
---
title: 关于
date: 2024-04-26 22:07:08
type: about
comments: false
---
```
```yml
---
title: 标签
date: 2024-04-26 22:07:08
type: tags
comments: false
---
```
```yml
---
title: 分类
date: 2024-04-26 22:07:08
type: categories
comments: false
---
```

### 搜索功能

`cd [folder]`
`npm install hexo-generator-searchdb`

对_config.next.yml进行编辑：
```yml
# Local Search
# Dependencies: https://github.com/theme-next/hexo-generator-searchdb
local_search:
  enable: true
  # If auto, trigger search by changing input.
  # If manual, trigger search by pressing enter key or search button.
  trigger: auto
  # Show top n results per article, show all results by setting to -1
  top_n_per_article: 1
  # Unescape html strings to the readable one.
  unescape: false
  # Preload the search data when the page loads.
  preload: false
```

在_config.yml添加字段：
```yml
# hexo-generator-searchdb
search:
  path: search.xml
  field: post
  format: html
  limit: 10
```

### 建站时间

对_config.next.yml进行编辑：
```yml
footer:
  # Specify the date when the site was setup. If not defined, current year will be used.
  since: 2024   #建站时间
```

### 文章末尾版权声明

在_config.next.yml添加字段：
```yml
creative_commons:
  license: by-nc-sa
  sidebar: true
  post: true
  language: zh-CN
```
[“知识共享”（CC协议）简单介绍](https://zhuanlan.zhihu.com/p/20641764)

### 文章字数和阅读时间

下载插件
`npm install hexo-symbols-count-time --save`

在blog根目录下_config.yml添加字段：
```yml
symbols_count_time:
  symbols: true
  time: true
  total_symbols: true
  total_time: true
  exclude_codeblock: false
  awl: 2    
  wpm: 275
  suffix: "mins."
```

对_config.next.yml进行编辑：
```yml
# Post wordcount display settings
# Dependencies: https://github.com/theme-next/hexo-symbols-count-time
symbols_count_time:
  separated_meta: true
  item_text_post: true
  item_text_total: false
```

### 添加社交媒体链接

对_config.next.yml进行编辑：
```yml
# Social Links
# Usage: `Key: permalink || icon`
# Key is the link label showing to end users.
# Value before `||` delimiter is the target permalink, value after `||` delimiter is the name of Font Awesome icon.
social:
  Music: https://music.163.com/#/user/home?id=1443483816 || fa fa-music
```

`||`之后是图标名，可以在[**Font Awesome**](https://fontawesome.com/icons)进行查找

### 右上角github横幅

对_config.next.yml进行编辑：
```yml
# `Follow me on GitHub` banner in the top-right corner.
github_banner:
  enable: true
  permalink: https://github.com/monochrommmme
  title: Follow me on GitHub
```

### 实现全局音乐播放

参考：

安装APlayer插件
`npm install --save hexo-tag-aplayer`

打开blog/themes/next/layout/_layout.swig，添加
```html
<!-- 引用依赖 -->
<link rel="stylesheet" 
  href="https://cdn.jsdelivr.net/npm/aplayer@1.10.1/dist/APlayer.min.css">
<script src="https://cdn.jsdelivr.net/npm/aplayer@1.10.1/dist/APlayer.min.js"></script>
<script src="https://cdn.jsdelivr.net/npm/meting@1.2.0/dist/Meting.min.js"></script>

<!-- APlayer本体 -->
<div class="aplayer" 
  data-id="8885348672" 
  data-server="netease" 
  data-type="playlist" 
  data-fixed="true"
  data-autoplay="false" 
  data-order="random" 
  data-volume="0.55" 
  data-theme="#cc543a" 
  data-preload="auto"
  data-lrctype="0" >
  </div>
```

安装pjax插件
`$ git clone https://github.com/theme-next/theme-next-pjax source/lib/pjax`

编辑_config.next.yml
```yml
pjax: true
```

对blog\themes\next\layout\_partials\head\head.swig进行编辑：
```html
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=2">
<meta name="theme-color" content="{{ theme.android_chrome_color }}">
<meta name="generator" content="Hexo {{ hexo_version }}">
  
  <!--pjax：防止跳转页面音乐暂停-->
  <script src="https://cdn.jsdelivr.net/npm/pjax@0.2.8/pjax.js"></script>
```
之所以不部署在_layout.swig是因为实践时发现，刷新某篇文章后会进入html源代码界面，很神秘

更新pjax的方法
`$ cd themes/next/source/lib/pjax`
`$ git pull`
