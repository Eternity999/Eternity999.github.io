---
title: 引用GitHub的静态资源文件
date: 2021-03-01 01:28:59
updated:
tags:
categories:
keywords:
description: 解决直接用 Github Raw 浏览器报错不执行
top _img:
comments:
cover: https://free.com.tw/blog/wp-content/uploads/2017/12/rawgit.png
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
参考[引用GitHub的静态资源文件](https://www.zhihu.com/question/22004590)

直接用 Github Raw 浏览器不执行，返回的 content-type 是 text/plain，实际上浏览器对 MIME 类型并没有强制检查，只是 Github 返回的 Header 加上了 X-Content-Type-Options: nosniff 强制浏览器执行 MIME 类型检查，于是就会报错。

解决办法：
[https://raw.githack.com](https://raw.githack.com)
[https://rawgit.org](https://rawgit.org)
[https://www.jsdelivr.com/github](https://www.jsdelivr.com/github)
