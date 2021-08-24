---
layout: post
title: "SpringBoot Actuator"
tags: spring springboot
category: essay
---

### 启用SpringBoot Actuator

在SpringBoot应用中启用Actuator只需要引入Actuator依赖，Actuator就会默认开启。

- 在Maven中引入`spring-boot-starter-actuator`依赖

```xml
<dependency>
    <groupId>org.springframeword.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

- 在Gradle中引入`spring-boot-starter-actuator`依赖

```gradle
dependencies {
	implementation 'org.springframework.boot:spring-boot-starter-actuator'
}
```

### 访问Actuator端点

Acutator端点可以通过两种方式访问：HTTP和JMX。

- 通过**HTTP**访问：使用对应的HTTP方法(通常是`GET`)访问URL: `<host>:<port>/actuator/<endpoint>[/<path>]`；其中`<endpoint>`为要访问的端点名称，某些端点可能允许你添加`<path>`来访问关于某个端点的更详细的信息
- 通过**JMX**访问：SpringBoot Actuator提供了所有端点的MBean，你可以在`org.springframework.boot`的`Endpoint`下找到所有端点的MBean并对相关指标进行监控

![](/assets/springboot_0.png)

### Endpoint

Actuator端点允许你监控应用程序的相关指标并且与应用程序进行监控。SpringBoot提供了一些内置Actuator端点并且允许你添加自己的Actuator端点。

| ID            | Description                        |
| ------------- | ---------------------------------- |
| `beans`       | 展示当前应用中的所有bean           |
| `configprops` | 展示应用中所有配置的属性           |
| `env`         | 展示Spring的环境配置属性           |
| `health`      | 展示应用程序的健康状况             |
| `info`        | 提供关于应用程序的信息             |
| `loggers`     | 展示并更改应用的日志配置           |
| `metrics`     | 展示该程序的所有监控指标           |
| `shutdown`    | 关闭应用程序。默认不启用(disabled) |
| ...           | ...                                |

当一个Endpoint既是启用的(enabled)又是暴露的(exposed)时，称该端点为**可访问**(available)的。你可以通过HTTP或JMX方式来访问该端点。

默认，所有端点都是**启用**(enabled)的。你可以通过属性来手动启用或关闭端点：

```properties
management.endpoints.enabled-by-default=true
management.endpoints.<endpoint-name>.enabled=true
```

默认，所有端点都**暴露**(exposed)给JMX，只有`health`和`info`端点可以通过HTTP访问。你可以通过属性来调整暴露哪些端点：

```properties
management.endpoints.jmx.exposure.include=*
management.endpoints.jmx.exposure.exclude=
management.endpoints.web.exposure.include=health,info
management.endpoints.web.exposure.exclude=
```

此外，你还可以重命名已经存在的端点，通过调整以下属性即可完成

```properties
management.endpoint.<endpoint>.id=<new-name>
```

