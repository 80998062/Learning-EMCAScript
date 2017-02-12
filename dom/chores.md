## innerHTML innerText

innerHTML是指某个网页元素内部的代码,而innerTEXT是指某个网页元素的文本内容.

举个🌰:

```js
<div name="abc"><b>测试</b></div>

document.all("abc").innerHTML // <b>测试</b>

document.all("abc").innerTEXT // 测试
```





```js
<div id="t"><div>lions,
tigers</div><div style="visibility:hidden">and bears</div></div>
```

* innerText : `"lions, tigers"`

* textContent: `"lions,\ntigersand bears"`



