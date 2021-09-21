---
title: html和css复习
date: 2021-04-26 23:25:13
tags:
  - 前端
  - html和css
categories:
  - 前端
  - html和css
description:  html和css复习
---

# HTML和CSS复习

## HTML

```html
// href 如果给的是压缩包(.zip等)或者文件(.exe) 就会下载这个文件
// href  锚点链接  href="#id"  定位到id的位置
// target  在当前窗口打开 还是新的窗口打开
<a href='路径/#/压缩包/文件' target="打开方式"></a>

//table
//属性：cellpadding(单元格和内容距离) cellspaching(单元格和单元格距离)
//属性: colspan(跨列合并)  rowspan(跨行合并)
<table>
    <thead>//结构 表格头部
        <tr>//行
            <th>表头</th>//表头  自动加粗居中
        </tr>
    </thead>
    
    <tbody>//结构 表格主体
        <tr>
            <td>表格</td>//列
        </tr>
    </tbody>
</table>

//无序列表
<ul>
    <li></li>
</ul>
//有序列表
<ol>
    <li></li>
</ol>
//自定义列表
<dl>
    <dt></dt>//小标题
    <dd></dd>//小标题下的
</dl>

//表单
<form>
    <label for='txt'></label>//绑定input
    <input type="text" id='txt'>
    //buton checkbox file hidden image password
 	//radio reset submit text
    <select>//下拉菜单
        <option selected="selected">11</option>
        <option>22</option>
    </select>
</form>
```



## CSS

### 伪类选择器

```css
//伪类选择器
{
    a:link;	    //未访问
    a:visited;	//已放问
    a:hover;	//鼠标悬停
    a:active;	//已选择
    input:focus; //已选中  获取焦点
    :first-child; 伪类与指定的元素匹配：该元素是另一个元素的第一个子元素。
}
```

### 复合属性

```css
// 复合属性
{
    //背景
    background:color url() no-repeat fixed right top;
    //外边距
    margin:top right bottom left;
    //内边距
    padding:top right bottom left;
    //字体 
    font: style weight *size *family;
}
```

### 属性权重  优先级问题

| 选择器               | 选择权重 |
| -------------------- | -------- |
| 继承或 *             | 0.0.0.0  |
| 元素选择器           | 0.0.0.1  |
| 类选择器，伪类选择器 | 0.0.1.0  |
| ID选择器             | 0.1.0.0  |
| 行内样式  style=""   | 1.0.0.0  |
| !important 重要的    | 无穷大   |

权重叠加

```css
.ul li{}   权重为 0.0.1.0 + 0.0.0.1  = 11
.li{}      权重为 0.0.1.0=10
```





### 内外边距 margin  padding



```css
// 外边距 margin  
{
    margin:top right bottom left;
    *当两个垂直外边距相遇时，它们将形成一个外边距。
    *合并后的外边距的高度等于两个发生合并的外边距的高度中的较大者。
    
    *当一个元素包含在另一个元素中时（假设没有内边距或边框把外边距分隔开），它们的上和/或下外边距也会发生合并  父盒子和子盒子
    解决办法：
    		1. 给父元素上边框
    		2. 给父元素定义上内边距
    		3. 给父元素添加overflow:hidden;
}

//内边距 padding
{ 
    padding  如果盒子本身给了宽度/高度，那么padding会把盒子撑大 width=100px；
    		 width=100%; 一般和父级元素一样宽就不指定width=100%； 不然如果设置padding 子级元素会比父级元素更大
    		
    		 如果盒子没给宽度和高度，padding就不会把盒子撑大
}

！！   浏览器会默认给内外边距  可以通过手动去除  
{
    margin:0;
    padding:0;
}

！！  行内元素为了照顾兼容性，尽量只设置左右内外边距，不设置上下内外边距  转换为行内块元素就可以
```

### 轮廓 outline

```css
// 轮廓 outline
{
    outline-style
    outline-color
    outline-width
    outline-offset
    outline
    *轮廓与边框不同.不同之处在于：轮廓是在元素边框之外绘制的，并且可能与其他内容重叠。同样，轮廓也不是元素尺寸的一部分；元素的总宽度和高度不受轮廓线宽度的影响。
}
```

### 文本格式化 text

```css
// 文本格式化
{
    direction 和 unicode-bidi 属性可用于更改元素的文本方向：
    vertical-align 属性设置元素的垂直对齐方式。
    text-decoration: none; 通常用于从链接上删除下划线：
    text-transform: uppercase; 属性用于指定文本中的大写和小写字母。
    text-indent 属性用于指定文本第一行的缩进
    letter-spacing 属性用于指定文本中字符之间的间距。
    text-shadow: 2px 2px 5px red;属性为文本添加阴影。
    line-height: 行间距  ：上间距、文本高度、下间距  其中 上间距=下间距
}
```

### 显示模式  display

| 元素模式                 | 元素排列                 | 设置样式               | 默认宽度         | 包含                     |
| ------------------------ | ------------------------ | ---------------------- | ---------------- | ------------------------ |
| 块级元素(block)          | 一行只能放一个块级元素   | 可以设置宽度高度       | 容器的100%       | 容器级可以包含任何标签   |
| 行级元素(inline)         | 一行可以放多个行内块元素 | 不可以直接设置宽度高度 | 它本身内容的宽度 | 容纳文本或者其他行级元素 |
| 行内块元素(inline-block) | 一行放多个行内块元素     | 它本身内容的宽度       | 它本身内容的宽度 |                          |

