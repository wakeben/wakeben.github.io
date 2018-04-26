---
title: hexo 搜索功能
data: 2018-04-26 15:06
tags: [hexo,搜索]
categories: hexo
---

开启站内搜索功能

NexT 支持集成 Swiftype、 微搜索、Local Search 和 Algolia，各种搜索配置官方文档均有说明，但是尝试了一下只有本地搜索用着比较顺手

配置也简单，如下：
1. 安装 hexo-generator-searchdb，在站点的根目录下执行以下命令：
<!--more-->

``` bash
npm install hexo-generator-searchdb --save
```

2. 站点配置文件，新增以下内容到任意位置：

经测试，这一步可以不做，不然多生成一个search.xml 冲突

``` bash
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
``` 

3. 主题配置文件，启用本地搜索功能：

``` bash
# Local search
local_search:
  enable: true
``` 