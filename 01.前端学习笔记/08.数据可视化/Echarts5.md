

# 广州弘源科教-数据可视化-ECharts5



## 1.ECharts 初体验

>  div容器必须要有高度，宽度可选

```html

    <div id="main" style="height: 400px"></div>


    <script src="../libs/echarts-5.3.3.js"></script>


    <script>
      // 1.基于准备好的dom，初始化echarts实例
      var myChart = echarts.init(document.getElementById("main"));
        
      // 2.指定图表的配置项和数据
      var option = {
        title: {
          text: "ECharts 入门示例",
        },
        tooltip: {},
        legend: {
          data: ["销量"],
        },
        xAxis: {
          data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"],
        },
        yAxis: {},
        series: [
          {
            name: "销量",
            type: "bar",
            data: [5, 20, 36, 10, 10, 20],
          },
        ],
      };
        
      // 3.使用刚指定的配置项和数据显示图表。
      myChart.setOption(option);
    </script>
```

最精简 配置版

```js

      var option = {
        xAxis: {
          data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"],
        },
          
        yAxis: {},
          
        series: [
          {
            name: "销量",
            type: "bar",
            data: [5, 20, 36, 10, 10, 20],
          },
        ],
      };
```



## 2.切换渲染引擎 和 主题色

```js
echarts.init(document.getElementById("main"), null, {renderer: "svg"});

echarts.init(document.getElementById("main"), "dark", {renderer: "svg"});
```



## 3.配置项（组件）

### 1.Grid 组件

```json
       backgroundColor: "rgba(255, 0, 0, 0.1)", 

       grid: {
          show: true,
          backgroundColor: "rgba(255, 0, 0, 0.1)",
          left: 0,
          right: 0,
          top:0,
          bottom:0,  
          containLabel: true, // grid 区域是否包含坐标轴的刻度标签
        }
```



### 2.x，y坐标系 组件

```json
        xAxis: {
            
          show: true,
          name: "类目坐标",
          type: "category", // 类目坐标才有data选项  
          data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"],

          axisLine: { // 坐标轴轴线相关设置。
            show: true,
            lineStyle: {
              color: "red",
              width: 3,
            },
          },

          axisLabel: { // 坐标轴刻度标签的相关设置。
            show: true,
            color: "green",
            fontSize: 16,
          },
          
          axisTick: {  // 坐标轴刻度相关设置。
            show: true,
            length: 10,
            lineStyle: {
              color: "blue",
              width: 3,
            },
          },
            
          splitLine: { // 坐标轴在 grid 区域中的分隔线。
            show: true,
            lineStyle: {
              color: "orange",
              width: 1,
            },
          }, 
            
            
        },
```



### 3.series 系列

#### 1.data 支持的编写方式

```json
        series: [
          {
            name: "产品销量柱形图",
            type: "bar",
            label: {
              show: true,
            },
            
            // 方式一
            // data: [5, 20, 36, 10, 10, 20],
              
              
            // 方式二
            // data: [
            //   [0, 5],
            //   [1, 20],
            //   [2, 36],
            //   [3, 10],
            //   [4, 10],
            //   [5, 20],
            // ],
                     
              
            // 方式三(推荐)
            data: [
              {
                value: 5,
                name: "衬衫", // 数据项名称, 比如pie系列 tooltip 需要用到
              },
              {
                value: 20,
                name: "羊毛衫",
              },
              {
                value: 36,
                name: "雪纺衫",
              },
              {
                value: 10,
                name: "裤子",
              },
              {
                value: 10,
                name: "高跟鞋",
              },
              {
                value: 20,
                name: "袜子",
              },
            ],
                      
              
            // 方式四
            // data: [
            //   {
            //     value: [0, 5], // 数组第一项为x轴值，第二项为y轴值
            //     name: "衬衫", // 数据项名称, 比如pie系列 tooltip 需要用到
            //   },
            //   {
            //     value: [1, 20],
            //     name: "羊毛衫",
            //   },
            //   {
            //     value: [2, 36],
            //     name: "雪纺衫",
            //   },
            //   {
            //     value: [3, 10],
            //     name: "裤子",
            //   },
            //   {
            //     value: [4, 10],
            //     name: "高跟鞋",
            //   },
            //   {
            //     value: [5, 20],
            //     name: "袜子",
            //   },
            // ],
              
                   
            // 方式五(地理坐标系推荐)
   			// data: [
            //   {
            //     value: [0, 5, 500], // 第一项为x轴或纬度值，第二项为y或维度轴值，第三项以后为扩展值
            //     name: "衬衫", // 数据项名称, 比如pie系列 tooltip 需要用到
            //   },
            //   {
            //     value: [1, 20, 400],
            //     name: "羊毛衫",
            //   },
            //   {
            //     value: [2, 36, 200],
            //     name: "雪纺衫",
            //   },
            //   {
            //     value: [3, 10, 100],
            //     name: "裤子",
            //   },
            //   {
            //     value: [4, 10, 600],
            //     name: "高跟鞋",
            //   },
            //   {
            //     value: [5, 20, 300],
            //     name: "袜子",
            //   },
            // ],
              
              

          },
        ],
```



