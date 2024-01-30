Closures happen as s result of writing code based on lexical scope.

**Closure is when a function is able to remember and access its lexical scope even when the function is executed outside of its lexical scope.**


## Modules

#### Revealing module pattern

```
function CoolModule() {
	var something = "cool";
	var another = [1, 2, 3];
	
	function doSomething() {
		console.log( something );
	}
	function doAnother() {
		console.log( another.join( " ! " ) );
	}
 
	return {
		 doSomething: doSomething,
		 doAnother: doAnother
	};
}

var foo = CoolModule();
foo.doSomething(); // cool
foo.doAnother(); // 1 ! 2 ! 3
```


#### SIngleton revealing module pattern

```
var foo = (function CoolModule() {
	var something = "cool";
	var another = [1, 2, 3];
	
	function doSomething() {
	console.log( something );
	}

	function doAnother() {
		console.log( another.join( " ! " ) );
	}
	
	return {
		doSomething: doSomething,
		doAnother: doAnother
	};
})();

foo.doSomething(); // cool
foo.doAnother(); // 1 ! 2 ! 3
```


## Dynamic Scope

As was written the key characteristic of lexical scope is that it is defined at author time, when the code is written.

In opposite to lexical scope dynamic one is not defined by author. It is defined at execution time by where the function is called from.

The key contrast: lexical scope is write-time, while dynamic scope is runtime.