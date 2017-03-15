# const and let

## 暂时性死区

**Temporal Dead Zone**\(_TDZ_

```js
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```

变量“绑定”（binding）某个块级作用域，不再受外部的影响。

**TDZ**也意味着`typeof`不再是一个百分之百安全的操作

```js
typeof x; // ReferenceError
let x;
```

## 块级作用域

```js
function f1() {
  let n = 5;
  if (true) {
    let n = 10;
  }
  console.log(n); // 5
}
```

块级作用域的出现，实际上使得获得广泛应用的立即执行函数表达式（_IIFE_）不再必要了。

> 避免在块级作用域里面声明函数

## const

暂存性死区:只能留在声明后使用,不存在变量提升\(类似`final`

## let

ES6新增了`let`命令，用来声明变量。它的用法类似于`var`，但是所声明的变量，只在`let`命令所在的代码块内有效。

🌰

```js
for (let i = 0; i < 10; i++) {}

console.log(i);
//ReferenceError: i is not defined
```

此外,`for`循环还有一个特别之处，就是循环语句部分是一个父作用域，而循环体内部是一个单独的子作用域。

```js
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);
}
// abc
// abc
// abc
```



