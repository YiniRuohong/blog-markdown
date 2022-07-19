---
title: 使用DailyCheckin实现B站等平台自动签到
date: 2022-02-26 10:44:38
categories: 教程分享
tags:
- 教程
---
随着越来越多的网络平台拥有了在线签到功能,自动签到也成为了许多人的需求。今天的教程就是利用GitHub上面的Dailycheckin项目来实现免费自动签到功能

<!--more-->

# 准备工作

腾讯云账号

# 教程
## 创建云函数

新建一个云函数
![](https://pic.imgdb.cn/item/6219962c2ab3f51d915f1b5e.png)

按图提示进行配置
![](https://pic.imgdb.cn/item/621996bd2ab3f51d9160549f.png)

继续向下,删掉默认文件内容,填入如下内容

``` py
# -*- coding: utf-8 -*-
from dailycheckin.main import checkin


def main_handler(event, context):
    checkin()
```

![](https://pic.imgdb.cn/item/621997382ab3f51d91615178.png)

展开高级配置,将执行超时时间设置为900秒

![](https://pic.imgdb.cn/item/621997852ab3f51d9161eda7.png)

展开「触发器配置」,切换到自定义创建,定时任务的名称填「checkin」,然后触发周期改为「自定义触发周期」,在Cron表达式处填入:45 8 * * *
![](https://pic.imgdb.cn/item/621998422ab3f51d9163999d.png)

点击完成,进入下一步