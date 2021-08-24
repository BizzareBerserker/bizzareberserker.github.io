---
layout: post
title: "Android唤醒锁"
tags: os android
category: essay
---

唤醒锁可以阻止Android系统进入休眠模式；一个应用程序可以占有以下唤醒锁中的一个：

- **full_wake_lock**: 处理器工作 | 屏幕亮 | 键盘亮
- **partial_wake_lock**: 处理器工作 | 屏幕关 | 键盘关
- **screen_dim_wake_lock**: 处理器工作 | 屏幕暗 | 键盘关
- **screen_bright_wake_lock**: 处理器工作 | 屏幕亮 | 键盘关

通过访问`/sys/power/wavelock`文件，用户可以再用户空间中访问内核中的电源管理的相应对象。