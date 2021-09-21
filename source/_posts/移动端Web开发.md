---
title: 移动端Web开发
date: 2021-05-19 23:23:01
tags:
  - 前端
  - 移动端web开发
categories:
  - 前端
  - 移动端web开发
description:  移动端Web开发
---

# 移动web开发

## 基础知识

### 视口 meta标签

```css
<meta name="viewport" content="width-dvice-width",user-scalable=no,initial-scale=1.0,maximum-scale=1.0,minimum=1.0">

width:宽度设置的是viewport宽度，可以设置device-width特殊值
initial-scale：初始化缩放比，大于0的数字
maximum-scale: 最大缩放比，大于0的数字
minimum-scale：最小缩放比，大于0的数字
user-scalable：用户是否可以缩放，yes或no（0或1)
```

### 物理像素与物理像素比

1px(物理像素)  不一定等于 1px(开发像素)

### 二倍图

多个物理像素显示一个开发像素，为了达到更高的分别率，可以使用比实际显示要大的图片，页面使用width和height调整实际显示大小

### 盒模型 box-sizing

移动端可以全部使用css3和模型：border-box;

如果不考虑兼容性，pc端可以使用：border-box;

## 布局

### 流式布局（百分比布局）

+ 流式布局就是百分比布局，也称非固定像素布局
+ 通过盒子的宽度设置成百分比来根据屏幕的宽度来伸缩，不受固定像素的限制，内容向两侧填充

### flex布局 弹性布局 display:flex;

```css
给容器盒子(父盒子)添加  display:flex;
容器默认存在两根轴：水平的主轴和数值的侧轴
```

#### 容器的属性

1. flex-direction:  设置轴

    ```css
    flex-direction: row | row-reverse | column | column-reverse;
    
    row（默认值）：主轴为水平方向，起点在左端。
    row-reverse：主轴为水平方向，起点在右端。
    column：主轴为垂直方向，起点在上沿。
    column-reverse：主轴为垂直方向，起点在下沿。
    ```

2. flex-wrap  是否换行

    ```css
    flex-wrap: nowrap | wrap | wrap-reverse;
    ```

3. flex-flow 是 flex-direction  和flex-wrap的缩写

    ```css
    flex-flow: <flex-direction> <flex-wrap>;
    ```

4. justify-content 项目在主轴上的对齐方式

    ```css
     justify-content: flex-start | flex-end | center | space-between | space-around;
    
    flex-start（默认值）：左对齐
    flex-end：右对齐
    center： 居中
    space-between：两端对齐，项目之间的间隔都相等。
    space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
    ```

5. align-items  交叉轴上如何对齐  单行。

    ```css
    align-items: flex-start | flex-end | center | baseline | stretch;
    
    flex-start：交叉轴的起点对齐。
    flex-end：交叉轴的终点对齐。
    center：交叉轴的中点对齐。
    baseline: 项目的第一行文字的基线对齐。
    stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。
    ```

6. align-content  交叉轴上如何对齐  多行

    ```css
    align-content: flex-start | flex-end | center | space-between | space-around | stretch;
    
    flex-start：与交叉轴的起点对齐。
    flex-end：与交叉轴的终点对齐。
    center：与交叉轴的中点对齐。
    space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
    space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
    stretch（默认值）：轴线占满整个交叉轴。
    ```

    #### 项目属性

    1. order属性  定义项目的排列顺序

        ```css
        order: <integer>;
        ```



### rem和less

#### rem

```css
root em  类似于em单位，rem只与html设置的font-size有关
```

#### 媒体查询

```css
@media mediatype and|not|only (media feature){
    css-Code;
}

mediatype:all(所有设备),print(打印机和打印预览),screen(电脑手机等)
media feature: 如  min-width:500px;  最小500px时

通过media来引入不同的css资源
<link rel="stylesheet" href="style320.css" media="screen and (min-width:320px)">
```

#### less

```less
1. 定义变量：
@color：red；
body{
    color：@color；
}

2. 嵌套
header{
    width:100px;
    height:100px;
    //子元素直接嵌套
    a{
        color:@color;
        //伪类   伪类和伪选择器和交集选择器需要加 & 符号
        &:hover{
            bule
        }
    }
}
转化为： header{}  和  header a{} 和header a:hover{};

3. 运算
width:50px + 50;   100px;
width:50px - 10;   40px;
width:50   * 5px;  250px;
width:50rem / 5px; 10rem;
width:(50px + 50px) * 2; 200px;
运算符两边必须用空格隔开
如果只有一个单位，那么结果就时这个单位
如果有两个不同的单位，结果以第一个单位为准

4. 导入样式
import "common"；
吧common.less 导入当前less文件
```

#### rem+less适配方案

1. 首先选择一套标准尺寸 如750为准
2. 用屏幕尺寸 除以 我们划分的分数 得到html里面文字的大小，不同屏幕的时不同的文字大小
3. 页面元素的rem = 页面元素在750像素下的px值 / html字体大小；

#### rem+flexible适配方案

使用[flexible.js](https://github.com/amfe/lib-flexible)轻松搞定各种不同的移动端设备兼容自适应问题。

#### 响应式布局

1. 响应式需要一个父级作为布局容器，来配合子级元素来实现变化效果

2. 原理就是在不同屏幕下，通过媒体查询来改变这个布局容器的大小，在改变里面子元素的排列方式和大小，从而实现不同屏幕下，看到不同的页面布局和样式变化

    + 1170px(大屏幕 大桌面显示器)

    + 970px(中等屏幕 桌面显示器)

    + 750px(小屏幕 平板)

    + 小于768px (超小手机屏幕)

```css
超小屏幕 小于768 
@media screen and (min-width:767px){
    .container{
        width:100%;
    }
}
小屏幕 大于768 
@media screen and (min-width:768px){
    .container{
        width:750px;
    }
}
中等屏幕 992px
@media screen and (min-width:992px){
    .container{
        width:970px;
    }
}
大屏幕 1200px
@media screen and (min-width:1200px){
    .container{
        width:1170px;
    }
}
```

## Bootstrap

  栅格系统：  col-设备型号-格子数  一行总共12个格子

1. 定义容器，相当于之前的table
    		container:  两边有一些留白
    		container-fluid: 每一种设备都是100%宽度
2. 定义行。相当于之前的tr  样式:row  每行一共12格
3. 定义元素  制定不同设备：col-设备型号-占格子数
    + 设备代号：
        + 手机小屏幕：   col-xs-
        + 平板小屏幕：   col-sm-
        + 电脑中等屏幕：col-md-
        + 电脑大屏幕：    col-lg-
    + 注意：
        + 如果定义超出12格，则会自动换行
        + 栅格类属性可以向上兼容，山各类适用于屏幕宽度大于或等于分界点大小的设备
        + 如果真是设备宽度小于了设置栅格类属性的设备代码的最小值，会一个元素沾满一整行



