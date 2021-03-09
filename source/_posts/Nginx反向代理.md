---
title: Nginx反向代理
date: 2021-03-09 21:56:05
updated:
tags: Nginx
categories: 
keywords:
description: Nginx反向代理
top _img:
comments:
cover: https://pic3.zhimg.com/v2-cac94d7c539964fed044c3091e390260_1440w.jpg
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
前两天的博文 [GDUT粤港机器人学院简介](/20210306/GDUT粤港机器人学院/) 里用 iframe 嵌套 [xbotpark机器人学院](http://www.xbotpark.com/robotic/) 的页面。由于 safari 中的 iframe 不支持 http 的加载，只支持 https。导致了手机上看到空白的 iframe 部分。而 xbotpark 的网站并没有配置 ssl，因此用自己的 vps 和域名对其反向代理再嵌套。
Nginx配置中插入
```conf
#PROXY-START/
location  ~* \.(php|jsp|cgi|asp|aspx)$
{
    proxy_pass http://www.xbotpark.com;
    proxy_set_header Host www.xbotpark.com;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header REMOTE-HOST $remote_addr;
}
location /
{
    proxy_pass http://www.xbotpark.com;
    proxy_set_header Host www.xbotpark.com;
    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header REMOTE-HOST $remote_addr;
    
    add_header X-Cache $upstream_cache_status;
    
    #Set Nginx Cache
    
    	add_header Cache-Control no-cache;
    expires 12h;
}

#PROXY-END/
```
### 参考资料
[nginx教程](https://nginx.rails365.net/)