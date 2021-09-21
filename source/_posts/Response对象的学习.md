---
title: Response对象的学习
date: 2021-03-27 19:07:35
tags:
  - Javaweb
  - Response
categories:
  - 后端
  - javaweb
description:  Response对象的学习
---

## Response对象的学习

功能：设置响应消息
		1.设置响应行
			1.格式：HTTP/1.1 200 ok
			2.设置状态码：setStatus(int sc)
		2.设置响应头：setHeader(String name,String value)
		3.设置响应体：
			使用步骤
				1.获取输出流
					字符输出流：PrintWriter getwriter();
					字节输出流：ServletOutputStream getOutputStream()
				2.使用输出流，将数据输出到客户端浏览器
			

```java
重定向：资源跳转的方式
代码实现：
	1.设置状态码302，设置状态头location
		response.setStatus(302);
		response.setHeader("location",/"day15/responseDemo2");
	2.简单的重定向方法
		response.sendRedirect("/day15/responseDemo2");
重定向的特点：redirect
	1.地址栏发生变化
	2.重定向可以访问其他站点(服务器)的资源
	3.重定向是两次请求。不能使用request对象来共享资源
转发的特点：forward
	1.转发地址栏路径不变
	2.转发只能访问当前服务器下的资源
	3.转法师一次请求，可以使用request对象来共享数据

服务器输出字符/字节数据到浏览器
	字符：
		0.设置编码
		response.setContentType("text/html;charset=utf-8");
		1.获取字符输出流
		PrintWriter pw=response.getWriter();
		2.输出数据
		pw.Writer(String);
		
	字节
		0.设置编码
		response.setContentType("text/html;charset=utf-8");
		1.获取字节输出流
		SevletOutputStream sos=response.getOutputStream();
		2.sos.writer(字节流内容);
```