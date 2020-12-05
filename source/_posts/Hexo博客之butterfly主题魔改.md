---
title: Hexo博客之butterfly主题魔改
date: 2020-11-19 20:33:45
updated:
tags:
categories:
keywords:
description: 对butterfly主题的diy修改（或许持续更新）
top _img:
comments:
cover: https://i.loli.net/2020/11/19/lGq8mQ4rsAiUVY6.gif
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

### snow特效
在逛[毒奶](https://limbopro.xyz/)的博客时看到鼠标在头像框附近会有个下雪的特效，学习一下如何实现。
首先看到他网页源代码css是这样写的。
```css
#aside .wrapper:hover {
	background: url(https://limbopro.xyz/usr/themes/handsome/assets/img/snow.gif);
	background-size: cover;
	color: #999;
}
```
然后检查自己博客相应想修改的位置div class="card-content"，由于对hexo的源码不太熟悉，直接到上传本站的github上进行card-content关键词搜索，找到themes/butterfly/source/css/_layout/aside.styl文件。
看到对应的元素背景：
```styl
  .card-widget
    overflow: hidden
    margin-top: 1rem
    border-radius: 8px
    background: var(--card-bg)
    box-shadow: 0 4px 8px 6px rgba(7, 17, 27, .06)
    transition: all .3s
```
然后在上一级目录里的var.styl文件中加一行：
```styl
$card-author-bg = url(https://i.loli.net/2020/11/19/lGq8mQ4rsAiUVY6.gif)
```
再到/css/_global文件夹下的index.styl文件加入：
```sytl
  --card-author-bg: $card-author-bg
```
回到原来/css/_layout中的aside.styl文件写入：
```styl
  .card-widget:first-child:hover
    background: var(--card-author-bg)
```
完成

### 网站右侧添加悬浮QQ客服代码
右侧悬浮的企鹅小图像，点击后可以直接通过“QQ 在线”功能与客服进行“QQ 在线”弹窗交流！

可在任意单页body内插入如下代码：
```html
<style>.animated{-webkit-animation-duration:.5s;animation-duration:.5s;-webkit-animation-fill-mode:both;animation-fill-mode:both}.livechat-girl{width:60px;height:60px;border-radius:50%;position:fixed;top:80%;right:40px;opacity:0;-webkit-box-shadow:0 5px 10px 0 rgba(35,50,56,0.3);box-shadow:0 5px 10px 0 rgba(35,50,56,0.3);z-index:700;transform:translateY(0);-webkit-transform:translateY(0);-ms-transform:translateY(0);cursor:pointer;-webkit-transition:all 1s cubic-bezier(0.86,0,0.07,1);transition:all 1s cubic-bezier(0.86,0,0.07,1)}.livechat-girl:focus{outline:0}.livechat-girl.animated{opacity:1;transform:translateY(-40px);-webkit-transform:translateY(-40px);-ms-transform:translateY(-40px)}.livechat-girl:after{content:'';width:12px;height:12px;border-radius:50%;background-image:linear-gradient(to bottom,#38dc79,#1ab744);position:absolute;right:1px;top:1px;z-index:50}.livechat-girl .girl{position:absolute;top:0;left:0;width:100%;height:auto;z-index:50;border-radius:100%}.livechat-girl .animated-circles .circle{background:rgba(26,183,68,0.25);width:60px;height:60px;border-radius:50%;position:absolute;z-index:49;transform:scale(1);-webkit-transform:scale(1)}.livechat-girl .animated-circles.animated .c-1{animation:2000ms scaleToggleOne cubic-bezier(0.25,0.46,0.45,0.94) forwards}.livechat-girl .animated-circles.animated .c-2{animation:2500ms scaleToggleTwo cubic-bezier(0.25,0.46,0.45,0.94) forwards}.livechat-girl .animated-circles.animated .c-3{animation:3000ms scaleToggleThree cubic-bezier(0.25,0.46,0.45,0.94) forwards}.livechat-girl.animation-stopped .circle{opacity:0 !important}.livechat-girl .livechat-hint{position:absolute;right:40px;top:50%;margin-top:-20px;opacity:0;z-index:0;-webkit-transition:all 0.3s cubic-bezier(0.86,0,0.07,1);transition:all 0.3s cubic-bezier(0.86,0,0.07,1);background-color:#1ab744}.livechat-girl .livechat-hint.show_hint{-webkit-transform:translateX(-40px);transform:translateX(-40px);opacity:1}.livechat-girl .livechat-hint.hide_hint{opacity:0;-webkit-transform:translateX(0);transform:translateX(0)}.rd-notice-tooltip{-webkit-box-shadow:0 2px 2px rgba(0,0,0,0.2);box-shadow:0 2px 2px rgba(0,0,0,0.2);font-size:14px;border-radius:3px;line-height:1.25;position:absolute;z-index:65;max-width:350px}.rd-notice-tooltip.thumb-heart-tooltip{z-index:100;margin-top:19px}.rd-notice-tooltip.thumb-heart-tooltip .rd-notice-content{padding:10px 20px}.rd-notice-tooltip:after{position:absolute;display:block;content:'';height:20px;width:20px;-webkit-box-shadow:none;box-shadow:none;-webkit-transform:rotate(-45deg);-moz-transform:rotate(-45deg);-ms-transform:rotate(-45deg);-o-transform:rotate(-45deg);transform:rotate(-45deg);-webkit-border-radius:3px;-moz-border-radius:3px;border-radius:3px;z-index:50;top:10px;right:-6px;background-color:#1ab744}.rd-notice-tooltip .rd-notice-content{background:0;border-radius:3px;width:100%;color:#fff;position:relative;z-index:60;padding:20px;font-weight:400;line-height:1.45}.rd-notice-tooltip .rd-notice-content a{color:#fff;text-decoration:underline}.rd-notice-tooltip .arrow{display:none !important}.rd-notice-tooltip.alert.rd-closing{white-space:normal;text-align:left}.rd-notice-tooltip.alert.rd-closing .rd-notice-content{padding-right:50px}.rd-notice-tooltip.single-line .rd-notice-content{height:40px;padding:0 20px;line-height:40px;white-space:nowrap}@keyframes scaleToggleOne{from{transform:scale(1);-webkit-transform:scale(1)}50%{transform:scale(2);-webkit-transform:scale(2)}100%{transform:scale(1);-webkit-transform:scale(1)}}@keyframes scaleToggleTwo{0%{transform:scale(1);-webkit-transform:scale(1)}20%{transform:scale(1);-webkit-transform:scale(1)}60%{transform:scale(2);-webkit-transform:scale(2)}100%{transform:scale(1);-webkit-transform:scale(1)}}@keyframes scaleToggleThree{0%{transform:scale(1);-webkit-transform:scale(1)}33%{transform:scale(1);-webkit-transform:scale(1)}66%{transform:scale(2);-webkit-transform:scale(2)}100%{transform:scale(1);-webkit-transform:scale(1)}}</style>
<a class="livechat-girl js-livechat-girl animated" id="lc-girl-block-en_2" href="http://wpa.qq.com/msgrd?v=3&uin=403571895&site=qq&menu=yes" target="_blank"><img class="girl" border="0" src="https://img.onlinedown.net/download/202010/190754-5f99510a1585e.jpg" alt="点击这里给我发消息" title="点击这里给我发消息">
  <div class="js-livechat-hint livechat-hint rd-notice rd-notice-tooltip single-line hide_hint">
     <div class="popover-content rd-notice-content">嘿！有什么能帮到您的吗？</div>
     </div>
  <div class="animated-circles js-animated-circles animated">
    <div class="circle c-1"></div>
    <div class="circle c-2"></div>
    <div class="circle c-3"></div>
  </div>
</a>
<script type='text/javascript' src='https://cdn.jsdelivr.net/gh/jquery/jquery@3.2.1/dist/jquery.min.js'></script>
<script>
jQuery(function(){
        setInterval(function(){
            jQuery('.js-animated-circles').toggleClass('animated');
        },4000);
 
        jQuery('#lc-girl-block-en_2').on({'mouseover':function(){
            jQuery(this).find('.js-livechat-hint').removeClass('hide_hint').addClass('show_hint');
        },
            'mouseleave':function(){
                jQuery(this).find('.js-livechat-hint').removeClass('show_hint').addClass('hide_hint');
            }
        })
    });
</script>
```

#### 个人 QQ 号码的替换：
代码第二行中，将http://wpa.qq.com/msgrd?v=3&uin=403571895&site=qq&menu=yes 这个链接中的403571895替换为你的 QQ 号码，同时你要在[QQ推广](https://shang.qq.com/v3/index.html)开通QQ通讯组件功能。

我们还要解决一个问题，就是想要这个代码，不出现在平版设备或者手机设备的页面上，要解决这个问题，只需要在第一行代码的style标签后面加入下面一段代码即可：
```css
@media(max-width:880px){.livechat-girl{display:none}}
```

#### 整合到butterfly主题中
直接在_config.butterfly.yml文件中搜索插入，在Inject栏的bottom下插入代码：
```yml
    - <style>@media(max-width:880px){.livechat-girl{display:none}}.animated{-webkit-animation-duration:.5s;animation-duration:.5s;-webkit-animation-fill-mode:both;animation-fill-mode:both}.livechat-girl{width:60px;height:60px;border-radius:50%;position:fixed;top:80%;right:40px;opacity:0;-webkit-box-shadow:0 5px 10px 0 rgba(35,50,56,0.3);box-shadow:0 5px 10px 0 rgba(35,50,56,0.3);z-index:700;transform:translateY(0);-webkit-transform:translateY(0);-ms-transform:translateY(0);cursor:pointer;-webkit-transition:all 1s cubic-bezier(0.86,0,0.07,1);transition:all 1s cubic-bezier(0.86,0,0.07,1)}.livechat-girl:focus{outline:0}.livechat-girl.animated{opacity:1;transform:translateY(-40px);-webkit-transform:translateY(-40px);-ms-transform:translateY(-40px)}.livechat-girl:after{content:'';width:12px;height:12px;border-radius:50%;background-image:linear-gradient(to bottom,#38dc79,#1ab744);position:absolute;right:1px;top:1px;z-index:50}.livechat-girl .girl{position:absolute;top:0;left:0;width:100%;height:auto;z-index:50;border-radius:100%}.livechat-girl .animated-circles .circle{background:rgba(26,183,68,0.25);width:60px;height:60px;border-radius:50%;position:absolute;z-index:49;transform:scale(1);-webkit-transform:scale(1)}.livechat-girl .animated-circles.animated .c-1{animation:2000ms scaleToggleOne cubic-bezier(0.25,0.46,0.45,0.94) forwards}.livechat-girl .animated-circles.animated .c-2{animation:2500ms scaleToggleTwo cubic-bezier(0.25,0.46,0.45,0.94) forwards}.livechat-girl .animated-circles.animated .c-3{animation:3000ms scaleToggleThree cubic-bezier(0.25,0.46,0.45,0.94) forwards}.livechat-girl.animation-stopped .circle{opacity:0 !important}.livechat-girl .livechat-hint{position:absolute;right:40px;top:50%;margin-top:-20px;opacity:0;z-index:0;-webkit-transition:all 0.3s cubic-bezier(0.86,0,0.07,1);transition:all 0.3s cubic-bezier(0.86,0,0.07,1);background-color:#1ab744}.livechat-girl .livechat-hint.show_hint{-webkit-transform:translateX(-40px);transform:translateX(-40px);opacity:1}.livechat-girl .livechat-hint.hide_hint{opacity:0;-webkit-transform:translateX(0);transform:translateX(0)}.rd-notice-tooltip{-webkit-box-shadow:0 2px 2px rgba(0,0,0,0.2);box-shadow:0 2px 2px rgba(0,0,0,0.2);font-size:14px;border-radius:3px;line-height:1.25;position:absolute;z-index:65;max-width:350px}.rd-notice-tooltip.thumb-heart-tooltip{z-index:100;margin-top:19px}.rd-notice-tooltip.thumb-heart-tooltip .rd-notice-content{padding:10px 20px}.rd-notice-tooltip:after{position:absolute;display:block;content:'';height:20px;width:20px;-webkit-box-shadow:none;box-shadow:none;-webkit-transform:rotate(-45deg);-moz-transform:rotate(-45deg);-ms-transform:rotate(-45deg);-o-transform:rotate(-45deg);transform:rotate(-45deg);-webkit-border-radius:3px;-moz-border-radius:3px;border-radius:3px;z-index:50;top:10px;right:-6px;background-color:#1ab744}.rd-notice-tooltip .rd-notice-content{background:0;border-radius:3px;width:100%;color:#fff;position:relative;z-index:60;padding:20px;font-weight:400;line-height:1.45}.rd-notice-tooltip .rd-notice-content a{color:#fff;text-decoration:underline}.rd-notice-tooltip .arrow{display:none !important}.rd-notice-tooltip.alert.rd-closing{white-space:normal;text-align:left}.rd-notice-tooltip.alert.rd-closing .rd-notice-content{padding-right:50px}.rd-notice-tooltip.single-line .rd-notice-content{height:40px;padding:0 20px;line-height:40px;white-space:nowrap}@keyframes scaleToggleOne{from{transform:scale(1);-webkit-transform:scale(1)}50%{transform:scale(2);-webkit-transform:scale(2)}100%{transform:scale(1);-webkit-transform:scale(1)}}@keyframes scaleToggleTwo{0%{transform:scale(1);-webkit-transform:scale(1)}20%{transform:scale(1);-webkit-transform:scale(1)}60%{transform:scale(2);-webkit-transform:scale(2)}100%{transform:scale(1);-webkit-transform:scale(1)}}@keyframes scaleToggleThree{0%{transform:scale(1);-webkit-transform:scale(1)}33%{transform:scale(1);-webkit-transform:scale(1)}66%{transform:scale(2);-webkit-transform:scale(2)}100%{transform:scale(1);-webkit-transform:scale(1)}}</style>
    - <a class="livechat-girl js-livechat-girl animated" id="lc-girl-block-en_2" href="http://wpa.qq.com/msgrd?v=3&uin=403571895&site=qq&menu=yes" target="_blank"><img class="girl" border="0" src="https://img.onlinedown.net/download/202010/190754-5f99510a1585e.jpg" alt="点击这里给我发消息" title="点击这里给我发消息">
    - <div class="js-livechat-hint livechat-hint rd-notice rd-notice-tooltip single-line hide_hint">
    - <div class="popover-content rd-notice-content">嘿！有什么能帮到您的吗？</div>
    - </div>
    - <div class="animated-circles js-animated-circles animated">
    - <div class="circle c-1"></div>
    - <div class="circle c-2"></div>
    - <div class="circle c-3"></div>
    - </div>
    - </a>
    - <script type='text/javascript' src='https://cdn.jsdelivr.net/gh/jquery/jquery@3.2.1/dist/jquery.min.js'></script>
    - <script>
    - jQuery(function(){setInterval(function(){jQuery(".js-animated-circles").toggleClass("animated")},4000);jQuery("#lc-girl-block-en_2").on({"mouseover":function(){jQuery(this).find(".js-livechat-hint").removeClass("hide_hint").addClass("show_hint")},"mouseleave":function(){jQuery(this).find(".js-livechat-hint").removeClass("show_hint").addClass("hide_hint")}})});
    - </script>
```
其实代码我们已经搞明白的情况下就不需要一行一行地插入了，可以运用工具[在线JS/CSS/HTML压缩](http://tool.oschina.net/jscompress/)直接把代码压缩成一行插入。
效果图：
<img src="https://i.loli.net/2020/12/03/BcuJlCFg23EAqSL.png" width="40%" height="40%">

#### BUG
加了这个后，右下角的一些按钮（阅读模式、繁简转换）就虚无了，所以并未实际应用到博客上。


### 关联阅读
[Hexo博客之butterfly主题优雅魔改系列（持续更新）](https://www.cnblogs.com/antmoe/p/12846393.html)
