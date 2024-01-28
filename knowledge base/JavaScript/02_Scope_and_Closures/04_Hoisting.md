The code `var a = 2` is processed in two phases:

1. Compilation: `a` is declared.
2. Executing: `2` is assigned to `a`.

This code prints `undefined` because `var` allows hoisting - moving variable declaration to the top of the code block:

```
console.log( a );

var a = 2;
```

Not everything is hoisted. Function declareations do, but function expressions don't.

### `var`

This variable is hoisted.

### `let` and `const`

ES6 is more strict to this variables they do not allow hoisting.


### Functions First

Functions are hoisted first, then variables.