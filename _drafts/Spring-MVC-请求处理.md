---
layout: post
title: "Spring MVC 请求处理"
tags: springmvc spring
category: essay
---

### 控制器

在Spring MVC中用`@Controller`注解标注一个控制器，这个控制器随后可以被组件扫描发现

如果该控制器使用REST API，那么使用`@RestController`注解来将其标注为一个RestController. 

### 接收参数

以下注解可以从请求中取出对应参数并进行处理：

- `@PathVariable`: 从请求URL路径中取出参数`value`，如

```java
@GetMapping("/{id}")
public void getId(@PathVariable long id) {
    // processing...
}
```

如果`@PathVariable`没有`value`，则默认要取的参数与标注的函数参数同名(本例中为`{id}`), 否则

```java
@GetMapping("/{id}")
public void getId(@PathVariable("id") long userId) {
    // processing...
}
```

- `@RequestParam`: 从请求的参数中获取参数`value`，如

```java
@GetMapping("/")
public void getId(@RequestParam("id") long id) {
    // processing...
}
```

从类似URL: `http://host:port/?id=0`中取出对应的参数

- `@RequestHeader`: 从请求头中获取对应的参数`value`，如

```java
@GetMapping("/")
public void getId(@RequestHeader("User-Agent") userAgent) {
    // processing...
}
```

- `@RequestAttribute`: 从请求的域属性中获取对应的参数`value`，如

在之前拦截请求后再请求中添加了域属性并将其转发

```java
{
    request.setAttribute("msg", new Message("Message"));
    // do something...
}
```

那么就可以通过`@RequestAttribute`从请求中获取属性

```java
@GetMapping("/")
public void getMsg(@RequestAttribute("msg")) {
    // processing...
}
```

- `@RequestBody`: 从请求体中获取数据，通常是从表单中获取的信息；信息可以根据格式自动填充到函数参数的对应字段中. 

```html
<form th:action="@{/save}" th:method="put">
    <input id="username" type="text">
    <!-- form code... -->
    
	<input type="submit"/>
</form>
```

如

```java
@PostMapping("/save")
public void getUserInfo(@RequestBody User user) {
    // processing
}
```

- `@CookieValue`: 从Cookie中读取对应数据的值
- `@MatrixVariable`: 从请求URL中取出`value` (适用于cookie禁用的情况)

如对于URL`http://host:port/id;param1=val1;param2=val2`形式可以使用`@Matrix`

[!] MatrixVariable可能导致URL注入，SpringBoot默认禁止启用

```java
@GetMapping("/id")
public void getUser(@MatrixVariable("name") String name, 
                   @MatrixVariable("password") String password) {
    // processing...
}
```

