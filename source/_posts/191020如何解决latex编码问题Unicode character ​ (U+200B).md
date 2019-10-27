---
title: 如何解决latex编码问题Unicode character (U+200B)
author: 可爱多
avatar: https://cdn.jsdelivr.net/gh/keaidoo/cdn/img/custom/avatar1.jpg
authorLink: https://wangyaqian.club
authorAbout: 喜爱一切可爱的事物～
authorDesc: 我知道，我们心有灵犀。
categories: 技术
date: 2019-10-20 10:47:54
comments: true
tags: 
 - 博客
 - 悦读
keywords: 编码错误
description: 编码(U+200B)错误
photos: https://cdn.jsdelivr.net/gh/keaidoo/cdn@1.2/img/custom/paperPhoto/4.jpg
---
## 报错如下
```
Package inputenc: Unicode character ​ (U+200B)
(inputenc)	not set up for use with LaTeX.
```



## 问题原因
```\u200b ((Zero width space) characters）```
即文档中有中文空格，但是latex里面只能识别英文字符，故我们需要找到这个中文空格，此时文档写的很长的朋友可能要懵圈了，这么多字符要怎么找出哪一个空格是中文的呢？
## 解决方法
点击这个[识别编码](https://w3c.github.io/xml-entities/unicode-names.html)网站，我们可以将自己的整个文档复制在文本框中，点击**convert**即可。


再使用**Ctrl+F**，搜索```U+200B```,找到错误的位置，最后再文章中替换掉中文编码的字符就解决啦！！撒花~