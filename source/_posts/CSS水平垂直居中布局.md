---
title: CSS水平垂直居中布局
author: 可爱多
avatar: https://cdn.jsdelivr.net/gh/keaidoo/CDN/img/custom/avatar.jpg
authorLink: 
authorAbout: 喜爱一切可爱的事物～
authorDesc: 喜爱一切可爱的事物～
categories: 技术
date: 2019-4-14 21:54:01
comments: true
tags: 
 - web
keywords: css
description: 
photos: https://cdn.jsdelivr.net/gh/keaidoo/cdn@1.2/img/custom/paperPhoto/1.jpg
---
## 一、水平居中
### (1）行内元素的水平居中
```
.parent{text-align: center;}    
.child{display: inline-block;}
```
### (2）块状元素的水平居中（定宽）
```
.child{
         width: 200px;
         margin: 0 auto;
     }
```
### (3）块状元素的水平居中（不定宽）
可以直接给不定宽的块级元素设置```text-align：center```来实现，也可以给父元素加```text-align:center``` 来实现居中效果。
## 二、垂直居中
### (1）条件是父元素是盒子容器且高度已经设定
子元素是行内元素，高度是由其内容撑开的
设定父元素的```line-height```为其高度
子元素是块级元素但是子元素高度没有设定
给父元素设定
```
display:table-cell;
vertical-align:middle
```
### (2）子元素是块级元素且高度已经设定
计算子元素的```margin-top```或```margin-bottom```
## 三、水平垂直居中
### (1）水平对齐+行高
```text-align + line-height```
### (2）水平+垂直对齐
在父元素设置```text-align```和```vertical-align```，并将父元素设置为```table-cell```元素，子元素设置为```inline-block```元素
### (3）相对+绝对定位
```
.parent{
 position: relative;
}
.child{
 position: absolute;
 top: 0;
 left: 0;
 right: 0;
 bottom: 0;
 height: 50px;
 width: 80px;
 margin: auto;
}
```