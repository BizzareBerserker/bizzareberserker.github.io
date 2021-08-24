---
layout: post
title: "Spring Integration Programming Considerations"
tag: springintegration
category: essay
---

- You should use POJO whenever possible and only expose the framework when absolute necessary.
- On a Spring Boot application, nothing more is needed with its default executable jar format. However, in a Spring application, `SpringFactories` mechanisms is required to load classes which plugin may not merge.

### POJO Method invocation

A POJO programming style is recommended as following example shows:

```java
@ServiceActivator
public String myService(String payload) {...}
```

Header information can be obtained in POJO methods, as the following example shows:

```java
@ServiceActivator
public String myService(@Payload String payload, 
                        @Header("foo") String fooHeader) {...}
```

You can also dereference properties on the message: 

```java
@ServiceActivator
public String myService(@Payload("payload.foo") String foo, 
                        @Header("bar.baz") String barbaz) {...}
```

Versions prior to 5.0 used SpEL to invoke POJO methods (for the capability to navigate a property path). Starting from version 5.0, `org.springframework.messaging.handler.invocation.InvocableHandlerMethod`is used by default, it is ususally faster than SpEL, under corner cases that do not work with `InvocableHandlerMethod`, we automatically fall back to using SpEL. 

If you wish to set up your POJO method such that it always uses SpEL, with `@UseSpelInvoker` as the following example shows: 

```java
@UseSpelInvoker(compilerMode = "IMMEDIATE")
public void bar(String bar) {...}
```

