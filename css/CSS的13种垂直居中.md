

# 11种锤爆面试官的 CSS 垂直居中

![web-css-gaoji-jichu](../../../../Downloads/web-css-gaoji-jichu.jpeg)



## 前言之锤爆面试官工具神器 - CSS

&#8195;&#8195; 无论是实际开发中，亦或者是求职面试中，css 垂直居中往往都是一个绕不开的话题，其中不乏有许多面试者在多次双重尝受打击之后，而没有一个很好的反击点，刚好结合自己以前受的委屈和痛苦，来给大家一个锤爆面试官大佬们的机会。



&#8195;&#8195; 其实垂直居中主要分为了两种类型：**居中元素宽高已知** 和 **居中元素宽高未知**，那么我们就结合这两种类型来一一做举例。

&#8195;&#8195; 	![css 垂直居中](../../../../Downloads/css 垂直居中.png)





## 居中元素宽高已知



### 1. absolute + margin auto

顾名思义，就是利用当前元素的 `position: absolute;` 和 `margin: auto;`

注意使用此方法：父元素与当前元素的高度要设置；

通过将各个方向的距离都设置为 0，此时将 `margin` 设置为 `auto`，就可以实现垂直居中显示了；

#### 具体代码如下：

```css
.parent{
  position: relative;
  width: 90vw;
  height: 90vh;
  border: 3px solid steelblue;
}

.child{
  background: tomato;
  width: 50vw; height: 50vh;
  /* 核心代码 */
  position:absolute;
  top: 0; bottom: 0; left: 0; right: 0;
  margin: auto;
}

```

#### 

#### 具体效果如下：

![image-20210729232149048](../../../../Library/Application Support/typora-user-images/image-20210729232149048.png)



### 2. absolute + 负 margin 

利用绝对定位百分比 50% 来实现，因为当前元素的百分比是基于相对定位（也就是父元素）来定位的;

然后再用负的 margin-top 和 margin-left 来进行简单的位移即可，因为现在的负 margin 是基于自身的高度和宽度来进行位移的。

#### 具体代码如下：

```css
.parent{
  position:relative;
  width: 90vw;
  height: 90vh;
  border: 3px solid steelblue;
}

.child{
  background: tomato;
  width: 100px; height: 100px;
  /* 核心代码 */
  position:absolute;
  top: 50%; left: 50%;
  margin-top: -50px;
  margin-left: -50px;
}

```



#### 具体效果如下：

![image-20210729232317142](../../../../Library/Application Support/typora-user-images/image-20210729232317142.png)



### 3. absolute + calc

使用 CSS3 的一个计算函数来进行计算即可；方法与上面类似

#### 具体代码如下：

```css
.parent{
  width: 90vw;
  height: 90vh;
  border: 3px solid steelblue;
  /* 核心代码 */
  position:relative;
}

.child{
  background: tomato;
  width: 200px; height: 200px;
  /* 核心代码 */
  position:absolute;
  top: calc(50% - 100px);
  left: calc(50% - 100px);
}

```



#### 具体效果如下：

![image-20210729232434257](../../../../Library/Application Support/typora-user-images/image-20210729232434257.png)



## 居中元素宽高未知



### 4. absolute + transform

利用 CSS3 的新特性 `transform`；因为 `transform` 的 `translate` 属性值如果是一个百分比，那么这个百分比将是基于自身的宽高计算出来的。

#### 具体代码如下：

```css
.parent{
  width: 90vw;
  height: 90vh;
  border: 3px solid steelblue;
  /* 核心代码 */
  position:relative;
}

.child{
  background: tomato;
  /* 核心代码 */
  position:absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
}
```



#### 具体效果如下：

![image-20210729232624466](../../../../Library/Application Support/typora-user-images/image-20210729232624466.png)



### 5. line-height + vertical-align

把当前元素设置为行内元素，然后通过设置父元素的` text-align: center;` 实现水平居中；

同时通过设置当前元素的 `vertical-align: middle;` 来实现垂直居中；

最后设置当前元素的 `line-height: initial;` 来继承父元素的`line-height`。

#### 具体代码如下：

```css
.parent{
  width: 90vw;
  border: 3px solid steelblue;
  /* 核心代码 */
  line-height: 500px;
  text-align: center;
}

.child{
  background: tomato;
  /* 核心代码 */
  display: inline-block;
  vertical-align: middle;
  line-height: initial;
}
```



#### 具体效果如下：

![image-20210729232748854](../../../../Library/Application Support/typora-user-images/image-20210729232748854.png)



## 6. table 表格元素

通过最经典的 table 元素来进行水平垂直居中，不过代码看起来会很冗余，不推荐使用；

#### 具体代码如下：

```html
<table>
  <tbody>
    <tr>
      <td class="parent">
        <div class="child"></div>
      </td>
    </tr>
  </tbody>
</table>

<style>
  .parent {
    width: 90vw;
    height: 90vh;
    border: 3px solid steelblue;
    /* 核心代码 */
    text-align: center;
  }
  .child {
    background: tomato;
    /* 核心代码 */
    display: inline-block;
  }
</style>
```



#### 具体效果如下：

