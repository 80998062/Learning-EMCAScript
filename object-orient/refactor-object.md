## 修改对象

`prototype`** 属性不仅可以定义构造函数的属性和方法，还可以为本地对象添加属性和方法。**

举个🌰:

```js
Number.prototype.toHexString = function() {
  return this.toString(16);
};
```

**重命名已有方法:**

可以给 Array 类添加两个方法 enqueue\(\) 和 dequeue\(\)，只让它们反复调用已有的 push\(\) 和 shift\(\) 方法即可：

```js
Array.prototype.enqueue = function(vItem) {
  this.push(vItem);
};

Array.prototype.dequeue = function() {
  return this.shift();
};
```

**重定义已有方法:**

```js
Function.prototype.toString = function(){
    return "Function code hidden";
};

function sayHi(){
    alert("Hi");
}

console.log(sayHi.toString());
```



> `toString() `指向的原始函数将被无用存储单元回收程序回收，因为它被完全废弃了。
>
> **没有能够恢复原始函数的方法**

所以在覆盖原始方法前，比较安全的做法是**存储它的指针**，以便以后的使用。

有时你甚至可能在新方法中调用原始方法：

```js
Function.prototype.originalToString = Function.prototype.toString;

Function.prototype.toString = function(){
  if (this.originalToString().length > 100) {
      return "Function too long to display.";
  } else {
    return this.originalToString();
  }    
};
```

**添加方法:**

```js
Array.prototype.indexOf = function (vItem) {
  for (var i=0; i<this.length; i++) {
    if (vItem == this[i]) {
      return i;
    }
  }

  return -1;
}
```

> 对 Object 对象做任何改变，都会反应在**所有**本地对象上。

```js
Object.prototype.showValue = function(){
    alter(this.valueOf());
};

var str = "hello";
var iNum = 24;
str.showValue();  // print "hello"
iNum.showValue(); // print "24"
```



