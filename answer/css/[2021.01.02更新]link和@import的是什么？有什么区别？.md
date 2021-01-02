### link: 链接样式

​	链接方式指的是使用HTML头部的标签引入外部的CSS文件

```html
<head>
	<link rel="stylesheet" type="text/css" href="./index.css">
</head>
```



### @import 导入样式

导入方式指的是使用CSS规则引入外部CSS文件

```html
<style>
	@import url(index.css);
</style>
```

或者在css样式中

```css
@import url(index.css);
body {
  margin: 0;
  padding: 0;
}
```



### 区别

1. link是XHTML标签，除了加载CSS外，还可以定义RSS等其他事物；@import属于CSS范畴，只能加载CSS；
2. link引用CSS时，在页面载入时同时加载；@import需要页面网页完全载入以后加载。所以会出现一开始没有CSS样式，闪烁一下出现样式后的页面（网速慢的情况下）
3. link是XHTML标签，无兼容性问题；@import是在CSS2.1提出来的，所以低版本浏览器支持性不友好；
4. link支持使用Javascript控制DOM去改变样式；而@import不支持；