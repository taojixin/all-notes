# jQuery

## 一、jQuery的概念

> jQuery是一个快速、简洁的JavaScript
>
> jQuery封装了JavaScript常用的功能代码，优化了DOM操作、事件处理、动画设计和Ajax互交。
>
> 学习jQuery本质：就是学习调用这些函数（方法）
>
> jQuery出现的目的是加快前端人员的开发速度，提高开发效率。

**优点**：

* 轻量级。核心文件才几十kb，不影响页面加载速度；
* 跨浏览器兼容。基本兼容现在主流浏览器；
* 链式编程、隐式迭代；
* 对事件、样式、动画支持，大大简化了DOM操作；
* 支持插件拓展开发。有丰富的第三方的插件；
* 免费开源；

## 二、基本使用

### 1.jQuery的入口函数

> $(function (){
>
> ​	...  //此处是页面DOM加载完成的入口
>
> })

> $(document).ready(function(){
>
> ​	...  //此处是页面DOM加载完成的入口
>
> })

* 等着DOM结构渲染完毕即可执行内部代码，不必等到所有外部资源加载完成，jQuery帮我们完成了封装。
* 相当于元素JS中的DOMContentLoaded。
* 不同于原生JS中的load事件是等页面文档、外部的js文件、css文件、图片加载完毕后才执行内部代码。
* 推荐第一种方式。

```html
<body>
    <script>
        // $('div').hide();
        // 1. 等着页面DOM加载完毕再去执行js 代码
        // $(document).ready(function() {
        //     $('div').hide();
        // })
        // 2.  等着页面DOM加载完毕再去执行js 代码
        $(function() {
            $('div').hide();

        })
    </script>
    <div></div>

</body>
```

### 2.jQuery对象和DOM对象

> 使用原生JS获取来的对象就是DOM对象；
>
> jQuery方式获取的元素就是jQuery对象；
>
> jQuery对象的本质是：利用$对DOM对象进行包装后产生的对象（伪数组形式）；

```html
<body>
    <div></div>
    <span></span>
    <script>
        // 1. DOM 对象：  用原生js获取过来的对象就是DOM对象
        var myDiv = document.querySelector('div'); // myDiv 是DOM对象
        var mySpan = document.querySelector('span'); // mySpan 是DOM对象
        console.dir(myDiv);
        // 2. jQuery对象： 用jquery方式获取过来的对象是jQuery对象。 本质：通过$把DOM元素进行了包装
        $('div'); // $('div')是一个jQuery 对象
        $('span'); // $('span')是一个jQuery 对象
        console.dir($('div'));
        // 3. jQuery 对象只能使用 jQuery 方法，DOM 对象则使用原生的 JavaScirpt 属性和方法
        // myDiv.style.display = 'none';
        // myDiv.hide(); myDiv是一个dom对象不能使用 jquery里面的hide方法
        // $('div').style.display = 'none'; 这个$('div')是一个jQuery对象不能使用原生js 的属性和方法
    </script>
</body>
```

**jQuery对象和DOM对象的互相转换**：

**1.DOM对象转换为jQuery对象：$(DOM对象)**

**2.jQuery对象转换为DOM对象（两种方式）**

* $('div')[index]   index是索引号
* $('div').get(index)   index是索引号

```html
<body>
    <video src="mov.mp4" muted></video>
    <script>
        // 1. DOM对象转换为 jQuery对象
        // (1) 我们直接获取视频，得到就是jQuery对象
        // $('video');
        // (2) 我们已经使用原生js 获取过来 DOM对象
        var myvideo = document.querySelector('video');
        // $(myvideo).play();  jquery里面没有play 这个方法
        // 2.  jQuery对象转换为DOM对象
        // myvideo.play();
        $('video')[0].play()
        $('video').get(0).play()
    </script>
</body>
```

## 三、jQuery选择器

#### 1.基础选择器

> $("选择器")   //里面选择器直接写css选择器即可，但要**加引号**。

| 名称       | 用法            | 描述                     |
| ---------- | --------------- | ------------------------ |
| ID选择器   | $("#id")        | 获取指定ID的元素         |
| 全选选择器 | $("*")          | 匹配所有元素             |
| 类选择器   | $(".class")     | 获取同一类class的元素    |
| 标签选择器 | $("div")        | 获取同一类标签的所有元素 |
| 并集选择器 | $("div,p,li")   | 选取多个元素             |
| 交集选择器 | $("li.current") | 交集元素                 |

#### 2.层级选择器

| 名称       | 用法       | 描述                                                         |
| ---------- | ---------- | ------------------------------------------------------------ |
| 子代选择器 | $("ul>li") | 使用>号，获取亲儿子层级的元素；注意，并不会获取孙子层级的元素 |
| 后代选择器 | $("ul li") | 使用空格，代表后代选择器，获取ul下的所有li元素，包括孙子等   |

#### 3.筛选选择器