### 浮动 和 清除浮动 float

1. 浮动后的元素将具有  行内块 元素的性质 inline-block

2. 浮动只会影响浮动盒子后面的标准流盒子，不会影响前面  不会压住标准流文字
3. 脱离标准流后不会发生  外边距合并 
4. 一般浮动元素搭配标准流父元素
5. 清除浮动：闭合浮动，只让浮动在父盒子内部产生影响

+ 由于父级元素很多情况下不方便给高度，但是子盒子浮动又不占有位置，最后父级盒子高度为0，就会影响到下面标准流盒子

+ 额外标签发：  不常用

    ```html
    在会浮动元素末尾追加一个空的标签 必须是块级元素
    <div style="clear:both"></div>
    优点：通俗易懂，书写方便
    缺点：添加许多无意义标签，结构化比较差
    ```



### 定位 position  子绝父相

1. position:static  静态定位  （了解）

    +  和标准流一样

2. position:relative  相对定位   （重要）

    + 相对于自己原来位置移动
    + 原来在标准流的位置继续占有，不脱标，保留位置  一般给绝对定位当爹

3. position:absolute 绝对定位   (重要)

    + 如果没有祖先元素，或者组选元素没有定位，以浏览器为准定位
    + 如果祖先有定位（相对、绝对、固定），则以最近的一级祖先为准
    + 绝对定位不占有原来的位置，脱离标准流  一般放在相对定位中

4. position:fixed;  固定定位   （重要）

    + 一浏览器的可视窗口为参照点，与父元素无关，不随滚动条滚动
    + 不占有原来位置，脱离标准流

5. position:sticky;  粘性定位   (了解)

    + 可以认为是相对定位和固定定位的混合

    + 以浏览器的可是窗口为参考点移动元素
    + 粘性定位占有原先的位置
    + 必须添加top、left、right、bottom其中一个支持 
    + 跟页面滚动搭配使用，兼容性比较差，IE不适用

    ```css
    注意：
    1. 可以通过top left right bottom 配合 margin调整盒子位置
    2. 加了定位之后具有行内块元素的性质  和浮动一样
    3. 脱离标准流之后不会发生外边距合并
    4. 定位元素会压住标准流的所有东西 包括文字
    {
        //固定定位
        固定在版心右侧： left:50%;   margin-left:版心宽度一半
    }
    {
        //绝对定位  绝对定位后不能使用margin：0 auto
        居中：left:50%  margin-left:-100;
    }
    ```

    

### 元素的显示和隐藏

```css
1. display  隐藏后不占有位置
{
    display:none;  //隐藏
    display:block; //显示
}
2. visibility  隐藏后占有位置
{
    visibility:visible; //显示
    visibility:hidden;  //隐藏
}
3. overflow  隐藏后不占有位置
{
    //超出元素框的部分
    overflow:visible; //显示
    overflow:hidden;  //隐藏
    overflow:scroll;  //显示滚动条
    overflow:auto;    //超出显示滚动条，不超出不显示
}
```



### 其他/进阶技巧

```css
// 最大宽
{
    max-width: 500px;
}

//box-sizing
{
    box-sizing 属性允许我们在元素的总宽度和高度中包括内边距（填充）和边框。
}

//背景图片
{
    //位置
    background-position:top left;
    //背景固定  可以做视差滚动效果
    background-attachment:scroll/fixed;
}

//表格 边框 合并
{
    // 将表格 table td  th 的相邻边框合并
    border-collapse:collapse;
}

// 鼠标样式 cursor
{
    cursor:pointer;
}

// 表单轮廓，锁文本域
{
    //取消轮廓
    outline:none;
    //防止拖拽文本域
    resize:none;
}

//三角形
{
    width:0;
    height:0;
    border-top:10px solid transparent;//透明
    border-right:10px solid red;
    border-bottom:10px solid blue;
    border-left:10px solid green;
}

// vertical-align
{
    //设置一个元素垂直对齐的方式  只对行内元素或行内块有效
    vertical-align:baseline/top/middle/bottom;
}

//图片默认空白缝隙问题
{
    1. 给图片添加vertical-align属性（推荐）
    2. 把图片改为块级元素
    
}

//单行溢出文字显示省略号
{
    1. 先强制一行内显示文本
    white-space:nowrap;
    2. 超出部分隐藏
    overflow:hidden;
    3. 文字用省略号代替超出部分
    text-overflow:ellipsis;
}

//多行文本溢出文字显示省略号  有兼容性问题，适合于webkit浏览器或移动端
{
    overflow:hidden;
    text-overflow:ellipsis;
    //弹性伸缩盒子模型
    display:-webkit-box;
    //限制在一个块元素显示的文本的行数
    -webkit-line-clamp:2;
    //设置或检索伸缩和对象的子元素排列方式
    -webkit-box-orient:vertical;
}

//布局技巧  边框重复
{
    //解决边框1+1=2的情况
    margin-left:-1px;
    //解决移动后被压住的问题 被压住后鼠标经过事件样式无法显示，可以给事件加
    position:relative;  如果已经有定位可以加  z-index;
}

//布局技巧  文字环绕浮动
{
    标准流文字可以环绕浮动元素
    浮动元素不会压住标准流文字
}
```



## 小技巧

```html
//生成html标签
div*5
div+p
div>span
div.dv
div#dv sv
.dv$*3  //class自增：dv1 dv2 dv3    自增符号：$
div{内容}
div{$}*3 //内容自增  <div>1</div> <div>2</div> <div>3</div>
```