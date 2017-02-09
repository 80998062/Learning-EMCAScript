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



