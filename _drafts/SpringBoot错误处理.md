---
layout: post
title: "SpringBoot错误处理"
tag: springboot spring
category: essay
---

SpringBoot提供了默认的错误处理页面

- 如果访问者是浏览器，则显示Whitelabel错误页面

![Whitelabel Error Page](/assets/springboot_1.png)

- 如果访问者是机器客户端，则返回一个json格式的错误信息

```json
{
    "timestamp": "2021-07-19T06:58:26.834+00:00",
    "status": 405,
    "error": "Method Not Allowed",
    "message": "",
    "path": "/"
}
```

### 自定义错误视图

要想自定义错误页面，最简单的方式用自定义的错误视图覆盖默认的错误视图. SpringBoot自动配置的默认错误处理器会查找名为`error`的视图，如果找不到就会返回默认的Whitelabel错误视图. 因此，在模板目录中添加一个自定义的错误视图`error`就可以替换默认的错误视图. 

如果想让不同类型的错误映射到不同的视图，那么在模板目录下新建一个`error`文件夹，将每个状态码对应的错误视图放在`templates/error`下即可: (以Thymeleaf为例)如`templates/error/404.html`代表404 Not Found错误的视图, `templates/error/5xx.html` 代表5xx系列的错误的视图. 

默认情况下，SpringBoot为错误视图提供以下属性

| 属性      | 描述           |
| --------- | -------------- |
| timestamp | 错误发生的时间 |
|status|HTTP状态码|
|error|错误原因|
|exception|异常的类名|
|message|异常消息|
|errors|BindingResult异常里的错误|
|trace|异常跟踪信息|
|path|错误发生时请求的URL路径|

