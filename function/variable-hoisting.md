## 变量提升

[问题链接](http://stackoverflow.com/questions/3725546/variable-hoisting/3725763#3725763)

## 变量对象和活动对象

调用一个函数时,一个新的执行上下文会被创建,可以被分为两个阶段:

* 创建阶段:

在这个阶段中，执行上下文会分别**创建变量对象**，**建立作用域链**，以及**确定this的指向**

* 代码执行阶段:

创建完成之后，就会开始执行代码，这个时候，会完成变量赋值，函数引用，以及执行其他代码。

![](http://upload-images.jianshu.io/upload_images/599584-7d131cfe82a20d37.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

变量对象的创建，依次经历了以下几个过程。

* **建立arguments对象**。检查当前上下文中的参数，建立该对象下的属性与属性值。

* 检查当前上下文的函数声明，也就是使用function关键字声明的函数。在变量对象中以函数名建立一个属性，属性值为指向该函数所在内存地址的引用。**如果函数名的属性已经存在，那么该属性将会被新的引用所覆盖。**

* 检查当前上下文中的变量声明，每找到一个变量声明，就在变量对象中以变量名建立一个属性，属性值为undefined。**如果该变量名的属性已经存在，为了防止同名的函数被修改为undefined，则会直接跳过，原属性值不会被修改**。

举个🌰:

```js
function test() {
    var foo;

    foo = 20;

    console.log(foo);

    function foo() {

    }

    console.log(foo);

}

test();
```

这个时候输出的结果是 **20,20**

那么是不是可以这么认为:`function foo() {}`相当于`var foo ,`

都是声明,声明在变量已经被赋值的情况下会被跳过

**然而赋值可以覆盖:**

```js
function test() {
    var foo;

    foo = 20;

    console.log(foo);

    foo = function () {

    }

    console.log(foo);
}

test();
```

输出结果:

```js
20
[Function: foo]
```

然后结合这个可以看出:

```js
function test() {
    function foo() {

    }

    var foo;

    console.log(foo);

    foo = 20;

    console.log(foo);
}

test();

// 输出:
// [Function: foo]
// 20
```

这样可以看出,同样是声明,`Function`的优先级要高于`undefined`

> 前提是在变量创建阶段

未进入执行阶段之前，变量对象中的属性都不能访问！但是进入执行阶段之后，变量对象转变为了活动对象，里面的属性都能被访问了，然后开始进行执行阶段的操作。

```js
// 创建过程
testEC = {
    // 变量对象
    VO: {},
    scopeChain: {},
    this: {}
}

// 因为本文暂时不详细解释作用域链和this，所以把变量对象专门提出来说明

// VO 为 Variable Object的缩写，即变量对象
VO = {
    arguments: {...},
    foo: <foo reference>  // 表示foo的地址引用
    a: undefined
}
```

举个🌰:

```js
function test() {
    console.log(foo);
    console.log(bar);

    var foo = 'Hello';
    console.log(foo);
    var bar = function () {
        return 'world';
    }

    function foo() {
        return 'hello';
    }
}

test();
```

**Alternatively:**

```js
function test() {
    var foo;
    var bar;
    function foo() {
        return 'hello';
    }
    console.log(foo);
    console.log(bar);

    foo = 'Hello';
    console.log(foo);
    bar = function () {
        return 'world';
    }   
}

test();
```

```js
function test() {
    var foo;

    foo = 20;

    function foo() {

    }

    var foo;

    console.log(foo);
}

test(); // 输出20
```

由上图可以看到,当一个变量已经被赋值的时候,再次声明它将会被跳过

而`function foo()`也是一个声明

而如果没有被赋值,再次声明就是有效的

举个🌰:

```js
function test() {
    var foo;

    function foo() {

    }

    console.log(foo);
}

test();  // 输出[Function: foo]
```

## 全局上下文的变量对象

以浏览器中为例，全局对象为`window`。



---

函数声明会被





