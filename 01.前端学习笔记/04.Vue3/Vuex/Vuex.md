# Vuex

## 一、Vuex基本使用

> Vuex的状态存储是响应式的 ，当Vue组件从store中读取状态的时候，若store中的状态发生变化，那么相应的组件也会被更新；
>
> 不能直接改变store中的状态，改变store中的状态的唯一途径就显示提交 (**commit**) **mutation**；这样使得我们可以方便的跟踪每一个状态的变化，从而让我们能够通过一些工具帮助我们更好的管理应用的状态；
>
> Vuex由五大部分组成：state,getters,mutations,modules,actions

### 1.使用步骤

* 创建Store对象

```javascript
import { createStore } from "vuex"

const store = createStore({
  state() {
    return {
      counter: 0,
      name: 'tjx',
      age: 18,
      height: 180
    }
  },
  mutations: {
    increment(state) {
      state.counter++
    }
  },
  getters: {
  },
  actions: {
  }
});


export default store
```

* 在app中通过插件安装

```javascript
import { createApp } from 'vue'
import App from './App.vue'
import store from "./store"

createApp(App).use(store).mount('#app')
```

### 2.组件中使用store

* 在模板中使用

```html
<h2>Home: {{$store.state.counter}}</h2>
```

* 在option API中使用，如computed

```javascript
computed: {
	sCounter() {
		return this.$store.state.counter
	}
}
```

* 在setup中使用

```javascript
<script>
import {useStore,mapState} from "vuex"
import {computed} from 'vue'
  export default {
    setup() {
      const store = useStore()
      const sCounter = computed(() => store.state.counter)
      
      return {
        sCounter
      }
    }
  }
</script>
```



## 二、state

### 1.mapState辅助函数

> 如果我们有很多个状态都需要获取话，可以使用**mapState**的辅助函数：

* mapState的方式一：**对象类型**；
* mapState的方式二：**数组类型**；
* 也可以使用展开运算符和来原有的computed混合在一起；

**在optionAPI中使用辅助函数：**

```vue
<template>
  <div>
    <h2>Home: {{$store.state.counter}}</h2>
    <h2>Home: {{sCounter}}</h2>
    <h2>Home: {{sNamge}}</h2>
    <h2>Home: {{age}}</h2>
    <h2>Home: {{height}}</h2>
  </div>
</template>

<script>
import {mapState} from "vuex"
  export default {
    computed: {
      // 辅助函数mapState返回的是一个对象
      // 1.数组写法
      ...mapState(["counter", "name", "age", "height"])
      // 2.对象写法:可以重命名
      ...mapState({
        sCounter: state => state.counter,
        sNamge: state => state.name
      })
    }
  }
</script>

<style scoped>

</style>
```

### 2.在setup中使用mapState

```vue
<template>
  <div>
    <h2>Home: {{sCounter}}</h2>
    <hr>
    <h2>Home: {{counter}}</h2>
    <h2>Home: {{name}}</h2>
    <h2>Home: {{age}}</h2>
    <h2>Home: {{height}}</h2>
  </div>
</template>

<script>
import {useStore,mapState} from "vuex"
import {computed} from 'vue'
  export default {
    setup() {
      const store = useStore()
      const sCounter = computed(() => store.state.counter)

      // 因为mapState返回的是一个对象，如果在return中直接通过 ...storeStateFns 返回的是一个个的函数对象，不能直接使用，所以需要进行进一步的封装
      const storeStateFns = mapState(['counter', 'name', 'age', 'height'])
      const storeState = {}
      // Object.keys用于获取 storeStateFns 所有的key，再通过forEach遍历给 storeStateFns每一个key对应的返回的函数绑定store，
      Object.keys(storeStateFns).forEach(fnKey => {
        const fn = storeStateFns[fnKey].bind({$store: store});
        // 再通过computed获取每一个key对应的ref值保存到新的对象 storeState 中，此时 storeState 中都是computed转化后的值
        storeState[fnKey] = computed(fn)
      })
        
      return {
        sCounter,
        // 再通过拓展运算符的方式
        ...storeState
      }
    }
  }
</script>

<style scoped>

</style>
```

