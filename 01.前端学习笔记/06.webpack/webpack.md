# webpack

## 一、webpack基本介绍

### 1.安装

> **Webpack**的运行是依赖**Node环境**的，所以我们电脑上必须有Node环境。
>
> **webpack**的安装目前分为两个：**webpack**、**webpack-cli**

* webpack与webpack-cli的**关系**：
* *  执行webpack命令，会执行node_modules下的.bin目录下的webpack； 
  * webpack在执行时是依赖webpack-cli的，如果没有安装就会报错； 
  * 而webpack-cli中代码执行时，才是真正利用webpack进行编译和打包的过程； 
  * 所以在安装webpack时，我们需要同时安装webpack-cli（第三方的脚手架事实上是没有使用webpack-cli的，而是类似于 自己的vue-service-cli的东西）
* 安装：
* * **npm install webpack webpack-cli –g** # 全局安装 
  * **npm install webpack webpack-cli –D** # 局部安装

### 2.基本使用

* 编写代码后，通过webpack进行打包，之后运行打包之后的代码。在目录下直接执行 webpack 命令。
* 生成一个dist文件夹，里面存放一个main.js的文件，就是我们打包之后的文件：
* * 这个文件中的代码被压缩和丑化了；
  * 另外我们发现代码中依然存在ES6的语法，比如箭头函数、const等，这是因为默认情况下webpack并不清楚 我们打包后的文件是否需要转成ES5之前的语法，后续需要通过babel来进行转换和设置；
* webpack是如何确定我们的入口的呢？
* * 事实上，当我们运行webpack时，webpack会查找当前目录下的 src/index.js作为入口；
  * 所以，如果当前项目中没有存在src/index.js文件，那么会报错



## 二、配置

### 1.指定入口和出口

> 可以通过配置来指定入口和出口。

* 方法一：在**package.json**文件中的**script**下配置 **webpack --entry ./src/main.js --output-path ./build** (不常用，一般使用方法二)

```json
{
  "name": "basic_webpack",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack --entry ./src/main.js --output-path ./build"
  },
  "author": "",
  "license": "ISC",
  "devDependencies": {
    "css-loader": "^6.7.1",
    "webpack": "^5.73.0",
    "webpack-cli": "^4.10.0"
  }
}
```

* 方法二：新建**webpack.config.js**文件，在其中配置

```javascript
const path = require("path")

module.exports = {
  // 设置入口文件
  entry: "./src/main.js",
  // 设置出口文件及打包后的文件名
  output: {
    // 这里必须是绝对路径
    path: path.resolve(__dirname, "./build"),
    filename: "bundle.js"
  }
}
```

### 2.指定配置文件

> 有时我们希望我们的配置文件不是webpack.config.js而是其他的，这时也可以配置

* 在package.json文件中：

```json
{
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "build": "webpack --config wk.config.js"
  },
  "devDependencies": {
    "css-loader": "^6.7.1",
    "webpack": "^5.73.0",
    "webpack-cli": "^4.10.0"
  }
}
```





## 三、loader

> **loader** 可以用于对模块的源代码进行转换； 
>
> 我们可以将css文件也看成是一个模块，我们是通过import来加载这个模块的； 
>
> 在加载这个模块时，webpack其实并不知道如何对其进行加载，我们必须制定对应的**loader**来完成这个功能；

**loader的使用方式：**

* 内联方式
* 配置方式：具体用法见下

### 1.css-loader

> 对于加载css文件来说，我们需要一个可以读取css文件的loader； 这个loader最常用的是css-loader。
>
> 安装：npm install css-loader -D

* 内联方式：`import "css-loader!../css/index.css"`

### 2.loader配置方式

> 配置方式就是在webpack.config.js文件中写明配置信息： 
>
> module.rules中允许我们配置多个loader（因为我们也会继续使用其他的loader，来完成其他文件的加载）；
>
> 这种方式可以更好的表示loader的配置，也方便后期的维护，同时也让你对各个Loader有一个全局的概览；

**module.rules的配置如下：**

* **test属性**：用于对 resource（资源）进行匹配的，通常会设置成正则表达式； 
* **use属性**：对应的值时一个数组：[UseEntry] ，UseEntry是一个对象，可以通过对象的属性来设置一些其他属性。传递字符串（如：use: [ 'style-loader' ]）是 loader 属性的简写方式（如：use: [ { loader: 'style-loader'} ]）；
* * **loader**：必须有一个 loader属性，对应的值是一个字符串；
  * **options**：可选的属性，值是一个字符串或者对象，值会被传入到loader中； 
  * **query**：目前已经使用options来替代；
* **loader属性**： Rule.use: [ { loader } ] 的简写

```javascript
const path = require("path")

module.exports = {
  // 设置入口文件
  entry: "./src/main.js",
  // 设置出口文件及打包后的文件名
  output: {
    // 这里必须是绝对路径
    path: path.resolve(__dirname, "./build"),
    filename: "bundle.js"
  },
  module: {
    // 在rules中配置loader
    rules: [
      {
        // test用于对 resource（资源）进行匹配的，通常会设置成正则表达式；
        test: /\.css$/, // 正在表达式 以css结尾的
        use: [
          {loader: 'style-loader'}, // 先使用的css-loader再styel-loader（从后往前）
          {loader: 'css-loader'}
          // 简写 "css-loader"
        ]
        // 简写：loader: "css-loader",
      },
      {
        test: /\.less$/,
        use: [
          "style-loader",
          "css-loader",
          "less-loader"
        ]
      }
    ]
  }
}
```

### 3.style-loader

