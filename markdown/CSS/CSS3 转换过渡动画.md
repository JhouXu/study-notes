@[TOC](文章目录)

<hr style=" border:solid; width:100px; height:1px;" color=#000000 size=1">

# 前言

前言

<hr style=" border:solid; width:100px; height:1px;" color=#000000 size=1">

# transform

transform 属性允许你`旋转`，`缩放`，`倾斜`或`平移`给定元素。这是通过修改 `CSS 视觉格式化模型的坐标空间`来实现的。其中 transform 属性可以根据转换后的效果分为 2D 和 3D 的，下面将分别从属性值和使用方式进行介绍。

## 2D transform

相关属性值：

- translate(x, y) - `平移`，根据 x,y 轴对应的值进行相对位置移动，类似 position:relative；translate(x) 等同于 translate(x,0)；可选单位：css 中关于长度单位均可。
  - translateX(x) - 仅设置 x 轴上的偏移位置。
  - translateY(y) - 仅设置 y 轴上的偏移位置。
- rotate(deg) - `旋转角度`，根据 deg 角度的设定让元素以`自身中心位置为原点`发生旋转；可选单位：deg（css 中表示角度的单位）。
- scale(mul) - `缩放`，根据 mul 缩放倍数根据`自身中心位置为原点`发生放大缩小效果，mul 参数是一个大于等于 0 的实数，默认值：1，大于 1 表示放大，小于 1 表示缩小。
  - scaleX(mul) - 改变元素的宽度。
  - scaleY(mul) - 改变元素的高度。
- skew(\<angle\> [,\<angle\>]) - `倾斜角度`，分别表示 X 轴和 Y 轴倾斜的角度，如果第二个参数为空，则默认为 0，参数为负表示向相反方向倾斜；可选单位：deg（css 中表示角度的单位）。
  - skewX(\<angle\>) - 表示只在 X 轴(水平方向)倾斜。
  - skewY(\<angle\>) - 表示只在 Y 轴(水平方向)倾斜。
- matrix(a, b, c, d, tx, ty) - 是 2D 变换方法的`组合设置`，设置缩放，倾斜和移动（平移）功能。。
  - a - 水平缩放
  - b - 水平倾斜
  - c - 垂直倾斜
  - d - 垂直缩放
  - tx - 水平移动
  - ty - 垂直移动

```html
<!-- 2d 案例 -->
<style>
  * {
    margin: 0;
    padding: 0;
  }
  .child {
    width: 100px;
    height: 100px;
    background-color: #8e44ad;
    transform: translate(150px, 60px) rotate(-35deg) scale(1.5) skew(1deg);
    /* transform: matrix(1.5, 0, 0, 1.5, 150, 60); */ /* 除了旋转外的同等配置 */
    color: #fff;
  }
</style>
<body>
  <div class="child">2D 转换</div>
</body>
```

## 3D transform

相关属性：

- translate3d(x,y,z) - 定义 3D `转化`。
  - translateX(x) - 仅使用用于 X 轴的值。
  - translateY(y) - 仅使用用于 Y 轴的值。
  - translateZ(z) - 仅使用用于 Z 轴的值。
- rotate3d(x,y,z,angle) - 定义 3D `旋转`。
  - rotateX(angle) - 定义沿 X 轴的 3D 旋转。
  - rotateY(angle) - 定义沿 Y 轴的 3D 旋转。
  - rotateZ(angle) - 定义沿 Z 轴的 3D 旋转。
- scale3d(x,y,z) - 定义 3D `缩放`转换。
  - scaleX(x) - 通过给定一个 X 轴的值。
  - scaleY(y) - 通过给定一个 Y 轴的值。
  - scaleZ(z) - 通过给定一个 Z 轴的值。
- matrix3d(a1, b1, c1, d1, a2, b2, c2, d2, a3, b3, c3, d3, a4, b4, c4, d4) - 定义 3D 转换，使用 16 个值的 4x4 矩阵。
- perspective(n) - 定义 3D 转换元素的`透视视图`。
  - perspective() 这个 CSS 函数定义了 z=0 平面与用户之间的距离，以便给三维定位元素一定透视度。当每个 3D 元素的 z>0 时会显得比较大，而在 z<0 时会显得比较小。其影响的程度由这个属性的值来决定。
  - 该参数是一个 \<length\> 给定从用户（显示屏）到 z = 0 平面的距离。 它用于将透视图转换应用于元素。 如果它是 0 或负值，则不应用透视变换。

相关单位与 2d 的一致，就不过多描述，直接上案例。

```html
<style>
  * {
    margin: 0;
    padding: 0;
  }
  body {
    padding: 100px;
  }
  .child {
    margin-bottom: 20px;
    width: 100px;
    height: 100px;
    color: #fff;
  }
  .translate3d {
    background-color: #8e44adee;
    transform: translate3d(30px, 30px, 30px);
  }
  .rotate3d {
    background-color: #2980b9ee;
    transform: rotate3d(20, 20, 20, 10deg);
  }
  .scale3d {
    background-color: #2c3e50ee;
    transform: scale3d(1.2, 1.2, 1.2);
  }
</style>
<body>
  <div class="child translate3d">3D 转化</div>
  <div class="child rotate3d">3D 旋转</div>
  <div class="child scale3d">3D 缩放</div>
</body>
```

## 其它相关转换属性

### transform-origin

transform-origin 属性允许您更改转换元素的位置。默认转换位置是在元素的正中心。
2D 转换元素可以改变元素的 X 和 Y 轴。 3D 转换元素，还可以更改元素的 Z 轴。

```css
/* 语法 */
transform-origin: x-axis y-axis z-axis;
```

可选值：

- x-axis - 定义视图被置于 X 轴的何处。可能的值：left、center、right、length、%。
- y-axis - 定义视图被置于 X 轴的何处。可能的值：left、center、right、length、%。
- z-axis - 定义视图被置于 Z 轴的何处。可能的值：length。

### transform-style

transform--style属性指定嵌套元素是怎样在三维空间中呈现。
注意： 使用此属性必须先使用 transform 属性.

可选值：

- flat - 表示所有子元素在2D平面呈现。
- preserve-3d - 表示所有子元素在3D空间中呈现。

### perspective

多少像素的 3D 元素是从视图的 perspective 属性定义。这个属性允许你改变 `3D 元素是怎样查看透视图`。
定义时的 perspective 属性，它是一个元素的子元素，透视图，而不是元素本身。perspective 属性只影响 3D 转换元素。

可选值：

- number - 元素距离视图的距离，以像素计。
- none - 默认值。与 0 相同。不设置透视。

### perspective-origin

perspective-origin 属性定义 3D 元素所基于的 X 轴和 Y 轴。该属性允许您改变 `3D 元素的底部位置`。
定义时的 perspective -Origin 属性，它是一个元素的子元素，透视图，而不是元素本身。

```css
/* 语法 */
perspective-origin: x-axis y-axis;
```

可选值：

- x-axis - 定义该视图在 x 轴上的位置。默认值：50%。可能的值：left、center、right、length、%。
- y-axis - 定义该视图在 y 轴上的位置。默认值：50%。可能的值：left、center、right、length、%。

### backface-visibility

backface-visibility 属性定义当元素背面向屏幕时是否可见。

可选值：

- visible - 背面是可见的。
- hidden - 背面是不可见的。

# transition

# animation