#### 2.type 图表类型(bar、pie)

折线图 和 条型图

```json
series: [
          {
            name: "产品销量柱形图",
            type: "line", // line  bar scatter   pie
            data: [5, 20, 36, 10, 10, 20], 
          },
],
```



饼图

```json
series: [
          {
            name: "产品销量柱形图",
            type: "pie",

			// 设置成百分比时第一项是相对于容器宽度，第二项是相对于容器高度。
            center: ["50%", "50%"], // 饼图的中心（圆心）坐标，数组的第一项是横坐标，第二项是纵坐标。
            
            // 百分比是参照容器高宽中较小一项( 感觉是直径 )
            radius: ["20%", "85%"], // 饼图的半径。数组的第一项是内半径，第二项是外半径。
            roseType: "area", //area玫瑰图(南丁格尔图)。 圆心角一样，通过半径展现数据大小(默认false)

            data: [
              {
                value: 5,
                name: "衬衫", // 数据项名称, 比如pie系列 tooltip 需要用到
              },
              {
                value: 20,
                name: "羊毛衫",
              },
              {
                value: 36,
                name: "雪纺衫",
              },
              {
                value: 10,
                name: "裤子",
              },
              {
                value: 10,
                name: "高跟鞋",
              },
              {
                value: 20,
                name: "袜子",
              },
            ],
              
              
              
          },
        ],
```



#### 3.label( 优先级 )

```json
        series: [
          {
            name: "产品销量柱形图",
            type: "bar",
              
            label: { // 系列图形上的文本标签
              show: true,
              position: [10, 10], // 支持的类型可以查文档，不同type的position的值会有些差异
              color: "white",
              fontSize: "20px",
            },
              
            data: [
              {
                value: 5,
                // 优先级别更高
                 label: {
                   show: false,
                 },
              },
                
              ....
            ],
          },
        ],
```



#### 4.itemStyle 图形默认色

```json
        series: [
          {
            name: "产品销量柱形图",
            type: "bar",
              
            itemStyle: { // 系列图形的样式
              color: "red",
              // borderColor: "orange",
              // borderWidth: 4,
              // opacity: 0.4,
            },
              
            data: [
              {
                value: 5,
                // 优先级别更高
                itemStyle: {
                  color: "green",
                },
              },
              ....
            ],
              
          },
        ],
```



#### 5.emphasis 高亮色

鼠标悬浮到图形元素上时，高亮的样式。

```json
        series: [
          {
            name: "产品销量柱形图",
            type: "bar",
              
            emphasis: { // 图形高亮( label、labelLine、itemStyle、lineStyle、areaStyle... )
              label: {
                // show: false,
                color: "gold",
              },
            },
              
            data: [
              {
                value: 5,
                // 优先级别更高
                emphasis: {
                  label: {
                    // show: false,
                    color: "green",
                  },
                },
              },
              ....
            ],
          },
        ],
```

