# CSS 不常使用但却很有用的技巧

下面列举一些 CSS 不经常使用，但却很有用的小技巧。

## 1. [cursor](https://developer.mozilla.org/en-US/docs/Web/CSS/cursor)

CSS 属性 **cursor** 用来设置光标的类型，在鼠标指针悬停在元素上时显示相应的样式。

通过 url 属性可以设置光标显示为自定义图片, 如下图 2

```css
cursor: url(./assets/arrow-down-circle.svg) 0 0, progress;
```

同时也支持 emoji 表情, 如图 3

```css
cursor: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg'  width='40' height='48' viewport='0 0 100 100' style='fill:black;font-size:24px;'><text y='50%'>😀</text></svg>"),
  pointer;
```

![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/22d76f2da7a14fd98ee77d9c852a57eb~tplv-k3u1fbpfcp-watermark.image)

cursor 属性可以为零个或多个\<url>值，它们之间用逗号分隔，最后必填一个关键字值。每个\<url>指向一个图像文件。

浏览器的加载顺序是这样：

1. 首先浏览器将尝试加载指定的第一个图像
2. 如果无法加载则尝试加载下一个图像
3. 如果所有 url 指定的图像都无法加载，则使用最后一个值。

每个\<url>后面都可选跟一对空格分隔的数字\<x>\<y>表示偏移。它们用来设置指针的热点(即自定义图标的实际点击位置)，位置相对于图标的左上角。

例如，下面的例子使用\<url>值指定两个图像，为第二个图像提供\<x>\<y>坐标，如果两个图像都无法加载，则返回 pointer 关键字值：

```css
cursor: url(cursor1.png), url(cursor1.png) 2 2, pointer;
```

## 2. [:target](https://developer.mozilla.org/en-US/docs/Web/CSS/:target)

使用 **:target** 伪类创建弹出框的效果

HTML

```HTML
<div class="wrapper">
  <a href="#demo-modal">Open Modal</a>

  <div id="demo-modal" class="modal">
    <div class="modal__content">
      <div class="modal__header">Modal Header</div>
      <div class="modal__body">
        <p>
          You can use the :target pseudo-class to create a modals with Zero
          JavaScript. Enjoy!
        </p>
      </div>
      <div class="modal__footer">Footer</div>
      <a href="#" class="modal__close">X</a>
    </div>
  </div>
</div>
```

CSS

```css
.modal {
  position: absolute;
  height: 100vh;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  visibility: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal:target {
  visibility: visible;
}
```

效果:

![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ddf0655b1f3d404b935e2e6564ecb595~tplv-k3u1fbpfcp-watermark.image)

## 3. [:empty](https://developer.mozilla.org/en-US/docs/Web/CSS/:empty)

**:empty** 伪类代表没有子元素的元素。子元素只可以是元素节点或文本（包括空格）。注释或处理指令都不会产生影响。

HTML

```html
<div class="wrapper">
  <div>red</div>
  <div><!-- green --></div>
</div>
```

CSS

```css
.wrapper div {
  width: 100px;
  height: 100px;
  margin: 0 20px;
  display: flex;
  justify-content: center;
  align-items: center;

  background-color: red;
}
.wrapper div:empty {
  background-color: green;
}
```

效果

![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/932643f242e34f94af64d59ff5ca300f~tplv-k3u1fbpfcp-watermark.image)

## 4. [-webkit-line-clamp](https://developer.mozilla.org/en-US/docs/Web/CSS/-webkit-line-clamp)

CSS 属性 **-webkit-line-clamp** 可以把 **块容器** 中的内容限制为指定的行数。

它只有在 display 属性设置成 -webkit-box 或者 -webkit-inline-box 并且 -webkit-box-orient 属性设置成 vertical 时才有效果

HTML

```html
<p>
  In this example the <code>-webkit-line-clamp</code> property is set to
  <code>3</code>, which means the text is clamped after three lines. An ellipsis
  will be shown at the point where the text is clamped.
</p>
```

CSS

```css
p {
  width: 300px;
  display: -webkit-box;
  -webkit-box-orient: vertical;
  -webkit-line-clamp: 3;
  overflow: hidden;
}
```

效果

![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/58bf7db56eea41f1955ddbb0fa073d8a~tplv-k3u1fbpfcp-watermark.image)

## 5. [sticky](https://developer.mozilla.org/zh-cn/docs/Web/CSS/position#sticky_positioning)

**sticky** 定位可以被认为是相对定位(relative)和固定定位(fixed)的混合。元素在跨越特定阈值前为相对定位，之后为固定定位。

例如：

```css
#one {
  position: sticky;
  top: 10px;
}
```

在 viewport 视口滚动到元素 top 距离小于 10px 之前，元素为相对定位。之后，元素将固定在与顶部距离 10px 的位置，直到 viewport 视口回滚到阈值以下。

HTML

```html
<div class="wrapper">
  <dl>
    <dt>A</dt>
    <dd>Andrew W.K.</dd>
    <dd>Apparat</dd>
  </dl>
  <dl>
    <dt>C</dt>
    <dd>Chromeo</dd>
    <dd>Common</dd>
    <dd>Converge</dd>
  </dl>
</div>
```

CSS

```css
dt {
  position: sticky;
  top: 0;
}
```

效果

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/82bfd0f2b1dc4d7f9bce9f48f277a381~tplv-k3u1fbpfcp-watermark.image)

