---
title: 使用APlayer&MetingJS插入音频
date: 2020-10-30 00:48:46
tags: 插件
categories: 分享
description: 🍭 Wow, such a beautiful HTML5 music player. 
cover: https://user-images.githubusercontent.com/2666735/30651452-58ae6c88-9deb-11e7-9e13-6beae3f6c54c.png
---
>🍭 Wow, such a beautiful HTML5 music player.

### 项目链接
https://github.com/MoePlayer/APlayer [【使用文档】](https://aplayer.js.org/#/zh-Hans/)
https://github.com/metowolf/MetingJS

#### 简单使用
在header上添加
```HTML
<link href="https://cdn.jsdelivr.net/npm/aplayer@1.7.0/dist/APlayer.min.css" rel="stylesheet">
<script src="https://cdn.jsdelivr.net/npm/aplayer@1.7.0/dist/APlayer.min.js"></script>
```
在footer上添加
```HTML
<script src="https://cdn.jsdelivr.net/npm/meting@1.1.0/dist/Meting.min.js"></script>
```
在使用的地方
```HTML
<div class="aplayer" data-id="60198" data-server="netease" data-type="playlist"></div>
<div class="aplayer" data-id="002QE24W26baEy" data-server="tencent" data-type="album" data-fixed="true" data-autoplay="false" data-volume="1.0" data-list-max-height="200px" data-list-folded="true"></div>
```
必要的参数:
<table>
<tr>
<td>data-id</td>
<td>音乐页面链接上的id号</td>
</tr>
<tr>
<td>data-server</td>
<td>平台名称。netease：网易；tencent：腾讯；xiami：虾米；kugou：酷狗；baidu：百度</td>
</tr>
<tr>
<td>data-type</td>
<td>类型。playlist：歌单；song：单曲；专辑：album；关键词：search；歌手：artist</td>
</tr>
</table>

### 写一个HTML单页
```HTML
<!DOCTYPE html>
<html>
<head>
    <link href="https://cdn.bootcss.com/aplayer/1.10.1/APlayer.min.css" rel="stylesheet">
    <script src="https://cdn.bootcss.com/aplayer/1.10.1/APlayer.min.js"></script>
    <style>
        .demo{width:360px;margin:60px auto 10px auto}
        .demo p{padding:10px 0}
    </style>
</head>
<body>
    <div class="demo">
        <p><strong>自制音乐播放器</strong></p>
        <div id="player1">
            <pre class="aplayer-lrc-content">
                [00:00.00] 作曲 : 林一峰
                [00:01.00] 作词 : 易家扬
                [00:24.898]听见 冬天的离开
                [00:29.697]我在某年某月 醒过来
                [00:34.768]我想 我等 我期待
                [00:40.598]未来却不能因此安排
                [00:53.398]阴天 傍晚 车窗外
                [00:58.758]未来有一个人在等待
                [01:04.298]向左向右向前看
                [01:09.599]爱要拐几个弯才来
                [01:14.369]我遇见谁 会有怎样的对白
                [01:19.638]我等的人 他在多远的未来
                [01:24.839]我听见风来自地铁和人海
                [01:30.399]我排着队 拿着爱的号码牌
                [01:56.388]阴天 傍晚 车窗外
                [02:02.298]未来有一个人在等待
                [02:06.650]向左向右向前看
                [02:12.000]爱要拐几个弯才来
                [02:16.980]我遇见谁 会有怎样的对白
                [02:22.289]我等的人 他在多远的未来
                [02:27.989]我听见风来自地铁和人海
                [02:32.688]我排着队 拿着爱的号码牌
                [02:43.380]我往前飞 飞过一片时间海
                [02:48.298]我们也曾在爱情里受伤害
                [02:53.689]我看着路 梦的入口有点窄
                [02:58.748]我遇见你是最美丽的意外
                [03:05.888]总有一天 我的谜底会揭开
            </pre>
        </div>
    </div>
    <script>
        var ap = new APlayer
                ({
                    element: document.getElementById('player1'),
                    narrow: false,
                    autoplay: true,
                    showlrc: true,
                    music: {
                            title: '遇见',
                            author: '孙燕姿',
                            url: 'http://music.163.com/song/media/outer/url?id=287035.mp3',
                            pic: 'http://y.gtimg.cn/music/photo_new/T002R300x300M000002ehzTm0TxXC2.jpg'
                            }
                });
        ap.init();
    </script>
</body>
</html>
```
APlayer参数：
<table>
	<tr><td>名称</td><td>默认值</td><td>描述</td></tr>
	<tr><td>container</td><td>document.querySelector('.aplayer')</td><td>播放器容器元素</td></tr>
	<tr><td>fixed</td><td>false</td><td>开启吸底模式, 详情</td></tr>
	<tr><td>mini</td><td>false</td><td>开启迷你模式, 详情</td></tr>
	<tr><td>autoplay</td><td>false</td><td>音频自动播放</td></tr>
	<tr><td>theme</td><td>'#b7daff'</td><td>主题色</td></tr>
	<tr><td>loop</td><td>'all'</td><td>音频循环播放, 可选值: 'all', 'one', 'none'</td></tr>
	<tr><td>order</td><td>'list'</td><td>音频循环顺序, 可选值: 'list', 'random'</td></tr>
	<tr><td>preload</td><td>'auto'</td><td>预加载，可选值: 'none', 'metadata', 'auto'</td></tr>
	<tr><td>volume</td><td>0.7</td><td>默认音量，请注意播放器会记忆用户设置，用户手动设置音量后默认音量即失效</td></tr>
	<tr><td>audio</td><td>-</td><td>音频信息, 应该是一个对象或对象数组</td></tr>
	<tr><td>audio.name</td><td>-</td><td>音频名称</td></tr>
	<tr><td>audio.artist</td><td>-</td><td>音频艺术家</td></tr>
	<tr><td>audio.url</td><td>-</td><td>音频链接</td></tr>
	<tr><td>audio.cover</td><td>-</td><td>音频封面</td></tr>
	<tr><td>audio.lrc</td><td>-</td><td>详情</td></tr>
	<tr><td>audio.theme</td><td>-</td><td>切换到此音频时的主题色，比上面的 theme 优先级高</td></tr>
	<tr><td>audio.type</td><td>'auto'</td><td>可选值: 'auto', 'hls', 'normal' 或其他自定义类型, 详情</td></tr>
	<tr><td>customAudioType</td><td>-</td><td>自定义类型，详情</td></tr>
	<tr><td>mutex</td><td>true</td><td>互斥，阻止多个播放器同时播放，当前播放器播放时暂停其他播放器</td></tr>
	<tr><td>lrcType</td><td>0</td><td>详情</td></tr>
	<tr><td>listFolded</td><td>false</td><td>列表默认折叠</td></tr>
	<tr><td>listMaxHeight</td><td>-</td><td>列表最大高度</td></tr>
	<tr><td>storageName</td><td>'aplayer-setting'</td><td>存储播放器设置的 localStorage key</td></tr>
