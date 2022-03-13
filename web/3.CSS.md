[TOC]

## CSS基础

### 一、CSS样式插入

**1.外部样式**：

```html
<head>
<link rel="stylesheet" type="text/css" href="mystyle.css">
</head>
```

**2.内部样式**：

```html
<head>
	<style>
		hr {color:sienna;}
		p {margin-left:20px;}
		body {background-image:url("images/back40.gif");}
	</style>
</head>
```

**3.内联样式**：

```html
<p style="color:sienna;margin-left:20px">这是一个段落。</p>
```

**多重样式优先级**：一般情况下，优先级如下：

（内联样式）Inline style > （内部样式）Internal style sheet >（外部样式）External style sheet > 浏览器默认样式

---------



### 二、常用选择器

#### 1.基本选择器
**1.通配选择器**

> 在开发测试阶段固然是好的，但是我不建议这么做，因为这样做会给浏览器增加很大的负担。

```html
* {
 margin: 0;
 padding: 0;
}
```

**2.ID选择器**

```html
#container {
 width: 960px;
 margin: auto;
}
```

**3.类选择器**

```html
.error {
	color: red;
}
```

**4.后代选择器**

```html
li a {
	text-decoration: none;
}
```

**5.元素选择器**

```html
a { color: red; }
ul { margin-left: 0; }
```

#### 2.结构伪类选择器

| 选择符                  | 简介                                                 |
| ----------------------- | ---------------------------------------------------- |
| E:first-child           | 选择父元素的第一个子元素                             |
| E:last-child            | 选择父元素的倒数第一个子元素                         |
| E:nth-child(n)          | 选择父元素的第n个子元素                              |
| E:nth-last-child        | 选择父元素的倒数第n个子元素                          |
| F E:first-of-type       | 选择父元素F中的第一个E元素                           |
| F E:last-of-type        | 选择父元素F中的倒数第一个E元素                       |
| F E:nth-of-type(n)      | 选择父元素F中的第n个E元素                            |
| F E:nth-last-of-type(n) | 选择父元素F中的倒数第n个E元素                        |
| E:empty                 | 选择没有子元素的元素，而且该元素也不包含任何文本节点 |

**注**：

1.n可以是关键字，even偶数，odd奇数

2.n可以是公式：2n偶数 2n+1奇数 5n(5,10,15···)

3.n从1开始

#### 3.属性选择器

| 选择符        | 简                                    |
| ------------- | ------------------------------------- |
| E[att]        | 选择具有att属性的E元素                |
| E[att="val"]  | 选择具有att属性且属性值等于val的E元素 |
| E[att^="val"] | 选择具有att属性且以val开头的E元素     |
| E[att$="val"] | 选择具有att属性且以val结尾的E元素     |
| E[att*="val"] | 选择具有att属性且值中含有val的E元素   |

#### 4.伪元素选择器

> 伪元素选择器可以帮助我们利用CSS创建新标签元素，为不需要html标签，从而简化html结构。

| 选择符   | 简介                     |
| -------- | ------------------------ |
| ::before | 在元素内部的前面插入内容 |
| ::after  | 在元素内部的后面插入内容 |

**注**：

1.before和after创建一个元素，但都属于**行内元素**

2.这个元素在**文档中找不到**，故称**伪元素**

3.before和after**必须有content属性**

4.权重为1

**应用场景**：伪元素字体图标

#### 5.层次选择器

**1.子选择器**

```HTML
body>p {
	background:red;
}
只有body后面的p标签会改变样式
```

只有与body元素有**直接关系（父子关系）的元素才会被变色**，如果是后代选择器，**body中的其他标签**若有p标签，**其他标签中的p标签也会变色**，这也是子选择器与后代选择器的区别

**2.相邻兄弟选择器**

```html
.a + .b{
    
}
向下改变
```

只改变a标签的下一个相邻的b标签，若下一个相邻的标签不是b标签，则不改变，即使下下一个是b标签，也不改变，只改变相邻的。

**3.通用选择器**

```html
.a ~ .b{
	background-color: red;
}
```

和相邻兄弟标签相似，改变a标签**之后**的**所有**的**兄弟关系**的**b标签**，a标签**之前**的兄弟b标签**不改变**。

------



### 三、字体（font）

#### 1.font-family

> 指定文本的字体

```html
body {
	font-family:'Microsoft YaHei',tohoma,···;
}
```

#### 2.font-size

单位可以是px,em,%等

#### 3.font-weight

> 字体粗细

**值**：

**nornal**:不加粗（默认值）

**bold**:粗体

**100-900**(不加单位px)

```html
p.thicker {font-weight:900;}
```

#### 4.font-style

**值**：

normal: 标准样式（默认值）

italic:斜体

#### 5.复合写法

font:font-sytle font-weighr font-size font-family;

**注**：**不可省略**size和family，若省略了font整行无效。尽可能**不交换顺序**，否则font正好代码无效，不便寻找错误。

----------



### 四、文本（text）

#### 1.颜色(color)

color:red;

color:#ffffff;

color:rgb(255,0,0);

#### 2.对齐文本(text-align)

left:左对齐

right:右对齐

center:居中

#### 3.修饰文本(text-decoration)

none:默认（常用，可用于去除超链接下划线）

underline:下划线

overline:上划线（几乎不用）

line-through:删除线

blink:定义闪烁的文本

#### 4.文本缩进(text-indent)

单位%，em(相当于当前元素的文字大小)，

