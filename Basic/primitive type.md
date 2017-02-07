* 原始值

存储在栈（**stack**）中的简单数据段，也就是说，它们的值直接存储在变量访问的位置。

ECMAScript 有 5 种原始类型（**primitive** **type**），即 **Undefined**、**Null**、**Boolean**、**Number** 和 **String**。

* typeof 运算符

如果变量是引用类型或者是Null类型 返回object

> 注释：您也许会问，为什么 typeof 运算符对于 null 值会返回 "Object"。这实际上是 JavaScript 最初实现中的一个错误，然后被 ECMAScript 沿用了。现在，null 被认为是对象的占位符，从而解释了这一矛盾，但从技术上来说，它仍然是原始值。



* undefined

变量未初始化时,就是undefined



* 引用值

存储在堆（**heap**）中的对象，也就是说，存储在变量处的值是一个指针（**point**），指向存储对象的内存处。



  
  






