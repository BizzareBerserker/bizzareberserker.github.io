---
layout: post
title: "Kafka生产者"
tag: kafka
category: essay
---

### 生产者概览

![Overview of Kafka Producer](\assets\kafka_1.png)

## 生产者配置

### 必选属性

`bootstrap.servers`: broker的地址清单。不需要包含所有broker地址，但建议至少提供2个。

`key.serializer`：键的序列化器。

`value.serializer`： 值的序列化器。

### 可选属性

`acks`：必须有多少个副本接收消息才认为消息发送成功。acks=0: Producer在成功写入前不等待服务器的响应；acks=1: 在broker的leader收到消息后Producer收到成功响应；acks=all: 所有参与复制的broker全部收到后Producer收到成功响应

`buffer.memory`：Producer的内存缓冲区大小

`compression.type`：消息压缩类型(snappy, gzip, lz4). 默认不压缩

`retries`：Producer重试次数（临时性错误）

`batch.size`：最大批次大小

`linger.ms`：发送批次前的等待时间

`client.id`：broker用来表示消息来源

`max.in.flight.requests.per.connection`： Producer在接到broker响应前最多发送消息树

`timeout.ms`, `request.timeout.ms`, and `metadata.fetch.timeout.ms`

`max.block.ms`：Producer的最大阻塞时间

`max.request.size`：Producer发送的请求大小

`receive.buffer.bytes` and `send.buffer.bytes`：TCP socket接收和发送数据包的缓冲大小. 默认为-1（OS默认值）

使用以上配置构造一个生产者：

```java
private Properties kafkaProps = new Properties(); 
kafkaProps.put("bootstrap.servers", "broker1:9092,broker2:9092");
kafkaProps.put("key.serializer", 
"org.apache.kafka.common.serialization.StringSerializer"); 
kafkaProps.put("value.serializer",
 "org.apache.kafka.common.serialization.StringSerializer");
producer = new KafkaProducer<String, String>(kafkaProps);
```

## Serializer

### Kafka提供的Serializer

Kafak在`org.apache.kafka.common.serialization`包中提供了几个内置的序列化器，如

- `ByteArraySerializer`
- `StringSerializer`
- `IntegerSerializer`
- `FloatSerializer`

### 自定义Serializer

实现`Serializer`接口来手动实现一个序列化器。

```java
public interface Serializer<T> extends Closeable {

    /**
     * Configure this class.
     * @param configs configs in key/value pairs
     * @param isKey whether is for key or value
     */
    default void configure(Map<String, ?> configs, boolean isKey) {
        // intentionally left blank
    }

    /**
     * Convert {@code data} into a byte array.
     *
     * @param topic topic associated with data
     * @param data typed data
     * @return serialized bytes
     */
    byte[] serialize(String topic, T data);

    /**
     * Convert {@code data} into a byte array.
     *
     * @param topic topic associated with data
     * @param headers headers associated with the record
     * @param data typed data
     * @return serialized bytes
     */
    default byte[] serialize(String topic, Headers headers, T data) {
        return serialize(topic, data);
    }

    /**
     * Close this serializer.
     * <p>
     * This method must be idempotent as it may be called multiple times.
     */
    @Override
    default void close() {
        // intentionally left blank
    }
}
```

### 已有的Serializer框架

推荐使用已有的Serializer/Deserializer框架，如

- JSON
- Avro
- Thrift
- Protobuf

## 分区

### 默认的Partitioner

Kafka提供了一些默认的分区器：

- DefaultPartitioner (如果分区指定，那么发往指定分区；如果为指定，则根据键的哈希值发往某个分区)
- RoundRobinPartitioner（将消息均匀发往各个分区）

### 自定义Partitioner

实现Partitioner接口可以自定义分区器：

```java
public interface Partitioner extends Configurable, Closeable {

    /**
     * Compute the partition for the given record.
     *
     * @param topic The topic name
     * @param key The key to partition on (or null if no key)
     * @param keyBytes The serialized key to partition on( or null if no key)
     * @param value The value to partition on or null
     * @param valueBytes The serialized value to partition on or null
     * @param cluster The current cluster metadata
     */
    public int partition(String topic, Object key, byte[] keyBytes, Object value, byte[] valueBytes, Cluster cluster);

    /**
     * This is called when partitioner is closed.
     */
    public void close();


    /**
     * Notifies the partitioner a new batch is about to be created. When using the sticky partitioner,
     * this method can change the chosen sticky partition for the new batch. 
     * @param topic The topic name
     * @param cluster The current cluster metadata
     * @param prevPartition The partition previously selected for the record that triggered a new batch
     */
    default public void onNewBatch(String topic, Cluster cluster, int prevPartition) {
    }
}

```