#### 5.文本方向(direction)

ltr:默认，文本从左到右

rtl:文本从右左

#### 6.行高(line-height)

行间距=上间距+文本高度+下间距

单位px

#### 7.阴影文本(text-shadow)

h-shadow:必须。水平阴影的位置，可以负值

v-shadow:必须。垂直阴影的位置，可以负值

blur:可选。模糊距离

color:可选。阴影的颜色

---------



### 五、背景

#### 1.背景颜色

background-color:

#### 2.背景图片

background-image:none | url();

#### 3.背景平铺

background-repeat: repeat | no-repeat;

#### 4.背景图片位置

background-position: x y;

单位可以是精确单位，如%，浮点数字；也可以是方位词(top,bottom,left,right,center)

#### 5.背景图像固定

background-attachment: scroll | fixed;

scroll:随对象内容滚动

fixed:固定

#### 6.背景复合写法

background: transparent url() repeat fixed top;

背景颜色半透明：rgba(0,0,0,0.2)

----------



### 六、链接修饰

#### 1.a:link

未访问的链接

#### 2.a:visited

已访问的链接

#### 3.a:hover

当用户鼠标放在链接上时

#### 4.a:avtive

链接被点击的那一刻

------------



### 七、边框

#### 基本概念

border-width:边框粗细，单位px

border-color:边框颜色

border-style:边框样式 solid(实线) dashed(虚线) double(双线边框) dotted(点线边框)

**边框简写**：没有顺序

**边框分开写**：border-top: 1px solid red;

#### 圆角边框

border-radio:length;

**注**：

1.参数可以是**数值或者百分比**的形式

2.可简写，跟四值，分别：左上角，右上角，右下角，左下角；

3.分开写: border-top-left-radios  border-bottom-right-radios；

4.如果是**正方形**，想要设置为一个**圈**，把**数值**修改为**高度**或者**宽度**的**一半**即可，或者直接写**50%**

5.如果是**矩形**，设置为**高度**的**一半**就可以

------------



### 八、边距

#### 内边距(padding)

**简写**：

| 代码                         | 简介                                 |
| ---------------------------- | ------------------------------------ |
| padding: 5px;                | 上下左右：5px                        |
| padding: 10px 5px;           | 上下：10px；左右：5px；              |
| padding: 5px 10px 20px;      | 上：5px；左右：10px；下：20px；      |
| padding: 5px 10px 20px 30px; | 上下左右分别为：5px,10px,20px,30px； |

#### 外边距(margin)

**简写方式和padding一致**

典型应用：让块级盒子水平居中

**常见写法**：

margin-left: left;margin-right: auto;

margin:auto;

margin: 0 auto;

---------



### 九、显示与隐藏

#### 1.display属性

display:none;隐藏对象

display:block;显示对象，还有转换成块元素的作用

**注**：display隐藏元素后，**不再占有原来的位置**

#### 2.visibility可见性

visibility:visible;可视

visibility:hidden;隐藏

**注**：visibility隐藏元素后**继续占有原来的位置**

#### 3.overflow溢出

| 属性值  | 简介                                   |
| ------- | -------------------------------------- |
| visible | 不剪切内容也不添加滚动条               |
| hidden  | 不显示超过对象尺寸的内容，超出部分隐藏 |
| scroll  | 不管超出内容与否，总是显示滚动条       |
| auto    | 超出自动显示滚动条，不超出不显示滚动条 |

**注**：如果盒子有定位，慎用overflow:hidden因为它会隐藏多余的部分

#### 嵌套块级元素垂直外边距的塌陷问题

**解决方案：**

（1）为父元素定义上边框

（2）为父元素定义内边距

（3）为父元素添加overflow:hedden;







## CSS三大特性

### 一、层叠性

> 层叠性是指多种CSS样式的叠加。
>
> 如果一个属性通过两个相同选择器设置到同一个元素上，那么这个时候一个属性就会将另一个属性层叠掉。

**层叠性原则**：

1.样式冲突：就近原则，那个样式离结构近，就执行哪个样式。

2.样式不冲突：不会层叠。

### 二、继承性

> 给父元素设置一些属性, 子元素也可以使用, 这个我们就称之为继承性。

- 不是所有元素都有继承性，只有以**color/font-/text-/line-**开头的属性才可以继承
- 在CSS的继承中不仅仅是儿子可以继承, 只要是**后代都可以继承**
- **a标签**的**文字颜色**和**下划线**是不能继承的
- **h标签的文字大小**是不能继承的
- 继承性一般用于设置网页上的公共信息，例如网页文字颜色、字体以及大小等
- 伪元素，伪类这些设置不能继承
-  **块元素**可以继承父级元素的**宽度**，**高度不继承** 

转载于:https://www.cnblogs.com/cowboybusy/p/11459004.html

### 三、优先级

| 选择器               | 权重       |
| -------------------- | ---------- |
| 继承或*              | 0，0，0，0 |
| 元素选择器           | 0，0，0，1 |
| 类选择器，伪类选择器 | 0，0，1，0 |
| ID选择器             | 0，1，0，0 |
| 行内样式 style=""    | 1，0，0，0 |
| ！important 重要的   | 最大       |

**注**：

1.继承的权重是0，如果该元素没有直接选中，不管父元素权重多高，子元素得到的权重都是0；

2.权重会叠加，eg：

div ul li---0,0,0,3

.nav ul li---0,0,1,2

a:hover---0,0,1,1

.nav a---0,0,1,1
