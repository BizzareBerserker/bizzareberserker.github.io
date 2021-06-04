---
layout: post
title: "在Spring中使用JdbcTemplate"
tag: "spring"
---

### 使用JdbcTemplate更改数据

使用JdbcTemplate来插入/更新/删除数据，使用update方法

```java
int update(String s, Object... objects)
```

其中s为要执行的SQL语句，objects为SQL语句按顺序对应的参数。

将该方法封装在Repository中：

### 使用JdbcTemplate读取数据

使用queryForObject方法来从数据库中读取一条记录并将其映射为Java对象

```java
<T> T queryForObject(String s, RowMapper<T> rowMapper, Object... objects)
```

其中s为要执行的SQL语句，rowMapper将记录映射为Java对象，objects为SQL语句对应参数

在Java8中可以利用Lambda表达式或方法引用来改写

```java
(rs, rowNum) -> {
    return new Spitter(
    	rs.getLong("id"),
        rs.getString("username"),
        rs.getString("password"));
}
```

将该方法封装在Repository中：

### 使用命名参数

使用命名参数需要使用`NamedParameterJdbcTemplate`模板类。它的声明方式与`JdbcTemplate`几乎完全相同。

```java
@Bean
public NamedParameterJdbcTemplate jdbcTemplate(DataSource dataSource) {
    return new NamedParameterJdbcTemplate(dataSource);
}
```

在SQL语句中用`:param`来表示参数名，在使用`NamedParameterJdbcTemplate`时要传入的就不是顺序参数，而是一个参数-对象的`Map`: `Map<String, Object> paramMap`. 

```java
jdbcOperations.update(INSERT_STATEMENT, paramMap);
```