## 6. [conic-gradient](<https://developer.mozilla.org/en-US/docs/Web/CSS/conic-gradient()>)

**conic-gradient()** 函数可用于创建锥形渐变, 最常用的场景是创建饼图。

如下代码

```css
.wrapper {
  width: 400px;
  height: 400px;
  border-radius: 50%;
  background-image: conic-gradient(
    #001133 0 15%,
    #aa0044 0 40%,
    #ddaa11 0 85%,
    #2da132 0 100%
  );
}
```

效果

![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/66bc017d082e4e56b27d83f6dceeb636~tplv-k3u1fbpfcp-watermark.image)

与其类似用法的还有径向渐变 [radial-gradient](<https://developer.mozilla.org/en-US/docs/Web/CSS/radial-gradient()>)

```css
width: 400px;
height: 400px;
border-radius: 50%;
background-image: radial-gradient(
  #001133 0 15%,
  #aa0044 0 40%,
  #ddaa11 0 56%,
  #208f25 0 100%
);
```

![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fe04c600c30d4e3f8fde65a0d793466a~tplv-k3u1fbpfcp-watermark.image)

## 7. [transform-origin](https://developer.mozilla.org/en-US/docs/Web/CSS/transform-origin)

**transform-origin** 属性可以设定元素旋转的基准点。
默认情况，会基于元素的中心点旋转

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9ee961a9ecbb46b6b33a6faa3ac12161~tplv-k3u1fbpfcp-watermark.image)

改变旋转点的位置后的效果

```css
.wrapper div {
  transform-origin: 50% 100%;
}
```

![](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/00a62f5ae0c84067ac56e507fc6159c0~tplv-k3u1fbpfcp-watermark.image)

## 8. [shape-outside](https://developer.mozilla.org/zh-CN/docs/Web/CSS/shape-outside)

**shape-outshide** 属性可以定义一个任意形状，并使其相邻的内容围绕在这个形状的周围布局。

HTML

```html
<div class="main">
  <div class="circle"></div>
  <p>
    Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Phasellus
    hendrerit. Pellentesque aliquet nibh nec urna. In nisi neque, aliquet vel,
    dapibus id, mattis vel, nisi. Sed pretium, ligula sollicitudin laoreet
  </p>
</div>
```

CSS

```css
.circle {
  shape-outside: circle(50%);
  width: 200px;
  height: 200px;
  float: right;
}

p {
  text-align: center;
}
```

当调整 circle 函数的参数时，效果如下：

![](https://p9-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/bcede3b746ed4f3d860dacab0441ebf7~tplv-k3u1fbpfcp-watermark.image)

除此之外，还可以使用 [ellipse()](<https://developer.mozilla.org/en-US/docs/Web/CSS/basic-shape#ellipse()>) 绘制椭圆形， [polygon()](<https://developer.mozilla.org/en-US/docs/Web/CSS/basic-shape#polygon()>) 绘制多边形等。

> 这个属性不支持 IE。

## 9. [mask-image](https://developer.mozilla.org/en-US/docs/Web/CSS/mask-image)

**mask-image** 属性可以为某个元素设置遮罩层。

HTML

```html
<div id="masked"></div>
```

CSS

```css
#masked {
  width: 100px;
  height: 100px;
  background-color: #8cffa0;
  -webkit-mask-image: url(https://media.prod.mdn.mozit.cloud/attachments/2016/03/03/12676/cef7251f571b727c87a4613cfb347bbc/star.svg);
  mask-image: url(https://media.prod.mdn.mozit.cloud/attachments/2016/03/03/12676/cef7251f571b727c87a4613cfb347bbc/star.svg);
}
```

效果

![](https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/ab201b8eb09b47ca9b73c16bcd730c2f~tplv-k3u1fbpfcp-watermark.image)

遮罩层可以是一张图片，通过 [url()](<https://developer.mozilla.org/en-US/docs/Web/CSS/url()>) 或者 [image()](https://developer.mozilla.org/en-US/docs/Web/CSS/image) 来指定，也可以是一个渐变的图层, 通过 [linear-gradient()](<https://developer.mozilla.org/en-US/docs/Web/CSS/linear-gradient()>) 或者 [radial-gradient()](<https://developer.mozilla.org/en-US/docs/Web/CSS/radial-gradient()>) 来实现。

> 这个属性不支持 IE。

## 10. [mix-blend-mode](https://developer.mozilla.org/en-US/docs/Web/CSS/mix-blend-mode)

**mix-blend-mode** 属性描述了元素的内容应该与其父元素的内容及元素的背景如何混合显示。

HTML

```html
<div class="blend">
  <img
    src="https://cdn.pixabay.com/photo/2016/12/11/12/02/bled-1899264_960_720.jpg"
  />
  <h1>NATURE</h1>
</div>
```

CSS

```css
.blend img {
  position: absolute;
  height: 300px;
}

.blend h1 {
  position: absolute;
  mix-blend-mode: overlay;
}
```

效果

![](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/53f630ca14b64947ad195e6a05b7fd47~tplv-k3u1fbpfcp-watermark.image)

css 内置了多种混合模式[\<blend-mode>](https://developer.mozilla.org/zh-CN/docs/Web/CSS/blend-mode)可供选择。

> 这个属性不支持 IE。
