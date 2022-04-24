## Node基础

### 一、给Node传递参数

> 在命令行执行js文件时，可以在命令后面直接写参数传入参数，传入的参数会存储到属性**process**的**内置对象argv**当中

```javascript
console.log(process.argv);
process.argv.forEach(item => {
  console.log(item);
});
```

### 二、Node的输出

* console.log ：最常用的输入内容的方式：console.log 
* console.clear ：清空控制台：console.clear 
* console.trace ：打印函数的调用栈：console.trace

### 三、全局对象

#### 1.常见全局对象

* **process对象**：process提供了Node进程中相关的信息
* **console对象**：提供了简单的调试控制台
*  定时器函数：在Node中使用定时器有好几种方式：
* * **setTimeout**(callback, delay[, ...args])：callback在delay毫秒后执行一次；
  * **setInterval**(callback, delay[, ...args])：callback每delay毫秒重复执行一次；
  * **setImmediate**(callback[, ...args])：callback I/O事件后的回调的“立即”执行； 
  * **process.nextTick**(callback[, ...args])：添加到下一次tick队列中；

#### 2.特殊全局对象

>  这些全局对象可以在模块中任意使用，但是在命令行交互中是不可以使用的；

*  _ _ dirname：获取当前文件所在的路径。
* _ _ filename：获取当前文件所在的路径和文件名称。

#### 3.global对象

>  global是一个全局对象，事实上前端我们提到的process、console、setTimeout等都有被放到global中。
>
> 类似于浏览器中的window对象。

### 四、模块化

#### 1.CommonJs

> Node中对CommonJS进行了支持和实现，让我们在开发node的过程中可以方便的进行模块化开发： 
>
> * 在Node中每一个js文件都是一个单独的模块； 
> * 这个模块中包括CommonJS规范的核心变量：exports、module.exports、require； 
> * 我们可以使用这些变量来方便的进行模块化开发；

**exporst**导出：

* 1.exports是一个对象，我们可以在这个对象中添加很多个属性，添加的属性会导出；

```javascript
exports.name = name;
exports.age = age;
```

* 2.另一个文件中导入

```javascript
const bar = require('./bar')
console.log(bar.name)
console.log(bar.age)
```



**module.exports**:

* Node中真正用于导出的其实根本不是exports，而是module.exports。
* module对象的exports属性是exports对象的一个引用



**require**:

总结比较常见的查找规则：导入格式如下：**require(X)**

* 情况一：X是一个核心模块，比如path、http p 直接返回核心模块，并且停止查找.
* 情况二：X是以 ./ 或 ../ 或 /（根目录）开头的.

>  **第一步**：将X当做一个文件在对应的目录下查找； 
>
> * 1.如果有后缀名，按照后缀名的格式查找对应的文件 
> * 2.如果没有后缀名，会按照如下顺序： 
> * * 直接查找文件X 
>   * 查找X.js文件 
>   * 查找X.json文件
>   * 查找X.node文件
>
> **第二步**：没有找到对应的文件，将X作为一个目录 ，查找目录下面的index文件 
>
> * 1> 查找X/index.js文件
> * 2> 查找X/index.json文件 
> * 3> 查找X/index.node文件
>
>  如果都没有找到，那么报错：not found

* 情况三：直接是一个X（没有路径），并且X不是一个核心模块，回去每个文件目录的node_modules中寻找，直到寻找到根目录。



**模块的加载过程**：

*  结论一：模块在被第一次引入时，模块中的js代码会被运行一次
*  结论二：模块被多次引入时，会缓存，最终只加载（运行）一次（每个模块对象module都有一个属性：loaded。为false表示还没有加载，为true表示已经加载；）
* 结论三：如果有循环引入（图结构这种）图结构在遍历的过程中，有深度优先搜索（DFS, depth first search）和广度优先搜索

#### 2.Node对ES Module的支持

* 方式一：在package.json中配置 type: module（后续学习，我们现在还没有讲到package.json文件的作用） 
* 方式二：文件以 .mjs 结尾，表示使用的是ES Module；



### 五、常见内置模块

#### 1.path

##### (1)从路径中获取信息

*  dirname：获取文件的父文件夹；
* basename：获取文件名；
* extname：获取文件扩展名；

```javascript
const path = require('path')

// 1.获取路径的消息
const filepath = '/User/why/abc.txt'

console.log(path.dirname(filepath));// /User/why
console.log(path.basename(filepath));// abc.txt
console.log(path.extname(filepath));// .txt
```



##### (2)路径的拼接

* join路径拼接
* resolve路径拼接

**区别：**join与resolev的区别，resolve会判断拼接路径字符串中，是否有以/或./或../开头的路径，有的话则会在路径开头打印根路径或当前路径或上一级路径

```javascript
const basepath = '/User/why'
const filename = 'abc.txt'
const file1path = path.join(basepath, filename);
console.log(file1path);//  \User\why\abc.txt
const file2path = path.resolve(basepath, filename);
console.log(file2path);//  D:\User\why\abc.txt

const basepath = './User/why'
const filename = 'abc.txt'
const file1path = path.join(basepath, filename);
console.log(file1path);//  User\why\abc.txt
const file2path = path.resolve(basepath, filename);
console.log(file2path);// D:\Microsoft VS Code web Node\01.Node基础\03.常见的内置模块\path\User\why\abc.txt

const basepath = '../User/why'
const filename = 'abc.txt'
const file1path = path.join(basepath, filename);
console.log(file1path);//  ..\User\why\abc.txt
const file2path = path.resolve(basepath, filename);
console.log(file2path);//  D:\Microsoft VS Code web Node\01.Node基础\03.常见的内置模块\User\why\abc.txt
```



