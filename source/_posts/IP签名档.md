---
title: IP签名档
date: 2020-10-21 15:55:21
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=2592365053,514857686&fm=26&gp=0.jpg
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
看了下PHP代码，调用了那人自己写的api，返回的都是空值
![ip_api.png](https://i.loli.net/2020/10/21/7vzBx364MykA8ao.png)
那咋办嘛
只好上网搜下常见的获取ip信息的免费API了，一堆人推荐的淘宝API早就改版了！没有accessKey什么鬼都不会给你好吗！
还好搜到了能用的accessKey（accessKey=alibaba-inc）
http://ip.taobao.com/outGetIpInfo?ip=$ip&accessKey=alibaba-inc
然后就能得到如下的JSON格式的信息
```
{"data":{"area":"","country":"中国","isp_id":"100025","queryIp":"120.229.108.xxx","city":"东莞","ip":"120.229.108.173","isp":"移动","county":"","region_id":"440000","area_id":"","county_id":null,"region":"广东","country_id":"CN","city_id":"441900"},"msg":"query success","code":0}
```
再通过获取到的城市，调用中华万年历的API：http://wthrcdn.etouch.cn/weather_mini?city=$region ，获取到当前的温度。
```
{"data":{"yesterday":{"date":"19日星期一","high":"高温 25℃","fx":"东北风","low":"低温 20℃","fl":"","type":"多云"},"city":"东莞","forecast":[{"date":"20日星期二","high":"高温 27℃","fengli":"","low":"低温 19℃","fengxiang":"北风","type":"多云"},{"date":"21日星期三","high":"高温 27℃","fengli":"","low":"低温 19℃","fengxiang":"北风","type":"多云"},{"date":"22日星期四","high":"高温 28℃","fengli":"","low":"低温 20℃","fengxiang":"北风","type":"多云"},{"date":"23日星期五","high":"高温 27℃","fengli":"","low":"低温 20℃","fengxiang":"东北风","type":"晴"},{"date":"24日星期六","high":"高温 25℃","fengli":"","low":"低温 20℃","fengxiang":"东北风","type":"晴"}],"ganmao":"感冒低发期，天气舒适，请注意多吃蔬菜水果，多喝水哦。","wendu":"27"},"status":1000,"desc":"OK"}
```
当日的天气取forecast[0]里面high、low值并用PHP的substr函数截取温度值即可。

#### 修复后
为了方便就把原项目fork了一份，修改后的项目地址：https://github.com/Eternity999/IP
效果：(静态的hexo没法展示成果)
![下载.jpg](https://i.loli.net/2020/10/21/p1mN7tgw46PEOhf.jpg)

### 类似的项目
https://www.liues.cn/lx-1147.html（手把手教如何写一个IP签名档）
https://www.liues.cn/lx-1327.html
使用了高德开发者平台的API来实现IP的定位和天气的数据
![ip签名档](https://www.liues.cn/wp-content/uploads/2020/01/20200127_085435_41.jpg)


### 注意事项
部署的网站域名不能套用CDN否则无法获取到真实IP

* 使用imagettftext()函数时报错Warning: imagettftext(): Could not find/open font。
查手册后发现由于GD版本更新，定义字体路径参数需要使用绝对路径。
可用获取绝对路径函数解决
```PHP
$fontpath = realpath('../fonts/abc.ttf');
```
* 使用imagettftext函数，页面不显示图片
注释掉header那行就知道错在哪了
