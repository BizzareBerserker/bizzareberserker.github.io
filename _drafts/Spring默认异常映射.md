---
layout: post
title: "Spring默认异常映射"
tags: spring springmvc
category: essay
---

在默认情况下，Spring会自动将一些异常转换为合适的状态码

|Exception|HTTP Status|
|---|---|
|`BindException`|400|
|`HttpMessageNotReadableException`|400|
|`MethodArgumentNotValidException`|400|
|`MissingServletRequestParameterException`|400|
|`MissingServletRequestPartException`|400|
|`TypeMismatchException`|400|
|`NoSuchRequestHandlingMethodException`|404|
|`HttpRequestMethodNotSupportedException`|405|
|`HttpMediaTypeNotAcceptableException`|406|
|`HttpMediaTypeNotSupportedException`|415|
|`ConversionNotSupportedException`|500|
|`HttpMessageNotWritableException`|500|