![image-20210729233002861](../../../../Library/Application Support/typora-user-images/image-20210729233002861.png)



### 7. css-table 表格样式

如果一定要使用 `table` 的特性，但是不想写 `table` 元素的话，那么`css-table` 就很适合你；

#### 具体代码如下：

```css
.parent{
  width: 90vw;
  height: 90vh;
  border: 3px solid steelblue;
  /* 核心代码 */
  display: table-cell;
  text-align: center;
  vertical-align: middle;
}

.child{
  background: tomato;
  /* 核心代码 */
  display: inline-block;
}
```



#### 具体效果如下：

![image-20210729233055305](../../../../Library/Application Support/typora-user-images/image-20210729233055305.png)



### 8. flex 布局（一）

要说现在较为流行和使用较多的布局方案，那么非 flex 莫属了，那么举例两个最常见的使用方式 ~

直接在 `flex-container` 上通过几行代码即可很优雅的实现

#### 具体代码如下：

```css
.parent {
  width: 90vw;
  height: 90vh;
  border: 3px solid steelblue;
  
  /* 核心代码 */
  display: flex;
  justify-content: center;
	align-items: center;
}
.child{
  background: tomato;
}
```

`justify-content` 表示：设置或检索弹性盒子元素在主轴（横轴）方向上的对齐方式；

`align-items` 表示：定义 flex 子项在 flex 容器的当前行的侧轴（纵轴）方向上的对齐方式。



#### 具体效果如下：

![image-20210729233155581](../../../../Library/Application Support/typora-user-images/image-20210729233155581.png)



### 9. flex + margin auto（二）

在  `flex-item` 上更加优雅的实现

#### 具体代码如下：

```css
.parent{
  width: 90vw;
  height: 90vh;
  border: 3px solid steelblue;
  
  /* 核心代码 */
  display: flex;
}

.child{
  background: tomato;
  
  /* 核心代码 */
  margin: auto;
}
```



#### 具体效果如下：

![image-20210729233243684](../../../../Library/Application Support/typora-user-images/image-20210729233243684.png)



> *** flex 的两种方法使用取舍，任凭您意 ***



#### 附赠 flex 兼容性图片一张

![image-20210725020146492](../../../../Library/Application Support/typora-user-images/image-20210725020146492.png)



### 10. grid 网格布局 (一)

grid 布局相信大家在实际项目中用的较少，主要是该布局实在是太超前，导致了兼容性不是那么理想，但是不可否认的是 grid 的能力在 css 布局中绝对是一个质的飞越。

不熟悉的可以看下阮一峰老师的详细[入门教程](https://www.ruanyifeng.com/blog/2019/03/grid-layout-tutorial.html)

`CSS Grid` 包含与 `Flexbox` 几乎相同的对齐选项，因此我们可以在 `grid-container` 上优雅的实现

#### 具体代码如下：

```css
.parent{
  width: 90vw;
  height: 90vh;
  border: 3px solid steelblue;
  /* 核心代码 */
  display: grid;
  align-items: center;
  justify-content: center;
}

.child{
  background: tomato;  
}
```



#### 具体效果如下：

![image-20210729233416689](../../../../Library/Application Support/typora-user-images/image-20210729233416689.png)



### 11. grid 网格布局 (二)

同样我们可以像 `Flexbox` 一样，在  `grid-item` 上优雅的实现



#### 具体代码如下：

```css
.parent{
  width: 90vw;
  height: 90vh;
  border: 3px solid steelblue;
  /* 核心代码 */
  display: grid
}

.child{
  background: tomato;
  /* 核心代码 */
  align-self: center;
  justify-self: center;
}
```



#### 具体效果如下：

![image-20210729233458535](../../../../Library/Application Support/typora-user-images/image-20210729233458535.png)



> *** flex 的两种方法使用取舍，任凭您高兴 ***



#### 附赠 grid 兼容性图片一张

![image-20210725020025034](../../../../Library/Application Support/typora-user-images/image-20210725020025034.png)



## 总结

在学习了上面的 11 种垂直居中布局方法后，我们简单概括一下

* 如果你的项目**在 PC 端有兼容性要求**并且**宽高固定**，推荐使用 `absolute + 负 margin`  方法实现；
* 如果你的项目**在 PC 端有兼容性要求**并且**宽高不固定**，推荐使用 `css-table` 方式实现；
* 如果你的项目**在 PC 端无兼容性要求** ，推荐使用 `flex` 实现居中，当然不考虑 IE 的话，`grid` 也是个不错的选择；
* 如果你的项目**在移动端使用** ，那么推荐你使用 `flex` ，`grid` 也可作为备选。



## 写在最后

&emsp; &#8195; 其实以上的是一种垂直居中方法，只是比较常见的，其实还有一些比较冷门的方式方法，例如 **伪类元素**、**grid-container 的 grid-template-rows** 等，大家下去可以自行尝试一下 ~

&#8195;&#8195; 明天周六，**庆幸** 的是还要赶早搬砖，祝大家有一个好的周末，晚安 ~

&#8195;&#8195; 帅气美丽的你给个赞呗再走呗 ~