#### 2.fs

>  fs是File System的缩写，表示文件系统。

##### (1)fs的API

> fs这些API大多数都提供三种操作方式： 
>
> * 方式一：同步操作文件：代码会被阻塞，不会继续执行； 
> * 方式二：异步回调函数操作文件：代码不会被阻塞，需要传入回调函数，当获取到结果时，回调函数被执行； 
> * 方式三：异步Promise操作文件：代码不会被阻塞，通过 fs.promises 调用方法操作，会返回一个Promise， 可以通过then、catch进行处理；

```javascript
const fs = require('fs')

// 1.方式一： 同步读取文件
const state = fs.statSync('../foo.txt');
console.log(state);
console.log("后续代码");

// 2.方式二：异步读取
fs.stat('../foo.txt', (err, state) => {
  if(err) {
    console.log(err);
    return ;
  }
  console.log(state);
})
console.log("后续代码执行");

// 3.方式三：Promise方式
fs.promises.stat('../foo.txt').then(state => {
  console.log(state);
  console.log(state.isDirectory());
}).catch(err => {
  console.log(err);
})
console.log("后续代码");
```

##### (2)描述符

> * 在 POSIX 系统上，对于每个进程，内核都维护着一张当前打开着的文件和资源的表格。 
> * 每个打开的文件都分配了一个称为文件描述符的简单的数字标识符。 
> * 在系统层，所有文件系统操作都使用这些文件描述符来标识和跟踪每个特定的文件。
> * Windows 系统使用了一个虽然不同但概念上类似的机制来跟踪资源。 
> * 为了简化用户的工作，Node.js 抽象出操作系统之间的特定差异，并为所有打开的文件分配一个数字型的文件描述 符。

```javascript
const fs = require('fs');

// 获取文件描述符
fs.open('./abc.txt', (err ,fd) => {
  if(err) {
    console.log(err);
    return ;
  }
  console.log(fd);
})

// 通过文件描述符获取文件信息
fs.fstat(3, (err, info) => {
  console.log(info);
})
```



##### (3)文件的读写

* fs.readFile(path[, options], callback)：读取文件的内容；
* fs.writeFile(file, data[, options], callback)：在文件中写入内容；

**option参数**： 

* **flag**：写入的方式；flag的值：

 **w**  打开文件写入，默认值； 

**w+**  打开文件进行读写，如果不存在则创建文件； 

**r+**  打开文件进行读写，如果不存在那么抛出异常； 

**r**  打开文件读取，读取时的默认值； 

**a**  打开要写入的文件，将流放在文件末尾。如果不存在则创建文件； 

**a+**  打开文件以进行读写，将流放在文件末尾。如果不存在则创建文件

* **encoding**：字符的编码； 如果不填写encoding，返回的结果是Buffer；

```javascript
const fs = require('fs');

// 文件写入
const content = "的房价来说"
fs.writeFile('./abcd.txt', content,{flag: "a"}, err => {
  console.log(err);
});

// 文件读取
fs.readFile("./abc.txt", (err, data) => {
  console.log(data); //<Buffer e7 9a 84 e6 88 bf e4 bb b7 e6 9d a5 e8 af b4>
})
fs.readFile("./abc.txt", {encoding: 'utf-8'}, (err, data) => {
  console.log(data); //的房价来说
})
```



##### (4)文件夹的操作

**新建文件夹**： 使用fs.mkdir()或fs.mkdirSync()创建一个新文件夹

**获取文件夹内容**：

**文件夹重命名**：

```javascript
const fs= require('fs');
const path = require('path')

// 1.创建文件夹
const dirname = './why';
if(!fs.existsSync(dirname)) {
  fs.mkdir(dirname, err => {
    console.log(err);
  })
}

// 2.读取文件夹中的所有文件
fs.readdir(dirname, (err, files) => {
  console.log(files);
});
const dirname = './why';

function getFiles(dirname) {
  fs.readdir(dirname,{withFileTypes: true}, (err, files) => {
    for (let file of files) {
      if (file.isDirectory()) {
        const filepath = path.resolve(dirname, file.name);
        getFiles(filepath)
      } else {
        console.log(file.name);
      }
    }
  })
}
getFiles(dirname)


// 3.文件夹的重命名
fs.rename('./why', './kobe', err => {
  console.log(err);
})
```

#### 3.events





### 六、包管理工具npm

#### 1.简介

* 包管理工具npm： 
* * Node Package Manager，也就是Node包管理器； 
  * 但是目前已经不仅仅是Node包管理器了，在前端项目中我们也在使用它来管理依赖的包； 
  * 比如express、koa、react、react-dom、axios、babel、webpack等等； 

* npm管理的包可以在哪里查看、搜索呢？ 
* * https://www.npmjs.com/ ：这是我们安装相关的npm包的官网；
* npm管理的包存放在哪里呢？ 
* * 我们发布自己的包其实是发布到**registry**上面的； 
  * 当我们安装一个包时其实是从registry上面下载的包；

#### 2.项目配置文件

> 每一个**项目**都会有一个对应的配置文件，无论是前端项目还是后端项目，这个配置文件会记录着你项目的名称、版本号、项目描述等；也会记录着你项目所依赖的其他库的信息和依赖库的版本号；这个配置文件在Node环境下面（无论是前端还是后端）就是**package.json**

**cli4脚手架的项目配置项**：

![image-20220115235905665](D:\Typora笔记\web\Node.js\img\cli4配置项.png)

