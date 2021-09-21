---
title: MVC开发模式
date: 2021-03-30 09:08:42
tags:
  - MVC
categories:
  - 后端
description:  MVC开发模式的学习
---

# MVC框架 MVC开发模式

### jsp演变历史

1. 早期只有servlet，只能使用response输出标签数据，非常麻烦
2. 后来有了jsp，简化了servlet的开发，但是如果过度使用jsp，在jsp即写 大量的Java代码，又写html代码，造成难以维护，难以分工协作的不便
3. 再后来，Java的web开发借鉴了MVC开发模式，使得程序的设计更加合理

### MVC

1. M：Model--模型--JavaBean
    + 完成具体的业务操作，如：查询数据库，封装对象
2. V：View--视图--JSP
    + 展示数据
3. C：Controller--控制器--Servlet



MVC的优缺点：

+ 优点：
    1. 耦合性低，方便维护，有利于分工协作
    2. 重用性高
+ 缺点：
    1. 是项目架构变得复杂
    2. 对开发人员要求更高