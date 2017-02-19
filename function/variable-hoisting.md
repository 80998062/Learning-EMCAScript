# Variables Are Hoisted

[问题链接](http://stackoverflow.com/questions/3725546/variable-hoisting/3725763#3725763)

Keys:

- *hoisted declaration*
- *assigment stays put*
- *function declaration prior to variable declaration*



举个🌰:

```javascript
// Function声明会被提升至最上面
function a() {
    function foo() {
    }
    var foo;  // (1) 变量声明在后
    console.log(foo); // (2) 输出 [Function: foo] 
}

function b() {
    var bar;
    function bar() {
    }
    console.log(bar);
}

a();
b();

// output:
[Function: foo] 
[Function: bar]
```





## 变量对象和活动对象

调用一个函数时,一个新的执行上下文会被创建,可以被分为两个阶段:

* 创建阶段:

在这个阶段中，执行上下文会分别**创建变量对象**，**建立作用域链**，以及**确定this的指向**

* 代码执行阶段:

创建完成之后，就会开始执行代码，这个时候，会完成变量赋值，函数引用，以及执行其他代码。

## 全局上下文的变量对象

以浏览器中为例，全局对象为`window`。





