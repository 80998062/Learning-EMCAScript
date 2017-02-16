## 函数声明



下面这两个有什么区别...为什么第二个函数名会叫做timer

```js
var timer = function foo() {};

console.log(timer);

// 输出 [Function: foo]
```

```js
var timer = function () {};

console.log(timer);

// 输出 [Function: timer]
```



