---
title: Linux 服务器搭建 Web 版 VSCode
date: 2021-03-03 20:47:04
updated:
tags: IDE
categories:
keywords:
description:
top _img: https://photo.lyh.best/2021/03/03/55e9728ef580a.png
comments:
cover: https://photo.lyh.best/2021/03/03/36661ed1a7d26.png
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
![CoderIDE](https://photo.lyh.best/2021/03/03/55e9728ef580a.png)

### 前言
最近有一个比较火的项目上线半个月就收获了 15.8k 个 star，继续在浏览器地址栏 GitHub 域名中 “github” 后面添加 “1s”，就能通过 VS Code 界面直接预览 GitHub 上的各类项目代码。**注意仅是只读的，不能在线编辑**。

github1s（项目地址：[https://github.com/conwnet/github1s](https://github.com/conwnet/github1s)），是一款纯静态的 Web 应用程序，目前基于 VS Code 1.52.1，核心使用 GitHub REST API 实现 VS Code 扩展。

### VSCode
Visual Studio Code 是微软的一款代码编辑器，使用 TypeScript + Electron 开发，最新版本的 VSCode 已经可以在普通浏览器中运行。

### code-server
code-server的官网: [https://coder.com/](https://coder.com/)
![code server](https://github.com/cdr/code-server/raw/main/docs/assets/screenshot.png)
建议配置：
* 1 GB of RAM
* 2 cores

安装教程：[https://github.com/cdr/code-server/blob/main/docs/install.md](https://github.com/cdr/code-server/blob/main/docs/install.md)
安装脚本：
```bash
curl -fsSL https://code-server.dev/install.sh | sh
```
运行：
```bash
./code-server
```
以守护进程运行:
```bash
sudo systemctl enable --now code-server@$USER
```
访问[http://127.0.0.1:8080](http://127.0.0.1:8080)即可。
登陆密码记录在```~/.config/code-server/config.yaml```
docker一键搭建:
```bash
docker run -it -p 8443:8443 -v "${PWD}:/home/${USER}/code" codercom/code-server --allow-http
```
最新版本能连接上了扩展商店，轻松安装语言包，Live Server 等拓展，还有其他的拓展可通过 .VSIX 离线包获取。VSCode扩展商店网页版：[https://marketplace.visualstudio.com/vscode](https://marketplace.visualstudio.com/vscode)搜索扩展，进入到详情页之后，选择右下角的Download Extension下载离线包。之后在扩展界面选择Install from VSIX，选择路径安装。
