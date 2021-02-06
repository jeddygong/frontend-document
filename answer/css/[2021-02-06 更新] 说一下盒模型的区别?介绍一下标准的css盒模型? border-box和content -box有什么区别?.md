### 盒模型

​	盒模型是css中的一种基础设计模式，web页面中的所有元素都可以当做一个盒模型，每一个盒模型都是由display, position，float， width, height， margin， padding 和border等属性组合所构成的，不同类型的盒模型会有不一样 的布局，css中 主要有inline, inline- -block, block, table, absolute position, float等类型。

#### 1.1 W3C标准模型和IE的传统模型(IE6以下)

​	css中的盒模型有两种: W3C标准模型和IE的传统模型，相 同之处是都是对web中元素计算尺寸的模型，不同之 处在于两者的计算方式不同。

​	w3c盒子模型的范围包括margin、border、padding、content,并且content部分不包含其他部分，IE盒子模型的 范围包括margin、border、 padding、 content,和w3c盒 子模型不同的是，IE盒子模型的content部分包含了padding和border



#### 1.2 W3C标准模型中元素尺寸的计算方式

		*  **height(空间高度) = 内容高度 + 内距 + 边框 + 外距 (height为内容高度)**
		*  **width(空间宽度) = 内容宽度 + 内距 + 边框 + 外距 (width为内容宽度)**



#### 1.3 IE的传统模型中元素尺寸的计算方式

	* **height(空间高度) = 内容高度 + 外距 (height包含了元素内容高度，边框，内距)**
	* **width(空间宽度) = 内容宽度 + 外距 (width包含 了元素内容宽度，边框，内距)**



#### 1.4 代码实例

```javascript
.box{
    border:20px solid;
    padding:30px;
    margin:30px;
    background:red;
    width:300px;
}
/* 标准模型 空间宽度 = 300 + 20*2 + 30*2 + 30*2  */
/* IE的传统模型 空间宽度  = 300 + 30*2  */
/* IE的传统模型中的width是包括了padding和border的，而标准模型不包括，不管padding和borde加多少内容区域的宽度不会改变。 */
```



#### 1.5 border-box & content- -box

	##### 1.5.1 content- -box

​	默认值，其让元素维持W3C的标准盒模型，也就是说元素的宽度和高度(width/height)等于元素边框宽度 (border)加上元素内距(padding) 加. 上元素内容宽度或 高度( content width/ height )， 也 就是element width/height = border + padding + content width /height

##### 1.5.2 border-box

​	重新定义CSS2.1中盒模型组成的模式，让元素维持IE传统的 盒模型(IE6以下版本和IE6- -7怪异模式)，也就是说元素的宽度或高度等于元素内容的宽度或高度。从上面盒模型介绍可知，这里的内容宽度或高度包含了元素的borderpadding、内容的宽度或高度(此处的内容宽度或高度=盒 子的宽度或高度一边框一-内距) 。

​	

#### Css设置标准模型和IE模型

* 标准盒模型: `box-sizing: content-box`
* IE传统盒模型: `box-sizing: border-box`

