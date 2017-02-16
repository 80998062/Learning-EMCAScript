## 闭包

当一个函数可以记住并访问所在的作用域（全局作用域除外），并在定义该函数的作用域之外执行时，该函数就可以称之为一个闭包

> 简单来说，**假设函数A在函数B的内部进行定义了，并在函数B的作用域之外执行**（不管是上层作用域，下层作用域，还有其他作用域），那么A就是一个闭包。

```js
var fn = null;
function foo() {
    var a = 2;
    function innnerFoo() { 
        console.log(a);
    }
    fn = innnerFoo; // 将 innnerFoo的引用，赋值给全局变量中的fn
}

function bar() {
    fn(); // 此处的保留的innerFoo的引用
}

foo();
bar(); // 2
```

> 这里我们可以称fn为闭包,我们在函数bar的执行环境中访问到了函数foo的a变量

那么这样算不算是一个闭包?

```js
var fn;

function foo() {
    var a = 2;

    function innerFoo() {
        console.log(a);
    }

    fn = innerFoo;
}

console.log(a); // 报错:ReferenceError: a is not defined

foo();
fn(); // 输出: 2
```

应该也算吧,直接`log(a)`会报错

```js
var fn = null;
function foo() {
    var a = 2;

    function innnerFoo() {
        console.log(c); // 在这里，试图访问函数bar中的c变量，会抛出错误
        console.log(a);
    }

    fn = innnerFoo; // 将 innnerFoo的引用，赋值给全局变量中的fn
}

function bar() {
    var c = 100;
    fn(); // 此处的保留的innerFoo的引用
}

foo();
bar();
```

不能再闭包fn中试图访问该变量c

> 在闭包中，能访问到的变量，仍然是作用域链上能够查询到的变量。

另外一个🌰:

```js
function test() {
    function bar (str) {
        console.log(str);
    }

    function foo (fn, string) {
        fn(string);
    }

    foo(bar, 'this is closure');
}

test();
```

根据定义,我们很容易看出`bar()`是一个闭包

测试题:

利用闭包，修改下面的代码，让循环输出的结果依次为1， 2， 3， 4， 5

```js
for (var i=1; i<=5; i++) { 
    setTimeout( function timer() {
        console.log(i);
    }, i*1000 );
}
```

这样吗?

```js
for (var i = 1; i <= 5; i++) {

    function fn(a) {
        console.log(a);
    }

    function timer(x) {
        fn(x);
    }

    setTimeout(timer, i * 1000, i);
}
```

> 感觉好丑陋...



或者可以这样?

```js
for (var i = 1; i <= 5; i++) {

    var timer = function t(x) {
        return function () {
            console.log(x);
        }
    }(i);

    setTimeout(timer, i * 1000, i);
}
```



