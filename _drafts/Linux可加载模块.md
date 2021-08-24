---
layout: post
title: "Linux可加载模块"
tags: linux os
category: essay
---

Linux虽然采用单体内核结构，但其特殊的模块结构使得其开发过程具备了很多微内核模式的优点。

Linux的可加载模块具有两个重要特征：

- **动态链接**：当内核已经在内存中时，内核模块可以被动态加载到内核，也可以在任何时刻移出内存。
- **可堆叠模块**：模块可按层级结构排列；

Linux模块所用结构的一个示例：

![Linux Kernel Modules](/assets/os_3.png)

- `*name`: 模块名
- `*refcnt`: 模块计数器；启动该模块功能时计数器递增，操作中止时计数器递减。
- `num_syms`: 导出的符号数
- `*syms`: 指向该模块符号表的指针