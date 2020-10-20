---
title: PT下载
date: 2020-10-19 12:24:05
tags: PT
---
[![BTSCHOOL](https://pt.btschool.club/pic/prolink.png "BTSCHOOL - 汇聚每一个人的影响力")](https://pt.btschool.club/promotionlink.php?key=493f313256638158bfe90b22c5164eb6)

碰巧国庆期间遇上了[PTSCHOOL](https://pt.btschool.club/promotionlink.php?key=493f313256638158bfe90b22c5164eb6)的开放注册，并快速顺利通过新人考核。记录一下混PT站的心得。

## PT站新手指北

### 注册
大多数PT站正常状态下关闭自由注册，只允许邀请注册或会在特定日子开放注册。
可以通过万能的捐赠成为会员或者找到能够邀请你进入PT站的朋友。
（顺路求个馒头PT的邀请）

### 新人考核
考核任务在30天内达到：
* 做种率： 5.0 （做种/下载时间比率）
* 上传量： 50G
* 下载量： 50G
* 魔力值： 5000

国内PT站点基本上都是同一套魔力值公式：
![魔力值](http://5b0988e595225.cdn.sohucs.com/images/20190921/b31583e9269d40ce9b8137b8dff155e5.png "魔力值计算公式")


### 如何通过

做种率：只要下载完资源不删并在后台开启了bt客户端都会处于做种状态，正常挂着就能达标。
下载量：下载非FREE种计算量到达50G即可。
上传量：国内的运营商都使用NAT而并没有公网IP并且上下行并不对等，上传量是比较难提上去的，甚至是你发布的种子上传量都被一些PT盒子们抢走是你的好几倍，但是只要你选择手头上有的大文件资源发布并做种，上传量一下子就上来了毕竟再怎么差的网络环境做种只要有一个人下载完成分享率也有1.0嘛。我选择使用手头上空闲的VPS下载一些刚发布刚开始做种的文件下载，就能蹭到比较多的上传量（其实就是站内seedboxes在互拉文件刷量...）
魔力值：根据魔力值计算公式，把站内种子按大小倒序排列，下最小的100个种子挂着做种，即可达到每小时50魔力值。

### 如何发布种子
uTorrent种子制作
![制作种子.png](https://i.loli.net/2020/10/20/9oX2tbTxhN6vjl5.png)
然后到PT站上发布候选，等投票通过后上传种子到网站上，再把带有个人passkey的种子下载丢进pt客户端，校验完毕就开始做种了。


### 客户端选择
Windows上我使用的是uTorrent。
VPS是在CentOS7上安装Transmission并搭配webui进行管理。（在[荒岛](https://lala.im)博客里发现的宝藏项目是真的多）

安装EPEL源：
``` 
$ yum -y install epel-release
```
然后直接使用yum安装
``` 
yum -y install transmission transmission-daemon
```
Transmission的配置文件需要在第一次启动后才会生成
``` 
systemctl start transmission-daemon
systemctl stop transmission-daemon
```
然后编辑它的配置文件
```
vi /var/lib/transmission/.config/transmission-daemon/settings.json
```
找出以下5个值进行修改
rpc-authentication-required的值改为true。
rpc-host-whitelist-enabled的值改为false。
rpc-password请设置一个高强度的密码。
rpc-username是你的WEBGUI登录用户名，这里可以自定义填写。
rpc-whitelist-enabled的值改为false。

重新运行Transmission：
``` 
systemctl start transmission-daemon
```
如无意外通过浏览器访问你的VPS公网IP:端口9091应该就可以访问到Transmission的WEB界面，通过上面刚刚设置的用户名密码登录操作。

原生是Transmission WEB界面太丑了，找到网上的第三方TransmissionWEBUI项目：https://github.com/ronggang/transmission-web-control

下载脚本并安装：
``` 
wget https://github.com/ronggang/transmission-web-control/raw/master/release/install-tr-control.sh --no-check-certificate
bash install-tr-control.sh
```
完成后重新访问WEB界面，瞬间焕然一新，可以根据自己的需求切换不同的Theme以及移动端界面和原生界面。
![Transmisson WEBUI](https://user-images.githubusercontent.com/8065899/38598199-0d2e684c-3d8e-11e8-8b21-3cd1f3c7580a.png)


### 注意事项
记得进站先看PT站的规则和常见问题，再到论坛看置顶帖以及新手区的一些内容，很快就能熟悉并上手。
PT站都有启用H&R考核（Hit and Run）打击下完就跑的吸血者，所以要有自觉保种的好习惯，最少也要根据规则做种够20小时或分享率达1.0以上。
不然再规定时间内没达到要求就会记录H&R并且只能用高额魔力值消除，H&R达到一定量就你号没了...
下载资源后改变了位置就显示没在做种的情况，在客户端重新打开那个种子并选择你文件所在的地方为下载路径，就能自动校验并继续做种。