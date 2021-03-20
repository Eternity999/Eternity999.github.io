---
title: web性能压力测试工具--Web Bench
tags:
  - '运维'
  - '性能测试'
  - '工具'
date: 2020-02-23 23:21:39
updated:
categories:
keywords:
description: Web Bench
top _img:
comments:
cover: https://pic4.zhimg.com/v2-fbb75babf06f50d6b1854e173b90a5dc_1440w.jpg
toc:
toc_number:
copyright:
copyright_author:
copyright_author_href:
copyright_url:
copyright_info:
mathjax:
katex:
aplayer:
highlight_shrink:
aside:
---
Webbench是Linux下的一个网站压力测试工具，它由Lionbridge公司（http://www.lionbridge.com）开发。它能测试处在相同硬件上，不同服务的性能以及不同硬件上同一个服务的运行状况。webbench的标准测试可以向我们展示服务器的两项内容：每秒钟相应请求数和每秒钟传输数据量。webbench不但能具有便准静态页面的测试能力，还能对动态页面（ASP,PHP,JAVA,CGI）进 行测试的能力。还有就是他支持对含有SSL的安全网站例如电子商务网站进行静态或动态的性能测试。Webbench最多可以模拟3万个并发连接去测试网站的负载能力。

官网：[http://home.tiscali.cz/~cz210552/webbench.html](http://home.tiscali.cz/~cz210552/webbench.html)

### 下载安装

依赖:ctags、gcc
如果没有安装 ctags make 编译会报错：/bin/sh: ctags: command not found
如果没有安装 gcc ，这时候可能会报错：
cc: Command not found
```bash
yum install gcc*  ctags* -y
```

```bash
wget http://home.tiscali.cz/~cz210552/distfiles/webbench-1.5.tar.gz
tar zxvf webbench-1.5.tar.gz 
cd webbench-1.5/
make
make install
webbench
```

### 用法
```bash
// webbench -c 并发数 -t 运行测试时间 URL
 webbench -c 100 -t 10 http://baidu.com/
```
参数说明
webbench [option]... URL
 -f|--force Don't wait for reply from server.
 -r|--reload Send reload request - Pragma: no-cache.
 -t|--time <sec> Run benchmark for <sec> seconds. Default 30.
 -p|--proxy <server:port> Use proxy server for request.
 -c|--clients <n> Run <n> HTTP clients at once. Default one.
 -9|--http09 Use HTTP/0.9 style requests.
 -1|--http10 Use HTTP/1.0 protocol.
 -2|--http11 Use HTTP/1.1 protocol.
 --get Use GET request method.
 --head Use HEAD request method.
 --options Use OPTIONS request method.
 --trace Use TRACE request method.
 -?|-h|--help This information.
 -V|--version Display program version.


注意：webbench 做压力测试时，该软件自身也会消耗CPU和内存资源，为了测试准确，请将 webbench 安装在别的服务器上。

### 经验总结
1. 压力测试工作应该放到产品上线之前，而不是上线以后；
2. 测试时并发应当由小逐渐加大，比如并发100时观察一下网站负载是多少、打开页面是否流畅，并发200时又是多少、网站打开缓慢时并发是多少、网站打不开时并发又是多少；
3. 更详细的进行某个页面测试，如电商网站可以着重测试购物车、推广页面等，因为这些页面占整个网站访问量比重较大。

### 参考资料
[（总结）Web性能压力测试工具之WebBench详解](http://www.ha97.com/4623.html)
[webbench源码分析](https://www.jianshu.com/p/dc1032b19c8d)