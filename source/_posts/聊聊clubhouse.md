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
由于Clubhouse只有iOS客户端以及邀请机制新用户只能邀请0-2个人，这导致的邀请码极其稀缺，在国内火爆期间一码难求，邀请码售价高达400人民币到100美元不等。
这种邀请机制下，在Telegram出现了一种火种接力群，基本上一传一部分人一传二便能保持火种不断，我也是通过这种接力邀请的方式得以尝鲜。感谢 @NFNF2046 发起的接力群。在当时[@Linmi](https://linmi.cc/)也发起了相似的接力群。
值得一提的是，当时有个有同样接力功能的bot@（[ClubHouseQueueBot](https://t.me/ClubHouseQueueBot)）应运而生，但存在严重的信息泄露bug，首先它会记录使用者的tg号、手机号以及Clubhouse ID，但居然能通过/info命令把所有的信息罗列出来。
同时Clubhouse会在个人主页显示邀请者，有完整的用户邀请关系链，违规账号会被连坐处罚封号。像下文中提到的aieks的封号可能就会影响与之相关的邀请人。

### 时间线
2月7日有个room讨论“clubhouse明天会被墙吗”
2月8日被墙，+86号码无法接收验证短信
2月16日，[aieks](https://github.com/ai-eks)在v2ex推广自己基于Python Flask + Agora SDK开发的的第三方 Clubhouse 音频播放器项目--OpenClubhouse。同时引发clubhouse用户注意并讨论。
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

#### 推特网友对clubhouse的录音
<img src="https://photo.lyh.best/2021/02/26/3631785032af4.jpeg" alt="推特网友对clubhouse的录音" width="50%" height="50%">

### Clubhouse的安全性
由于Clubhouse的ID名字只能改一次，很多人使用了真实的姓名身份，以及配合邀请的链条，基本上就是在实名发言。从上面提到的几个安全问题可以看出，Clubhouse的使用和发言（指在公开房间中）并不私密，随时都可能被多种手段录音记录存档，如上述的OpenClubhouse、clubhouse-py等，只需要记录到当时的发言者，将录音导入到语音转文字的api中转换再导出，再做个关键词过滤，很快就能精准记录你说了什么不该说的话了。

### 趣闻
　　音频社交应用Clubhouse被马斯克带火之后，一家与之同名的公司ClubHouse Media Group Inc．（OTCMKTS：CMGR）因此意外飙涨，今年以来股价已飙升了1000%以上。这只美国股票的公司主体，实际上是广西同济健康医疗集团股份公司(Tongji Healthcare Group)。这家健康医疗集团在2020年8月，收购了Hudson Group公司，而后者全资拥有主营内容创作和营销（网红营销）的媒体公司“The ClubHouse”，这个媒体公司和真正热门的音频社交软件ClubHouse，没有任何关系。

#### 没有墙的隔阂，两岸人民会聊些什么
<img src="https://photo.lyh.best/2021/02/26/e8605560b855c.jpeg" alt="两岸的交流" width="50%" height="50%">

#### clubhouse火起来之后
<img src="https://photo.lyh.best/2021/02/26/ffe641c93444b.jpeg" alt="微博小文章" width="50%" height="50%">

#### 使用体验

clubhouse的语音交流是相当低效的知识获取过程，主要是初入人群相对比较高端，提供了一个平台如此近距离地和大佬交流并有可能建立联系，你有机会举手发言和奇葩说的辩手庞颖、各种公司ceo以及不同流域的大牛交流探讨问题。但在听他们的交流时可能并不会受益太多并可能会产生巨大的焦虑感和消磨了时间。

在被墙的前夕，大量的room管理员通过头像放二维码，导流到自己的企业微信群，转化为自己的私域流量。然后当时有个room就在讨论“惯性思维多可怕，用着Clubhouse留联系方式为什么不留iMessage？”room主@ngbin的bio则写道：“我快看不下去了，还都产品经理，还都号称翻墙了都会独立思考，CH之后iOS端，那你们为啥还要加微信？还要换头像扫码？为什么不用iMessage？”

在我进的不同room里，感受最深的时香港人发起的room是相对比较有秩序的，有专门主持的人控制时间，排序发言，听起来的感受会觉得这像是一个正式的访谈节目一样。

这种语音room的场景，颇像面试中群面环节，果然就有人在上面举办了模拟群面相关的room，还有大量求职、招聘的room，越听越让我这还没找到工作的大四废物焦虑。

根据clubhouse的算法，一加入不关注任何人是只有很少room推荐的，只有你关注更多的人，你才会看到你关注的人所在的room从而加入进去。同时，Clubhouse的room是中途没有邀请链接的，好像是只有开room的人能发room开启的预告时间以及邀请链接。所以很可能你退出了一个room的时候你follow的人也退出了，在期间你没关注房间内的人时，你就会尴尬地发现找不回那个room了。（在OpenClubhouse未封号之前，则可以通过上面列出的room链接进入该房间）

#### 使用场景
感觉玩Clubhouse这样的一个语音聊天室，适合下班回家的车内或者独居的状态，无论是外放被别人听到还是在会被熟悉的人听到的情况下大放厥词，都颇为尴尬。感觉利好airpods一类的产品，有良好的收音以及降噪功能的耳机会让你在使用这个软件的同时能干别的事情，不然感觉只专注于clubhouse语音交流，实在是太低效和消磨时间了。

#### 国内的仿品

国内多个互联网公司砸钱军备竞赛。。。
记忆中最早的是递爪，刚火爆的时候就说有相似的功能。
小米--米聊 2月19日停服的米聊，在7天后的2月26日秽土转生，宣布推出与Clubhouse像素级相似的针对高端人士的语音社交软件--米聊。（头七还魂）
映客--对话吧 上线12日后于2月22日紧急下架
36kr--coffeechat
微信小程序--clubhorse、clubchat+ 这名字仿得不想吐槽...，已消失。后者在其小程序中添加了大量虚假名人大V，因侵权而下架。
当然国外巨头twitter也推出了与clubhouse一样的产品。

看了这么多仿品，想到clubhouse早期用户中有着如此高浓度的产品经理，难道他们真的觉得这个产品的复刻能复现火爆而不是水土不服吗？有想过他们的平台会有哪些用户吗？会有Elon Musk、Bill Gates，还是会有国内对应咖位的人在上面设room交流？会有两岸三地的交流room？怕不是要割地自治画地为牢，签约某些行业大v在各自平台开room聊天，想听的人还要去下载不同的平台追随...像游戏开黑交流用的早有TeamSpeak、YY语音、TT语音、Discord等等...专业的远程会议软件也在疫情期间发展起来了...我真想不到像这样低效的语音聊天室除了上面比较精英的人群带来的吸引力，能有什么发展。

#### 一些个人想法
**关于墙**
在国内都需要审核监管的互联网环境下，Clubhouse 的被阻断是必然的。就算某部门没有及时关注这个平台，国内竞争者也可以用举报、投毒的方式来让其无法正常访问。
举个例子就懂了：
[陌生人交友应用Soul高管的骚操作：在竞争对手平台发布黄图举报致其下架](https://www.landiannews.com/archives/71108.html)

>利用GFW漏洞进行勒索的恶行正在蔓延
越来越多的信息表明有人正以屏蔽网站为要挟勒索大中型境外华文站点。
攻击者通过向目标网站提交大量包含违禁词的http明文请求、将被墙域名解析到目标网站所用IP等方式触发GFW的封锁机制。
攻击者要求网站以低廉的价格给他们投放广告，如果拒绝则进行上述的栽赃嫁祸。
更为糟糕的是越来越多的人正照猫画虎，当你有一把锤子看什么都像钉子。
那些选择托管于境外呕心沥血成长起来的网站现在要面临新的挑战。
[消息等级 Level B·#重要 ]<p align="right">——[VPS信号旗播报](https://t.me/vps_xhq)</p>