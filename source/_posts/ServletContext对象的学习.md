---
title: ServletContext对象的学习
date: 2021-03-27 19:29:05
tags:
  - Javaweb
  - ServletContext
categories:
  - 后端
  - javaweb
description:  ServletContext对象的学习
---

# ServletContext对象

### 概念

代表整个web应用，可以和程序的容器（服务器）来通信



### 获取

1. 通过 request 对象获取

    ```java
    request.getServletContext();
    ```

2. 通过 HttpServlet 获取

    ```java
    this.getServletContext();
    ```



### 功能：

1. 获取 MIME 类型：

    + MIMI 类型：在互联网通信过程中定义的一种文件数据类型
    + 格式类型： 大类型/小类型   例如： text/html    image/jpeg
    + 获取方式：

    ```java
    String getMimeType(String file);
    ```

2. 域对象：共享数据

    ```java
    1. setAttribute(String name,Object value);
    2. getAttribute(String name);
    3. removeAttribute(String name);
    ```

    + ServletContext对象范围：所有用户松油请求的数据

3. 获取真实(服务器)路径

    ```java
    String getRealPath(String path)；
    ```

    