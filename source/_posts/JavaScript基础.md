---
title: JavaScript基础
date: 2021-04-22 22:45:00
tags:
  - 前端
  - JavaScript
  - JavaScript 基础
categories:
  - 前端
  - javascript
description:  JavaScript 基本语法
---

```javascript
var nll=null;	//此时nll属于object类型，因为赋值
	 	null时吧nll看作为一个对象，所以为
		object类型，但是String(nll);  输出为null

!=   不严格的不等
!== 严格的不等  
==  不严格的相等	//值相等
===严格的相等	//类型和值都相等

switch-case   使用的是严格的相等


=============！！！=================！！！==============！！！===============！！！=====


数组：  
1.构造函数方式创建数组  var 数组名=new Array();
如果（）里是一个数字，那表述数组的长度
如果（）里是多个数字，就表示输入元素，数组个数为数组长度
只有长度没有元素的数组默认数组元素为undefined类型

2. 通过字面量的方式创建数组   var 数组名=[ ]；
    数组的使用：
     数组名[下标/索引]=值;
     数组长度：数组名.length;
    ***   数组里存储的数据的类型不一定相同 ： var array=[1,10.2,"哈哈",new Object(),null,undefine]；
    									是可以执行的；
      数组的长度是可以改变的  var array=new Array(1); array(2)=3;是可以执行的；
    									 array(44)=undefine; 未定义的就是undefein

    

=============！！！=================！！！==============！！！===============！！！=====
	
	
函数：  
function 函数名(){}     //定义函数参数时不需要加上参数的数据类型  例如：
									function twoSum(x,y){}
函数调用时，形参和实参的个数不一定相同，如果实参	大于形参，后面的无效；如果形参大于实参
多余的形式参数按照 undefined 类型处理
如过函数没有返回值或  return;  ，接收到的是 undefined

var 函数名=function (){};   //通过函数表达式创建函数 相当于一个变量
函数名();  					//调用方法相同

(function (){console.log("123");})();  //函数的自调用  一次性

函数的数据类型为 function         typeof(函数名) = function;

函数可以作为参数使用  function f1(fn){}

函数可以作为返回值   return f1;   return function (){};

作用域： 	//除了函数内部定义的变量以外，其他位置定义的都是全局变量

全局变量：用var声明的就是全局变量，可以在任何位置访问到
局部变量：在函数内部定义的变量，只能在函数内部使用


块级作用域：一个大括号{}里面的就是一个块级作用域，//js中没有块级作用域
全局作用域：全局变量的使用范围
局部作用域：局部变量的使用范围

*** 隐式全局变量：声明时没有 var ，就是隐式全局变量，就算在函数里定义也可以在外面使用
全局变量不会被 delete 删除 （ delete num1；） ，隐式全局变量可以被 delete 删除
即有 var 不会被删除  没有 var 会被删除

预解析：在解析代码之前
1、把变量是声明提前到当前所在作用域的最上面
2、把函数的声明提前到当前所在作用域的最上面
函数调用时，会把函数的声明提到作用域的最上面
变量的声明提升到变量使用的前面
** 先提前变量的声明，再提前函数的声明，也就是说预解析过后函数的声明在下面
!!!!!   //  因为b和c没有var是隐式全局变量   所以在函数的外面也可以使用相当于
        //   var a=9；   b=a; c=b;
        f1();
        console.log(c);//  9
        console.log(b);//  9   
        console.log(a);//   报错
        function f1()
        {
            var a=b=c=9;
        console.log(a);//9
        console.log(b);//9
        console.log(c);//9
!!!!!	}


=============！！！=================！！！==============！！！===============！！！=====


面向对象：  封装、继承（js没有继承）、多态
Js 不是面向对象的语言，是基于对象的语言
**一个对象占了两块空间  栈(存储对象在堆中的地址)  堆(存储对象内容)
1、通过构造函数创建对象
var student=new Object();
对象的属性(特点)：    student.name="小苏";
对象的方法(行为)：    student.study=function(){};

//  通过   变量(对象) instanceof 类型名字 判断给对象是不是这个类型的
//           返回值为boolean类型  true是  false不是

2、工厂模式创建对象：把创建对象的构成封装成函数，创建对象时直接调用:
!!!!!   var Student=function(name,age,sex){
            var stu=new Object();
            stu.name=name;
            stu.sex=sex;
            stu.age=age;	//创建对象属性的时候不能使用this
            stu.siHi=function()
            {
                console.log("我叫"+this.name+"，我今年"+this.age+"岁了，我是"+this.sex+"生");
            };		// 对象的方法调用对象属性时可以用this来代替
            return stu;
        }
        var student1=Student("小明",18,"男");
        var student2=Student("小红",17,"女");
        student1.siHi();
!!!!!   student2.siHi();

3、****通过自定义构造函数创建对象**********
!!!!!   function Person(name,age ,sex){
            this.name=name;
            this.age=age;
            this.sex=sex;
            this.sayHi=function ()
            {
                console.log("我叫"+this.name+"，我今年"+this.age+"岁了，我是"+this.sex+"生");
            } 
        }
        var per=new Person("小红",16,"女");
        var per2=new Person("小明",19,"男");
        per.sayHi();
        per2.sayHi();
!!!!!   console.log(per instanceof Person); // true
//     通过自定义构造函数创建对象时  当  var per=new Person("小红",16,"女");执行时
//			系统做了四件事
//		1、想内存中申请一块空闲的空间用于存储创建的新对象
//		2、把 this 设置为当前对象
//		3、设置当前对象的属性和方法
//		4、把 this 这个对象返回

4、通过 字面量 的方式创建对象    一次性对象
		//优化前
!!!!!   var obj={};                //相当于  var obj=new Object();
        obj.name="小明";
        obj.age=10;
        obj.sex="男";
        obj.sayHi=function (){
            console.log("我叫"+obj.name+"，我今年"+this.age+"岁了，我是"+this.sex+"生");
        }
        obj.sayHi();

        //优化过后
        var obj1={
            name:"小红",
            age:15,
            sex:"女",
            sayHi:function(){
                console.log("我叫"+this.name+"，我今年"+this.age+"岁了，我是"+this.sex+"生");
            }
        };

!!!!!   obj1.sayHi();

Js是动态语言：

1. 当代码执行到这个位置的时候才知道变量中存储的到底是什么，如果是对象，就有对象的属性和方法
    	如果是变量，就有变量的作用
2. 点语法： 对象没有什么直接 点出来  通过点语法为对象添加属性或方法
    per["name"]		等同于	per.name
    per["play"]();	等同于	per.play();
    **对象中实际存在的属性用 点   如果对象中不存在还用 点  就会自动给你创建一个属性，值为 undefined

JSON格式的数据： 成对存在，键值对
		//json 也是一个对象 属性都是  "":"", 的形式
	var json={
		"name":"小明",
		"sex":"男",
		"age":"10",
	};
JSON格式数据的遍历：
		//通过 for-in 循环遍历
	for(var any in json){			//key是一个变量存储的是该对象所有属性的名字
		 console.log(any+"--------"+json[any]);  //此处不能用 点 如果用点 就会自动创建一个
	}											//  any属性  其值为undefined
	
	
=============！！！=================！！！==============！！！===============！！！=====


简单类型和复杂类型：
1、原始数据类型：number、string、boolean、undefined、null、object
	基本类型(简单类型),值类型： number、string、boolean
	复杂类型(引用类型)：object
	空类型: null、undefined
// 值类型的值存储在栈中
// 引用类型的存储在栈和堆中		地址在栈中  对象在堆中
2、值类型和引用类型的传递
// 值类型传递的是值(在栈中存储)
// 引用类型传递的是地址(在栈中存储)
// 值类型作为函数的参数,传递的是值
// 引用类型作为函数的参数，传递的是地址


=============！！！=================！！！==============！！！===============！！！=====


内置对象
实例对象：通过构造函数创建出来的实例化的对象
静态对象：不需要创建，直接就是一个对象，方法(静态方法)直接通过这个对象名字调用
//实例方法必须通过实例对象去调用
//静态方法必须通过大写的对象去调用

Math 对象的常用属性和方法  静态对象 static  不需要创建实例对象

Math.PI			Π
Math.E			e自然对数的底数
Math.abs(a)		a的绝对值
Math.ceil(a)	a数字向上取整  （小数进1）
Math.floor(a)	a数字向下取整	(小数舍去)
Math.max(a,b..) 找出括号传入的数字中的最大值
Math.min(a,b..) 找出括号传入的数字中的最小值
Math.pow(a,b)	a的b次方
Math.sqrt(a)	a的平方根
Math.sin(a)		a的正弦值
Math.random()	返回一个[0~1)之间的随机数


Date 对象的常用方法  实例对象 var dt=new Date();  需要创建实例对象

dt.getFullYear();	获取当前	年份
dt.getMonth();		获取当前	月份//月份从0开始  0是一月  实际月份要加一
dt.getDate();		获取当前	日期
dt.getHours();		获取当前	小时
dt.getMinutes();	获取当前	分钟
dt.getSeconds();	获取当前	秒数
dt.getDay();		获取当前	星期//星期从0开始  0是周日
	
dt.toString();				Tue Jan 28 2020 21:20:55 GMT+0800 (中国标准时间)
dt.toDateString();			Tue Jan 28 2020
dt.toLocaleDateString();	2020/1/28
dt.toTimeString();			21:20:55 GMT+0800 (中国标准时间)
dt.toLocaleTimeString();	下午9:20:55
dt.valueOf();				1580217655210  //从1970年开始的毫秒时间

String 对象常用的方法和属性  var str="";

str.lenght					获取字符串长度
String.fromCharCode(下标);	方法返回由指定的UTF-16代码单元序列创建的字符串
str.concat("str1","str2");	返回str+str1+str2..的字符串
str.indexOf("str1");		返回“str1”在 str 中第一次出现的索引
str.lastIndexOf("str1");	返回 str1 在 str 中最后一次出现的索引
str.replace("str1","str2");	返回将str中的str1替换为str2后的字符串
str.slice("索引1","索引2");	返回包括索引1到不包括索引二之间的字符串
str.split("str1","num");	num是返回个数，把str已str1为分割线切割
str.substr("索引","num");	截取索引往后取num个字符
str.substring("索引1","索引2");	返回从索引1(包括)到索引2的字符串
str.toLocaleLowerCase();	将str转为小写返回
str.toLowerCase();			将str转为小写返回
str.toUpperCase();			将str转为大写返回
str.trim();					删除字符串前后的空格
str.trimLeft();				删除字符串左边的空格
str.trimRight();			删除字符串右边的空格


Array 对象的常用方法和属性	var arr=[];

arr.length;					数组的长度
arr.push(值);				向数组的后面追加一个元素	返回值为插入后数组长度
arr.pop();					删除数组的最后一个元素，返回值就是删除的这个元素
arr.shift();				删除数组的第一个元素，返回值就是删除的这个元素
arr.unshift(值);			向数组的前面插入一个元素	返回值为插入后数组长度

Array.isArray(arr);			判断arr是不是一个数组 返回true/false
arr.concat(arr1,arr2);		返回arr+arr1+arr2的新数组
arr.every(函数);			返回布尔类型，函数有三个参数，第一个是参数的值，第二个是参数
							的索引，第三个是原来的数组(没什么用);
arr.filter(函数);			返回可以满足函数要求的元素，组成一个新的数组
arr.forEach(函数);			遍历数组
arr.indexOf(元素值);		返回索引，没有则是-1
arr.join("str");			通过str把每个元素连接起来，返回一个字符串
arr.map(函数);				把数组中的每个元素执行函数，把执行后的结果返回一个新的数组
arr.reverse();				反转数组，返回反转后的数组
arr.sort();					排序，不稳定	可能需要在括号里补充以下函数
								function (a,b){
									if(a>b){return 1;}
									else if(a==b){return 0;}
									else if(a<b){return -1}
								}
arr.slice(开始索引，结束索引);	把截取的字符串返回一个新的字符串，包括开始不包括索引
arr.splice(开始的位置，要删除的个数，替换的元素的值);
							用于删除数据，替换元素，插入元素;
							
=============！！！=================！！！==============！！！===============！！！=====					


基本包装类型：

//普通的变量没办法直接调用属性和方法
//对象可以直接调用属性和方法

基本包装类型：本身是基本类型，但在执行代码的过程中，这个变量调用了属性或者方法，那么这
			  种类型就不再是基本类型，变量也不是普通的变量，而是基本包装类型对象
//例如：  str.replace();     num.toString();    var flag=new Boolean(false);

  string  number  boolean  就会动不动就变成基本包装类型

对象&&true   	结果就是true
true&&对象	 	结果就是对象
```

