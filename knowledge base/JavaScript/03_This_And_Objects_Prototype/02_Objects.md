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


# Properties

In object property name is always a string or a symbol. But symbol should be exactly the same.

Property can be either value or function (method). Technically, method is also a property with the value of function. The function does not belong to the object like classical methods in Object Oriented languages.


# Arrays

Arrays assume numeric indexing which means that values are stored in locations usually called indices.

If you try to add a validly convertible to number property it will be added with index:

```
var myArray = [ "foo", 42, "bar" ];
myArray["3"] = "baz";
myArray.length; // 4
myArray[3]; // "baz"
```


# Property Descriptors

Any property has an object that describes what can be done with the property.

## Writable

The abitity to change the value of a property is controlled by `writable` of the descriptor.

In non-strict mode value not be changed but the program runs on. On strict mode `TypeError` will be thrown.

Writable can be modified to `false` if `true`. But not from `true` to `false`.


## Configurable

If a property is configurable then we can modify it with `Object.defineProperty`. If not, `TypeError` will be thrown. Remember that setting `configurable` to `false` is one-way action. It can be undone!

Non-configurable properties cannot be deleted.

## Enumerable

If `true` then property will be shown in certain object-property enumerations, such as `for ... in`.


## Immutability

## Object constant

With `writable: false` and `configurable: false` you can create a constant as on object property.

## Prevent extensions

If you want to prevent on object from adding new properties use `Object.preventExtensions(..)`.

In non-strict mode a try of extension runs silently but in strict-mode it throws `TypeError`.

## Seal

`Object.seal(..)` takes an existing object and immediately `Object.preventExtendsion` on it. All properties also have `configurable: false`. So you not only cannot add more properties but you cannot also reconfigure and delete existing ones.

## Freeze

`Object.freeze(..)` takes an existing object, invokes `Object.seal` on it and marks all it's properties as `writable: false`. This approach is the highest level of immutability.