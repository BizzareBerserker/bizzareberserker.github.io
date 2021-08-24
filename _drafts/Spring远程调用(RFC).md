---
layout: post
title: "Spring远程调用(RFC)"
tag: spring java rfc
category: essay
---

**远程调用** 指客户端应用和服务端之间的对话。客户端所需要的一些功能并不在其实现范围内，所以应用要向其他功能系统寻求帮助；而服务端的远程应用则通过远程服务暴露这些功能。

Spring目前支持多种RFC模型：

|RFC模型|场景|
|---|---|
|RMI|不考虑网络限制时|
|Hessian 或 Burlap|考虑网络限制，通过HTTP发布/访问基于Java的服务|
|HTTP Invoker|考虑网络限制，通过基于XML或序列化机制实现Java序列化，发布基于Spring的服务|
|JAX-RPC 和 JAX-WS|访问/发布平台独立的，基于SOAP的Web服务|

### RFC客户端模型 

![](\assets\spring_0.png)

客户端向代理发起调用，就好像代理提供了这些服务一样。代理代表客户端与远程服务进行通信，它负责处理网络通讯细节并向远程服务发起调用。

### RFC服务端模型

![](\assets\spring_1.png)

服务端使用一种RFC模型将服务bean发布为远程服务，并由远程导出器负责与客户端的远程通信。