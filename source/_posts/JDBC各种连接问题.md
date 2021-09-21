---
title: JDBC各种连接问题
date: 2021-03-25 11:12:08
tags:
  - Java
  - JDBC
categories:
  - 后端
  - javaweb
description:  java通过JDBC连接数据库和c3p0数据库连接池，最常见的两个问题
---

### java通过JDBC连接数据库时，最常见的两个问题

 1. 数据库连接的驱动问题

    ​	随着mysql的更新在不同的mysql-connector-java  的jar包下JDBC的配置也发生了一些变化，可能会出现以下错误

    ​    Loading class `com.mysql.jdbc.Driver'. This is deprecated. The new driver class is `com.mysql.cj.jdbc.Driver'. 

    ​	从错误的提示信息不难看出，将原本的（6.0以下版本）

    ```java
    Class.forName("com.mysql.jdbc.Driver");
    ```

    改为新版的（6.0及以上版本)

    ```java
    Class.forName("com.mysql.cj.jdbc.Driver");
    ```

    即可解决问题。

    

    

2. 数据库连接的时区

    ​	同样，在数据库连接的过程中连接时区也经常容易出错发生以下异常：

    ​	java.sql.SQLException: The server time zone value '�й���׼ʱ��' is unrecognized or represents more than one time zone. 

    ​	这也是6.0及以上版本更新后出现的问题，只需要在mysqUrl后加上时区即可

    ​	将原本的

    ```java
    connection= DriverManager.getConnection("jdbc:mysql://localhost:3306/stusql","root","root");
    ```

    ​	加上时区信息  ?serverTimezone=UTC

    ```java
    connection= DriverManager.getConnection("jdbc:mysql://localhost:3306/stusql?serverTimezone=UTC","root","root");
    ```

    即可成功连接

    

## 同样在使用C3P0和Druid数据库连接池时，也可能会出现的异常

​	1. 在使用c3p0时

java.sql.SQLException: An attempt by a client to checkout a Connection has timed out.

也可能是因为在配置c3p0-config.xml连接参数时忽略了时区问题

将

```xml
<property name="driverClass">com.mysql.jdbc.Driver</property>   
<property name="jdbcUrl">jdbc:mysql://localhost:3306/stusql</property>
```

改为

```xml
<property name="driverClass">com.mysql.cj.jdbc.Driver</property>
<property name="jdbcUrl">jdbc:mysql://localhost:3306/stusql?serverTimezone=UTC</property>
```

即可正常运行。

 2. 在使用Druid时

    将

```properties
driverClassName=com.mysql.jdbc.Driver
url=jdbc:mysql://127.0.0.1:3306/stusql
```

​     改为

```properties
driverClassName=com.mysql.cj.jdbc.Driver
url=jdbc:mysql://127.0.0.1:3306/stusql?serverTimezone=UTC
```

即可正常运行