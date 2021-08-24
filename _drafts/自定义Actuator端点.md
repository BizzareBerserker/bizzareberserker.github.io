---
layout: post
title: "自定义Actuator端点"
tag: springboot
category: essay
---

### Health

在Actuator中给health端点添加额外的监控指标的方法有两种：

- 实现`HealthIndicator`接口并用`@Component`标注。类的名称应该为`XxxHealthIndicator`. 示例：

```java
@Component
public class CustomHealthIndicator implements HealthIndicator {

    private static Health.Builder builder = new Health.Builder();

    @Override
    public Health health() {
        Map<String, Object> map = new HashMap<>();
        if (true) {
            map.put("status", true);
            return builder.up().withDetails(map).build();
        } else {
            map.put("status", false);
            map.put("timeout", 300);
            return builder.down().withDetails(map).build();
        }
    }
}
```

- 继承`AbstractHealthIndicator`抽象类并用`@Component`标注。类的名称应该为`XxxHealthIndicator`. 示例：

```java
@Component
public class CustomHealthIndicator extends AbstractHealthIndicator {

    @Override
    protected void doHealthCheck(Health.Builder builder) throws Exception {
        if (true) {
            builder.up().withDetail("expected", true);
        } else {
            builder.down().withDetail("timeout", 300)
                .withDetail("expected", false);
        }
    }
}
```

### Info

`info`端点展示了关于当前应用的相关信息。在SpringBoot中，访问info端点默认为空：

```json
{}
```

如果要为`info`端点添加内容，可以通过以下两种方法：

- 在`application.properties`中添加相应内容. 在`info`后添加的任意属性都会作为info端点下的信息。

```properties
info.id=reading-list
info.version=1.0.0
```

- 实现`InfoContributor`. 通过`withDetail`方法向 `info`端点添加属性。示例：

```java
@Component
public class AppInfoContributor implements InfoContributor {
    @Override
    public void contribute(Info.Builder builder) {
        builder.withDetail("parent", "None");
    }
}
```

应用启动时，SpringBoot会取application.properties和InfoContributor中属性的并集作为`info`端点的内容：

```json
{"id":"reading-list","version":"2.8.1","parent":"None"}
```

