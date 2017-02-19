# Closures

Each `function` stays connected to the variables of the functions that surround it, **even after it** **leaves the scope in which it was created**

举个🌰:

```js
function fn() {
    var a = 2;
    return function innerFoo() { // (1)
        console.log(a);
    }
}

console.log(a); // 报错:ReferenceError: a is not defined

var f = fn(); // 输出: 2

f();
```

*(1)*中的的`innerFoo()`函数在全局的*scope*中被执行,离开创建它的上下文`fn()`,依然保持着它原来的*scope*中的变量`a`

我们把`innerFoo()`称为一个**闭包**(*Closure*):

So,a *closure* is a *function* **plus the connection to** the *variables* of its surrounding *scopes*.

再举个🌰(*一个不明显的闭包*):

```js
function test() {
    var s = ' is closure';

    function bar(str) {
      	var x = 'variable in bar()';
        console.log(str + s);
    }

    function foo(fn, string) {
        fn(string);
      	console.log(x); // (1) ReferenceError: x is not defined
    }

    foo(bar, 'bar()');
}

console.log(s); //(1) ReferenceError: s is not defined

test(); //(3) output: bar() is closure
```

- 根据定义,我们很容易看出`bar()`是一个闭包


- *(1)* 说明只能是内部的函数保存外面变量的*snapshot*

然而,只有函数才有*scope*,`if{}`语句没有

```javascript
function foo() {
    var x = -512;
    if (x < 0) {  // (1)
        var tmp = -x;
        ...
    }
    console.log(tmp);  // 512
}
```

# The IIFE Pattern: Introducing a New Scope

## concept