**Vuex并没有提供非常方便的使用mapState的方式，这里我们进行了一个函数的封装：**再创建一个hooks文件夹用于存放封装的函数，在其中创建一个useState.js的文件

```javascript
import { mapState, useStore } from "vuex";
import {computed} from 'vue'

export function useState(mapper) {
  // 获取store对象
  const store = useStore()

  // 获取到对应的对象的function：{name: function, age:function,...}
  const storeStateFns = mapState(mapper)

  // 对数据进行转换
  const storeState = {}
  Object.keys(storeStateFns).forEach(fnKey => {
    const fn = storeStateFns[fnKey].bind({ $store: store });
    storeState[fnKey] = computed(fn)
  })

  return storeState
}
```

**封装后使用：**

```javascript
<script>
// 引入useState
import {useState} from '../hooks/useState'
  export default {
    setup() {
      const storeState = useState(['counter', 'name', 'age', 'height'])
      
      return {
        ...storeState
      }
    }
  }
</script>
```



## 三、getters

### 1.基本使用

* 定义：

```javascript
getters: {
  totalPrice(state, getters) {
    let totalPrice = 0;
    for (const book of state.books) {
      totalPrice += book.count * book.price
    }
    return totalPrice * getters.currentDiscount
  },
}
```

* 使用：

```html
<div>
    <h2>{{ $store.getters.totalPrice}} </h2>
</div>
```

### 2.getters第二个参数

> 第二个参数用于获取**getters**中定义的其他函数。

```javascript
getters: {
    totalPrice(state, getters) {
        let totalPrice = 0;
        for (const book of state.books) {
            totalPrice += book.count * book.price;
        }
        return totalPrice + ',' + getters.myName;
    },
    myName(state) {
        return state.name
    }
}
```

### 3.getters的返回函数

> getters中的函数本身，可以**返回一个函数**，那么**在使用的地方相当于可以调用这个函数**.

* 定义：

```javascript
// 为了getter接受参数，可以return一个函数，此时传递参数
    totalPriceCountGreaterN(state, getters) {
      return function (n) {
        let totalPrice = 0;
        for (const book of state.books) {
          if (book.count <= n) continue
          totalPrice += book.count * book.price
        }
        return totalPrice * getters.currentDiscount
      }
    }
```

* 使用：这样相当于就可以传递参数了

```html
<h2>总价值：{{ $store.getters.totalPriceCountGreaterN(2) }}</h2>
```

### 4.mapGetters辅助函数

* 在options API中使用：

```javascript
computed: {
    // 数组类型
    ...mapGetters(["nameInfo", "ageInfo", "heightInfo"]),
    // 对象类型
    ...mapGetters({
      sNameInfo: "nameInfo",
      sAgeInfo: "ageInfo",
      sHeight: 'heightInfo'
    })
  },
```

* 在setup中使用：也是可以先进行一个封装，再只用

**封装：**

```javascript
import { mapGetters, useStore } from "vuex";
import {computed} from 'vue'

export function useGetters(mapper) {
  // 获取store对象
  const store = useStore()

  // 获取到对应的对象的function：{name: function, age:function,...}
  const storeStateFns = mapGetters(mapper)

  // 对数据进行转换
  const storeState = {}
  Object.keys(storeStateFns).forEach(fnKey => {
    const fn = storeStateFns[fnKey].bind({ $store: store });
    storeState[fnKey] = computed(fn)
  })

  return storeState
}
```

**使用：**

