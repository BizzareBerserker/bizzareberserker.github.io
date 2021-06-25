---
layout: post
title: "关于Lambda和方法引用"
tag: java
category: essay
---

### 关于Lambda表达式

在Java8中，带有单个抽象方法的接口称为**函数接口**，应尽量通过Lambda表达式创建这些接口的实例（函数对象）。在使用Lambda表达式时：

- 不要添加Lambda参数的类型，除非它能使代码更清晰或编译器无法推导其类型。
- 如果计算本身不是自描述或过长，避免使用Lambda
- 尽量避免序列化Lambda

### 关于方法引用

方法引用通常比Lambda更加简洁。如果方法引用更加简洁，使用方法引用；如果方法引用不简洁，使用Lambda表达式。

### 关于函数接口

`java.util.Function`中定义了43个函数接口，其中6个基础函数接口如下：

|接口|函数签名|
|---|---|
|`UnaryOperator<T>`|`T apply(T t)`|
|`BinaryOperator<T>`|`T apply(T t1, T t2)`|
|`Predicate<T>`|`boolean test(T t)`|
|`Function<T, R>`|`R apply(T t)`|
|`Supplier<T>`|`T get()`|
|`Consumer<T>`|`void accept(T t)`|

通过这六个基础函数接口就可以推断出其他的函数接口的名称。在使用函数接口时，应注意：

- 如果标准函数接口能够满足需求，就考虑标准函数接口而不是创建新的函数接口
- 不要使用带包装类型的基础函数接口来代替基础函数接口
- 在下列情况考虑构建专用的函数接口
  - 通用，名称具有描述性
  - 接口有与其相关的规定
  - 有定制的缺省方法
- 始终用`@FunctionalInterface`标注自己编写的函数接口