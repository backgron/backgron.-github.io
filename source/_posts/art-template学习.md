---
title: art-template学习
date: 2021-05-19 18:07:11
tags:
  - 前端
  - AJAX
  -  art-template 模板引擎
categories:
  - 前端
  - art-template 模板渲染引擎
description:   art-template 模板引擎
---

# art-template 模板引擎

## 基本使用

```html
// 引入文件
<script src="template-web.js"></script>
// 设置模板
<script type="text/x-art-template" id="temp1">
    {{each comments}}
    <tr>
        <td>{{$value.id}}</td>
        <td>{{$value.name}}</td>
        <td>{{$value.age}}</td>
    </tr>
    {{/each}}
</script>
// 调用模板
<script>
    $.psot("getUserServlet",{},function(data){
        var com={comments:data};
        var html=template('temp1',com);
        document.getElementById("dv").innerHTML=html;
    },'json');
</script>
```

## 核心方法

```javascript
// 基于模板名渲染模板
template(filename, data);

// 将模板源代码编译成函数
template.compile(source, options);

// 将模板源代码编译成函数并立刻执行
template.render(source, data, options);
```

## 标准语法

### 原文输出

```html
<div>
    {{@ value}}
</div>
原文输出value
```

### 条件输出

```html
<div>
    {{if flag === 1}}
    flag的值是1
    {{else if flag === 0}}
    flag的值是0
    {{/if}}
</div>
```

### 循环输出

```html
<div>
    {{each arr}}
    	索引是：{{$index}}
    	值是： {{$value}}
    {{/each}}
</div>
```

### 过滤器

```js
//使用过滤器
<div> 注册事件: {{regTime | dateFormat}}</div>
//定义过滤器
template.defaults.imports.dateFormat=function(regTime){
    var y = dete.getFullYear();
    var m = date.getMonth()+1;
    var d = date.getDate();
	return y + '-' + m + '-' + d; //runturn回去就是过滤后的结果
}
```

