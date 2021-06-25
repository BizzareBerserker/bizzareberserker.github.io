---
layout: post
title: "在Spring中使用缓存"
tags: Spring Java
category: essay
---

Spring对缓存的支持主要有两种方式：

- 注解驱动的缓存
- XML声明的缓存

### 启用Cache支持

在bean上添加缓存之前，必须先启用Spring缓存的支持。通过Java配置的方式如下：在一个配置类上添加注解`@EnableCaching`, 同时声明一个缓存管理器，它能够与多个流行的缓存进行集成。

```java
@Configuration
@EnableCaching
public class CachingConfiguation {
    
    @Bean
    public CacheManager cacheManager() {
        return new ConcurrentMapCacheManager();
    }
}
```

通过XML声明启用注解驱动缓存的方法如下：

```xml
<?xml version="1.0" encoding="UTF-8" ?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:cache="http://www.springframework.org/schema/cache"
       xmlns:schemaLocation="...">
    <!-- nm$l -->
    <cache:annotation-driven />
    
    
    <bean id="cacheManager" class="org.springframework.cache.concurrent.ConcurrentMapCacheManager"
</beans>
```

### 为方法添加注解以支持Cache

所有Cache注解都能应用在类或方法上，当其应用在方法上时，缓存行为只会应用到这个方法上；当其应用在类上时，缓存行为会应用到这个类的所有方法上。

|注解|描述|
|---|---|
|`@Cacheable`|在Cache中查找方法返回值，如果找不到就调用并将方法返回值放到Cache中，否则返回Cache值|
|`@CachePut`|Spring将方法返回值放到Cache中(不会在调用前检查Cache)|
|`@CacheEvict`|Spring在缓存中清楚一个或多个Entry|
|`@Caching`|一个分组的注解|
|`@CacheConfig`|类级别注解，为类中所有Cache方法声明缓存名称|

`@Cacheable`和`@CachePut`的一些公有的属性

|属性|描述|
|---|---|
|`value`|缓存名称|
|`condition`|SpEL表达式，如果值为False则不会在方法调用上应用缓存|
|`key`|SpEL表达式，用来计算自定义的缓存key|
|`unless`|SpEL表达式，如果值为True则不会在方法上将返回值写入缓存Cache|

`@CacheEvict`的属性

|属性|描述|
|---|---|
|`value`|要使用的Cache名称|
|`key`|SpEL表达式，涌来了计算自定义的缓存key|
|`condition`|...|
|`allEntries`|布尔值，特定缓存的所有条目都会被驱逐|
|`beforeInvocation`|如果为True，在方法调用前移除，否则(False, 默认)在方法调用后移除|

Spring提供了多个用来定义缓存规则的SpEL扩展

| 表达式 | 描述 |
| ------ | ---- |
|`#root.args`|传递给缓存方法的参数，形式为数组|
|`#root.caches`|该方法对应的Cache，形式为数组|
|`#root.target`|目标对象|
|`#root.targetClass`|目标对象的类|
|`#root.method`|缓存方法|
|`#root.methodNamee`|缓存方法的名字|
|`#result`|缓存方法调用的返回值|
|`#Argument`|任意的方法参数名（`#argName`或`#a0`/`#p0`）|

