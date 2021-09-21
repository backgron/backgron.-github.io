---
title: Express的学习
date: 2021-05-28 17:26:03
tags:
  - Nodejs
  - Express
categories:
  - 后端
  - Nodejs
description:  Express的学习
---

# Express

Express是基于Node.js平台，快速、开放、极简的Web开发框架

## 安装

在项目根目录下

```
npm i express

## 使用

### 基本使用

1. 导入  require()

    ```js
    const express = require('express');
```

2. 创建web服务器 express()

    ```js
    const app = express();
    ```

3. 调用 app.listen(端口号，启动成功后的回调函数)，启动服务器

    ```js
    app.listen(80,()=>{
        console.log();
    })
    ```

4. 监听GET请求 app.get()

    ```js
    app.get('请求url',function( req , res ){/* 处理函数 */})
    ```

5. 监听POST请求 app.post()

    ```js
    app.post('请求url',function( req , res ){/*处理函数*/})
    ```

6. 把内容响应给客户端   res.send();

    ```js
    res.send('相应内容');
    ```

7. 获取url中携带的查询参数  req.query;

    ```js
    req.query;
    
    req,query 默认为一个空对象
    客户端使用 ?name=zs&age=20 发送参数后
    可以通过 req.query.name 访问到
    ```

8. 获取url中的动态参数  req.params

    ```js
    app.get('/user/:id/:name', (req, res) => {
        res.send(req.params);
    });
    
    req.params 默认为一个空对象
    里面存放着通过 : 动态匹配到的参数
    ```

9. 托管静态资源 express.static()

    ```js
    express.static('托管目录')app.use(express.static('./public'))// 127.0.0.1/index.html创建一个静态资源服务器将 public 目录下的图片，css文件、js文件对外开放访问Express 在指定的静态目录中找插文件，并对外提供资源的访问路径。因此，存放静态文件的目录名不会出现在url中如果前面加挂在路径前缀，访问需要加上路径app.use('public',express.static('./public'));// 127.0.0.1/public/index.html托管多个静态资源时，会按照从上到下的顺序一次寻找
    ```

## 路由 / 映射关系

```js
app.post('url',function(){});app.get('url',function(){});1. 按照定义的先后顺序匹配2. 只有url和请求类型同时匹配成功才会调用对应的处理函数
```

### 路由模块化

1. 创建路由模块对应的.js文件，引入express模块

    ```js
    const express = require('express');
    ```

2. 调用express.Router()函数创建路由对象

    ```js
    const router = express.Router();
    ```

3. 向路由对象挂在具体的路由

    ```js
    router.get();router.post();
    ```

4. 使用module.exports 向外共享路由对象

    ```js
    module.exports = router;
    ```

5. 使用路由模块

    ```js
    1. 导入路由模块const router = require('./router');2. 注册路由模块app.use(router);使用app.use() 注册路由，可以添加访问前缀app.use('/api',router);
    ```

## 中间件

### 基本信息

1. 特指业务流程的中间环节
2. 当一个请求到达 Express 的服务器之后，可以连续调用多个中间件，从而对这次请求进行预处理。

### 创建中间件

1. Express 的中间件本质上就是一个function 处理函数，但是中间件的形参中必须要包括一个next()函数，而路由只包括req和res

    ```js
    app.get('/',function(req,res,next){    next();})
    ```

2. next()函数的作用

    + 实现多个中间件连续调用的关键，表示把流转关系转交给下一个中间件或者路由

3. 全局生效的中间件

    + 客户端发送的任何请求，到达服务器之后，都会触发的中间件，叫做全局生效的中间件
    + 通过app.use(中间件函数),可以定义一个全局生效的中间件

    ```js
    const mw = function(req,res,next){    console.log('中间件');    next();}//全局生效的中间件app.use(mw);简化：app.use(function(req,res,next){    console.log('中间件');    next();})
    ```

### 中间件的作用

1. 多个中间件之间，共享同一分req和res，基于这样的特性，我们可以在上游的中间件中，统一为req或res对象添加自定义的属性或者方法，供下游中间件或路由使用。

2. 通过app.use()连续定义多个全局中间件时，会按照定义的先后顺序调用 

3. 局部中间件：不适用app.use()定义的中间件，叫做局部生效的中间件

    ```js
    //定义中间件函数 mw1const mw1=function(req,res,next){    console.log('这是中间件函数');    next();}//mw1 这个中间件只在‘当前路由中生效’ ，即局部生效的中间件app.get('/',mw1,function(req,res){    res.send('Home Page');})// mv1 不会影响下面的路由app.get('/user',function(req,res){res.send('User Page')});
    ```

4. 多个局部中间件

    ```js
    //  以下两种写法是完全等价的app.get('/',mw1,mw2,(req,res)=>{    res.send('Home page');});app.get('/',[mw1,mw2],(req,res)=>{    res.send('Home page');});
    ```

#### 注意事项

1. 一定要在路由之前注册中间件
2. 客户端发送过来的请求，可以连续调用多个中间件处理
3. 执行完中间件的业务代码之后，不要忘记调用next()函数
4. 为了防止代码逻辑混乱，调用next()之后不要再写额外的代码
5. 连续调用多个中间件时，多个中间件之间共享req和res对象

#### 中间件分类

1. 应用级别的中间件

    + 通过app.use()  app.get()  app.post()，绑定到app实例上的中间件，叫应用级别的中间件

2. 路由级别的中间件

    + 绑定到express.Router() 实例上的中间件，叫做路由级别的中间件它的用法和应用级别的中间件没有区别

3. 错误级别的中间件

    + 用来捕获整个项目中发生的异常错误，从而防止项目有异常崩溃的问题

    + 错误级别中间件的function处理函数中必须有四个参数，分别为(err,req,res,next);

        ```js
        //抛出一个自定义的错误app.get('/',function(req,res){    throw new Error('服务器内部发生了错误');    res.send('Home page');})//错误级别的中间件//在服务器打印错误消息//向客户端相应错误相关的内容app.use(function(err,req,res,next){    console.log('发生了错误'+err.message);    res.send('Error'+err.message);})
        ```

    + 错误级别的中间件一定要注册到所有路由之后

4. Express 内置的中间件

    + Express 4.16.0 版本开始，内置了3个常用的中间件

    + express.static  快速托管静态资源

    + express.json  解析json格式的请求体数据

        ```js
        app.use(express.json());
        ```

    + express.urlencoded  解析url-encode格式的请求体数据

        ```js	
        app.use(express.urlencoded({extended:false}));
        ```

5. 第三方的中间件

    + 第三方开发出来的中间件
    + npm install 名称   安装
    + require  导入
    + app.use()  注册并使用

### cors解决跨域问题

1. 安装cors中间件

    + npm i cors

2. 在路由之前，配置cors

    + const cors=require('cors');
    + app.use(cors());

3. 设置跨域请求 cors 响应头   Access-Control-Allow-Origin

    + res.setHeader('Access-Control-Allow-Origin','url');


## mysql模块

1. 安装

    + npm i mysql

2. 配置mysql 模块

    ```js
    const mysql = require('mysql');const db = mysql.createPool({    host:'127.0.0.1',   //IP地址    user:'root',		// 账号    password:'root',	//密码    database:'my_db_01' // 数据库名})
    ```

3. 使用SELECT语句查询数据

    ```js
    const sqlStr = 'select * from student';db.query(sqlStr,(err,results)=>{    if(err) return console.log(err.message);    console.log(results);})
    ```

4. 插入数据

    ```js
    const stu = {id:3 , name:'xiaohong'};const sqlStr = 'insert into student(id,name) values(?,?)';db.query(sqlStr,[stu.id,stu.name],(err,results)=>{    if(err) return console.log(err.message);    if(results.affectedRows === 1){console.log('成功')}})；//直接插入对象const stu = {id:3 , name:'xiaohong'};const sqlStr = 'insert into student set ?';db.query(sqlStr,stu,(err,results)=>{    if(err) return console.log(err.message);    if(results.affectedRows === 1){console.log('成功')}})；
    ```

5. 更新数据

    ```js
    const stu = {id:3 , name:'xiaohong'};const sqlStr = 'update student set id=?,name=? where  id=?';db.query(sqlStr,[stu.id,stu.name,stu.id],(err,results)=>{    if(err) return console.log(err.message);    if(results.affectedRows === 1){console.log('成功')}})；//直接更新对象const stu = {id:3 , name:'xiaohong'};const sqlStr = 'update student set ? where  id=?';db.query(sqlStr , [stu , stu.id] ,(err,results)=>{    if(err) return console.log(err.message);    if(results.affectedRows === 1){console.log('成功')}})；
    ```

6. 删除数据

    ```js
    const sqlStr = 'delete from student where id=?';db.query(sqlStr , 6 ,(err,results)=>{    if(err) return console.log(err.message);    if(results.affectedRows === 1){console.log('成功')}})；
    ```

    
