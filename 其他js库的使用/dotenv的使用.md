# 环境变量的管理

> 在**Node.js**开发项目中，有时一个变量在项目中会多次使用或一个变量在**开发阶段**和**测试阶段**变量的值不同，为了能方便管理和使用这些环境变量，我们可以使用**dotenv**来**统一管理环境变量**。

## dotenv简介

### 1.简介

> **dotenv**是一个零依赖性模块，它能将**环境变量**从**.env文件**加载到**process.env**中，所以我们只需要在**.env文件**中写好环境变量，然后通过**process.env.环境变量**的方式使用环境变量。

### 2.安装

```
npm install dotenv --save
```

### 3.使用

* 首先，创建.env文件，并配置好环境变量

```env
APP_PORT = 8881

MYSQL_HOST=localhost
MYSQL_PORT=3306
MYSQL_DATABASE=myblog
MYSQL_USER=root
MYSQL_PASSWORD=123456
```

* 然后，在**入口文件main.js**(有的入口文件取名为**app.js**)里**引入dotenv**

```javascript
require('dotenv').config()
```

* 最后，通过**process.env.环境变量**的方式使用

```javascript
const app = require('./app')
require('dotenv').config()

app.listen(8887, ()=> {
  console.log(`服务器在${process.env.APP_PORT}端口启动成功！`);
})
```

### 4.进一步优化管理

> 当环境变量过多时，.env中环境变量不便于管理，或有一些特别的环境变量时，也不便于管理，所以我们可以**额外创建一个配置文件**用于统一管理环境变量。

* 创建一个如config.js的文件(具体在哪里创建看自己目录结构)，在里面导入dotenv
* 在里面导入所有的**.env**中的环境变量，再导出

```javascript
// 通过dotenv统一管理环境标量
const dotenv = require('dotenv').config();
const fs = require('fs')
const path = require('path')
// 这里读取到的文件时buffer
const PRIVATE_KEY = fs.readFileSync(path.resolve(__dirname, './keys/private.key'))
const PUBLIC_KEY = fs.readFileSync(path.resolve(__dirname, './keys/public.key'))

const {
  // 启动端口
  APP_PORT,
  // 连接数据库环境变量
  MYSQL_HOST,
  MYSQL_PORT,
  MYSQL_DATABASE,
  MYSQL_USER,
  MYSQL_PASSWORD,
  // 私密
  SERCET_KEY
} = process.env;
module.exports = {
  APP_PORT,
  MYSQL_HOST,
  MYSQL_PORT,
  MYSQL_DATABASE,
  MYSQL_USER,
  MYSQL_PASSWORD,
  SERCET_KEY
}
// 注意这里的导出需要写到module.exports={}的后面
module.exports.PRIVATE_KEY = PRIVATE_KEY;
module.exports.PUBLIC_KEY = PUBLIC_KEY;
```

* 使用，在需要使用的地方导入config.js文件再使用

```javascript
const app = require('./app');
require('./app/database')
// 全局变量
const config = require('./app/config')


app.listen(config.APP_PORT, () => {
  console.log(`服务器在${config.APP_PORT}端口启动成功`);
})
```

