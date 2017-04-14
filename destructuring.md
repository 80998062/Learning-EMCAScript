# 变量的结构赋值

最基本的用法:

```js
let a = 1;
let b = 2;
let c = 3;
```

现在可以写成:

```js
let [a, b, c] = [1, 2, 3];
```

如果等号的右边不是数组（或者严格地说，不是可遍历的结构\)那么将会报错

```js
// 报错
let [foo] = 1;
let [foo] = false;
let [foo] = NaN;
let [foo] = undefined;
let [foo] = null;
let [foo] = {};
```

上面的语句都会报错，因为等号右边的值，要么转为对象以后不具备 `Iterator` 接口（前五个表达式），要么本身就不具备 `Iterator` 接口（最后一个表达式）。



## 默认值

```js
let [foo = true] = [];
foo // true

let [x, y = 'b'] = ['a']; // x='a', y='b'
let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'

let [x = 1] = [undefined];
x // 1

let [x = 1] = [null];
x // null
```

上面代码中，如果一个数组成员是`null`，默认值就不会生效，因为`null`**!===**`undefined`

默认值可以引用解构赋值的其他变量，但该变量必须已经声明。

```js
let [x = 1, y = x] = [];     // x=1; y=1
let [x = 1, y = x] = [2];    // x=2; y=2
let [x = 1, y = x] = [1, 2]; // x=1; y=2
let [x = y, y = 1] = [];     // ReferenceError
```

```js
let foo;

let {foo} = {foo: 1}; // SyntaxError: Identifier 'foo' has already been declared

console.log(foo);
```

```js
let foo;
({foo} = {foo: 1}); // 成功

let baz;
({bar: baz} = {bar: 1}); // 成功
```

上面代码中，`let`命令下面一行的圆括号是必须的，否则会报错。**因为解析器会将起首的大括号，理解成一个代码块，而不是赋值语句。**

> 这是什么意思???



## 解构嵌套结构的对象

```js
var node = {
  loc: {
    start: {
      line: 1,
      column: 5
    }
  }
};

var { loc: { start: { line }} } = node;
line // 1
loc  // error: loc is undefined
start // error: start is undefined
```

上面代码中，只有`line`是变量，`loc`和`start`都是**模式**，不会被赋值。

### 嵌套赋值

```js
let obj = {};
let arr = [];

({ foo: obj.prop, bar: arr[0] } = { foo: 123, bar: true });

obj // {prop:123}
arr // [true]
```



> JavaScript里面用{}表示的就是对象吗???



其实类似

```js
var { foo, bar } = { foo: "lorem", bar: "ipsum" };
console.log(foo);
// "lorem"
console.log(bar);
// "ipsum"
```

是有一个语法糖的.它本来的形式应该是:

```js
var { foo:foo, bar:bar } = { foo: "lorem", bar: "ipsum" };
```



