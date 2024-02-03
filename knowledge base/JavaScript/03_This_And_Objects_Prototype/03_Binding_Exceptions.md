
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