| 语法       | 用法          | 描述                                                    |
| ---------- | ------------- | ------------------------------------------------------- |
| :first     | $('li:first') | 获取第一个li元素                                        |
| :last      | $('li:last')  | 获取最后一个li元素                                      |
| :eq(index) | $('li:eq(2)') | 获取到的li元素，选中索引号为2的元素，索引号index从0开始 |
| :odd       | $('li:oddt')  | 获取到的li元素中，选择索引号为奇数的元素                |
| :even      | $('li:eveb')  | 获取到的li元素中，选中索引号为偶数的元素                |

```html
<body>
    <ul>
        <li>多个里面筛选几个</li>
        <li>多个里面筛选几个</li>
        <li>多个里面筛选几个</li>
        <li>多个里面筛选几个</li>
        <li>多个里面筛选几个</li>
        <li>多个里面筛选几个</li>
    </ul>
    <ol>
        <li>多个里面筛选几个</li>
        <li>多个里面筛选几个</li>
        <li>多个里面筛选几个</li>
        <li>多个里面筛选几个</li>
        <li>多个里面筛选几个</li>
        <li>多个里面筛选几个</li>
    </ol>
    <script>
        $(function() {
            $("ul li:first").css("color", "red");
            $("ul li:eq(2)").css("color", "blue");
            $("ol li:odd").css("color", "skyblue");
            $("ol li:even").css("color", "pink");
        })
    </script>
</body>
```

#### 4.筛选方法

| 语法               | 用法                           | 说明                                                   |
| ------------------ | ------------------------------ | ------------------------------------------------------ |
| parent()           | $("li").parent();              | 查找父级                                               |
| children(selector) | $("ul").children("li")         | 最近一级（亲儿子）                                     |
| find(selector)     | $("ul").find("li")             | 相当于$("ul li"),后代选择器                            |
| siblings(selector) | $(".first").siblings("li")     | 查找兄弟节点，不包括自己本身                           |
| nextAll([expr])    | $(".first").nextAll()          | 查找当前元素之后所有的同辈元素                         |
| prevtAll([expr])   | $(".last").prevAll()           | 查找当前元素之前所有的同辈元素                         |
| hasClass(class)    | $("div").hasClass("protected") | 检查当前的元素是否含有某个特定的类，如果有，则返回true |
| eq(index)          | $("li").eq(2)                  | 相当于$("li:eq(2)"),index从0开始                       |

**重点记住**：parent() children() find() siblings() eq()

```html
<body>
    <div class="yeye">
        <div class="father">
            <div class="son">儿子</div>
        </div>
    </div>

    <div class="nav">
        <p>我是屁</p>
        <div>
            <p>我是p</p>
        </div>
    </div>
    <script>
        // 注意一下都是方法 带括号
        $(function() {
            // 1. 父  parent()  返回的是 最近一级的父级元素 亲爸爸
            console.log($(".son").parent());
            // 2. 子
            // (1) 亲儿子 children()  类似子代选择器  ul>li
            // $(".nav").children("p").css("color", "red");
            // (2) 可以选里面所有的孩子 包括儿子和孙子  find() 类似于后代选择器
            $(".nav").find("p").css("color", "red");
            // 3. 兄
        });
    </script>
</body>
```

```html
<body>
    <ol>
        <li>我是ol 的li</li>
        <li>我是ol 的li</li>
        <li class="item">我是ol 的li</li>
        <li>我是ol 的li</li>
        <li>我是ol 的li</li>
        <li>我是ol 的li</li>
    </ol>
    <ul>
        <li>我是ol 的li</li>
        <li>我是ol 的li</li>
        <li>我是ol 的li</li>
        <li>我是ol 的li</li>
        <li>我是ol 的li</li>
        <li>我是ol 的li</li>
    </ul>
    <div class="current">俺有current</div>
    <div>俺木有current</div>
    <script>
        // 注意一下都是方法 带括号
        $(function() {
            // 1. 兄弟元素siblings 除了自身元素之外的所有亲兄弟
            $("ol .item").siblings("li").css("color", "red");
            // 2. 第n个元素
            var index = 2;
            // (1) 我们可以利用选择器的方式选择
            // $("ul li:eq(2)").css("color", "blue");
            // $("ul li:eq("+index+")").css("color", "blue");
            // (2) 我们可以利用选择方法的方式选择 更推荐这种写法
            // $("ul li").eq(2).css("color", "blue");
            // $("ul li").eq(index).css("color", "blue");
            // 3. 判断是否有某个类名
            console.log($("div:first").hasClass("current"));
            console.log($("div:last").hasClass("current"));


        });
    </script>
</body>
```



### 隐式迭代（重要）

> 遍历内部DOM元素（伪数组形式存储）的过程就叫做隐式迭代。
>
> 简单理解：给匹配到的所有元素进行循环遍历，执行相应的方法，而不用我们再进行循环，简化我们的操作。

