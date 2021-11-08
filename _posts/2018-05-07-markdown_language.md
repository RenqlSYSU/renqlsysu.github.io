<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
    tex2jax: {
      inlineMath: [ ['$','$'], ["\\(","\\)"] ],
      processEscapes: true
    }
  });
</script>
<script src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS-MML_HTMLorMML" type="text/javascript"></script>

---
layout: post
title: Markdown 常用语法记录
categories: 杂学
tags: 博客 编程语法 整理
author: renql
---

* content
{:toc}

# Markdown语法
发现用Markdown写博客时总有一些常用的语法记不住，故罗列如下：

1. 超链接（用另一个页面打开）：`<a href="http://链接网址" target="_blank">超链接文字</a>`     

2. 插入图片：先把图片上传到新浪微博相册，然后复制图片地址，插入格式如下     
`![](http://wx2.sinaimg.cn/mw690/006fa9Xlgy1fr34g1tkdpj30ow0j9gq1.jpg)`    
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
4. 上下标表示方法    

```
H<sub>2</sub>O  CO<sub>2</sub>  注意：第二个sub前有斜杠
爆米<sup>TM</sup>
```

效果

> H<sub>2</sub>O  CO<sub>2</sub>     
> 爆米<sup>TM</sup>

5. 数学公式   
据说目前github的markdown不支持公式渲染，因此如果需要插入公式可以借助外部网站，使用方法见下面这个文档。  
<a href="https://slowlythinking.github.io/2019/07/BlogWriting_Equations_in_Markdown/" target="_blank">https://slowlythinking.github.io/2019/07/BlogWriting_Equations_in_Markdown/</a> 

尝试了第一种方案 Script+MathJax，确实可以，举例如下，但换行符号好像失效：

样本量的变化：$M_n=M_{n-1}+m_n$  

\begin{split}
\bar E_n &= \frac{(M_n-m_n)\bar E_{n-1} + \sum_{i=1}^{m_n} a_i}{M_n}  
&=\bar E_{n-1} + \frac{\sum_{i=1}^{m_n} a_i - m_n\bar E_{n-1}}{M_n}
\end{split}

# 分类 categories
发现博客中如果分类或者标签太多，则会显得有些混乱，因此将目前有的分类整理如下。    

**读书笔记**：读专业书或课外书的读书笔记  
**linux**  
**ncl**   
**ponder** = thinking   
**文献笔记**  
**大气科学**：整理的一些关于大气科学的常用知识点   
**讲座笔记**：包括讲座和会议笔记   
**课堂笔记**   
**模式学习**   
**杂学**：关于电脑、编程等因兴趣而学的内容      
**English_learning**：英语学习笔记   
**数据资料**：研究用的数据资料列举

# 标签
**整理**：最常用的标签   
