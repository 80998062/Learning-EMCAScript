## 继承机制

所有开发者定义的类都可作为基类。

> 出于安全原因，**本地类**和**宿主类**不能作为基类



### 对象冒充object masquerading

**基类:**

```js
function ClassA(sColor) {
    this.color = sColor;
    this.sayColor = function () {
        console.log(this.color)
    };
}
```

**继承:**

```js
function ClassB(sColor) {
    this.newMethod = ClassA;
    this.newMethod(sColor);
    delete this.newMethod;
}
```

把 ClassA 作为常规函数来建立继承机制，而不是作为构造函数。

在这段代码中，为 ClassA 赋予了方法 newMethod（请记住，**函数名只是指向它的指针**）。然后调用该方法，传递给它的是 ClassB 构造函数的参数 sColor。**最后一行代码删除了对 ClassA 的引用**，这样以后就不能再调用它。



**重写:**

```js
function ClassC(sColor, sName) {
    this.newMethod = ClassA;
    this.newMethod(sColor);
    delete this.newMethod;

    this.name = sName;
    this.sayName = function () {
        console.log(this.name)
    };
}
```

所有新属性和新方法都**必须**在删除了新方法的代码行后定义。否则，可能会覆盖超类的相关属性和方法：



**对象冒充也可以实现多重继承:**

举个🌰:

```js
unction ClassZ() {
    this.newMethod = ClassX;
    this.newMethod();
    delete this.newMethod;

    this.newMethod = ClassY;
    this.newMethod();
    delete this.newMethod;
}
```

> 如果存在两个类 ClassX 和 ClassY 具有同名的属性或方法，ClassY 具有高优先级。



ECMAScript 的第三版为 **Function** 对象加入了两个方法，即 `call()` 和 `apply()`。



