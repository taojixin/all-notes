## Loading自定义指令

> 相关知识查看官方文档：[自定义指令)](https://cn.vuejs.org/guide/reusability/custom-directives.html)

## 一、介绍

> 通过**v-loading**指令的方式为某个Dom添加Loading动画。如在发送请求时，请求还在响应时某个Dom需要的请求数据还未获取到，此时Dom内容为空，可以通过添加Loading动画解决暂时的Dom空白的问题。

## 二、自定义指令及使用

### 1.创建loading组件

```vue
<template>
  <div class="loading">
    <div class="loading-content">
      <img src="./loading.gif" width="24" height="24" alt="" />
      <p class="desc">{{ title }}</p>
    </div>
  </div>
</template>

<script setup></script>
<script>
export default {
  data() {
    return {
      title: "正在输入...",
    };
  },
  methods: {
    setTitle(title) {
      this.title = title;
    },
  },
};
</script>

<style lang="less" scoped>
.loading {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  .loading-content {
    text-align: center;
    .desc {
      line-height: 20px;
      font-size: 12px;
      color: black;
    }
  }
}
.g-relative {
  position: relative;
}
</style>
```

### 2.自定义指令

```javascript
import { createApp } from 'vue'
import Loading from './loading.vue'

// g-realtive为一个calssName，定义在全局中，仅有属性position:relative这一个
const relativeCls = 'g-relative'

const loadingDirective = {
    // el：指令绑定到的元素。这可以用于直接操作 DOM。
    mounted(el, binding) {
        const app = createApp(Loading)
        const instance = app.mount(document.createElement('div'))
        // 保存instance后面还会多次使用
        el.instance = instance
        // 添加文字
        const title = binding.arg
        if (typeof title !== 'undefined') {
            // setTitle方位为组件loding中的方法，注意这里的setTitle不能写在setup语法糖中，可能会找不到
            instance.setTitle(title)
        }
        // 如果为binding.value为真，将loading组件挂在到el上
        if (binding.value) {
            append(el)
        }
    },
    updated(el, binding) {
        const title = binding.arg
        if (typeof title !== 'undefined') {
            // setTitle方位为组件loding中的方法
            el.instance.setTitle(title)
        }
        if (binding.value !== binding.oldValue) {
            binding.value ? append(el) : remove(el)
        }
    }
}

// 添加loading
function append(el) {
    // 优化loading让更具通用性。loading组将使用了position:absolute
    const style = getComputedStyle(el)
    // 如果不是以下三个中的一个，添加新的className，添加属性position:relative
    if (['absolute', 'fixed', 'relative'].indexOf(style.position) === -1) {
        // 添加样式
        addClass(el, relativeCls)
    }
    // appendChild方法可向节点的子节点列表的末尾添加新的子节点
    el.appendChild(el.instance.$el)
    // 注意这里的el和el.instance.$el不是同一个，el为需要绑定到的节点，el.instance.$el为loading组件
}
// 移除loading
function remove(el) {
    // 移除样式
    removeClass(el, relativeCls)
    el.removeChild(el.instance.$el)
}
// 添加className
function addClass(el, className) {
    // classList.contains(X)：查看元素是否存在类名为x的类
    if (!el.classList.contains(className)) {
        el.classList.add(className)
    }
}
function removeClass(el, className) {
    el.classList.remove(className)
}

export default loadingDirective
```

### 3.main.js中全局注册

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import router from './router'
import store from './store'
// 全局样式
import './assets/css/global.css'

// 引入自定义指令
import loadingDirective from '@/components/base-ui/loading/directive'

createApp(App).use(store).use(router).directive('loading', loadingDirective).mount('#app')
```

### 4.使用

```vue
<template>
  <!-- v-loading:[loadingText] 动态指令参数 -->
  <div class="div" v-loading:[loadingText]="isShow"></div>
</template>
<script setup>
import { ref } from "vue";

// import Loading from "@/components/base-ui/loading/loading.vue";
let isShow = ref(true);
setTimeout(() => {
  isShow.value = false;
}, 3000);
let loadingText = "正在加载...";
</script>
<style lang="less">
.div {
  width: 100px;
  height: 100px;
  background-color: red;
}
</style>
```