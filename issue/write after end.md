@[TOC](目录)
> npm运行服务器，在调用某一个接口时报错**Error [ERR_STREAM_WRITE_AFTER_END] write after end**，虽然实际接口功能未受影响。
### 问题

```javascript
const {isExistName} = require('../service/login.service')
const verifyLogin = async (req, res, next) => {
  // 获取用户名
  const {name} = req.body
  // 根据用户名判断用户是否存在 
  if (await isExistName(name)) { // 这里调用isExistName返回的是promise，所以使用async和await简化返回结果（即true或false）
    // 这里必须是return出去否则报错 Error [ERR_STREAM_WRITE_AFTER_END] write after end
    next() // 存在则进行下一个中间件
  }
  res.end("用户不存在")
}

module.exports = {
  verifyLogin
}
```



### 原因
> 在if中已经调用一次next()了（进行下一中间件，然会后续代码不再执行），但是后面又使用res.end()，就报错了。同理，如果先执行了res.end()再执行res.end()或next()也会报此类错误。

### 解决
> 在调用next()时把它return出去。

```javascript
const {isExistName} = require('../service/login.service')
const verifyLogin = async (req, res, next) => {
  // 获取用户名
  const {name} = req.body
  // 根据用户名判断用户是否存在 
  if (await isExistName(name)) { // 这里调用isExistName返回的是promise，所以使用async和await简化返回结果（即true或false）
    // 这里必须是return出去否则报错 Error [ERR_STREAM_WRITE_AFTER_END] write after end
    return next() // 存在则进行下一个中间件
  }
  res.end("用户不存在")
}

module.exports = {
  verifyLogin
}
```

