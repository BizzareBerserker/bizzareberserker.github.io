---
layout: post
title: "使用Spring发送电子邮件"
tag: spring
category: essay
---

使用Spring Mail之前先引入依赖: 

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-mail</artifactId>
    <version>2.5.2</version>
</dependency>
```

### 配置MailSender

Spring Email的核心是`MailSender`接口. Spring Email通过`MailSender`接口实现来连接到Email服务器并发送邮件. 

```java
public interface MailSender {
    
    void send(SimpleMailMessage simpleMessage) throw MailException;
    
    void send(SimpleMailMessage... simpleMessages) throw MailException;
}
```

Spring自带了一个`MailSender`实现即`JavaMailSenderImpl`, 它使用Java Mail API来发送邮件. 

按最简单的形式配置一个MailSender形式如下: 

```java
@Bean
public MailSender mailSender(Environment env) {
    JavaMailSenderImpl mailSender = new JavaMailSenderImpl();
    mailSender.setHost(env.getProperty("mailserver.host"));
    return mailSender;
}
```

在SpringBoot中，你可以通过属性来调节自动配置的MailSender: 

|Property|Default Value|
|---|---|
|spring.mail.host||
|spring.mail.port||
|spring.mail.username||
|spring.mail.password||
|spring.mail.protocol|smtp|

### 使用MailSender

首先在服务类中装配MailSender: 

```java
@Autowired
JavaMailSender mailSender;
```

之后需要构建消息. 以发送简单的文本消息为例，指明消息的发送者和接受者，以及主题和内容. 最后把消息传递给mailSender的send方法就可以发送邮件了. 

```java
public void sendSimpleMessage(String to, String subject, String content) {
    SimpleMailMessage message = new SimpleMailMessage();
    message.setFrom("noreply@mail.com");
    message.setTo(to);
    message.setSubject(subject);
    message.setText(content);
    mailSender.send(message);
}
```

### 构建复杂的Email消息

- 带有附件的Email

对于带有附件的Email，我们使用MIME消息来发送一个Multipart类型的Email. 

```java
MimeMessage message = mailSender.createMimeMessage(); 
```

由于MimeMessage的API过于笨重，Spring提供了MimeMessageHelper来简化MIME消息的配置. 

```java
public MimeMessageHelper(MimeMessage mimeMessage, boolean multipart) throws MessagingException {
    //...
}
```

将创建的Mime消息传给此构造器构造一个MimeMessageHelper, 之后就可以使用helper的方法组装Email消息了

Helper中的相关方法: 

```java
public void setFrom(String from);

public void setTo(String to);

public void setSubject(String subject) throw MessagingException;

public void setText(String text) throw MessagingException;

public void setText(String text, boolean html);

public void addAttachment(String attachmentFilename, DataSource dataSource) throws MessagingException;

public void addAttachment(String attachmentFilename, File file) throws MessagingException;

public void addAttachment(String attachmentFilename, InputStreamSource inputStreamSource) throws MessagingException;
```

- 富文本内容的Email

你可以使用方法`setText(String text, boolean html)`中将html设置为true来发送带有HTML格式的Email. 

为消息添加嵌入式内容的方法与添加附件的方法很类似: 

```java
public void addInline(String contentId, DataSource dataSource) throws MessagingExceptoin;

public void addInline(String contentId, File file) throws MessagingException;

public void addInline(String contentId, Resource resource) throws MessagingException;

public void addInline(String contentId, InputStreamSource inputStreamSource, String contentType) throws MessagingException;
```

其中第一个参数指内嵌内容的标识符，第二个参数指内嵌内容的资源引用; 例如，对于图片，你可以通过`<img src="cid:[contentId]">`来引用嵌入的图片 (其中contentId指在addInline方法中设置的内嵌内容标识符)

- 通过模板构建Email

以Thymeleaf为例，