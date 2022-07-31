# vue Router v4.x

### 1.使用步骤

> **安装：**npm install vue-router@4

* 第一步：创建路由组件的组件； 
* 第二步：配置路由映射: 组件和路径映射关系的routes数组；
* 第三步：通过createRouter创建路由对象，并且传入routes和history模式；
* 第四步：使用路由: 通过< router-link>和< router-view>；

**router文件夹中的index.js：**

```javascript
import { createRouter, createWebHashHistory } from 'vue-router'

// 导入创建的组件
import Home from '../pages/Home.vue'
import About from '../pages/About.vue'

// 配置路由的映射
const routes = [
    { path: '/home', component: Home },
    { path: '/about', compnent: About}
]

// 创建路由对象
const router = createRoter({
    routes,
    history: createWebHashHistory()
})

// 导出，在main.js中引入并使用
export default router
```

**main.js：**

```javascript
import { createApp } from 'vue'
import router from './router'
import App from './App.vue'

const app = createApp(App)

app.use(router)

app.mount('#app')

// 简写：链式调用，use本身返回的就是app对象
// createApp(App).use(router).mount("#app")
```

**组件中使用：**

```html
<template>
	<div class="app">
        <p>
            <router-link to="/home">首页</router-link>
            <router-link to="/about">关于</router-link>
        </p>
        <router-view></router-view>
    </div>
</template>
```



### 2.路由的默认路径

> 路由的默认路径即重定向，第一次打开时默认跳转到该页面。

```javascript
const routes = [
    // 默认路由
    // { path: '/', component: Home},
    // 重定向
    { path: '/', redirect: '/home' },
    { path: '/home', component: Home },
    { path: '/about', compnent: About}
]
```



### 3.跳转的模式

> 通过导入`import {createRouter, createWebHashHistory, createWebHistory} from 'vue-router'`来选择使用**history模式**还是**hash模式**。



### 4.router-link

**router-link配置：**

* **to属性：**用于跳转到的地方
* **replace属性**：和to属性相似，该跳转后不可返回
* **active-class属性**：设置激活a元素后应用的class，默认是router-link-active

```html
<!-- 修改a标签的class，默认为router-link-active -->
  <router-link to="/home" active-class="tjx">home</router-link>
```

* **exact-active-class属性：**链接精准激活时，应用于渲染的  的 class，默认是router-link-exact-active；

**router-link也可以自定义渲染：**

```html
  <!-- 插槽 -->
  <!-- 1.默认 -->
  <!-- <router-link to="/home">
    <button>首页</button>
  </router-link> -->
  <!-- 2.组件 -->
  <!-- <router-link to="/home">
    <nav-bar title="首页"></nav-bar>
    <span>hhh</span>
  </router-link> -->

  <!-- 3.作用域插槽 -->
  <!-- props中有很多东西，如 1.href 以及要跳转的路由对象 2.route 还有 3.navigate导航函数 和 4.isActive 是否当前处于活跃状态-->
  <!-- 注：custom：添加了这个属性router-link中的元素将不再被a标签包裹，同时不能跳转到to的path，需要手动跳转，这时可以使用 navigate 导航函数，跳转到to的path -->
  <router-link to="/home" v-slot="props" custom>
    <button @click="props.navigate">{{props.href}}</button>
    <!-- <p>{{props.route}}</p> -->
  </router-link>
```



### 5.路由懒加载

```javascript
const routes = [
  // 默认路由
  // { path: '/', component: Home},
  // 重定向
  { path: '/', redirect: '/home' },
  {
    path: '/home', name: "home", component: () => {
      return import("../pages/Home.vue") // 路由懒加载：完整写法
    }
  },
  // 路由懒加载：简写
  { path: '/user', component: () => import('../pages/User.vue') }
]
```



### 6.路由的其他属性

* name属性：路由记录独一无二的名称；
* meta属性：自定义的数据

```javascript
const routes = [
  { path: '/home', name: "home", component: Home},
  {
    path: '/about', component: About,
    meta: {
      name: 'tjx',
      age: 18
    }
  }
]
```



### 7.动态路由基本匹配

> 很多时候我们需要将给定匹配模式的路由映射到同一个组件： 例如，我们可能有一个 User 组件，它应该对所有用户进行渲染，但是用户的**ID是不同**的； 在Vue Router中，我们可以在路径中使用一个动态字段来实现，我们称之为 **路径参数**；

定义：`{ path: '/user/:id', component: User }`

跳转：`<router-link to="/user/123">用户：123</router-link>`



