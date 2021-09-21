---
title: Nodejs和npm学习
date: 2021-05-23 18:17:19
tags:
  - Nodejs
categories:
  - 后端
  - Nodejs
description:  Nodejs和npm学习
---

# Node.js

## 基本信息

 	1. Node.js 是基于Chrome V8引擎的JavaScript运行环境。
 	 + 浏览器是JavaScript的前端运行环境
 	 + Node.js是JavaScript的后端运行环境
 	 + Node.js中无法调用和DOM和BOM等浏览器内置API

2. Node.js可以做什么
    + Node.js作为一个JavaScript的运行环境，仅仅提供了基础的功能和API
    + 基于Express框架，可以快速构建Web应用
    + 基于Electron框架，可以快速构建跨平台的桌面应用
    + 基于restify框架，可以快速构建API接口项目
    + 读写和操作数据库、创建使用的命令行工具等。。

## fs 文件系统模块

fs模块是Node.js官方提供的、用来操作文件的模块

```js
const fs = require('fs');
```

### fs.readFile()

```js
fs.readFile(path[,options],function(err,dataStr){ });

path:读取文件的存放路径
options:读取文件时候采用的编码格式，一般使用 utf8
function: 回调函数，拿到读取失败和成功的结果 err / dataStr
如果成功 err 的值为 null ，dataStr为成功结果
如果读取失败， err 的值为错误对象 dataStr的值为undefined
```

### fs.writeFile()

```js
fs.writeFile(file,data[,options],function(err){})

file:路径
data:写入内容
option: 编码
function:回调函数
```

### 路径动态拼接问题

1. 代码在运行的时候，会执行node命令所处的目录，动态拼接处被操作文件的完整目录，很可能出现路径动态拼接错误的问题

2. 解决办法：

    ```js
    不要使用相对路径
    __dirname 表示当前文件所处的目录
    
    fs.readFile(__dirname+'/flie/1.txt','utf8',function(){]});
    ```

## path 路径模块

path模块是Node.js官方提供的、用来处理路径的模块。

```js
const path = require('path')
```

### path.join()

通过path.join()，可以把多个路径片段拼接为完整的路径字符串

```js
path.join([...paths]);

path.join('/a','/b/c','../','./d','e');
//  \a\b\d\e   ../会抵消一层路径
const pathStr=path.join(__dirname,'./files/1.txt');
以后凡是涉及到路径拼接的操作，都要使用path.join() 不能直接+
```

### path.basename()

通过path.basename()，可以从文件路径中获取文件名的部分

```js
const fpath = 'a/b/c/index.html';
path.basename(fpath);  //返回index.html
path.basename(fpath,'.html'); //返回 index
```

### path.extname()

通过path.extname()，可以获取文件路径中的扩展名部分

```js
path.extname(path);
```

## http模块

http模块是Node.js官方提供、用来创建web服务器的模块，通过http模块提供的http.createServer()方法，技能很方便地把一台普通的电脑变成一台web服务器

```js
const http = require('http');
```

### 创建最基本的web服务器

```js
const server = http.createServer();// 使用服.on()方法为服务器绑定一个request事件server.on('request',(req,res)=>{    console.log('someone visit this server');});//启用web服务器server.listen(80,()=>{    console.log('http server running at http://127.0.0.1');})
```

### req 请求对象

1. req.url 是客户端请求的url地址
    + req.url
2. req.method 是客户端请求的method类型
    + req.method

### res 响应对象

1. res.end(str) 可以向客户端响应一些内容
    + res.end(str);
2. res.setHeader(),设置响应回去的编码格式
    + res.setHeader('Content-Type','text/html;charset=utf-8');

## Node.js 中的模块化

### 基本信息

1. 模块作用域
    + 只能在当前模块内被访问
2. CommonJS的规范
    + 每个模块内部，module变量代表当前模块
    + module变量是一个对象，它的exports属性是对外的接口
    + 加载某个模块时，加载的其实是改模块的module.exports属性，require() 方法用于加载模块

### require(),

```js
1. 加载内置的fs模块const fs = require('fs');2. 加载用户的自定义模块const custom = require('./custom.js');  //可以省略 .js3. 加载第三方模块  需要先下载const moment = require('moment');!使用require() 方法加载其他模块时，会执行被加载模块中的代码
```

### module 对象

1. modle对象
    + 每个.js自定义模块中都有一个module对象，它里面存储了和当前模块有关的信息
