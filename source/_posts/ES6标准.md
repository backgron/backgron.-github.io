---
title: ES6标准
date: 2021-05-17 22:51:08
tags:
  - 前端
  - JavaScript
categories:
  - 前端
  - javascript
description:  JavaScript ES6标准
---

# JavaScript ES6标准

## 类 Class

### 类 构造函数 属性 方法

```javascript
class Person{  //类
    construcor(name,age){  //构造函数
        this.name = name;  //属性
        this.age = age;
    }
    say(){ //方法
        console.log("hello world");
    }
}
var per=new Person("name",18);
```

### 继承 extends

```javascript
class Student extends Person{  //继承
    construcor(name,age,id){
        super(name,age);  //super指向父类构造方法  必须放在this之前
        this.id = id;
    }
    say(){
        console.log(super.say()+"自己的");  //super 指向父类一般方法
    }
}
```

### 注意事项和this指向

```javascript
1. 在ES6中，类没有变量提升，所以必须先定义类，才能通过类实例化对象
2. 类里面共有的属性和方法一定要加this使用
3. construcor里面的this只想实例对象
4. 方法里面的this指向这个方法的调用者
```

## ES6 的新生语法

### let关键字

```js
let a=1;
1. 用来声明变量，具有块级作用域
2. 不存在变量提升
3. 具有暂时死区特性，会和当前块级区域绑定，影响var声明的同名变量

注意：
1. 在{} 中，使用let声明的变量才有作用域，用var不具备块级作用域
2. 在for（）中使用let 可以防止循环变量变成全局变量
```

### const 关键字

```js
const a=1;
1. 具有块级作用域
2. 声明常量
3. 必须赋初始值
4. 常量复制后，值（地址）不能修改（对于简单类型，不能修改值。对于复杂类型，可以修改复杂类型内部的值，不能改地址） 
```

### 数组解构赋值

```js
let [a, b, c] = [1,2,3];
将数组中的值分别赋给abc  
```

### 对象解构

```js
let person = {name:'lisi'，age:30，sex:'男'};
let {name,age,sex} = person;
将变量名匹配对象的属性，匹配成功后赋值

变量名和属性名也可以不同  通过冒号连接    属性：变量名
let {name:myName,age:myAge} = person;
```

### 箭头函数

```js
const fn = (x,y) => {
    console.log(x+y);
}
1. 如果函数体只有一句代码，并且执行结果就时函数的返回值，函数体的大括号可以省略
2. 如果形参只有一个 形参外侧的小括号也可以省略
3. 箭头函数中没有自己的 this ，如果在箭头函数中使用 this ， this 关键字只想箭头函数定义位置作用域(对象不能产生作用域)中的 this
```

### 剩余参数

```js
function sum(first,...args){
    console.log(first); //10
    console.log(args); // [20,30]
}
sum(10,20,30);
1. 剩余参数语法允许我们将一个不定数量的参数表示为一个数组
2. 剩余参数配合解构使用
let arr1 = ['张三','李四','王五'];
let[s1,...s2] = arr1; // s1:张三  s2:[’李四','王五']

```

### 扩展运算符

```js
let arr = ['a','b','c'];
console.log(...arr); //相当于  console.log('a','b','c');
输出 a b c;

1. 合并数组：
let arr1 = [1,2,3];
let arr2 = [4,5,6];
let arr3 = [...arr1,...arr2];
或者  把arr2放入arr1中
arr1.push(...arr2);

2. 将伪数组转换为真正的数组
var div=document.getElementByTagName('div');
var ary = [...div];
```

### 新的原始数据类型 Symbol

```js
ES6 引入了一种新的原始数据类型 Symbol ，表示独一无二的值，最大的用法是用来定义对象的唯一属性名。

let name = Symbol("姓名");
let age = Symbol("年龄");
let sex = Symbol("性别");

let obj = {
    [name]:'张三',
    [age]:15，
    [sex]:'男'
}

// symbol  的属性无法通过 for-in  Object.keys()  来获取
// 可以通过： 来获取
Object.getOwnPropertySymbols();    // [Symbol(key1)]
Reflect.ownKeys();                 // [Symbol(key1)]

```



## ES6 的内置对象扩展

### Array的扩展方法

```js
1. Array.from(arrayLike,()=>{}); //将伪数组转化为数组
var arrayLike={
    '0':'1';
    '1':'2';
    'length':2;
}
var ary = Array.from(arrayLike,item => item * 2);

2. ary.find(); //找出第一个符合条件的数组成员，没有返回undefined
ary.find( item => item.id == 2 );

3. arr.findIndex(); //找出第一个符合条件数组的索引 没有返回 -1
let ary = [1,2,3,4,5];
let index = ary.findIndex(item => item > 3);

4. arr.includes(); //数组是否包含某个元素 返回布尔值
['a','b','c'].includes('a'); // true
['a','b','c'].includes('g'); // false
```

### String的扩展方法

```js
1. 模板字符串   
let name = '张三';
let sayHello = `hellomy name is ${name}`; // 模板字符串可以使用变量
let html = `
	<div>
		<span>${result.name}</span>
		<span>${result.age}</span>
	</div>
`; //模板字符串可以换行
const say = () => '哈哈';
let great = `${say()},嘿嘿`； //模板字符串可以使用函数
console.log(great);  // 哈哈，嘿嘿

2. startsWith() 和 endsWith()  //判断是否以..开头和结尾 返回布尔
let str = 'hello es6';
str.startsWith('hello');  //true
str.endsWith('es5');	//false

3. repeat();  //将原字符串重复n次，返回一个新字符串
'hello'.repeat(2); // 'hellohello'
```

### Set数据结构

```js
Set 数据结构，值唯一，没有重复值
Set本身是一个构造函数
const s1 = new Set();

Set 的实例属性
s1.size

Set 的实例方法
s1.add(1).add(2);  //添加 1 2
s1.delete(2);	   //删除 2
s1.has(1);		   //判断是否有 1  返回布尔
s1.clear();		   //清除 set 所有值

遍历set
s1.forEach(value => {
    console.log(value);
})
```





## 其他

### 添加元素 insertAdjacentHTML();

```js
//将指定的文本解析为 Element 元素，并将结果节点插入到DOM树中的指定位置
var li="<li>这是一个标签</li>";
ul.insertAdjacentHTML("position",text);

// position  位置
<!-- beforebegin -->
<p>
  <!-- afterbegin -->
  foo
  <!-- beforeend -->
</p>
<!-- afterend -->
```

## ES5新增方法

### 数组 Array

```js
arr.forEach()  遍历数组  return 不会退出
arr.filter()   过滤器 选出符合条件元素
arr.some()	   循环数组  遇到 return 退出
arr.every()	   检测数组所有元素是否都符合指定条件
```

### 字符串 String

```js
str.trim();		去除字符串两侧空格
```

### 对象 Object

```js
Object.keys(obj);	查询obj中的所有属性名 返回数组
Object.defineProperty(obj,prop,descriptor); 定义对象中新属性或者原有的属性
descriptor: {value writable enumerable configurable}

```

