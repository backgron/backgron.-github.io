---
title: AJAX学习
date: 2021-05-19 21:47:09
tags:
  - 前端
  - AJAX
categories:
  - 前端
  - javascript
description:  AJAX的学习
---

# AJAX

## JavaScript 原生方式实现ajax

1. 概念 

    + AJAX = Asynchronous JavaScript and XML（异步的 JavaScript 和 XML）。
    + AJAX 是与服务器交换数据并更新部分网页的艺术，在不重新加载整个页面的情况下。

2. 通过JavaScript原生方式实现ajax

    ```javascript
    // get方式
    var xhr=new XMLHttpRequest();
    xhr.open("GET","localhost/loging?username=zhangsan",true);
    xhr.send(null);
    xhr.onreadystatechange=function(){
        console.log(xhr.responseText);
    };
    // post方式
    var xhr=new XMLHttpRequest();
    xhr.open("POST","localhost/loging");
    xhr.setRequestHeader('Foo','Bar');  //可以设置响应体数据
    xhr.setRequestHeade("Content-Type","application/x-www-form-urlencoded"); //设置数据格式
    xhr.send("username=zhangsan");
    xhr.onreadystatechange=function(){
        console.log(xhr.responseText);
    }
    ```

3. xhr.readyState的四个状态

    - 0: 请求未初始化
    - 1: 服务器连接已建立
    - 2: 获得了响应头
    - 3: 请求体获取中
    - 4: 请求已完成，且响应已就绪

## JQuery方式实现ajax

1. 底层封装 （常用属性)

    ```javascript
    $.ajax({
        url:'testServlet',  //地址
        type:'post',  //请求方式
        data:{id:1},  //请求参数
        dataType:'json',  //响应参数理性,和data无关！！！
        success:function(){}, //成功的回调函数
        error:function(){},  //失败的回调函数
        complete:function(){}, //请求完成后的回调函数  无论成功失败
    });
    ```

    

2. 进一步封装（常用)

    ```javascript
    1. get方式
    $.get(url,{data:data},function(data){},'json');
    
    2. post方式
    $.post(url,{data:data},function(data){},'json');
    
    3. getJSON特殊方式
    $.getJSON(url,{data:data},function(data){});
    ```

## JQuery-AJAX load()方法

1. 通过load可以实现局部的页面数据交换，在不刷新整个页面的情况下更新页面部分内容

    ```javascript
    $(selector).load(URL,data,callback);
    
    1. $("#div1").load("demo_test.txt");
    2. $("#div1").load("demo_test.txt #p1");
    ```

## JQuery-AJAX  全局事件方法

```javascript
//全局ajax开始时
$(document).ajaxStart(function(){
    NProgress.start();   //进度条  NProgress库  需要引入对应的css文件和js文件
});
//全局ajax结束时
$(document).ajaxStop(function(){
    NProgress.done();
});
```

## JQuery 实现文件上传

```js
$.ajax({
    method:'post',
    url:'http://www.liulongbin.top:3006/api/upload/avatar',
    data:fd,
    // 不修改Content-Type 属性，使用FormData默认的Content-Type值
    contentType:false,
    // 不对FormData中的数据进行url编码，而是将FormDate数据鸳鸯发送到服务器
    processData:false,
    success:function(res){
        console.log(res);
    }
})
```

## axios 专注于网络数据请求的js库

axios 相比于 xhr更简单方便，相比于jq更轻量

### get请求

```js
axios.get('url',{params:{参数}}).then(callback);

var url="http://www.url.com";
var paramsObj={name:'zs',age:20};
axios.get(url,{params:paramsObj}).then(function(res){
    var result=res.data;
    console.log(res);
})
```

### post请求

```js
axios.post(url,paramsObj).then(function(){});
```

### 直接使用axios发送请求

```js
//  post请求
axios({
    method:'post',
    url:url,
    data{
    name:'zs',
    age:20}
}).then(callback);

//get请求
axios({
    method:'get',
    url:url,
    params:{
    name:'zs',
    age:20}
}).then(callback);
```



## 跨域请求问题

### 概念

