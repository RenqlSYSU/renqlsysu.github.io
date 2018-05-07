---
layout: post
title: Markdown 常用语法记录
categories: 杂学
tags: 博客 编程语法 整理
author: renql
---

* content
{:toc}

发现用Markdown写博客时总有一些常用的语法记不住，故罗列如下：

1. 超链接（用另一个页面打开）：`<a href="http://链接网址" target="_blank">超链接文字</a>`     

2. 插入图片：先把图片上传到新浪微博相册，然后复制图片地址，插入格式如下 `![](http://wx2.sinaimg.cn/mw690/006fa9Xlgy1fr34g1tkdpj30ow0j9gq1.jpg)`
其中，如插入小图为small，大图为large，mw690介于大图与小图之间     

3. github博客的开头必须为：
```
---
layout: post
title: 文章标题
categories: 类别
tags: 标签，可有多个，每个标签之间用空格隔开
author: renql
---

* content
{:toc}
```