2. module.exports 对象
    + 在自定义模块中，可以使用module.exports对象，将模块内的成员共享出去，供外界使用
    + 外界用require()方法导入自定义模块时，得到的就是module.exports所指向的对象
3. exports 对象
    + 默认情况下 exports 和 module.exports 指向的时同一个对象
    + 最终共享的对象还是以 module.exports 为准
4. 注意
    + 如果 通过 = 将exports 或者 module.exports 指向新的对象，则它们就不相同了，且最后require() 以module.exports为准

## npm与包

### 包

1. Node.js 中的第三方模块又叫做 包
2. 可以通过 npm 下载包

### npm

npm 为包的管理工具

1. 在项目中安装包的命令
    + npm install 完整的包名
    + npm i 完整的包名
    + npm i 完整的包名@版本号
        + 包的语义化版本规范
        + 总共有三位十进制数字
        + 第一位数字：大版本
        + 第二位数字：功能版本
        + 第三位数字：bug修复版本
        + 只要前面版本号增长了，后面的版本号归零
2. 卸载包
    + npm uninstall 完整的包名
    + 卸载后也会在配置文件中删除独赢的信息
3. node_modules 文件夹
    + 用来存放所有已安装到项目中的包
    + require() 就时从这个目录找第三方包的
4. package-lock.json 配置文件
    + 用来记录node_modules 目录下每一个包的下载信息

### 包管理配置文件

npm规定，在项目根目录中，必须提供一个焦作package.json的包管理配置文件，用来记录与项目有关的配置信息

如：

+ 项目的名称、版本号、描述等
+ 项目中都用到了那些包
+ 那些包只在开发时间会用到
+ 那些包在开发和部署时都会用到 

注意：在今后项目开发中，一定要把node_modules文件夹添加到.gitignore忽略文件中。通过项目根目录创建的package.json来记录安装了那些包

1. 快速创建package.json
    + npm init -y
    + 在执行命令所处的目录中，创建package.json
    + 上述命令只能在英文目录下运行成功，所以项目文件夹的名称一定要使用英文命名
    + 运行npm install命令安装包时，npm会自动把包的名称和版本号记录到package.json中

2. dependencies 节点
    + 在package.json中，有一个dependencies 节点，专门用来记录您使用npm install命令安装了哪些包
    + npm install  一次性安装package.json 中dependencies 中的所有包

3. devDependencies 节点
    + npm i 包名 -D
    + npm install 包名 --save-dev
    + 建议将只在项目开发阶段会用到的包记录到devDependenci中

### npm镜像服务器 和 nrm

1. 淘宝 NPM 镜像服务器
    + 查看当前的下包镜像源
        + npm config get registry
    + 将下包镜像源切换为淘宝镜像源
        + npm config set registry=https://registry.npm.taobao.org/
    + 检查镜像源是否下载成功
        + npm config get registry
2. 通过 nrm 方便切换下包镜像源
    + 通过npm 包管理器，将nrm安装为全局可用的工具
        + npm i nrm -g
    + 查看所有可用的惊现管
        + nrm ls
    + 将下包的镜像源切换为taobao 镜像
        + nrm use taobao

### 包的分类

1. 项目包  被安装到node_modules目录中的包都是项目包
    + 开发依赖包  只在开发期间会用到，被记录到devDependencies节点
        + npm i 包名 -D
    + 核心依赖包 在开发和上线之后都会用到，被记录到dependencies节点
        + npm i 包名
2. 全局包  在npm i 时提供了参数-g
    + npm i 包名 -g
    + npm uninstall 包名 -g
    + 只有工具性质的包，才有必要全局安装，因为它们提供了好用的终端命令
    + 可以参考观法提供的使用说明

### i5ting_toc 包

i5ting_toc 是一个可以把md文档转换为html页面的小工具

1. 将 i5ting_toc 安装为全局包
    + npm install -g i5ting_toc
2. 调用 i5ting_toc,轻松是按 md 转 html 的功能
    + i5ting_toc -f 要转换的md文件路径 -o

### 规范的包结构

1. 包必须以单独的目录而存在
2. 包的顶级目录下必须包含package.json 配置文件
3. package.json 中必须包含 name 、version、main这三个属性，分别代表包的名字、版本号、包的入口

### 发布一个自己的包

1. 在终端登录npm
    + npm login
    + 输入用户名和密码
2. 发布npm包
    + 将路径换位包的根目录
    + npm publish
3. 删除一个包（72小时以内发布的）
    + npm unpublish 包名 --force