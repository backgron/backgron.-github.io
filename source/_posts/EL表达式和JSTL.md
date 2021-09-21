---
title: EL表达式和JSTL
date: 2021-03-31 09:42:33
tags:
  - Javaweb
  - JSP
categories:
  - 后端
  - javaweb
description:  EL表达式和JSTL的学习
---

# EL表达式和JSTL



## EL表达式

1. 概念：Expression Language 表达式语言

2. 作用：替换和简化jsp页面中java代码的编写

3. 语法：${表达式}

4. 注意：jsp默认支持el表达式的。如果要忽略el表达式

    + 设置jsp中page指令中：isELIgnored=“true” 忽略当前jsp页面所偶的el表达式
    + \\${表达式} ：忽略当前这个el表达式

5. 使用：

    1. 运算：

        + 运算符：
            1. 算术运算符：+	-	*	/(div)	%(mod)
            2. 比较运算符：>  <   >=   <=   ==  !=
            3. 逻辑运算符：&&(and)  ||(or)  !(not)
            4. 空运算符：empty
                + 功能：用于判断字符串、集合、数组对象是否为null或者长度是否为0
                + ${empty list}：判断字符串、集合、数组对象是否为null或者长度为0
                + ${not empty str}：表示判断字符串、集合、数组对象是否为null 并且 长度>0

    2. 获取值

        1. el表达式只能从与对象中获取值

        2. 语法：

            + ${与名称.键名}：从指定域中获取指定键的值

                ```jsp
                1.pageScope--------->pageContext
                2.requestScope------>request
                3.sessionScope------>session
                4.applicationScope-->application(SerletContext)
                ```

            + ${键名}：表示依次从最小的域中查找是否有该键对应的值，直到找到为止

        3. 获取对象、List集合、Map集合的值

            1. 对象：${域名称.键名.属性名}
                + 本质上回去当调用对象的getter方法
            2. List集合：${域名称.键名[索引]}
            3. Map集合：
                + ${域名称.键名.key名称}
                + ${域名称.键名["key名称"]}

    3. 隐式对象：

        + el表达式中有11一个隐式对象

        + pageContext：

            + 获取jsp其他八个内置对象

                ```jsp
                ${pageContext.request.contextPath}：动态获取虚拟目录
                ```

                

## JSTL

1. 概念： JavaServer page Tag Library  JSP标准标签库
2. 作用：用于简化和替换jsp页面上的Java代码
3. 使用步骤：
    + 导入jstl相关jar包
    + 引入标签库：taglib指令  <%@ taglib %>
    + 使用标签
4. 常用的JSTL标签
    1. if：相当于java代码里的if语句
        + 属性：
            + test 必须属性，接受bolean表达式
            + 如果表达式为true，则显示if标签体内容，如果为false，则不显示标签体内容
        + 注意：
            + c:if 标签没有else情况，要想要else情况，可以再定义一个c:if 标签
    2. choose：相当于java代码switch语句
        + 使用choose标签声明	相当于switch声明
        + 使用when标签做判断	相当于case
        + 使用otherwise标签做其他情况的声明	相当于default
    3. foreach：相当于java中的for循环  可以完成重复操作  遍历容器
        + 完成重复操作：
            + begin：开始值
            + end：结束值
            + var：临时变量
            + step：步长
            + varStatus：循环状态对象
                + index：容器中元素的索引，从0开始
                + count：循环次数，从1开始
        + 遍历容器
            + items：容器对象
            + var：容器中元素的临时变量
            + varStatus：循环状态对象
                + index：容器中元素的索引，从0开始
                + count：循环次数，从1开始