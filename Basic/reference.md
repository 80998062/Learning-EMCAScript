引用类型通常叫做类（**class**），也就是说，遇到引用值，所处理的就是对象。

> 注意：从传统意义上来说，ECMAScript 并不真正具有类。事实上，除了说明不存在类，在 ECMA-262 中根本没有出现“类”这个词。ECMAScript 定义了“对象定义”，逻辑上等价于其他程序设计语言中的类。

对于无参的构造函数,\(\)不是必需的

```js
var o = new Object;
```

Number对象

* toFixed\(\)

```js
var oNumberObject = new Number(68)
alert(oNumberObject.toFixed(2));  //输出 "68.00"
```

* toExponential\(\) 

```js
var oNumberObject = new Number(68);
alert(oNumberObject.toExponential(1));  //输出 "6.8e+1"
```

> 指定输出的小数的位数

String对象

charAt\(\) 方法返回的是包含指定位置处的字符的字符串：

```js
var oStringObject = new String("hello world");
alert(oStringObject.charAt(1));    //输出 "e"
```

charCodeAt\(\) 得到的是字符的代码

indexOf\(\) 方法是从字符串的开头（位置 0）开始检索字符串，而 lastIndexOf\(\) 方法则是从字符串的结尾开始检索子串。



###### typeOf\(\) 和 instanceOf\(\)

使用 typeof 运算符时采用**引用类型**存储值会出现一个问题，无论引用的是什么类型的对象，它都返回 "object"。

```js
var oStringObject = new String("hello world");
alert(oStringObject instanceof String);    //输出 "true"
```

> 变量 oStringObject 是否为 String 对象的实例？



