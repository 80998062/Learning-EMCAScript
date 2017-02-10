## HTML DOM

**文档对象模型**\(**Document Object Model**\)

![](http://www.w3school.com.cn/i/ct_htmltree.gif)

### 查找HTML元素

* id
* 标签名
* 类名



```js
var x = document.getElementById('intro');
```



```js
var y = x.getElementByTagName('p');
```



* 直接向html输出流写内容

```js
document.write(Date())
```

> 绝不要使用在文档**加载之后**使用 document.write\(\)。这会覆盖该文档。



> 同理,JavaScript中函数不要有返回值,也会覆盖整个文档



* 改变 HTML 元素的内容

```js
document.getElementById(id).innerHTML = new HTML
```

> innerHTML到底指的是:
>
> 标签之内的内容吗?



### 改变HTML元素的属性







