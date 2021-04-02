### 主要技术有：

> 目前流行的js模块化规范有CommonJS、AMD、CMD以及ES6的模块系统。



### 一、CommonJS

​	**CommonJS的出发点:** JS没有完善的模块系统，标准库较少，缺少包管理工具。伴随着NodeJS的兴起，能让JS在任何地方运行，特别是服务端，也达到了具备开发大型项目的能力，所以CommonJS营运而生。

​	`Node.js`是`commonJS`规范的主要实践者，它有四个重要的环境变量为模块化的实现提供支 持: `module` 、`exports` 、require 、`global`。 实际使用时，用`module.exports`定义当前模块对外输出 的接口(不推荐直接用`exports` )，用require加载模块。

​	`commonJS`用同步的方式加载模块。在服务端，模块文件都存在本地磁盘，读取非常快，所以这样做不会有问题。但是在浏览器端，限于网络原因，更合理的方案是使用异步加载。

	* 暴露模块: **module.exports = value 或exports.xxx = value**
	* 引入模块: **require(xxx)**

#### CommonJS规范

* 一个文件就是一个模块，拥有单独的作用域；
* 普通方式定义的变量、函数、对象都属于该模块内；
* 通过require来加载模块
* 通过exports和module.exports来 暴露块中的内容

#### 注意

1. 当exports和module.exports同时存 在时,module.exports会覆羊exports;
2. 当模块内全是exports时，就等同于module.exports;
3. exports就 是module.exports的子集;
4. 所有代码都运行在模块作用域，不会污染全局作用域；
5. 模块可以多次加载，但只会在第一次加载时候运行,然后运行结果就被缓存了，以后再加载，就直接读取缓存结果；
6. 模块加载顺序，按照代码出现的顺序同步加载；
7. _ _dirname代表 当前文件所在的文件夹路径；
8. _ flename代表 当前模块文件所在的文件夹路径+文件名



### 二、ES6模块化

​	ES6在语言标准的层面上，实现了模块功能，而且实现得相当简单，旨在成为浏览器和服务器通用的模块解决方案。 其模块功能主要由两个命令构成: `export` 和`import`。`export`命令用于规定模块的对外接口，`import`命令用于输入其他模块提供的功能。

​	其实ES6还提供了`export default` 命令，为模块指定默认输出，对应的`import`语句不需要使用大括号。这也更趋近于AMD的引用写法。

​	ES6的模块不是对象，`import` 命令会被JavaScript引擎静态分析，在编译时就引入模块代码，而不是在代码运行时加载，所以无法实现条件加载。也正因为这个，使得静态分析成为可能。



#### export

​	export可以导出的是一个对象中包含的多个属性、方法。 export default只能导出一个可以不具名的函数。我们可以通过import进行引用。同时，我们也可以直接使用require使用，原因是webpack起了server相关。

#### import

1. import {fn} from './xxx/xxx' ( export导出方式的引用方式)；
2. import fn from './ xxx/xxx1' ( export default导出方式的引用方式)



### 三、AMD

​	Asynchronous Module Defnition,异步加载模块。它是一个在浏览器端模块化开发的规范，不是原生js的规范，使用AMD规范进行页面开发需要用到对应的函数库，RequireJS。

​	AMD规范采用异步方式加载模块，模块的加载不影响它后面语句的运行。所有依赖这个模块的语句，都定义在一个回调函数中，等到加载完成之后，这个回调函数才会运行。

​	使用require.js 实现AMD 规范的模块化: 用require. config()指定引用路径等，用define()定义模块，用require()加载模块。

```javascript
// 定义模块
define('moduleName', ['a', 'b'] , function(ma, mb){
  return someExpor tValue;
})

// 引入模块
require( ['a','b'], function(ma ,mb){
	/ *code*/
})
```

#### RequireJS主要解决的问题

* 文件可能有依赖关系，被依赖的文件需要早于依赖它的文件加载到浏览器；
* js加载的时候浏览器会停止页面渲染，加载文件愈多，页面相应事件就越长；
* 异步前置加载；

#### 语法

​	`define ( id, dependencies, factory)`

	*  id可选参数，用来定义模块的标识，如果没有提供该参数，脚本文件名(去掉拓展名)
	*  dependencies 是一个当前模块用来的模块名称数组
	*  factory工厂方法，模块初始化要执行的函数或对象，如果为函数，它应该只被执行一次，如果是对象，此对象应该为模块的输出值。

### 四、CMD

​	CMD是另一种js模块化方案，它与AMD很类似，不同点在 于: **AMD推崇依赖前置、提前执行，CMD推崇依赖就近、延迟执行**。此规范其实是在sea.js推广过程中产生的。

​	因为CMD推崇-一个文件一个模块，所以经常就用文件名作 为模块id; CMD推 崇依赖就近，所以-般不在defne的参 数中写依赖，而是在factory中写 。

​	`define(id, deps, factory)`

​	factory有三个参数: `function ( require, exports, module ) {}`

 * require: require是factory函数的第-个参数,require是一个方法，接受模块标识作为唯一参数，用来获取其他模块提供的接口;

 * exports exports是一个对象，用来向外提供模块接口;

 * module module是一个对象，上面存储了与当前模块相关联的一-些属性和方法。

   ```javascript
   
   // 定义没有依赖的模块
   define(function(require,exports,module){
     exports.xxx = vaule;
     module.exports = value;
   })
   
   //定义有依赖的模块
   define(function(require,exports,module){
     //同步引入模块
     var module1 = require("./module1.js");
     //异步引入模块
     require.async("./module2.js",function(m2){
       /***/
     })
     //暴露接口
     exports.xxx = value;
   })
   
   //引入模块
   define(function(require){
     const m1 = require("./module1.js");
     m1.show();
   })
   ```

   

### 五、UMD 通用规范

​	一种整合了CommonJS和AMD规范的方法，希望能解决跨平台模块方案。

> 运行原理

	* UMD先判断是否支持Node.js的模块(exports) 是 否存在，存在则使用Nnde.js模块模式；
	* 再判断是否支持AMD（define是否存在），存在则使用AMD方式加载模块；

```javascript
(function (window, factory) {
    if (typeof exports === 'object') {  
        module.exports = factory();
    } else if (typeof define === 'function' && define.amd) {
        define(factory);
    } else {    
        window.eventUtil = factory();
    }
})(this, function () {
    //module ...
});
```



### 六、总结

​	**commonjs**是同步加载的。主要是在nodejs也就是服务端 应用的模块化机制，通过`module. export`导出声明， 通过`require('')` 加载。每个文件都是一个模块。他有自己的作用域，文件内的变量，属性函数等不能被外界访问。node会将模块缓存，第二次加载会直接在缓存中获取。

​	**AMD**是异步加载的。主要应用在浏览器环境下。requireJS 是遵循AMD规范的模块化工具。他是通过`define()` 定 义声明，通过`require('' , function(){})`加载。

​	**ES6的模块化**加载时通过 `export default` 导出,用`import`导入可通过{}对导出的内容进行解构。

​	ES6的模块的运行机制与common不一样，js引擎对脚本静态分析的时候，遇到模块加载指令后会生成一个只读引用,等到脚本真正执行的时候才会通过弓|用去模块中获取值，在引用到执行的过程中模块中的值发生了变化，导入的这里也会跟着变，ES6模块是动态引用，并不会缓存值，模块里总是绑定其所在的模块。