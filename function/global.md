# The Global Object

The **global object** can be used to create, read, and change global variables.In global scope, `this` points to it:

```javascript
> var foo = 'hello';
> this.foo  // read global variable
'hello'

> this.bar = 'world';  // create global variable
> bar
'world'
```

## Cross-Platform Considerations

Browsers and **Node.js** have global variables for referring to the global object.

- Browser: `window` as part of **DOM** not as part of **ECMAScript 5**
- **Node.js** contains `global` 

在一个*module*里面,`global`和`this`是不同的

 If you want to access the global object in a *cross-platform* manner, you can use a pattern such as the following:

```javascript
(function (glob){
  // glob points to global object 
}(typeof window !== 'undefined' ? window : global));
```

## Use Cases for window

You can access global variables via `window` ,but the general rule is:
*avoid doing that as much as possible*

### Use case: marking global variables

The prefix `window`:

```javascript
var foo = 123;
(function () {
    console.log(window.foo);  // 123
}());
```

It ceases:终止 to work as soon as you move `foo` from global scope to another surrounding scope: 

```javascript
(function () {
    var foo = 123;
    console.log(window.foo);  // undefined
}());
```

Thus, it is better to refer to `foo` as a variable, not as a property of `window`. 

The custom name prefix such as `_g`

```javascript
var g_foo = 123;
(function () {
    console.log(g_foo);
}());
```

### Use case: built-ins

I prefer not to refer to build-in global variables via `window`

```Javascript
window.isNaN(...)  // no
isNaN(...)  // yes
```