#### 3.配置文件常见属性

##### (1)必须填写的属性

* **name**是项目的名称； 
* **version**是当前项目的版本号；
* **description**是描述信息，很多时候是作为项目的基本描述； 
* **author**是作者相关信息（发布时用到）；
* **license**是开源协议（发布时用到）

##### (2)private属性

*  private属性记录当前的项目是否是私有的； 
* 当值为true时，npm是不能发布它的，这是防止私有项目或模块发布出去的方式；

##### (3)main属性

*  设置程序的入口。
* 疑惑，webpack不是会自动找到程序的入口吗？
* * 这个入口和webpack打包的入口并不冲突；
  * 它是在你发布一个模块的时候会用到的； 
  * 比如axios文件夹下也有index.js和package.json文件，main属性对应的便是axios文件夹下的index.js文件

##### (4)scripts属性

* scripts属性用于配置一些脚本命令，以键值对的形式存在； 
* 配置后我们可以通过 npm run 命令的key来执行这个命令； 
* npm start和npm run start的区别是什么？
* * 它们是等价的；
  * 对于常用的 **start、 test、stop、restart**可以省略掉run直接通过 npm start等方式运行；
* 如配置一个**"start": "node ./sandbox/server.js"**，只需要在命令行输入npm run start便可执行start对应的命令。

##### (5) dependencies属性

* dependencies属性是指定无论**开发环境**还是**生成环境**都需要依赖的包； 
* 通常是我们项目实际开发用到的一些库模块；
* 与之对应的是devDependencies；

##### (6) devDependencies属性

* 一些包在生成环境是不需要的，比如webpack、babel等；
* 这个时候我们会通过 npm install webpack --save-dev，将它安装到devDependencies属性中；

##### (7) engines属性

* engines属性用于指定Node和NPM的版本号； 
* 在安装的过程中，会先检查对应的引擎版本，如果不符合就会报错； 
* 事实上也可以指定所在的操作系统 "os" : [ "darwin", "linux" ]，只是很少用到；

##### (8) browserslist属性

*  用于配置打包后的JavaScript浏览器的兼容情况，参考；
* 否则我们需要手动的添加polyfills来让支持某些语法；
* 也就是说它是为webpack等打包工具服务的一个属性（这里不是详细讲解webpack等工具的工作原理，所以 不再给出详情）；



#### 4.版本管理问题

> 安装的依赖版本出现：^2.0.3或~2.0.3，这是什么意思呢？

* npm的包通常需要遵从semver版本规范;
* semver版本规范是X.Y.Z： 
* * X主版本号（major）：当你做了不兼容的 API 修改（可能不兼容之前的版本）； 
  * Y次版本号（minor）：当你做了向下兼容的功能性新增（新功能增加，但是兼容之前的版本）； 
  * Z修订号（patch）：当你做了向下兼容的问题修正（没有新功能，修复了之前版本的bug）；

* ^和~的区别： 
* * **^x.y.z**：表示x是保持不变的，y和z永远安装最新的版本； 
  * **~x.y.z**：表示x和y保持不变的，z永远安装最新的版本；



#### 5.npm install 命令

*  安装npm包分两种情况： 
* * 全局安装（global install）： **npm install axios -g**
  * 项目（局部）安装（local install）： **npm install axios **

**注**：使用npm全局安装的包都是一些工具包：yarn、webpack等；并不是类似于 axios、express、koa等库文件；所以全局安装了之后并不能让我们在所有的项目中使用 axios等库。

*  局部安装分为开发时依赖和生产时依赖：

```shell
# 安装开发和生产依赖
npm install axios
npm i axios

# 开发依赖
npm install webpack --save-dev
npm install webpack -D
npm i webpack –D

# 根据package.json中的依赖包
npm install
```



#### 6.项目安装

> 目安装会在当前目录下生产一个 node_modules 文件夹



#### 7.npm install 原理

![image-20220116002525730](D:\Typora笔记\web\Node.js\img\npminstall原理图.png)

首先 npm install会检测是有package-lock.json文件。然后

* 没有lock文件
* * 分析依赖关系，这是因为我们可能包会依赖其他的包，并且多个包之间会产生相同依赖的情况；
  * 从registry仓库中下载压缩包（如果我们设置了镜像，那么会从镜像服务器下载压缩包）；
  * 获取到压缩包后会对压缩包进行缓存（从npm5开始有的）； 
  * 将压缩包解压到项目的node_modules文件夹中（前面我们讲过，require的查找顺序会在该包下面查找）

*  有lock文件
* * 检测lock中包的版本是否和package.json中一致（会按照semver版本规范检测）；
  * * 不一致，那么会重新构建依赖关系，直接会走顶层的流程；

* * 一致的情况下，会去优先查找缓存 
  * * 没有找到，会从registry仓库下载，直接走顶层流程；

* *  查找到，会获取缓存中的压缩文件，并且将压缩文件解压到node_modules文件夹中；

#### 8.package-lock.json文件

![image-20220116003114118](D:\Typora笔记\web\Node.js\img\package-lock.png)

* package-lock.json文件解析： 
* name：项目的名称；
* version：项目的版本；
* lockfileVersion：lock文件的版本；
* requires：使用requires来跟着模块的依赖关系；
*  dependencies：项目的依赖
* * 当前项目依赖axios，但是axios依赖follow-redireacts； 
  * axios中的属性如下：
  * *  version表示实际安装的axios的版本；
    * resolved用来记录下载的地址，registry仓库 中的位置；
    * requires记录当前模块的依赖；
    * integrity用来从缓存中获取索引，再通过索引 去获取压缩包文件；

