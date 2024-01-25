### 需求

> 需求：在做项目时，遇到了需要制作地址列表的功能，这一般都会用到一些开源的组件库，但是有个问题是不同组件库之间的城市列表**数据结构不一样**，虽然可以找到很多的城市列表的数据，但是都不一定是我们想要的，所以最好就是**对已有数据结构进行转换**，转换成我们需要的结构然后单独放在一个文件中(毕竟城市列表数据也比较多)。



### 1.首先寻找类似需求的数据

[比如这种)](https://github.com/misitesun/index.list.js/blob/main/index.list.js)：

```json
list: [
    {
      letter: "A",
      data: [
        {
          name: "阿巴嘎旗",
          city_pinyin: "abagaqi",
          city_id: 152522,
          py: "abgq",
        },
        {
          name: "阿坝县",
          city_pinyin: "abaxian",
          city_id: 513231,
          py: "abx",
        },
        ......
      ],
    },
    {
      letter: "B",
      data: [
        {
          name: "八步区",
          city_pinyin: "babuqu",
          city_id: 451102,
          py: "bbq",
        },
        {
          name: "巴楚县",
          city_pinyin: "bachuxian",
          city_id: 653130,
          py: "bcx",
        },
        ......
      ],
    },
    ......
  ]
```

**但是我们需要的是这种结构的数据：**

```json
{
  "A": [
    { "areaId": 152522, "areaName": "阿巴嘎旗" },
    { "areaId": 513231, "areaName": "阿坝县" },
    .....
  ],
  "B": [
    { "areaId": 451102, "areaName": "八步区" },
    { "areaId": 653130, "areaName": "巴楚县" },
    ......
  ],
  ......
}
```



### 2.对数据进行转换

> 具体需要什么样的数据格式看你的需求。

```js
let cityTransList = {};
// list为上面所说的类似数据
list.map((item) => {
  let value = [];
  item.data.map((item) => {
    let oneCity = {};
    oneCity.areaId = item.city_id;
    oneCity.areaName = item.name;
    value.push(oneCity);
  });
  cityTransList[item.letter] = value;
});
```



### 3.将转换后的数据转为json文件

```js
function exportJson(name, data) {
  let blob = new Blob([data]);
  let link = document.createElement("a");
  link.href = URL.createObjectURL(blob);
  link.download = name; //  下载的文件名
  link.click();
}

exportJson("cityList.json", JSON.stringify(cityTransList));
```



### 4.完整代码

> 以下代码直接引入html中。

```js
// 准备数据
const similarData = [...]

// 转换数据
let cityTransList = {};
list.map((item) => {
  let value = [];
  item.data.map((item) => {
    let oneCity = {};
    oneCity.areaId = item.city_id;
    oneCity.areaName = item.name;
    value.push(oneCity);
  });
  cityTransList[item.letter] = value;
});

// 另存为文件
function exportJson(name, data) {
  let blob = new Blob([data]);
  let link = document.createElement("a");
  link.href = URL.createObjectURL(blob);
  link.download = name; //  下载的文件名
  link.click();
}

exportJson("cityList.json", JSON.stringify(cityTransList));
```



