---
title: win11运行安卓APP教程
date: 2022-02-21 11:16:11
categories: 教程分享
tags: 
- 教程
---
早在Windows11发布前,微软就承诺加入Android子系统,今天这项更新终于到来。

用户无需加入Insider计划,即可享用到这项新功能。

<!--more-->

但是Windows 11限制用户只可以从亚马逊应用商店安装App,我们中国区用户怎么办呢?别急。

# 教程
虽然非美区用户还无法在微软商店下载Amazon Appstore,不过已经有大神可以绕过这一限制,实现安装任意apk。

首先进入网站[https://store.rg-adguard.net](http://),分别选择ProductID、Slow,在搜索框中输入9P3395VX91NR,点击确定。

选择下载最后一个msibundle文件。
![](https://pic.imgdb.cn/item/621305902ab3f51d91ea5c3b.png)

比如你希望将Android子系统安装在E:\Android\文件夹下,那么就把msibundle文件移到该文件夹中,并在PowerShell中以管理员身份运行以下命令:

``` shell
cd C:\WSA\
```

再输入以下命令完成Android子系统的安装:

``` shell
Add-AppxPackage MicrosoftCorporationII.WindowsSubsystemForAndroid_1.8.32837.0_neutral___8wekyb3d8bbwe.Msixbundle
```

这样Android子系统和Amazon Appstore就安装成功了。

如果我们不想限制在Amazon Appstore里,想安装任意apk怎么办呢?

点击“开始”菜单,选择所有应用,找到Windows Subsystem for Android?? Settings,启用开发者模式,并找到子系统的IP地址。

接下来如何安装自己准备的apk包呢?
目前还没有界面的安装方法,所以就要利用ADB工具。

1. 解压ADB工具到当前文件夹,并进入解压出的文件夹 platform-tools。

2. 在路径框中输入CMD后回车。

3. 输入 `.\adb connect 127.0.0.1:58526` 也就是之前在开发人员模式中看到带端口的IP地址。

显示 connected to 127.0.0.1:58526 即为连接成功。

4. 在命令指示符窗口中输入

```shell
adb install
```

空格后将准备好的APK文件直接拖入命令指示符窗口后,敲击回车。 

回车后提示 Performing Streamed Install 则为正在安装。

当提示success 则为安装成功。