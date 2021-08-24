---
layout: post
title: "Message Channel Interface"
tag: springintegration
category: essay
---

## Message Channel

### `MessageChannel`

Spring Interation's top-level `MessageChannel` interface is defined as below:

```java
public interface MessageChannel {
    
    boolean send(Message message);
    
    boolean send(Message message, long timeout);
}
```

When sending a message, the return value is `true` if the message is sent successfully. If the send call times out or is interrupted, it returns `false`.

### `PollableChannel`

`PollableChannel` defines the buffering behavior (receive).

```java
public interface PollableChannel extends MessageChannel {

    Message<?> receive();

    Message<?> receive(long timeout);

}
```

When receiving a message, the return value is null in the case of a timeout or interrupt.

### `SubscribableChannel`

The base interface is implemented by channels that send messages directly to their subscribed `MessageHandler` instances. They define methods for managing those subscribers.

```java
public interface SubscribableChannel extends MessageChannel {

    boolean subscribe(MessageHandler handler);

    boolean unsubscribe(MessageHandler handler);

}
```

## Channel Interceptors

Channel Interceptors provides one way to capture meaningful information about the messages passing through the system in a non-invasive way. 

```java
public interface ChannelInterceptor {

    Message<?> preSend(Message<?> message, MessageChannel channel);

    void postSend(Message<?> message, MessageChannel channel, boolean sent);

    void afterSendCompletion(Message<?> message, MessageChannel channel, boolean sent, Exception ex);

    boolean preReceive(MessageChannel channel);

    Message<?> postReceive(Message<?> message, MessageChannel channel);

    void afterReceiveCompletion(Message<?> message, MessageChannel channel, Exception ex);
}
```

The methods that returns a `Messge` instance can be used for transforming the `Message` or return `null` to simply prevent further processing. 

Also, the `preReceive` method can return `false` to prevent the receive operation from proceeding.