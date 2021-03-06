---
title: Flex 弹性盒模型
categories:
- CSS
tags:
- 盒模型
- Flex
date: 2017-12-08 15:04:51
---

# Flex 弹性盒模型

## 福利

第一篇博客，什么也不说，先来波福利。

[Nice and Free CSS Templates](http://www.mycelly.com/)

#### 1.1 两列自适应布局 (menu and content dynamic)
```html
<div id="menu">
    <h1>left column</h1>
</div>
<div id="content">
    <h1>right column</h1>
</div>
```
```css
body {
    background-color: #8b4513;
    font-size: 11px;
    font-family: Verdana, Arial, Helvetica, SunSans-Regular, Sans-Serif;
    padding:0px;
    margin:0px;
}
#content {
    margin-left: 30%;
    background:#fff;
    border-right:2px solid #996666;
    border-bottom:2px solid #996666;
    margin-right:15px;
    padding-bottom:20px;
}
```

#### 1.2 一列固定自适应布局 (menu fixed, content dynamic)
```html
<div id="menu">
    <h2>right column</h2>
</div>
<div id="content">
    <h2>content column</h2>
</div>
```
```css
html {
    padding:0px;
    margin:0px;
}
body {
    background-color: #e1ddd9;
    font-size: 12px;
    font-family: Verdana, Arial, SunSans-Regular, Sans-Serif;
    color:#564b47;
    padding:0px 20px;
    margin:0px;
}
#menu {
    position: absolute;
    width: 200px;
    left: 20px;
    padding:0px;
    margin:0px;
}
#content {
    margin-left: 200px;
    background-color:#fff;
    overflow: auto;
}
```

![img](http://olq0r66c9.bkt.clouddn.com/md/1512982815479.png)

图中的布局大家应该都看过，经常为了实现某种特定布局而询问古哥和度娘，找到的方案也有可能并不适用移动端。

下面就介绍一下，已经被 w3c 定为标准的 (Flex Box)[https://www.w3.org/TR/css-flexbox-1/] 布局。

## 弹性盒模型属性介绍

#### 1.1 弹性盒模型容器 (Flex Container)

```css
#box {
    display: flex | inline-flex;
}
```

声明一个页面元素为展现形式为 flex(inline-flex) 后，该元素成为弹性盒模型容器，同时会默认创建一个弹性盒模型上下文 (Flex Formatting Context) 。使里面的子元素都会受到弹性盒模型的控制，称为弹性盒模型项目 Flex Items 。

#### 1.2 弹性盒模型简介

Flex Container 包含一个交叉轴 （cross axis) ，一个主轴 (main axis) ，主轴空间 (main size) 等。这些属性为 Flex Items 的方向、起始位置、大小等等提供了参照依据。

注意：主轴如果起点在左端，那么纵轴起点就在上端。以此类推。

![img](http://olq0r66c9.bkt.clouddn.com/md/1512985335295.png)

#### 1.3 确定轴方向 (flex-direction)

```css
#box {
    flex-direction: row | row-reverse | column | column-reverse;
}
```

四个属性值：
- row: （默认值）主轴为水平方向，起点在左端。
- row-reverse: 主轴为水平方向，起点在右端。
- column: 主轴为垂直方向，起点在上沿。
- column-reverse: 主轴为垂直方向，起点在下沿。

#### 1.4 如何换行 (flex-wrap)

```css
#box {
    flex-wrap: nowrap | wrap | wrap-reverse;
}
```

三个值属性：
- nowrap: 单行，不换行
- wrap: 多行，正常换行
- wrap-reverse: 多行，第一行从轴线尾端开始。

#### 1.5 项目主轴上的对齐方式 (justify-content)

```css
#box {
    justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

假设，主轴从左到右，属性值表示：
- flex-start: （默认值）左对齐
- flex-end: 右对齐
- center: 居中
- space-between: 两端对齐，项目之间的间隔都相等。
- space-around: 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

#### 1.6 项目在交叉轴方向上的对齐方式 (align-items)
```css
#box {
    align-items: flex-start | flex-end | center | baseline | stretch;
}
```

假设，交叉轴从上到下，属性值表示：
- flex-start: 交叉轴的起点对齐。
- flex-end: 交叉轴的终点对齐。
- center: 交叉轴的中点对齐。
- baseline: 项目的第一行文字的基线对齐。
- stretch: （默认值）如果项目未设置高度或设为 auto，将占满整个容器的高度。

#### 1.7 多行项目在交叉轴方向上的对齐方式 (align-content)
```css
#box {
    align-content: flex-start | flex-end | center | space-between | space-around | stretch;
}
```

属性值表示：
- flex-start: 与交叉轴的起点对齐。
- flex-end: 与交叉轴的终点对齐。
- center: 与交叉轴的中点对齐。
- space-between: 与交叉轴两端对齐，轴线之间的间隔平均分布。
- space-around: 每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- stretch: （默认值）轴线占满整个交叉轴。

#### 2.1 弹性盒模型项目
弹性盒模型项目 Flex Items 为弹性盒模型容器的子元素，依据弹性盒模型进行布局。

#### 2.2 指定当前项目所在顺序 (order)
```css
.item {
    order: <integer>; /* default 0 */
}
```
默认为 0 ，越小越靠前，可以为负数。

#### 2.3 扩大当前项目所占剩余空间 (flex-grow)
```css
.item {
    flex-grow: <number>; /* default 0 */
}
```
如果设置默认值0，即使存在剩余空间也不会扩大所占空间。

如果有4个项目，都为1，那么每个项目所占比例为 1/4 等分。

如果有4个项目，如果其中有一个项目为2，那么该项目占 2/5，其余占 1/5。

如果项目都不为0，容器扩大，那么项目等比例扩大。

#### 2.4 缩小当前项目所占剩余空间 (flex-shrink)
```css
.item {
    flex-shrink: <number>; /* default 1 */
}
```
如果设置值为0，即使剩余空间不足该项目也不会缩小自身空间。

如果有4个项目，都为1，那么每个项目所占比例为 1/4 等分。

如果有4个项目，如果其中有一个项目为2，那么该项目占 2/5，其余占 1/5。

如果项目都不为0，如果容器缩小，那么项目等比例缩小。

#### 2.5 指定当前项目所占固定空间大小 (flex-basis)
```css
.item {
    flex-basis: <length> | auto; /* default auto */
}
```
属性表示，固定占据容器比例，容器变化不影响项目占据空间变化。

如果设为跟 width 或 height 属性一样的值，比如：350px ，则项目将占据固定空间。

#### 2.6 当前项目独立设定对齐方式 (align-self)
```css
.item {
    align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```
该属性将覆盖容器的 align-items 属性。

默认 auto 将继承容器的 align-items 属性，没有 align-items 的话，将等同 stretch 。

除了 auto ，其他都与 align-items 属性完全一致。

#### 3.1 弹性盒模型容器属性简写 (flex-flow)

```css
.box {
    flex-flow: <flex-direction> || <flex-wrap>;
}
```

默认值：`row nowrap` 。

#### 3.2 弹性盒模型项目属性简写 (flex)
```css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```
默认值：`0 1 auto` 。后两个属性可选。

缩写值：`auto` 等同于 `1 1 auto` ；`none` 等同于 `0 0 auto`

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

至此，弹性盒模型 Flex 相关属性已经介绍完毕。

通过仔细阅读，细心的朋友可以发现，这些属性和通常 word 中的文字排版类似，左对齐，右对齐，两端对齐，只不过需要指定主轴方向，以及设置哪端为起点。

主轴为垂直方向时，只要想像把 word 横过来看就好了。

如果还不明白，想一想 web 页面创建最初的目的，追寻起源，可能会有启发。

网页的本质就是超级文本标记语言，目的是为了展示资源信息，是媒体的载体。而文字最初占据了页面的大部分内容。


## 弹性盒模型实例

![formatter](/img/bg2015071327.png)

#### 1.1 骰子布局

![img](http://olq0r66c9.bkt.clouddn.com/md/1513066684036.png)

```html
<div class="first-face">
  <span class="pip"></span>
</div>
<div class="second-face">
  <span class="pip"></span>
  <span class="pip"></span>
</div>
<div class="third-face">
  <span class="pip"></span>
  <span class="pip"></span>
  <span class="pip"></span>
</div>
<div class="fourth-face">
  <div class="column">
    <span class="pip"></span>
    <span class="pip"></span>
  </div>
  <div class="column">
    <span class="pip"></span>
    <span class="pip"></span>
  </div>
</div>
<div class="fifth-face">
  <div class="column">
    <span class="pip"></span>
    <span class="pip"></span>
  </div>
  <div class="column">
    <span class="pip"></span>
  </div>
  <div class="column">
    <span class="pip"></span>
    <span class="pip"></span>
  </div>
</div>
<div class="sixth-face">
  <div class="column">
    <span class="pip"></span>
    <span class="pip"></span>
    <span class="pip"></span>
  </div>
  <div class="column">
    <span class="pip"></span>
    <span class="pip"></span>
    <span class="pip"></span>
  </div>
</div>
```

```css
.first-face {
  display: flex;
  justify-content: center;
  align-items: center;
}

.second-face {
  display: flex;
  justify-content: space-between;
}

.second-face .pip:nth-of-type(2) {
  align-self: flex-end;
}

.third-face {
  display: flex;
  justify-content: space-between;
}

.third-face .pip:nth-of-type(2) {
  align-self: center;
}

.third-face .pip:nth-of-type(3) {
  align-self: flex-end;
}

.fourth-face, .sixth-face {
  display: flex;
  justify-content: space-between;
}

.fourth-face .column, .sixth-face .column {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.fifth-face {
  display: flex;
  justify-content: space-between;
}

.fifth-face .column {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.fifth-face .column:nth-of-type(2) {
  justify-content: center;
}

/* OTHER STYLES */

* {
  box-sizing: border-box;
}

html, body {
  height: 100%;
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  vertical-align: center;
  flex-wrap: wrap;
  align-content: center;
  font-family: 'Open Sans', sans-serif;

  background: linear-gradient(top, #222, #333);
}

[class$="face"] {
  margin: 16px;
  padding: 4px;

  background-color: #e7e7e7;
  width: 104px;
  height: 104px;
  object-fit: contain;

  box-shadow:
    inset 0 5px white,
    inset 0 -5px #bbb,
    inset 5px 0 #d7d7d7,
    inset -5px 0 #d7d7d7;

  border-radius: 10%;
}

.pip {
  display: block;
  width: 24px;
  height: 24px;
  border-radius: 50%;
  margin: 4px;

  background-color: #333;
  box-shadow: inset 0 3px #111, inset 0 -3px #555;
}
```

#### 1.2 九宫格布局

##### 1.2.1 单项目

基本使用弹性盒模型对齐方式就可实现
```html
<div class="box">
  <span class="item"></span>
</div>
```

```css
.box {
    display: flex;
    justify-content: center | flex-end;
    align-items: center | flex-end;
}
```

定义为弹性盒模型，创建弹性盒模型上下文，默认流方向，从左到右，从上到下。

默认主轴左对齐，改变对齐方式为居中或右对齐；默认交叉轴为上对齐，改为垂直居中对齐或下对齐。

可以试试改变属性值，改变点的位置。

##### 1.2.2 双项目

```html
<div class="box">
  <span class="item"></span>
  <span class="item"></span>
</div>
```
```css
.box {
  display: flex;
  flex-direction: column;
  justify-content: space-between | flex-end;
  align-items: center | flex-end;
}
```
水平或垂直双项目时，不添加 `flex-direction` 属性时候，默认主轴水平方向，添加 `flex-direction: column;` 属性后，主轴改为垂直方向。

当只有一个轴上有项目，导致 `align-items: space-between` 不会起作用，`justify-content: space-between` 与主轴方向配合起作用。

```css
.box {
  display: flex;
  justify-content: space-between;
}

.item:nth-child(2) {
  align-self: center | flex-end;
}
```
对角线布局双项目，独立改变第二个 Flex Item 交叉轴对齐位置。

##### 1.2.3 对角线三项目
```css
.box {
  display: flex;
}

.item:nth-child(2) {
  align-self: center;
}

.item:nth-child(3) {
  align-self: flex-end;
}
```

##### 1.2.4 四项目
```css
.box {
    display: flex;
    flex-wrap: wrap;
    justify-content: flex-end;
    align-content: space-between;
}
```
三项一排，单独一项对齐。

前提，每个项目固定宽度，容器宽度可以导致换行，出现多行容器状态，使 `align-content` 可以起作用。

```html
<div class="box">
  <div class="column">
    <span class="item"></span>
    <span class="item"></span>
  </div>
  <div class="column">
    <span class="item"></span>
    <span class="item"></span>
  </div>
</div>
```
```css
.box {
  display: flex;
  flex-wrap: wrap;
  align-content: space-between;
}
.column {
  flex-basis: 100%;
  display: flex;
  justify-content: space-between;
}
```
两两项目分组。

前提，每组占据空间 `flex-basis: 100%` 可以导致换行，进行多行布局对齐。

每组为单独弹性盒模型，再进行主轴对齐方式设置。

##### 1.2.5 五项目、六项目
```html
<div class="box">
  <div class="row">
    <span class="item"></span>
    <span class="item"></span>
    <span class="item"></span>
  </div>
  <div class="row">
    <span class="item"></span>
  </div>
  <div class="row">
     <span class="item"></span>
     <span class="item"></span>
  </div>
</div>
```
```css
.box {
    display: flex;
    flex-wrap: wrap;
}
.row {
    flex-basis: 100%;
    display:flex;
}
.row:nth-child(2) {
    justify-content: center;
}
.row:nth-child(3) {
    justify-content: space-between;
}
```
可以看成三三分组。

前提，每组占满容器空间，设置每组排列方式

```css
.afifth-face {
    display: flex;
    justify-content: space-between;
}
.afifth-face .column {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.afifth-face .column:nth-child(2) {
    justify-content: center;
}
```

可以尝试通过设置主轴方向，改变整体布局结构。

#### 2.2 网格布局（栅格布局）

网格布局最重要的是保证平均分布，每项占据空间相等。

```html
<div class="Grid">
  <div class="Grid-cell">...</div>
  <div class="Grid-cell">...</div>
  <div class="Grid-cell">...</div>
</div>
```
```css
.Grid {
  display: flex;
}
.Grid-cell {
  flex: 1;
}
```

flex 属性设置扩大或缩小剩余空间策略。

#### 2.3 百分比布局
该布局特点是某个项目固定百分比，其他项目平均分配剩余空间。

```html
<div class="Grid">
  <div class="Grid-cell u-1of4">...</div>
  <div class="Grid-cell">...</div>
  <div class="Grid-cell u-1of3">...</div>
</div>
```
```css
.Grid {
  display: flex;
}
.Grid-cell {
  flex: 1;
}
.Grid-cell.u-full {
  flex: 0 0 100%;
}
.Grid-cell.u-1of2 {
  flex: 0 0 50%;
}
.Grid-cell.u-1of3 {
  flex: 0 0 33.3333%;
}
.Grid-cell.u-1of4 {
  flex: 0 0 25%;
}
```
设置每个项目等分占据空间，再每项单独设置固定宽度。

其他实用的布局请移步[阮老师的博客文章](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)，讲得很清楚。

## 兼容性

#### 1.1 W3C 各个版本的 flex

2009 version

tag: `display: box; or a property that is box-{*} (eg. box-pack)`

2011 version

tag: `display: flexbox; or the flex() function or flex-pack property`

2012 version

tag: `display: flex/inline-flex; and flex-{*} properties`

2014 version

新增了对 `flex` 项 `z-index` 的规定，创建层叠上下文

2015 W3C Editor’s Draft

没有大的改动，只是个草案，还处于修修改改的阶段，还没有征集浏览器供应商的意见

2017 W3C Candidate Recommendation

已经被推荐使用，命名 Level 1

#### 兼容性

根据 [CanIUse](http://caniuse.com/#feat=flexbox) 的数据可以总结如下：

IE10 部分支持 2012 ，需要 -ms- 前缀

Android4.1/4.2-4.3 部分支持 2009 ，需要 -webkit- 前缀

Safari7/7.1/8 部分支持 2012 ，需要 -webkit- 前缀

IOS Safari7.0-7.1/8.1-8.3 部分支持 2012 ，需要 -webkit- 前缀

[flexbox 版本2012](http://www.w3.org/TR/2012/CR-css3-flexbox-20120918/)

[flexbox 版本2009](http://www.w3.org/TR/2009/WD-css3-flexbox-20090723/)

总体来说不是全兼容，IE 就算了吧，移动端兼容还算不错，只需要注意一下 Android UC 兼容使用。


# 小结

这是本人的第一篇博客，只是一个总结，写了文章，总是会想自己有没有问题，会去尝试，感觉能够再提高一些。

文章只是总结，不能算深入理解，才疏学浅，希望大家还是多看参考链接，深入理解。

### 相关参考
> [Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)
>
> [Flex 布局教程：实例篇](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)
>
> [A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/))
>
> [Centering in CSS: A Complete Guide](https://css-tricks.com/centering-css-complete-guide/)
>
> [https://davidwalsh.name/flexbox-dice](https://davidwalsh.name/flexbox-dice)
>
> [Solved by Flexbox](https://philipwalton.github.io/solved-by-flexbox/)
>
> [【web】flex布局浏览器兼容处理](http://blog.csdn.net/u014641010/article/details/50968567)
