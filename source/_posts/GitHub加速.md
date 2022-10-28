---
title: GitHub加速
top_img: "/img/5.png"
cover: "https://cdn.jsdelivr.net/gh/Amireuxxf/PicGo/img/17.jpg"
abbrlink: 7b72b0de
date: 2022-08-31 11:24:33
tags: 教程
description: GitHub加速访问
swiper_index: 4
---
## 问题描述：

&emsp;&emsp;GitHub想必大家都不陌生吧，它是一个面向开源及私有软件项目的托管平台，因为只支持Git作为唯一的版本库格式进行托管，故名GitHub。

&emsp;&emsp;GitHub于2008年4月10日正式上线，除了Git代码仓库托管及基本的Web管理界面以外，还提供了订阅、讨论组、文本渲染、在线文件编辑器、协作图谱（报表）、代码片段分享（Gist）等功能。目前，其注册用户已经超过350万，托管版本数量也是非常之多，其中不乏知名开源项目Ruby on Rails、jQuery、Python等。

&emsp;&emsp;GitHub因其强大的代码托管功能受到广大程序员的信赖，但因其服务器在国外，国内使用过GitHub的小伙伴一定遇到过这种情况

![GitHub访问错误](/img/GitHub访问错误.png)

## 解决方案

&emsp;&emsp;这里给大家提供几种本人亲自测试过的解决方案，以供大家选择。

### 方案一：Github镜像源

&emsp;&emsp;1.https://hub.fastgit.org/

&emsp;&emsp;2.https://github.com.cnpmjs.org/

&emsp;&emsp;3.https://github.wuyanzheshui.workers.dev/

### 方案二：dev-sidecar

&emsp;&emsp;开发者边车，命名取自service-mesh的service-sidecar，意为为开发者打辅助的边车工具 通过本地代理的方式将https请求代理到一些国内的加速通道上

&emsp;&emsp;下载地址：https://gitee.com/interesting-goods/dev-sidecar?_from=gitee_search

### 方案三：修改Host地址

&emsp;&emsp;可以查询https://github.com.ipaddress.com/#ipinfo的IP地址

![20210509084840985](/img/20210509084840985.png)

&emsp;&emsp;以及https://fastly.net.ipaddress.com/github.global.ssl.fastly.net#ipinfo，

![20210509084809134](/img/20210509084809134.png)

&emsp;&emsp;在Host文件的最后加上如下内容（Host文件一般在“C(系统盘):\Windows\System32\drivers\etc”文件夹下）：

```
#github
140.82.112.4 github.com
199.232.69.194 github.global.ssl.fastly.net
```

&emsp;&emsp;更改完成后，打开命令提示符（cmd），刷新DNS

```
ipconfig /flushdns
```

### 方案四：FastGithub(推荐)

github加速神器，解决github打不开、用户头像无法加载、releases无法上传下载、git-clone、git-pull、git-push失败等问题。

#### 0 写在前面

- **fastgithub不具备“翻墙”功能,也没有相关的计划**
- **fastgithub不支持Windows7等已被发行方停止支持的操作系统，并且也不会主动提供支持**
- **fastgithub不能为您的游戏加速**
- **fastgithub没有主动在github和[fastgithub@qq.com](mailto:fastgithub@qq.com)之外的任何渠道发布**

#### 1 程序下载

- [github-release下载](https://github.com/dotnetcore/fastgithub/releases)
- 发送任意邮件到[fastgithub@qq.com](mailto:fastgithub@qq.com)

#### 2 部署方式

##### 2.1 windows-x64桌面

- 双击运行FastGithub.UI.exe

##### 2.2 windows-x64服务

- `fastgithub.exe start` // 以windows服务安装并启动
- `fastgithub.exe stop` // 以windows服务卸载并删除

##### 2.3 linux-x64终端

- `sudo ./fastgithub`
- 设置系统自动代理为`http://127.0.0.1:38457`，或手动代理http/https为`127.0.0.1:38457`

##### 2.4 linux-x64服务

- `sudo ./fastgithub start` // 以systemd服务安装并启动
- `sudo ./fastgithub stop` // 以systemd服务卸载并删除
- 设置系统自动代理为`http://127.0.0.1:38457`，或手动代理http/https为`127.0.0.1:38457`

##### 2.5 macOS-x64

- 双击运行fastgithub
- 安装cacert/fastgithub.cer并设置信任
- 设置系统自动代理为`http://127.0.0.1:38457`，或手动代理http/https为`127.0.0.1:38457`
- [具体配置详情](https://github.com/dotnetcore/FastGithub/blob/master/MacOSXConfig.md)

##### 2.6 docker-compose一键部署

- 准备好docker 18.09, docker-compose.
- 在源码目录下，有一个docker-compose.yaml 文件，专用于在实际项目中，临时使用github.com源码，而做的demo配置。
- 根据自己的需要更新docker-compose.yaml中的sample和build镜像即可完成拉github.com源码加速，并基于源码做后续的操作。

#### 3 软件功能

- 提供域名的纯净IP解析；
- 提供IP测速并选择最快的IP；
- 提供域名的tls连接自定义配置；
- google的CDN资源替换，解决大量国外网站无法加载js和css的问题；

#### 4 证书验证

##### 4.1 git

git操作提示`SSL certificate problem`
需要关闭git的证书验证：`git config --global http.sslverify false`

##### 4.2 firefox

firefox提示`连接有潜在的安全问题`
设置->隐私与安全->证书->查看证书->证书颁发机构，导入cacert/fastgithub.cer，勾选“信任由此证书颁发机构来标识网站”

#### 5 安全性说明

FastGithub为每台不同的主机生成自颁发CA证书，保存在cacert文件夹下。客户端设备需要安装和无条件信任自颁发的CA证书，请不要将证书私钥泄露给他人，以免造成损失。

#### 6 合法性说明

《国际联网暂行规定》第六条规定：“计算机信息网络直接进行国际联网，必须使用邮电部国家公用电信网提供的国际出入口信道。任何单位和个人不得自行建立或者使用其他信道进行国际联网。” FastGithub本地代理使用的都是“公用电信网提供的国际出入口信道”，从国外Github服务器到国内用户电脑上FastGithub程序的流量，使用的是正常流量通道，其间未对流量进行任何额外加密（仅有网页原有的TLS加密，区别于VPN的流量加密），而FastGithub获取到网页数据之后发生的整个代理过程完全在国内，不再适用国际互联网相关之规定。