```html
<body>
    <div>惊喜不，意外不</div>
    <div>惊喜不，意外不</div>
    <div>惊喜不，意外不</div>
    <div>惊喜不，意外不</div>
    <ul>
        <li>相同的操作</li>
        <li>相同的操作</li>
        <li>相同的操作</li>
    </ul>
    <script>
        // 1. 获取四个div元素 
        console.log($("div"));

        // 2. 给四个div设置背景颜色为粉色 jquery对象不能使用style
        $("div").css("background", "pink");
        // 3. 隐式迭代就是把匹配的所有元素内部进行遍历循环，给每一个元素添加css这个方法
        $("ul li").css("color", "red");
    </script>
</body>
```



### 链式编程

> $(this).css('color','red').sibling().css('color','');
>
> 链式编程是为了节省代码量，看起来优雅。

```html
<body>
    woshi body 的文字
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <script>
        $(function() {
            // 1. 隐式迭代 给所有的按钮都绑定了点击事件
            $("button").click(function() {
                // 2. 让当前元素颜色变为红色
                // $(this).css("color", "red");
                // 3. 让其余的姐妹元素不变色 
                // $(this).siblings().css("color", "");
                // 链式编程
                // $(this).css("color", "red").siblings().css("color", "");
                // 我的颜色为红色, 我的兄弟的颜色为空
                // $(this).siblings().css('color', 'red');
                // 我的兄弟变为红色  ,我本身不变颜色
                $(this).siblings().parent().css('color', 'blue');
                // 最后是给我的兄弟的爸爸 body 变化颜色 

            });
        })
    </script>
</body>
```



### 排他思想

```html
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="jquery.min.js"></script>
</head>

<body>
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <button>快速</button>
    <script>
        $(function() {
            // 1. 隐式迭代 给所有的按钮都绑定了点击事件
            $("button").click(function() {
                // 2. 当前的元素变化背景颜色
                $(this).css("background", "pink");
                // 3. 其余的兄弟去掉背景颜色 隐式迭代
                $(this).siblings("button").css("background", "");
            });
        })
    </script>
</body>

</html>
```

### 事件切换

> hover([over,]out)
>
> over：鼠标移动到元素上要触发的函数（相当于mouseenter）
>
> out：鼠标移出元素要触发的函数（相当于mouseleave）

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        
        li {
            list-style-type: none;
        }
        
        a {
            text-decoration: none;
            font-size: 14px;
        }
        
        .nav {
            margin: 100px;
        }
        
        .nav>li {
            position: relative;
            float: left;
            width: 80px;
            height: 41px;
            text-align: center;
        }
        
        .nav li a {
            display: block;
            width: 100%;
            height: 100%;
            line-height: 41px;
            color: #333;
        }
        
        .nav>li>a:hover {
            background-color: #eee;
        }
        
        .nav ul {
            display: none;
            position: absolute;
            top: 41px;
            left: 0;
            width: 100%;
            border-left: 1px solid #FECC5B;
            border-right: 1px solid #FECC5B;
        }
        
        .nav ul li {
            border-bottom: 1px solid #FECC5B;
        }
        
        .nav ul li a:hover {
            background-color: #FFF5DA;
        }
    </style>
    <script src="jquery.min.js"></script>
</head>

<body>
    <ul class="nav">
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
    </ul>
    <script>
        $(function() {
            // 鼠标经过
            // $(".nav>li").mouseover(function() {
            //     // $(this) jQuery 当前元素  this不要加引号
            //     // show() 显示元素  hide() 隐藏元素
            //     $(this).children("ul").slideDown(200);
            // });
            // // 鼠标离开
            // $(".nav>li").mouseout(function() {
            //     $(this).children("ul").slideUp(200);
            // });
            // 1. 事件切换 hover 就是鼠标经过和离开的复合写法
            // $(".nav>li").hover(function() {
            //     $(this).children("ul").slideDown(200);
            // }, function() {
            //     $(this).children("ul").slideUp(200);
            // });
            // 2. 事件切换 hover  如果只写一个函数，那么鼠标经过和鼠标离开都会触发这个函数
            $(".nav>li").hover(function() {
                $(this).children("ul").slideToggle();
            });
        })
    </script>
</body>

</html>
```







## 四、jQuery样式操作

### 1.操作css方法

* 参数只写属性名，则是放回属性值 **$(this).css("color");**
* 参数是属性名，属性值，逗号分隔，是设置一组样式，属性必须加引号，值如果是数字可以不用跟单位和引号**$(this).css("color","red")**
* 参数可以是对象形式，方便设置多组样式。属性名和属性值用冒号隔开，属性可以不用加引号 **$(this).css({"color":"red","font-size":"30px"});**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="jquery.min.js"></script>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <div></div>
    <script>
        // 操作样式之css方法
        $(function() {
            console.log($("div").css("width"));
            // $("div").css("width", "300px");
            // $("div").css("width", 300);
            // $("div").css(height, "300px"); 属性名一定要加引号
            $("div").css({
                width: 400,
                height: 400,
                backgroundColor: "red"
                    // 如果是复合属性则必须采取驼峰命名法，如果值不是数字，则需要加引号
            })
        })
    </script>
</body>

</html>
```

