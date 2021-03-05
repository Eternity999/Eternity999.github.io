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
## 前言
### github1s
![github1s](https://img.hellogithub.com/hellogithub/59/img/github1s.gif)
最近有一个比较火的项目上线半个月就收获了 15.8k 个 star，继续在浏览器地址栏 GitHub 域名中 “github” 后面添加 “1s”，就能通过 VS Code 界面直接预览 GitHub 上的各类项目代码。**注意仅是只读的，不能在线编辑**。

github1s（项目地址：[https://github.com/conwnet/github1s](https://github.com/conwnet/github1s)），是一款纯静态的 Web 应用程序，目前基于 VS Code 1.52.1，核心原理使用 GitHub REST API 实现一个带 FileSystemProvider 的VS Code Extension。网站直接使用 GitHub Page 托管。由于对未授权的请求，API 的请求频率是有限制的，每个 IP 每小时访问限制是60次，如果遇到了 Rate Limiting 只要点击 Generate New OAuth Token 跳到自己的 GitHub Setting 页面，生成一个 Token ，在 github1s 中填入 OAuth Token 就可以提升到 5000 次啦。
还有一个配套同名的 Chrome 插件，只要上 chrome web store 上搜索 [github1s](https://chrome.google.com/webstore/search/github1s) 就有啦.

## 搭建 Web 版 VSCode 作为云端IDE
### VSCode
Visual Studio Code 是微软的一款代码编辑器，使用 TypeScript + Electron 开发。
VS Code 1.40 之后，开发者已经可以直接从 VS Code 的源代码编译出 Web 版 VS Code。更多内容，查看 VS Code 1.40 的发布说明： [https://code.visualstudio.com/updates/v1_40](https://code.visualstudio.com/updates/v1_40)
#### CentOS7.9部署
安装依赖：
```bash
yum install -y make  # make
pkg-config --version  # pkg-config
yum groupinstall -y "Development Tools"  # GCC or another compile toolchain：
yum install -y libX11-devel.x86_64 libxkbfile-devel.x86_64  # native-keymap
yum install -y libsecret-devel  # keytar
```
安装Node.js和npm：
```bash
curl -sL https://rpm.nodesource.com/setup_10.x | bash -
yum install -y nodejs
node --version
npm --version
```
安装yarn：
```bash
curl --silent --location https://dl.yarnpkg.com/rpm/yarn.repo | sudo tee /etc/yum.repos.d/yarn.repo
yum install -y yarn
yarn --version
```
拉取vscode源码：
通过wget命令下载zip包，然后解压。
```bash
wget https://github.com/microsoft/vscode/archive/1.45.1.zip
unzip 1.45.1.zip
```
或者，通过git clone命令下载。
```bash
git clone --depth 1 --branch 1.45.1 https://github.com/microsoft/vscode.git
```
- 参数“--depth 1”  表示最近一次 commit 的代码
- 参数“--branch 1.45.1”  表示tag 1.45.1

在代码根目录下，执行 yarn 命令安装依赖，用时较久，耐心等待
```bash
cd vscode-1.45.1/
yarn
```
运行Web VS Code
执行 yarn watch 命令 (watch是在package.json文件中scripts属性指定的命令)
```bash
yarn watch
```
在执行 yarn watch 命令之后，执行 yarn web 命令构建 Web 版本的VS code
```bash
yarn web
```
执行 yarn web 命令时， 可以指定Host和Port
例如：
```bash
yarn web --host 127.0.0.1 --port 8080
```
注意：非本机访问，需要开启防火墙规则 或者 关闭防火墙
```bash
# 开启防火墙端口
firewall-cmd --zone=public --permanent --add-port=8080/tcp
firewall-cmd --reload

# 关闭并禁止开机启动防火墙
systemctl stop firewalld
systemctl disable firewalld
```
### code-server
code-server的官网: [https://coder.com/](https://coder.com/)
项目仓库：[https://github.com/cdr/code-server](https://github.com/cdr/code-server)
![code server](https://github.com/cdr/code-server/raw/main/docs/assets/screenshot.png)

code-server 是 [Coder公司](https://coder.com/) 基于VSCode的开源项目，可以实现通过浏览器访问在远程服务器上的VS Code。
简单地说，是基于 VSCode 进行了一些修改，专门为浏览器设计优化，以便作为可托管的 Web 服务来运行。
换而言之，配置服务器端（code-server）后，就可以在任何浏览器上访问和使用 VS Code。
此外，Coder还提供了sshcode工具（Run VS Code on any server over SSH.） [https://github.com/cdr/sshcode](https://github.com/cdr/sshcode)
相关文档：
* 总体概述：https://github.com/cdr/code-server/blob/master/README.md
* 安装：https://github.com/cdr/code-server/blob/master/doc/install.md
* 设置指引：https://github.com/cdr/code-server/blob/master/doc/guide.md
* 常见问答：https://github.com/cdr/code-server/blob/master/doc/FAQ.md

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
docker run -dit -p 8080:8080 \
  --restart=always \
  --name codeserver \
  -h vscode \
  -u root \
  -v /tmp/coder-data:/home \
  -v /tmp/coder-config:/root \
  -v /etc/localtime:/etc/localtime:ro \
  -e PASSWORD=mycodeserver \
  codercom/code-server:3.4.1 
```
注意：-e PASSWORD=mycodeserver 设置密码为mycodeserver。

最新版本能连接上了扩展商店，轻松安装语言包，Live Server 等拓展，还有其他的拓展可通过 .VSIX 离线包获取。VSCode扩展商店网页版：[https://marketplace.visualstudio.com/vscode](https://marketplace.visualstudio.com/vscode)搜索扩展，进入到详情页之后，选择右下角的Download Extension下载离线包。之后在扩展界面选择Install from VSIX，选择路径安装。

### WebIDE
通过浏览器访问IDE，实现云端开发环境获取、代码编写、编译调试、运行预览、访问代码仓库、命令行执行等能力，同时支持丰富的插件扩展。
可以让开发者拥有一个统一、标准化的开发环境，节省了安装配置和维护组件的成本，可以更加专注于开发本身。
WebIDE已经有了一段时间的发展，不同的组织和厂商，先后推出了多种工具和产品。
* AWS Cloud9：https://aws.amazon.com/cloud9/
* Eclipse Che：http://www.eclipse.org/che/
* 腾讯扣钉：https://cloudstudio.net/
* repl.it：https://repl.it/
GitLab、Gitee等开源代码托管服务也先后发布了 WebIDE 功能。
例如，Github 推出了基于 VS Code 的的 Codespaces https://github.com/features/codespaces
Codespaces 集成浏览器版 VS Code 编辑器，支持代码补全、导航、扩展、终端访问等功能，具备完整的 Visual Studio Code 体验。

### 参考资料
[VSC - VS Code 运行Web IDE](https://www.cnblogs.com/anliven/p/13363811.html)