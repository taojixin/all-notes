## flex布局

### 1.flex-direction

> flex-direction属性决定主轴的方向（即项目的排列方向）。

- row（默认值）：主轴为水平方向，起点在左端。
- row-reverse：主轴为水平方向，起点在右端。
- column：主轴为垂直方向，起点在上沿。
- column-reverse：主轴为垂直方向，起点在下沿。

### 2.flex-wrap

> 默认情况下，项目都排在一条线（又称”轴线”）上。flex-wrap属性定义，如果一条轴线排不下，如何换行。

**三个值：**

![image-20220925201223881](./images/flex-wrap.png)

### 3.flex-flow

> flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。

### 4.justify-content

> justify-content属性定义了项目在主轴上的对齐方式。

- flex-start（默认值）：左对齐
- flex-end：右对齐
- center： 居中
- space-between：两端对齐，项目之间的间隔都相等。
- space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

![image-20220925201359897](./images/justify-content.png)

### 5.align-items

> align-items属性定义项目在交叉轴上如何对齐。

- flex-start：交叉轴的起点对齐。
- flex-end：交叉轴的终点对齐。
- center：交叉轴的中点对齐。
- baseline: 项目的第一行文字的基线对齐。
- stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

![image-20220925201459473](./images/align-items.png)

### 6.align-content

> align-content属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

- flex-start：与交叉轴的起点对齐。
- flex-end：与交叉轴的终点对齐。
- center：与交叉轴的中点对齐。
- space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
- space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- stretch（默认值）：轴线占满整个交叉轴。

![image-20220925201604463](./images/align-content.png)