### 2.设置类样式方法

#### (1)添加类

> $("div").addClass("current");

#### (2)移除类

> $("div").removeClass("current");

#### (3)切换类

> $("div").toggleClass("current");

**类操作与className区别**：

* 元素js中className会覆盖元素原先里面的类名。
* jQuery里面操作只是对指定类进行操作，不影响原先的类名。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 150px;
            height: 150px;
            background-color: pink;
            margin: 100px auto;
            transition: all 0.5s;
        }
        
        .current {
            background-color: red;
            transform: rotate(360deg);
        }
    </style>
    <script src="jquery.min.js"></script>
</head>

<body>
    <div class="current"></div>
    <script>
        $(function() {
            // 1. 添加类 addClass()
            // $("div").click(function() {
            //     // $(this).addClass("current");
            // });
            // 2. 删除类 removeClass()
            // $("div").click(function() {
            //     $(this).removeClass("current");
            // });
            // 3. 切换类 toggleClass()
            $("div").click(function() {
                $(this).toggleClass("current");
            });
        })
    </script>
</body>

</html>
```



## 五、jQuery效果

### 1.显示隐藏效果

#### (1)显示效果

**语法规范**：show([speed,[easing],[fn]])

**显示参数**：

* 参数都可以省略，无动画直接显示。
* speed：三种预定速度之一的字符串（"slow","normal","fast"）或表示动画时长的毫秒数值（如：1000）。
* easing：（Optional）用来指定切换效果，默认是"swing",可用参数"linear"。
* fn：回调函数，在动画完成时执行的函数，每个元素执行一次。

#### (2)隐藏效果

**语法规范**：hide([speed,[easing],[fn]])

**隐藏参数**：

* 参数都可以省略，无动画直接显示。
* speed：三种预定速度之一的字符串（"slow","normal","fast"）或表示动画时长的毫秒数值（如：1000）。
* easing：（Optional）用来指定切换效果，默认是"swing",可用参数"linear"。
* fn：回调函数，在动画完成时执行的函数，每个元素执行一次。

#### (2)显示隐藏切换效果

**切换语法规范**：hoggle([speed,[easing],[fn]])

**切换参数**：

* 参数都可以省略，无动画直接显示。
* speed：三种预定速度之一的字符串（"slow","normal","fast"）或表示动画时长的毫秒数值（如：1000）。
* easing：（Optional）用来指定切换效果，默认是"swing",可用参数"linear"。
* fn：回调函数，在动画完成时执行的函数，每个元素执行一次。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 150px;
            height: 300px;
            background-color: pink;
        }
    </style>
    <script src="jquery.min.js"></script>
</head>

<body>
    <button>显示</button>
    <button>隐藏</button>
    <button>切换</button>
    <div></div>
    <script>
        $(function() {
            $("button").eq(0).click(function() {
                $("div").show(1000, function() {
                    alert(1);
                });
            })
            $("button").eq(1).click(function() {
                $("div").hide(1000, function() {
                    alert(1);
                });
            })
            $("button").eq(2).click(function() {
                    $("div").toggle(1000);
                })
                // 一般情况下，我们都不加参数直接显示隐藏就可以了
        });
    </script>
</body>

</html>
```

### 2.滑动效果

#### (1)下滑效果

**下滑效果语法规范**：slideDown([speed,[easing],[fn]])

**下滑效果参数**：

* 参数都可以省略，无动画直接显示。
* speed：三种预定速度之一的字符串（"slow","normal","fast"）或表示动画时长的毫秒数值（如：1000）。
* easing：（Optional）用来指定切换效果，默认是"swing",可用参数"linear"。
* fn：回调函数，在动画完成时执行的函数，每个元素执行一次。

#### (2)上滑效果

**上滑效果语法规范**：slideUp([speed,[easing],[fn]])

**上滑效果参数**：

* 参数都可以省略，无动画直接显示。
* speed：三种预定速度之一的字符串（"slow","normal","fast"）或表示动画时长的毫秒数值（如：1000）。
* easing：（Optional）用来指定切换效果，默认是"swing",可用参数"linear"。
* fn：回调函数，在动画完成时执行的函数，每个元素执行一次。

#### (3)滑动效果

**滑动切换效果语法规范**：slideToggle([speed,[easing],[fn]])

**滑动切换效果参数**：

* 参数都可以省略，无动画直接显示。
* speed：三种预定速度之一的字符串（"slow","normal","fast"）或表示动画时长的毫秒数值（如：1000）。
* easing：（Optional）用来指定切换效果，默认是"swing",可用参数"linear"。
* fn：回调函数，在动画完成时执行的函数，每个元素执行一次。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 150px;
            height: 300px;
            background-color: pink;
            display: none;
        }
    </style>
    <script src="jquery.min.js"></script>
</head>

