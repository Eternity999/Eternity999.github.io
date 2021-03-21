---
title: GitHub加速
tags:
  - '工具'
  - '代理'
date: 2021-03-21 01:49:55
updated:
categories:
keywords:
description: gh-proxy——基于cloudflare workers的GitHub文件加速
top _img:
comments:
cover: https://static.wixstatic.com/media/b99025_4bd0764828f54aaaa6a83e7c86e5289f~mv2.jpg
toc:
toc_number:
copyright: true
copyright_author: hunsh
copyright_author_href: https://hunsh.net/
copyright_url: https://hunsh.net/archives/23/
copyright_info: 本文由 hunsh 创作，采用 知识共享署名4.0 国际许可协议进行许可
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---
>最近很多例子表明，从这个月初开始（2021.3），github 在部分地区遭到 sni 探测阻断，就是 github 的域名指向哪个 ip，哪个 ip 的 443 端口和本地的连接就会被劣化至几乎不可用的状态。这个是针对域名的攻击，无关 dns，改 hosts 是无解的。--	[ruixue](https://www.v2ex.com/t/761907) 


### GitHub 文件加速
演示：[https://gh.api.99988866.xyz/](https://gh.api.99988866.xyz/)
项目基于Cloudflare Workers，开源于[GitHub hunshcn/gh-proxy](https://github.com/hunshcn/gh-proxy)

以下都是合法输入：

* 分支源码：https://github.com/hunshcn/project/archive/master.zip
* release源码：https://github.com/hunshcn/project/archive/v0.1.0.tar.gz
* release文件：https://github.com/hunshcn/project/releases/download/v0.1.0/example.zip
* 分支文件：https://github.com/hunshcn/project/blob/master/filename
* commit文件：https://github.com/hunshcn/project/blob/1111111111111111111111111111/filename

#### cf worker版本部署
首页：[https://workers.cloudflare.com](https://workers.cloudflare.com)
注册，登陆，Start building，取一个子域名，Create a Worker。
复制 index.js 到左侧代码框，Save and deploy。如果正常，右侧应显示首页。
index.js默认配置下clone走github.com.cnpmjs.org，项目文件会走jsDeliver，如需走worker，修改Config变量即可

#### Python版本部署
##### Docker部署
```bash
docker run -d --name="gh-proxy-py" \
  -p 0.0.0.0:80:80 \
  --restart=always \
  hunsh/gh-proxy-py:latest
```
第一个80是你要暴露出去的端口

##### 直接部署
安装依赖（请使用python3）
pip install flask requests
按需求修改app/main.py的前几项配置

##### 注意
python版本的机器如果无法正常访问github.io会启动报错，请自行修改静态文件url
默认配置下clone走github.com.cnpmjs.org，项目文件会走jsDeliver，如需走服务器，修改配置即可

##### 计费
到 overview 页面可参看使用情况。免费版每天有 10 万次免费请求，并且有每分钟1000次请求的限制。
如果不够用，可升级到 $5 的高级版本，每月可用 1000 万次请求（超出部分 $0.5/百万次请求）。

##### 参考
jsproxy

### 参考资料
以上部署方法来源：
[开源分享：gh-proxy——基于cloudflare workers的GitHub文件加速](https://hunsh.net/archives/23/)