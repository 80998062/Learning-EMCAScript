## 对象类型

**在 ECMAScript 中，所有对象并非同等创建的。**

**一般来说，可以创建并使用的对象有三种：本地对象、内置对象和宿主对象。**



## 本地对象

独立于宿主环境的 ECMAScript 实现提供的对象:

```js
Object
Function
Array
String
Boolean
Number
Date
RegExp
Error
EvalError
RangeError
ReferenceError
SyntaxError
TypeError
URIError
```

## 内置对象

由 ECMAScript 实现提供的、独立于宿主环境的所有对象，在 ECMAScript 程序开始执行时出现

ECMA-262 只定义了两个内置对象:

* Global
* Math

## 宿主对象

所有非本地对象都是宿主对象（host object），即由 ECMAScript 实现的宿主环境提供的对象。

所有 BOM 和 DOM 对象都是宿主对象。

