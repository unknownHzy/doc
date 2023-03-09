flex:

当使用flex布局，紫云素的float/clear/vertical-calign将会失效。


flex布局原理：通过给父盒子添加flex属性，来控制子盒子的位置和排列方式。


### 给父项添加常见属性

1. flex-direction: 设置主轴方向
2. justify-content: 主轴对其方式 设置“主轴”上的字元素的排列方式
3. flex-wrap: 设置子元素是否换行
4. align-content: 设置侧轴上的字元素的排列方式（多行）
5. align-items: 设置侧轴上的字元素排列方式 （单行）
6. flex-flow: 复合属性，相当于同时设置了flex-direction和flex-wrap

#### 主轴与侧轴说明
flex布局中，分为主轴与侧轴两方向，同样有x轴与y轴叫法   
默认主轴方向就是x轴方向，水平向右垂直。   
主轴与侧轴是可以变换的，就看flex-direction设置的谁是主轴，剩下的就是侧轴。子元素是跟着主轴方向来排列的
##### flex-direction四个属性：
row: 默认值从左到右   
row-reverse: 从右到左   
column: 从上到下   
column-reverse: 从下到上   

##### justify-content5个属性:主轴方向
flex-start: 默认值从头部开始，如果主轴是x轴，则从左到右（全部挤在一起）   
flex-end: 从尾部开始排列 （全部挤在一起）   
center: 在主轴剧中对齐（如果主轴是x轴则水平居中） （全部挤在一起）   
space-around: 平分剩余空间（两边也会有剩余）   
space-between: 线两边贴边，再平分剩余空间（重要：注意与space-around区别是两边贴边）   

##### flex-wrap 设置子元素是否换行
默认情况下，所有的子元素是不换行的，都排在一条轴线上。flex布局中默认是不换行的   
nowrap：默认值，不换行。而且容器的大小会自动收缩，以满足在一行中显示。   
wrap：换行   

##### align-items 设置侧轴上的字元素排列方式（单行）
该属性是控制子项在侧轴（默认是y轴）上的排列方式 在子项为单项的时候使用：   
flex-start: 默认值 从上到下   
flex-end: 从下到上   
center: 挤在一起居中（垂直居中）   
stretch： 拉伸，沿着侧轴拉伸满   

##### align-content: 相对于align-items，这个属性是多行。 注意： 在单行效果下无效
（在按照子项的宽度，然后按照flex-wrap： nowrap不换行进行侧轴排列，如果容器的宽度<子项的宽度，则会使得子项缩小。如果此时使用nowrap，则会换行，此时应该使用align-content）
属性值：   
flex-start: 默认值在侧轴的头部开始排列   
flex-end: 默认值在侧轴的尾部开始排列   
center：在侧轴中间显示   
space-around: 子项在侧轴平分剩余空间   
space-between: 子项在侧轴先分布在两头，再平分剩余空间   
stretch: 设置子项元素高度平分父元素高度   

设置子项在侧轴上的排列方式，并且只能用于子项出现“换行”的情况（多行），在单行下是没有效果的

##### flex-wrap：flex-direction和flex-wrap
把设置主轴方向和是否换行（换列）简写：flex-flow: column wrap;


flex布局子项常见属性：

重要
##### flex属性定义子项分配剩余空间，用flex来表示占多少份数：
.item {
flex: <number>; /* default 0 */   
}

### 案例1：左右固定，中间自适应
父容器：   
display: flex   
子项：   
左右两个固定宽度，中间自适应使用flex：1   

### 案例2: 在父容器中的n个子项，每个能够平均分配父容器空间
```css
<p>
	<span></span>
	<span></span>
	<span></span>
</p>
```

```css
// 各个子项平均分父容器空间
p span {
	flex: 1
}
```

```css
// 第一个与第三个只占一份 1/4
p span {
	flex: 1;
}
// 第二个占两份 2/4
p span:nth-child(2) {
	flex: 2;
	background-color: black;
}
```

##### align-self 控制子项自己在侧轴上的排列方式
align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认为auto，
表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。


```css
<p>
	<span></span>
	<span></span>
	<span></span>
</p>
```

```css
span:nth-child(2) {
/* 设置自己在侧轴上的排列方式: 假设纵轴为侧轴，则flex-end的元素，会在纵轴的底部 */
align-self: flex-end
}

```
##### order 属性定义子项的左右排列顺序
数值越小，排列越靠前，默认为0. 注意：和z-index不一样。


### 案例：
1. 水平垂直居中的两种方式：  
   1）一行有多个元素需要垂直居中：   
   flex-direction: row;   
   justify-content: center;   
   align-items: center   

2）垂直居中：
flex-direction: column; // 主轴是y轴   
justify-content: center; // y轴上居中 
