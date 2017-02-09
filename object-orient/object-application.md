## 对象应用

**对象的创建和销毁都在 JavaScript 执行过程中发生，理解这种范式的含义对理解整个语言至关重要。**

  


### 回收机制

无用存储单元收集程序: **garbage collection routine**

废除: **dereference**

把对象的所有引用都设置为 null，可以强制性地废除对象。

举个🌰:

```js
var oObject = new Object;
// do something with the object here
oObject = null;
```



早绑定: early binding

在实例化对象之前就定义它的属性和方法

> ECMAScript不是强类型语言,所以不支持



晚绑定: late binding

> ECMAScript所有变量都采用晚绑定方法



