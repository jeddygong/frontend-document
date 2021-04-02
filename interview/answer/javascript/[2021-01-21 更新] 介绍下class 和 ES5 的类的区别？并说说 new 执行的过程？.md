### 前言

	* ES5中主要通过构造函数方式和原型方式来定义一个类（Function）；
	* ES6中通过class类来定义类，类声明创建一个基于原型继承的具有给定名称的新类；



### 区别

	* class类声明不可以提升；
	* class类声明不允许再次声明已经存在的类，否则将会抛出一个类型错误；
	* class内部是严格模式，构造函数是可选的；
	* class 的静态方法或者原型方法都不可枚举（custructor中的属性会枚举到），且这些方法都没有原型，不可被new；
	* class 必须使用new来调用，不能直接执行；
	* class 内部无法重写类名



### 代码示例

```javascript
/**
 *ES6的类
**/
const bar = Symbol('bar');
const snaf = Symbol('snaf');
class Parent {
    constructor(a) {
        this.a = a;
        this.printName = this.printName.bind(this)
    }
    print() {
        console.log('parent')
    }
    printName(name = 'there') {
        this.print(`Hello ${name}`);
    }
    // 公有方法
    foo(baz) {
        this[bar](baz);
    }
    // 私有方法
    [bar](baz) {//[bar]用方括号代表从表达式获取的属性名
        return this[snaf] = baz;
    }

}
```

* Parent中定义的方法不可用`Object.keys(Point.prototype)`枚举到;
* 重复定义Parent class会报错;
* 可通过实例的proto属性向原型添加方法；
* 没有私有方法和私有属性用symbol模拟；
* class静 态方法与静态属性：
  * class定义的静态方法前加static关键字
  * 只能通过类名调用0不能通过实例调用
  * 可与实例方法重名
  * 静态方法中的this指向类而非实例；
  * 静态方法可被继承
  * 在子类中可通过super方法调用父类的静态方法
  * class内部没有静态属性，只能在外面通过类名定义。
* `new target`属性指向当前的构造函数,不能在构造函数外部调用会报错

### 等同于es5的：

```javascript
function Parent () {}
Parent.prototype = {
    constructor() { },
    print() { },
}
```

* function构造 器原型方法可被`Object.keys(Point.prototype)`枚举到, constructor除外；
* 重复定义Parent function，之前的会被覆盖掉
* 可通过实例的proto属性向原型添加方法；
* 没有私有属性；

> 所有原型方法属性都可用Object.getOwnPropertyNames(Point.prototype)访问到



### 关于New

 * 每次使用new关键字会执行的步骤：

   1. 创建一个空的新对象，作为将要返回的对象实例；

      ​	var obj = {};

   2. 将该对象的_proto__(隐式原型)指向创建该对象的类的原型对象; ( 注意proto前后是双下划线)

      ​	// 假设类叫做 A
      　obj._proto__ = A.prototype；

   3. 将构造函数环境中的this，指向该对象；

       相当于：this = obj；// 意识到位，代码这样写是错误的

   4. 执行构造函数中的代码，并返回刚刚创建的新对象；

> 注意：class 定义的类，必须使用new关键字调用，不然会报错，
>
> ​			new关键字总是返回一个对象，如果new 普通函数，会返回一个空对象。



### 关于构造函数constructor

	* constructor方法是类的默认方法，通过new命令生成对象实例时，自动调用该方法。
	* 在类中必须存在构造函数，可以不书写，会默认补一个空构造constructor{}。