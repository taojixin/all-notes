## 一、基本步骤

### 1.创建组件构造器

> 调用Vue.extend()方法创建组件构造器。

* 通常在创建组件构造器时，传入**template**代表我们自定义组件的模板。该模板就是在使用到组件的地方，要显示的HTML代码。(此种方法很少使用)

### 2.注册组件

> 调用Vue.component()方法注册组件。

* 调用Vue.component()是将刚才的组件构造器注册为一个组件，并且给它起一个组件的标签名称。所以需要传递两个参数：1、注册组件的标签名 2、组件构造器

### 3.使用组件

> 在Vue实例的作用范围内使用组件。

```html
<body>
    <div id="app">
        <!-- 3.使用组件 -->
        <my-cpn></my-cpn>
        <my-cpn></my-cpn>
        <my-cpn></my-cpn>
    </div>

    <script>
        //1.创建组件构造器
        const cpnC = Vue.extend({
            template:`
                <div>
                    <h2>我是标题</h2>
                    <p>我是内容，哈哈哈</p>
                    <p>我是内容，呵呵呵</p>
                </div>`
        })

        //2.注册组件(全局组件)
        // Vue.component("组件标签名", 组件构造器)
        Vue.component("my-cpn", cpnC);

        const app = new Vue({
            el: '#app',
            data: {
                
            },
        })

    Vue.config.productionTip = false
    </script>
</body>
```

## 二、全局组件与局部组件

* 当我们通过调用**Vue.component**()注册组件时，组件的注册是全局的,这意味着该组件可以在任意**Vue**示例下使用。
* 如果我们注册的组件是**挂载在某个实例中**, 那么就是一个**局部组件**

```html
<body>
    <div id="app">
        <cpn></cpn>
        <cpn></cpn>
        <cpn></cpn>
    </div>
    <div id="root">
        <cpn></cpn>
        <cpn></cpn>
        <cpn></cpn>
    </div>

    <script>
        //1.创建组件构造器
        const cpnC = Vue.extend({
            template:`
                <div>
                    <h2>我是标题</h2>
                    <p>我是内容，哈哈哈</p>
                    <p>我是内容，呵呵呵</p>
                </div>`
        })
        // //2.注册组件(全局组件,意味着可以在多个Vue实例下面使用)
        // Vue.component("cpn", cpnC);

        const app1 = new Vue({
            el: '#app',
            data: {
                
            },
            //这里注册局部组件,只能在该Vue实例下面使用 
            components:{
                cpn: cpnC
            }
        });
        const app2 = new Vue({
            el: '#root',
            data: {
                
            },
        })

    Vue.config.productionTip = false
    </script>
</body>
```



## 三、父组件与子组件

* 父子组件**错误用法**：**以子标签的形式在Vue实例中使用**

1.因为当子组件注册到父组件的components时，Vue会编译好父组件的模块

2.该模板的内容已经决定了父组件将要渲染的HTML（相当于父组件中已经有了子组件中的内容了）

3.< cpn1>< /cpn1>是只能在父组件中被识别的。

```html
<body>
    <div id="app">
        <cpn2></cpn2>
    </div>

    <script>
        //1.创建第一个组件构造器（子组件）
        const cpnC = Vue.extend({
            template:`
                <div>
                    <h2>我是标题1</h2>    
                    <p>内容1</p>
                </div>`
        });
        //创建第二个组件构造器(父组件)
        const cpnC2 = Vue.extend({
            template:`
                <div>
                    <h2>我是标题2</h2>    
                    <p>内容2</p>
                    <cpn1></cpn1>
                </div>`,
            components:{
                cpn1: cpnC,//在父组件中声明子组件
            }
        })

        const app = new Vue({
            el: '#app',
            data: {
                
            },
            components:{
                cpn2: cpnC2
            }
        })

    Vue.config.productionTip = false
    </script>
</body>
```



## 四、注册组件的语法糖

> 主要是省去了调用Vue.extend()的步骤，而是可以直接使用一个对象来代替。

```html
<body>
    <div id="app">
        <cpn1></cpn1>
        <cpn2></cpn2>
    </div>

    <script>
        //全局注册组件语法糖写法
        // const cpnC1 = Vue.extend()
        Vue.component("cpn1",{
            template:`
                <div>
                    <h2>我是标题</h2>    
                    <p>内容</p>
                </div>`
        });


        const app = new Vue({
            el: '#app',
            data: {
                
            },
            components:{
                //局部组件语法糖
                cpn2:{
                    template:`
                        <div>
                            <h2>我是标题2</h2>    
                            <p>内容2</p>
                        </div>`
                } 
            }
        })

    Vue.config.productionTip = false
    </script>
</body>
```



## 五、组件模板抽离

Vue提供了两种方案来定义HTML模块内容：

* 使用< script>标签
* 使用< template>标签

