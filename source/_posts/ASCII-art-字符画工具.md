---
title: ASCII Art 字符画工具
tags:
  - '工具'
  - 'Python'
date: 2021-03-21 00:09:49
updated:
categories:
keywords:
description: ASCII Art
top _img:
comments:
cover: https://cdn5.telesco.pe/file/uWbiOSR-3mwuh456gVosiGNzFkeAiuzUQGBRfO8HmdgB1fGAOhZsd8apmIOxi3J2QkJGUYvXIWCeMHuz99WBX9HRN9_ESXCONzcgoDYCKBQY1OLEeHwN6588j3QvqaoedcA1EFhb6QQ2TA7xFtNbmXsYElA9P48mI208iAwzXAIT-q_6Vgp8xMLuVeP6hokREnBl3JwMQVtsijMOqSAYTa1vp-u5b5vOrePOvv8CNfZjpUVrgT_4jGGRhBiF6fEwdPqW15eyCsLQDAodOxcYVKUJU7c5Ebbiq0xR6XWhjz50f1UC0EIq3kKwNNMfuAhZkcLjTHvTh-961Xts5CR14g.jpg
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
```art

██╗  ██╗   ██╗██╗  ██╗   ██████╗ ███████╗███████╗████████╗
██║  ╚██╗ ██╔╝██║  ██║   ██╔══██╗██╔════╝██╔════╝╚══██╔══╝
██║   ╚████╔╝ ███████║   ██████╔╝█████╗  ███████╗   ██║   
██║    ╚██╔╝  ██╔══██║   ██╔══██╗██╔══╝  ╚════██║   ██║   
███████╗██║   ██║  ██║██╗██████╔╝███████╗███████║   ██║   
╚══════╝╚═╝   ╚═╝  ╚═╝╚═╝╚═════╝ ╚══════╝╚══════╝   ╚═╝   

```
ASCII Art 能够帮助我们通过电脑字符来表达图片、文本，甚至是流程图。

1️⃣ fun-comment