<body>
    <button>下拉滑动</button>
    <button>上拉滑动</button>
    <button>切换滑动</button>
    <div></div>
    <script>
        $(function() {
            $("button").eq(0).click(function() {
                // 下滑动 slideDown()
                $("div").slideDown();
            })
            $("button").eq(1).click(function() {
                // 上滑动 slideUp()
                $("div").slideUp(500);


            })
            $("button").eq(2).click(function() {
                // 滑动切换 slideToggle()

                $("div").slideToggle(500);

            });

        });
    </script>
</body>

</html>
```

### 3.自定义动画animate

**语法**：animate(params,[speed,[easing],[fn])

**参数**：

* params：想要更改的样式属性，以对象形式传递，必须写。属性名可以不用带引号，如果是符合属性则需要采取驼峰命名法borderLeft。

* speed：三种预定速度之一的字符串（"slow","normal","fast"）或表示动画时长的毫秒数值（如：1000）。
* easing：（Optional）用来指定切换效果，默认是"swing",可用参数"linear"。
* fn：回调函数，在动画完成时执行的函数，每个元素执行一次。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="jquery.min.js"></script>
    <style>
        div {
            position: absolute;
            width: 200px;
            height: 200px;
            background-color: pink;
        }
    </style>
</head>

<body>
    <button>动起来</button>
    <div></div>
    <script>
        $(function() {
            $("button").click(function() {
                $("div").animate({
                    left: 500,
                    top: 300,
                    opacity: .4,
                    width: 500
                }, 500);
            })
        })
    </script>
</body>

</html>
```



### 4.动画队列及其停止排队方法

> 动画或者特效一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行。

**停止排队**：stop()

* stop()方法用于停止动画或效果。
* 注意：stop()写到动画或者效果的前面，相当于停止结束上一次动画。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        * {
            margin: 0;
            padding: 0;
        }
        
        li {
            list-style-type: none;
        }
        
        a {
            text-decoration: none;
            font-size: 14px;
        }
        
        .nav {
            margin: 100px;
        }
        
        .nav>li {
            position: relative;
            float: left;
            width: 80px;
            height: 41px;
            text-align: center;
        }
        
        .nav li a {
            display: block;
            width: 100%;
            height: 100%;
            line-height: 41px;
            color: #333;
        }
        
        .nav>li>a:hover {
            background-color: #eee;
        }
        
        .nav ul {
            display: none;
            position: absolute;
            top: 41px;
            left: 0;
            width: 100%;
            border-left: 1px solid #FECC5B;
            border-right: 1px solid #FECC5B;
        }
        
        .nav ul li {
            border-bottom: 1px solid #FECC5B;
        }
        
        .nav ul li a:hover {
            background-color: #FFF5DA;
        }
    </style>
    <script src="jquery.min.js"></script>
</head>

<body>
    <ul class="nav">
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
        <li>
            <a href="#">微博</a>
            <ul>
                <li>
                    <a href="">私信</a>
                </li>
                <li>
                    <a href="">评论</a>
                </li>
                <li>
                    <a href="">@我</a>
                </li>
            </ul>
        </li>
    </ul>
    <script>
        $(function() {
            // 鼠标经过
            // $(".nav>li").mouseover(function() {
            //     // $(this) jQuery 当前元素  this不要加引号
            //     // show() 显示元素  hide() 隐藏元素
            //     $(this).children("ul").slideDown(200);
            // });
            // // 鼠标离开
            // $(".nav>li").mouseout(function() {
            //     $(this).children("ul").slideUp(200);
            // });
            // 1. 事件切换 hover 就是鼠标经过和离开的复合写法
            // $(".nav>li").hover(function() {
            //     $(this).children("ul").slideDown(200);
            // }, function() {
            //     $(this).children("ul").slideUp(200);
            // });
            // 2. 事件切换 hover  如果只写一个函数，那么鼠标经过和鼠标离开都会触发这个函数
            $(".nav>li").hover(function() {
                // stop 方法必须写到动画的前面
                $(this).children("ul").stop().slideToggle();
            });
        })
    </script>
</body>

</html>
```



## 六、jQuery属性操作

### 1.设置或获取元素固有属性

> 所谓元素固有属性就是元素本身自带的属性，比如< a>元素里面的href

**获取属性语法**：prop("属性")

**设置属性语法**：prop("属性","属性值")

### 2.设置或获取元素自定义属性值 attr()

**获取属性语法**：attr("属性")  //类似元素getAttribute()

**设置属性语法**：attr("属性","属性值")  //类似元素setAttribute()

### 3.数据缓存 data()

> data()方法可以在指定的元素上存取数据，并不会修改DOM元素结构。一旦页面刷新，之后存放的数据都将被移除。

**附加数据语法**：data("name","value")  //向被选元素附加数据

**获取数据语法**：data("name")  //向被选元素获取数据

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="jquery.min.js"></script>
</head>

<body>
    <a href="http://www.itcast.cn" title="都挺好">都挺好</a>
    <input type="checkbox" name="" id="" checked>
    <div index="1" data-index="2">我是div</div>
    <span>123</span>
    <script>
        $(function() {
            //1. element.prop("属性名") 获取元素固有的属性值
            console.log($("a").prop("href"));
            $("a").prop("title", "我们都挺好");
            $("input").change(function() {
                console.log($(this).prop("checked"));

            });
            // console.log($("div").prop("index"));
            // 2. 元素的自定义属性 我们通过 attr()
            console.log($("div").attr("index"));
            $("div").attr("index", 4);
            console.log($("div").attr("data-index"));
            // 3. 数据缓存 data() 这个里面的数据是存放在元素的内存里面
            $("span").data("uname", "andy");
            console.log($("span").data("uname"));
            // 这个方法获取data-index h5自定义属性 第一个 不用写data-  而且返回的是数字型
            console.log($("div").data("index"));





        })
    </script>
</body>

</html>
```



