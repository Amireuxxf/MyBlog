---
title: npm安装依赖报错
top_img: "/img/5.png"
cover: "https://cdn.jsdelivr.net/gh/Amireuxxf/PicGo/img/34.png"
abbrlink: 4dbbe0bc
date: 2022-08-30 21:01:47
tags: 技术教程
description: 技术教程
swiper_index: 5
---
#### 在仓库上拉取项目，安装依赖时报错：

&emsp; npm报错：npm ERR! code ECONNREFUSED npm ERR! errno ECONNREFUSED，npm ERR! npm ERR! If you are behind a proxy, please make sure that the

#### 问题出现原因：

&emsp;Github相当于程序员的百度，但是速度有时又太慢，就使用了某VPN代理访问。结果，VPN开了一个端口，npm的一些依赖包访问速度巨慢，就出现了报错

#### 解决方法：

1. ##### 查看代理

   ```
   npm config get proxy
   npm config get https-proxy
   ```

   如果发现有代理，就清空它

    ```
	npm config delete proxy
	npm config delete https-proxy
    ```



2. ##### 全局配置淘宝镜像

   ```
   npm install -g cnpm --registry=https://registry.npm.taobao.org 
   ```

   再安装依赖就OK了

