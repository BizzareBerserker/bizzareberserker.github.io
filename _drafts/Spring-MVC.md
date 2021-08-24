---
layout: post
title: "Spring MVC"
tag: spring springmvc
category: essay
---

### Spring MVC的请求流程

![Request](/assets/spring_4.png)

## Spring MVC配置

### 通过XML配置

1. 配置Spring容器: `WEB-INF/web.xml`

- 配置`ContextLoaderListener`

```xml
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>classpath:applicationContext.xml</param-value>
</context-param>

<!-- Bootstrap the root web application context -->
<listener>
	<listener-class>ContextLoaderListener</listener-class>
</listener>
```

- 配置`DispatcherServlet`

```xml
<servlet>
	<servlet-name>dispatcherServlet</servlet-name>
    <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
    <load-on-startup>1</load-on-startup>
</servlet>

<servlet-mapping>
	<servlet-name>dispatcherServlet</servlet-name>
    <url-pattern>/</url-pattern>
</servlet-mapping>
```

- 配置`CharacterEncodingFilter`

```xml
<filter>
	<filter-name>CharacterEncodingFilter</filter-name>
    <filter-class>org.springframework.web.filter.CharacterEncodingFilter</filter-class>
    
    <init-param>
    	<param-name>encoding</param-name>
        <param-value>utf-8</param-value>
    </init-param>
    
    <init-param>
    	<param-name>forceRequestEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
    
    <init-param>
    	<param-name>forceResponseEncoding</param-name>
        <param-value>true</param-value>
    </init-param>
</filter>

<filter-mapping>
	<filter-name>CharacterEncodingFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

- 配置`HiddenHttpMethodFilter`

```xml
<filter>
	<filter-name>HiddenHttpMethodFilter</filter-name>
    <filter-class>org.springframework.web.filter.HiddenHttpMethodFilter</filter-class>
</filter>

<filter-mapping>
	<filter-name>HiddenHttpMethodFilter</filter-name>
    <url-pattern>/*</url-pattern>
</filter-mapping>
```

2. 配置Spring MVC (`DIspatcherServlet`): `dispatcherServlet-serlvet.xml`

- 开启组件扫描

```xml
<context:component-scan base-package="com.atguigu" use-default-filters=true>
	<context:include-filter type="annotation" expression="org.springframework.stereotype.Controller"></context:include-filter>
</context:component-scan>
```

- 配置视图解析器

```xml
<bean class="org.springframework.web.servlet.view.InternalViewResolver">
	<property name="prefix" value="/WEB-INF/views/"></property>
    <property name="suffix" value=".html"></property>
</bean>
```

- 其他标准配置

```xml
<!-- dispatch requests that Spring MVC unable to handle to Tomcat -->
<mvc:default-servlet-handler/>
<!-- add more supports -->
<mvc:annotation-driven/>
```

3. 配置Spring (业务逻辑 / `ContextLoaderListener`): `src/main/resources/applicationContext.xml`

### 通过Java配置

1. 继承`AbstractAnnotationConfigDispatcherServletInitializer`

```java
public class WebAppInitializer extends AbstractAnnotationConfigDispatcherServletInitializer {
    
    @Override
    protected String[] getServletMappings() {
        return new String[] { "/" };
    }
    
    @Override
    protected Class<?>[] getRootConfigClasses() {
        return new Class<?>[] { RootConfig.class };
    }
    
    @Override
    protected Class<?>[] getServletConfigClasses() {
        return new Class<?>[] { WebConfig.class };
    }
}
```

2. 配置DispatcherServlet配置类

```java
@Configuration
@EnableWebMvc
@ComponentScan
public class WebConfig extends WebMvcConfigurerAdapter {
    
    @Bean
    public ViewResolver viewResolver() {
        InternalResourceViewResolver = new InternalResourceViewResolver();
        resolver.setPrefix("/WEB-INF/views/");
        resolver.setSuffix(".html");
        resolver.setExposeContextBeanAsAttributes(true);
        return resolver;
    }
    
    @Override
    public void configureDefaultServletHandling(DefaultServletHandlerCOnfigurer configurer) {
        configurer.enable();
    }
}
```

3. 配置ContextLoaderListener配置类

```java
@Configuration
@ComponentScan(basePackage={}, excludeFilters={...})
public class RootConfig {}
```

