---
layout: post
title: "使用RMI装配/导出Spring服务"
tags: rmi java spring
category: essay
---

## 发布RMI服务

`RmiServiceExporter`可以把任意Spring管理的bean作为RMI服务发布。`RmiServiceExporter`将bean包装在一个适配器中，将适配器类绑定到RMI注册表中，并将其代理到服务类的实现`ServiceImpl`. 

![RmiServiceExporter](/assets/spring_2.png)

示例：将`SpitterService`发布为RMI服务

```java
@Bean
public RmiServiceExporter rmiExporter(SpitterService spitterService) {
    RmiServiceExporter rmiExporter = new RmiServiceExporter();
    rmiExporter.setService(spitterService);
    rmiExporter.setServiceName("SpitterService");
    rmiExporter.setServiceInterface(SpitterService.class);
    rmiExporter.setRegistryHost("localhost");
    rmiExporter.setRegistryPort(1099);
    return rmiExporter;
}
```

- 如果未设置RegistryHost和RegistryPort，则`RmiServiceExporter`默认会将服务绑定到`localhost:1099`上的注册表。

## 装配RMI服务

Spring中的`RmiProxyFactoryBean`可以为RMI服务创建代理。

示例：使用上文发布的`SpitterService`服务。

```java
@Bean
public RmiProxyFactoryBean spitterService() {
    RmiProxyFactoryBean rmiProxy = new RmiProxyFactoryBean();
    rmiProxy.setServiceUrl("rmi://localhost:1099/spitterService");
    rmiProxy.setServiceInterface(SpitterService.class);
    return rmiProxy;
}
```

下图展示了客户端和RMI代理的交互。

![](/assets/spring_3.png)