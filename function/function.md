## Function对象

**ECMAScript 的函数实际上是功能完整的对象。**



用Function类可以直接创建函数:

```js
var function_name = new function(arg1, arg2, ..., argN, function_body)
```

> 在上面的形式中，每个**args**都是一个参数，最后一个参数是**函数主体**（要执行的代码）。
>
> 这些参数必须是**字符串**呢!

举个🌰:

```js
function sayHi(sName, sMessage) {
    alert("Hello" + sName + sMessage);
}
```

**Equiavalently:**

```js
// 不要忘记转义和分号之类的东西!
var sayHi = new Function("sName","sMessage","alert(\"Hello\" + sName + sMessage);");
```

> 虽然由于**字符串**的关系，这种形式写起来有些困难，但有助于理解函数只不过是一种引用类型，它们的行为与用** Function** 类明确创建的函数行为是相同的。



所以像这样重写一个函数,并不是重载,而相当于重新new了一个Function对象:

```js
function doAdd(iNum) {
  alert(iNum + 20);
}

function doAdd(iNum) {
  alert(iNum + 10);
}

doAdd(10);	//输出 "20"
```

**Alternatively:**

```js
var doAdd = new Function("iNum", "alert(iNum + 10)");
var alsodoAdd = doAdd;
doAdd(10);	//输出 "20"
alsodoAdd(10);	//输出 "20"
```



### 函数也可以作为参数

举个🌰:

```js
function callAnotherFunc(fnFunction, vArgument) {
  fnFunction(vArgument);
}

var doAdd = new Function("iNum", "alert(iNum + 10)");

callAnotherFunc(doAdd, 10);	//输出 "20"
```

### length属性

```js
function doAdd(iNum) {
  alert(iNum + 10);
}

function sayHi() {
  alert("Hi");
}

alert(doAdd.length);	//输出 "1"
alert(sayHi.length);	//输出 "0"
```

> 属性 length 声明了函数**期望**的参数个数





### toString方法

Function 对象也有与所有对象共享的 `valueOf()` 方法和 `toString()` 方法。这两个方法返回的都是函数的**源代码**，在调试时尤其有用。

举个🌰:

```js
function doAdd(iNum) {
  alert(iNum + 10);
}

document.write(doAdd.toString());
```

**print:**

`function doAdd(iNum) { alert(iNum + 10); }`

