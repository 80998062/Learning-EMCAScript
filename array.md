## 数组下标

> Array是从Object那里继承下。它具备Object所有的功能和特性。

```js
新建： var  object  =   new  Object();  
增加： object[strIndex ]  =  value; (strIndex 为string)  
删除： delete  object[strIndex ];  
遍历： for  (  var  strObjIndex  in  object ) object[strObjIndex ]; 
```

举个🌰:

```js
var obj = new Object();  
obj["first"] = "my";  
obj["second"] = "name";  
obj["third"] = "is";  
obj["fourth"] = "chenssy";
```

因为Array继承Object，那么Array也是可以用字符串作为数组下标的：

```js
var array = new Array();  
array["first"] = "my";  
array["second"] = "name";  
array["third"] = "is";  
array["fourth"] = "chenssy"; 
```