### 4.title 组件

```json
   title: {
      text: "Echart 5.x 条形图",
      left: 20,
      top: 10,
   },
```




### 5.legend 图例组件

pie

```json
        legend: {
          show: true,
          // width: 50, // 图例组件的宽度。默认自适应
          itemWidth: 20, // 图例标记的图形宽度。
          // icon: "circle",
          // top: 10,
          // bottom: 0,
            

          // formatter: "liu-{name}",  // 用来格式化图例标记文本，支持字符串模板和回调函数两种形式。
          formatter: function (name) {
            return name + "  {countSty|40%}"; // 富文本语法：{style_name|value} 不能有空格
          },

          textStyle: {
              
              
            color: "red",
            rich: { // 在 rich 里面，可以自定义富文本样式。
              countSty: {
                color: "red",
              },
            },
          },
            
            
        },
```






### 6.tooltip 组件

```json
        tooltip: {
          show: true,
          
          // 使用了 trigger ，一般也结合 axisPointer
          trigger: "axis",  // 默认是 item
          
          axisPointer: {
            type: "line", //  (默认是竖线 line)  (横线 + 竖线 cross)  (横线 + 竖线 shadow)
          },
          
        },
```



### 7.Color的渐变色

对象配置方式（ 推荐 ）

```json
              color: {
                // 渐变
                type: "linear",
                x: 0,
                y: 0,
                x2: 0,
                y2: 1,
                colorStops: [
                  {
                    offset: 0,
                    color: "red",
                  },
                  {
                    offset: 1,
                    color: "blue",
                  },
                ],
              },
```

调用 API 生成

```json
 			color: new echarts.graphic.LinearGradient(
                0,
                0,
                0,
                1,
                [
                  {
                    offset: 0,
                    color: "#20FF89",
                  },
                  {
                    offset: 1,
                    color: "rgba(255, 255, 255, 0)",
                  },
                ],
                false
              ),
```



## 4.图表实战

### 1.柱形图

```json
var option = {
        backgroundColor: "rbg(40,46,72)",
        grid: {
          left: "5%",
          right: "6%",
          top: "30%",
          bottom: "5%",
          containLabel: true, // grid 区域是否包含坐标轴的刻度标签
        },
        tooltip: {},
        xAxis: {
          name: "月份",
          axisLine: {
            show: true,
            lineStyle: {
              color: "#42A4FF",
            },
          },
          axisTick: {
            show: false,
          },
          axisLabel: {
            color: "white",
          },

          data: ["一月", "二月", "三月", "四月", "五月", "六月", "七月"],
        },
        yAxis: {
          name: "个",
          nameTextStyle: {
            color: "white",
            fontSize: 13,
          },
          axisLine: {
            show: true,
            lineStyle: {
              color: "#42A4FF",
            },
          },
          axisTick: {
            show: false,
          },
          splitLine: {
            show: true,
            lineStyle: {
              color: "#42A4FF",
            },
          },
          axisLabel: {
            color: "white",
          },
        },
        series: [
          {
            name: "销量",
            type: "bar",
            barWidth: 17,
            itemStyle: {
              color: {
                type: "linear",
                x: 0,
                y: 0,
                x2: 0,
                y2: 1,
                colorStops: [
                  {
                    offset: 0,
                    color: "#01B1FF", // 0% 处的颜色
                  },
                  {
                    offset: 1,
                    color: "#033BFF", // 100% 处的颜色
                  },
                ],
                global: false, // 缺省为 false
              },
            },
            data: [500, 2000, 3600, 1000, 1000, 2000, 4000],
          },
        ],
      };
      
```



### 2.折线图

