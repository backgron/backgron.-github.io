---
title: JavaScript高级与正则表达式
date: 2021-04-22 22:50:16
tags:
  - 前端
  - JavaScript
  - JavaScript高级
  - 正则表达式
categories:
  - 前端
  - javascript
description:  JavaScript高级与正则表达式
---

```javascript
//判断一个对象是不是这种数据类型
console.log(dog.__proto__.constructor==Person)   false; 
dog instanceof Person    false;
Object.prototype.toString.call(dog);   通过call改变同toString方法

//通过原型实现数据共享  节省空间  prototype
Person.prototype.eat=function(){};   //让Person的实例化对象公用一个方法
Person.prototype.name="pig";       //  共享属性
Person.prototype={ 				//可以以对象的方式赋值
		constructor:Student,   //手动添加构造器
		"width":"100px",
		eat:function(){};
		} 



//构造函数可以实例化对象   实例对象中的__proto__指向prototype     prototype的构造器指向构造函数
	构造函数有一个属性叫prototype，是构造函数的原型对象
	构造函数的原型对象（prototype）中有一个constructor构造器
构造器指向的就是自己所在的原型对象的构造函数
	实例对象的运行对象（__proto__）指向的是该构造函数的原型对象
	构造函数的原型对象（prototype）中的方法时可以被实例对象直接访问的

原型中的方法也可以互相访问，使用时先去实例对象中找方法或属性，再去原型中找、

原型链：是一种关系：是实例对象和原型对象的一个关系，关系是通过原型
		所联系的（__proto__ 指向原型对象）


//将局部变量转变为全局变量
function(window){
	var num=10;
	window.num=10;
}


//通过call继承  ：  构造函数名字.call(当前对象this,属性,属性,...);   方法无法继承
function Student(name,age,sex,sc){
	Person.call(this,name,age,sex);
	this.sc=sc;
}

//继承：
原型继承：改变原型的指向
借用构造函数继承： 解决属性的问题
组合继承： 原型继承＋借用构造函数继承
			既能解决属性问题，又能解决方法问题
拷贝继承： 就是把对象中需要共享的属性或方法，直接遍历复制到另一个对象中去


//因为存在预解析问题 优先使用函数表达式的方法声明函数  
函数表达式  var fun=function(){};  //优先
函数声明    function fun(){};

//严格模式：
"use strict";


//函数也是对象  所有的函数都是Function的构造函数创建出来的对象
var f1=new Function("name","age","return name+age");
等于  function f1(name,age){return name+age};


//apply 和 call   改变this的指向


	1.apply和call方法也是函数的调用方式
	2.apply和call方法中如果没有参数，或者传入的是null，那么该方法的函数对象中的

this就是默认的window
	3. f1(100,200)
	   f1.apply(null,[100.200]); 
	   f1.call(null,100,200);
	    apply和call 都可以让函数或者方法来调用，传入参数和函数自己调用的方法不同
	   但是效果是一样的
	   
//bind   改变this 指向
	1. var ff=f1.bind(null);  在赋值的时候改变this指向
	2. 函数名.bind(对象，参数1，参数2..)  返回值是复制之后的这个函数
	2. 方法名.bind(对象，参数1，参数2..)  返回值是复制之后的这个方法

//函数中的几个参数
	f1.name   函数名  name是只读属性，不能修改
	f1.arguments.length   函数的实参个数
	f1.length     函数定义时 形参的个数
	f1.caller    函数的调用者---f1 函数是在f2函数中调用的
	

//闭包	
	闭包的作用：缓存数据延长作用域链	优点也是缺点  数据没有及时的释放
	局部变量在函数中，函数使用结束后，局部变量就会被释放
	但是在闭包后，里面的局部变量的作用域链就会被延长
	

	function fn(){
		var num=parseInt(Math.random);
		return function f2(){
			return num;
		}
	}
	var ff=fn();  此时  console.log(ff())  console.log(ff())是相同的随机数


//正则表达式

元字符：

	.  除了\n意外的任意一个单字符
	[] 范围
	() 分组，提升优先级
	|  或者
	*  0-多次
	+  1-多次
	？ 0-1次
	{0,} 和*一样
	{1,} 和+一样
	{0,1} 和？一样
	\d	数字中的一个
	\D	非数字
	\s	空白符
	\S	非空白符
	\W	特殊符号
	\w	非特殊符号
	^	取反  以什么开始
	$	以什么结束
	
	\b  单词边界

正则表达式中:g 表示的是全局模式匹配
正则表达式中:i 表示的是忽略大小写
正则表达式对象.$3
```

