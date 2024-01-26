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