---
title: Cookie和Session对象的学习
date: 2021-03-29 09:44:39
tags:
  - Javaweb
  - Cookie和Session
categories:
  - 后端
  - javaweb
description:  Cookie和Session对象的学习
---

# Cookie 和 Session的学习

+ Cooie 和 Session 是会话技术
    + 会话：一次会话中包含多次请求和响应，浏览器第一次给服务器资源发送请求，建立会话，知道有一方断开为止。
    + 功能：在一次会话的范围内的多次请求间共享数据。
    + 方式：
        + 客户端会话技术：Cookie
        + 服务器端会话技术：Session

## Cookie（客户端会话技术）

1. 概念：客户端绘画技术，将数据保存到客户端

2. 使用步骤：

    ```java
    1. 创建Cookie对象，绑定数据
        new Cookie(String name,String value);
    2. 发送Cookie对象
        response.addCookie(Cookie cookie);
    3. 获取Cookie，拿到数据
        Cookie[] request.getCookies();
    ```

3. 实现原理：基于响应头set-cookie和请求头cookie实现

     

4. Cookie的细节：

    + 一次可以发送多个cookie：创建多个Cookie对象并多次发送

    + cookie在浏览器中保存多长时间？

        + 默认情况下，当浏览器关闭后，cookie数据被销毁

        + 持久化存储：

            ```java
            setMaxAge(int seconds);
            1. 正数：将cookie数据写到硬盘文件中，持久存储，seconds为时间
            2. 负数：默认值
            3. 零 ：删除存储的cookie信息
            ```

    + cookie能不能存中文？

        + 在tomcat 8.5之前不能存储中文
            + 需要将中文数据转码---一般采用URL编码
        + 在tomcat 8.5以及以后可以存储中文，但不支持特殊符号
            + 建议使用URL编码存储，解析

    + cookie共享问题

        + 在一个tomcat服务器中部署了多个web项目，那么在这些web项目中cookie默认情况下也不能共享

            ```java
            //设置范围i，默认为当前虚拟目录
            setPath(String path)
            //如果要共享，可以设置path为： “/”
            ```

        + 不同的tomcat服务器cookie共享问题

            ```java
            //如果设置一级域名相同，那么多个服务器间的cookie可以共享
            setDomain(String path);
            ```

    + Cookie的特点和作用

        + 特点
            + cookie存储数据在客户端浏览器（不安全）
            + 浏览器对单个cookie的大小要求在4kb左右，以及同一域名下的总cookie不能超过20个
        + 作用
            + cookie一般用于存储少量不太敏感的数据
            + 在不登陆的情况下，完成服务器对客户但身份的识别



## Session  (服务器会话技术)

1. 概念：服务器端绘画技术，在一次会话的多次请求见共享数据，将数据保存在服务器对象中

    **HttpSesion**

2. 快速入门：

    ```java
    1.获取HttpSession对象
        HttpSession session=request.getSession();
    2.使用HttpSession对象
        Object getAttribute(String name);
    	void setAttribute(String name,Object value);
    	void removeAttribute(String name);
    ```

3. 原理：

    + Session的实现时以来Cookie的

4. 细节：

    + 当客户端关闭后，服务器不关闭两次获取的session是否为同一个？

        + 默认情况下不是

        + 如果需要相同，则可以创建Cookie，键为JSESSIONID，设置最大存活时间，让Session对象持久化保存

            ```java
            Cookie C=new Cookie("JESSIONID",session.getid());
            c.setMaxAge(60*60);
            response.addCookie(c);
            ```

    + 客户端不关闭，服务器关闭后，两次获取的session是同一个吗

        + 不是同一个，但是要确保数据不丢失，tomact会自动完成以下工作
            1. session的钝化：(tomcat会将数据信息存入work文件夹中)
                + 在服务器正常关闭之前，将session对象序列化到硬盘上
            2. session的活化：(将work文件夹数据取出，加入内存后删除)
                + 在服务器启动后，将session文件转化为内存中的session对象

    + session什么时候被销毁？

        + 服务器关闭

        + session对象调用invalidate();方法

        + session默认失效时间30分钟

            ```xml
            <session-config>
                <session-timeout>30</session-timeout>
            </session-config>
            ```

5. session的特点

    + session用于存储一次会话的多次请求的数据，存在服务器端
    + session可以存储任意类型，任意大小的数据

6. session与cookie的区别：

    + session存储树在服务器端，cookie在客户端
    + session没有数据大小和类型的限制，cookie有
    + session数据安全，cookie相对不安全