*IIFE*模式([immediately invoked function expression](http://bit.ly/i-ife), 念作*"iffy"*)

写法:

```javascript
(function () {  // open IIFE
    var tmp = ...;  // not a global variable
}());  // close IIFE
```

- *function called immediately after you define it*
- *a new scope produced*
- *preventing `tmp` from becoming global*

> 问题: 难道在`function`的变量会提升至global,
>
> `function`不是有*scope*吗?

🌰:

```javascript
function f() {
    var a = 2; // 哪里提升到global了?
}

f();

console.log(a); // ReferenceError: a is not defined
```



🌰: *inadvertent sharing via closures*

**Closures** keep their connections to outer variables, which is sometimes not what you want:

```javascript
var result = [];
for (var i=0; i < 5; i++) {
    result.push(function () { return i });  // (1)
}
console.log(result[1]()); // 5 (not 1)
console.log(result[3]()); // 5 (not 3)
```

> 这样是不是说`for()`语句是有*scope*的,所以`function()`是一个闭包了

如果你想要`i`的*snapshot*(快照),你可以用*IIFE*:

```javascript
for(var i = 0;i < 5;i++){
  (function(){
    var j = i; // create a snapshot of current i
    result.push(function(){	return j;});
  }());
}
```



🌰:(*in the then part of an `if` statement*)

```javascript
function f() {
    if (condition) {
        var tmp = ...;
        ...
    }
    // tmp still exists here
    // => not what we want
}
```

so you can **immediately** to invoke the `function` to simulate a block scoping:

- *to avoid "leak out"*

```javascript
function f() {
    if (condition) {
        (function () {  // open block
            var tmp = ...;
            ...
        }());  // close block
    }
}
```

> just for didactic reason

### notes about *IIFE*

1. *it is immediately invoked*
2. *it must be an expression(a function within an open parenthesis :圆括号)*
3. *The trailing semicolon: 分号 is required*
4. *it incurs costs,so it rarely make sense to be used in an `if` statement*

## Prefix Operators

You can also enforce the expression context via prefix operators.

🌰:

```javascript
!function () { // open IIFE
    // inside IIFE
}(); // close IIFE
```

```javascript
void function () { // open IIFE
    // inside IIFE
}(); // close IIFE
```

The advantage of using prefix operators is that forgetting the terminating semicolon does not cause trouble.

## Variation: Already Inside Expression Context

```javascript
var File = function () { // open IIFE
    var UNTITLED = 'Untitled';
    function File(name) {
        this.name = name || UNTITLED;
    }
    return File;
}(); // close IIFE
```

In the preceding example,on one hand, there is the function that is only directly accessible inside the IIFE. On the other hand, there is the variable that is declared in the first line. 

## An IIFE with Parameters

```javascript
var x = 23;
(function (twice) {
    console.log(twice);
}(x * 2));
```

This is similar to:

```javascript
var x = 23;
(function () {
    var twice = x * 2;
    console.log(twice);
}());
```



## Best Practice

### Avoid Creating Global Variables

- *all of the JavaScript on a web page shares the same global variables*
- *pieces of software that rely on global variables are subject to side effects*

🌰:

```javascript
<!-- Don’t do this -->
<script>
    // Global scope
    var tmp = generateData();
    processData(tmp);
    persistData(tmp);
</script>
```

The variable `tmp` becomes global, because its declaration is executed in global scope.

> 函数一旦执行,`tmp`的作用域就变成全局了

🌰:

```javascript
<script>
    (function () {  // open IIFE
        // Local scope
        var tmp = generateData();
        processData(tmp);
        persistData(tmp);
    }());  // close IIFE
</script>
```

#### Module Systems Lead to Fewer Globals

Thankfully, module systems (see [Module Systems](http://speakingjs.com/es5/ch31.html#module_systems)) mostly eliminate the problem of global variables,because modules *don’t interface via the global scope* and because each module *has its own scope for module-global variables*.

### Creating fresh environments; avoiding sharing

```javascript
function f() {
    var result = [];
    for (var i=0; i<3; i++) {
        var func = function () {
            return i;
        };
        result.push(func);
    }
    return result;
}
console.log(f()[0]());  // 3
console.log(f()[1]());  // 3
console.log(f()[2]());  // 3
```

**This** is not what we want. To fix things, we need to make a *snapshot* of the index `i` before creating a function that uses it.

🌰:

```javascript
function f() {
    var result = [];
    for (var i = 0; i < 3; i++) {
        (function () { // step1: IIFE
            var index = i; // step2: create snapshot for i
            var func = function () {
                return index;
            }
            result.push(func);
        }());
    }
    return result;
}
console.log(f()[1]());  // 1
```

Note that the example has real-world relevance, because similar scenarios arise when you *add event handlers to **DOM** elements* via `loops`.

### Keeping global data private to all of a constructor

```javascript
var StringBuilder = function () { // open IIFE
    var KEY_BUFFER = '_StringBuilder_buffer_' + uuid.v4();

    function StringBuilder() {
        this[KEY_BUFFER] = [];
    }
    StringBuilder.prototype = {
        // Omitted: methods accessing this[KEY_BUFFER]
    };
    return StringBuilder;
}(); // close IIFE
```

Note that if you are using a module system (see [Chapter 31](http://speakingjs.com/es5/ch31.html)), you can achieve the same effect with cleaner code by *putting the constructor plus methods in a module*.

### Attaching global data to a singleton object

You don’t need a *constructor* to associate an object with private data in an environment. The following example shows how to use an *IIFE* for the same purpose, by wrapping it around a singleton object:

```javascript
var obj = function () {  // open IIFE

    // public
    var self = {
        publicMethod: function (...) {
            privateData = ...;
            privateFunction(...);
        },
        publicData: ...
    };

    // private
    var privateData = ...;
    function privateFunction(...) {
        privateData = ...;
        self.publicData = ...;
        self.publicMethod(...);
    }

    return self;
}(); // close IIFE
```

### Attaching global data to a method

Sometimes you only need *global* data for a **single** method. You can keep it `private` by putting it in the environment of an *IIFE* that you wrap around the method. 

🌰:

```javascript
var obj = {
    method: function () {  // open IIFE

        // method-private data
        var invocCount = 0;

        return function () {
            invocCount++;
            console.log('Invocation #'+invocCount);
            return 'result';
        };
    }()  // close IIFE
};
```

Here is the interaction:

```javascript
> obj.method()
Invocation #1
'result'
> obj.method()
Invocation #2
'result'
```