```json
 var option = {
        backgroundColor: "rbg(40,46,72)",
        grid: {
          left: "5%",
          right: "1%",
          top: "20%",
          bottom: "15%",
          containLabel: true, // grid 区域是否包含坐标轴的刻度标签
        },
        legend: {
          bottom: "5%",
          itemGap: 20,
          itemWidth: 13,
          itemHeigth: 12,
          textStyle: {
            color: "#64BCFF",
          },
          icon: "rect",
        },
        tooltip: {
          trigger: "axis",
          axisPointer: {
            type: "line",
            lineStyle: {
              color: "#20FF89",
            },
          },
        },
        xAxis: [
          {
            type: "category",
            axisLine: {
              show: false,
            },
            axisLabel: {
              color: "#64BCFF",
            },
            splitLine: {
              show: false,
            },
            axisTick: {
              show: false,
            },
            data: [
              "1月",
              "2月",
              "3月",
              "4月",
              "5月",
              "6月",
              "7月",
              "8月",
              "9月",
              "10月",
              "11月",
              "12月",
            ],
          },
        ],
        yAxis: [
          {
            type: "value",
            splitLine: {
              show: false,
            },
            axisLine: {
              show: false,
            },
            axisLabel: {
              show: true,
              color: "#64BCFF",
            },
          },
        ],
        series: [
          {
            name: "正常",
            type: "line",
            smooth: true,  // 是否平滑曲线显示。
            symbolSize: 5, // 标记的大小
            showSymbol: false,
            itemStyle: {
              color: "#20FF89",
            },
            // 区域填充样式。设置后显示成区域面积图。
            areaStyle: {
              color: new echarts.graphic.LinearGradient(
                0,
                0,
                0,
                1,
                [
                  {
                    offset: 0,
                    color: "#20FF89",
                  },
                  {
                    offset: 1,
                    color: "rgba(255, 255, 255, 0)",
                  },
                ],
                false
              ),
            },
            data: [200, 200, 191, 234, 290, 330, 310, 201, 154, 190, 330, 410],
          },
          {
            name: "异常",
            type: "line",
            smooth: true, // 是否平滑曲线显示。
            symbolSize: 5, // 标记的大小，可以设置成诸如 10 这样单一的数字
            showSymbol: false, // 是否显示 symbol, 如果 false 则只有在 tooltip hover 的时候显示。
            itemStyle: {
              // 折线的颜色
              color: "#EA9502",
            },
            // 折线区域的颜色
            areaStyle: {
              color: {
                type: "linear",
                x: 0,
                y: 0,
                x2: 0,
                y2: 1,
                colorStops: [
                  {
                    offset: 0,
                    color: "#EA9502",
                  },
                  {
                    offset: 1,
                    color: "rgba(255, 255, 255, 0)",
                  },
                ],
              },
            },
            data: [500, 300, 202, 258, 280, 660, 320, 202, 308, 280, 660, 420],
          },
        ],
      }; 
      
```



### 3.饼图

