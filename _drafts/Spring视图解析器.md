---
layout: post
title: "Spring视图解析器"
tags: spring springmvc
category: essay
---

Spring控制器只通过逻辑视图名来了解视图，具体使用哪一个视图来渲染模型则通过视图解析器来完成。

传入一个逻辑视图名和一个Locale, 视图解析器会返回视图View. 

```java
public interface ViewResolver {
    View resolveViewName(String viewName, Locale locale) throws Exception;
}
```

View的任务时接受模型和Servlet的Request和Response对象，并把输出的结果写入到response中. 

```java
public interface View {
    String getContentType();
    void render(Map<String, ?> model, HttpServletRequest request, HttpServletResponse response) throws Exception;
}
```