```vue
<template>
  <div>
    <h2>总价值：{{ $store.getters.totalPrice }}</h2>
    <h2>总价值：{{ $store.getters.totalPriceCountGreaterN(2) }}</h2>
    <hr />
    <h2>{{ $store.getters.nameInfo }}</h2>
    <h2>{{ ageInfo }}</h2>
    <h2>{{ heightInfo }}</h2>
    <hr />
    <h2>{{ sNameInfo }}</h2>
    <h2>{{ sAgeInfo }}</h2>
    <h2>{{ sHeightInfo }}</h2>
    <hr>
    <h2>{{ sNameInfoa }}</h2>
  </div>
</template>

<script>
import {useGetters} from '../hooks/useGetters'
export default {
  setup() {
    // const store = useStore();
    // const sNameInfoa = computed(() => store.getters.nameInfo)
    const storeGetters = useGetters(["nameInfo", "ageInfo", "heightInfo"])

    return {
      ...storeGetters
    }
  }
};
</script>

<style scoped>
</style>
```



## 四、mutations

> **只能**在**mutations**中进行对**state**状态的**修改**。

### 1.基本使用

* 定义：

```javascript
mutations: {
    increment(state) {
      state.counter++
    },
    decrement(state) {
      state.counter--
    },
    [INCREMENT_N](state, payload) {
      state.counter += payload.n
    }
  },
```

* 提交：

```html
<template>
  <div>
    <h2>当前计数：{{ $store.state.counter }}</h2>
    <button @click="$store.commit('increment')">+1</button>
    <button @click="$store.commit('decrement')">-1</button>
    <hr>
  </div>
</template>
```

### 2.mutations携带参数

> 第二个参数**payload**为携带的参数。

* 定义：

```javascript
mutations: {
    increment(state) {
      state.counter++
    },
    decrement(state) {
      state.counter--
    },
    [INCREMENT_N](state, payload) {
      state.counter += payload.n
    },
    addBannerData(state, payload) {
      state.banners = payload
    }
  }
```

* 提交：两种提交风格

```vue
<template>
  <div>
    <h2>当前计数：{{ $store.state.counter }}</h2>
    <button @click="$store.commit('increment')">+1</button>
    <button @click="$store.commit('decrement')">-1</button>
    <button @click="addTen">+10</button>
    <hr>
  </div>
</template>

<script>
import {INCREMENT_N} from '../store/mutation-types'
export default {
  methods: {
    addTen() {
      // this.$store.commit('incrementN', 10)
      // this.$store.commit('incrementN', {n: 10, name: 'yn'})
      // 另一种提交风格
      this.$store.commit({
        type: INCREMENT_N,
        n: 10,
        name: 'yn',
        age: 18
      })
    }
  }
};
</script>

<style scoped>
</style>
```

### 3.mutations常量类型

* 定义常量：mutation-type.js

`export const ADD_NUMBER = 'add_number'`

* 定义mutations

```javascript
[INCREMENT_N](state, payload) {
   state.counter += payload.n
}
```

* 提交

```javascript
$store.commit({
    type: ADD_NUMBER,
    count: 100
})
```

### 4.mapMutations辅助函数

* 在option API中使用：

```javascript
methods: {
    ...mapMutations(['increment', 'decrement', INCREMENT_N]),
    addTen() {
      this.increment_n({n:10})
    }
}
```

* 在setup中使用：由于mutation本身就是函数，所以可以直接解构

```javascript
setup() {
    const stateMutations = mapMutations(['increment', 'decrement', INCREMENT_N])

    return {
      ...stateMutations
    }
}
```

### 5.mutation重要原则

* 一条重要的原则就是要记住 mutation 必须是**同步函数**
* * 这是因为devtool工具会记录mutation的日记；
  * 每一条mutation被记录，devtools都需要捕捉到前一状态和后一状态的快照；
  * 但是**在mutation中执行异步操作，就无法追踪到数据的变化**；
  * 所以Vuex的重要原则中要求 mutation必须是同步函数；



## 五、actions

> Action类似于mutation，不同在于： **Action提交的是mutation**，而不是直接变更状态； Action可以包含任意异步操作；

### 1.基本使用

* **参数context**： context是一个和**store**实例均有相同方法和属性的context对象； 可以从其中获取到**commit**方法来提交一个**mutation**，或者通过 **context.state** 和 **context.getters** 来 获取 state 和 getters；