## 七、jQuery文本属性值

### 1.普通元素内容 html()

> 相当于元素innerHTML

html()  //获取元素内容

html("内容")  //设置元素内容

### 2.普通元素文本内容text()

> 相当于元素innerText

text()  //获取元素的文本内容

text("文本内容")  //设置元素的文本内容

### 3.表单的值val() 

> 相当于元素value

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="jquery.min.js"></script>
</head>

<body>
    <div>
        <span>我是内容</span>
    </div>
    <input type="text" value="请输入内容">
    <script>
        // 1. 获取设置元素内容 html()
        console.log($("div").html());
        // $("div").html("123");
        // 2. 获取设置元素文本内容 text()
        console.log($("div").text());
        $("div").text("123");

        // 3. 获取设置表单值 val()
        console.log($("input").val());
        $("input").val("123");
    </script>
</body>

</html>
```



## 八、jQuery元素操作

### 1.遍历元素

> jQuery隐式迭代是对同一类元素做了同样的操作。如果想要给同一类元素做不同操作，就需要遍历。

**语法1**：$("div").sech(function (index, domEle ) {})

* each()方法遍历比配的每一个元素，只要用DOM处理；
* 里面的回调函数有2个参数：index是每个元素索引号；demEle是每个DOM元素对象，不是jQuery对象
* 所有要想使用jQuery方法，需要给这个dom元素转换为jQuery对象$(domEle)

**语法2**：$.each(object, function (index, element ) {} )

* $.each()方法可以用于遍历任何对象。主要用于数据处理，比如数值，对象
* 里面的函数有2个参数：index是每个元素的索引号；element遍历内容

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>

    </style>
    <script src="jquery.min.js"></script>
</head>

<body>
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <script>
        $(function() {
            // $("div").css("color", "red");
            // 如果针对于同一类元素做不同操作，需要用到遍历元素（类似for，但是比for强大）
            var sum = 0;
            // 1. each() 方法遍历元素 
            var arr = ["red", "green", "blue"];
            $("div").each(function(i, domEle) {
                // 回调函数第一个参数一定是索引号  可以自己指定索引号号名称
                // console.log(index);
                // console.log(i);
                // 回调函数第二个参数一定是 dom元素对象 也是自己命名
                // console.log(domEle);
                // domEle.css("color"); dom对象没有css方法
                $(domEle).css("color", arr[i]);
                sum += parseInt($(domEle).text());
            })
            console.log(sum);
            // 2. $.each() 方法遍历元素 主要用于遍历数据，处理数据
            // $.each($("div"), function(i, ele) {
            //     console.log(i);
            //     console.log(ele);

            // });
            // $.each(arr, function(i, ele) {
            //     console.log(i);
            //     console.log(ele);


            // })
            $.each({
                name: "andy",
                age: 18
            }, function(i, ele) {
                console.log(i); // 输出的是 name age 属性名
                console.log(ele); // 输出的是 andy  18 属性值


            })
        })
    </script>
</body>

</html>
```

### 2.创建元素

**语法**：$("< li>< /li>")   动态的创建了一个< li>

### 3.添加元素

#### 内部添加

* 把内容放入匹配元素内部最**后面**：element.append("内容")
* 把内容放到匹配元素内部最**前面**：elemenet.prepend("内容")

#### 外部添加

* 把内容放入目标元素后面：element.after("内容")   生成之后，它们是父子关系
* 把内容放入目标元素前面：element.before("内容")   生成之后，它们是兄弟关系

### 4.删除元素

* 删除匹配的元素（本身）：element.remove()
* 删除匹配的元素集合中所有的子节点：element.empty()
* 清空匹配的元素内容：element.html("")

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <script src="jquery.min.js"></script>
</head>

<body>
    <ul>
        <li>原先的li</li>
    </ul>
    <div class="test">我是原先的div</div>
    <script>
        $(function() {
            // 1. 创建元素
            var li = $("<li>我是后来创建的li</li>");
            // 2. 添加元素

            // (1) 内部添加
            // $("ul").append(li);  内部添加并且放到内容的最后面 
            $("ul").prepend(li); // 内部添加并且放到内容的最前面

            // (2) 外部添加
            var div = $("<div>我是后妈生的</div>");
            // $(".test").after(div);
            $(".test").before(div);
            // 3. 删除元素
            // $("ul").remove(); 可以删除匹配的元素 自杀
            // $("ul").empty(); // 可以删除匹配的元素里面的子节点 孩子
            $("ul").html(""); // 可以删除匹配的元素里面的子节点 孩子

        })
    </script>
