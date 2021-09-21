---
title: Request的学习
date: 2021-03-27 09:18:20
tags:
  - Javaweb
  - Request
categories:
  - 后端
  - javaweb
description:  Request对象的学习
---

## Request对象的学习

Request：
	1.request对象和response对象的原理
		request和response对象是由服务器创建的，我们来使用他们
		request对象是来获取请求消息的，response对象是来设置相应消息的
	

```java
2.request 对象继承体系结构：
	ServletRequest   -- 接口
		|继承
	HttpServletRequest  --接口
		|实现
	org.apache.catalina.connector.RequestFacade类 (tomcat)

3.request功能
	1.获取请求消息数据
		1.获取请求行数据
			GET / day14/demo1?name=zhangsan HTTP/1.1
			方法：
			1. 获取请求方式  GET
				String getMethod();
			2.(*) 获取虚拟目录： /day14
				String getContextPath();
			3. 获取Servlet路径:  /demo1
				String getServletPath();
			4. 获取get方式请求参数:  name=zhangsan
				String getQueryString();
			5.(*) 获取URI：
				String getRequestURI();  /day14/demo1
				StringBuffer getRequestURL  http://localhost/day14/demo1
			
				URL: 统一资源定位符
				URI: 统一资源标识符
			6. 获取协议及版本： HTTP/1.1
				String getProtocol();
			7. 获取客户机的IP地址：
				String getRemoteAddr();
				
2. 获取请求头数据
	(*) String getHeader(String):通过请求头名称获取请求头的值
		Enumeration<String getHeaderNames();  获取所有的请求头名称

3.获取请求体的方法 只有POST 有请求体
	1.获取流对象
		BufferedReader getReader();  获取字符流，只能操作字符数据
		ServletInputStream getInputStream(); 获取字节流 可以操作任何数据
	2.再从流对象种拿数据

2.其他功能：重要
	1.获取请求参数通用方式：不论是get还是post都可以用
		String getParameter(String name)  根据参数名称获取参数值
		String[] getParameterValues(String name);  根据参数名称获取参数值的数组
		Enumeration<String> getParameterNames(); 获取所有请求的参数名称
		Map<String,String[]> getParameterMap();  获取所有参数的map集合
	
		中文乱码问题 
			get: tomcat 8 已经解决了get的乱码问题
			post： 咋获取参数前设置request的编码
					request.setCharacterEncoding("utf-8");

4.请求转发：一种在服务器内部的资源跳转方式
	1.步骤：
		通过request对象获取请求转发器对象：RequestDispatcher getRequestDispatcher(String path)
		使用RequestDispatcher对象来进行转发: forward(ServletRequest request,ServletResponse response)
		
	2.特点：
		浏览器地址栏路径不发生变化
		只能转发到当前服务器内部资源中
		只请求一次
		
6.共享数据：
	域对象：一个有作用范围的对象，可以在范围内共享数据
	request域：代表一次请求的范围，一般用于请求转发的多个资源中共享数据
	方法：
		void setAttribute(String name,Object obj)存储数据
		Object getAttribute(String name)
		void removeAttribute(String name)
```