---
title: web相关知识和tomcat
date: 2021-03-31 09:49:09
tags:
  - Javaweb
  - web相关知识和tomcat
categories:
  - 后端
  - tomcat
description:  ServletContext对象的学习
---

# Web相关知识和Tomcat

## Web相关概念

1. 软件架构
    + C/S	客户端/服务器端
    + B/S	浏览器/服务器端
2. 资源分类
    + 静态资源：所有用户访问后，得到的结果都是一样的，成为静态资源，静态资源可以被浏览器直接解析
        + 如：HTML	CSS	JS
    + 动态资源：每个用户访问相同资源后，得到的结果可能不相同，称为动态资源，动态资源被访问后，需要先转化为静态资源，在返回给浏览器
        + 如：Servlet / 	JSP，PHP，ASP
3. 网络通信的三要素：
    + IP：电子设备在网络中的唯一标识
    + 端口：应用程序在计算机中的唯一标识
    + 传输协议：规定了数据传输的规则
        + TCP协议：安全协议，三次握手，速度较慢
        + UDP协议：不安全协议，速度快
4. Web服务器软件：
    + 服务器：安装了服务器软件的计算机
    + 服务器软件：接受用户的请求，处理请求，做出响应
    + Web服务器软件：接受用户请求，处理请求，做出相应
    + 在Web服务器软件中，可以部署Web项目，让用户通过浏览器来访问这些项目Web容器



## Tomcat：Web服务器软件

1. 下载

2. 安装：目标不要有中文和空格

3. 卸载：删除文件夹

4. 启动：注意配置环境变量，端口要注意不要被占用  8080

5. 关闭：ctrl+C

6. 配置：

    ```
    * 部署项目的方式：
    1. 直接将项目放到webapps目录下即可。
    * /hello：项目的访问路径-->虚拟目录
    * 简化部署：将项目打成一个war包，再将war包放置到webapps目录下。
    * war包会自动解压缩
    
    2. 配置conf/server.xml文件
    在<Host>标签体中配置
    <Context docBase="D:\hello" path="/hehe" />
    * docBase:项目存放的路径
    * path：虚拟目录
    
    3. 在conf\Catalina\localhost创建任意名称的xml文件。在文件中编写
    <Context docBase="D:\hello" />
    * 虚拟目录：xml文件的名称
    ```

* 静态项目和动态项目：
				目录结构
					* java动态项目的目录结构：
						-- 项目的根目录
							-- WEB-INF目录：
								-- web.xml：web项目的核心配置文件
								-- classes目录：放置字节码文件的目录
								-- lib目录：放置依赖的jar包
		* 将Tomcat集成到IDEA中，并且创建JavaEE的项目，部署项目。