#### 9.npm其他命令

*  卸载某个依赖包：
* *  **npm uninstall package** 
  * **npm uninstall package --save-dev** 
  * **npm uninstall package -D**
* 强制重新build 
* * npm rebuild
* 清除缓存
* * **npm cache clean**
* npm的命令其实是非常多的：  https://docs.npmjs.com/cli-documentation/cli 更多的命令，可以根据需要查阅官方文档

#### 10.其他包管理工具

##### (1)Yarn工具

> * yarn是由Facebook、Google、Exponent 和 Tilde 联合推出了一个新的 JS 包管理工具；
> * yarn 是为了弥补 npm 的一些缺陷而出现的； 
> * 早期的npm存在很多的缺陷，比如安装依赖速度很慢、版本依赖混乱等等一系列的问题； 
> * 虽然从npm5版本开始，进行了很多的升级和改进，但是依然很多人喜欢使用yarn；

##### (2)cnpm工具

> * 由于一些特殊的原因，某些情况下我们没办法很好的从 https://registry.npmjs.org下载下来一些需要的包。
> * 查看npm镜像：**npm config get registry # npm config get registry**
> * 我们可以直接设置npm的镜像：**npm config set registry https://registry.npm.taobao.org**
> * 且将cnpm设置为淘宝的镜像： **npm config get registry # npm config get registry npm config set registry https://registry.npm.taobao.org**                     **npm install -g cnpm --registry=https://registry.npm.taobao.org cnpm config get registry # https://r.npm.taobao.org/**

##### (3)npx工具

> * npx是npm5.2之后自带的**一个命令**。 npx的作用非常多，但是比较常见的是使用它来调用项目中的某个模块的指令。
> * 解决局部命令执行。





### 七、Buffer的使用

> Node为了可以方便开发者完成更多功能，提供给了我们一个类Buffer，并且它是全局的。
>
> Buffer中存储的是二进制数据，那么到底是如何存储呢？ 
>
> * 我们可以将Buffer看成是一个存储二进制的数组； 
> * 这个数组中的每一项，可以保存8位二进制： 00000000
> *  Buffer相当于是一个字节的数组，数组中的每一项对应一个字节的大小.





### 八、事件循环



## http模块

### 1.创建服务器

* 方法一：通过 **createServer** 来完成；http.createServer会返回服务器的对象；底层其实使用直接 new Server 对象。

```javascript
// 方式一：
const server1 = http.createServer((req,res) => {
  res.end("serve1")
})
server1.listen(8000, () => {
  console.log("server1启动成功");
})
```

* 方式二：直接 **new Server** 对象。

```javascript
const server2 = new http.Server((req,res) => {
  res.end("serve2")
})
server2.listen(8001, () => {
  console.log("server2启动成功");
})
```


* 回调函数在 被调用时会传入两个参数： 
* * req：**request请求对象**，包含请求相 关的信息；
  * res：**response响应对象**，包含我们 要发送给客户端的信息；



### 2.监听方法listen

>  Server通过listen方法来开启服务器，并且在某一个主机和端口上监听网络请求。

```javascript
const server1 = http.createServer((req,res) => {
  res.end("serve1")
})
// 2.监听方法的使用
server1.listen(8000, () => {
  console.log("server1启动成功");
  console.log(server1.address().port);// 获取端口号
})
```

**listen函数有三个参数**：

*  端口port: 可以不传, 系统会默认分配端, 后续项目中我们会写入到环境变量中；
*  **主机host**: 通常可以传入localhost、ip地址127.0.0.1、或者ip地址0.0.0.0，默认是0.0.0.0；（注意他们三个的区别）
*  **回调函数**：服务器启动成功时的回调函数；



### 3.request对象

>  在向服务器发送请求时，我们会携带很多信息，比如： 
>
> * 本次请求的URL，服务器需要根据不同的URL进行不同的处理； 
> * 本次请求的请求方式，比如GET、POST请求传入的参数和处理的方式是不同的； 
> * 本次请求的headers中也会携带一些信息，比如客户端信息、接受数据的格式、支持的编码格式等；
> * 这些信息，Node会帮助我们封装到一个**request的对象**中，我们可以直接来处理这个request对象：

```javascript
const http = require('http')
const url = require('url')
const qs = require('querystring') // 用于对query进行结构

// 创建一个web服务器
const server = http.createServer((req, res) => {
  // request对象中封装了客户端给我们服务器传递过来的所有信息
  console.log(req.url);
  console.log(req.method);// 请求方式，如Post，Get
  console.log(req.headers);// 请求头信息
 
    // 最基本的请求方式
  if (req.url === '/login') {
    res.end("欢迎回来");
  } else if (req.url === '/users') {
    res.end("用户列表");
  } else {
    res.end("错误请求，检查")
  }
});

server.listen(8888, '127.0.0.1', () => {
  console.log("服务器启动成功！");
})
```

#### (1)URL

> 当得到的URL中携带参数时，通过内置模块**url**、**querystring**提取参数。

```javascript
const http = require('http')
const url = require('url')
// 用于对query进行结构
const qs = require('querystring')

// 创建一个web服务器
const server = http.createServer((req, res) => {
    // URL: http://127.0.0.1:8888/login?username=sfd&id=1
  console.log(url.parse(req.url));
  const {pathname, query} = url.parse(req.url);
  console.log(pathname); //  /login
  console.log(query);//  username=sfd&id=1
  const {username, id} = qs.parse(query);
  console.log(username, id);// 

});

server.listen(8888, '127.0.0.1', () => {
  console.log("服务器启动成功！");
})
```

