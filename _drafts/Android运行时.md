---
layout: post
title: "Android运行时"
tags: os android
category: essay
---

## Dalvik虚拟机

**Dalvik虚拟机**执行`.dex`格式的文件；DVM运行在Linux内核之上，依靠Linux内核的底层功能。每个Android进程都持有一个DVM示例。

**dex文件格式**：标准Java编译器将`.java`文件编译为字节码文件(`.class`)， 随后使用内置工具`dx`将Java类编译为`.dex`文件；DVM在运行应用程序时完成从`.dex`到原生机器码的**即时(Just-In-Time)编译**；DVM会识别经常被编译的代码并将其编译后的代码缓存下来以加快速度。

## Android Runtime

**Android运行时** (ART)会在安装应用时通过**预先(Ahead-Of-Time)编译**直接将`.dex`字节码编译为原生机器码，ART使用`dex2oat`工具执行这项编译任务。

**apk生命周期**：源代码被编译为`.dex`格式后会与其他配套支持代码编译为`.apk`文件并发布；到了用户端，`.apk`文件接收后会被解压

- DVM：`dexopt`函数会应用到`.dex`文件上产生一个优化过的`.odex`文件以让字节码能够更快地在DVM上运行
- ART：`dex2oat`函数执行类似的操作产生一个优化过的`.odex`文件，然后将文件编译为目标设备的原生代码 (一个ELF文件).

### ART优缺点

**ART优点**：

- 减少应用程序启动时间
- 减少JIT对处理器和内存的损耗，提升了电池续航和小内存下的灵活性
- 整合了GC优化和调试改进

**ART缺点**：

- 应用程序在安装时需要更多时间执行AOT编译
- 需要额外存储空间存储原生代码