---
title: BeanUtils的使用
date: 2021-03-27 09:10:10
tags:
  - Java
  - JDBC
  - BeanUtils
categories:
  - 后端
  - javaweb
description:  BeanUtils的简单使用
---

## BeanUtils 的简单实用和出现的问题

首先，今天学习的是apache包下的BeanUtils，今天因为导包错误，导入Spring包下的BeanUtils而找不到BeanUtils.populate(user,map)方法需要注意一下



BeanUtils工具类  简化数据封装
	用于封装JavaBean的
	1.JavaBean： 标准的Java类
		要求：
			类必须被public修饰
			必须提供空参的构造函数
			成员变量必须使用private修饰
			提供给公共的getter和setter方法
		功能： 封装数据
	

```java
概念：
	成员变量：private String name;
	属性： setter和getter建方法截取后的产物
		例如： getName()->Name->name

方法：
	1.setProperty();
	2.getProperty();
	3.populate(Object obj,Map map)  将map集合键值对信息封装为JavaBean对象
```
```java
        //1  获取Map集合
        Map<String,String[]> map=req.getParameterMap();
        //2  调用BeanUtil
        User user=new User();
        try {
            BeanUtils.populate(user,map);
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        } catch (InvocationTargetException e) {
            e.printStackTrace();
        }
```