`This` is a runtime binding. 

`This` is contextual based on the conditions of the function's invocation. `this` binding has nothing to do with where a function was declared, but instead everything to do with the manner in which the function is invoked. 

When a function is invoked, an activation record called context, is created. This context contains information about arguments and other. One of parameters of the context is `this` reference.


## Call-site

A call-site is a place where a function is called from.


## Binding rules

#### Default Binding

To take this engine examines where the function is called from and takes current `this`. If the function is called with a plain, undecorated function reference then `this` will be assigned with global object if the code not runs in strict mode. If true, then global object will not be assigned as `this`.


#### Implicit Binding

If there is a function object as context reference then this object should be used as `this`.

```
function foo() { 
	console.log( this.a ); 
} 

var obj = { a: 2, foo: foo }; 

obj.foo(); // 2
```

There can be lost of `this`.

```
function foo() {
 console.log( this.a );
}

var obj = {
 a: 2,
 foo: foo
};

var a = "oops, global"; // `a` also property on global object

setTimeout( obj.foo, 100 ); // "oops, global"
```


#### Explicit Binding

If you want to use a particular object for `this` binding use `call`, `apply` or `bind` function methods.


#### `new` Binding

You can use `function` as class constructor but it is not a constructor like any object-oriented languages have. Basically there's no such thing as constructor function, but rather constructor call of function:

```
something = new MyClass(..);
```

When function is called with the `new` keyword the following steps occur:

1. A brand new object created.
2. `[[Prototype]]` is linked to this object.
3. This object is set as `this` for the function.
4. Unless the function returns another object, the function returns the newly constructed object.
```
function foo(a) { 
	this.a = a;
} 

var bar = new foo( 2 ); 

console.log( bar.a ); // 2
```

By calling `foo(..)` with `new` in front of it, we’ve constructed a new object and set that new object as the `this` for the call of `foo(..)`. So `new` is the final way that a function call’s `this` can be bound. We’ll call this **new binding**.

## Rules order

From the least strong to the most strong:

1. Default
2. Implicit
3. Explicit
4. new

1. If the function is called with `new` binding the `this` will be a newly constructed object. (new binding)

	`var bar = new foo()`

2. If the function is called with `call`, `apply`, `bind` then `this` will be the provided object. (explicit binding)

	`var bar = foo.call( obj2 )`

3. If the function is called with a context object owning the call then `this` will be that context object. (implicit binding)

	`var bar = obj1.foo()`

4. Otherwise, default the `this` - `undefined` in strcit mode, `global` object otherwise. (default binding)


## Binding Exeptions

### Ignored this

When you call `call` or `apply` with `null` or `undefined` as `this` that value will be ignored and default binding will be applied.

```
function foo() {
 console.log( this.a );
}

var a = 2;

foo.call( null ); // 2
```

Such a pitfall can lead to a variety of bugs that are very difficult to diagnose and track down.

To prevent this behavior you can explicitly create a new object to use it as `this`.

### Indirection

Another thing to be aware of is that you can (intentionally or not!) create “indirect references” to functions, and in those cases, when that function reference is invoked, the default binding rule also applies. One of the most common ways that indirect references occur is from an assignment:

```
function foo() {
 console.log( this.a );
}
var a = 2;
var o = { a: 3, foo: foo };
var p = { a: 4 };
o.foo(); // 3
(p.foo = o.foo)(); // 2
```


## Arrow functions

Arrow functions was introduced in ES6. The do not create their own `this` but uses the context that is found in its lexical scope. 

Lexical binding of arrows function cannot be overwritten even with `new`.