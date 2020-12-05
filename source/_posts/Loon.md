---
title: Loon
date: 2020-11-13 08:41:13
updated:
tags:
categories:
keywords:
description: IOS网络代理工具
top _img:
comments:
cover: https://is5-ssl.mzstatic.com/image/thumb/Purple114/v4/79/30/5f/79305f6e-de52-e79b-af5b-f202371866c5/AppIcon-0-0-1x_U007emarketing-0-0-0-7-0-0-sRGB-0-0-0-GLES2_U002c0-512MB-85-220-0-0.png/460x0w.png
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
### 新入手Loon
很久之前用别人的账号玩过[Quantumult X](https://apps.apple.com/us/app/quantumult-x/id1443988620?l=zh)觉得挺好玩的，而且最近这些网络代理工具都开始支持跑脚本了，但又觉得 Quan X 挺贵的，于是找App Store代购买了一个新的代理工具 [Loon](https://apps.apple.com/us/app/loon/id1373567447) 

#### App Store代购：
* [aneeo杂货铺](https://buy.aneeo.com/)
* [火箭少女](https://t.me/RocketGirls_bot)的[发卡网站](https://www.rocketgirls.space/product/)

#### 使用Loon去广告
[正则表达式30分钟入门教程](https://deerchao.cn/tutorials/regex/regex.htm)
参考教程：[利用 Quantumult X 去网页广告（正则表达式以及开发者工具、调试）](https://limbopro.xyz/archives/12782.html)
通过安装CA证书使代理软件能通过MITM（Man-in-the-MiddleAttack，“中间人攻击”）解密https流量，并通过正则表达式匹配响应的请求进行改写替换请求可达到去除广告的效果。
前后对比：
![去广告前.PNG](https://i.loli.net/2020/11/19/2cBxbgt6kf9MX4I.jpg)
![去广告后.PNG](https://i.loli.net/2020/11/19/yKPzolw2FtuD49b.jpg)

可以copy一下[毒奶大佬](https://limbopro.xyz/)写的去广告规则，但是由于Quantumult X 与Loon的格式不太一样，应当仿照Loon配置里的格式进行修改。
可以选择直接对广告请求直接reject，但还是会显示一个灰色无法加载图片的框，所以选用网上一些透明的图片链接进行302重定向达到上图的效果。
你可以写成xxx.plugin文件放在GitHub上，通过raw链接远程加载插件，也可以直接写在配置中，还可以在 配置页-复写-单个复写 自行选取复写类型（目前支持header、302、reject、307、reject-200、reject-img、reject-dict、reject-array），写好正则表达式进行匹配和替换成相应内容。
```JSON
# 去除nfmovie广告
[Rule]
DOMAIN-SUFFIX, s96.cnzz.com, reject
DOMAIN-SUFFIX, yabo729.com, reject

[URL Rewrite]
^https:?/\/www\.nfmovies\.com\/static\/\w{6}-\d{1,2}\.(jpg|gif) https://limbopro.xyz/usr/uploads/2020/10/2091577197.png 302
^https:?/\/www\.nfmovies\.com\/static\/2011\w.*\.jpg https://limbopro.xyz/usr/uploads/2020/10/2091577197.png 302
^https:?/\/www\.nfmovies\.com\/static\/\d{1,4}.jpg https://limbopro.xyz/usr/uploads/2020/10/2091577197.png 302
^https:?/\/www\.naifei\.shop\/static\/banner\/banner.jpg https://limbopro.xyz/usr/uploads/2020/10/2091577197.png 302
^https:?/\/www\.naifei\.shop\/static\/banner\/banner_mobile.jpg https://limbopro.xyz/usr/uploads/2020/10/2091577197.png 302
^https\b.*\bbanner.jpg url reject-img
^https\b.*\bbanner\b.*\.jpg url reject-img
^https://\b.*\bnaifei\b.*/\?sid=\w{1,6} url reject-img
^http.*yabo729.\b.* url https://limbopro.xyz/usr/uploads/2020/10/2091577197.png 302
^http.*yabo.\b.* url https://limbopro.xyz/usr/uploads/2020/10/2091577197.png 302

[MITM]
hostname = *.nfmovies.com,*.yabo.*,*.naifei.shop
```
Loon的复写栏中暂时还没有直接对Request、Response的重写，但是在脚本中是可以是实现的，暂时还需要研究下如何写脚本去除视频播放的广告倒计时。
此方法的广告过滤效果并不特别理想，只要某一次请求广告链接成功了，就会缓存到相关的元素并一直显示。
因此还是推荐使用AdGuard等更专业的去广告工具，但很多时候一些网站会做反广告拦截要求你关闭广告过滤...因此才会用更多热爱折腾的大佬写出各种网络代理工具的规则和脚本。
### 参考教程
更多的脚本、插件和用法请看：
[Loon 教程](https://github.com/chiupam/tutorial/blob/master/Loon/Plus/README.md)

### 最后
所以有好心人赞助我买个Quantumult X吗？