[GitHub](https://github.com/5A59/fun-comment) | [VSCode](https://marketplace.visualstudio.com/items?itemName=ZYLAB.fun-comment)

这是一款面向 VSCode 的内置插件，通过 fun-comment，你可以上传静态图片或者选择文字，将它们转换为 ASCII art 字符画。可作注释用途，也可以分享给他人

2️⃣ Patorjk
[官网](http://patorjk.com/software/taag/)
这是一个通过文本生成 ASCII art 字符画的在线网站，其中提供了包含字体、宽度、高度等在内的多个自定义选项。输入你想要转换的文本，点击「Test All」，在众多样式中找到你中意的那一个
同时作者还有另外一个ascii图形生成器：[http://patorjk.com/arial-ascii-art](http://patorjk.com/arial-ascii-art)

3️⃣ char-dust 

[GitHub](https://github.com/YunYouJun/char-dust/) | [Web](https://www.yunyoujun.cn/char-dust/)

 Features：

- 支持上传 GIF / PNG / JPG 图片，但只支持生成静态字符画
- 可自定义的图片大小
- 可自定义的字符串

 相信随着机器学习等领域的不断发展，字符画将越来越生动逼真，能够作为一门「Art」被越来越多的人了解和制作

4️⃣ 命令行工具figlet
```bash
figlet [ -cklnoprstvxDELNRSWX ] [ -d fontdirectory ]
      [ -f fontfile ] [ -m layoutmode ]
      [ -w outputwidth ] [ -C controlfile ]
      [ -I infocode ] [ message ]
```
安转后直接在命令行中使用即可。更多高级用法参考[figlet-man](http://www.figlet.org/figlet-man.html)

### 更多字符画生成器
[ascii-art-generator](https://www.ascii-art-generator.org/)
[IMG2TXT](https://www.degraeve.com/img2txt.php)
[Ascii.mastervb](http://ascii.mastervb.net/)
[GlassGiant ASCII Art](http://glassgiant.com/ascii/)
[ASCII码艺术（字符图像）在线生成器](https://wow.techbrood.com/fiddle/40897)

### Python 实现
#### video2char
```json
{
    "width": 135,
    "height": 240,
    "charset": "$@B%8&WM#*oahkbdpqwmzcvunxrjft/\\|()1{}[]?-_+~<>i!;:,\"^`'. ",
    "file": "c://Users/0/Desktop/python/goodluck.mp4"
}
```
```python
# coding=utf-8
import os
import json
from PIL import Image
import webbrowser


# 写入的 HTML 的配置
STYLE = '<style>pre{font-size: 10px;line-height: 7px;}</style>\r\n'
CHAR_TEMP = '<pre style="display:none">\r\n%s</pre>'
JAVASCRIPT = '''<script>
    var body;
    var first;
    var init = function() {
        body = document.getElementsByTagName("body")[0];
        first = body.firstChild;
    }
    var doframe = function() {
        body.removeChild(first);
        first = body.firstChild;
        first.style.display = 'block';
    }
    setTimeout(init, 1);
    setInterval(doframe, 100);
</script>'''


def charset256(charset):
    # 将字符集长度扩展为 256
    charset_len = len(charset)
    if charset_len > 256:
        return charset[:256]
    r = 256 // charset_len
    m = 256 % charset_len
    s = ''
    for i in charset[:m]:
        s += i * (r + 1)
    for i in charset[m:]:
        s += i * r
    return s


def image2char(image, width, height, charset):
    # 将图片转换为字符画
    image = image.convert('L').resize((width, height))  # 将图片转换为灰度模式
    pix = image.load()

    char_set = []

    for i in range(height):
        for j in range(width):
            # 读取每一个像素的值，找出对应的字符
            char = charset[pix[j, i]]
            char_set.append(char)
        char_set.append('\r\n')
    # 返回合并后的字符画
    return ''.join(char_set)


def gif2char(gif, width, height, charset):
    gif = Image.open(gif)
    gif.seek(1)

    char_set = []
    count = 0

    try:
        # 逐帧将 GIF 转换
        while True:
            char_set.append(CHAR_TEMP % image2char(gif, width, height, charset))
            if count % 10 == 0:
                print('生成 %d S 字符画' % (count / 10))
            count += 1
            gif.seek(gif.tell() + 1)
    except EOFError:
        # 合并所有帧
        return ''.join(char_set)


def video2gif(video, width, height):
    # 调用 FFmpeg ，将视频转换为指定大小的 GIF
    os.system('ffmpeg -i %s -s %d*%d -r 10 %s.gif' %
              (video, width, height, video))


if __name__ == '__main__':
    # 从 config.json 中读取 json 格式的配置
    with open('config.json') as fr:
        data = json.loads(fr.read())
    # 将配置的字符集长度扩展为 256
    charset = charset256(data['charset'])
    width = data['width']  # 要生成的字符画的宽度
    height = data['height']  # 要生成的字符画的高度
    file = data['file']  # 要转换的视频文件

    # 将视频文件转换为 GIF
    video2gif(file, width, height)

    # 逐帧将 GIF 转换为字符画
    char = gif2char(file + '.gif', width, height, charset)

    # 将生成的字符画写入文件
    with open(file + '.html', 'w') as fr:
        fr.write(JAVASCRIPT + STYLE + char)

webbrowser.open("goodluck.mp4.html")
```
效果：
<video src="https://photo.lyh.best/2021/03/21/5ab87f1a9ca78.mp4" alt="video2char.mp4" width="100%" height="100%" controls="controls"></video>


### 参考资料
以上内容部分来源于：
* Telegram频道：[@NewlearnerChannel](https://t.me/NewlearnerChannel/6734)

[【Python AsciiArt】利用命令行打印出字符图案](https://blog.csdn.net/u014636245/article/details/83661559)