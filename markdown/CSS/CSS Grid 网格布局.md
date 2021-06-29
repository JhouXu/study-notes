@[TOC](文章目录)

<hr style=" border:solid; width:100px; height:1px;" color=#000000 size=1">

# 前言

在页面开发的过程中，CSS 页面布局技术允许我们拾取网页中的元素，并且控制它们相对正常布局流、周边元素、父容器或者主视口/窗口的位置。
当前主要的布局方式有：浮动布局(Float)、定位布局(Position)、弹性布局(Flex)、网格布局(Grid)等，本文将探讨 flex 弹性布局。

<hr style=" border:solid; width:100px; height:1px;" color=#000000 size=1">

# Grid

CSS 网格布局擅长于将一个页面划分为几个主要区域，以及定义这些区域的大小、位置、层次等关系（前提是 HTML 生成了这些区域）。

像表格一样，网格布局让我们能够按行或列来对齐元素。 然而在布局上，`网格比表格更可能做到或更简单`。 例如，网格容器的子元素可以自己定位，以便它们像 CSS 定位的元素一样，真正的有重叠和层次。

# 一、术语

## 1. 网格 Grid

是指通过 display: grid 属性定义的盒子，称为网格。可以通过 `grid-template-rows` 和 `grid-template-columns` 属性分别设置网格的 行属性 和 列属性。

```html
<style>
  .wrapper {
    display: grid; /* 定义 wrapper 盒子为网格 */
    grid-template-rows: 100px 100px; /* 设置为两行，且行宽度均为100px */
    grid-template-columns: 100px 100px; /* 设置为两列，且列宽度均为100px */
  }
</style>
<body>
  <div class="wrapper"></div>
</body>
```

img1

## 2. 网格线 Grid Line

是指通过定义显式网格时并且设置行列时，自动创建分界线，与 table 表格的边框线类似。（如上图的虚线）

## 3. 网格轨道 Grid Tracks

是指两条网格线之间的空间，常称行或列轨道。

## 4. 网格单元格 Grid Cell

是指网格中的`子项元素`，与表格单元格相似。如下，子项 div1~6 为网格单元格。

```html
<style>
  .wrapper {
    display: grid; /* 定义 wrapper 盒子为网格 */
    grid-template-rows: 100px 100px; /* 设置为两行，且行宽度均为100px */
    grid-template-columns: 100px 100px; /* 设置为两列，且列宽度均为100px */
  }
</style>
<body>
  <div class="wrapper">
    <div>1</div>
    <div>2</div>
    <div>3</div>
    <div>4</div>
    <div>5</div>
  </div>
</body>
```

## 5. 网格区域 Grid Areas

是网格中由`一个或者多个`网格单元格组成的一个矩形区域。是通过网格线位置放置一个项目或者使用命名的网格区域定义区域时，创建的。`网格区域一定是矩形`。

## 6. 网格间隙 Gutters

是指`网格轨道之间的间距`，可以通过 grid-column-gap、grid-row-gap 或者 grid-gap 属性在 Grid 布局中创建。

## 7. 网格轴 Grid Axis

Grid 布局是一种二维布局方法，能够在行和列中布置内容。因此在任何网格中`都有两个轴`，横轴（即行轴，内联）和纵轴（即列轴，块）。基于网格轴可以使用盒模型对齐规范中定义的属性对项目进行行对齐和列对齐。

## 8. 网格行和网格列 Grid Row and Grid Column

- 网格行是 Grid 布局中的水平轨道，即两个`水平网格线`之间的空间。
- 网格列是 Grid 布局中的垂直轨道，即两个`垂直网格线`之间的空间。

两者可以通过简写属性 grid，grid-template 实现快速定义。