![image-20220116205438889](D:\Typora笔记\web\Node.js\img\URL.png)

#### (2)method

* GET：数据查询；
* POST：新建数据；
* PATCH：更新数据；
* DELETE：删除数据；

```javascript
// 程序中如何进行判断以及获取对应的数据呢？
// 这里我们需要判断接口是 /users，并且请求方式是POST方法去获取传入的数据；
// 获取这种body携带的数据，我们需要通过监听req的 data事件来获取；

const http = require('http')
// 导入url模块，用于获取req中的url中的pathname
const url = require('url')
// 用于对query进行结构
const qs = require('querystring')

// 创建一个web服务器
const server = http.createServer((req, res) => {
  const {pathname} = url.parse(req.url);
  if(pathname === '/login') {
    if(req.method === 'POST') {
      // 拿到body中的数据
      // 将拿到的body中的数据（buffer)转字符串
      req.setEncoding('utf-8')
      req.on('data', (data) => {
        // console.log(data.toString());
        // console.log(data);//字符串
        const {username,password} = JSON.parse(data);
        console.log(username, password);
      })
    }
  }
});
// 启动web服务器
server.listen(8888, '127.0.0.1', () => {
  console.log("服务器启动成功！");
})
```

**注**： 将JSON字符串格式转成对象类型，通过JSON.parse方法即可。

#### (3)headers

>  在request对象的header中也包含很多有用的信息，客户端会默认传递过来一些信息.

![image-20220116235542060](D:\Typora笔记\web\Node.js\img\headers.png)

* **content-type**是这次请求携带的数据的类型： 
* * application/json表示是一个json类型；
  * text/plain表示是文本类型；
  * application/xml表示是xml类型； 
  * multipart/form-data表示是上传文件；

*  **content-length**：文件的大小和长度
*  **keep-alive**：http是基于TCP协议的，但是通常在进行一次请求和响应结束后会立刻中断；但是在http1.1中，所有连接默认是 connection: keep-alive的；不同的Web服务器会有不同的保持 keep-alive的时间；Node中默认是5s中；
*  **accept-encoding**：告知服务器，客户端支持的文件压缩格式，比如js文件可以使用gzip编码，对应 .gz文件；
*  **accept**：告知服务器，客户端可接受文件的格式类型；
*  **user-agent**：客户端相关的信息；

### 4.response对象

#### (1)返回响应结果

>  如果我们希望给客户端响应的结果数据，可以通过两种方式:wirte方法和end方法；
>
>  如果我们没有调用 end和close，客户端将会一直等待结果，所以客户端在发送网络请求时，都会设置超时时间。

*  **write方法**：这种方式是直接写出数据，但是并没有关闭流；
* **end方法**：这种方式是写出最后的数据，并且写出后会关闭流；

```javascript
const http = require('http')
const server = http.createServer((req, res) => {
  // 响应结果
  res.write("hello world")
  res.end('hello serve')
});
server.listen(8888, 'localhost', () => {
  console.log("服务器启动成功！");
})
```

#### (2)返回状态码

>  Http状态码（Http Status Code）是用来表示Http响应状态的数字代码，Http状态码非常多，可以根据不同的情况，给客户端返回不同的状态码；

![image-20220117000552580](D:\Typora笔记\web\Node.js\img\statecode.png)

* **res.statusCode = 200;**
* **res.writeHead(400);**

```javascript
const http = require('http')
const server = http.createServer((req, res) => {
  // 设置状态码
  // 方式一：直接给属性赋值
  // res.statusCode = 400;
  // 方式二：和head一起设置
  res.writeHead(400, {
    // 这里是header内容,如content-type等属性
  })
  // 响应结果
  res.write("姐hi")
  res.end('hello serve')
});
server.listen(8888, 'localhost', () => {
  console.log("服务器启动成功！");
})
```

#### (3)返回响应头

> Header设置 Content-Type有什么作用呢？
>
> 默认客户端接收到的是字符串，客户端会按照自己默认的方式进行处理；

 返回头部信息，主要有两种方式：

* **res.setHeader**：一次写入一个头部信息；
* **res.writeHead**：同时写入header和status；

```javascript
const http = require('http')
const server = http.createServer((req, res) => {
  // 返回响应header
  // 方式一：
  // res.setHeader("Content_Type", "text/plain;chartset=utf8")
  // 方式二：
  res.writeHead(200, {
    "Content_Type": "text/html;chartset=utf8"
  })
  // 响应结果
  res.end("<h2>heol</h2>")
});
server.listen(8888, 'localhost', () => {
  console.log("服务器启动成功！");
})
```

### 5.http中发送网络请求

>  axios库可以在浏览器中使用，也可以在Node中使用：
>
> 在浏览器中，axios使用的是封装xhr；
>
> 在Node中，使用的是http内置模块；

```javascript
const http = require('http')

// http发送get请求
// http.get('http://localhost:8888', (res) => {
//   res.on('data', (data) => {
//     console.log(data.toString());
//   });
//   res.on('end', () => {
//     console.lo("获取到了所有的结果!");
//   })
// })

// http发送post请求
const req = http.request({
  method: 'POST',
  hostname: 'localhost',
  port: 8888
}, (res) => {
  res.on('data', data => {
    console.log(data.toString());
    console.log(JSON.parse(data.toString()));
  })
})
```

### 6.文件上传

**方法一：**

![image-20220117001445248](D:\Typora笔记\web\Node.js\img\方法一.png)

