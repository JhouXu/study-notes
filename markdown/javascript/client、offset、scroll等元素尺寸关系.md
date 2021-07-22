@[TOC](文章目录)

<hr style=" border:solid; width:100px; height:1px;" color=#000000 size=1">

# 前言

在 Element 和 HTMLElement 中提供了一系列获取元素相关宽高的属性，常用到的有 client、offset、scroll等三大属性，将浅谈它们之前的关系和区别。

<hr style=" border:solid; width:100px; height:1px;" color=#000000 size=1">

# client

![请添加图片描述](https://img-blog.csdnimg.cn/img_convert/4ecd26d41007a912bf2088f01f33495d.png)

Element.clientWidth 属性表示元素的`内部宽度`，以像素计。该属性包括内边距 padding，但不包括边框 border、外边距 margin 和垂直滚动条（如果有的话）。
Element.clientHeight 属性表示元素的`内部高度`，以像素计。该属性包括内边距 padding，但不包括边框 border、外边距 margin 和水平滚动条（如果有的话）。

# offset

![请添加图片描述](https://img-blog.csdnimg.cn/img_convert/4f399a3e94b9d8023e1637068c7d67ee.png)

HTMLElement.offsetWidth 属性表示元素的`外部宽度`，以像素计。该属性包括内边距 padding、边框 border，但不包括外边距 margin 和垂直滚动条（如果有的话）。
HTMLElement.offsetHeight 属性表示元素的`外部高度`，以像素计。该属性包括内边距 padding、边框 border，但不包括外边距 margin 和水平滚动条（如果有的话）。

# scroll

Element.scrollWidth 这个只读属性是元素内容宽度的一种度量，`包括由于 overflow 溢出而在屏幕上不可见的内容`。该属性包括内边距 padding，但不包括边框 border、外边距 margin 和垂直滚动条（如果有的话）。
Element.scrollHeight 这个只读属性是元素内容高度的一种度量，`包括由于 overflow 溢出而在屏幕上不可见的内容`。该属性包括内边距 padding，但不包括边框 border、外边距 margin 和水平滚动条（如果有的话）。

# 对比

|   尺寸单位   |       说明       |
| :----------: | :--------------: |
| clientWidth  | 内容可视区域宽度 |
| clientHeight | 内容可视区域高度 |
| offsetWidth  |   元素实际宽度   |
| offsetHeight |   元素实际高度   |
| scrollWidth  |   实际内容宽度   |
| scrollHeight |   实际内容高度   |

# 案例

```html
<style>
  * {
    margin: 0;
    padding: 0;
  }
  .main {
    margin: 30px;
    padding: 20px;
    width: 100px;
    height: 100px;
    background-color: #7f8c8d;
    border: 10px solid #2c3e50;
    overflow-x: scroll;
  }
</style>
<body>
  <div class="main">
    Lorem, ipsum dolor sit amet consectetur adipisicing elit. Cum quibusdam doloremque magnam vel, fuga tempora tempore
    officia tenetur quidem qui!
  </div>
</body>
<script>
  const main = document.querySelector(".main");
  console.log(main.clientWidth, main.clientHeight); //123, 123
  console.log(main.offsetWidth, main.offsetHeight); //160, 160
  console.log(main.scrollWidth, main.scrollHeight); //134, 397
</script>
```

![请添加图片描述](https://img-blog.csdnimg.cn/img_convert/c8194c5ab9139e9f146b1852c9abb05d.png)

<hr style=" border:solid; width:100px; height:1px;" color=#000000 size=1">

`最后，如果您有更好的方法，欢迎在留言区中分享；或者实际操作中遇到什么问题均可留言或者私信我，感谢您的观看！`

官方文档：
[MDN Web Docs](https://developer.mozilla.org/zh-CN/docs/Web/API/Element)
