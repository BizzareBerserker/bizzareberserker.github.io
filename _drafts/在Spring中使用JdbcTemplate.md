---
layout: post
title: "在Spring中使用JdbcTemplate"
tag: "spring"
---

### 使用JdbcTemplate插入数据

使用JdbcTemplate来插入数据

```java
int update(String s, Object... objects) {
    // ...
}
```

### 使用JdbcTemplate读取数据

`int queryForObject(String s, RowMapper<T> rowMapper)`

### 使用命名参数
