---
layout: post
title: "Kafka配置"
tag: kafka
category: essay
---

Kafka broker的一些配置选项。这些参数是单个服务器的基本配置，在部署到其他环境时需要修改。

### 基本

`broker.id` : broker 的标识符，默认为0. 这个值在一个Kafka集群里必须是唯一的。

### Socket服务器设置

`listeners` : 设置Socket服务器监听的地址。格式：`listener_name://host:port`

### 日志信息

`log.dirs`: 一个由逗号分隔的列表，设置日志文件的保存路径

`num.partitions`: 每个主题的默认分区数。该值越大并行程度越高。

`num.recovery.threads.per.data.dir`: 为每个日志目录分配的线程数。在服务崩溃时，每个日志目录分配多个线程可以执行并行操作加快恢复速度。默认情况下每个目录只使用1个线程。

`log.rentention.hour`: 日志的保留时间。根据时间保留数据一般是通过检查日志的最后修改时间来实现。

`log.rentention.bytes`: 该主题最多可以保存的数据大小。当消息超过了限定值，多出的部分会被删除。

`log.segment.bytes`: 单个日志片段的最大大小。当超过此大小时，会创建一个新的日志片段。

`log.segment.ms`: 多长时间后一个日志片段会被关闭（创建一个新的日志片段）

`message.max.bytes`: 单个消息的最大大小。如果生产者尝试发送的消息超过这个大小，broker会返回错误信息。

### Zookeeper设置

`zookeeper.connect`: 设置保存broker元数据的Zookeeper地址. 

`zookeeper.connectin.timeout.ms`: 连接zookeeper的超时时间 (单位：ms)

### 其他

`auto.create.topics.enable`: 设置是否自动创建主题。默认情况下kafka在以下情况下自动创建主题：

- 生产者开始往主题写入消息
- 消费者开始从主题都区小溪
- 任意客户端向主题发送元数据请求

### 说明

- 为主题选定分区数量需要考虑以下几个因素：
  - 主题需要的吞吐量
  - 单个分区的最大吞吐量
  - 可用的磁盘空间和网络带宽
- 如果同时指定了`log.rentention.bytes`和`log.rentention.ms`，那么只要满足其中任意一个条件，消息就会被删除
-  如果同时指定了`log.segment.ms`和`log.segment.bytes`，那么只要满足其中任意一个条件，日志片段就会被关闭
- 如果消费者设置的`fetch.message.max.bytes`小于broker的`message.max.bytes` ，消费者可能被堵塞。确保协调客户端和broker之间的消息大小配置。