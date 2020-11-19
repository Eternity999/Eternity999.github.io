---
title: 自建iOS APP在线安装页面
date: 2020-11-12 17:51:00
tags: ios
description: 转载「突破国区/ID限制 自建iOS APP在线安装页面」
categories: 分享
cover: https://yorkchou.com/usr/uploads/2018/12/2756551164.png
---
>本文所述可能因ios的更新失效，时效性未作验证，因近期搜索发现彼萌大佬的文章删了所以mark一下，作为存档。
❗共享账号app的做法并不可取，有能力在外区付费购买app的请多支持开发者，同时谨慎选择淘宝等地方购买兑换码，很有可能因黑卡盗刷等信用问题对你的apple id封号甚至锁设备无法再下载软件。
❗使用他人的apple id切勿登入icloud，可能会被他人远程锁机。

一直不少朋友借我的apple id下载小火箭（最近一小心开了两步验证，登录麻烦了很多）
小火箭就不介绍了，是一个国区下架了的收费app，目前依旧是支持协议最多，操作最简单的网络代理app。

制作在线安装页就可以绕过App Store方便快捷地直接下载app。
需要注意的是，即便提高了下载安装的便捷度，但是安装完成后，首次打开，依旧需要填写已经购买相应APP的ID和密码，且首次登录后，由于iOS机制原因，iTunes与App Store系关联的，因此iTunes也会随之登录，如果存在敏感信息，记得首次登录后及时让对方注销或自己更改密码。

#### 在线安装页
[Get Shadowrocket](https://free.shadowrocket.online/)

## 如何制作
网站结构：
```
web
├── index.html                 #首页（导航页）
├── xxxxx文件夹              #用于存放静态网页所需的图片、js、css等
         ├── img              
         ├── js
         ├── css
├── 相关软件的ipa包       #必需（否则玩个🔨）
└── ipa.plist                     #软件包以及开发者信息
```
以下内容大量转载自：[突破国区/ID限制 自建iOS APP在线安装页面](https://yorkchou.com/ios-app-installation.html)
封面图片亦来自[York Chou](https://yorkchou.com/)
### 准备工作
#### 提取需要分享的iOS APP
iOS的APP为.ipa格式，我们需要将其提取，供用户下载，在这里我推荐一个最为简单且来自官方的.ipa文件提取方式。
iTunes 12.6.3.6是最后一个依旧支持App管理的版本[点击下载](https://dl.yorkchou.com/software/iTunes64Setup12.6.3.6.exe)，我们下载安装后，打开iTunes，登录已经购买了相应APP的ID账户，下载需要的APP，然后在资料库中右击“在Windows资源管理器中显示”，就能找到下载到的.ipa文件。
当然你也可以选择[Newlearner](https://www.newlearner.site/)的博主分享的[《利用Charles抓取旧版 iOS App》](https://www.newlearner.site/2018/12/19/charles-ipa.html)，该方法甚至实现了历史版本下载。
![image.png](https://i.loli.net/2020/11/12/UbLuVztpC3rg7no.png)

#### 编写ipa.plist
.ipa的安装，还需要ipa.plist文件，下面提供一份ipa.plist范例文件：
```XML
<?xml version="1.0" encoding="UTF-8"?><!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
    <dict>
        <key>items</key>
        <array>
            <dict>
                <key>assets</key>
                <array>
                    <dict>
                        <key>kind</key>
                        <string>software-package</string>
                        <key>url</key>
                        <string>请填上你的ipa下载地址(比如:http://www.example.com/app.ipa)</string>
                    </dict>
                </array>
                <key>metadata</key>
                <dict>
                    <key>bundle-identifier</key>
                     <string>开发者信息，需提取，见后文</string>
                     <key>bundle-version</key>
                    <string>版本号</string>
                    <key>kind</key>
                    <string>software</string>
                    <key>title</key>
                    <string>APP名字</string>
                </dict>
            </dict>
        </array>
    </dict>
</plist>
```
在以上代码中，除bundle-identifier/开发者信息，其余均可以根据实际分享的APP及其版本，自行填写。

#### 提取bundle-identifier/开发者信息 
我们使用压缩工具打开提取到的.ipa文件，会看到其中大致的内容如下：
![image.png](https://i.loli.net/2020/11/12/PR7towldJTeQLUX.png)
解压出其中的iTunesMetadata.plist文件，并用文本编辑器打开，并找到softwareVersionBundleId内容段，其中的内容就是ipa.plist文件中所需的bundle-identifier/开发者信息。下面是以Shadowrocket为例，则bundle-identifier/开发者信息为com.liguangming.Shadowrocket。
![image.png](https://i.loli.net/2020/11/12/rZGBuDAX4RkISUM.png)

### 一个好看的Web-UI
#### 下载
万事具备，只欠东风，我们接下来需要一个好看且容易操作的WebUI，博主[彼萌](https://bimoes.com/)就提供了一个非常好看的Web-UI，原文链接：~~https://9499460.com/87.html~~
![image.png](https://i.loli.net/2020/11/12/DoaWtHN6vzZkO8A.png)
我们首先下载源文件：
~~官方链接：https://files.re/codes/shadowrocket_online.zip~~已失效
备用链接：https://dl.yorkchou.com/web/shadowrocket_online.zip

#### 替换文件
由于博主彼萌的Web-UI是针对Shadowrocket这一款APP的，且其中内置的.ipa为其所有，因此我们需要将其中的.ipa文件及ipa.plist文件用上文提取和编写的进行替换。

#### 修改index.html
根据不同的App，我们也需要修改index.html中的代码。
首先是ipa.plist的链接，我们可以将ipa.plist上传至自己的服务器或OSS等，但是必须要是能够直接下载的直链。
![image.png](https://i.loli.net/2020/11/12/iJPS1ZYxtfUr8zd.png)
其次，博主彼萌为其贴心加入了ID账户及密码的点击复制功能，因此我们需要注意将index.html中的相应ID账户及密码，修改为上文中用来提取.ipa的ID账户及密码。
同时，index.html中的百度统计代码、底部版权信息，也可以根据你的需要自行修改。
![image.png](https://i.loli.net/2020/11/12/n1oYGitXdVK3haJ.png)

#### 修改App图标
压缩包中/assets/images/下的icon.jpg和favicon.ico分别为App的图标及网站图标，需自行根据实际情况生成并替换。

### 大功告成
至此，一切准备都已完成，将.ipa文件、WebUI一并上传至服务器/虚拟空间，创建网站即可，但是别忘了网站必须要有SSL证书，相信在Let's Encrypt的帮助下，对于各位站长来说这并不算太困难。（直接使用Cloudflare免費SSL更为省事）

## 关联阅读
[突破国区/ID限制 自建iOS APP在线安装页面](https://yorkchou.com/ios-app-installation.html)
[制作一个iOS app在线下载页面](https://www.newlearner.site/2018/12/22/iosapp-donwloading-online.html)
[plist苹果安装包实现](https://segmentfault.com/q/1010000000623121)