跨域的安全限制都是对浏览器端来说的，服务器端是不存在跨域安全限制的。

浏览器的同源策略限制从一个源加载的文档或脚本与来自另一个源的资源进行交互。

如果协议，端口和主机对于两个页面是相同的，则两个页面具有相同的源，否则就是不同源的。

### 通过script标签实现跨域请求 Jsonp

通过script标签可以发送跨域请求，但要拿到数据必须通过回调函数，服务端需要返回

application/javascript 类型数据的一个函数调用，来调用客户端函数

为避免函数名重复可以给函数名加上   时间戳＋随机数

服务端：

``` java
response.setHeader("Content-Type", "application/javascript;charset=utf-8");
response.getWriter().write("foo("+json+")");
```

客户端：

```javascript
//通过创建script标签的方式发送跨域请求
var script = document.createElement("script");
script.src = "http://localhost/getUserDemoServlet?id=1";
//将script加入到body中
document.body.appendChild(script);
//通过响应调用
function foo(data) {
    console.log(data);
}
```

### JQuery的方式实现跨域请求

jquery会自动传入一个   callback=。。。的参数作为回调函数的函数名

客户端：

```javascript
//jquery中的jsonp
        $.ajax({
            url: 'http://localhost/getUserDemoServlet',
            dataType: 'jsonp',
            success: function(res) {
                console.log(res);

            }
        })
```

服务端：

```java
response.setHeader("Content-Type", "application/javascript;charset=utf-8");
String callbackName=request.getParameter("callback");
response.getWriter().write(callbackName+"("+json+")");
```

### 通过设置服务端设置响应头直接允许跨域访问

客户端只需要加一个响应头即可

```java
//  第二个参数为url地址   * 为通配符 
response.setHeader("Access-Control-Allow-Origin","*");
```

## XHR level2 新特性

### 设置http请求时间限制

```js
xhr.timeout = 3000;  //设置时限 ms
xhr.ontimeout = function(event){  //对应的回调函数
    alert("请求超时");
}
```

### FormDate对象管理表单数据

```js
//创建FormDate对象
var fd = new FormDate();
//手动为FormDate添加表单项
fd.append('username','张三');
fd.append('password','12345');
//发送数据
xhr.send(fd);  //和提交网页表单效果相同


//自动获取表单数据  需要通过submit  注意阻止submit的默认事项
var form = document.querySelector('form');
var fd = new FormDate(form);
```

### 显示文件上传进度

```js
xhr.upload.onprogress 事件

xhr.upload.onprogress = function(e){
    // e.lenghtComputable 是一个布尔值，表示上传资源是否具有可计算的长度
    if(e.lenghtComputable){
        //e.loaded 已传字节
        //e.total  总字节
        var percentComplete = Math.cell((e.loaded / e.total)*100);
    }
}
```

## 其他

### 防抖

```js
以keyup发送请求为例

// 输入框防抖  减少发送多余的请求
var timer=null;
function debounceSearch(keywords){
    timer = setTimeout(function(){
        getSuggestList(keyword);  //延迟500毫秒发送请求
    },500);
}

$('#ipt').on('keyup',function(){
   clearTimeout(timer);  // 两次延迟小于500  清除上一次的timer
    ...
    debounceSearch(keywords);
})
```

### 节流

```js
节流阀为空，可以执行操作，节流阀不为空，不执行
执行完当前操作后将节流阀重置为空
执行前判断节流阀是否为空


以图片跟随鼠标为例
$(function(){
    var angel=$('#angel');
    var timer=null;  //定义一个timer节流阀
    $(document).on('mousemove',function(e){
        if(timer){
            return；//节流阀不为空，不执行
        }
        timer=setTimeout(function(){
            $(angel).css('left',e.pageX + 'px').css('top',e.pageY + 'px');
            timer=null; //执行结束，重置节流阀
        });
    },16);
})
```

### 防抖和节流的区别

+ 防抖：如果事件被频繁触发，防抖能保证只有最后一次触发生效！前面N多次的触发都会被忽略
+ 节流：如果事件被频繁触发，节流能够减少事件触发的频率，因此，节流是具有选择性的执行一部分事件