```javascript
incrementAction(context) {
   setTimeout(() => {
     context.commit("increment")
   }, 1000)
}
```

* 进行action的分发使用的是 store 上的**dispatch函数**；

* 携带参数

```javascript
increment() {
      // this.$store.dispatch('incrementAction', {count: 100})
   // 另外一种提交方式
   this.$store.dispatch({
     type: 'incrementAction',
     count: 100
   })
},
```

### 2.mapActions辅助函数

```vue
<template>
  <div>
    <h2>当前计数：{{ $store.state.counter }}</h2>
    <button @click="incrementAction">+1</button>
    <button @click="decrementAction">-1</button>
    <hr>
  </div>
</template>

<script>
import {mapActions} from 'vuex'
export default {
  methods: {
    // 数组写法
    ...mapActions(['incrementAction', 'decrementAction']),
    // 对象写法
    ...mapActions({
      add: 'incrementAction',
      sub: 'decrementAction'
    })
  },
  setup() {
    const actions = mapActions(['incrementAction', 'decrementAction'])
    const actions2 = mapActions({
      add: 'incrementAction',
      sub: 'decrementAction'
    })
    return {
      ...actions,
      ...actions2
    }
  }
};
</script>

<style scoped>
</style>
```

### 3.actions异步操作

> Action 通常是异步的，那么如何知道 action 什么时候结束呢？我们可以通过让action返回Promise，在Promise的then中来处理完成后的操作；

```javascript
actions: {
    // 异步请求
    getHomeMultidata(context) {
      return new Promise((resolve, reject) => {
        axios.get("http://123.207.32.32:8000/home/multidata").then(res => {
          context.commit("addBannerData", res.data.data.banner.list)
          resolve(res)
        }).catch(err => {
          reject(err)
        })
      })
    }
}
```

```javascript
setup() {
    const store = useStore()

    onMounted(() => {
      const promise = store.dispatch("getHomeMultidata")
      promise.then(res => {
        console.log(res);
      }).catch(err => {
        console.log(err);
      })

    })
    return {
    }
  }
```



## 六、modules

> 由于使用单一状态树，应用的所有状态会集中到一个比较大的对象，当应用变得非常复杂时，store对象就有可能变得相当臃肿；为了解决以上问题，Vuex 允许我们将 store 分割成模块（module）；每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块

### 1.基本使用

> 一般会在**store文件夹**下再创建一个**modules文件夹**用于存放子模块，这里我们在modules文件夹下创建**home.js**文件。

**store中index.js：**

```javascript
import { createStore } from "vuex"
import home from "./modules/home";
import user from "./modules/user";

const store = createStore({
  state() {
    return {
      rootCounter: 0
    }
  },
  mutations: {
    increment(state) {
      state.rootCounter++
    }
  },
  modules: {
    home,
    user
  }
});

export default store
```

**home.js：**

```javascript
const homeModule = {
  namespaced: true,
  state() {
    return {
      homeCounter: 100
    }
  },
  getters: {
  },
  mutations: {
  },
  actions: {
  }
}

export default homeModule
```

**使用：**

```html
<template>
  <div>
    <h2>{{ $store.state.rootCounter }}</h2>
    <h2>{{ $store.state.home.homeCounter }}</h2>
    <h2>{{ $store.state.user.userCounter }}</h2>
    <hr>
  </div>
</template>
```

### 2.modules的局部状态

> 对于模块内部的 mutation 和 getter，接收的第一个参数(**state**)是模块的**局部状态对象**，不是根模块中的状态对象。所以他们会有额外的参数**rootState, rootGetters**用于获取根模块中的状态。

### 3.modules的命名空间

