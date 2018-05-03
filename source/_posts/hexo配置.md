---
title: hexo配置
data: 2018-04-26 15:06
tags: [hexo,配置,设置]
categories: hexo配置
copyright: true
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

----------------------------------------------------
## 文末结束标记
打开    \themes\next\layout\_macro 

新建文件 passage-end-tag.swig

添加下列内容
``` bash
{% if theme.passage_end_tag.enabled %}
<div style="text-align:center;color: #ccc;font-size:16px;"><br/><br/><br/>
-------------本文结束， 感谢您的阅读！-------------</div>
<br/>
```

打开 \themes\next\layout\_macro\post.swig
查找 wechat  在此前插入下列代码， 在337行处
``` bash
  <div>
  {% if not is_index %}
    {% include 'passage-end-tag.swig' %}
  {% endif %}
</div>
```

打开 \themes\next\_config.yml 在合适位置添加下列代码

``` bash
文章末尾添加“本文结束”标记
passage_end_tag:
  enabled: true
```
----------------------------------------------
## 主页文章添加阴影效果
打开\themes\next\source\css\_custom\custom.styl ,添加下列代码
``` bash
/ 主页文章添加阴影效果
 .post {
   margin-top: 60px;
   margin-bottom: 60px;
   padding: 25px;
   -webkit-box-shadow: 0 0 5px rgba(202, 203, 203, .5);
   -moz-box-shadow: 0 0 5px rgba(202, 203, 204, .5);
  }
```

----------------------------------------------
## 底部增加版权信息  - 第一种
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
## 底部增加版权信息  - 第二种
在目录 next/layout/_macro/下添加 my-copyright.swig 文件。内容如下
``` bash
{% if page.copyright %}
<div class="my_post_copyright">
  <script src="//cdn.bootcss.com/clipboard.js/1.5.10/clipboard.min.js"></script>

  <!-- JS库 sweetalert 可修改路径 -->
  <script src="https://cdn.bootcss.com/jquery/2.0.0/jquery.min.js"></script>
  <script src="https://unpkg.com/sweetalert/dist/sweetalert.min.js"></script>
  <p><span>本文标题:</span><a href="{{ url_for(page.path) }}">{{ page.title }}</a></p>
  <p><span>文章作者:</span><a href="/" title="访问 {{ theme.author }} 的个人博客">{{ theme.author }}</a></p>
  <p><span>发布时间:</span>{{ page.date.format("YYYY年MM月DD日 - HH:MM") }}</p>
  <p><span>最后更新:</span>{{ page.updated.format("YYYY年MM月DD日 - HH:MM") }}</p>
  <p><span>原始链接:</span><a href="{{ url_for(page.path) }}" title="{{ page.title }}">{{ page.permalink }}</a>
    <span class="copy-path"  title="点击复制文章链接"><i class="fa fa-clipboard" data-clipboard-text="{{ page.permalink }}"  aria-label="复制成功！"></i></span>
  </p>
  <p><span>许可协议:</span><i class="fa fa-creative-commons"></i> <a rel="license" href="https://creativecommons.org/licenses/by-nc-nd/4.0/" target="_blank" title="Attribution-NonCommercial-NoDerivatives 4.0 International (CC BY-NC-ND 4.0)">署名-非商业性使用-禁止演绎 4.0 国际</a> 转载请保留原文链接及作者。</p>  
</div>
<script> 
    var clipboard = new Clipboard('.fa-clipboard');
      $(".fa-clipboard").click(function(){
      clipboard.on('success', function(){
        swal({   
          title: "",   
          text: '复制成功',
          icon: "success", 
          showConfirmButton: true
          });
        });
    });  
</script>
{% endif %}
```

在目录next/source/css/_common/components/post/下添加my-post-copyright.styl 文件 内容如下
``` bash
.my_post_copyright {
  width: 85%;
  max-width: 45em;
  margin: 2.8em auto 0;
  padding: 0.5em 1.0em;
  border: 1px solid #d3d3d3;
  font-size: 0.93rem;
  line-height: 1.6em;
  word-break: break-all;
  background: rgba(255,255,255,0.4);
}
.my_post_copyright p{margin:0;}
.my_post_copyright span {
  display: inline-block;
  width: 5.2em;
  color: #b5b5b5;
  font-weight: bold;
}
.my_post_copyright .raw {
  margin-left: 1em;
  width: 5em;
}
.my_post_copyright a {
  color: #808080;
  border-bottom:0;
}
.my_post_copyright a:hover {
  color: #a3d2a3;
  text-decoration: underline;
}
.my_post_copyright:hover .fa-clipboard {
  color: #000;
}
.my_post_copyright .post-url:hover {
  font-weight: normal;
}
.my_post_copyright .copy-path {
  margin-left: 1em;
  width: 1em;
  +mobile(){display:none;}
}
.my_post_copyright .copy-path:hover {
  color: #808080;
  cursor: pointer;
}
```
修改next/layout/_macro/post.swig，在代码
``` bash
<div>
      {% if not is_index %}
        {% include 'wechat-subscriber.swig' %}
      {% endif %}
</div>
```
之前添加增加如下代码：
``` bash
<div>
      {% if not is_index %}
        {% include 'my-copyright.swig' %}
      {% endif %}
</div>
```

修改next/source/css/_common/components/post/post.styl文件，在最后一行增加代码：
``` bash
@import "my-post-copyright"
```

保存重新生成即可。
如果要在该博文下面增加版权信息的显示，需要在 Markdown 中增加copyright: true的设置，类似：

``` bash
---
title: hexo设置
date: 2018-04-29 22:53:53
tags: hexo设置
categories: hexo设置
copyright: true
---
```

------------------------------------------

## 修改博客页宽
打开　\themes\next\source\css\_variables\custom.styl 添加下列内容
``` bash
$main-desktop                   = 1200px
$content-desktop                = 900px
```

----------------------------------------------
## 分割线样式修改

打开　\themes\next\source\css\_common\scaffolding\base.styl

注释下列内容
``` bash
  #background-image: repeating-linear-gradient(
  #  -45deg,
  #  white,
  #  white 4px,
  #  transparent 4px,
  #  transparent 8px
  #);
```

添加下列内容
``` bash
hr {
  margin: 20px 20px;
  height: 3px;
  background-color: #002661;
}
```

