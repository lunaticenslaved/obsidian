### Binding rules

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

### Rules order

From the least strong to the most strong:

1. Default
2. Implicit
3. Explicit
4. new

1. If the function is called with `new` binding the `this` will be a newly constructed object. (new binding)

	`var bar = new foo()`

2. If the function is called with `call` or `apply` then `this` will be the provided object. (explicit binding)

	`var bar = foo.call( obj2 )`

3. If the function is called with context then `this` will be that context object. (implicit binding)

	`var bar = obj1.foo()`

4. Otherwise, default the `this`. (default binding)
