## Mock.js的使用

> Mock.js用于随机生成一些数据。原理是对请求进行了拦截，并未发送真是的向服务端的请求。这里只讲在Vue中的使用。

### 1.安装

`npm install mock.js`

### 2.配置

> 在src下创建**mockjs**文件夹，再创建index.js文件。在index.js中对mock进行配置及模拟数据。

```javascript
import Mock from 'mockjs'
// 模拟get请求，实际是对真是请求的拦截
// (注意这里的url，反斜杠不能少，之前少了第一个反斜杠一直报错找不到原因)
Mock.mock('/api/account', 'get', {
  code: 0,
  msg: 'success',
  data: {
  	'id|1-99': 0 // 生成1-99的随机id
  }
})

// 设置延迟
Mock.setup({
  timeout: "500-1000",
});
```

### 3.引入

> 这一步很重要，必须要在main.js中引入，否则报错404。

```javascript
import Vue from 'vue'
import App from './App.vue'
import router from './router'

import '@/mockjs/index'

Vue.config.productionTip = false

new Vue({
  router,
  render: h => h(App)
}).$mount('#app')
```

### 4.使用

> 和正常的请求一样，由于是拦截，浏览器中看不到请求记录。这里我是对axios进行了二次封装，api统一管理。

```javascript
// requests为二次封装的axios
import requests from '@/api/requests'

const reqAccount = () => {
  return requests({
    url: '/account',
    method: 'get'
  })
}

export {
  reqAccount
}
```

### 5.常用语法

> 更多用法查文档：[Mock.js (mockjs.com)](http://mockjs.com/)

```javascript
let Random = Mock.Random
// 随机生成一个常见的中文姓名。
Random.cname()
// 随机生成日期
Random.date()
// 随机生成一句中文标题
Random.ctitle()
// 随机生成一段中文文本
Random.cparagraph()
// 生成一段随机的 Base64 图片编码。
Random.dataImage()

Mock.mock('/api/entries', 'get', {
  code: 0,
  msg: 'success',
  data: {
    'entries': [
      {
        'id|1-999': 0, // 生成1-99的随机数
        name: "@cname",
        data: '@date',
        title: '@ctitle',
        content: '@cparagraph',
        "browse|20-999": 125,
        "good|1-999": 1231,
        "comments|1-99": 0,
        imagesurl: '@dataImage'
      },
     ]
  }
}
```