**方法二**：

![image-20220117001523985](D:\Typora笔记\web\Node.js\img\方法二.png)





## Express

>  Express整个框架的核心就是中间件。

### 一、安装Express

**方式一**：通过express提供的脚手架，直接创建一个应用的骨架；

> 安装脚手架 **npm install -g express-generator** 
>
> 创建项目 express express-demo 
>
> 安装依赖 **npm install** 
>
> 启动项目 **node bin/www**

**方式二**：从零搭建自己的express应用结构；

> 生产package.json文件：**npm init -y**
>
> 手动安装express: **npm install express**



### 二、基本使用

请求的路径中如果有一些参数，可以这样表达： 

* users/:userId； 
* 在request对象中药获取可以通过 req.params.userId;

返回数据，我们可以方便的使用json： 

* res.json(数据)方式； 
* 可以支持其他的方式，可以查看文档；https://www.expressjs.com.cn/guide/routing.html

### 三、中间件

> 中间件的本质是传递给express的一个回调函数；这个回调函数接受三个参数：
>
> * 请求对象（request对象）；
> * 响应对象（response对象）；
> * next函数（在express中定义的用于执行下一个中间件的函数）；

#### 1.最普通的中间件

```javascript
const express = require('express')
const app = express();
// 编写普通的中间件
// use注册一个中间件（回调函数）
// 默认响应第一个中间件
// 若需要响应其他中间件，需要调用next()
app.use((req, res, next) => {
  console.log("注册了第1个普通的中间件");
  res.end("hello world");
  next();
})

app.use((req, res, next) => {
  console.log("注册了第2个普通的中间件");
  // res.end("hello world");  //前面已经调用过end了，已经结束了周期，再调用会报错
  // 所以一般end出现在最后一个普通中间件
  next()
})

app.use((req, res, next) => {
  console.log("注册了第3个普通的中间件");
})

app.listen(8000, () => {
  console.log("普通中间件服务器启动成功");
})
```

#### 2.匹配路径中间件

```javascript
const express = require('express')
const app = express();

// 中间件：查找所有路径匹配的中间件，只执行第一个满足的中间件，除非第一个中调用了next

app.use((req, res, next) => {
  console.log("home middleware 03");
  res.end("01");
  // next();
})

// 路径匹配中间件  与请求关系无关，与路径有关
app.use('/home', (req, res, next) => {
  console.log("home middleware 01");
  res.end("01");
  next();
})
// 永远是第一个中间件
app.use('/home', (req, res, next) => {
  console.log("home middleware 02");
})

app.listen(8000, () => {
  console.log("普通中间件服务器启动成功");
})
```

#### 3.匹配路径和请求方法中间件

```javascript
const express = require('express')
const app = express();
// 路径和方法都匹配的中间件
app.get('/home', (req, res, next) => {
  console.log("home path and method middlelevel01");
})

app.post('/home', (req, res, next) => {
  console.log("home path and method middlelevel02");
})

app.listen(8000, () => {
  console.log("普通中间件服务器启动成功");
})
```

#### 4.连续注册中间件

```javascript
const express = require('express')
const app = express();

app.use((req, res, next) => {
  console.log("home middleware 01");
  next();
})

app.get('/home', (req, res, next) => {
  console.log("home middleware 01");
  next();
}, (req, res, next) => {
  console.log("home middleware 02");
  next();
}, (req, res, next) => {
  console.log("home middleware 03");
  next();
}, (req, res, next) => {
  console.log("home middleware 04");
  res.end();
})

app.listen(8000, () => {
  console.log("普通中间件服务器启动成功");
})
```

#### 5.中间件应用

**body解析**：

```javascript
const express = require('express')
const app = express();
// 处理body信息
// app.use((req, res, next) => {
//   if (req.headers["content-type"] === 'application/json') {
//     req.on('data', (data) => {
//       console.log(data.toString());
//       const info = JSON.parse(data.toString())
//       req.body = info;
//     });
//     req.on('end', () => {
//       next();
//     })
//   }
// })

// 手写太麻烦了。有写好的
// body-parser
app.use(express.json())
// extended :
// true:对urlencoded解析时用的第三方库：qs
// false:对urlencoded解析时用的Node内置模块：querystring
app.use(express.urlencoded({extended:true}))//解析的是 application/x-www-form-urlencoded：



app.post('/login', (req, res, next) => {
  console.log(req.body);
  res.end("coder, welcome back");
})
app.post('/products', (req, res, next) => {
  console.log(req.body);
  res.end("uplog");
})

app.listen(8000, () => {
  console.log("普通中间件服务器启动成功");
})
```



**请求日志记录**:使用第三方中间件：**morgan**(需要单独安装)

```javascript
const fs = require('fs')
const express = require('express')
const morgan = require('morgan')

const app = express();

const writeStream = fs.createWriteStream('./logs/access.log', {
  flags: 'a+'
})

app.use(morgan("combined", {stream: writeStream}))
app.get('/home', (req, res, next) => {
  res.end("hello")
})
app.listen(8000, () => {
  console.log("解析服务器启动成功");
})
```

**上传文件中间件 – 添加后缀名**:这里不在详细演示



### 四、参数解析

>  客户端传递到服务器参数的方法常见的是5种：
>
> * 方式一：通过get请求中的URL的params；
> * 方式二：通过get请求中的URL的query；
> * 方式三：通过post请求中的body的json格式（中间件中已经使用过）；
> * 方式四：通过post请求中的body的x-www-form-urlencoded格式（中间件使用过）； 
> * 方式五：通过post请求中的form-data格式（中间件中使用过）；

