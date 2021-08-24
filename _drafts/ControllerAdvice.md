---
layout: post
title: "ControllerAdvice"
tags: spring springmvc
category: essay
---

`@ControllerAdvice`是在类上标注的注解，其本身包含了`@Component`注解. 在`@ControllerAdvice`标注的类内的`@ExceptionHandler`, `@InitBinder`, `@ModelAttribute`方法可以在全局范围内生效. 

### `@ExceptionHandler`

`@ExceptionHandler`用来处理该控制器内抛出的异常，配合`@ControllerAdvice`可实现全局异常处理. 

`@ExceptionHandler(value)`会处理`value`异常，如果value为空，则该方法会默认处理方法参数中列出的所有异常. 

```java
@ExceptionHandler(Exception.class)
public String customException(Exception e) {
	// do something
}
```

### `@ModelAttribute`

使用`@ModelAttribute`标记的方法在控制器任何`@RequestMapping`方法被调用之前初始化Model中的数据. 

```java
@ModelAttribute
public void populatedModel(@RequestParam String number, Model model) {
    model.addAttribute(accountRepository.findAccount(number));
    // add more ...
}
```

### `@InitBinder`

`@InitBinder`注解的方法会初始化`WebDataBinder`实例. 可以: 

- 将request参数(query参数或表单内容)绑定到Model上
- 将字符串类型的request值(request参数, 路径变量, header, cookie等)绑定到目标类型的控制器参数上

```java
@InitBinder("book")
public void bookBinder(WebDataBinder binder) {
    binder.setFieldDefaultPrefix("book.");
}
```

