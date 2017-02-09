## Scoping

> To fully understand the concept of hoisting,first let's take a necessary detour to understand JavaScript's scoping



举个🌰:

```c
#include <stdio.h>
int main() {
	int x = 1;
	printf("%d, ", x); // 1
	if (1) {
		int x = 2;
		printf("%d, ", x); // 2
	}
	printf("%d\n", x); // 1
}
```

output:

`1,2,1`

C family language:**blocking-level scope**



而在JavaScript中:

```js
var x = 1;
console.log(x); // 1
if (true) {
	var x = 2;
	console.log(x); // 2
}
console.log(x); // 2
```



JavaScript: **function-level scope**

> 比如一个`if`语句,不会创建一个新的**scope**



If you must create** temporary scopes** within a function, do the following:

> 哇塞

```js
function foo() {
	var x = 1;
	if (x) {
		(function () {
			var x = 2;
			// some other code
		}());
	}
	// x is still 1.
}
```



## Declarations, Names, and Hoisting {#declarations_names_and_hoisting}

In JavaScript, a name enters a scope in one of four basic ways:

1. **Language-defined:**
   All scopes are, by default, given the names`this`and`arguments`.
2. **Formal parameters:**
   Functions can have named formal parameters, which are scoped to the body of that function.
3. **Function declarations:**
   These are of the form`function foo() {}`.
4. **Variable declarations:**
   These take the form`var foo;`.

函数和变量声明会被\(hoisting invisible\)提升到它们**所在scope**的顶部

> Function parameters and language-defined names are, obviously, already there.

举个🌰:

```js
function foo() {
	bar();
	var x = 1;
}
```

解释器是这样认为的:

```js
function foo() {
	var x;
	bar();
	x = 1;
}
```

**It turns out that it doesn’t matter whether the line that contains the declaration would ever be executed?**

 The following two functions are equivalent:

```js
function foo() {
	if (false) {
		var x = 1;
	}
	return;
	var y = 1;
}

function foo() {
	var x, y;
	if (false) {
		x = 1;
	}
	return;
	y = 1;
}
```