</body>

</html>
```



## 九、jQuery尺寸操作

| 语法                               | 用法                                                 |
| ---------------------------------- | ---------------------------------------------------- |
| width()/height()                   | 取得匹配元素宽度和高度值 只算width/height            |
| innerWidth()/innerHieght()         | 取得匹配元素宽度和高度值 包含padding                 |
| outerWidth()/outerHeight()         | 取得匹配元素宽度和高度值 包含padding、border         |
| outerWidth(true)/outerHeight(true) | 取得匹配元素宽度和高度值 包含padding、border、margin |

* 以上参数为空，则是获取相应值，返回的是数字型。
* 如果参数为数值，则是修改相应值。
* 参数可以不写单位。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 200px;
            height: 200px;
            background-color: pink;
            padding: 10px;
            border: 15px solid red;
            margin: 20px;
        }
    </style>
    <script src="jquery.min.js"></script>
</head>

<body>
    <div></div>
    <script>
        $(function() {
            // 1. width() / height() 获取设置元素 width和height大小 
            console.log($("div").width());
            // $("div").width(300);

            // 2. innerWidth() / innerHeight()  获取设置元素 width和height + padding 大小 
            console.log($("div").innerWidth());

            // 3. outerWidth()  / outerHeight()  获取设置元素 width和height + padding + border 大小 
            console.log($("div").outerWidth());

            // 4. outerWidth(true) / outerHeight(true) 获取设置 width和height + padding + border + margin
            console.log($("div").outerWidth(true));


        })
    </script>
</body>

</html>
```



## 十、jQuery位置操作

### 1.offse()设置或获取元素偏移

* offset()方法设置或返回被选元素相对于文档的偏移坐标，跟父级没有关系。
* 该方法有2个属性left、top，offset().top用于获取距离文档顶部的距离，offset().left用于获取距离文档左侧的距离。
* 可以设置元素的偏移：offset({top:20,left:30});

### 2.position() 获取元素偏移

* position()方法用于返回被选元素相对于带有定位的父级偏移坐标，如果父级都没有定位，则以文档为准。

```html
<body>
    <div class="father">
        <div class="son"></div>
    </div>
    <script>
        $(function() {
            // 1. 获取设置距离文档的位置（偏移） offset
            console.log($(".son").offset());
            console.log($(".son").offset().top);
            // $(".son").offset({
            //     top: 200,
            //     left: 200
            // });
            // 2. 获取距离带有定位父级位置（偏移） position   如果没有带有定位的父级，则以文档为准
            // 这个方法只能获取不能设置偏移
            console.log($(".son").position());
            // $(".son").position({
            //     top: 200,
            //     left: 200
            // });
        })
    </script>
</body>
```

### 3.scrollTop()/scrollLeft() 设置或获取元素被卷去的头部和左侧

* scrollTop()方法设置或返回被选元素被卷去的头部。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        body {
            height: 2000px;
        }
        
        .back {
            position: fixed;
            width: 50px;
            height: 50px;
            background-color: pink;
            right: 30px;
            bottom: 100px;
            display: none;
        }
        
        .container {
            width: 900px;
            height: 500px;
            background-color: skyblue;
            margin: 400px auto;
        }
    </style>
    <script src="jquery.min.js"></script>
</head>

<body>
    <div class="back">返回顶部</div>
    <div class="container">
    </div>
    <script>
        $(function() {
            $(document).scrollTop(100);
            // 被卷去的头部 scrollTop()  / 被卷去的左侧 scrollLeft()
            // 页面滚动事件
            var boxTop = $(".container").offset().top;
            $(window).scroll(function() {
                // console.log(11);
                console.log($(document).scrollTop());
                if ($(document).scrollTop() >= boxTop) {
                    $(".back").fadeIn();
                } else {
                    $(".back").fadeOut();
                }
            });
            // 返回顶部
            $(".back").click(function() {
                // $(document).scrollTop(0);
                $("body, html").stop().animate({
                    scrollTop: 0
                });
                // $(document).stop().animate({
                //     scrollTop: 0
                // }); 不能是文档而是 html和body元素做动画
            })
        })
    </script>
</body>

