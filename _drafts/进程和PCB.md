---
layout: post
title: "进程和PCB"
tag: os
category: essay
---

### 进程

**进程** (process)：

- 一个正在执行的程序
- 一个正在计算机上执行的程序示例
- 能分配给处理器并由处理器执行的实体
- 由一组指令、一个当前状态和一组相关的系统资源表征的活动单元

进程的两个基本元素是**程序代码** (program code)和相关的**数据集** (set of data)。

进程由程序代码、相关数据和**进程控制块** (PCB)组成。

### 进程控制块

进程控制块是一个由操作系统管理和创建的一个数据结构，它包含了一组可以表征某个进程当前状态的相关元素，如：

- **标识符** (identifier)：与进程相关的唯一标识符
- **状态** (state)：表示进程执行状态，如运行态、阻塞态、挂起态……
- **优先级** (priority)：相对于其他进程的优先顺序
- **程序计数器** (program counter)：指向该进程下一条指令的地址
- **内存指针** (memory pointer)：指向该进程的程序代码及相关数据节的指针
- **上下文数据** (context data)：进程执行时处理器寄存器的数据
- **I/O状态信息** (I/O status information)：包括发起的I/O请求、分配给进程的I/O设备和打开的文件等
- **记账信息** (accounting information)：包括处理器时间总和、时钟数总和、时间限制等

![Simplified PCB](/assets/os_5.png)