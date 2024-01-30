There are two main scope models: Lexical Scope and Dynamic Scope.


### Lexical Scope

The first phase of standard compiler is called lexing. So the scopes defined in that stage is called lexical scopes.

**The lexing process examines a string of source code characters and assigns semantic meaning to the tokens as a result of some stateful parsing.**

**Lexical scope is the set of rules about how the engine can look up a variable and where it will find it.**
**The key characteristic of lexical scope is that it is defined at author time, when the**
**code is written.**

![[Pasted image 20240124232618.png]]


### Look-ups

When Engine searches for some variable it asks Scope find the first match.

**No matter where a function is invoked from, or how it is invoked. Its lexical scope is only defined by where the function is declared.**



### Cheating Lexical

There are two ways to update lexical scope it runtime. **Both of them are bad practices and lead to poorer perfomance.**

JS Engine has pretty much of scope optimizations. But using these cheating Engine suppose that scope can be modified at any time so no point of making optimizations what leads to poorer perfomance.

#### eval

```
function foo(str) { 
	"use strict"; 
	eval( str ); 
	console.log( a ); // ReferenceError: a is not defined 
} 

foo( "var a = 2" );
```


#### with

```
function foo(obj) { 
	with (obj) {
		a = 2; 
	} 
} 

var o1 = { a: 3 }; 
var o2 = { b: 3 }; 

foo( o1 ); console.log( o1.a ); // 2 

foo( o2 ); console.log( o2.a ); // undefined 

console.log( a ); // 2—Oops, leaked global!
```


