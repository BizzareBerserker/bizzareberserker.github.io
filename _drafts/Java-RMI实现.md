---
layout: post
title: "Java RMI实现"
tags: rmi java
category: essay
---

### 直接使用Registry实现RMI

服务端：

```java
public class Main {

    public static void main(String[] args) {
        try {
            Registry registry = LocateRegistry.createRegistry(1099);
            HelloFacade facade = new HelloFacadeImpl();
            registry.bind("helloFacade", facade);
        } catch (RemoteException | AlreadyBoundException e) {
            e.printStackTrace();
        }

    }
}
```

接口：

```java
public interface HelloFacade extends Remote {

    String greet(String name) throws RemoteException;
}
```

实现：

```java
public class HelloFacadeImpl extends UnicastRemoteObject implements HelloFacade{

    public HelloFacadeImpl() throws RemoteException {
        super();
    }

    @Override
    public String greet(String name) throws RemoteException {
        return "Hello, " + name + "!";
    }
}
```

客户端：

```java
public class Main {

    public static void main(String[] args) {
        try {
            Registry registry = LocateRegistry.getRegistry(1099);
            HelloFacade facade = (HelloFacade) registry.lookup("helloFacade");
            String response = facade.greet("world");
            System.out.println(response);
        } catch (RemoteException | NotBoundException e) {
            e.printStackTrace();
        }
    }
}
```

### 通过Naming实现RMI

服务端：

```java
public static void main(String[] args) {
    try {
        Registry registry = LocateRegistry.createRegistry(1100);
        HelloFacade facade = new HelloFacadeImpl();
        Naming.bind("rmi://localhost:1099/helloFacade", facade);
    } catch (RemoteException | AlreadyBoundException | MalformedURLException e) {
        e.printStackTrace();
    }
}
```

客户端：

```java
public static void main(String[] args) {
    try {
        String remoteAddr = "rmi://localhost:1100/helloFacade";
        HelloFacade facade = (HelloFacade) Naming.lookup(remoteAddr);
        String response = facade.greet("world");
        System.out.println(response);
    } catch (RemoteException | NotBoundException | MalformedURLException e) {
        e.printStackTrace();
    }
}
```