</table>

MetingJS参数：
<table>
	<tr><td>option</td><td>default</td><td>description</td></tr>
	<tr><td>id</td><td>require</td><td>song id / playlist id / album id / search keyword</td></tr>
	<tr><td>server</td><td>require</td><td>music platform: netease, tencent, kugou, xiami, baidu</td></tr>
	<tr><td>type</td><td>require</td><td>song, playlist, album, search, artist</td></tr>
	<tr><td>auto</td><td>options</td><td>music link, support: netease, tencent, xiami</td></tr>
	<tr><td>fixed</td><td>false</td><td>enable fixed mode</td></tr>
	<tr><td>mini</td><td>false</td><td>enable mini mode</td></tr>
	<tr><td>autoplay</td><td>false</td><td>audio autoplay</td></tr>
	<tr><td>theme</td><td>#2980b9</td><td>main color</td></tr>
	<tr><td>loop</td><td>all</td><td>player loop play, values: 'all', 'one', 'none'</td></tr>
	<tr><td>order</td><td>list</td><td>player play order, values: 'list', 'random'</td></tr>
	<tr><td>preload</td><td>auto</td><td>values: 'none', 'metadata', 'auto'</td></tr>
	<tr><td>volume</td><td>0.7</td><td>default volume, notice that player will remember user setting, default volume will not work after user set volume themselves</td></tr>
	<tr><td>mutex</td><td>true</td><td>prevent to play multiple player at the same time, pause other players when this player start play</td></tr>
	<tr><td>lrc-type</td><td>0</td><td>lyric type</td></tr>
	<tr><td>list-folded</td><td>false</td><td>indicate whether list should folded at first</td></tr>
	<tr><td>list-max-height</td><td>340px</td><td>list max height</td></tr>
	<tr><td>storage-name</td><td>metingjs</td><td>localStorage key that store player setting</td></tr>
</table>

### 感谢
* [METO大佬](https://i-meto.com/)
