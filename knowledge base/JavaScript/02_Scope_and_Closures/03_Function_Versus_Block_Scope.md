### Scope from functions

Inside of function a new scope bubble is created. This scope contains definitions for all local variables no matter where they were declared.


### Hiding in Plain Scope

When a variable or a function is used only in specific place it useful to keep them as close as possible to the place according to the [Principle of Least Privilege](https://en.wikipedia.org/wiki/Principle_of_least_privilege)(// TODO write more about the principle).


### Collisions Avoidance

Another benefit of hiding variable inside of a scope is to avoid of unintended collisions between two different identifiers with the same name but different usage.

#### Global namespace

Many collisions can occur in the global scope because many libraries use global scope to keep their settings and constants.

#### Module management

Use module approach to keep every variable in its place and avoid collisions.


### Functions as Scopes

Function declaration

```
function foo() {
    console.log('a')
}

foo()
```


Function expression

```
(function foo() {
    console.log('a')
})

foo() // throws ReferenceError
```


The key difference is that FE does not pollute the outer scope and can be available only inside its own scope.


### Anonymous vs Named

Function expressions are also used as callback:

```
setTimeout( function(){ console.log("I waited 1 second!"); }, 1000 );
```

FE can not have the name. In this case it is called anonymous function expression. 
But function declaration must have name otherwise JS error will be thrown.

It's better always name you FE at least for code readability reasons. There FE are called inline FE.



### Invoking function expression immediately

You can invoke FE just after declaration. It is called IIFE.


### Block as Scope

New scope is created inside a block.


###  Variables

#### `var`

`var` has function visibility.

#### `let`

`let` was introduced in ES6. In opposite to `var` it has block NOT FUNCTION visibility and not hoisted.

It's especially helpful for loops when using `var i = 0` redefines `i` variable in the same scope.

#### `const`

`const` is pretty much like `let` but it cannot be redefined.



### `var` and `let` difference

`var` is inside function scope. So in nested scopes declaring the same variable with `var` redefines the initial variable whilst with `let` a new variable will be created:

```
var a = 5;
var b = 10;

if (a === 5) {
  let a = 4; // The scope is inside the if-block
  var b = 1; // The scope is inside the function

  console.log(a);  // 4
  console.log(b);  // 1
}

console.log(a); // 5
console.log(b); // 1
```

Also in `for` loops because of `i` variable is redeclared in every iteration:

 - as `var` has function visibility so `i` is declared in the upper scope and will have the same value for all callback:

```
for (var i=1; i<=5; i++) {
 setTimeout( function timer(){
 console.log( i ); // 6 times prints 6
 }, i*1000 );
}
```

- as `let` has block visibility so for every iteration is created new `i` variable with actual value:

```
for (let i=1; i<=5; i++) {
 setTimeout( function timer(){
 console.log( i ); // prints 1...6 - actual value for every iteration
 }, i*1000 );
}
```

### Garbage collecting

Declaring explicit blocks for block-scoped variables is a powerful tool that can help Garbage Collector to delete extra data.



