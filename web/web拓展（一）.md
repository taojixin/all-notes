# web拓展（一）

## 一、精灵图的使用

**注**：

1.主要借助于背景位置来实现 background-position；

2.一般情况下精灵图是负值；

3.使用精灵图的时候需要精确测量每个图片的大小和位置。

## 二、字体图标

### 下载

icomoon字库 http://icomoon.io

阿里iconfont字库 http://www.iconfont/

### 引入

1.将下载后的压缩包**解压后**将**文件fonts**复制到**html同目录文件中**；

2.在CSS样式中全局声明字体(**直接复制就好**)

```html
 <style>
    @font-face {
  font-family: 'icomoon';
  src:  url('../fonts/icomoon.eot?tomleg');
  src:  url('../fonts/icomoon.eot?tomleg#iefix') format('embedded-opentype'),
    url('../fonts/icomoon.ttf?tomleg') format('truetype'),
    url('../fonts/icomoon.woff?tomleg') format('woff'),
    url('../fonts/icomoon.svg?tomleg#icomoon') format('svg');
  font-weight: normal;
  font-style: normal;
  font-display: block;
}
<style/>
```

3.打开压缩后的**demo.html文件**选中图表字体然后复制黏贴到html代码中**(font-family和content属性不可省略)**

```html
div::before {
      	font-family: "icomoon";  
		content: "\e91b";
      	font-size: 100px;
      	color: hotpink;

   }
```

## 三、CSS三角

### 基础

```html
<style>
    div {
        width: 0;
        height: 0;
        line-height: 0;
        font-size: 0;
        border: 50px solid transparent;
        border-left-color: pink;
    }
</style>
```

### 强化

```html
<style>
    div {
        width: 0;
        height: 0;
        border-color: transparent red transparent transparent;
        border-style: solid;
        border-width: 22px 8px 0 0;
    }
</style>
```



## 四、溢出文字显示省略号

### 单号文本显示省略号

**注**：必须满足三个条件

```html
<style>
    选择器 {
        white-space: nowrap;		/*先强制一行内显示文本*/
        overflow: hidden;			/*超出部分隐藏*/
        text-overflow: ellipsis;	/*文本用省略号代替超出部分*/
    }
</style>
```

### 多行文本溢出显示省略号

```html
<style>
    选择器 {
        overflow: hidden;			/*超出部分隐藏*/
        text-overflow: ellipsis;	/*文本用省略号代替超出部分*/
        -webkit-line-clamp: 2;		/*限制在一个块元素显示的文本行数*/
        -webkit-box-orient: vertical;
    }
</style>
```



## 五、margin负值运用

> 用于一些商品li标签

1.让每个盒子margin往左移动-1px，正好压住相邻盒子边框

2.鼠标经过某个盒子时，提高当前盒子的层级（如果没有定位，则加相对定位保留位置，如果有定位，则加z-index）

## 六、文字环绕（浮动）

**原理**：浮动不会压住下面标准流文字内容。

## 七、行内块元素的巧妙运用

给行内块元素的父盒子添加text-align: center;所有行内块元素则会在父元素中水平居中

## 八、CSS初始化

## 九、盒子阴影

**语法**：box-shadow: h-shadow v-shadow blur apread color inset;

**属性**：

* h-shadow：必须。水平阴影位置。运行负值
* v-shadow：必须。垂直阴影位置。允许负值
* blur：可选。迷糊距离
* spread：可选。阴影尺寸
* color：可选。阴影颜色
* inset：可选。将外部阴影改为内部阴影

**注**：

1.默认的是外部阴影(outset)，但是不可以写这个单词，否则导致阴影无效，此属性直接省略默认即可。

2.盒子阴影不占用空间，不会影响其他盒子排列

## 十、CSS用户界面样式

### 1.鼠标样式cursor

```html
<style>
    li {
        cursor: pointer;
    }
</style>
```

| 属性        | 简介 |
| ----------- | ---- |
| default     | 默认 |
| pointer     | 小手 |
| move        | 移动 |
| text        | 文本 |
| not-allowed | 禁止 |

### 2.轮廓线outline

> 给表单添加outline: 0;或outline: none;之后，就可以去掉默认的蓝色边框

```html
<style>
    li {
        outline: none;
    }
</style>
```

### 3.防止拖拽文本域resize

> 实际开发中，我们文本域右下角是不可拖拽的

```html
<style>
    textarea {
        resize: none;
    }
</style>
```