> **css-loader**只是负责将**.css文件进行解析**，并不会将解析之后的css插入到页面中； p如果我们希望再完成插入style的操作，那么我们还需要另外一个loader，就是**style-loader**；
>
> 安装：**npm install style-loader -D**
>
> 添加方式同上

### 4.处理less文件

> 首先将less转换为css，在使用css-loader和style-loader。
>
> 这里需要使用less这个工具（安装：npm install less -D），通过less-loader去使用这个工具。
>
> 安装less-loader：**npm install less-loader -D**

### 5.PostCSS

> **PostCSS**是一个通过JavaScript来转换样式的工具；这个工具可以帮助我们进行一些CSS的转换和适配，比如**自动添加浏览器前缀、css样式的重置**；需要借助于PostCSS对应的插件；
>
> 如何使用PostCSS呢？主要就是两个步骤： 
>
> * 第一步：查找PostCSS在构建工具中的扩展，比如webpack中的postcss-loader；
> * 第二步：选择可以**添加**你需要的PostCSS相关的**插件**；

#### (1)命令行使用postcss

> 直接在终端使用PostCSS需要单独安装一个工具**postcss-cli**；前提还要安装**postcss**
>
> 安装：**npm install postcss postcss-cli -D**

#### (2)autoprefixer插件

* 因为我们需要添加前缀，所以要安装autoprefixer： 
* *  npm install autoprefixer -D
*  直接使用使用postcss工具，并且制定使用autoprefixer
* * npx postcss --use autoprefixer -o end.css ./src/css/style.css

#### (3)postcss-loader

> 真实开发中我们必然不会直接使用命令行工具来对css进行处理，而是可以借助于构建工具： 在webpack中使用**postcss**就是使用**postcss-loader**来处理的；
>
> 安装：npm install postcss-loader -D

* postcss需要有对应的插件才会起效果，所以我们需要配置它的**plugin**；

#### (4)单独的postcss配置文件

* 在根目录下创建postcss.config.js文件：

```javascript
module.exports = {
  plugins:[
    require("postcss-preset-env")
  ]
}
```

#### (5)postcss-preset-env

> 事实上，在配置postcss-loader时，我们配置插件并不需要使用autoprefixer。 
>
> 我们可以使用另外一个插件：postcss-preset-env ppostcss-preset-env也是一个postcss的插件； 
>
> 它可以帮助我们将一些现代的CSS特性，转成大多数浏览器认识的CSS，并且会根据目标浏览器或者运行时环境添加所需的polyfill； 
>
> 也包括会自动帮助我们添加autoprefixer（所以相当于已经内置了autoprefixer）；
>
> 安装：**npm install postcss-preset-env -D**

```javascript
const path = require("path")

module.exports = {
  // 设置入口文件
  entry: "./src/main.js",
  // 设置出口文件及打包后的文件名
  output: {
    // 这里必须是绝对路径
    path: path.resolve(__dirname, "./build"),
    filename: "bundle.js"
  },
  module: {
    // 在rules中配置loader
    rules: [
      {
        // test用于对 resource（资源）进行匹配的，通常会设置成正则表达式；
        test: /\.css$/, // 正在表达式 以css结尾的
        use: [
          "style-loader",
          // 先使用的css-loader再styel-loader（从后往前）
          {
            loader: 'css-loader',
            options: {
              // 处理过的loader再处理一次
              importLoaders: 1
            }
          },
          "postcss-loader"

          // 对一下进行抽离
          // {
          //   loader: 'postcss-loader',
          //   // postcss-loader需要使用autoprefixer插件s
          //   options: {
          //     postcssOptions: {
          //       plugins: [
          //         // autoprefixer：用于给一些css样式增加浏览器前缀
          //         // require("autoprefixer"),
          //         // postcss-preset-env：增加浏览器前缀，同时将现代css装化为大部分浏览器可以执行的css，所以postcss-preset-env使用较多
          //         // postcss-preset-env 里面已经包含了 autoprefixer
          //         // require("postcss-preset-env")
          //         // 简写（但不是所有的插件都可以这样简写）
          //         "postcss-preset-env"
          //       ]
          //     }
          //   }
          // }
          // 简写 "css-loader"
        ]
        // 简写：loader: "css-loader",
      },
      {
        test: /\.less$/,
        use: [
          "style-loader",
          {
            loader: 'css-loader',
            options: {
              importLoaders: 2
            }
          },
          "postcss-loader",
          "less-loader"
        ]
      }
    ]
  }
}
```



## 三、浏览器兼容性问题

> 开发中，浏览器的兼容性问题，我们应该如何去解决和处理？这里指的兼容性是针对不同的浏览器支持的特性：比如css特性、js语法，之间的兼容性；

> 查询到浏览器的市场占有率：https://caniuse.com/usage-table

### 1.browserslist工具

> Browserslist是什么？Browserslist是一个在不同的前端工具之间，共享目标浏览器和Node.js版本的配置
>
> *  Autoprefixer 
> * Babel 
> * postcss-preset-env 
> * eslint-plugin-compat 
> * stylelint-no-unsupported-browser-features 
> * postcss-normalize 
> * obsolete-webpack-plugin

**Browserslist编写规则**：

![image-20220630111320793](.\images\编写规则1.png)

![image-20220630111404076](.\images\编写规则2.png)

### 2.命令行使用browserslist

> **npx browserslist ">1%, last 2 version, not dead"**

### 3.配置browserslist

* 在package.json中配置：

```json
{
  "browserslist": [
    ">1%",
    "last 2 version",
    "not dead"
  ]
}
```

* 创建**.browserslistrc**文件进行配置

```
>1%
last 2 version
not dead
```

### 4.默认配置和条件关系

![image-20220630111749966](.\images\默认配置.png)



