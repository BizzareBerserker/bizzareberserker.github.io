---
layout: post
title: "Servlet技术"
tags: java javaweb
category: essay
---

## Servlet

**Servlet**是运行在服务器上的Java小程序，它接收客户端发送的请求(request)并像客户端发送响应(response)。

要想编写一个Servlet，你需要实现`Servlet`接口：

```java
public interface Servlet {
    void init(ServletConfig var1) throws ServletException;

    ServletConfig getServletConfig();

    void service(ServletRequest var1, ServletResponse var2) throws ServletException, IOException;

    String getServletInfo();

    void destroy();
}
```

## Servlet配置

为了将Servlet注册到Web容器上，你需要在`web.xml`内填写配置信息对Servlet进行注册。对于Tomcat, 其配置文件在`webapp/WEB-INF/web.xml`下

```xml
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns="http://xmlns.jcp.org/xml/ns/javaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://xmlns.jcp.org/xml/ns/javaee http://xmlns.jcp.org/xml/ns/javaee/web-app_4_0.xsd"
         version="4.0">

</web-app>
```

配置文件中的元素包含下列：

- `<servlet>`: 将servlet注册到Web容器中. 
  - `<servlet-name>`: Servlet的名字 (区分Servlet的类名) 约定上与Servlet的类名对应
  - `<servlet-class>`: Servlet的完全限定类名 (供Web容器进行索引)
  - `<init-param>`: 为Servlet提供初始化参数
    - `<param-name>`: 参数名称
    - `<param-value>`: 参数值

```xml
<servlet>
    <servlet-name>HelloServlet</servlet-name>
    <servlet-class>com.example.HelloServlet</servlet-class>
    <init-param>
    	<param-name>username</param-name>
        <param-value>root</param-value>
    </init-param>
</servlet>
```

- `<servlet-mapping>`: 建立某个servlet和特定地址的请求的映射.
  - `<servlet-name>`: 要建立映射的servlet
  - `<url-pattern>`: 要映射到的URL (完整的请求URL为: http://host:port/project-directory\<url-pattern\>). 一般约定url应当和Servlet名称对应

```xml
<servlet-mapping>
    <servlet-name>HelloServlet</servlet-name>
    <url-pattern>/hello</url-pattern>
</servlet-mapping>
```

## Servlet生命周期

Servlet的声明周期包含以下几步：初始化 -> 执行 -> 销毁

### 初始化

1. 寻找：Web容器(如Tomcat) 会在程序启动时根据web.xml中的完全限定类名寻找类
2. 加载：类加载器会在某一时刻将找到的Servlet加载
3. 创建Servlet: 调用Servlet的构造器创建Servlet
4. `init`: 执行初始化方法初始化Servlet，通过两个配置信息进行配置
   - `ServletConfig`: 当前Servlet的配置参数，从`web.xml`中加载，只对当前Servlet有效
   - `ServletContext`: 全局配置信息，对当前容器中的所有Servlet有效. `ServletContext`只能通过`ServletConfig`来间接得到

```java
public interface ServletConfig {
    
    public String getServletName();

    public ServletContext getServletContext();

    public String getInitParameter(String name);

    public Enumeration<String> getInitParameterNames();

}
```

```java
public interface ServletContext {
    
    public String getInitparameter(String name);
    
    public String getContextPath();
    
    public String getRealPath();
}
```



### 执行

1. 创建请求(ServletRequest)和响应(ServletResponse)，并为当前会话开一个线程
2. 调用`service`方法
3. 执行代码：读取`ServletRequest`内容，并写入`ServletResponse`

### 销毁

1. 调用`destroy`方法

## HttpServlet

对于基于HTTP的服务，一般情况下实现`Servlet`的子接口`HttpServlet`来提供HTTP服务。`HttpServlet`与`Servlet`大体相同，但是把`service`方法分解了`doGet`和`doPost`等方法，分别对应HTTP的GET, POST等请求

```java
public abstract class HttpServlet extends GenericServlet {
	public HttpServlet() {
    }
    
    protected void doGet(HttpServletRequest req, HttpServletResponse resp) 
        	throws ServletException, IOException {
        String protocol = req.getProtocol();
        String msg = lStrings.getString("http.method_get_not_supported");
        if (protocol.endsWith("1.1")) {
            resp.sendError(405, msg);
        } else {
            resp.sendError(400, msg);
        }

    }
    
    protected void doPost(HttpServletRequest req, HttpServletResponse resp) 
        	throws ServletException, IOException {
        String protocol = req.getProtocol();
        String msg = lStrings.getString("http.method_post_not_supported");
        if (protocol.endsWith("1.1")) {
            resp.sendError(405, msg);
        } else {
            resp.sendError(400, msg);
        }

    }
    
    ...
    
    protected void service(HttpServletRequest req, HttpServletResponse resp) 
        	throws ServletException, IOException {
        String method = req.getMethod();
        long lastModified;
        if (method.equals("GET")) {
            lastModified = this.getLastModified(req);
            if (lastModified == -1L) {
                this.doGet(req, resp);
            } else {
                long ifModifiedSince = req.getDateHeader("If-Modified-Since");
                if (ifModifiedSince < lastModified) {
                    this.maybeSetLastModified(resp, lastModified);
                    this.doGet(req, resp);
                } else {
                    resp.setStatus(304);
                }
            }
        } else if (method.equals("HEAD")) {
            lastModified = this.getLastModified(req);
            this.maybeSetLastModified(resp, lastModified);
            this.doHead(req, resp);
        } else if (method.equals("POST")) {
            this.doPost(req, resp);
        } else if (method.equals("PUT")) {
            this.doPut(req, resp);
        } else if (method.equals("DELETE")) {
            this.doDelete(req, resp);
        } else if (method.equals("OPTIONS")) {
            this.doOptions(req, resp);
        } else if (method.equals("TRACE")) {
            this.doTrace(req, resp);
        } else {
            String errMsg = lStrings.getString("http.method_not_implemented");
            Object[] errArgs = new Object[]{method};
            errMsg = MessageFormat.format(errMsg, errArgs);
            resp.sendError(501, errMsg);
        }

    }
    
    ...
}
    
```

### Servlet Hierarchy

![Servlet Hierarchy](/assets/servlet_0.png)