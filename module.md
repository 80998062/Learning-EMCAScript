## 模块

作用:

* 可维护性：根据定义，每个模块都是独立的。良好设计的模块会尽量与外部的代码撇清关系，以便于独立对其进行改进和维护。维护一个独立的模块比起一团凌乱的代码来说要轻松很多。

* 命名空间：在JavaScript中，最高级别的函数外定义的变量都是全局变量（这意味着所有人都可以访问到它们）。也正因如此，当一些无关的代码碰巧使用到同名变量的时候，我们就会遇到“命名空间污染”的问题。

* 可复用性：现实来讲，在日常工作中我们经常会复制自己之前写过的代码到新项目中。





> 在JavaScript中，函数是创建作用域的唯一方式。



### 模块模式

模块模式一般用来模拟类的概念（因为原生JavaScript并不支持类，虽然最新的ES6里引入了`Class`不过还不普及）这样我们就能把公有和私有方法还有变量存储在一个对象中——这就和我们在**Java**或**Python**里使用类的感觉一样。这样我们就能在公开调用API的同时，仍然在一个闭包范围内封装私有变量和方法。







