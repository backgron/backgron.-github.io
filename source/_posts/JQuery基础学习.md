---
title: JQuery基础学习
date: 2021-04-22 22:52:39
tags:
  - 前端
  - JavaScript
  - JQuery
categories:
  - 前端
  - JQuery
description:  JQuery基础学习
---

```javascript
//事件
X	$(function(){})  页面加载事件
X	\$("#btn").click(function(){});  事件
X	.bind({"click":function(){},"mouseover":function(){}...});  为元素绑定多个事件
X	.bind("mouseover mouseout",function(){});
X	$(div).delegate("span","click",function(){});    通过div为div中的span绑定事件
***通常推荐使用on
$(div).on("click",function(){});          为div绑定事件
$(div).on("click","span",function(){});		为div中的span绑定事件
***解绑事件
.off("click");    解绑通过on 绑定的事件   不影响子元素的事件
.off("click","**");    解绑子级元素的点击事件
.off();    移除子级和父级所有事件
.unbind("click");   绑定通过bind 绑定的事件
$(div).undelegate("span","click");   解绑通过delegate绑定的$(div) 的子元素span的click事件
如果父级元素和自己元素都是通过正常的方式绑定事件
		off解绑父级元素时，子级元素的事件不会被解绑
如果父级元素调用delegate的方式绑定事件，
		父级元素通过off解绑事件，子级元素的相同时间都会被解绑
***触发事件
$("div").click();    触发div的点击事件
$("div").trigger("click");  触发div的点击事件
$("div").triggerHandler("click")   触发div的点击事件  不会触发浏览器的默认事件
return false;   取消事件冒泡，取消浏览器默认事件
***事件对象 function(event){};
event.delegateTarget    代码绑定事件的对象
event.currentTarget     绑定事件的对象
event.target            真正触发事件的对象
event.keyCode           获取按键   keydown事件



//选择器
$("#id")  
$(".class")
$("ul")
$("ul,div,span")
$("ul li")
$("ul>li")
$("ul+ul")
$("ul~ul")
$("ul *")
$("li.class");
$("ul>li:even")		奇数
$("ul>li:odd")		偶数
$("ul>li:eq(4)");  index=4
$("ul>li:gt(4)");  index>4
$("ul>li:lt(4)");  index<4
$("input[type=buttom]")



//属性
.height();
.css("width");   得到的是  "100px"  字符串
.css(); 样式设置:
	.css("color","red")   
	.css({"color":"red","width":"100px"})
.val(); 
.html(); 
.text();
.attr();   自定义属性:   .attr("year",19);   year=.attr("year");
.prop("checked");    checked 复选框中是否选中问题  bool=.prop("checked");   .prop("checked",false);
.offset().left;
.offset().top;
.offset("left":100,"top":100);
.scrollLeft();
.scrollTop();





//动画
***向左上角
.show();   显示    可加回调函数  .show(1000,function(){});
.hide();	隐藏
***向上
.slideUp;    滑入
.slideDown();   滑出
.slideToggle();  切换
***透明度
.fadeIn();	淡入
.fadeOut();	淡出
.fadeToggle(); 切换
.fadeTo(1000,0.3)  改变透明度
***animate
.animate(键值对对象,时间,回调函数);
***其他
.stop();  停止当前元素动画




//获取元素
.siblings("element"); 获取兄弟元素
.find(); 获取所有后代元素
.next(); 下一个兄弟元素 
.nextAll();  
.prev(); 当前元素的前面的兄弟元素
.prevAll();
.end();  恢复到断链之前
.frist("element");  第一个元素
.last();    最后一个元素




//设置class
.addClass(); 添加类 多个类中间用空格隔开 不加点
.removeClass();删除类，括号不填全部删除
.hasClass();  判断有没有某个类样式  返回布尔类型
.toggleClass();  切换类样式




//添加元素  删除元素  克隆元素
***添加
var pObj=$("<p></p>");
.append(pObj);   依次向后添加子元素
.prepend(pObj);   依次向前添加子元素
.after(pObj);	向后添加兄弟元素
.befor(pObj);   向前添加兄弟元素
pObj.appendTo("div")  p加入到div中
.html("<p></p>")   添加p
***删除
.html("")  删除元素内的东西
.empty()   删除元素内的东西
.remove()  删除当前元素
***克隆元素
.clone(pObj);



//其他
arguments.callee  相当于递归
arguments.length   获取当前函数调用时有几个参数
***链式编程的基本原理
sayName(name){
	if(name)
		return this;
	else
		return name;
}
方法将对象返回就可以

.each(function(index,element){});
***多库共存冲突问题
var xy=$.noConflict();   将$的控制权给xy  之后xy取代$  xy(function)
jQuery(function(){})  还可以用


```

