---
title: 聊聊Clubhouse
date: 2021-02-26 15:30:31
updated:
tags:
categories:
keywords:
description: 关于clubhouse的使用观察
top _img:
comments:
cover: https://pic4.zhimg.com/v2-14a540aa983aa94c0b19326bbf44ddd0_1440w.jpg?source=172ae18b
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

## Clubhouse
Clubhouse在国内火起来大概是在1月31日，马斯克在社交平台发布了一条推文，他将于北京时间2月1日的下午两点在Clubhouse创建聊天室。
![](https://img.36krcdn.com/20210219/v2_647d87d5a7ec4c8f946c619dd24833df_img_000)

### 时间线
2月7日有个room讨论“clubhouse明天会被墙吗”
2月8日被墙，+86号码无法接收验证短信
2月16日，[aieks](https://github.com/ai-eks)在v2ex推广自己基于Python Flask + Agora SDK开发的的第三方 Clubhouse 音频播放器--OpenClubhouse。同时引发clubhouse用户注意并讨论。
网站链接: [https://opench.aix.uy/](https://opench.aix.uy/)（2月21日被clubhouse封号）
相关新闻：
> #互联网 #隐私 #安全 #信息安全 #Clubhouse
【Clubhouse安全性存疑：聊天音频泄露至第三方】
有消息指出近期大热的邀请制音频聊天室软件 Clubhouse 可能被第三方窃听。上周末发生的一起攻击，让 Clubhouse 的安全问题引发了更多网络专家的担忧。
据彭博社2月21日报道，Clubhouse 的发言人 Reema Bahnasy 证实，一位身份不明的用户本周末从“多个房间”将音频流传输到了自己的第三方网站中。尽管公司表示，已经“永久封禁”该用户并安装了新的“保障措施”以阻止类似事件重复发生，但研究者认为该平台可能无法做出这种保证。
美国斯坦福大学下属研究机构斯坦福互联网观察实验室（Stanford Internet Observatory）于2月13日首次提出了该应用的安全担忧。2月21日晚些时候，该实验室再次发声称，Clubhouse 应该假设平台上所有的对话都被录音。
斯坦福互联网观察实验室主管 Alex Stamos 表示：“Clubhouse 不能为世界各地进行的对话提供任何隐私承诺”，值得一提的是，他同时也是 Facebook 前网络安全主管。
处理 Clubhouse 大部分后端业务的上海创业公司 Agora 表示，它无法评论 Clubhouse 的安全或隐私协议，并坚称它不会对任何客户 "存储或分享个人身份信息"，Clubhouse只是其中之一。"我们致力于使我们的产品尽可能地安全。"该公司说。
随着 Clubhouse 的全球流行，近期该公司完成了1亿美元募资，估值达到10亿美元。([澎湃新闻](https://www.thepaper.cn/newsDetail_forward_11414111))([彭博社·Bloomberg](https://www.bloomberg.com/news/articles/2021-02-22/clubhouse-chats-are-breached-raising-concerns-over-security))

### Python Flask + Agora SDK = [clubhouse-py客户端](https://github.com/stypr/clubhouse-py)
<video src="https://photo.lyh.best/2021/02/26/f3fc008b01cae.mp4" alt="Python Flask + Agora SDK.mp4" width="100%" height="100%" controls="controls"></video>

### 趣闻
　　音频社交应用Clubhouse被马斯克带火之后，一家与之同名的公司ClubHouse Media Group Inc．（OTCMKTS：CMGR）因此意外飙涨，今年以来股价已飙升了1000%以上。这只美国股票的公司主体，实际上是广西同济健康医疗集团股份公司(Tongji Healthcare Group)。这家健康医疗集团在2020年8月，收购了Hudson Group公司，而后者全资拥有主营内容创作和营销（网红营销）的媒体公司“The ClubHouse”，这个媒体公司和真正热门的音频社交软件ClubHouse，没有任何关系。

#### 推特网友对clubhouse的录音
<img src="https://photo.lyh.best/2021/02/26/3631785032af4.jpeg" alt="推特网友对clubhouse的录音" width="50%" height="50%">

#### 没有墙的隔阂，两岸人民会聊些什么
<img src="https://photo.lyh.best/2021/02/26/e8605560b855c.jpeg" alt="两岸的交流" width="50%" height="50%">

#### clubhouse火起来之后
<img src="https://photo.lyh.best/2021/02/26/ffe641c93444b.jpeg" alt="微博小文章" width="50%" height="50%">

#### 使用体验

clubhouse的语音交流是相当低效的知识获取过程，主要是初入人群相对比较高端，提供了一个平台如此近距离地和大佬交流并有可能建立联系，你有机会举手发言和奇葩说的辩手庞颖、各种公司ceo以及不同流域的大牛交流探讨问题。但在听他们的交流时可能并不会受益太多并可能会产生巨大的焦虑感和消磨了时间。
在被墙的前夕，大量的room管理员通过头像放二维码，导流到自己的企业微信群，转化为自己的私域流量。然后当时有个room就在讨论“惯性思维多可怕，用着Clubhouse留联系方式为什么不留iMessage？”room主@ngbin的bio则写道：“我快看不下去了，还都产品经理，还都号称翻墙了都会独立思考，CH之后iOS端，那你们为啥还要加微信？还要换头像扫码？为什么不用iMessage？”
在我进的不同room里，感受最深的时香港人发起的room是相对比较有秩序的，有专门主持的人控制时间，排序发言，听起来的感受会觉得这像是一个正式的访谈节目一样。


