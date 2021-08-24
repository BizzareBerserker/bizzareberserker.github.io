---
layout: post
title: "Multipart"
tags: spring springmvc
---

### 配置MultipartResolver

SpringBoot的自动配置一个Multipart解析器. 可以在配置文件中修改Multipart解析器的相关属性: 

|属性|默认值|备注|
|---|---|---|
|`spring.servlet.multipart.enabled`|`true`|是否启用multipart|
|`spring.servlet.multipart.file-size-threshold`|0MB|当上传文件大小达到此容量时，将文件写入到磁盘中|
|`spring.servlet.multipart.location`|(默认写到一个临时文件中)|文件存储的位置|
|`spring.servlet.multipart.max-file-size`|1MB|单个文件的最大大小|
|`spring.servlet.multipart.max-request-size`|10MB|单个请求的最大大小|

### multipart

为了允许用户提交文件，我们需要修改前端页面以支持Multipart： 

```html
<form method="post" th:action="@{/save}" enctype="multipart/form-data">
    
    ...
    <input type="file" name="avatar" accept="image/jpeg,image/png,image/gif"/>
    ...
    
</form>
```

|标签|属性|说明|
|---|---|---|
|`form`|`enctype`|对表单的编码方式, 如果表单包含文件则必须使用`multipart/form-data`|
|`input`|`type`|表单控件，"file"表示上传文件|
|`input`|`accept`|接收上传文件的MIME类型|
|`input`|`multiple`|接收多个文件|

在后端，使用`@RequestPart`注解获取Multipart文件. Spring 提供了`MultipartFile`接口用来支持对Multipart文件的更多操作: 

```java
@PostMapping("/register")
public String processRegistration(
	@RequestPart("avatar") MultipartFile avatar
	@RequestParam("name") String username) {
    // processing code...
    
    return "registration";
}
```
Multipart支持的方法: 

|方法签名|
|---|
|`String getName()`|
|`String getOriginalFilename()`|
|`String getContentType()`|
|`boolean isEmpty()`|
|`long getSize()`|
|`byte[] getBytes()`|
|`InputStream getInputStream()`|
|`void transferTo(File dest)`|

