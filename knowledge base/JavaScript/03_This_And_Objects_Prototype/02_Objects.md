# Syntax

Syntax come in two forms:

- declarative (literal):

```
var myObj = {
 key: value
 // ...
};
```

- constructed form:

```
var myObj = new Object();
myObj.key = value;
```


# Built-in Objects

There are several built-in objects.

When you create a new string like `"wow"` its is not an object. But when you want to call `length` property on the string it has to be an object. 

Luckily, the language's engine automatically coerces a string primitive to an object when it is necessary.

The same sort of coercion happens for `Number` ans `Boolean`.

`null` and `undefined` has not object wrapper form. 

By contrast, `Date` can be used only as an object. 

`Objects`, `Arrays`, `Functions` and `RegExps` are objects regardless of what the form is used.


## Properties

In object property name is always a string or a symbol. But symbol should be exactly the same.

