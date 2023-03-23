# token的颁发、保存与携带

> **http**是**无状态协议**(不知道上一次是否登录过了)，所以要返回一个**登录凭证**（如**cookie+session**、**token**)。这里我们使用token实现身份认证。

## 一、JWT实现token的机制

> JWT生成token由三部分组成：
>
> * header
> * payload
> * signature

### 1.header

*  alg：采用的加密算法，**默认**是 HMAC SHA256（**HS256**，对称加密），采用同一个密钥进行 加密和解密；
* type： JWT，固定值，通常都写成JWT即可；
* 会通过base64Url算法进行编码；

### 2.payload

*  携带的数据，比如我们可以将用户的id和name放到payload中；
* 默认也会携带令牌的签发时间；
* 我们也可以设置过期时间：exp（expiration time）；
* 会通过base64Url算法进行编码

### 3.signature

*  设置一个secretKey，通过将前两个的结果**合并后**进行HMACSHA256的算法； 
* HMACSHA256(base64Url(header)+.+base64Url(payload), secretKey); 
* 但是如果secretKey暴露是一件非常危险的事情，因为之后就可以模拟颁发token， 也可以解密token；



## 二、登录接口中颁发token的实现

> 在项目中通过一个库完成：**jsonwebtoken**
>
> 并且一般都是使用**非对称加密**：
>
> * 私钥：用于发布令牌 
> * 公钥：用于验证令牌

### 1.生成公钥与私钥

> 这里使用git bash生成；
>
> git bash 中输入**openssl**：

* 生成公钥到当前文件夹：**genrsa -out private.key 1024**
* 根据私钥生成公钥的当前文件夹：**rsa -in private.key -pubout public.key**

### 2.将公钥与私钥放到配置文件中

```javascript
// 通过dotenv统一管理环境标量
const dotenv = require('dotenv').config();
const fs = require('fs')
const path = require('path')

// 这里读取到的文件时buffer
const PRIVATE_KEY = fs.readFileSync(path.resolve(__dirname, './keys/private.key'))
const PUBLIC_KEY = fs.readFileSync(path.resolve(__dirname, './keys/public.key'))


const {
  APP_PORT,
    .....
  
} = process.env;

module.exports = {
  APP_PORT,
    ......
}
// 注意这里的导出需要写到module.exports={}的后面
module.exports.PRIVATE_KEY = PRIVATE_KEY;
module.exports.PUBLIC_KEY = PUBLIC_KEY;
```

### 3.登录接口中颁发令牌

> 颁发令牌之前要先通过账号的验证（如账号秘密）中间件，然后再在另一个中间件颁发令牌。

```javascript
const express = require('express')
const LoginRouter = express.Router()

const {
  login
} = require('../controller/login.controller')
const {
  verifyLogin,
} = require('../middleware/login.middleware')
// verifyLogin 为颁发令牌前的信息验证。login中间件中颁发令牌
LoginRouter.post('/', verifyLogin, login)

module.exports = LoginRouter;
```

**login中间件**：

> 调用jwt的sign方法生成token，sign()的参数：
>
> * 第一个参数为：payload中的可携带的数据
> * 第二个参数为：私钥
> * 第三个参数为：sign()的其他设置，**expiresIn**为token生效时间，**algorithm**为加密方式，这里需指明为**SH256**(非对称加密)

```javascript
const { getPassword } = require('../service/login.service')
const jwt = require('jsonwebtoken')
const { PRIVATE_KEY } = require('../app/config')
class LoginController {
  // 登录
  async login(req, res, next) {
    const { name, password } = req.body

    if (password === await getPassword(name)) {
      // 生成token
      const token = jwt.sign({ name, password }, PRIVATE_KEY, {
        expiresIn: 60 * 60 * 24, // 一天
        algorithm: "RS256" // 这里必须写RS256(非对象加密)，因为默认为HS256(对称加密)
      })
      return res.json({
        data: { code: 0, token: token },
        meta: { message: "登录成功！", status: 200 }
      })
    }

  }
}

module.exports = new LoginController();
```



### 4.验证前端请求携带的token

> 通过公钥验证token。

```javascript
// 验证授权  （验证token）
const verifyAuth = async (req, res, next) => {
  // 1.获取token (这里假设前端通过data携带token)
  const token = req.headers.token
  // 2.验证token 返回的结果为token携带的数据，如payload中携带的name，passqord，以及过期时间等
  try {
    const result = jwt.verify(token, PUBLIC_KEY, {
      algorithms: ["RS256"]
    });
    next();
  } catch {
    res.json({
      meta: {
        message: "无效的token！",
        status: 401 // 未授权
      }
    })
  }
}
```

**注**：在需要验证token的地方直接插入这个中间件即可。如：

`studyRouter.get('/getsortlist', verifyAuth, getSortList)`



## 三、前端保存token和请求携带token

### 1.保存token

`localStorage.setItem('adminToken', data.token)`

### 2.请求携带token

* 请求头携带token
* url携带token
* data携带token
* 前端二次axios在请求拦截器中携带token

**这里展示请求拦截器中携带token:**

```javascript
// 二次封装axios
import axios from 'axios'

const requests = axios.create({
  baseURL: '/admin',
  timeout: 5000
})

// 请求拦截器
requests.interceptors.request.use(config => {
  if (localStorage.getItem('adminToken')) {
    config.headers.token = localStorage.getItem("adminToken")
  }
  // config: 配置对象，里面有一个熟悉很重要，headers请求头
  return config
})

// 响应拦截器
requests.interceptors.response.use(res => {
  return res.data
}, error => {
  return Promise.reject(error)
})

export default requests;
```