```json
     // =====准备数据=====
      let pieDatas = [
        {
          value: 100,
          name: "广州占比",
          percentage: "5%",
          color: "#34D160",
        },
        {
          value: 200,
          name: "深圳占比",
          percentage: "4%",
          color: "#027FF2",
        },
        {
          value: 300,
          name: "东莞占比",
          percentage: "8%",
          color: "#8A00E1",
        },
        {
          value: 400,
          name: "佛山占比",
          percentage: "10%",
          color: "#F19610",
        },
        {
          value: 500,
          name: "中山占比",
          percentage: "20%",
          color: "#6054FF",
        },
        {
          value: 600,
          name: "珠海占比",
          percentage: "40%",
          color: "#00C6FF",
        },
      ];

      // 将 pieDatas 格式的 数据映射为 系列图所需要的数据格式
      var data = pieDatas.map((item) => {
        return {
          value: item.value,
          name: item.name,
          itemStyle: {
            color: item.color, 
          },
        };
      });

      // 求出总数
      let total = pieDatas.reduce((a, b) => {
        return a + b.value * 1;
      }, 0);
      // =====准备数据=====

      // 2.指定图表的配置项和数据
      var option = {
        backgroundColor: "rbg(40,46,72)",
        title: {
          text: `充电桩总数`,
          top: "50%",
          left: "50%",
          padding: [-20, 0, 0, -45],
          textStyle: {
            fontSize: 19,
            color: "white",
          },

          // 副标题使用-富文本语法：{style_name|value}， 注意不能有空格
          subtext: `{totalSty|${total}}`,
          subtextStyle: {
            rich: {
              totalSty: {
                fontSize: 19,
                color: "white",
                width: 90,
                align: "center",
              },
            },
          },
        },
        legend: {
          orient: "vertical",
          right: "10%",
          top: "18%",
          itemGap: 20,
          itemWidth: 16,
          itemHeigth: 16,
          icon: "rect",
          // 自定义图例的名称
          formatter: function (name) {
            // 图例文本格式化 + 富文本定制样式  
            var currentItem = pieDatas.find((item) => item.name === name);
            return (
              "{nameSty|" +
              currentItem.name +
              "}\n" +
              "{numberSty|" +
              currentItem.value +
              "个 }" +
              "{preSty|" +
              currentItem.percentage +
              "}"
            );
          },
          textStyle: {
            rich: {
              nameSty: {
                fontSize: 12,
                color: "#FFFFFF",
                padding: [10, 14],
              },
              numberSty: {
                fontSize: 12,
                color: "#40E6ff",
                padding: [0, 0, 0, 14],
              },
              preSty: {
                fontSize: 12,
                color: "#40E6ff",
              },
            },
          },
        },
        series: [
          {
            type: "pie",
            center: ["50%", "50%"], // 饼图的中心（圆心）坐标，数组的第一项是横坐标，第二项是纵坐标。
            radius: ["30%", "75%"], // 饼图的半径。数组的第一项是内半径，第二项是外半径。
            label: {
              show: false,
            },
            // data: [  { name: '',   value: '',   itemStyle }  ],
            data: data,
            roseType: "area", //  area 玫瑰图, 圆心角一样，通过半径展现数据大小( 默认为false )
          },
        ],
      };
      
```



### 4.地图

#### 1.geo 地理坐标系组件

1.引入 geo_json

2.注册需要的地图 GeoJSON （在调 setOption 之前注册即可）

3.配置显示地图

```js
    <!-- 1.引入geo_json -->
    <script src="../libs/echarts-5.3.3.js"></script>
    <script src="./geojson/china_json.js"></script>
    <script src="./geojson/gd_geojson.js"></script>
	
    <!-- 南昌这个不需要注册了，因为该文件已经自动注册了 -->
    <script src="./geojson/南昌.js"></script>
    
    <script>
      // 2.注册地图
      echarts.registerMap("中国", { geoJSON: china_json });
      echarts.registerMap("gd", { geoJSON: gd_geojson });

      var myChart = echarts.init(document.getElementById("main"), null, {
        renderer: "svg",
      });

      var option = {
        backgroundColor: "rgba(40,46,72, 0.2)",
        grid: {
          show: true,
          backgroundColor: "rgba(0, 0, 255, 0.2)",
        },
        // 4.配置地图
        // 全局的地理坐标系组件。地理坐标系组件用于地图的绘制，支持在地理坐标系上绘制散点图，线集。
        // geo 支持数组和对象，数组可创建多个地理坐标系 
          geo: [
            {
              map: "南昌", // 中国 、gd、南昌
            },
          ]
        // series: [],
      };
      myChart.setOption(option);
    </script>
```



#### 2.map series

1.引入 geo_json

2.注册需要的地图 GeoJSON （支持注册多个，也需要引入多个）

3.配置显示地图

```js

    <script src="../libs/echarts-5.3.3.js"></script>
    <script src="./geojson/china_json.js"></script>
    <script>
      echarts.registerMap("中国", { geoJSON: china_json });
      var myChart = echarts.init(document.getElementById("main"), null, {
        renderer: "svg",
      });
      var option = {
        // 系列地图
        series: [
          {
            type: "map",
            map: "中国",
          },
        ],
      };
      myChart.setOption(option);
    </script>
```



#### 3.itemStyle着色

areaColor  

borderColor

