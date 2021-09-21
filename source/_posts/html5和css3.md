---
title: html5和css3
date: 2021-05-07 22:40:59
tags:
  - 前端
  - html5和css3
categories:
  - 前端
  - html和css
description:  html5和css3的学习
---

# HTML5 和 CSS3

## HTML5

### 新增语义化标签

```html
<header>头部标签</header>
<nav>导航栏标签</nav>
<article>内容标签</article>
<section>定义文档某个区域</section>
<aside>侧边栏标签</aside> 
<footer>尾部标签</footer>
```

1. 有兼容性问题，ie9+支持，ie9需要display:block 把标签转换为块级元素
2. 标签可以多次使用
3. 移动端好用

### video视频标签    audio 音频标签

#### video

```css
<video src=""></video>
属性：
autoplay = autoplay  自动播放
muted = muted  谷歌浏览器自动播放/静音播放
controls = contr ols  显示播放控件
loop = loop  循环播放
preload = auto/none  预选加载
poster = "图片链接"   预先加载图片（视频没有播放的时候可以先显示图片）

支持: 需要兼容性
mp4:所有支持
ogg:部分支持
webm:部分支持
```

#### audio

```css
<audio src=""></audio>
属性：
autoplay
controls
loop
muted

支持： 需要兼容性
mp3：所有支持
wav：部分支持
ogg：部分支持
```

### input类型和属性

#### 新增input 类型

```html
需要填在form表单中，提交时进行校验
<input type="email" />
<input type="number" />
<input type="date" />
<input type="month" />
<input type="week" />
<input type="time" />
<input type="color" />
<input type="tel" />
<input type="search" />
<input type="url" />
```

#### 新增表单属性

```css
required="required";  表单必须填入，提交时校验
placeholder="提示"     提示信息
autofocus="autofocus" 自动获得焦点
autocomplete="off/on" 记录之前输入过的信息  默认打开
multiple="multiple"	  可以多选文件 type=file使用

可以通过为元素修改属性
{
	input::placeholder{
		color:pink;改变颜色
	}
}
}
```





## CSS3

### 属性选择器

+ 注意：类选择器、属性选择器、伪类选择器的权重都为10

```css
E[att]			选择具有att属性的E
E[att="val"]	选择具有att属性且属性值等于val的E
E[att^="val"]	匹配具有att属性且属性值以val开头的E
E[att$="val"]	匹配具有att属性且属性值以val结尾的E
E[att*="val"]	匹配具有att属性且属性值中含有val的E
```

#### 结构伪类选择器

```css
E:first-child		匹配父元素中的第一个子元素E
E:last-child		匹配父元素中最后一个E元素
E:nth-child(n)		匹配父元素中的第n个子元素E
E:first-of-type		指定类型E的第一个
E:last-child		指定类型E的最后一个
E:nth-of-type(n)	指定类型E的第n个

区别：nth-child对付元素里面的所有元素排序，先找到第n个孩子，看是否和E匹配
	 nth-of-type对付元素里面指定子元素进行排序。先去匹配E，然后根据E找到第n个
```

### 元素选择器

```css
::before		在元素内部的前面插入内容
::after			在元素内部的后面插入内容
```

1. before 和 after 创建一个元素，但属于行内元素

2. 新创建的这个元素在文档树种是找不到的

3. 语法：element::before{}

4. before和after必须有content属性

5. before在父元素内容的前面创建，after在父元素内容的后面插入元素

6. 伪元素选择器和标签选择器一样,权重伪1

7. 伪元素清除浮动

    ```css
    .clearfix:after{
        content:"";
        display:block;
        height:0;
        clear:both;
        visibility:hidden;
    }
    
    //升级版：
    .clearfix:befor,.clearfix:after{
        content:"";
        display:table;  //转为块级元素，并同一行显示
    }
    .clearfix:after{
        clear:both;
    }
    ```

### css3盒子模型

