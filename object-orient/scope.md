## 对象作用域

#### ECMAScript 只有公用作用域





由于缺少私有作用域，开发者确定了一个规约，说明哪些属性和方法应该被看做私有的。这种规约规定在属性前后加下划线：

```
obj._color_ = "blue";
```

### 静态作用域

严格来说，ECMAScript 并没有静态作用域。

### 关键词this

```js
var oCar = new Object;
oCar.color = "red";
oCar.showColor = function() {
  alert(this.color);
};

oCar.showColor();		//输出 "red"
```