```html
<body>
    <div id="app">
        <cpn></cpn>
    </div>

    <!-- 方法1：<script type="text/x-template" id="temp"> -->
    <!-- <script type="text/x-template" id="temp">
        <div>
            <h2>标题</h2>
            <p>内容</p>
        </div>
    </script> -->

    <!-- 方法2： -->
    <template id="temp">
        <div>
            <h2>标题</h2>
            <p>内容</p>
        </div>
    </template>
    
    <script>
        Vue.component("cpn",{
            template:"#temp"
        })


        const app = new Vue({
            el: '#app',
            data: {
                
            },
        })

    Vue.config.productionTip = false
    </script>
</body>
```



## 六、组件中的数据存放问题

> 组件是一个单独功能模块的封装：这个模块有属于自己的HTML模板，也应该有属性自己的数据data。
>
> 组件中的数据是保存在哪里呢？**顶层的Vue实例中吗？**答：不在顶层的Vue实例中，Vue组件有**自己保存数据的地方**。

* 组件对象也有一个data属性(也可以有methods等属性，下面我们有用到)，只是这个data属性必须是一个函数，而且这个函数返回一个对象，对象内部保存着数据。

* 为什么data在组件中必须是一个函数呢?  原因是在于Vue让每个组件对象都返回一个新的对象，因为如果是同一个对象的，组件在多次使用后会相互影响。

```html
<body>
    <div id="app">
        <!-- 这里的content是 数组数据 -->
        <cpn></cpn>
        <!-- 这里的content是 title -->
        <cpn2></cpn2>
    </div>

    <template id="temp">
        <div>
            <h2>标题</h2>
            <p>{{content}}</p>
        </div>
    </template>
    
    <script>
        //Vue组件
        Vue.component("cpn", {
            template:"#temp",
            data() {//这里的data必须是函数
                return {
                    content: "组件数据"
                }
            }
        });
        //顶层Vue
        const app = new Vue({
            el: '#app',
            data: {
                content: "根数据"
            },
            components:{
                cpn2:{
                    template:"#temp",
                    data() {
                        return {
                            content: "title"
                        }
                    }
                }
            }
        })

    Vue.config.productionTip = false
    </script>
</body>
```



## 七、父子组件的通讯

### 1.通过props向子组件传递数据

#### (1)props的值有两种方式

* 方式一：字符串数组，数组中的字符串就是传递时的名称。

* 方式二：对象，对象可以设置传递时的类型，也可以设置默认值等。

类型可以是： String Number Boolean Array Object Date Function Symbol

```html
<body>
    <div id="app">
        <div>
             内容
        </div>
        <cpn v-bind:cmovies="movies" ></cpn>//注意这里要用v-bind绑定数据
    </div>

    <template id="temp">
        <!-- div不能省略 -->
        <div>
            <p>{{cmessage}}</p>
            <p>{{cmovies}}</p>
            <ul>
                <li v-for="item in cmovies">{{item}}</li>
            </ul>
        </div>
    </template>

    <script>
        // const cpn = Vue.extend({
        //     template:"#temp",  //此处#忘记加了
        //     data() {
        //         return {}
        //     },
        //     props:["cmovies","cmessage"],
        // });
        // 可以简写为
        const cpn = {
            template:"#temp",  //此处#忘记加了
            data() {
                return {}
            },
            // 方式一：字符串数组，数组中的字符串就是传递时的名称。
            // props:["cmovies","cmessage"],
            // 方式二：对象，对象可以设置传递时的类型，也可以设置默认值等。
            props:{
                // 1.类型限制
                cmovies: Array,
                cmessage: String,
                
                // 2.可以是多个可能的类型
                // cmessage: [String,Number]

                // 3.提供一些默认值
                // cmessage:{
                //     type: String,
                //     default: "aaaaaaaa"
                // }

                // 4.必须传递值
                // cmessage:{
                //     type: String,
                //     required: true,
                // }

                // 5.type是对象或数组时必须从工厂函数获取
                // cmessage: {
                //     type: Object,
                //     default() {//这里必须是工厂函数
                //        return {
                //            cmessage:"hello"
                //        } 
                //     }
                // }

                // 6.自定义验证函数
            }

        }

        const app = new Vue({
            el: '#app',
            data: {
                movies:["该往","发生的反对","范德萨"],
                message: "sfd"
            },
            components:{
                cpn
                // 也可以写成
                // cpn:{
                //     template:"#temp",  //此处#忘记加了
                //     data() {
                //         return {}
                //     },
                //     props:["cmovies","cmessage"],
                // }
            }
            
            
        })

    Vue.config.productionTip = false
    </script>
</body>
```



#### (2)驼峰标识问题

```html
<body>
    <div id="app">
        <!-- 驼峰标识，这里需要使用c-message的形式 -->
        <cpn :c-message="message"></cpn>
    </div>


    <template id="temp">
        <div>
            <!-- 这里直接驼峰标识就可以了，不用c-message的形式 -->
            <h2>{{cMessage}}</h2>
            <h2>{{cMessage}}</h2>
        </div>
    </template>
    <script>

        const app = new Vue({
            el: '#app',
            data: {
                message: [12,21,312]
            },
            components:{
                cpn:{
                    template:"#temp",//又一次忘了#
                    props:{
                        cMessage: {
                            type: Array,
                            default() {
                                return "默认值"
                            }
                        }
                    }
                }
            }
        })

    Vue.config.productionTip = false
    </script>
</body>
```