```json
      var option = {
        geo: {
          map: "中国", // 中国 、gd、南昌
          roam: false, // 是否开启鼠标缩放和平移漫游。默认不开启。
          label: {
            // 图形上的文本标签，可用于说明图形的一些数据信息，比如值，名称等。
            show: false,
          },
          aspectScale: 0.75, // 这个参数用于 scale 地图的长宽比，如果设置了projection则无效。

          // =======地图着色=========
          itemStyle: {
            areaColor: "#023677", // 地图区域的颜色。
            borderColor: "#1180c7", // 图形的描边颜色。
          },
            
          emphasis: {
            itemStyle: {
              areaColor: "#4499d0",
            },
            label: {
              color: "white",
            },
          },
          // =======地图着色=========
        },
        series: [],
      };
```



#### 4.map data

```json
    var data = [
        { name: "北京", value: 199 },
        { name: "天津", value: 42 },
        { name: "河北", value: 102 },
        { name: "山西", value: 81 },
        { name: "内蒙古", value: 47 },
        { name: "辽宁", value: 67 },
        { name: "吉林", value: 82 },
        { name: "黑龙江", value: 123 },
        { name: "上海", value: 24 },
        { name: "江苏", value: 92 },
        { name: "浙江", value: 114 },
        { name: "安徽", value: 109 },
        { name: "福建", value: 116 },
        { name: "江西", value: 91 },
        { name: "山东", value: 119 },
        { name: "河南", value: 137 },
        { name: "湖北", value: 116 },
        { name: "湖南", value: 114 },
        { name: "重庆", value: 91 },
        { name: "四川", value: 125 },
        { name: "贵州", value: 62 },
        { name: "云南", value: 83 },
        { name: "西藏", value: 9 },
        { name: "陕西", value: 80 },
        { name: "甘肃", value: 56 },
        { name: "青海", value: 10 },
        { name: "宁夏", value: 18 },
        { name: "新疆", value: 180 },
        { name: "广东", value: 123 },
        { name: "广西", value: 59 },
        { name: "海南", value: 14 },
      ];


        series: [
          {
            name: "中国地图",
            type: "map",
            map: "中国",

            // =====地图着色======
            itemStyle: {
              areaColor: "#023677",
              borderColor: "#1180c7",
            },
            emphasis: {
              itemStyle: { areaColor: "#4499d0" },
              label: { color: "white" },
            },
            select: {
              label: { color: "white" },
              itemStyle: { areaColor: "#4499d0" },
            },
            // =====地图着色======
            
              
            // ===== 添加数据(不需要地理坐标点，直接使用name) =====
            // name: 数据所对应的地图区域的名称，例如 '广东'，'浙江'。  
            // value: 该区域的数据值。。  
            // data: [ {name:'' ,  value: '' }, .... ]  
            data
          },
        ],
        
```



#### 5.visualmap

seriesIndex: [0]

inRange 指定选中范围的视觉元素样式

```json
      var option = {
          
        // 1.视觉数据映射
        visualMap: [
          {
            // type: "continuous", // 连续型视觉映射组件 (默认)
            // type: "piecewise", // 分段型视觉映射组件
            left: "20%",
            seriesIndex: [0], // 指定取哪个系列的数据
            // 定义 在选中范围中 的视觉元素, 对象类型。
            inRange: {
              color: ["#04387b", "#467bc0"], // 映射组件和地图的颜色(一般和地图色相近)
            },
          },
        ],
          
          
       }
```



### 5.散点图

#### 1.地图上散点图的基本用法

1.配置地理坐标系组件（ 在 geo 配置）

2.散点图系列

3.散点图复用地图坐标系组件 (  geoIndex  )

