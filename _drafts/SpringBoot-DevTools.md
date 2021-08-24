---
layout: post
title: "SpringBoot DevTools"
tag: springboot
category: essay
---

SpringBoot DevTools提供了以下功能: 

- 自动重启
- Live-Reload
- 默认的开发时属性
- ...

### 自动重启

激活DevTools之后，对Classpath里的文件执行任何修改都会触发应用程序重启. DevTools默认排除的目录包括: `/META-INF/resources`, `/resources`, `/static`, `/public`. 可以通过属性来覆盖默认排除的目录: 

```properties
spring.devtools.restart.exclude=/static/**,/templates/**
```

如果要关闭自动重启，使用

```properties
spring.devtools.restart.enabled=false
```

此外可以设置一个触发文件，只有修改这个触发文件时才会重启. 在没有设置触发文件时，每次变更都会触发自动重启. 触发文件可以确保只有你想重启时才会发生重启.  

```properties
spring.devtools.restart.trigger-file=.trigger
```

### LiveReload

禁用LiveReload: 

```properties
spring.devtools.livereload.enabled=false
```

### 默认的开发时属性

DevTools会为其支持的各种视图模板设置开发时缓存选项(禁用缓存 `false`)， 包括

- `spring.thymeleaf.cache`
- `spring.freemarker.cache`
- `spring.velocity.cache`
- `spring.mustache.cache`
- `spring.groovy.template.cache`