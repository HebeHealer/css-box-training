# css-box-training
css box model training

```
谈谈对css盒模型的认识？
1、基本概念： 标准模型 + IE模型
2、标准模型和IE模型的区别
3、CSS是如何设置这两种模型的
4、JS如何设置获取盒模型对应的宽和高
5、实例题（根据盒模型解释边距重叠）
6、BFC（边距重叠解决方案）

标准模型与IE模型的区别： 指宽度和高度计算方式不同。

IE模型： 宽度和高度计算包含border padding；

CSS如何设置这两种模型
box-sizing: content-box; (浏览器默认， 即标准模型)
box-sizing: border-box;

JS如何设置获取盒模型对应的宽和高？
dom.style.width/height
dom.currentStyle.width/height (获取浏览器即时运行渲染后的宽高，只有IE支持)
window.getComputedStyle(dom).width/height（同第2点，兼容性更好些）
dom.getBoundingClientReact().width/height （计算元素的绝对位置，相比于左上角位置）

实例题（根据盒模型解释边距重叠）


当标准盒模型时，父容器高度为100
当IE模型时，父容器为110

overflow: hidden;  父子元素边距重叠，兄弟元素重叠，取两者的最大值
为父级元素创建BFC

BFC解决边距重叠问题

BFC基本概念
IFC基本概念
BFC的原理（BFC的渲染规则）
      1. BFC这个元素的垂直方向边距会发生重叠
      2. BFC区域不会与浮动元素的box重叠
      3. BFC是一个独立的元素，里外元素互不影响
      4. BFC计算高度时，浮动元素也会参与计算
如何创建BFC
      1. overflow不为visible； 
      2. float不为none；
      3. position的值不是relative或static；
      4. display为table相关；


```

BFC的使用场景
1、垂直方向上计算父容器的高度
```
<section class="vertical-container">
        <p>1</p>
        <div class="bfc">
            <p>2</p>
        </div>
        <p>3</p>
    </section>
```

```
.vertical-container .bfc {
  overflow: hidden;
}

.vertical-container p {
  margin: 5px auto 25px;
  background-color: red;
}
```
2、BFC不与float重叠
```
<section class="horizontal-container">
        <div class="left"></div>
        <div class="right"></div>
    </section>
```
```
.horizontal-container {
    background-color: yellow;
}

.horizontal-container .left{
    float: left;
    width: 100px;
    height: 100px;
    background-color: #090;
}

.horizontal-container .right{
    height: 120px;
    background-color: #ccc;
    overflow: auto;
}
```
3、水平方向上清除浮动
```
<section class="float-container">
        <div class="float">balabalabala  BFC子元素是float也会参与计算， 清除浮动，对父元素创建BFC</div>
    </section>
```
```
.float-container {
    overflow: auto;
    /* float: left */
    background-color: red;
}

.float-container .float {
    float: left;
    font-size: 30px;
}
```
