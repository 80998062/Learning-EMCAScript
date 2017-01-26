## 变量

ECMAScript 的解释程序遇到未声明过的标识符时,用该变量名创建一个**全局变量**,并将其初始化为指定的值

与 Java 不同,ECMAScript 中的变量并_不一定要初始化._因此,下面这一行代码也是有效的:

```js
var test = "hi";
alert(test);   
test = 55;
alert(test);
```

> 但是使用变量时,好的编程习惯是始终存放相同的类型



