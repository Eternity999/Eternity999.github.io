---
title: IP签名档
date: 2020-10-21 15:55:21
cover: https://camo.githubusercontent.com/a7e5514d72f7cdd23250ac65c107561c91572795/68747470733a2f2f692e6c6f6c692e6e65742f323031392f30372f31362f3564326435623161313163383732343537392e706e67
---
在逛PT论坛的时候看到个签名档能显示ip、时间、UserAgent等一些信息，好奇去搜了下源码。

## 如何制作

### 项目地址
[https://github.com/xhboke/IP](https://github.com/xhboke/IP)
正常来说git clone到你的vps建好的网站根目录下就能直接部署成功了

### 它不对劲！
但是打开发现事情并不简单
效果变成了下面这个样子
![ip签名档](https://xhboke.com/news/?s=6L+Z5piv5ryU56S65pWI5p6c77yM6L+Z6YeM5paH5a2X5Y+v5Lul5pS55Y+Y)
啊这...很多东西虚无了
看了下程序的php代码，调用了那人自己写的api，返回的都是空值
![ip_api.png](https://i.loli.net/2020/10/21/7vzBx364MykA8ao.png)
那咋办嘛
只好上网搜下常见的获取ip信息的免费api了，一堆人推荐的淘宝API早就改版了！没有accessKey什么鬼都不会给你好吗！
还好搜到了能用的accessKey（accessKey=alibaba-inc）
http://ip.taobao.com/outGetIpInfo?ip='.$ip.'&accessKey=alibaba-inc