### 2.通过事件向父组件发送消息

**自定义事件的流程：**

1.在子组件中，通过$emit()来触发事件。

2.在父组件中，通过v-on来监听子组件事件。

```html
<body>
    <div id="app">
        <!-- cpnclick这里省略参数后，默认将item传过去 -->
        <!-- 父组件监听子组件发射的itemclick事件，当收到子组件发射的自定义事件(itemclick事件)后执行事件cpnclick -->
        <cpn v-on:itemClick="cpnclick"></cpn>
    </div>

    <template id="temp">
        <div>
            <!-- 当点击了按钮触发btnclicl事件，btnclick(item)事件的作用是将自定义事件发射给父组件 -->
            <button v-for="item in choice" @click="btnclick(item)">{{item.name}}</button>
        </div>
    </template>
    <script>
        //子组件
        const cpn = {
            template:"#temp",
            data() {
                return {
                    choice:[
                    {id: 'aaa', name: '热门推荐'},
                    {id: 'bbb', name: '手机数码'},
                    {id: 'ccc', name: '家用电器'},
                    {id: 'ddd', name: '电脑办公'},
                    ]
                }
            },
            methods: {
                btnclick(item) {
                    // 发射事件(itemclick)给父组件
                    this.$emit('itemclick',item);//itemclick事件名称，itemclick为自定义事件,item为传递的参数
                }
            }
        }

        const app = new Vue({
            el: '#app',
            data: {
                
            },
            components: {
                cpn
            },
            methods: {
                cpnclick(item) {
                    console.log(item);
                }
            }
        })

    Vue.config.productionTip = false
    </script>
</body>
```

### 3.父组件访问子组件

> 父组件访问子组件：使用$children或$refs

**$children的缺陷：**

* 通过$children访问子组件时，是一个数组类型，访问其中的子组件必须通过索引值。
* 但是当子组件过多，我们需要拿到其中一个时，往往不能确定它的索引值，甚至还可能会发生变化。
* 有时候，我们想明确获取其中一个特定的组件，这个时候就可以使用$refs

**$refs的使用：**

* $refs和ref指令通常是一起使用的。
* 首先，我们通过ref给某一个子组件绑定一个特定的ID。
* 其次，通过this.$refs.ID就可以访问到该组件了。

```html
<body>
    <div id="app">
        <cpn></cpn>
        <cpn></cpn>
        <cpn ref="aaa"></cpn>
        <button @click="btnClick">按钮</button>
    </div>

    <template id="temp">
        <div>我是子组件</div>
    </template>
    <script>
        const app = new Vue({
            el: '#app',
            data: {
                message: "你好啊"
            },
            methods: {
                btnClick() {
                    // 1.$children （开发中很少用）
                    // console.log(this.$children);
                    // for (let c of this.$children) {
                    //     console.log(c.name);
                    //     c.showMessage();
                    // }

                    // 2.$refs（开发中几乎都用这个方法）
                    console.log(this.$refs.aaa.name);

                }
            },
            components:{
                cpn: {
                    template:"#temp",
                    methods: {
                        showMessage() {
                            console.log("showMessage")
                        }
                    },
                    data() {
                        return {
                            name: "我是子组件的name"
                        }
                    }
                }
            }
        })

    Vue.config.productionTip = false
    </script>
</body>
```

### 4.子组件访问父组件(了解)

> 如果我们想在子组件中直接访问父组件，可以通过$parent

**注意事项：**

* 尽管在Vue开发中，我们允许通过$parent来访问父组件，但是在真实开发中尽量不要这样做。
* 子组件应该尽量避免直接访问父组件的数据，因为这样耦合度太高了。
* 如果我们将子组件放在另外一个组件之内，很可能该父组件没有对应的属性，往往会引起问题。
* 另外，更不好做的是通过$parent直接修改父组件的状态，那么父组件中的状态将变得飘忽不定，很不利于我的调试和维护。

```html
<body>

<div id="app">
  <cpn></cpn>
</div>

<template id="cpn">
  <div>
    <h2>我是cpn组件</h2>
    <ccpn></ccpn>
  </div>
</template>

<template id="ccpn">
  <div>
    <h2>我是子组件</h2>
    <button @click="btnClick">按钮</button>
  </div>
</template>

<script src="../js/vue.js"></script>
<script>
  const app = new Vue({
    el: '#app',
    data: {
      message: '你好啊'
    },
    components: {
      cpn: {
        template: '#cpn',
        data() {
          return {
            name: '我是cpn组件的name'
          }
        },
        components: {
          ccpn: {
            template: '#ccpn',
            methods: {
              btnClick() {
                // 1.访问父组件$parent
                // console.log(this.$parent);
                // console.log(this.$parent.name);

                // 2.访问根组件$root
                console.log(this.$root);
                console.log(this.$root.message);
              }
            }
          }
        }
      }
    }
  })
</script>

</body>
```



### 5.slot插槽

#### (1)默认插槽







#### (2)具名插槽







#### (3)作用域插槽