##### 1.传递参数params

> 请求地址：http://localhost:8000/login/abc/why

##### 2.传递参数query

> 请求地址：http://localhost:8000/login?username=why&password=123

```javascript
const express = require('express')
const app = new express();

app.use('/login/:id/:name', (req, res, next) => {
  console.log(req.params); // { id: 'abc', name: 'why' }
  res.end('请求成功')
})

app.use('/login', (req, res, next) => {
  console.log(req.query); // { username: 'why', password: '123' }
  res.end('请求成功')
})

app.listen(8000, () => {
  console.log("express初体验服务器启动~");
})
```



### 五、响应数据

* **end方法** ：类似于http中的response.end方法，用法是一致的 
* **json方法** ：json方法中可以传入很多的类型：object、array、string、boolean、number、null等，它们会被转换成 json格式返回；
* **status方法**：用于设置状态码；
* **更多响应的方式**：https://www.expressjs.com.cn/4x/api.html#res



### 六、express路由

> 使用 express.Router来创建一个路由处理程序： 一个Router实例拥有完整的中间件和路由系统；

**路由：**

```javascript
const express = require('express')
const router = express.Router();

router.get('/', (req, res, next) => {
  res.json(["why","koce","dksf"])
})

router.get('/:id', (req, res, next) => {
  res.json(`${req.params.id}用户信息`)
})

router.post('/', (req, res, next) => {
  res.json("sdfsdf")
})

module.exports = router;
```

**请求**：

```javascript
const express = require('express')
const router = require('./12.express路由1')

const app = express();

app.use('/user', router);
app.use('/user/id', router);

app.listen(8000, () => {
  console.log("启动成功");
})
```



### 七、静态资源服务器

> Node也可以作为静态资源服务器，并且express给我们提供了方便部署静态资源的方法**static()**



### 八、服务端的错误处理





## Koa

### 一、koa基本使用

koa注册的中间件提供了两个参数： **ctx和next**

* **ctx**：上下文（Context）对象；
* * koa并没有像express一样，将req和res分开，而是将它们作为 ctx的属性； 
  * ctx代表依次请求的上下文对象； 
  * ctx.request：获取请求对象； 
  * ctx.response：获取响应对象； 
* **next**：本质上是一个dispatch，类似于之前的next；

```javascript
// koa导出的是一个类
const Koa = require('koa')

const app = new Koa();

app.use((ctx, next) => {
  ctx.response.body = "hello world";
  console.log("中间件被执行");
})

app.listen(8000, () => {
  console.log("koa服务器启动成功");
})
```

### 二、koa中间件

> koa通过创建的app对象，注册中间件只能通过use方法：Koa并没有提供methods的方式来注册中间件；也没有提供path中间件来匹配路径；

真实开发中我们如何将路径和method分离呢？

* 方式一：根据request自己来判断；
* 方式二：使用第三方路由中间件

```javascript
const Koa = require('koa')
const app = new Koa();
// 注册中间件，没有提供POST，GET,path匹配方式以及连续注册的方式等
app.use((ctx, next) => {
  if(ctx.request.url === '/login') {
    if (ctx.request.method === 'GET') {
      console.log("中间件被执行");
      ctx.response.body = "login success"
    }
  } else {
    ctx.response.body = "hello world";
  }
})

app.listen(8000, () => {
  console.log("koa服务器启动成功");
})
```

### 三、路由的使用

> koa官方并没有给我们提供路由的库，我们可以选择第三方 库：**koa-router**
>
> **npm install koa-router**

**路由**：

```javascript
const Router = require('koa-router')
const router = new Router({prefix: '/users'});

// koa本来没有put这个方式，但是路由有这个方式
router.get('/', (ctx, next) => {
  ctx.response.body = "User listex";
})

router.put('/', (ctx, next) => {
  ctx.response.body = "put request~";
})

module.exports = router;
```

**请求**：

```javascript
const Koa = require('koa')
const userRouter = require('./router/uer')
const app = new Koa();

app.use((ctx, next) => {
  // ctx.response.body = "hello word"
  next();
})

app.use(userRouter.routes());
app.use(userRouter.allowedMethods())

app.listen(8000, () => {
  console.log("koa服务器启动成功");
})
```

**注**：allowedMethods用于判断某一个method是否支持： 

* 如果我们请求 get，那么是正常的请求，因为我们有实 现get； 
* 如果我们请求 put、delete、patch，那么就自动报错： Method Not Allowed，状态码：405；
* 如果我们请求 link、copy、lock，那么久自动报错： Not Implemented，状态码：501；



### 四、参数解析

#### 1.params - query

```javascript
const Koa = require('koa')
const app = new Koa();
const Router = require('koa-router')

// 请求地址：http://localhost:8000/users/123
// 通过路由解析params
const userRouter = new Router({prefix: '/users'})
userRouter.get('/:id', (ctx, next) => {
  console.log(ctx.request.params.id); // 123
})

// 请求地址：http://localhost:8000/login?username=why&password=123
// 解析query
app.use((ctx, next) => {
  console.log(ctx.request.query); //{ username: 'why', password: '123' }
  ctx.response.body = "hello word"
})
app.use(userRouter.routes())

app.listen(8000, () => {
  console.log("koa服务器启动成功");
})
```

#### 2.解析json

> 获取json数据： 
>
> * 安装依赖： npm install koa-bodyparser;
> * 使用 koa-bodyparser的中间件；

#### 3.解析x-www-form-urlencoded

