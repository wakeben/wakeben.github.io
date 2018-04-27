---
title: hexo配置
data: 2018-04-26 15:06
tags: [hexo,配置,设置]
categories: hexo配置
---


----------------------------------------------
## 开启站内搜索功能

NexT 支持集成 Swiftype、 微搜索、Local Search 和 Algolia，各种搜索配置官方文档均有说明，但是尝试了一下只有本地搜索用着比较顺手

配置也简单，如下：
 安装 hexo-generator-searchdb，在站点的根目录下执行以下命令：

``` bash
npm install hexo-generator-searchdb --save
```
<!--more-->
站点配置文件，新增以下内容到任意位置：

经测试，这一步可以不做，不然多生成一个search.xml 冲突

``` bash
search:
  path: search.xml
  field: post
  format: html
  limit: 10000
```

主题配置文件，启用本地搜索功能：

``` bash
# Local search
local_search:
  enable: true
```



----------------------------------------------
## 显示摘要和阅读全文按钮

使用Hexo时，在使用markdown语法编辑文件时可以在index.html页面上显示摘要和阅读全文按钮。

在合适的位置插入下列内容作为分隔符

``` bash
 <!--more-->
```




----------------------------------------------
## 站点建立时间

这个时间将在站点的底部显示，例如 © 2013 - 2015。 编辑 主题配置文件，新增字段 since。

配置示例

``` bash
 since: 2013
```




----------------------------------------------
## 设置「动画效果」

编辑主题配置文件， 搜索 canvas_nest 或 three_waves，根据您的需求设置值为 true 或者 false 即可： 

注意： three_waves 在版本 5.1.1 中引入。只能同时开启一种背景动画效果。 

canvas_nest 配置示例

``` bash  
  # canvas_nest;  
  canvas_nest: true //开启动画;  
  canvas_nest: false //关闭动画;  
```




----------------------------------------------
## 代码高亮主题

NexT 使用 Tomorrow Theme 作为代码高亮，共有5款主题供你选择。 NexT 默认使用的是 白色的 normal 主题，可选的值有 normal，night， night blue， night bright， night eighties： 

更改 highlight_theme 字段，将其值设定成你所喜爱的高亮主题，例如：

```bash
# Code Highlight theme
# Available value: normal | night | night eighties | night blue | night bright
# https://github.com/chriskempson/tomorrow-theme
highlight_theme: normal
```



----------------------------------------------
## 文章插入本地图片

首先确认 _config.yml 中有 post_asset_folder:true 。 
``` bash				
postpost_asset_folder: true
```

在 hexo 目录，执行下面的命令，安装上传本地图片的插件
``` bash
npm install https://github.com/CodeFalling/hexo-asset-image --save
```
安装完成以后，重新启动hexo ，新建一个post 这时在\source\_posts下会产生和MD文件同名的文件夹


假设在
``` bash
Imgtest
├── 111.jpg
├── 222.jpg
└── 333.jpg
Imgtest.md
```

这样的目录结构（目录名和文章名一致），只要使用下列命令就可以插入图片。

 ``` bash
  ![111](Imgtest/111.jpg) 
```
生成的结构为
``` bash
public/2018/04/27/Imgtest
├── 111.jpg
├── index.html
├── 222.jpg
└── 333.jpg
```

同时，生成的 html 是这样的

``` bash
<img src="/2018/04/27/imgtest/test.jpg" alt="test">
```

----------------------------------------------

## 添加版权声明模块
Theme文件夹下的layout/_Marco/post.swig文件，这个和于layout下的post.swig的区别是前者扶着具体的post-content的生成，而后者是调用前者，然后补充类似comment第三方的模块的脚本。找到post-body所在的标签，并在其后加上如下代码：
``` bash
<div>    
 {# 表示如果不在索引列表中加入后续的HTML代码 #}
 {% if not is_index %}
    <ul class="post-copyright">
      <li class="post-copyright-author">
          <strong>本文作者：</strong>{{ theme.author }}
      </li>
      <li class="post-copyright-link">
        <strong>本文链接：</strong>
        <a href="{{ url_for(page.path) }}" title="{{ page.title }}">{{ page.path }}</a>
      </li>
      <li class="post-copyright-license">
        <strong>版权声明： </strong>
        本博客所有文章除特别声明外，均采用 <a href="http://creativecommons.org/licenses/by-nc-sa/3.0/cn/" rel="external nofollow" target="_blank">CC BY-NC-SA 3.0 CN</a> 许可协议。转载请注明出处！
      </li>
    </ul>
  {% endif %}
</div>
```

这样就生成了基础的HTML代码。类似theme.autor的变量，或从配置中读取或在运行时获取

加上样式
定位到Next下的source/css/_custom/custom.styl,并在里面添加如下样式代码:
``` bash
.post-copyright {
    margin: 2em 0 0;
    padding: 0.5em 1em;
    border-left: 3px solid #ff1700;
    background-color: #f9f9f9;
    list-style: none;
}
```


----------------------------------------------
## 修改底部#号标签

 效果      #      →      <i class="fa fa-tag"></i>
打开/themes/next/layout/_macro/post.swig 

``` bash 
rel="tag">#       \\搜索rel="tag">#  将 # 换成 <i class="fa fa-tag"></i>

rel="tag"><i class="fa fa-tag"></i> 
```

----------------------------------------------
## next的样式选择
next的样式其实有三种：Muse、Mist和Pisces，步骤2中看到的其实是next默认的模式Muse，根据官方说明三个样式的特点如下：

    Muse： 默认 Scheme，这是 NexT 最初的版本，黑白主调，大量留白
    Mist： Muse 的紧凑版本，整洁有序的单栏外观
    Pisces： 双栏 Scheme，小家碧玉似的清新

打开\themes\next\_config.yml  搜索 Scheme Settings 字段

``` bash
# ---------------------------------------------------------------
# Scheme Settings
# ---------------------------------------------------------------

# Schemes
#scheme: Pisces
scheme: Mist
#scheme: Pisces
#scheme: Gemini
```

----------------------------------------------

## 添加文章统计功能

在根目录下安装 hexo-wordcount 插件,运行下列命令
``` bash
npm install hexo-wordcount --save
```
打开next主题配置文档 \themes\next\_config.yml,搜索Post wordcount 字段，修改参数
``` bash
# Post wordcount display settings
# Dependencies: https://github.com/willin/hexo-wordcount
post_wordcount:
  item_text: true
  wordcount: true
  min2read: true
```

