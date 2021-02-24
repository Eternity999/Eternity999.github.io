---
title: BASE64加解密
date: 2021-02-24 03:17:49
updated:
tags:
categories:
keywords:
description: BASE64加解密小工具
top _img:
comments:
cover: https://ss3.bdstatic.com/70cFv8Sh_Q1YnxGkpoWK1HF6hhy/it/u=1214333833,130892204&fm=26&gp=0.jpg
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
### BASE64加解密小工具
{% raw %}
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <div class="panel-heading font-bold">BASE64加密解密</div>
                <textarea class="textarea form-control" id="best" rows="5"></textarea>
            <div class="text-center">
                <button type="submit" id="btn1" class="btn btn-info">加密</button>&nbsp;
                <button type="submit" id="btn2" class="btn btn-info">解密</button>
            </div>
        <div class="entry-content l-h-2x" id="data">
        </div>
</head>

<script type="text/javascript">
    $.extend({
        message: function (a) {
            var b = {};
            "string" == typeof a && (b.message = a), "object" == typeof a && (b = $.extend({}, b, a));
            var c, d, e, f = b.showClose ? '<div class="c-message--close">×</div>' : "",
                g = "" !== b.title ? '<h2 class="c-message__title">' + b.title + "</h2>" : "",
                h = '<div class="c-message animated animated-lento slideInRight"><i class=" c-message--icon c-message--' + b.type + '"></i><div class="el-notification__group">' + g + '<div class="el-notification__content">' + b.message + "</div>" + f + "</div></div>",
                i = $("body"),
                j = $(h);
            d = function () {
                j.addClass("slideOutRight"), j.one("webkitAnimationEnd mozAnimationEnd MSAnimationEnd oanimationend animationend", function () {
                    e()
                })
            }, e = function () {
                j.remove(), b.onClose(b), clearTimeout(c)
            }, $(".c-message").remove(), i.append(j), j.one("webkitAnimationEnd mozAnimationEnd MSAnimationEnd oanimationend animationend", function () {
                j.removeClass("messageFadeInDown")
            }), i.on("click", ".c-message--close", function (a) {
                d()
            }), b.autoClose && (c = setTimeout(function () {
                d()
            }, b.time))
        }
    })
</script>
<script>
    var keyStr = "ABCDEFGHIJKLMNOP" +
        "QRSTUVWXYZabcdef" +
        "ghijklmnopqrstuv" +
        "wxyz0123456789+/" +
        "=";
    function encode64(input) {
        input = escape(input);
        var output = "";
        var chr1, chr2, chr3 = "";
        var enc1, enc2, enc3, enc4 = "";
        var i = 0;
        do {
            chr1 = input.charCodeAt(i++);
            chr2 = input.charCodeAt(i++);
            chr3 = input.charCodeAt(i++);
            enc1 = chr1 >> 2;
            enc2 = ((chr1 & 3) << 4) | (chr2 >> 4);
            enc3 = ((chr2 & 15) << 2) | (chr3 >> 6);
            enc4 = chr3 & 63;
            if (isNaN(chr2)) {
                enc3 = enc4 = 64;
            }
            else if (isNaN(chr3)) {
                enc4 = 64;
            }
            output = output +
                keyStr.charAt(enc1) +
                keyStr.charAt(enc2) +
                keyStr.charAt(enc3) +
                keyStr.charAt(enc4);
            chr1 = chr2 = chr3 = "";
            enc1 = enc2 = enc3 = enc4 = "";
        } while (i < input.length);
        return output;
    }
    function decode64(input) {
        var output = "";
        var chr1, chr2, chr3 = "";
        var enc1, enc2, enc3, enc4 = "";
        var i = 0;
        var base64test = /[^A-Za-z0-9\+\/\=]/g;
        if (base64test.exec(input)) {
            $.message({
                title: '工具提示',
                message: '请输入有效的base64字符',
                type: 'warning'
            });
        }
        input = input.replace(/[^A-Za-z0-9\+\/\=]/g, "");
        do {
            enc1 = keyStr.indexOf(input.charAt(i++));
            enc2 = keyStr.indexOf(input.charAt(i++));
            enc3 = keyStr.indexOf(input.charAt(i++));
            enc4 = keyStr.indexOf(input.charAt(i++));
            chr1 = (enc1 << 2) | (enc2 >> 4);
            chr2 = ((enc2 & 15) << 4) | (enc3 >> 2);
            chr3 = ((enc3 & 3) << 6) | enc4;
            output = output + String.fromCharCode(chr1);
            if (enc3 != 64) {
                output = output + String.fromCharCode(chr2);
            }
            if (enc4 != 64) {
                output = output + String.fromCharCode(chr3);
            }
            chr1 = chr2 = chr3 = "";
            enc1 = enc2 = enc3 = enc4 = "";
        } while (i < input.length);
        return unescape(output);
    }
    $('#btn1').click(function () {
        var best = $('#best').val();
        if (best == "") {
            $.message({
                title: '工具提示',
                message: '请输入您要加密的内容',
                type: 'warning'
            });
        } else {
            $.message({
                title: '工具提示',
                message: '加密成功',
                type: 'success'
            });
            $('#data').html('<p class="tip inlineBlock success">原文：' + best + '<br>加密：' + encode64(best) + '</p>');
        }
    });
    $('#btn2').click(function () {
        var best = $('#best').val();
        if (best == "") {
            $.message({
                title: '工具提示',
                message: '请输入您要解密的内容',
                type: 'warning'
            });
        } else {
            $.message({
                title: '工具提示',
                message: '解密成功',
                type: 'warning'
            });
            $('#data').html('<p class="tip inlineBlock success">原文：' + best + '<br>解密：' + decode64(best) + '</p>');
        }
    });
</script>
</html>
{% endraw %}

### 尝试在hexo中嵌入html代码
在hexo的github issue中找到 [hexo能在markdown中插入一段html代码不被渲染么？\(´･\_･\`\)](https://github.com/hexojs/hexo/issues/1692)

```markdown
{% raw %}
your html
{% endraw %}
```
详细参考：[hexo中tag plugins的用法](https://hexo.io/docs/tag-plugins)

#### 踩坑
注意插入的html中使用jQuery插件时避免重复引入jquery.js文件
debug过程
1. 猜测jQuery加载顺序不是最早造成的。
2. F12工具查看 JS 的加载顺序，发现 jQuery 是最早加载的，只是加页面加载完毕后，突然有个请求又加载了一次 jQuery

由于我用的是hexo的butterfly主题，然后就到 ```.\themes\butterfly\layout\includes\additional-js.pug``` 中把 ```script(src=url_for(theme.CDN.jquery))```注释掉，再到hexo的 ```_config.butterfly.yml```配置里 inject项中把jquery插入到```</head>```之前。

```yml
# Inject
# Insert the code to head (before '</head>' tag) and the bottom (before '</body>' tag)
# 插入代码到头部 </head> 之前 和 底部 </body> 之前
inject:
  head:
  # - <link rel="stylesheet" href="/xxx.css">
    - <script type="text/javascript" src="https://cdn.jsdelivr.net/npm/jquery@latest/dist/jquery.min.js"></script>
  bottom:
  # - <script src="xxxx"></script>

```
工具的样式就先咕咕咕了，以后再补...