> 默认情况下，**模块内部**的action和mutation仍然是注册在**全局**的命名空间中的： 这样使得多个模块能够对同一个 action 或 mutation 作出响应； Getter 同样也默认注册在全局命名空间；
>
> 如果我们希望模块具有更高的封装度和复用性，可以添加 **namespaced: true** 的方式使其成为带命名空间的模块：当模块被注册后，它的所有 getter、action 及 mutation 都会自动根据模块注册的路径调整命名；

**home.js：**

```javascript
const homeModule = {
  namespaced: true,
  state() {
    return {
      homeCounter: 100
    }
  },
  getters: {
    doubleHomeCounter(state) {
      // doubleHomeCounter(state, getters, rootState, rootGetters) {
      return state.homeCounter * 2
    }
  },
  mutations: {
      increment(state) {
        state.homeCounter++
      }
  },
  actions: {
    incrementAction({context}) {
      // incrementAction({context, dispatch, state, rootState, getters, rootGetters}) {
      context.commit("increment")
    }
  }
}

export default homeModule
```

**使用：**

```vue
<template>
  <div>
    <h2>{{ $store.state.rootCounter }}</h2>
    <h2>{{ $store.state.home.homeCounter }}</h2>
    <h2>{{ $store.state.user.userCounter }}</h2>
    <hr>
    <h2>{{ $store.getters["home/doubleHomeCounter"] }}</h2>

    <button @click="homeIncrement">home+1</button>
    <button @click="homeIncrementAction">home+1</button>
    <hr>
  </div>
</template>

<script>
export default {
  methods: {
    homeIncrement() {
      this.$store.commit("home/increment")
    },
    homeIncrementAction() {
      this.$store.dispatch("home/incrementAction")
    }
  }
};
</script>

<style scoped>
</style>
```

### 4.modules修改或派发根组件

**如果我们希望在action中修改root中的state，那么有如下的方式：**

```javascript
actions: {
    incrementAction({context}) {
      // incrementAction({context, dispatch, state, rootState, getters, rootGetters}) {
      context.commit("increment")
      // context.commit("increment", null, {root: true}) // 表示此次的提交是对根进行的提交
      // dispatch("increment", null, {root: true})
    }
}
```

### 5.modules的辅助函数

**如果辅助函数有三种使用方法：**

* 方式一：通过**完整的模块空间名称**来查找；
* 方式二：第一个参数传入模块空间名称，后面写上要使用的属性；
* 方式三：通过 **createNamespacedHelpers** 生成一个模块的辅助函数；

```vue
<template>
  <div>
    <h2>{{ homeCounter }}</h2>
    <h2>{{ doubleHomeCounter }}</h2>
    <button @click="increment">home+1</button>
    <button @click="incrementAction">home+1</button>
    <hr>
  </div>
</template>

<script>
// import {mapState, mapGetters, mapMutations, mapActions, createNamespacedHelpers} from 'vuex'
import {createNamespacedHelpers} from 'vuex'
// const hyMapState = createNamespacedHelpers('home').mapState
const {mapState, mapGetters, mapMutations, mapActions} = createNamespacedHelpers('home')
export default {
  computed: {
    // 1.写法一：
    // ...mapState({
    //   homeCounter: state => state.home.homeCounter
    // }),
    // ...mapGetters({
    //   doubleHomeCounter: 'home/doubleHomeCounter'
    // }),

    // 写法二：
    // ...mapState('home', ["homeCounter"]),
    // ...mapGetters('home', ['doubleHomeCounter'])

    // 写法三：
    ...mapState(["homeCounter"]),
    ...mapGetters(['doubleHomeCounter'])
  },
  methods: {
    // 写法一：
    // ...mapMutations({
    //   increment: 'home/increment'
    // }),
    // ...mapActions({
    //   incrementAction: 'home/incrementAction'
    // })

    // 写法二：
    // ...mapMutations('home', ['increment']),
    // ...mapActions('home', ['incrementAction'])

    // 写法三：
    ...mapMutations(['increment']),
    ...mapActions(['incrementAction'])
  },
  setup() {
    

    return {
      // 02:08:53
    }
  }
};
</script>

<style scoped>
</style>
```