```json
var option = {
        backgroundColor: "rgba(40,46,72, 0.2)",
        grid: {
          show: true,
          backgroundColor: "rgba(0, 0, 255, 0.2)",
        },
        // 4.配置地图
        geo: {
          map: "中国",
        },
    
        series: [
          {
            name: "散点图",
              
            type: "effectScatter",
            geoIndex: 0, // geo 支持数组，默认是 0
            coordinateSystem: "geo", // 使用地理坐标系，通过 geoIndex 指定相应的地理坐标系组件。
              
              
            data: [
              {
                name: "广东",
                value: [113.280637, 23.125178, 193],
              },
              {
                name: "北京",
                value: [116.405285, 39.904989, 199],
              },
            ],
              
           // ====== 散点大小和着色========   
            symbolSize: function (val) {
              return val[2] / 10;
            },
            itemStyle: {
              color: "yellow",
              shadowBlur: 10,
              shadowColor: "yellow",
            },
           // ====== 散点大小和着色========    
              
          },
        ],
      };
```



#### 2.地图散点图+地图的数据

```json

      var data = [
        { name: "北京", value: 199 },
        { name: "天津", value: 42 },
        { name: "河北", value: 102 },
        { name: "山西", value: 81 },
        { name: "内蒙古", value: 47 },
        { name: "辽宁", value: 67 },
        { name: "吉林", value: 82 },
        { name: "黑龙江", value: 123 },
        { name: "上海", value: 154 },
        { name: "江苏", value: 102 },
        { name: "浙江", value: 114 },
        { name: "安徽", value: 109 },
        { name: "福建", value: 116 },
        { name: "江西", value: 91 },
        { name: "山东", value: 119 },
        { name: "河南", value: 137 },
        { name: "湖北", value: 116 },
        { name: "湖南", value: 114 },
        { name: "重庆", value: 101 },
        { name: "四川", value: 125 },
        { name: "贵州", value: 62 },
        { name: "云南", value: 83 },
        { name: "西藏", value: 9 },
        { name: "陕西", value: 80 },
        { name: "甘肃", value: 56 },
        { name: "青海", value: 10 },
        { name: "宁夏", value: 18 },
        { name: "新疆", value: 120 },
        { name: "广东", value: 193 },
        { name: "广西", value: 59 },
        { name: "海南", value: 14 },
      ];



      var option = {
        tooltip: {}, // 提示框组件
          
        // 1.地理坐标系
        geo: {
          map: "中国",
        },
          
        series: [

          // 3.地图上的数据  
          {
            name: "中国地图",
            type: "map",
            map: "中国",
            data,
            itemStyle: {
              areaColor: "#023677",
              borderColor: "#1180c7",
            },
            emphasis: {
              itemStyle: { areaColor: "#4499d0" },
              label: { color: "white" },
            },
            select: {
              label: { color: "white" },
              itemStyle: { areaColor: "#4499d0" },
            },
          },

          // 2.散点图，复用地理坐标系
          {
            name: "散点图充电桩",
            type: "effectScatter",
            geoIndex: 0, // geo 支持数组
            coordinateSystem: "geo", // 使用地理坐标系，通过 geoIndex 指定相应的地理坐标系组件。
            data: [
              {
                name: "广东",
                value: [113.280637, 23.125178, 193],
              },
              {
                name: "北京",
                value: [116.405285, 39.904989, 199],
              },
            ],
            symbolSize: function (val) {
              return val[2] / 10;
            },
            itemStyle: {
              color: "yellow",
              shadowBlur: 10,
              shadowColor: "yellow",
            },
          },
        ],
      };

```



#### 3.地图+散点图最终的案例

