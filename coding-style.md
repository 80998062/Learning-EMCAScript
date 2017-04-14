# 编程风格

* `let`取代`var`



* 字符串

静态字符串一律使用单引号或反引号，不使用双引号。动态字符串使用反引号。



```js
// bad
const a = "foobar";
const b = 'foo' + a + 'bar';

// acceptable
const c = `foobar`;

// good
const a = 'foobar';
const b = `foo${a}bar`;
const c = 'foobar';
```

* 解构赋值

  














