---
title: robocon
date: 2021-03-09 19:40:30
updated:
tags:
categories:
keywords:
description:
top _img:
comments:
cover:
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
{% raw %}
<!--设置外部div样式，尽量不要写在页面div style中，有可能不起作用-->
.show_iframe{
-webkit-overflow-scrolling: touch;
overflow-y: 
scroll;position: absolute;
top: 0;
right: 0;
left: 0;
bottom: 0;
}
.show_iframe iframe {position: absolute;bottom: 0;height: 100%;width: 100%}
{% endraw %}
<!--在iframe外包一个div-->
<div class="show_iframe">
			<div style="display:none" class="loading"></div>
			<iframe scrolling="yes" frameborder="0" wicket:id="mainPage" src="https://photo.lyh.best/2021/03/09/3b998d820df3b.pdf" type="application/pdf"></iframe>
</div>