```javascript
const Koa = require('koa')
const bodyParser = require('koa-bodyparser')
const multer = require('koa-multer');
const Router = require('koa-router');

const app = new Koa();
const upload = multer();

app.use(bodyParser())
app.use(upload.any())


// 解析json
app.use((ctx, next) => {
  console.log(ctx.request.body); // { title: '华为', prise: '23' }
  ctx.response.body = "hello world"
})

app.listen(8000, () => {
  console.log("koa服务器启动成功");
})
```

#### 4.文件上传Multer

![image-20220118220629991](D:\Typora笔记\web\Node.js\img\文件上传.png)



### 五、数据的响应

> 输出结果：body将响应主体设置为以下之一： 
>
> * **string** ：字符串数据 
> * **Buffer** ：Buffer数据 
> * **Stream** ：流数据 
> * **Object|| Array**：对象或者数组
> * **null** ：不输出任何内容 
> * 如果response.status尚未设置，Koa会自动将状态设置为200或204。

```javascript
const Koa = require('koa')
const app = new Koa();

app.use((ctx, next) => {
  console.log(ctx.request.body);
  // 设置内容
  // ctx.response.body = "hello world"
  // ctx.response.body = {
  //   name: 'coder',
  //   age: 20,
  //   rul: 'dsf'
  // }
  // 设置状态码
  ctx.status = 200
  // ctx.response.body = ["dfdsf", "df", "df"]
  // 简写
  ctx.body = "dfjsf"
  
})

app.listen(8000, () => {
  console.log("koa服务器启动成功");
})
```

### 六、静态服务器

> koa并没有内置部署相关的功能，所以我们需要使用第三方库：
>
> **npm install koa-static**

![image-20220118222855652](D:\Typora笔记\web\Node.js\img\静态服务器.png)

### 七、错误处理

![image-20220118222931556](D:\Typora笔记\web\Node.js\img\错误处理.png)



## cookie session token

### 一、cookie

>  * Cookie（复数形态Cookies），又称为“小甜饼”。类型为“小型文本文件，某些网站为了辨别用户身份而存储 在用户本地终端（Client Side）上的数据。
>
>  * Cookie总是保存在客户端中，按在客户端中的存储位置，Cookie可以分为内存Cookie和硬盘Cookie。  
>  * * 内存Cookie由浏览器维护，保存在内存中，浏览器关闭时Cookie就会消失，其存在时间是短暂的；  
>    * 硬盘Cookie保存在硬盘中，有一个过期时间，用户手动清理或者过期时间到时，才会被清理；

#### 1.cookie常见属性

**cookie的生命周期**： 

* 默认情况下的cookie是内存cookie，也称之为会话cookie，也就是在浏览器关闭时会自动被删除； 
* 我们可以通过设置expires或者max-age来设置过期的时间；
* * expires：设置的是Date.toUTCString()，设置格式是;expires=date-in-GMTString-format；
  * max-age：设置过期的秒钟，;max-age=max-age-in-seconds (例如一年为60*60*24*365)；

**cookie的作用域**：（允许cookie发送给哪些URL） 

* Domain：指定哪些主机可以接受cookie Ø 如果不指定，那么默认是 origin，不包括子域名。 Ø 如果指定Domain，则包含子域名。例如，如果设置 Domain=mozilla.org，则 Cookie 也包含在子域名中（如developer.mozilla.org）。 
* Path：指定主机下哪些路径可以接受cookie Ø 例如，设置 Path=/docs，则以下地址都会匹配：  /docs   /docs/Web/      /docs/Web/HTTP

#### 2.客户端设置cookie

* js直接设置和获取cookie

`console.log(document.cookie);`

* 这个cookie会在会话关闭时被删除

```javascript
// 设置国过期时间就是本地cookie，不设置就是内存cookie
document.cookie = 'name=coderwhy';
document.cookie = 'age=18';
```

* 设置cookie同时设置时间（默认单位是秒钟）

`document.cookie = 'name=coderwhy;max-age=5'`

#### 3.服务器设置cookie

```javascript
const Koa = require('koa')
const Router = require('koa-router')
const app = new Koa();
const testRouter = new Router();

// /test请求中设置cookie
testRouter.get('/test', (ctx, next) => {
  ctx.cookies.set("name", "lilei", {
    // maxAge对应毫秒
    maxAge: 50 * 1000
  })
  ctx.body = "test"
})
// /demo请求中获取cookie
testRouter.get('/demo', (ctx, next) => {
  // 读取cookie
  const value = ctx.cookies.get('name');
  console.log(value);
})

app.use(testRouter.routes());
app.use(testRouter.allowedMethods());

app.listen(8002, () => {
  console.log("服务器启动成功");
})
```



### 二、session

```javascript
const Koa = require('koa')
const Router = require('koa-router')
const Session = require('koa-session')
const app = new Koa();
const testRouter = new Router();

// 创建session的配置
const session = Session({
  key: 'sessionid',
  maxAge: 10 * 1000,
  signed: true
}, app);
app.keys = ['aaaa']
app.use(session)


// 登录
testRouter.get('/test', (ctx, next) => {
  // 数据库中查到了id和name
  const id = 110;
  const name = "coderwhy"
  // session携带id和name信息
  ctx.session.user = {id,name};

  ctx.body = "test"
})
testRouter.get('/demo', (ctx, next) => {
  console.log(ctx.session.user);
  ctx.body = "demo"
})

app.use(testRouter.routes());
app.use(testRouter.allowedMethods());
app.listen(8002, () => {
  console.log("服务器启动成功");
})
```



