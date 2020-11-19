---
title: Hexo博客之butterfly主题魔改
date: 2020-11-19 20:33:45
updated:
tags:
categories:
keywords:
description:
top _img:
comments:
cover: https://i.loli.net/2020/11/19/lGq8mQ4rsAiUVY6.gif
toc:
toc_ number:
copyright:
copyright _author:
copyright_ author _href:
copyright_ url:
copyright _info:
mathjax:
katex:
aplayer:
highlight_ shrink:
aside:
---
在逛[毒奶](https://limbopro.xyz/)的博客时看到鼠标在头像附近会有个下雪的特效，学习一下如何实现。
首先看到他网页源代码css是这样写的。
```styl
#aside .wrapper:hover {
	background: url(https://limbopro.xyz/usr/themes/handsome/assets/img/snow.gif);
	background-size: cover;
	color: #999;
}
```
然后检查自己博客相应想修改的位置div class="card-content"，由于对hexo的源码不太熟悉，直接到上传本站的github上进行card-content关键词搜索，找到themes/butterfly/source/css/_layout/aside.styl文件。
看到对应的元素背景：
```css
  .card-widget
    overflow: hidden
    margin-top: 1rem
    border-radius: 8px
    background: var(--card-bg)
    box-shadow: 0 4px 8px 6px rgba(7, 17, 27, .06)
    transition: all .3s
```
然后在上一级目录里的var.styl文件中加一行：
```styl
$card-author-bg = url(https://i.loli.net/2020/11/19/lGq8mQ4rsAiUVY6.gif)
```
再到/css/_global文件夹下的index.styl文件加入：
```sytl
  --card-author-bg: $card-author-bg
```
回到原来/css/_layout中的aside.styl文件写入：
```styl
  .card-widget:first-child:hover
    background: var(--card-author-bg)
```
完成