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


# \[\[Get]]

To get a value of property a \[\[Get]]() operation is performed. The operation does not look just the object for the property. It also looks in prototypes chain. If the property does not found `undefined` will be returned.


# \[\[Put]]

To get a value of property a \[\[Put]] operation is performed. How it behaves differs on whether the property exists or not.

1. If the property exists:

	1. Is the property an accessor descriptor - call setter.
	2. Is the property a data descriptor? Check `writable`:
		1. `true` - set value
		2. `false` - silently fail in non-strict mode and throw `TypeError` in strict-mode.
	3. Otherwise set the property as normal.

2. If the property does not exist the way is more complicated. // TODO: add link


# Getters and Setters

You can define an accessor descriptor with getter and/or setter for property. For it `writable` and `value` settings are ignored.

If the property has getter and no setter so error is silently thrown when assignment occurs.


# Existense