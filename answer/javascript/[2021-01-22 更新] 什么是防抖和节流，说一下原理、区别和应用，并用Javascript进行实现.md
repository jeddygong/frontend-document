### 防抖 & 节流

	#### 一、防抖

 * **原理：**在事件被触发n秒后再执行回调，如果在这n秒内又被触发，则重新计时。

 * **适用场景:**

   	* 按钮提交场景：防止多次提交按钮，只执行最后提交的一次；
   	* 搜索框联想场景：防止联想发送请求，只发送最后一次输入；

* **简易版实现**

  ```javascript
  function debounce(func, wait) {
      let timeout;
      return function () {
          const context = this;
          const args = arguments;
          clearTimeout(timeout)
          timeout = setTimeout(function(){
              func.apply(context, args)
          }, wait);
      }
  }
  ```

* **立即执行版本实现**

  * 有时希望立刻执行函数，然后等到停止触发 n 秒后，才可以重新触发执行

  ```javascript
  // 有时希望立刻执行函数，然后等到停止触发 n 秒后，才可以重新触发执行。
  function debounce(func, wait, immediate) {
    let timeout;
    return function () {
      const context = this;
      const args = arguments;
      if (timeout) clearTimeout(timeout);
      if (immediate) {
        const callNow = !timeout;
        timeout = setTimeout(function () {
          timeout = null;
        }, wait)
        if (callNow) func.apply(context, args)
      } else {
        timeout = setTimeout(function () {
          func.apply(context, args)
        }, wait);
      }
    }
  }
  ```

* **返回值版实现**

  * func函数可能会有返回值，所以需要返回函数结果，但是当 immediate 为 false 的时候, 因为使用了 setTimeout , 我们将

    func. apply(context, args)的返回值赋给变量，最后再 return 的时候, 值将会一直是undefned，所以只在 immediate 为true的时候返回函数的执行结果。

  ```javascript
  	function debounce(func, wait, immediate) {
    let timeout, result;
    return function () {
      const context = this;
      const args = arguments;
      if (timeout) clearTimeout(timeout);
      if (immediate) {
        const callNow = !timeout;
        timeout = setTimeout(function () {
          timeout = null;
        }, wait)
        if (callNow) result = func.apply(context, args)
      }
      else {
        timeout = setTimeout(function () {
          func.apply(context, args)
        }, wait);
      }
      return result;
    }
  }	
  ```

#### 二、节流

 * **原理：**规定在一个单位时间内，只能触发一次函数。如果这个单位时间内触发多次函数，只有一次生效。

 * **适用场景：**

   	* **拖拽场景：**固定时间内只执行一-次，防止超高频次触发位置变动；
   	* **缩放场景：**监控浏览器resize；
   	* **动画场景：**避免短时间内多次触发动画引起性能问题；

* **使用时间戳实现**

  * 使用时间戳，当触发事件的时候，我们取出当前的时间戳，然后减去之前的时间戳(最一开始值设为0 ),如果大于设置的时间周期，就执行函数，然后更新时间戳为当前的时间戳，如果小于，就不执行。

    ```javascript
    function throttle(func, wait) {
      let context, args;
      let previous = 0;
    
      return function () {
        let now = +new Date();
        context = this;
        args = arguments;
        if (now - previous > wait) {
          func.apply(context, args);
          previous = now;
        }
      }
    }
    ```

* **使用定时器实现**

  * 当触发 事件的时候，我们设置一个定时器，再触发事件的时候，如果定时器存在，就不执行，直到定时器执行，然后执行函数，清空定时器，这样就可以设置下个定时器。

    ```javascript
    function throttle(func, wait) {
      let timeout;
      return function () {
        const context = this;
        const args = arguments;
        if (!timeout) {
          timeout = setTimeout(function () {
            timeout = null;
            func.apply(context, args)
          }, wait)
        }
    
      }
    }
    ```

    