</html>
```



## 十一、jQuery事件

### 1.jQuery事件注册

**单个事件注册**：

element.事件(function() {})

$("div").click(function) { 事件处理程序 }

### 2.jQuery事件处理

#### on() 绑定事件

> on() 方法在匹配元素上绑定一个或多个事件的事件处理函数

**on() 绑定事件**：element.on(event,[selector],fn)

* events：一个或多个用空格分隔的事件类型，如"click"或"keydown"。
* selector：元素的子元素选择器。
* fn：回调函数 即绑定在元素身上的监听函数。

**on() 方法优势1**：可以绑定多个事件，处理多个事件处理程序。

**on() 方法优势 2**：可以事件委派操作。事件委派的定义就是，把原来加给子元素身上的事件绑定在父元素身上，就是把事件委派给父元素。

**on() 方法优势 3**：动态创建元素，click()没有办法绑定事件，on()可以动态生成的元素绑定事件。

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }
        
        .current {
            background-color: purple;
        }
    </style>
    <script src="jquery.min.js"></script>
</head>

<body>
    <div></div>
    <ul>
        <li>我们都是好孩子</li>
        <li>我们都是好孩子</li>
        <li>我们都是好孩子</li>
        <li>我们都是好孩子</li>
        <li>我们都是好孩子</li>
    </ul>
    <ol>

    </ol>
    <script>
        $(function() {
            // 1. 单个事件注册
            // $("div").click(function() {
            //     $(this).css("background", "purple");
            // });
            // $("div").mouseenter(function() {
            //     $(this).css("background", "skyblue");
            // });

            // 2. 事件处理on
            // (1) on可以绑定1个或者多个事件处理程序
            // $("div").on({
            //     mouseenter: function() {
            //         $(this).css("background", "skyblue");
            //     },
            //     click: function() {
            //         $(this).css("background", "purple");
            //     },
            //     mouseleave: function() {
            //         $(this).css("background", "blue");
            //     }
            // });
            $("div").on("mouseenter mouseleave", function() {
                $(this).toggleClass("current");
            });
            // (2) on可以实现事件委托（委派）
            // $("ul li").click();
            $("ul").on("click", "li", function() {
                alert(11);
            });
            // click 是绑定在ul 身上的，但是 触发的对象是 ul 里面的小li
            // (3) on可以给未来动态创建的元素绑定事件
            // $("ol li").click(function() {
            //     alert(11);
            // })
            $("ol").on("click", "li", function() {
                alert(11);
            })
            var li = $("<li>我是后来创建的</li>");
            $("ol").append(li);
        })
    </script>
</body>

</html>
```

#### off() 解绑事件

> off() 方法可以移除通过on() 方法添加的事件处理程序。

* 解绑p元素所有事件处理程序：$("p").off()
* 解绑p元素上面的点击事件 后面的是监听函数名：$("p").off("click")
* 解绑事件委托：$("ul").off("click","li")

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }
    </style>
    <script src="jquery.min.js"></script>
    <script>
        $(function() {
            $("div").on({
                click: function() {
                    console.log("我点击了");
                },
                mouseover: function() {
                    console.log('我鼠标经过了');
                }
            });
            $("ul").on("click", "li", function() {
                alert(11);
            });
            // 1. 事件解绑 off 
            // $("div").off();  // 这个是解除了div身上的所有事件
            $("div").off("click"); // 这个是解除了div身上的点击事件
            $("ul").off("click", "li");
            // 2. one() 但是它只能触发事件一次
            $("p").one("click", function() {
                alert(11);
            })
        })
    </script>
</head>

<body>
    <div></div>
    <ul>
        <li>我们都是好孩子</li>
        <li>我们都是好孩子</li>
        <li>我们都是好孩子</li>
    </ul>
    <p>我是屁</p>
</body>

</html>
```

#### trigger() 自动触发事件

> 有些事件希望自动触发，比如轮播图自动播放功能跟点击右键按钮一致。可以利用定时器自动触发右侧按钮点击事件，不必鼠标点击触发。

**语法格式**：

* element.trigger("type")
* element.triggerHandler(type)

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }
    </style>
    <script src="jquery.min.js"></script>
    <script>
        $(function() {
            $("div").on("click", function() {
                alert(11);
            });

            // 自动触发事件
            // 1. 元素.事件()
            // $("div").click();会触发元素的默认行为
            // 2. 元素.trigger("事件")
            // $("div").trigger("click");会触发元素的默认行为
            $("input").trigger("focus");
            // 3. 元素.triggerHandler("事件") 就是不会触发元素的默认行为
            $("div").triggerHandler("click");
            $("input").on("focus", function() {
                $(this).val("你好吗");
            });
            // $("input").triggerHandler("focus");

        });
    </script>
</head>

<body>
    <div></div>
    <input type="text">
</body>

</html>
```

### 3.事件对象

> 事件触发，就会有事件对象的产生。

* element.on(events,[selector],function(event) {} )

**阻止默认行为**：event.preventDefaule() 或 return false

**阻止冒泡**：event.stopPropagation()

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
    <style>
        div {
            width: 100px;
            height: 100px;
            background-color: pink;
        }
    </style>
    <script src="jquery.min.js"></script>
    <script>
        $(function() {
            $(document).on("click", function() {
                console.log("点击了document");

            })
            $("div").on("click", function(event) {
                // console.log(event);
                console.log("点击了div");
                event.stopPropagation();
            })
        })
    </script>
</head>

<body>
    <div></div>
</body>

</html>
```