```json
      var mapName = "中国"
      var data = [
        { name: "北京", value: 199 },
        { name: "天津", value: 42 },
        { name: "河北", value: 102 },
        { name: "山西", value: 81 },
        { name: "内蒙古", value: 47 },
        { name: "辽宁", value: 67 },
        { name: "吉林", value: 82 },
        { name: "黑龙江", value: 123 },
        { name: "上海", value: 154 },
        { name: "江苏", value: 102 },
        { name: "浙江", value: 114 },
        { name: "安徽", value: 109 },
        { name: "福建", value: 116 },
        { name: "江西", value: 91 },
        { name: "山东", value: 119 },
        { name: "河南", value: 137 },
        { name: "湖北", value: 116 },
        { name: "湖南", value: 114 },
        { name: "重庆", value: 101 },
        { name: "四川", value: 125 },
        { name: "贵州", value: 62 },
        { name: "云南", value: 83 },
        { name: "西藏", value: 9 },
        { name: "陕西", value: 80 },
        { name: "甘肃", value: 56 },
        { name: "青海", value: 10 },
        { name: "宁夏", value: 18 },
        { name: "新疆", value: 120 },
        { name: "广东", value: 193 },
        { name: "广西", value: 59 },
        { name: "海南", value: 14 },
      ];

      var geoCoordMap = {};
      /*获取地图数据*/
      myChart.showLoading();
      // console.log(echarts.getMap(mapName));
      var mapFeatures = echarts.getMap(mapName).geoJson.features;
      mapFeatures.forEach(function (v) {
        // 地区名称
        var name = v.properties.name;
        // 地区经纬度
        geoCoordMap[name] = v.properties.cp;
      });
      myChart.hideLoading();
      console.log("data=>", data);
      console.log("geoCoordMap=>", geoCoordMap);

      var convertData = function (data) {
        var res = [];
        for (var i = 0; i < data.length; i++) {
          var geoCoord = geoCoordMap[data[i].name];
          if (geoCoord) {
            res.push({
              name: data[i].name,
              value: [...geoCoord, data[i].value],
            });
          }
        }
        console.log("res=>", res);
        return res;
      };

      // 2.指定图表的配置项和数据
      var option = {
        tooltip: {},
        visualMap: {
          left: "20%",
          seriesIndex: [0],
          inRange: {
            color: ["#04387b", "#467bc0"], // 蓝绿
          },
        },
        geo: {
          map: "中国",
          roam: false,
          label: { show: false },
          aspectScale: 0.75,
          itemStyle: {
            areaColor: "#023677",
            borderColor: "#1180c7",
          },
          emphasis: {
            itemStyle: { areaColor: "#4499d0" },
            label: { color: "white" },
          },
        },
        series: [
          {
            name: "中国地图",
            type: "map",
            map: "中国",
            data,
            // 地图样式
            itemStyle: {
              areaColor: "#023677",
              borderColor: "#1180c7",
            },
            emphasis: {
              itemStyle: { areaColor: "#4499d0" },
              label: { color: "white" },
            },
            select: {
              label: { color: "white" },
              itemStyle: { areaColor: "#4499d0" },
            },
          },
            
          {
            name: "散点图充电桩",
            type: "effectScatter",
            geoIndex: 0,
            coordinateSystem: "geo", // 使用地理坐标系，通过 geoIndex 指定相应的地理坐标系组件。
            data: convertData(data),
            symbolSize: function (val) {
              return val[2] / 10;
            },
            itemStyle: {
              color: "yellow",
              shadowBlur: 10,
              shadowColor: "yellow",
            },
            tooltip: {
              show: true,
              trigger: "item",
              formatter: function (params) {
                console.log(params);
                var data = params.data;
                return `${params.seriesName} <div style="margin:5px 0px;"/> ${data.name} ${data.value[2]}`;
              },
            },
          },
        ],
      };

```



## 5.ECharts API

### 1.响应式图表

```js
      // 1.响应式图表
      window.addEventListener("resize", function () {
        console.log("resize");
        myChart.resize(); // 可以接收一个对象，传递修改后的宽 和 高
        // myChart.resize({ height: "600px" });
      });
```



### 2.自动轮播提示框

```json
     // 自动轮播图 bar
      setInterval(function () {
        autoToolTip();
      }, 1000);

      let index = 0; // 0-5
      function autoToolTip() {
        index++;
        if (index > 5) {
          index = 0;
        }
        // 1.显示提示框
        myChart.dispatchAction({
          type: "showTip", // 触发的action type
          seriesIndex: 0, // 系列的 索引
          dataIndex: index,// 数据项的 索引
          position: "top", // top
        });
      }
```



### 3.图表点击事件(地图下钻)

```js
      // 1..监听鼠标点击事件
      myChart.on("click", function (event) {
        console.log(event);
        if (event.name === "广东") {
          option.geo.map = "gd";
          myChart.setOption(option);
        }
      });
```









