---
layout: post
title: "JMX架构和MBean"
tags: jmx java
category: essay
---

**JMX **(Java Management eXtension)是一个为应用程序植入管理功能的框架，它允许用户在应用运行过程中监控Bean和应用的各项属性以及在运行时更改应用配置。

## JMX架构

JMX架构可以分为三层：**监测层**(Instrumentation / Probe Level)、**代理层**(Agent Level)和**远程管理**(Remote Management Level)。

**监测层**：被管理的资源。通常情况下包含许多MBean，每个MBean用来监测一类性能指标。

**代理层**：负责对资源的注册和管理。核心组件为MBean Server(所有的MBean在这个容器中注册)， 这个容器接受外部请求，并返回其中注册的MBean的对应的监控信息 (JMX代理内嵌在Java程序中)。它的功能类似于WEB容器的功能。

**远程管理**：提供访问资源的入口。外部的管理程序可以通过适配器(adapter)或连接器(connector)来连接到MBean Server 并对资源进行监测。

## MBeans

| 类型           | 描述 |
| -------------- | ---- |
| standard MBean | 最简单的MBean。 |
|dynamic MBean|所有的属性和方法都在运行时定义|
|open MBean|*不完善*|
|model MBean|?|