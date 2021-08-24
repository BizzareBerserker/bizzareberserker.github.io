---
layout: post
title: "Spring Integration Message Endpoints"
tag: springintegration
category: essay
---

## Message Endpoints

### Message Transformer

A message transformer is responsible for converting a message’s content or structure and returning the modified message.

![Message Transformer](/assets/spring_5.png)

### Message Filter

A message filter determines whether a message should be passed to an output channel at all.

![Message Filter](/assets/spring_6.png)

### Message Router

A message router is responsible for deciding what channel or channels (if any) should receive the message next.

![Message Router](/assets/spring_7.png)

### Splitter

A splitter is another type of message endpoint whose responsibility is  to accept a message from its input channel, split that message into  multiple messages, and send each of those to its output channel.

![Splitter](/assets/spring_8.png)

### Aggregator

The aggregator is a type of  message endpoint that receives multiple messages and combines them into a single message.

![Aggregator](/assets/spring_9.png)

### Service Activator

A Service Activator is a generic endpoint for connecting a service instance to the messaging system. The service activator invokes an operation on some service object to  process the request message, extracting the request message’s payload  and converting (if the method does not expect a message-typed  parameter). Whenever the service object’s method returns a value, that return value  is likewise converted to a reply message if necessary (if it is not  already a message type). That reply message is sent to the output channel.

![Service Activator](/assets/spring_10.png)

### Channel Adapter

A channel adapter is an endpoint that connects a message channel to some other system or transport. Channel adapters may be either inbound or outbound.

![Channel Adapter](/assets/spring_11.png)

