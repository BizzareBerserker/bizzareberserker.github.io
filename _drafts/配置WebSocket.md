---
layout: post
title: "配置WebSocket"
tags: websocket spring
category: essay
---

首先引入WebSocket依赖: 

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-websocket</artifactId>
</dependency>
```

要想配置WebSocket，在一个配置类上使用`@EnableWebSocket`注解，并实现`WebSocketConfigurer`接口，如下面程序清单所示: 

```java
@EnableWebSocket
public class WebSocketConfig implements WebSocketConfigurer {
    
    public void registerWebSocketHandlers(WebSocketHandlerRegistry registry) {
        registry.addHandler(helloHandler(), "/hello");
    }
    
    public HelloHandler helloHandler() {
        return new HelloHandler();
    }
}
```