```css
{
    //盒子大小为width+padding+border （以前默认）
    box-sizing:content-box;
    //盒子大小伪width  不会被border和padding撑大 （前提是padding和border不会超过width的宽度）
    box-sizing:border-box;
}
```

### filter滤镜

```css
//添加各种滤镜
filter: none | blur() | brightness() | contrast() | drop-shadow() | grayscale() | hue-rotate() | invert() | opacity() | saturate() | sepia() | url();

```

### calc函数

```css
calc()在声明属性时进行一些计算 + - * /
例如：
{
    width:calc(100px+50px);
    height:calc(80%+10px);
}

```

### transition 过渡

```css
//谁要过渡给谁加
transition:属性 花费时间 运动曲线 何时开始

属性：想要变化的css属性，如果想要所有属性就写all
花费时间：单位是秒s，必须写单位
运动曲线：默认是ease(可以省略)
何时开始：单位是秒s，必须写单位，默认是0，可以省略
```



### 2D转换 transform

#### 2D移动 translate

```css
transform:translate(x,y);
transform:translateX(n);
transform:translateY(n);

1. translate最大优点：不会影响到其他元素的位置
2. translate中的百分比单位时相对于自身元素高度或者宽度的
3. 对行内标签没有效果
```

#### 2D旋转 rotate

```css
正直为顺时针，负值为逆时针
transform:rotate(45deg);

转换中心  默认为50% 50%
transform-origin:x y;
```

#### 2D缩放 scale

```css
不会影响其他盒子 以中心点缩放
transform:scale(x,y); x宽和y高的倍数
transform:scale(n);  n宽和n高
```

#### 2D转换的综合写法

```css
transform:translate() rotate() scale();
存在执行顺序的问题
旋转会影响坐标轴方向
当我们同时有唯一和其他属性的时候，记得要将位移放到最前面
```

### 3D转换 transform

#### 3D透视perspective

```css
perspective:500px;
1. 透视越大，图像越小
2. 透视单位为像素
3. 透视写在被观察元素的父盒子上面
```

#### 3D呈现 transfrom-style

```css
transfrom-style:preserve-3d;  开启子元素3D
1. 控制子元素是否开启3D
2. 给父元素添加，影响的是子元素
3. 默认为flat不开启
```



#### 3D移动 translate

```css
transfrom:translateX(); 
transfrom:translateY();
transfrom:translateZ();

transfrom:translate3d(x,y,z);
```

#### 3D旋转 rotate3d

```css
transfrom:rotateX(deg);
transfrom:rotateY(deg);
transfrom:rotateZ(deg);
transfrom:rotate3d(x,y,z,deg);
```



### 动画 animation

```css
1. 动画定义
@keyframes 动画名{
    0%{
        
    }
    50%{
        
    }
    100%{
        
    }
}
2. 动画调用
div{
    animation-name:动画名;
    animation-duration:10s; 持续时间
    animation-timing-function:ease; 速度曲线  steps(n) 分n步
    animation-delay:0s; 何时开始
    animation-iteration-count:infinite; 播放次数 默认为1
    animation-direction:alternate; 下一周期是否逆播放 默认为normal
    animation-play-state:paused; 是否播放或暂停 默认为running
    animation-fill-mode:forwards; 动画结束后的状态 默认为backwards
    
    简写  name和duration必须写
    animation: name duration timing-function delay iteration-count direction;
}
```



```css
//边框
{
  border-radius:50px;  //圆角 半径50
  border-image-source:url(); 路径
  border-image-slice:上 右 下 左;裁剪尺寸
  border-image-width:大小;不是边框宽度，是图片宽度
  border-image-repeat: 平铺repeat/铺满round/拉伸stretch（默认）
}

//盒子
{
    //不影响盒子排列
    //盒子阴影：  水平      垂直       模糊距离  阴影尺寸  颜色     内阴影（不写为外阴影）
    box-shadow：h-shadow  v-shadow   blur   spread   color   inset;
}

//文字
{
    //文字阴影
    text-shadow：h-shadow v-shadow blur color;
}
```

