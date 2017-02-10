## arguments

在函数代码中，使用特殊对象 arguments，开发者_无需明确指出参数名_，就能访问它们。

因此,ES中的重载函数可以这样写:

```js
function doAdd() {
  if(arguments.length == 1) {
    alert(arguments[0] + 5);
  } else if(arguments.length == 2) {
    alert(arguments[0] + arguments[1]);
  }
}

doAdd(10);    //输出 "15"
doAdd(40, 20);    //输出 "60"
```

> 所以ES是没有重载这个概念的吗?
>
> 注释：与其他程序设计语言不同，ECMAScript **不会验证传递给函数的参数个数是否等于函数定义的参数个数**。开发者定义的函数都可以接受任意个数的参数（根据 Netscape 的文档，最多可接受 **255** 个），而不会引发任何错误。任何遗漏的参数都会以 **undefined** 传递给函数，多余的函数将**忽略**。



### 按值传递和按引用传递





### 动态原型方法

```js
function Car(sColor,iDoors,iMpg) {
  this.color = sColor;
  this.doors = iDoors;
  this.mpg = iMpg;
  this.drivers = new Array("Mike","John");
  
  if (typeof Car._initialized == "undefined") {
    Car.prototype.showColor = function() {
      alert(this.color);
    };
	
    Car._initialized = true;
  }
}
```

在构造函数内定义**非函数属性**，而函数属性则利用**原型属性定义**

> 总之原型属性是类似singleton的东西