### 8.获取动态路由的值

* 在**template**中，直接通过 **$route.params**获取值； 

```html
<template>
	<div>
        <h2>{{ $route.params.id }}</h2>
    </div>
</template>
```

* 在**created**中，通过 **this.$route.params**获取值； 
* 在**setup**中，我们要使用 vue-router库给我们提供的一个hook **useRoute**； 该Hook会返回一个Route对象，对象中保存着当前路由相关的值；

```javascript
<script>
import { useRouter } from "vue-router";
export default {
  name: "App",
  // setup中通过useRouter获取$router，注意不是useRoute
  setup() {
    const router = useRouter();
    console.log(router.params.id)
  },
  methods: {
    console.log(this.$route.params.id)
  }
};
</script>
```



### 9.NotFound

> 对于哪些没有匹配到的路由，我们通常会匹配到固定的某个页面,比如NotFound的错误页面中，这个时候我们可编写一个动态路由用于匹配所有的页面；

**定义**：`{ path: '/:pathMatch(.*)', component: NotFound }`

**可以通过 $route.params.pathMatch获取到传入的参数：** 

`<h2>Not Found: {{ $route.params.pathMatch }}</h2>`



### 10.嵌套路由

```javascript
  {
    path: '/home', name: "home", component: () => {
      return import("../pages/Home.vue") // 路由懒加载：完整写法
    },
    children: [
      { path: 'message', component: () => import('../pages/HomeMessage.vue') },
      { path: 'shops', component: () => import('../pages/HomeShops.vue') },
    ]
  }
```

 

### 11.手动的页面跳转

> 有时候我们希望通过代码来完成页面的跳转，比如点击的是一个按钮。

```javascript
<script>
import { useRouter } from "vue-router";
export default {
  name: "App",
  // setup中通过useRouter获取$router，注意不是useRoute
  setup() {
    const router = useRouter();
    const jumpToAbout = () => {
      // 1.传递字符串
      // router.push("/about");
      // 2.传递对象
      router.push({
        path: '/about',
        query: {
          name: 'yn',
          age: 18
        }
      })
      // router.replace("/about")
    };

    return {
      jumpToAbout,
    };
  },
  // methods: {
  //   jumpToAbout() {
  //     // router对象
  //     this.$router.push('/about')
  //   }
  // }
};
</script>
```



### 12.query方式的参数

**通过query的方式传递参数：**

```javascript
jumpJToProfile() {
    this.$router.push({
        path: '/profile',
        query: { name: 'tjx', age: 18}
    })
}
```

**在界面中通过 $route.query 来获取参数：**

`<h2>query: {{ $router.query.name }} </h2>`



### 13.动态添加路由

```javascript
// 动态添加路由
const categoryRoute = {
  path: '/category',
  component: () => import("../pages/Category.vue")
}
router.addRoute(categoryRoute)

// 给一级路由对象home添加二级路由对象
router.addRoute('home', {
  path: 'moment',
  component: () => import('../pages/HomeMount.vue')
})
```



### 14.动态删除路由

* 方式一：添加一个name相同的路由； 
```javascript
router.addRouter({ path: '/about', name: 'about', component: About})
// 这将会删除之前已经添加的路由，因为他们具有相同的名字且名字必须是唯一的
router.addRouter({ path: '/other', name: 'about', component: Home})
```
* 方式二：通过removeRoute方法，传入路由的名称； 

```javascript
router.addRouter({ path: '/about', name: 'about', component: About})
router.removeRoute('about')
```

* 方式三：通过addRoute方法的返回值回调；

```javascript
const removeRoute = router.addRoute(routeRecord)
removeRoute()  
```

**补充：**

*  **router.hasRoute()**：检查路由是否存在。
* **router.getRoutes()**：获取一个包含所有路由记录的数组。



### 15.导航守卫

> vue-router 提供的导航守卫主要用来通过跳转或取消的方式守卫导航。Vue提供了很多的其他守卫函数，目的都是在某一个时刻给予我们回调，让我们可以更好的控制程序的流程或者功能： https://next.router.vuejs.org/zh/guide/advanced/navigation-guards.html

```javascript
// 导航守卫 beforEach
// router.beforeEach((to, form) => {
//   // to: route对象，即将跳转到的route对象
//   // from: route对象，从哪一个路由对象跳转过来的
//   // 返回值：1.false 不进行导航 2.undefined或不写返回值：进行默认导航，该去哪去哪 3.字符串：路径，跳转到该路径中去
//   console.log();
//   return false // 不能跳转
// })
```

