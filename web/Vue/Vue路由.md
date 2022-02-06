## 一、安装vue-router

`npm install vue-router`

## 二、创建Vue实例

> 在模块化工程中使用它(因为是一个插件, 所以可以通过Vue.use()来安装路由功能)

### 0.首先

> **在src目录下创建router文件夹，里面创建文件index.js。**
>
> 在**index.js文件中**配置路由相关信息并创建路由。

![image-20220107141956037](D:\Typora笔记\web\Vue\image\image-20220107141956037.png)



### 1.第一步

> 通过Vue.use(插件),安装插件

### 2.第二步

> 创建VueRouter对象

### 3.第三步

> 将router对象传入Vue实例，并在Vue实例(main.js)中挂载创建的路由实例

![image-20220107143158957](D:\Typora笔记\web\Vue\image\创建VueRouter实例.png)

![image-20220107143921874](D:\Typora笔记\web\Vue\image\挂载路由.png)



## 三、创建路由组件

> 在components文件夹中创建  **.vue**  的路由组件。

![image-20220107144307739](D:\Typora笔记\web\Vue\image\路由组件1.png)

![image-20220107144415312](D:\Typora笔记\web\Vue\image\路由组件2.png)

![image-20220107144444508](D:\Typora笔记\web\Vue\image\路由组件3.png)



## 四、配置组件和路径的映射关系

![image-20220107144715565](D:\Typora笔记\web\Vue\image\关系.png)



## 五、使用路由

> 在App.vue文件模板中使用路由标签，在main.js文件中引入router。

**注**：

* **< router-link>**: 该标签是一个vue-router中已经内置的组件, 它会被渲染成一个< a>标签.
* **< router-view>**: 该标签会根据当前的路径, 动态渲染出不同的组件.
* 网页的其他内容, 比如顶部的标题/导航, 或者底部的一些版权信息等会和< router-view>处于同一个等级.
* 在路由切换时, 切换的是< router-view>挂载的组件, **其他内容不会发生改变.**

![image-20220107144844706](D:\Typora笔记\web\Vue\image\使用路由.png)

**注意这里Vue是引入到main.js而不是App.vue的原因是：**

> 实际上App.vue只是提供了一个模板，App.vue模板中仅仅是使用了< router-link>等路由标签，所以VueRouter最终是在main.js文件中的vue实例(**new Vue(){}**)中。



**最终效果**：

![image-20220107145133283](D:\Typora笔记\web\Vue\image\最终效果.png)

## 六、路由的默认路径

> 默认情况下, 进入网站的首页, 我们希望< router-view>渲染首页的内容,但是我们的实现中, 默认没有显示首页组件, 必须让用户点击才可以,如何可以让**路径**默认跳到到**首页**, 并且< router-view>渲染首页组件呢?
>
> 只需要配置**多配置一个映射**

**配置解析:**

* 在routes中又配置了一个映射. 
* path配置的是根路径: /
* redirect是重定向, 也就是我们将根路径重定向到/home的路径下, 这样就可以得到我们想要的结果了.

![image-20220107150718355](D:\Typora笔记\web\Vue\image\默认路径.png)

## 七、改变路径的两种方式

* URL的hash

* HTML5的history

**注**：默认情况下, 路径的改变使用的URL的hash.

如果希望使用HTML5的history模式, 非常简单, 进行如下配置即可:![image-20220107151224122](D:\Typora笔记\web\Vue\image\history.png)



## 八、< router-link>

**属性**：

* **to**: 用于指定跳转的路径.
* **tag**: tag可以指定< router-link>之后渲染成什么组件, 比如上面的代码会被渲染成一个< li>元素, 而不是< a>
* **replace**: preplace不会留下history记录, 所以指定replace的情况下, 后退键返回不能返回到上一个页面中.
* **active-class**: 当< router-link>对应的路由匹配成功时, 会自动给当前元素设置一个router-link-active的class, 设置active-class可以修改默认的名称.
* * 在进行高亮显示的导航菜单或者底部tabbar时, 会使用到该类.
  * 但是通常不会修改类的属性, 会直接使用默认的router-link-active即可. 

![image-20220107151702526](D:\Typora笔记\web\Vue\image\router-link.png)

**补充**：修改inkActiveClass

![image-20220107152341930](D:\Typora笔记\web\Vue\image\activeclass.png)



## 九、路由代码跳转

![image-20220107154041792](D:\Typora笔记\web\Vue\image\代码跳转.png)



## 十、动态路由

> 在某些情况下，一个页面的path路径可能是不确定的，比如我们进入用户界面时，希望是如下的路径：
>
> * /user/aaaa或/user/bbbb
> * 除了有前面的/user之外，后面还跟上了用户的ID
> * 这种path和Component的匹配关系，我们称之为动态路由(也是路由传递数据的一种方式)。

**步骤**：

* 1.设置需要动态的地方

![image-20220107162435174](D:\Typora笔记\web\Vue\image\firstdongai.png)

* 2.动态绑定to

![image-20220107162716709](D:\Typora笔记\web\Vue\image\动态绑定.png)

* 3.通过$route.params获取动态的数据

![image-20220107163120439](D:\Typora笔记\web\Vue\image\动态.png)



## 十一、路由的懒加载

> * 路由懒加载的主要作用就是将路由对应的组件打包成一个个的js代码块.
> * 只有在这个路由被访问到的时候, 才加载对应的组件

![image-20220107191736768](D:\Typora笔记\web\Vue\image\懒加载1.png)

![image-20220107191815176](D:\Typora笔记\web\Vue\image\懒加载2.png)



## 十二、路由的嵌套

> 实现嵌套路由有两个步骤:
>
> * 创建对应的子组件, 并且在路由映射中配置对应的子路由.
> * 在组件内部使用< router-view>标签.

![image-20220107200033386](D:\Typora笔记\web\Vue\image\嵌套1.png)

![image-20220107200134765](D:\Typora笔记\web\Vue\image\嵌套2.png)

**注**：也可以嵌套默认路径，方法相同。



## 十三、传递参数

**传递参数主要有两种类型**: params和query

### 1.params的类型

* 配置路由格式: **/router/:id**
* 传递的方式: **在path后面跟上对应的值**
* 传递后形成的路径: **/router/123, /router/abc**

### 2.query的类型

* 配置路由格式: **/router, 也就是普通配置**
* 传递的方式: **对象中使用query的key作为传递方式**
* 传递后形成的路径: **/router?id=123, /router?id=abc**

![image-20220107203940955](D:\Typora笔记\web\Vue\image\传参2.png)



![image-20220107203233759](D:\Typora笔记\web\Vue\image\传值3.png)





## 十四、导航守卫





## 十五、keep-alive

