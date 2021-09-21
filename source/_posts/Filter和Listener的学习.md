---
title: Filter和Listener的学习
date: 2021-04-08 12:33:21
tags:
  - Javaweb
  - Filter和Listener的学习
categories:
  - 后端
  - javaweb
description:   Filter和Listener的学习
---

# Filter 和 Listener

## Filter：监听器

1. 概念：

    + 当访问服务器资源时，过滤器可以将请求拦截下来，完成一些特殊的功能
    + 一般用于完成通用的操作。如：登陆验证、统一编码处理、敏感字符过滤等

2. 快速入门：

    + 定义一个类，实现Filter接口
    + 复写方法
    + 配置拦截路径：web.xml 或者  注解

3. 过滤器细节

    1. web.xml配置

        ```xml
        <filter>
          <filter-name>demo1</filter-name>
          <filterclass>cn.itcast.web.filter.FilterDemo1</filter-class>
        </filter>
        <filter-mapping>
        	<filter-name>demo1</filter-name>
        	<!-- 拦截路径 -->
        	<url-pattern>/*</url-pattern>
        </filter-mapping>
        ```

    2. 过滤器执行流程

        + 执行过滤器
        + 执行放行后的资源
        + 回来执行过滤器放行代码下的代码

    3. 过滤器声明周期

        + init：在服务器启动后，会创建Filter对昂，然后调用init方法。只执行一次。用于加载资源
        + doFilter：每次请求被拦截资源是，会执行，可以多次执行
        + destroy：在服务器关闭后，Filter对象被销毁。如果服务器正常关闭，则会执行destroy方法。只执行一次。用于释放资源

    4. 过滤器配置详解

        + 路径配置：

            1. /index.jsp  只有访问index.jsp资源时，过滤器才会被执行
            2. 拦截目录：/user/* 访问/user下的所有资源时，过滤器都会被执行
            3. 后缀名拦截：*.jsp 访问所有后缀名为jsp资源时，过滤器都会被执行
            4. 拦截所有资源：/* 访问所有资源，过滤器都会被执行

        + 拦截方式配置：

            1. 注解配置：设置dispatcherTypes属性

                + REQUEST：默认值。浏览器直接请求资源
                + FORWARD：转发访问资源
                + INCLUDE：包含访问资源
                + ERROR：错误跳转资源
                + ASYNC：异步访问资源

            2. webxml配置      
                + 设置<dispatcher></dispatcher>标签即可

    5. 过滤器链(配置多个过滤器)

        + 执行顺序：如果有两个过滤器： 过滤器1和过滤器2
            1. 过滤器1
            2. 过滤器2
            3. 执行资源
            4. 过滤器2
            5. 过滤器1
        + 过滤器先后顺序：
            1. 注解配置：按照类名的字符串比较规则比较，较小的限制性
            2. web.xml配置：<filter-mapping>谁定义在上面谁先执行



## Listener：监听器

1. 概念：web的三大组件之一

    + 事件监听机制：
        + 事件：一件事情
        + 事件源：事情发生的地方
        + 监听器：一个对象
        + 注册监听：将事件、事件源、监听器绑定在一起。当事件源上发生某个事件后，执行监听器代码

2. ServletContextListener：监听ServletContext对象的创建和销毁：

    + 方法：

        ```java
        void contextDestroyed(ServletContextEvent sce):ServletContext对象被销毁之前会调用该方法
        void contextInitialized(ServletContextEvent sce):ServletContext对象创建后会调用该方法
        ```

    + 步骤：

        1. 定义一个类，实现ServletContextListener接口

        2. 复写方法

        3. 配置：

            + web.xml

                ```xml
                <listener>				 <listener-class>cn.itcast.web.listener.ContextLoaderListener</listener-class>			
                </listener>
                
                * 指定初始化参数<context-param>
                ```

            + 注解

                + @WebListener

