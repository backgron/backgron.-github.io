---
title: Mysql的学习
date: 2021-04-22 22:56:54
tags:
  - Mysql
categories:
  - 数据库
  - mysql
description:  Mysql的学习
---

```mysql
查询：
	selct 字段,字段 from 表 where 条件;
	
分组函数/多行处理函数：
	sum min max avg count;        group by
	例：select max(sal) from emp;
	    select max(sal) from emp group by job;
	分组函数通常与group by 连用并且后于group by后运行
	分组函数自动忽略空；
	
排序(order by):
	order by 		desc(降序)  asc(升序)  默认升序；
	例：select sal from emp order by sal desc;
	
去重(distinct):
	select distinct job from emp;
	select distinct job,deptno from emp;
	
	
	
	

	顺序：
	select 			5
		..
	from    		1
		..
	where			2
		..
	group by		3
		..
	having 			4
		..
	order by		6
		..
	limit			7
		..			

表连接:

	内连接：
		select
			..
		from
			..
		join
			..
		on
			..
		
	外连接:
		select
			..
		from
			..
		left join
			..
		on
			..
		right join
			..
		on
			..

子查询：
	select
		..(select).
	from 
		..(select).
	where
		..(select).
		
		
union链接:
	将两个查询结果相加，需要列数相同
	select ename from emp
	union
	select ename from emp;

limit(分页查询):
	limit是mysql中特有的
	limit取结果集中的部分数据(是sql语句最后执行的一个环节)
	limit startIndex,length
		startIndex(表示其实位置) length(表示取出几个)

	例：select ename,sal from emp order by sal desc limit 0,5;

limit(通用的标准分页sql)

每页显示3条记录：
第一页：0，3
第二页: 3, 3
第三页: 6, 3
第四页: 9, 3
	...
第n页，：(n-1)*3,3;




创建表：
	create table 表名(
		字段1，数据类型，
		字段2，数据类型，
		字段3，数据类型，
		..
		字段n，数据类型
		);

	mysql数据类型:
		int			整数型(java 中的 int)
		bigint		长整型(java 中的 long)
		float		浮点型(java 中的 float double)
		double
		char		定长字符串(java 中的 String)
		varchar		可变长字符串(java 中的 StringBuffer/Stringbuilder)
		date		日期类型(java 中的java.sql.data)
		BLOB		二进制大对象(存储图片，视频等流媒体信息) Binary Large Object
		CLOB		字符型大对象(存储较大文本，如4个G的字符串)Character Large Object


insert语句插入数据
	语法模式：
		insert into 表名(字段1，字段2，字段3...)values(值1，值2，值3);
		insert into 表名 values(值1，值2，值3) 值得顺序和数量必须和建表时相同
		insert into 表名(字段1，字段2，字段3...)values(值1，值2，值3...),(值1，值2，值3...);
	要求:字段的数量和值的数量相同，并且数据类型要对应相同
	当一条insert执行成功时，表格当中必然会多出一行记录；
	
表的复制
	语法：
		create table 表名 as select语句;
	将查询结果当作表创建出来
	

	将查询结果插入一张表中
		insert into dept1 select * from dept;   将dept 插入dept1 中

修改表中数据
	语法：
		update 表名 set 字段=值，字段=值 where 条件;  ！！如果不加where条件，则修改全部数据
		
删除数据
	语法:
		delete from 表名 where 条件;	如果不加where条件，则全部删除

	删除大表中的数据
		truncate table 表名；   无法恢复


​		
​		
约束：
​	非空约束（not nul)  不能为null  只有列级
​			id int not null;
​			

	唯一约束（unique）	不能重复，可以为null	
			username unique;   列级
			unique(id,username);  表级  id和username不能同时重复
			
	主键约束（primary key）（PK）	既不能为null 也不能重复 一个表只能有一个
			id int primary key;
			
		主键：
			主键约束： primary key
			主键字段： id 是主键字段
			主键值：   id 的每一个值都是主键值
		主键的作用：
			表的设计三范式中，第一范式就要求任何一张表都应该有主键
			主键的作用：主键值是这行记录在这张表中的唯一标识
		
		主键的分类：
			根据主键字段的字段数量来分：
				单一主键： 推荐的，常用的
				复合主键：多个字段联合起来添加一个主键约束（不推荐使用，违背三范式
			根据主键性质来分：
				自然主键：主键值最好是一个和业务没有任何关系的自然数(推荐)
				业务主键：主键值和系统的业务挂钩 如银行卡号，身份证号（不推荐用）
			
		！！！一张表的主键约束只能有一个

!!!		*mysql 提供主键自增:   auto_increment;  id字段自动维护一个自增的数字,从1开始,加1递增
			id int primary key auto_increment
				

	外键约束（foreign key）（FK）
		外键约束：foreign key
		外键字段：添加有外键约束的字段
		外键值：外键字段中的每一个值
		外键约束可以为空，引用的字段必须有唯一性，一般引用为主键
		
	检查约束（check）： oracle有，mysql无

备份数据库：

mysqldump -uroot -proot db1 >c://a.sql  备份
source c://a.sql  还原


事务：
	start transaction;  开始
	rollback;			回滚	
	commit;				提交
隔离级别：
read uncommitted; 读未提交——脏读、幻读、不可重复读
read committed;   读已提交--不可重复读、幻读
repeatable read;  可重复度--幻读
serializable;     串行化，锁表  没有问题
查询隔离级别：
	select @@tx_isolation;
设置隔离界别:
	set global transaction isolation level 隔离界别;
	
DCL：
  创建用户：
		create user '用户名’@‘主机名' identified by '密码';
  查询用户：
		1、进入mysql 数据库   use myql;
		2、查询用户：		  select * from user;
  删除用户：
		drop user “用户名”@“主机名”;
  修改用户名密码：
		修改语句：update user set password=password("新密码") where user="用户名";
		DCL语句： set password for "用户名"@"主机名" =password("新密码");
  忘记root用户密码：
		1.管理员运行cmd输入  net stop mysql  停止mysql服务
		2.使用无验证方式启动mysql服务: mysqld --skip-grant-tables
		3.打开新的cmd窗口输入mysql直接登录 进入mysql数据库修改root用户密码
		4.关闭两个窗口，通过任务管理器结束mysqld.exe进程
		5.cmd启动mysql服务：  net start mysql
		6.可以使用新密码登录了

权限管理:
	1、查询用户权限：
		show grant from "用户名"@"主机名";
	2、授予权限:
		grant 权限列表 on 数据库名.表名 to "用户名"@"主机名";
	    授予全部权限： grant all on *.* to "用户名"@"主机名";
	3、撤销权限：
		revoke 权限列表 on 数据库名.表名 from "用户名"@"主机名":
```

​	
​	