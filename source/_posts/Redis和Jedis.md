---
title: Redis和Jedis
date: 2021-04-10 16:58:02
tags:
  - Javaweb
  - Redis和Jedis
categories:
  - 数据库
  - redis
description:  Redis和Jedis
---

# Redis和Jedis

## Redis

### 概念

Redis是一款高性能的NOSQL系列的非关系型数据库

NOSQL系列数据库：存储在缓存中(内存)

+ 成本低、查询速度快、存储格式为键值对(key,value)、扩展性高
+ 维护的工具和资料有限、不提供对sql的支持、不提供事务的处理

关系型数据库和NOSQL数据库并非对立而是互补的关系，即通常情况下使用关系型数据库，在适合的时候使用NOSQL时使用NOSQL数据库，一般在NOSQL数据库中备份存储关系型数据库的数据

### 主流的NOSQL产品

•	键值(Key-Value)存储数据库
				相关产品： Tokyo Cabinet/Tyrant、Redis、Voldemort、Berkeley DB
				典型应用： 内容缓存，主要用于处理大量数据的高访问负载。 
				数据模型： 一系列键值对
				优势： 快速查询
				劣势： 存储的数据缺少结构化
		•	列存储数据库
				相关产品：Cassandra, HBase, Riak
				典型应用：分布式的文件系统
				数据模型：以列簇式存储，将同一列数据存在一起
				优势：查找速度快，可扩展性强，更容易进行分布式扩展
				劣势：功能相对局限
		•	文档型数据库
				相关产品：CouchDB、MongoDB
				典型应用：Web应用（与Key-Value类似，Value是结构化的）
				数据模型： 一系列键值对
				优势：数据结构要求不严格
				劣势： 查询性能不高，而且缺乏统一的查询语法
		•	图形(Graph)数据库
				相关数据库：Neo4J、InfoGrid、Infinite Graph
				典型应用：社交网络
				数据模型：图结构
				优势：利用图结构相关算法。
				劣势：需要对整个图做计算才能得出结果，不容易做分布式的集群方案。

### Redis

Redis是用C语言开发的一个开源的高性能键值对（key-value）数据库，官方提供测试数据，50个并发执行100000个请求,读的速度是110000次/s,写的速度是81000次/s ，且Redis通过提供多种键值数据类型来适应不同场景下的存储需求，目前为止Redis支持的键值数据类型如下：

1. 字符串类型 string
2. 哈希类型 hash：map格式（键值对）
3. 列表类型 list：linkedlist格式，支持重复元素
4. 集合类型 set：不允许重复元素
5. 有序集合类型 sortedset：不允许重复元素，且元素有序

redis的应用场景：

1. 缓存（数据查询、短链接、欣慰内容、商品内容等）
2. 聊天室的在线好友列表
3. 任务队列（秒杀、抢购、12306）
4. 应用排行榜
5. 网站访问统计
6. 数据过期处理
7. 分布式集群架构的session分离

命令操作：

1. 字符串类型 string：
    + 存储：set key value
    + 获取：get key
    + 删除：del key
2. 哈希类型 hash：
    + 存储：hset key field value
    + 获取：hget key field
    + 获取所有field和value：hgetall key
    + 删除：hdel key field
3. 列表类型 list：
    + 头部添加：lpush key value
    + 尾部添加：rpush key value
    + 获取：lrange key start end
    + 头部删除：lpop key：删除头部元素，并将元素返回
    + 删除尾部：rpop key：删除尾部元素，并将元素返回
4. 集合类型 set：
    + 存储：sadd key value
    + 获取：smembers key
    + 删除：srem key value
5. 有序集合类型 sortedset：
    + 存储：zadd key score value
    + 获取：zrange key start end [withscores]
    + 删除：zrem key value
6. 通用命令：
    + key *：查询所有的键
    + type key：获取键对应的value的类型
    + del key：删除指定的key value

 持久化：

+ RDB：默认方式，推荐使用
+ AOF：日志模式，不推荐使用

## JAVA客户端 Jedis

1. 下载和安装jedis的jar包

2. 使用：

    ```java
    Jedis jedis=new Jedis("localhost",6379);//创建
    jedis.close();//关闭
    ```

3. 操作各种类型：

    ```java
    1. 字符串string：
        jedis.set();
    	String str=jedis.get();
    	jedis.setex();
    2. 哈希类型
        jedis.hset();
    	String str=jedis.hget();
    	Map<String,String> map=jedis.hgetAll();
    3. 列表类型
        jedis.lpush();
    	jedis.rpush();
    	String lp=jedis.lpop();
    	String rp=jedis.rpop();
    	List<String> list=jedis.lrange("list",0,-1);
    4. 集合类型：
        jedis.sadd();
    	Set<String> set=jedis.smembers();
    5. 有序集合类型
        jedis.zadd();
    	Set<String> set=jedis.zrange();
    ```

4. jedis连接池：JedisPool

    + 使用：

        1. 创建连接池对象JedisPool
        2. 调用getResource()方法获取Jedis连接
        3. jedis.close()归还连接池

    + 工具类：

        ```java
        public class JedisPoolUtils {
        
        			    private static JedisPool jedisPool;
        			
        			    static{
        			        //读取配置文件
        			        InputStream is = JedisPoolUtils.class.getClassLoader().getResourceAsStream("jedis.properties");
        			        //创建Properties对象
        			        Properties pro = new Properties();
        			        //关联文件
        			        try {
        			            pro.load(is);
        			        } catch (IOException e) {
        			            e.printStackTrace();
        			        }
        			        //获取数据，设置到JedisPoolConfig中
        			        JedisPoolConfig config = new JedisPoolConfig();
        			        config.setMaxTotal(Integer.parseInt(pro.getProperty("maxTotal")));
        			        config.setMaxIdle(Integer.parseInt(pro.getProperty("maxIdle")));
        			
        			        //初始化JedisPool
        			        jedisPool = new JedisPool(config,pro.getProperty("host"),Integer.parseInt(pro.getProperty("port")));
                        }
          			    /**
        			     * 获取连接方法
        			     */
        			    public static Jedis getJedis(){
        			        return jedisPool.getResource();
        			    }
        			}  
        ```

        

