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

遇到的报错：引入CSS出现because its MIME type ('text/plain') is not executable错误
错误提示：Refused to execute script from 'xxxx' because its MIME type ('text/plain') is not executable, and strict MIME type checking is enabled.
情况：引入上传在github的CSS、JS文件，无法显示样式，开发者模式（F12）显示Refused to execute script from 'xxx' because its MIME type ('text/plain') is not executable, and strict MIME type checking is enabled。但能访问到CSS、JS文件（在网页下查看源代码，访问CSS、JS文件），没有出现404问题。

直接用 Github Raw 浏览器不执行，返回的请求头 content-type 是 text/plain，但实际上浏览器对 MIME 类型并没有强制检查，只是 Github 返回的 Header 加上了 X-Content-Type-Options: nosniff 强制浏览器执行 MIME 类型检查，于是就会报错。

解决办法：
可以利用[https://raw.githack.com](https://raw.githack.com)解决，用法简单，只需将你的github链接填入输入框，即可看到use this url里面有生成其他链接，引入那个链接，将不再报错，CSS、JS样式显示出来。

类似网站：
[https://rawgit.org](https://rawgit.org)
[https://www.jsdelivr.com/github](https://www.jsdelivr.com/github)

### 参考资料
[引用GitHub的静态资源文件](https://www.zhihu.com/question/22004590)
[引入CSS出现because its MIME type ('text/plain') is not executable错误](https://blog.csdn.net/qq_38243612/article/details/104333825)

