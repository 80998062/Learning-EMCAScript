## 字符串拼接

一般:

```js
var str = "hello ";
str += "world";
```

**Alternatively:**

```js
var arr = new Array();
arr[0] = "hello ";
arr[1] = "world";
var str = arr.join("");
```

**StringBuffer:**

```js
function StringBuffer () {
  this._strings_ = new Array();
}

StringBuffer.prototype.append = function(str) {
  this._strings_.push(str);
};

StringBuffer.prototype.toString = function() {
  return this._strings_.join("");
};
```

```js
var buffer = new StringBuffer ();
buffer.append("hello ");
buffer.append("world");
var result = buffer.toString();
```



