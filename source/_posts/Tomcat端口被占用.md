---
title: Tomcat端口被占用
abbrlink: 7d637b24
date: 2022-09-14 15:42:37
tags: Tomcat
description: Tomcat启动报错
swiper_index: 2
---
## Tomcat启动
&emsp;&emsp;在启动Tomcat是出现了端口1099被占用的问题，重启以及重新配置Tomcat都无法解决问题。

&emsp;&emsp;报错信息：localhost：1099 is already used

## 解决方案
### 方案一：查找占用1099端口的进程并结束
&emsp;&emsp;运行cmd，分别输入以下代码，重启Tomcat。
```
   # 查找所有端口为1099的进程
   netstat -ano | findstr 1099
   # 结束端口为1099的进程
   taskkill -f -pid 1099端口进程所对应的pid
   ```
### 方案二：关闭Java.exe进程
&emsp;&emsp;1、打开任务管理器（ctrl+shift+esc）,选择进程

&emsp;&emsp;2、找到所有的Java.exe进程，然后关闭

&emsp;&emsp;3、找到JDK安装目录，进入bin目录下，双击java.exe文件运行

&emsp;&emsp;4、重新启动idea

### 方案三：关闭Hyper-v

&emsp;&emsp;可能我们电脑开启了Hyper-V服务，系统默认会分配给一些保留端口供Hyper-V使用，可能与Tomcat冲突。

&emsp;&emsp;首先我们可以查看一下我们系统默认的端口占用范围：

```
    # 查看系统默认的端口占用范围
   netsh int ipv4 show dynamicport tcp
   ```
```
   协议 tcp 动态端口范围
   ---------------------------------
   启动端口        : 1024
   端口数          : 13977
   ```
&emsp;&emsp;可以看到Windows系统默认的tcp动态端口范围为：1024~13977

&emsp;&emsp;当开启Hyper-V后，系统默认会分配给一些保留端口供Hyper-V使用

&emsp;&emsp;IDEA运行Tomcat需要JMX的1099端口刚好在端口排除范围中，这样就导致了IDEA需要使用1099端口是会被占用

&emsp;&emsp;**解决方案**：控制面板->程序->程序和功能->Windows功能，去掉Hyper-V前边的勾选框

![](/img/微信图片_20220914183905.jpg)

&emsp;&emsp;此电脑右键->管理->服务和应用程序->服务

&emsp;&emsp;将Hyper相关服务全部停止并设置为手动类型。然后重启电脑即可

![](/img/微信图片_20220914190309.jpg)

### 方案四：cmd命令修改端口范围

&emsp;&emsp;前提是Windows系统默认的tcp动态端口范围为：1024~13977，关闭Hyper-V后也不能用
```
    # 使用命令修改配置，重启Tomcat
   netsh int ipv4 set dynamicportrange tcp start=49152 num=16384
   ```

### 方案五：重建Tomcat
&emsp;&emsp;将Tomcat删除，重新建立运行。

### 方案六：重置winsock目录

&emsp;&emsp;Netsh winsock reset是一个命令提示程序，用于将winsock目录重置为默认设置或清除状态。如有时候上不了网或者网络出现问题经常用到它，简单地理解就是：重置程序通过操作系统链接网络的入口点。

&emsp;&emsp;以管理员身份运行cmd，然后重启计算机 
```
    netsh winsock reset
   ```

### 方案七：查看host
&emsp;&emsp;在SwtichHosts中查看是否少了 127.0.0.1 localhost这行，如果少了就再单独配置一行，启动项目。