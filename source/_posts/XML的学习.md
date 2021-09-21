---
title: XML的学习
date: 2021-03-30 11:56:01
tags:
  - Javaweb
  - XML和Jsoup对象
categories:
  - 后端
  - javaweb
description:  XML和Jsoup对象的学习
---

# XML和Jsoup对象的学习

## XML

1. 概念：

    + 可扩展：标签都是自己定义的
    + 功能：存储数据 配置文件
    + 特点：自定义标签，语法严格，存储数据

2. 语法：

    + 后缀名： .xml
    + 第一行为文档声明
    + 有且仅有一个根标签
    + 属性必须使用引号括起来
    + 标签正确关闭
    + 区分大小写

3. 组成部分：

    + 文档声明：
        + 格式：<?xml 属性列表?>
        + 属性列表：
            + version：版本号  必须有
            + encoding：编码方式
            + standalone：是否独立  yes 独立  no  不独立
        + 属性：id属性值唯一
        + 文本CDATA区域会被原样展示  <![CDATA[数据]]>

4. 约束：

    + 分类：

        + DTD：一种简单的约束技术   .dtd
        + Schema：一种复杂的约束技术  .xsd

    + DTD：

        + 引入dtd文档到xml文档中
        + 内部dtd：将约束规则定义在xml文档中
        + 外部dtd：将约束的规则定义在外部的dtd文件中
        + 本地：<!DOCTYPE 根标签名 SYSTEM "dtd文件的位置">
        + 网络：<!DOCTYPE 根标签名 PUBLIC "dtd文件名字" "dtd文件的位置URL">

    + Schema:

        + 填写xml文档的根元素

        + 引入xsi前缀.  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"

        + 引入xsd文件命名空间.  xsi:schemaLocation="http://www.itcast.cn/xml  student.xsd"

        + 为每一个xsd约束声明一个前缀,作为标识  xmlns="http://www.itcast.cn/xml" 

            ```xml
            <students   xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            					xmlns="http://www.itcast.cn/xml"
            					xsi:schemaLocation="http://www.itcast.cn/xml  student.xsd">
            ```



## JAVA中的Jsoup类：解析html或者xml文件

1. Jsoup 获取document对象方法：

    ```java
    1.Jsoup.parse(file,"utf-8");   通过本地路径获取
    2.Jsoup.parse(url,time);	通过网络地址获取 
    3.Jsoup.parse(str)；	通过字符串获取   不常用
    ```

2. 通过document获取Elemenet对象

    ```java
    	通过document获取Element对象  （部分）
    		1.通过TagName
    			document.getElementsByTag("tagname");
    		2.通过属性名获取
    			document.getElementsByAttribute("name");
    		3.通过属性值获取
    			document.getElementsByAttributeValue("name","lisi");
    		4.通过id值获取
    			document.getElementById("value");
    ```

3. ELement 对象：

    ```java
        1.获取子元素
            1.通过TagName
            document.getElementsByTag("tagname");
            2.通过属性名获取
            document.getElementsByAttribute("name");
            3.通过属性值获取
            document.getElementsByAttributeValue("name","lisi");
            4.通过id值获取
            document.getElementById("value")
        2.获取属性值  .attr(key);
            String name=element.attr("name");
        3.获取文本内容
            String text=element.text();
            String html=element.html();
    ```

4. 快速查询方式：

    + Selector 选择器查询

        ```java
        element.select(cssQuery);
        ```

    + Xpath查询