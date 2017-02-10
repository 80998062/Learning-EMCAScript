因为函数也是对象,所以可以下面这个函数可以作为Car对象的构造函数

```js
function Car(sColor,iDoors,iMpg) {
  this.color = sColor;
  this.doors = iDoors;
  this.mpg = iMpg;
  this.showColor = function() {
    alert(this.color);
  };
}

var oCar1 = new Car("red",4,23);
var oCar2 = new Car("blue",3,25);
```

> 我靠好酷炫,一切皆对象吗



但是上面的构造方法会造成浪费,每次initialization都会生成一个新的`showColor()`方法,无法复用

所以有:

### 原型方式

```js
function Car() {
}

Car.prototype.color = "blue";
Car.prototype.doors = 4;
Car.prototype.mpg = 25;
Car.prototype.showColor = function() {
  alert(this.color);
};

var oCar1 = new Car();
var oCar2 = new Car();
```

所有 Car 实例存放的都是指向一个` showColor()` 函数的指针。从语义上讲，所有属性看起来都属于一个对象.

> 为什么, 属性不应该指向不同的实例吗?



